```js
// ./loginSlice.js
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit'
import axios from 'axios'
import { delay } from '../../utilities/delay';
  
// Define una función asincrónica para obtener los datos de la API
export const fetchLogin = createAsyncThunk('login/fetchLogin', async (loginData) => {
  const response = await axios.post('http://localhost:3001/api/login', loginData)
  await delay()
  return response.data
});
  
const initialState = {
  data: { username: '', name: '', token: '' },
  loading: false,
  error: null
}
  
export const loginSlice = createSlice({
  name: 'login',
  initialState,
  reducers: {
    logOut(state) {
      state.data.username = ''
      state.data.name = ''
      state.data.token = ''
    },
  },
  extraReducers: (builder) => {
    builder
      .addCase(fetchLogin.pending, (state) => {
        state.loading = true;
        state.error = null;
      })
      .addCase(fetchLogin.fulfilled, (state, action) => {
        state.loading = false;
        state.data = action.payload.data;
      })
      .addCase(fetchLogin.rejected, (state, action) => {
        state.loading = false;
        state.error = action.error;
      });
  },
})
  
export const { logOut } = loginSlice.actions
export default loginSlice.reducer
```

```js
// ./store.js
import { configureStore } from '@reduxjs/toolkit'
import loginReducer from '../slices/loginSlice'
import dishesReducer from '../slices/dishesSlice'
  
export default configureStore({
  reducer: {
    login: loginReducer,
    dishes: dishesReducer
  },
})
```

```js
// ./Component.jsx
const dispatch = useDispatch();
const { loading, data: loggedUserData, error } = useSelector((state) => state.login);
dispatch(fetchLogin(loginData))
```