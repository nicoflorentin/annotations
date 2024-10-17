
### Arquitectura de Flux
VIEW -> ACTION -> DISPATCHER -> STORE -> VIEW

### Redux
Redux es una librería para implementar flux.

#### Action
El estado del store se cambia con **acciones**. Las acciones son objetos que tienen al menos un campo que determina el _tipo_ de acción
```js
{
  type: 'INCREMENT'
}
```

#### Reducer
El impacto de la acción sobre el estado de la aplicación se define mediante un **reducer**. **Es una función a la que se le da el estado actual y una acción como parámetros. _Devuelve_ un nuevo estado.**
```js
const counterReducer = (state = 0, action) => {  
switch (action.type) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    case 'ZERO':
      return 0
    default: // if none of the above matches, code comes here
      return state
  }
}
```

#### Método getState
Puedes **averiguar el estado del store** utilizando el método getState()
```js
const store = createStore(counterReducer)
store.dispatch({ type: 'INCREMENT' })
console.log(store.getState())
```

#### Método subscribe
Se utiliza para **crear funciones callback** que el store llama luego de cambiar su estado.
```js
const store = createStore(counterReducer)

store.subscribe(() => {
  const storeNow = store.getState()
  console.log(storeNow) // cada vez que cambie el estado, se hace log del valor del estado actualizado
})
```

#### Reducer con método concat()
```js
const noteReducer = (state = [], action) => {
  if (action.type === 'NEW_NOTE') {
  // agrega una nota creando un nuevo array con los elementos anteriores mas el elemento pasado como argumento
    return state.concat(action.payload)  }

  return state
}
```

Lo mismo pero con spread operator
```js
const noteReducer = (state = [], action) => {
  switch(action.type) {
    case 'NEW_NOTE':
    // spread operator
      return [...state, action.payload]    case 'TOGGLE_IMPORTANCE':
      // ...
    default:
    return state
  }
}
```

### Action creators
Estas funciones se pasan como argumento al dispatch en reemplazo del objeto de acción
```js
const createNote = (content) => {
  return {
    type: 'NEW_NOTE',
    payload: {
      content,
      important: false,
      id: generateId()
    }
  }
}

const toggleImportanceOf = (id) => {
  return {
    type: 'TOGGLE_IMPORTANCE',
    payload: { id }
  }
}

// se hace dispatch de la acción retornada por la función
store.dispatch(createNote(content))
```


### Combine reducers
```js
const noteReducer = (state = initialState, action) => {
  // ...
}

const filterReducer = (state = 'ALL', action) => {
  switch (action.type) {
    case 'SET_FILTER':
      return action.payload
    default:
      return state
  }
}
```

```js
import { createStore, combineReducers } from 'redux'

import noteReducer from './reducers/noteReducer'
import filterReducer from './reducers/filterReducer'
const reducer = combineReducers({  notes: noteReducer,  filter: filterReducer})

const store = createStore(reducer)

```

### Communicate w/ server
```js
// services/notes.js

const baseUrl = 'http://localhost:3001/notes'

const getAll = async () => {
  const response = await axios.get(baseUrl)
  return response.data
}

const createNew = async (content) => {  
const object = { content, important: false } 
const response = await axios.post(baseUrl, object) 
return response.data
}

export default {
  getAll,
  createNew,
  }
```

```js
// app.jsx
import { useDispatch } from 'react-redux'
import { createNote } from '../reducers/noteReducer'
import noteService from '../services/notes'
const NewNote = (props) => {
  const dispatch = useDispatch()
  
  const addNote = async (event) => {    event.preventDefault()
    const content = event.target.note.value
    event.target.note.value = ''
    const newNote = await noteService.createNew(content)    dispatch(createNote(newNote))  }

  return (
    <form onSubmit={addNote}>
      <input name="note" />
      <button type="submit">add</button>
    </form>
  )
}

export default NewNote
```

### Async actions and Redux Thunk

La async action llama al servicio y se encarga de llamar la action sincrona para modificar el estado

```jsx
import noteService from "../services/notes";

const noteSlice = createSlice({
  name: "notes",
  initialState: [],
  reducers: {
    toggleImportanceOf(state, action) {
    // ...
    },
    appendNote(state, action) {
      state.push(action.payload);
    },
    setNotes(state, action) {
      // ..
    },
    // createNote definition removed from here!
  },
});

export const { toggleImportanceOf, appendNote, setNotes }=noteSlice.actions;

// async action creator - returns a async function
export const initializeNotes = () => {
  return async (dispatch) => {
    const notes = await noteService.getAll();
    dispatch(setNotes(notes));
  };
};

// async action creator - returns a async function
// after achieve server communication, dispatch the state manager action that appends new data
export const createNote = (content) => {
  return async (dispatch) => {
    const newNote = await noteService.createNew(content);
    dispatch(appendNote(newNote));
  };
};

export default noteSlice.reducer;
```


### React Query
https://fullstackopen.com/es/part6/react_query_use_reducer_y_el_contexto
