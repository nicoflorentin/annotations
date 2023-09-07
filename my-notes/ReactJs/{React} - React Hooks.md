## useState( )

```js
const initialValue = {
	key1: value1,
	key2: value2
}

const anotherValue = {
	key3: value3,
	key4: value4
}

[estado, setEstado] = useState(initialValue)

setEstado(anotherValue)
```
Si le paso un callback al setState, ésta callback recibirá como parámetro el current state:
```js
setEstado((estadoActual) => {...estadoActual, ...anotherValue} ))
```
## useEffect( )

```js
useEffect(() => {
    //la callback se ejecuta cuando se monta el componente
	return () => {
	//clean up: React performs the cleanup when the component unmounts
	//puede NO haber return
	}
}, [dependencyArray])
```
- Si **no hay array de dependencias**, el efecto se ejecuta cada vez que se rerenderiza el componente
- Si el array de dependencias esta **vacío**, el efecto se ejecuta solo una vez
- Si el array de dependencias **tiene una variable**, el efecto se ejecuta sólo cuando cambie esa variable.