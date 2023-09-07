### Conectar el usuario a la base de datos en postgres : 
```sql
\c {name of DB}
```
## Sequelize : 

![[Pasted image 20230405095023.png]]
lo que le pasamos a la nueva instancia es un string y se denomina **AURI**
![[Pasted image 20230405100213.png]]

force true para hacer que borre y cree la tabla nuevamente cuando registre cambios
si quiero hacer cambios chicos sin borrar la tabla utilizo ALTER TRUE
![[Pasted image 20230405100717.png]]

![[Pasted image 20230405101711.png]]
![[Pasted image 20230412150156.png]]
enum marca los unicos valores que puede admitir
![[Pasted image 20230405102437.png]]

timestamp false como tercer parametro para eliminar las columnas de createdAt y updatedAt de sequelize

logging false para evitar que se muestre todo el sql en la consola
![[Pasted image 20230405104528.png]]


#### tabla intermedia

database tiene una propiedad llamada "models" **database.models**
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

#### freezeTableName
![[Pasted image 20230606215339.png]]
## Resumen Chat GPT : 

Sequelize.js es un ORM (Object-Relational Mapping) para Node.js que se utiliza para interactuar con bases de datos relacionales como MySQL, PostgreSQL y SQLite. Algunos de los métodos más importantes de Sequelize.js son:

1.  Define: Este método se utiliza para definir modelos en Sequelize.js. Los modelos son clases que representan tablas en la base de datos.
2.  Sync: Este método se utiliza para sincronizar los modelos con la base de datos. Sequelize.js creará las tablas correspondientes si aún no existen en la base de datos.
3.  FindAll: Este método se utiliza para buscar todos los registros en una tabla. Se puede utilizar para filtrar resultados con opciones como where, limit, order, entre otros.
4.  FindOne: Este método se utiliza para buscar un solo registro en una tabla. Al igual que FindAll, se puede utilizar para filtrar resultados con opciones.
5.  Create: Este método se utiliza para crear un nuevo registro en la base de datos.
6.  Update: Este método se utiliza para actualizar un registro existente en la base de datos.
7.  Destroy: Este método se utiliza para eliminar un registro existente en la base de datos.
8.  Raw: Este método se utiliza para ejecutar consultas SQL personalizadas en la base de datos.
9.  Associations: Sequelize.js permite establecer asociaciones entre modelos, como "hasMany", "belongsTo" y "belongsToMany", para simplificar la navegación entre tablas relacionadas.
10.  Transactions: Sequelize.js también admite transacciones para garantizar que varias operaciones en la base de datos se realicen como una sola unidad atómica.

#### Ejemplos de cada método mencionado anteriormente en Sequelize.js:

- **Define**
```js
const { Sequelize, DataTypes } = require('sequelize'); const sequelize = new Sequelize('sqlite::memory:'); const User = sequelize.define('User', { // definir los campos de la tabla User
firstName: { type: DataTypes.STRING, allowNull: false }, lastName: { type: DataTypes.STRING
// allowNull por defecto es true													   
} }); 
sequelize.sync() .then(() => { console.log('La tabla User ha sido creada'); });
```

- **Sync** :
```js
sequelize.sync({ force: true }) .then(() => { console.log('Todas las tablas han sido sincronizadas'); });
```
- **FindAll** : 
```js
User.findAll({ where: { firstName: 'John' } }).then(users => { console.log(users); });
```
- **FindOne** : 
```js
User.findOne({ where: { id: 1 } }).then(user => { console.log(user); });
```
- **Create** : 
```js
User.create({ firstName: 'John', lastName: 'Doe' }).then(user => { console.log(user); });
```
- **Update** : 
```js
User.update({ lastName: 'Doe Jr.' }, { where: { id: 1 } }).then(() => { console.log('El usuario ha sido actualizado'); });
```
- **Destroy** :
```js
User.destroy({ where: { id: 1 } }).then(() => { console.log('El usuario ha sido eliminado'); });
```
- **Raw** : 
```js
sequelize.query('SELECT * FROM users', { type: sequelize.QueryTypes.SELECT }) .then(users => { console.log(users); });
```
- **Associations** : 
```js
const Project = sequelize.define('Project', {
name: DataTypes.STRING 
}); 

User.hasMany(Project);
Project.belongsTo(User); 
// crear un proyecto y asignarlo a un usuario
User.findByPk(1).then(user => {
	Project.create({ name: 'Proyecto A' }).then(project => {
		project.setUser(user);
	})
}); 
// obtener todos los proyectos de un usuario
User.findByPk(1, { include: Project }).then(user => {
console.log(user.projects);
});
```
- **Transactions** : 
```js
sequelize.transaction(async (t) => {
await User.create({ firstName: 'Jane', lastName: 'Doe' }, { transaction: t }); await User.update({ lastName: 'Doe Jr.' }, {
	where: {
		firstName: 'John'
	}, 
	transaction: t
	})
}).then(() => {
	console.log('Transacción completada')
}).catch((err) => {
		console.error('Error en la transacción', err);
});
```