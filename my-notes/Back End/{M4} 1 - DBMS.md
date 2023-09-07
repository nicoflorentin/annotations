
Data Base Management System
Acceder - Manipular - Hacer CONSULTAS
No modificamos de forma directa la base de datos, por eso se usa un DBMS
Para manipular datos usamos **postgreSQL**
Bases de datos relacionales

#### modelo entidad relación : 
- entidad  : cada usuario
- atributos :  cada dato del usuario
- conjunto de relaciones : es una asociacion entre varias entidades

relacion de uno a muchos ( 1 : N )
realcion de muchos a muchos ( N : M )
relacion de uno a uno ( 1 : 1 )

#### diagrama de flujo

![[Pasted image 20230404224726.png]]



## Tercera forma normal ( 3FN )

- los datos deben ser atómicos, tienen que ser indivisibles
- no debe haber dependendia parcial entre los atributos

#### primary key

- hasta ahora los llamabamos como id
- sirve para realcionar una entidad con otra tabla

#### foreign keys

- cuando utilizamos primary keys que pertenecen a otra tabla

![[Pasted image 20230404232837.png]]

