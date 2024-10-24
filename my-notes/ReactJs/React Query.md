https://www.youtube.com/watch?v=1Ytp_M3P6Xc&ab_channel=FaztCode

### Configurar la instancia y el provider de React Query

```tsx
// queryClient.ts
import { QueryClient } from "@tanstack/react-query";
const queryClient = new QueryClient();
export default queryClient;
```

```tsx
// main.tsx
import { QueryClientProvider } from "@tanstack/react-query";
import ReactDOM from "react-dom/client";
import App from "./App";
import queryClient from "./queryClient";

ReactDOM.createRoot(document.getElementById("root") as HTMLElement).render(
  <React.StrictMode>
    <QueryClientProvider client={queryClient}>
      <App />
    </QueryClientProvider>
  </React.StrictMode>
);
```

### Instanciar axios

```ts
// api/github.ts
import axios from "axios";

const api = axios.create({
  baseURL: "https://api.github.com",
});

export default api;
```


### Custom hook

```ts
// hooks/useRepos.ts

import { QueryFunctionContext, useQuery } from "@tanstack/react-query";
import api from "../api/github";
import { Repository } from "./types";

async function fetchRepos(ctx: QueryFunctionContext) {
  const [_, githubUser] = ctx.queryKey;
  const { data } = await api.get<Repository[]>(`/users/${githubUser}/repos`);
  return data;
}

export function useFetchRepositories(githubUser: string) {
  return useQuery(["repos", githubUser], fetchRepos);
}
```

### Store
```ts
import create from "zustand";
import { persist } from "zustand/middleware";

type favoriteRepoState = {
  favoriteReposIds: number[];
  addFavoriteRepo: (id: number) => void;
  removeFavoriteRepo: (id: number) => void;
};

export const useFavoriteReposStore = create(
  persist((set) => ({
    favoriteReposIds: [],
    addFavoriteRepo: (id: number) =>
      set((state) => ({ favoriteReposIds: [...state.favoriteReposIds, id] })),
    removeFavoriteRepo: (id: number) =>
      set((state) => ({
        favoriteReposIds: state.favoriteReposIds.filter(
          (repoId) => repoId !== id
        ),
      })),
  }), {
    name: "favoriteRepos",
  })
);
```
### Consumiendo estado
```tsx
// App.tsx
import Card from "./components/Card";
import { useFetchRepositories } from "./hooks/useRepos";
import { useFavoriteReposStore } from "./store/favoriteRepos";

function App() {
  const { data, isLoading } = useFetchRepositories("fazt");
  const favoriteRepos = useFavoriteReposStore(
    (state) => state.favoriteReposIds
  );

  if (isLoading) return <div>Loading...</div>;

  return (
    <div>
      {data.map((repository) => (
        <Card
          repository={repository}
          key={repository.id}
          isFavorite={favoriteRepos.includes(repository.id)}
        />
      ))}
    </div>
  );
}

export default App;
```

---------------------------


Si ves un refetch que no estás esperando, es probable que sea porque acabas de enfocar la ventana y **React Query está haciendo un refetchOnWindowFocus**, que es una gran característica para la producción
Si el usuario va a una pestaña diferente del navegador, y luego vuelve a tu aplicación, un refetch en segundo plano se activará automáticamente, y los datos en la pantalla se actualizarán si algo ha cambiado en el servidor en el ínterin. Todo esto ocurre sin que se muestre un spinner de carga, y **tu componente no se volverá a renderizar si los datos son los mismos que tienes actualmente en la caché**.

### staleTime
La duración hasta que una consulta pasa de fresca a antigua. Mientras la consulta esté fresca, los datos siempre se leerán de la caché - ¡no se realizará ninguna petición de red! Si la consulta es antigua (que por defecto es: instantáneamente), los datos se seguirán obteniendo de la caché, pero en determinadas circunstancias puede producirse una recuperación en segundo plano.  
### gcTime
La duración hasta que las consultas inactivas sean eliminadas de la caché. Por defecto es de 5 minutos. Las consultas pasan al estado inactivo tan pronto como no hay observadores registrados, es decir, cuando todos los componentes que utilizan esa consulta se han desmontado.

