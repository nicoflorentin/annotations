https://www.youtube.com/watch?v=pAHPHivDbuE&list=WL&index=54&t=329s&ab_channel=FaztCode
```ts
// counterStore.js

import create from "zustand";

// crea las interfaces de entidad y estado
export interface Post {
  id: number;
  title: string;
  body: string;
}

interface CounterState {
  count: number;
  title: string;
  posts: Post[];
  increment: (value: number) => void;
  getPosts: () => Promise<void>;
  cleanStore: () => void;
  multiply: (value: number) => void;
}

// crea el store usando create de zustand, recibe set y get como argumento
export const useCounterStore = create<CounterState>((set, get) => ({
  title: "Some title",
  count: 10,
  posts: [],
  increment: (value: number) =>
    set((state) => ({ ...state, count: state.count + value })),
  getPosts: async () => {
    const posts = await (
      await fetch("https://jsonplaceholder.typicode.com/posts")
    ).json();
    set((state) => ({ ...state, posts }));
  },
  // El `true` en el método `set` en `cleanStore` asegura que las partes del estado que no han cambiado no causen renders innecesarios, optimizando así el rendimiento.
  cleanStore: () => set({}, true),
  multiply: (value: number) => {
    // const count = get().count
    const { count } = get();
    set({ count: count * value });
  },
}));

```

```tsx
// App.tsx

import { useEffect } from "react";
import shallow from "zustand/shallow";
import { useCounterStore } from "./store/counterStore";

function App() {
  const { count, title, posts } = useCounterStore(
    (state) => ({
      count: state.count,
      title: state.title,
      posts: state.posts,
    }),
    // Solo actualizará el componente si las propiedades que se están desestructurando cambian. Como no se puede comparar objeto con objeto superficialmente, ésta funcion de zustand lo hace posible
    shallow
  );
  const { increment, getPosts, cleanStore, multiply } = useCounterStore();

  useEffect(() => {
    getPosts();
  }, []);
```

