## Nested routes
Se renderiza el componente UserDashboard y se pone un enrutador para definir al hijo de que va a tener UserDashboard.
```jsx
// App.jsx
import { Route, Routes } from "react-router-dom"

<Route path='userDashboard' element={<UserDashboard/>}>
	<Route path='personalInfo' element={<PersonalInfo />}/>
	<Route path='mypurchases' element={<MyPurchases />}/>
	<Route path='myproducts' element={<MyProducts />}/>
	<Route path='addproducts' element={<AddProducts />}/>
	<Route path='sells' element={<SellsRegistry />}/>
	<Route path='orders' element={<Orders />}/>
</Route>
```

Definiendo el hijo de UserDashboard :
```jsx
// UserDashboard.jsx
// EL componente Outlet define donde se va a renderizar el componente hijo
import { Outlet } from "react-router-dom"

const UserDashboard = () => {
  return (
      <div>
        <div className=" h-full col-span-2" id="leftContainer">
          <AsideBar />
        </div>
        <div className=" h-full col-span-8" id="rightContainer">
          <Outlet />
        </div>
      </div>
  )
}
  
export default UserDashboard
```

## NavLink
Contcatenar strings y handlers
```jsx
<NavLink
	className={({ isActive }) => {
		return (
		`flex w-full p-3 gap-2 rounded-lg border-2 border-transparent
		hover:border-red-200 hover:border-2` + activeStyles(isActive)
		)
	}}
	to={`/userDashboard/${sectionPath}`}
>	
	<img className="h-5" src={icon} alt={icon} />
	<p>{sectionName}</p>
</NavLink>
```

## No match route
Para definir un elemento a renderizar cuando no existe una ruta
```jsx
 <Route path='*' element={<NoMatch />} />
```

## Index route
Para definir la ruta que se renderiza por defecto al renderizar el componente padre
```jsx
<Route path='products' element={<Products />}>
	<Route index element={<FeaturedProducts />} />
	<Route path='featured' element={<FeaturedProducts />} />
	<Route path='new' element={<NewProducts />} />
</Route>
```

## Active link
La callback que recibe el atributo html recibe como parámetro el booleano isActive
```jsx
import { NavLink } from 'react-router-dom'
	export const Navbar = () => {	
	const navLinkStyles = ({ isActive }) => {
		return {
			fontWeight: isActive ? 'bold' : 'normal',
			textDecoration: isActive ? 'none' : 'underline'
		}
	}
	return (
		<nav className='primary-nav'>
			<NavLink to='/' style={navLinkStyles}>
			Home
			</NavLink>
		</nav>
	)
}
```

## Dynamic routes and URL params
```jsx
//App.jsx
<Route path='users' element={<Users />}>
	<Route path=':userId' element={<UserDetails />} />
</Route>
```
userId llega como parámetro al componente UserDetails : 
```jsx
//UserDetail.jsx
import { useParams } from 'react-router-dom'

export const UserDetails = () => {
  const { userId } = useParams()
  return <div>Details about user {userId}</div>
}
```

## Search params
usar querys de la URL : 

```jsx
import { useSearchParams } from 'react-router-dom'

export const Users = () => {
  const [searchParams, setSearchParams] = useSearchParams()
  const showActiverUsers = searchParams.get('filter') === 'active'
  return (
    <>
      <div>
        <button onClick={() => setSearchParams({ filter: 'active' })}>
          Active Users
        </button>
        <button onClick={() => setSearchParams({})}>Reset Filter</button>
      </div>
      {showActiverUsers ? (
        <h2>Showing active users</h2>
      ) : (
        <h2>Showing all users</h2>
      )}
    </>
  )
}
```

## Relative links
Sin la barra adelante es una ruta absoluta, sobreescribe toda la ruta
Con la barra adelante es una ruta relativa, se acopla a la ruta padre mas cercana
```jsx
//absoluta. resultado : /featured
<Route path='featured' element={<FeaturedProducts />} />

//relativa. resultado : /products/new
<Route path='new' element={<NewProducts />} />
```

## Lazy loading
Descargar un componente sólo cuando el usuario lo requiera
```jsx
const LazyAbout = React.lazy(() => import('./components/About'))
function App() {
  return (
	<Routes>
		<Route
		  path='about'
		  element={
			<React.Suspense fallback='Loading...'>
			  <LazyAbout />
			</React.Suspense>
		  }
		/>
	</Routes>

  )
}
export default App
```

