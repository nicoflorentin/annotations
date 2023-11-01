##### PRIMERA DUDA

![[Pasted image 20231011164403.png]]

linea 24 : Cuando creamos una consulta. Los productos llegarían tambien por párams? en la documentacion de la api dice que recibe el dni para asociarlo al usuario, y por body llegan los datos de la consulta. Tal vez al crear la consulta haga falta indicar que productos se van a utilizar para luego actualizar stock ? No me queda clara la relación.

Ejemplo de la documentacion ⬇ (no hay productos)

```json
{  
"prestacion": "Limpieza y blanqueamiento",  
"zona": "Distal",  
"caras": "V",  
"sector": 16,  
"observaciones": "alguna observacion"  
}
```

##### SEGUNDA DUDA

Cómo es la relacion usuario paciente?
Hay una ruta para crear paciente que automaticamente relaciona el paciente creado con el usuario a traves del DNI. (linea 46)
![[Pasted image 20231011205945.png]]
El paciente se crea desde el front, o hay que crear automaticamente un paciente al crear un usuario desde el back?