```tsx
import {
  useQuery,
  useMutation,
  useQueryClient,
  QueryClient,
  QueryClientProvider,
} from '@tanstack/react-query'
import { getTodos, postTodo } from '../my-api'

// Create a client
const queryClient = new QueryClient()

function App() {
  return (
    // Provide the client to your App
    <QueryClientProvider client={queryClient}>
      <Todos />
    </QueryClientProvider>
  )
}

function Todos() {
  // Access the client
  const queryClient = useQueryClient()

  // Queries
  const query = useQuery({ queryKey: ['todos'], queryFn: getTodos })

  // Mutations
  const mutation = useMutation({
    mutationFn: postTodo,
    onSuccess: () => {
      // Invalidate and refetch
      queryClient.invalidateQueries({ queryKey: ['todos'] })
    },
  })

  return (
    <div>
      <ul>{query.data?.map((todo) => <li key={todo.id}>{todo.title}</li>)}</ul>

      <button
        onClick={() => {
          mutation.mutate({
            id: Date.now(),
            title: 'Do Laundry',
          })
        }}
      >
        Add Todo
      </button>
    </div>
  )
}

render(<App />, document.getElementById('root'))
```

### Midudev example
https://www.youtube.com/watch?v=WKfVjQUa6nE&ab_channel=midulive
```tsx
import './App.css'
import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query'
import { getComments, type CommentWithId, type Comment, postComment } from './service/comments'
import { FormInput, FormTextArea } from './components/Form'
import { Results } from './components/Results'

function App () {
  const { data, isLoading, error } = useQuery<CommentWithId[]>(
    ['comments'], // <-----
    getComments
  )
  const queryClient = useQueryClient()

  const { mutate, isLoading: isLoadingMutation } = useMutation({
    mutationFn: postComment,
    onMutate: async (newComment) => {
      await queryClient.cancelQueries(['comments'])

      // esto lo hacemos para guardar el estado previo
      // por si tenemos que hacer un rollback
      const previousComments = queryClient.getQueryData(['comments'])

      queryClient.setQueryData(['comments'], (oldData?: Comment[]): Comment[] => {
        const newCommentToAdd = structuredClone(newComment)
        newCommentToAdd.preview = true

        if (oldData == null) return [newCommentToAdd]
        return [...oldData, newCommentToAdd]
      })

      return { previousComments } // -----> context
    },
    onError: (error, variables, context) => {
      console.error(error)
      if (context?.previousComments != null) {
        queryClient.setQueryData(['comments'], context.previousComments)
      }
    },
    onSettled: async () => {
      await queryClient.invalidateQueries({
        queryKey: ['comments']
      })
    }
  })

  const handleSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    if (isLoadingMutation) return

    event.preventDefault()
    // ---> ???
    const data = new FormData(event.currentTarget)
    const message = data.get('message')?.toString() ?? ''
    const title = data.get('title')?.toString() ?? ''

    if (title !== '' && message !== '') {
      mutate({ title, message })
    }
  }

  return (
    <main className='grid h-screen grid-cols-2'>
      <div className='col-span-1 p-8 bg-white'>

        {isLoading && <strong>Cargando...</strong>}
        {error != null && <strong>Algo ha ido mal</strong>}
        <Results data={data} />

      </div>
      <div className='col-span-1 p-8 bg-black'>
        <form className={`${isLoadingMutation ? 'opacity-40' : ''} block max-w-xl px-4 m-auto`} onSubmit={handleSubmit}>

          <FormInput />
          <FormTextArea />

          <button
            disabled={isLoadingMutation}
            type='submit' className='mt-4 px-12 text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm py-2.5 text-center mr-2 mb-2'
          >
            {isLoadingMutation ? 'Enviando comentario...' : 'Enviar comentario'}
          </button>
        </form>
      </div>
    </main>
  )
}

export default App
```

