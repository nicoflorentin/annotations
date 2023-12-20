# Model

## Model Definition

```js
sequelize.define(modelName, attributes, options)
```
 
 example :
```js
const { Sequelize, DataTypes } = require('sequelize');  
const sequelize = new Sequelize('sqlite::memory:');  
  
const User = sequelize.define('User', {  
	// Model attributes are defined here  
		firstName: {  
		type: DataTypes.STRING,  
		allowNull: false  
	},  
	lastName: {  
		type: DataTypes.STRING  
		// allowNull defaults to true  
	}  
	}, {  
	// Other model options go here  
});  

// `sequelize.define` also returns the model  
console.log(User === sequelize.models.User); // true
```

After a model is defined, it is available in 
```js
sequelize.models
```

## Auto Pluralization

You can **stop** the auto-pluralization of model -> table performed by Sequelize using the `freezeTableName: true` option.
```js
sequelize.define('User', {  // ... (attributes)}, {  freezeTableName: true});
```

This behavior can also be defined globally for the sequelize instance, when it is created:
```js
const sequelize = new Sequelize('sqlite::memory:', {  define: {    freezeTableName: true  }});
```

## Model synchronization

- `User.sync()` - This creates the table if it doesn't exist (and does nothing if it already exists)
- `User.sync({ force: true })` - This creates the table, dropping it first if it already existed
- `User.sync({ alter: true })` - This checks what is the current state of the table in the database (which columns it has, what are their data types, etc), and then performs the necessary changes in the table to make it match the model.

### Dropping tables

```js
await User.drop();console.log("User table dropped!");
```


## Creating an instance

### BUILD
```js
const jane = User.build({ name: "Jane" })
console.log(jane instanceof User); // trueconsole.log(jane.name); // "Jane"
```

**The code above does not communicate with the database**.
This is because the **BUILD** method only creates an object that _represents_ data that _can_ be mapped to a database
```js
await jane.save()
console.log('Jane was saved to the database!');
```


### CREATE
Combines the `build` and `save` methods
```js
const jane = await User.create({ name: "Jane" })
// Jane exists in the database now!console.log(jane instanceof User); // trueconsole.log(jane.name); // "Jane"
```


## Updating an instance

### SAVE
If you change the value of some field of an instance, calling **SAVE** again will update it accordingly:
```js
const jane = await User.create({ name: "Jane" })
console.log(jane.name) // "Jane"
jane.name = "Ada"
// the name is still "Jane" in the database
await jane.save()
// Now the name was updated to "Ada" in the database!
```

### SET
You can update several fields at once
```js
const jane = await User.create({ name: "Jane" })
jane.set({  name: "Ada",  favoriteColor: "blue"})
// As above, the database still has "Jane" and "green"
await jane.save()
// The database now has "Ada" and "blue" for name and favorite color
```

### UPDATE
Note that the `save()` here will also persist any other changes that have been made on this instance, not just those in the previous `set` call. If you want to update a specific set of fields
```JS
const jane = await User.create({ name: "Jane" });
jane.favoriteColor = "blue"
await jane.update({ name: "Ada" })
// The database now has "Ada" for name, but still has the default "green" for favorite color
await jane.save()
// Now the database has "Ada" for name and "blue" for favorite color
```

## Deleting an instance

### DESTROY
```js
const jane = await User.create({ name: "Jane" });
console.log(jane.name); // "Jane"
await jane.destroy(); // Now this entry was removed from the database
```

## Reloading an instance

### RELOAD
```JS
const jane = await User.create({ name: "Jane" });
console.log(jane.name); // "Jane"
jane.name = "Ada"; // the name is still "Jane" in the database
await jane.reload();
console.log(jane.name); // "Jane"
```

## Saving only some fields
```js
const jane = await User.create({ name: "Jane" });
console.log(jane.name); // "Jane"
console.log(jane.favoriteColor); // "green"
jane.name = "Jane II";
jane.favoriteColor = "blue";
await jane.save({ fields: ['name'] });
console.log(jane.name); // "Jane II"
console.log(jane.favoriteColor); // "blue"// The above printed blue because the local object has it set to blue, but// in the database it is still "green":
await jane.reload();
console.log(jane.name); // "Jane II"
console.log(jane.favoriteColor); // "green"
```

## Incrementing and decrementing integer values[​](https://sequelize.org/docs/v6/core-concepts/model-instances/#incrementing-and-decrementing-integer-values "Direct link to Incrementing and decrementing integer values")

