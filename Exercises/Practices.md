
    Name:                   Practices.md
    Author:                 Juan Carlos Valera Velazquez
    Proyect:                Practices
    Creation:               09/01/2024
    Last Modification:      09/01/2024
    
    Modify by:              Juan Carlos Valera Velazquez
    Description:            In this file we start to create some excercises to practice SQL 


## Usando como base la base de datos Northwind responda la siguientes preguntas

### ¿Cómo contar el número de registros en una tabla en SQL?

~~~~sql
SELECT 
    COUNT(*) AS NumRegistre 
FROM 
    Employees
~~~~

### Dada una tabla "Orders" y una tabla "Customers", ¿cómo listar todos los clientes que no han realizado ninguna compra?

~~~~sql
SELECT 
    * 
FROM 
    Orders O
INNER JOIN Customers C 
    ON C.CustomerID = O.CustomerID
WHERE 
    ShipRegion IS NULL
~~~~


### Realiza una consulta SQL para obtener la segunda fila de una tabla.

~~~~sql
SELECT 
    *
FROM (
  SELECT *, 
    ROW_NUMBER() OVER (ORDER BY (SELECT NULL)) AS rn
  FROM 
    Employees
) AS subquery
WHERE 
    rn = 2;
~~~~


### Realiza una consulta SQL para actualizar la información en una tabla.

~~~sql
UPDATE Employees 
SET 
    LastName = 'King' 
WHERE
    EmployeeID = 7
~~~


### Dada una tabla con duplicados, ¿cómo eliminar solo los registros duplicados?
~~~sql
WITH cte AS (
	SELECT *, 
		ROW_NUMBER() OVER (PARTITION BY Title ORDER BY Title DESC) AS RowNumber
	FROM Employees
)
DELETE FROM cte WHERE RowNumber > 1
~~~
