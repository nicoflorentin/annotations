
## Instalación :

## Configuración : 

## Actions

#### Action asincronica con dispatch :
```js
export const getCelularDetails = (id) => {
    return function (dispatch) {
        return fetch(`http://localhost:3001/celulares/${id}`)
            .then((data) => data.json())
            .then((celular) => {
                dispatch({ type: GET_CELULARES_DETAIL, payload: celular });
            });
    };
};
```
#### Action sincronica sin dispatch : 
```js
export const deleteCelular = (id) => {
    return { type: DELETE_CELULAR, payload: id };
};
```

## Reducer

```js
/* Importa las action-types aquí. */
import { GET_ALL_CELULARES } from "../actions/index";
import { GET_CELULARES_DETAIL } from "../actions/index";
import { CREATE_CELULAR } from "../actions/index";
import { DELETE_CELULAR } from "../actions/index";
  
const initialState = {
    celulares: [],
    celularDetail: {},
};

const rootReducer = (state = initialState, action) => {
    // Tu código
    switch (action.type) {
        case GET_ALL_CELULARES:
            return { ...state, celulares: action.payload };
      case GET_CELULARES_DETAIL:
         return {...state, celularDetail: action.payload}
      case CREATE_CELULAR:
         return {...state, celulares: [...state.celulares, action.payload]}
      case DELETE_CELULAR:
         return {...state, celulares: state.celulares.filter((celular)=> celular.id !== action.payload)}
        default:
            return state;
    }
};

export default rootReducer;
```

## Store

```js
import { createStore, applyMiddleware, compose } from 'redux';
import rootReducer from '../reducer';
import thunk from 'redux-thunk';

const composeEnhancers =
   (typeof window !== 'undefined' &&
      window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__) ||
   compose;

const store = createStore(
   rootReducer,
   composeEnhancers(applyMiddleware(thunk)),
);
  
export default store;
```

## Index

```js
import App from './App';
import React from 'react';
import ReactDOM from 'react-dom';
import store from './redux/store';
import { Provider } from 'react-redux';
  
ReactDOM.render(
   <React.StrictMode>
      <Provider store={store}>
         <BrowserRouter>
            <App />
         </BrowserRouter>
      </Provider>
   </React.StrictMode>,
   document.getElementById('root')
);
```

## Usar una action

```js
import React from 'react';
import { useDispatch } from 'react-redux';
import * as actions from '../../redux/actions/index'
  
const CelularCard = (props) => {
  
   const dispatch = useDispatch()
   const closeHandler = (id) => {
      dispatch(actions.deleteCelular(id))
   }
}
```

## Usar el estado global

```js
import React from "react";
import { useDispatch, useSelector } from "react-redux";
 
const CelularDetail = (props) => {
    const dispatch = useDispatch();
    const celular = useSelector((state) => state.celularDetail);
      console.log(celular)
}
```

