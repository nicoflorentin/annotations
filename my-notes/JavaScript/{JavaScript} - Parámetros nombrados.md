#### Buena práctica para que las funciones sean más escalables :
```js

// funcion que crea un godzila y recibe parametros a traves de un objeto
// puede o no recibir dichos parámetros
// admite valores por defecto en caso de que no le llegue por parámetro
// se le pasa un objeto completo como parámetro

function createGodzilla ({color, material = 'metal', weight = 200, sound, powers})

const godzilaParams = {
	color: 'blue',
	material: 'plastic',
	sound: 'GROARR',
	powers: ['lighting', 'fire']
}

// ejecuta la funcion con el objeto de configuracion como argumento
createGodzilla(godzillaParams)
```

