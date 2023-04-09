

![[Pasted image 20230405095023.png]]

![[Pasted image 20230405100213.png]]


force true para hacer que borre y cree la tabla nuevamente cuando registre cambios
si quiero hacer cambios chicos sin borrar la tabla utilizo ALTER TRUE
![[Pasted image 20230405100717.png]]

![[Pasted image 20230405101711.png]]

enum marca los unicos valores que puede admitir
![[Pasted image 20230405102437.png]]

timestamp false como tercer parametro para eliminar las columnas de createdAt y updatedAt de sequelize

logging false para evitar que se muestre todo el sql en la consola
![[Pasted image 20230405104528.png]]


#### tabla intermedia

craemos las tablas con una funcion que recibe database
sacamos los modelos de la database
linkeamos las dos tablas y le pasamos el nombre de la tabla intermedia
![[Pasted image 20230405111132.png]]

#### metodos de los modelos

findAll( )
create( { name } )
findByPk( )

#### filtrar

![[Pasted image 20230405122115.png]]

#### destroy

![[Pasted image 20230405123802.png]]

#### bulk

para agregar varios datos a la vez pasandole un array