
## Comandos de SQL más comunes.

1.  **SELECT**: 
Para recuperar todos los registros de la tabla "clientes":
```sql
SELECT * FROM clientes;
```

Para recuperar los registros de la tabla "clientes" donde el campo "edad" es mayor o igual a 18:
```sql
SELECT * FROM clientes WHERE edad >= 18;
```
Para recuperar los registros de la tabla "clientes" y ordenarlos por el campo "apellido":
```sql
SELECT * FROM clientes ORDER BY apellido;
```

2.  **INSERT**: 
Para insertar un nuevo registro en la tabla "clientes":
```sql
INSERT INTO clientes (nombre, apellido, edad) VALUES ('Juan', 'Pérez', 25);
```

3.  **UPDATE**: 
Para actualizar el campo "edad" a 30 en el registro de la tabla "clientes" con el "id" 1:
```sql
UPDATE clientes SET edad = 30 WHERE id = 1;
```

4.  **DELETE**: 
Para eliminar el registro de la tabla "clientes" con el "id" 2:
```sql
`DELETE FROM clientes WHERE id = 2;`
```

5.  **CREATE**:
Para crear una nueva tabla "empleados" con las columnas "nombre", "apellido" y "edad":
```sql

CREATE TABLE empleados (id INT PRIMARY KEY, nombre VARCHAR(50), apellido VARCHAR(50), edad INT );
```

6.  **ALTER**: 
Para agregar una nueva columna "email" a la tabla "clientes":
```sql
ALTER TABLE clientes ADD COLUMN email VARCHAR(100);
```

7.  **DROP**: 
Para eliminar la tabla "empleados":
```sql
DROP TABLE empleados;
```

8.  **JOIN**: 
Para combinar los datos de las tablas "clientes" y "compras" utilizando el campo "id_cliente":
```sql
SELECT clientes.nombre, compras.producto  FROM clientes JOIN compras ON clientes.id = compras.id_cliente;
```

9.  **WHERE**: 
Para recuperar los registros de la tabla "clientes" donde el campo "edad" es mayor o igual a 18:
```sql
SELECT * FROM clientes WHERE edad >= 18;
```


10.  **ORDER BY**: 
Para ordenar los registros de la tabla "clientes" por el campo "apellido":
```sql
SELECT * FROM clientes ORDER BY apellido;
```

11.  **GROUP BY:** 
Para agrupar los registros de la tabla "ventas" por el campo "producto" y calcular la suma de los campos "cantidad" y "precio":
```sql
SELECT producto, SUM(cantidad), SUM(precio)  FROM ventas GROUP BY producto;
```

12.  **HAVING**: 
Para recuperar los productos de la tabla "ventas" que han tenido ventas por encima de 100 unidades:
```sql
SELECT producto, SUM(cantidad) as total_cantidad  FROM ventas GROUP BY producto HAVING total_cantidad > 100;
```

13.  **DISTINCT**: 
Para recuperar los valores únicos del campo "producto" de la tabla "ventas":
```sql
`SELECT DISTINCT producto FROM ventas;`
```

14.  **UNION**: 
Para combinar los resultados de dos consultas que recuperan los productos vendidos en el mes de enero y febrero, respectivamente:
```sql
SELECT producto FROM ventas WHERE mes = 'enero' UNION SELECT producto FROM ventas WHERE mes = 'febrero';
```

15.  **EXISTS**: 
Para verificar si existe algún registro en la tabla "clientes" con el nombre "Juan":
```sql
IF EXISTS (SELECT * FROM clientes WHERE nombre = 'Juan')   PRINT 'El cliente Juan existe en la tabla' ELSE   PRINT 'El cliente Juan no existe en la tabla'
```