### INCREMENT / DECREMENT
```JS
const jane = await User.create({ name: "Jane", age: 100 });
const incrementResult = await jane.increment('age', { by: 2 });
// Note: to increment by 1 you can omit the `by` option and just do `user.increment('age')`// In PostgreSQL, `incrementResult` will be the updated user, unless the option// `{ returning: false }` was set (and then it will be undefined).// In other dialects, `incrementResult` will be undefined. If you need the updated instance, you will have to call `user.reload()`.
```

You can also increment **multiple fields at once**:
```JS
const jane = await User.create({ name: "Jane", age: 100, cash: 5000 });
await jane.increment({  'age': 2,  'cash': 100});
// If the values are incremented by the same amount, you can use this other syntax as well:
await jane.increment(['age', 'cash'], { by: 2 });
```


# Model Querying - Basics

## Simple SELECT queries

### FINDALL
You can read the whole table from the database
```js
// Find all users
const users = await User.findAll();
console.log(users.every(user => user instanceof User)); // true
console.log("All users:", JSON.stringify(users, null, 2));
```

```sql
SELECT * FROM ...
```

## Specifying attributes for SELECT queries[​](https://sequelize.org/docs/v6/core-concepts/model-querying-basics/#specifying-attributes-for-select-queries "Direct link to Specifying attributes for SELECT queries")

### ATTRIBUTES
```JS
Model.findAll({  attributes: ['foo', 'bar']});
```
```SQL
SELECT foo, bar FROM ...
```

## Applying WHERE clauses

### WHERE
The `where` option is used to filter the query. There are lots of operators to use for the `where` clause, available as Symbols from OP (operators)

### The basics
```js
Post.findAll(
	{ where: {
			authorId: 2,
			status: 'active'
		}
	}
);
// SELECT * FROM post WHERE authorId = 2;
```

### OP EQ
```js
const { Op } = require("sequelize");
Post.findAll(
	{where: {  
		authorId: {[Op.eq]: 2}  
	}}
);
// SELECT * FROM post WHERE authorId = 2;
```

Multiple checks can be passed:
```js
Post.findAll({  where: {    authorId: 12,    status: 'active'  }});// SELECT * FROM post WHERE authorId = 12 AND status = 'active';
```

### OP AND
```js
const { Op } = require("sequelize");
Post.findAll(
{where:
	{[Op.and]: [
		{authorId: 12 },
		{status: 'active'}
	]
	}
});
// SELECT * FROM post WHERE authorId = 12 AND status = 'active';
```

cleaner equivalence
```js
const { Op } = require("sequelize");
Post.destroy(
{where:
	 {authorId:{
		 [Op.or]:[12, 13]
	}
	}
 }
);// DELETE FROM post WHERE authorId = 12 OR authorId = 13;
```

## Simple UPDATE queries
Update queries also accept the `where` option, just like the read queries shown above.
```js
// Change everyone without a last name to "Doe"
await User.update({ lastName: "Doe" }, {where: {lastName: null}});
```

## Creating in bulk[​](https://sequelize.org/docs/v6/core-concepts/model-querying-basics/#creating-in-bulk "Direct link to Creating in bulk")

### BULKCREATE
```JS
const captains = await Captain.bulkCreate(
	[
		{ name: 'Jack Sparrow' },
		{ name: 'Davy Jones' }
	]
);
console.log(captains.length); // 2
console.log(captains[0] instanceof Captain); // true
console.log(captains[0].name); // 'Jack Sparrow'
console.log(captains[0].id); // 1 // (or another auto-generated value)
```

## Limits and Pagination[​](https://sequelize.org/docs/v6/core-concepts/model-querying-basics/#limits-and-pagination "Direct link to Limits and Pagination")

### LIMIT / OFFSET

```js
// Fetch 10 instances/rows
Project.findAll({ limit: 10 });
// Skip 8 instances/rows
Project.findAll({ offset: 8 });
// Skip 5 instances and fetch the 5 after that
Project.findAll({ offset: 5, limit: 5 });
```

# Model Querying - Finders

Sequelize **automatically wraps results in proper instance objects**
When there are too many results, **this wrapping can be inefficient.**
To disable this wrapping and receive a plain response instead, pass
`{ raw: true }` 
as an option to the finder method.

### FINDALL
## FINDBYPK
Obtains only a single entry from the table
```js
const project = await Project.findByPk(123);
if (project === null) {
	console.log('Not found!');
} 
else {console.log(project instanceof Project); // true 
// Its primary key is 123}
```

### FINDONE
The `findOne` method obtains the first entry it finds (that fulfills the optional query options, if provided).
```js
const project = await Project.findOne({ where: { title: 'My Title' } });
if (project === null) {  console.log('Not found!');}
else {  console.log(project instanceof Project); // true  
console.log(project.title); // 'My Title'}
```

