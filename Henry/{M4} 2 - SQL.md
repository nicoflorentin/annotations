
Tabla intermedia
![[Pasted image 20230404095354.png]]

Estructura de datos

![[Pasted image 20230404095442.png]]

#### Software : 
- PostgreSQL
- pgAdmin
- SQL Shell

#### Comandos :

- " \l "
- DROP DATABASE nombre ; , borrar base de datos
- CREATE DATABASE nombre ; 
-  \dt display table

![[Pasted image 20230404111419.png]]

#### ingresar registro :
![[Pasted image 20230404111515.png]]
![[Pasted image 20230408175209.png]]

### query tool para usar comandos sql en postgresSQL :
![[Pasted image 20230408174808.png]]

#### SELECT traer todos los campos (**) de personajes
![[Pasted image 20230404112855.png]]

![[Pasted image 20230408180311.png]]

![[Pasted image 20230404113056.png]]
![[Pasted image 20230408180458.png]]

### group and order :

##### GROUP
con COUNT cuenta la cantidad que agrupa y cuenta lo que pongas en el campo COUNT, en este caso cuenta el campo id.
![[Pasted image 20230404114018.png]]

#### ORDER
![[Pasted image 20230408180623.png]]

#### insert
![[Pasted image 20230408175847.png]]

#### DELETE
![[Pasted image 20230408180134.png]]

####  Sub Query

#### Join :
une dos tablas
![[Pasted image 20230408185449.png]]

![[Pasted image 20230408185543.png]]




#### Create

![[Pasted image 20230408165531.png]]

![[Pasted image 20230408165316.png]]

una primary key es unica
es un campo obligatorio, no puede estar vacio

##### constraints : 

NOT NULL significa que no puede estar vacio, es una restriccion
UNIQUE significa que el campo debe ser unico
primary key tiene not null y unique al mismo tiempo


#### foreign key to primary key :
![[Pasted image 20230408174622.png]]

