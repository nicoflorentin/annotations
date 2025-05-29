Crear un **Context** en React es muy útil cuando querés compartir estado o funciones entre componentes sin pasarlas manualmente vía props. A continuación te muestro cómo hacerlo paso a paso, de forma clara y profesional:

---

### 🧱 1. Crear el Context

```jsx
// src/context/ThemeContext.jsx
import { createContext, useContext, useState } from 'react';

export const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () =>
    setTheme((prev) => (prev === 'light' ? 'dark' : 'light'));

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}
```

### 🧩 2. Usar el Provider en tu app

```jsx
// src/main.jsx o src/App.jsx
import { ThemeProvider } from './context/ThemeContext';
import App from './App';

const Root = () => (
  <ThemeProvider>
    <App />
  </ThemeProvider>
);

export default Root;
```

### 🧪 3. Consumir el contexto

```jsx
// src/components/Header.jsx
import { useContext } from 'react';
import { ThemeContext } from '../context/ThemeContext';

function Header() {
  const { theme, toggleTheme } = useContext(ThemeContext);

  return (
    <header className={`header ${theme}`}>
      <button onClick={toggleTheme}>Cambiar tema</button>
    </header>
  );
}
```

### 📌 Buenas prácticas
- Separá el archivo del contexto (`ThemeContext.jsx`, `AuthContext.jsx`, etc.).
- Exportá tanto el **contexto** como el **provider**.
- Usá `useContext` solo dentro de componentes hijos del Provider