### FINDORCREATE
```js
const [user, created] = await User.findOrCreate({
	where: { username: 'sdepold' },
	defaults: {job: 'Technical Lead JavaScript'}}
);
console.log(user.username); // 'sdepold'
console.log(user.job); // This may or may not be 'Technical Lead JavaScript'
console.log(created); // The boolean indicating whether this instance was just created
if (created) {console.log(user.job); // This will certainly be 'Technical Lead JavaScript'
}
```

### FINDANDCOUNTALL
The `findAndCountAll` method is a convenience method that combines `findAll` and `count`. This is useful when dealing with queries related to pagination where you want to retrieve data with a `limit` and `offset` but also need to know the total number of records that match the query.

When `group` is not provided, the `findAndCountAll` method returns an object with two properties:

- `count` - an integer - the total number records matching the query
- `rows` - an array of objects - the obtained records

When `group` is provided, the `findAndCountAll` method returns an object with two properties:

- `count` - an array of objects - contains the count in each group and the projected attributes
- `rows` - an array of objects - the obtained records

```JS
const { count, rows } = await Project.findAndCountAll(
	{where:	{
		title: { [Op.like]: 'foo%'} },
		offset: 10,
		limit: 2
	}
);
console.log(count);
console.log(rows);
```

# Getters, Setters

## Getters

A getter is a `get()` function defined for one column in the model definition:
```js
const User = sequelize.define('user', { 
// Let's say we wanted to see every username in uppercase, even
// though they are not necessarily uppercase in the database itself  
	username: {
	type: DataTypes.STRING,
	get() {
		const rawValue = this.getDataValue('username');
		return rawValue ? rawValue.toUpperCase() : null;
	}
}});
```

This getter, just like a standard JavaScript getter, is called automatically when the field value is read:
```js
const user = User.build({ username: 'SuperUser123' });
console.log(user.username); // 'SUPERUSER123'
console.log(user.getDataValue('username')); // 'SuperUser123'
```

## Setters

A setter is a `set()` function defined for one column in the model definition. It receives the value being set :
```js
const User = sequelize.define('user', {
	username: DataTypes.STRING,
	password: {
	type: DataTypes.STRING,
	set(value) {
		// Storing passwords in plaintext in the database is terrible.
		// Hashing the value with an appropriate cryptographic hash function is better.
		this.setDataValue('password', hash(value));
	}
}});
```

```js
const user = User.build({
    username: 'someone',
    password: 'NotSo§tr0ngP4$SW0RD!'
});
console.log(user.password);
//'7cfc84b8ea898bb72462e78b4643cfccd77e9f05678ec2ce78754147ba947acc'
console.log(user.getDataValue('password')); //'7cfc84b8ea898bb72462e78b4643cfccd77e9f05678ec2ce78754147ba947acc'
```

Observe that Sequelize called the setter automatically, before even sending data to the database. The only data the database ever saw was the already hashed value.

If we wanted to involve another field from our model instance in the computation, that is possible and very easy!

```js
const User = sequelize.define('user', {
    username: DataTypes.STRING,
    password: {
        type: DataTypes.STRING,
        set(value) {
        // Storing passwords in plaintext in the database is terrible.
        // Hashing the value with an appropriate cryptographic hash function is better.
        // Using the username as a salt is better.      
            this.setDataValue('password', hash(this.username + value));
        }
    }
});
```


# Misc

## Including everything[​](https://sequelize.org/docs/v6/advanced-association-concepts/eager-loading/#including-everything "Direct link to Including everything")

To include all associated models, you can use the `all` and `nested` options:

```js
// Fetch all models associated with User
User.findAll({
    include: {
        all: true
    }
}); // Fetch all models associated with User and their nested associations (recursively)
User.findAll({
    include: {
        all: true,
        nested: true
    }
});
```

## Relacionar modelos con las keys
### Relacionar uno a uno (set)
```js
await currentUsuario?.setPaciente(newPaciente)
```
### Relacionar uno a muchos (add)
```js
await currentUsuario?.addPaciente(newPaciente)
```

### Configurar un alias para el include
```js
//controller.js
const odontograma = await Odontograma.findByPk(id, {
    include: [
      {model: Diente, order: [['number', 'ASC']]},
		{
			model: Observacion, 
			as: 'observaciones'
		}
	]
})
  
/// (...more code)
// observaciones instead observacion
await newOdontograma.addObservaciones(observacion)
```
```js
//model.js
Odontograma.hasMany(Observacion, { foreignKey: "odontogramaId", as: 'observaciones' })
Observacion.belongsTo(Odontograma, { foreignKey: "odontogramaId", as: 'odontograma' })
```