## Authentication and protected routes
##### App.jsx
```jsx
//App.jsx
import { AuthProvider } from './components/auth'
import { Login } from './components/Login'
import { Profile } from './components/Profile'
import { RequireAuth } from './components/RequireAuth'

function App() {
  return (
    <AuthProvider>
      <Navbar />
      <Routes>
        <Route path='/' element={<Home />} />
        <Route path='/login' element={<Login />} />
        <Route
          path='/profile'
          element={
            <RequireAuth>
              <Profile />
            </RequireAuth>
          }
        />
      </Routes>
    </AuthProvider>
  )
}

export default App
```
##### Auth.js
```jsx
//auth.js
import { useState, createContext, useContext } from 'react'

// se crea una instancia del contexto con valor inicial null
const AuthContext = createContext(null)

// provider del contexto
export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null)

  const login = user => {
    setUser(user)
  }
  const logout = () => {
    setUser(null)
  }

  return (
  // provider con el estado y las funciones manejadoras, todo dentro de un objeto
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  )
}

// useAuth es el custom hook que devuelve la instancia del contexto
export const useAuth = () => {
  return useContext(AuthContext)
}
```
##### Login.jsx
```jsx
//Login.jsx
import { useState } from 'react'
import { useNavigate, useLocation } from 'react-router-dom'
import { useAuth } from './auth'

export const Login = () => {
  const [user, setUser] = useState('')
  // devuelve una funcion que espera una ruta como argumento para cambiar la url y navegar
  const navigate = useNavigate()
  // devuelve la ruta actual
  const location = useLocation()
  // en auth esta el objeto que representa el contexto
  const auth = useAuth()

// location.state se usa para acceder a los datos de estado pasados a través de la navegación de la aplicación. Por ejemplo, si navegas de una página a otra, puedes pasar datos adicionales a través del objeto `state`.
  const redirectPath = location.state?.path || '/'

  const handleLogin = () => {
    auth.login(user)
    // una vez que hace el login navega a la ruta, y reemplaza el historial para que si solicita ir
    // atrás, no vuelva a la pantalla de login
    navigate(redirectPath, { replace: true })
  }
  return (
    <div>
      <label>
        Username: <input type='text' onChange={e => setUser(e.target.value)} />
      </label>{' '}
      <button onClick={handleLogin}>Login</button>
    </div>
  )
}
```
##### NavBar.jsx
```jsx
//NavBar.jsx
import { NavLink } from 'react-router-dom'
import { useAuth } from './auth'

export const Navbar = () => {
// auth es el objeto del contexto con sus propiedades
  const auth = useAuth()
  const navLinkStyles = ({ isActive }) => {
    return {
      fontWeight: isActive ? 'bold' : 'normal',
      textDecoration: isActive ? 'none' : 'underline'
    }
  }

  return (
    <nav className='primary-nav'>
      <NavLink to='/profile' style={navLinkStyles}>
        Profile
      </NavLink>
      // si no esta logueado entonces se renderiza el boton login
      {!auth.user && (
        <NavLink to='/login' style={navLinkStyles}>
          Login
        </NavLink>
      )}
    </nav>
  )
}
```
##### Profile.jsx
```jsx
//Profile.jsx
import { useNavigate } from 'react-router-dom'
import { useAuth } from './auth'

export const Profile = () => {
  const navigate = useNavigate()
  const auth = useAuth()
  const handleLogout = () => {
    auth.logout()
    navigate('/')
  }
  return (
    <div>
      Welcome {auth.user}.<button onClick={handleLogout}>Logout</button>
    </div>
  )
}
```
##### RequireAuth.jsx
```jsx
//RequireAuth.jsx
import { Navigate, useLocation } from 'react-router-dom'
import { useAuth } from './auth'

// componente que envuelve a la ruta y limita el acceso a la misma
export const RequireAuth = ({ children }) => {
  const location = useLocation()
  const auth = useAuth()
  if (!auth.user) {
  // El prop `state` se utiliza para pasar datos adicionales a la ruta de destino. En este caso, se 
  // pasa un objeto que contiene la propiedad `path`, que es la ruta actual (`location.pathname`) 
  // donde se encontraba el usuario antes de ser redirigido a la página de inicio de sesión.
    return <Navigate to='/login' state={{ path: location.pathname }} />
  }
  return children
}
```
