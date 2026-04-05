[[Datos y Programación]]

-----
### SQL Básico

**Crear tablas**

```sql
#CREATE TABLE nombreTabla (variable1 tipo, variable2 tipo ...)

CREATE TABLE EmployeeDemographics 
(EmployeeID int, 
FirstName varchar(50),
LastName varchar(50),
Age int,
Gender varchar(50)
)
```

**Insertar información**

```sql
#INSERT INTO nombreTabla VALUES (valor1, valor2, valor3...), (), ()

INSERT INTO `sqltutorial`.`employeedemographics` VALUES 
(1001, 'Jim', 'Halpert', 30, 'Male'), 
(1001, 'Jim', 'Halpert', 30, 'Male')
```

**Select + From**

```sql
#SELECT (____) FROM nombreTabla;

SELECT * FROM sqltutorial.employeedemographics; #Todo
SELECT FirstName FROM sqltutorial.employeedemographics; #Columna específica
SELECT FirstName, LastName FROM sqltutorial.employeedemographics; #Columnas específicas
SELECT TOP 5 * FROM sqltutorial.employeedemographics; #Solo los primeros 5
SELECT DISTINCT(EmployeeID) FROM sqltutorial.employeedemographics; #Selecciona los valores únicos
SELECT COUNT(LastName) FROM sqltutorial.employeedemographics;

SELECT MAX(Salary) FROM sqltutorial.employeesalary;
SELECT MIN(Salary) FROM sqltutorial.employeesalary;
SELECT AVG(Salary) FROM sqltutorial.employeesalary;
```

- MySQL no soporta la clausula de _**SELECT TOP**_. Otros sistemas si.

**Where**

```sql
SELECT * FROM sqltutorial.employeedemographics WHERE FirstName = 'Jim'; #Devuelve todo lo que cumpla la condición
SELECT * FROM sqltutorial.employeedemographics WHERE FirstName != 'Jim'; #Otra variante es "<>"
SELECT * FROM sqltutorial.employeedemographics WHERE AGE > 30;

SELECT * FROM sqltutorial.employeedemographics WHERE AGE <= 30 AND Gender = 'Male';
SELECT * FROM sqltutorial.employeedemographics WHERE AGE <= 30 OR Gender = 'Male';

SELECT * FROM sqltutorial.employeedemographics WHERE LastName LIKE 'S%'; #Selecciona lo que sea "parecido" a la condición, en este caso, que comience con S
SELECT * FROM sqltutorial.employeedemographics WHERE LastName LIKE '%S%'; #En cualquier lugar
SELECT * FROM sqltutorial.employeedemographics WHERE LastName LIKE 'S%o%'; #Contiene "S" al principio y "o" en cualquier lugar

SELECT * FROM sqltutorial.employeedemographics WHERE FirstName is NULL;
SELECT * FROM sqltutorial.employeedemographics WHERE FirstName is NOT NULL;

SELECT * FROM sqltutorial.employeedemographics WHERE FirstName IN ('Jim', 'Michael'); #"Igual a (=)", pero muchas veces
```

**Group By + Order By**

```sql
SELECT Gender, COUNT(Gender) FROM sqltutorial.employeedemographics GROUP BY Gender;
SELECT * from employeedemographics ORDER BY Age, Gender DESC;
```

### SQL Intermedio

**Joins:** Sirven para juntar múltiples tablas en un solo output.

![[JoinsSQL.png]]

```sql
#Inner Join
SELECT * 
FROM `employeedemographics` 
Inner Join `employeesalary`
	ON employeedemographics.EmployeeID = employeesalary.EmployeeID

#Outer Join - Full Join
SELECT * 
FROM sqltutorial.employeedemographics
Full Join sqltutorial.employeesalary
	ON employeedemographics.EmployeeID = employeesalary.EmployeeID

# Left - Right Outer Join
SELECT * 
FROM sqltutorial.employeedemographics
Left Outer Join sqltutorial.employeesalary
	ON employeedemographics.EmployeeID = employeesalary.EmployeeID
	
#Más ejemplos
SELECT employeedemographics.EmployeeID, FirstName, LastName, JobTitle, Salary 
FROM sqltutorial.employeedemographics
Right Outer Join sqltutorial.employeesalary
	ON employeedemographics.EmployeeID = employeesalary.EmployeeID
```

---

**Unions:** Otra forma de combinar tablas en un solo resultado, pero una unión selecciona toda la información de todas la tabla y no está separada.

```sql
SELECT * FROM sqltutorial.employeedemographics
UNION 
SELECT * FROM sqltutorial.warehouseemployeedemographics

SELECT EmployeeID, FirstName, Age 
FROM sqltutorial.employeedemographics
UNION ALL
SELECT EmployeeID, JobTitle, Salary FROM sqltutorial.employeesalary
ORDER BY EmployeeID
```

---

**Case Statements:** Permite especificar una condición, y escoger que se va a mostrar cuando esa condición se cumpla. Si hay multiples condiciones que cumplan el criterio, se tomará solo el primer condicional.

```sql
SELECT FirstName, LastName, Age, 
CASE 
	WHEN Age > 30 THEN 'Old'
    ELSE 'Young'
END AS NombreNuevaColumna
FROM sqltutorial.employeedemographics

SELECT FirstName, LastName, Age, 
CASE 
	WHEN Age > 30 THEN 'Old'
    WHEN Age BETWEEN 27 AND 30 THEN 'Young'
    ELSE 'Baby'
END
FROM sqltutorial.employeedemographics
```

---

**Having Clause**

```sql
SELECT JobTitle, COUNT(JobTitle)
FROM sqltutorial.employeedemographics
JOIN sqltutorial.employeesalary
	ON employeedemographics.EmployeeID = employeesalary.EmployeeID
GROUP BY JobTitle
HAVING COUNT(JobTitle) > 1

#EL GROUP BY DEBE ESTAR **SIEMPRE ANTES** DEL HAVING

SELECT JobTitle, AVG(Salary)
FROM sqltutorial.employeedemographics
JOIN sqltutorial.employeesalary
	ON employeedemographics.EmployeeID = employeesalary.EmployeeID
GROUP BY JobTitle
HAVING AVG(Salary) > 45000
ORDER BY AVG(Salary)
```

---

**Updating / Deleting Data _(Actualizar / Borrar datos)_:** Actualizar es diferente de añadir, porque modificará las existentes.

```sql
#UPDATE - Actualizar
UPDATE sqltutorial.employeedemographics
SET Age = 31, Gender = 'Female'
WHERE FirstName = 'Holly' AND LastName = 'Flax'

#DELETE - Borrar
DELETE FROM sqltutorial.employeedemographics
WHERE EmployeeID = 1005;
```

---

**Aliasing _(Aliases)_:** Es muy útil para mejorar la legibilidad del código.

```sql
SELECT FirstName AS Fname #El 'AS' es opcional, funciona igual sin él.k
FROM sqltutorial.employeedemographics;

SELECT AVG(Age) AS AvgAge
FROM sqltutorial.employeedemographics;

SELECT Demo.EmployeeID, Sal.Salary
FROM sqltutorial.employeedemographics AS Demo
JOIN sqltutorial.employeesalary AS Sal
	ON Demo.EmployeeID = Sal.EmployeeID
	
SELECT Demo.EmployeeID, Demo.FirstName, Demo.LastName, Sal.JobTitle, Ware.Age
FROM sqltutorial.employeedemographics AS Demo
LEFT JOIN sqltutorial.employeesalary AS Sal
	ON Demo.EmployeeID = Sal.EmployeeID
LEFT JOIN sqltutorial.warehouseemployeedemographics AS Ware
	on Sal.EmployeeID = Ware.EmployeeID
```

---

**Partition By _(Particiones)_:** Siempre se compara con el **Group By**. Este ultimo solo mete todo junto, por decirlo así, mientras que el **Partition** separa los resultados de acuerdo a un cálculo.

```sql
SELECT Gender,
COUNT(Gender) OVER (PARTITION BY Gender) as TotalGender
FROM sqltutorial.employeedemographics AS Demo
JOIN sqltutorial.employeesalary AS Sal
	ON Demo.EmployeeID = Sal.EmployeeID
```

### SQL Avanzado

**CTE: Common Table Expression.**

```sql
WITH CTE_Employee as

#Select promedio que trabajamos
(SELECT FirstName, LastName, Gender, Salary,
	COUNT(Gender) OVER (PARTITION BY Gender) as TotalGender,
    AVG(Salary) OVER (PARTITION BY Gender) as AvgSalary
FROM sqltutorial.employeedemographics emp
JOIN sqltutorial.employeesalary sal
	on emp.EmployeeID = sal.EmployeeID
WHERE Salary > '45000'
)

SELECT * FROM CTE_Employee
```

---

**Temp Table:** Son tablas temporales que se crean durante la duración de la sesión.

```sql
CREATE TABLE #temp_Employee ( #FORMA GENERAL
EmployeeID int,
JobTitle varchar(100),
Salary int
)

CREATE TEMPORARY TABLE temp_Employee ( #FORMA ESPECÍFICA DE MYSQL
EmployeeID int,
JobTitle varchar(100),
Salary int)
```

- Se le puede añadir información de igual manera que una tabla tradicional.

```sql
DROP TABLE IF EXISTS temp_Employee, temp_Employee2 #Un truco para que no bote errores.

CREATE TEMPORARY TABLE temp_Employee2 (
JobTitle varchar(50),
EmployeesPerJob int,
AvgAge int,
AvgSalary int
)

INSERT INTO temp_Employee2 (
SELECT JobTitle, COUNT(JobTitle), AVG(Age), AVG(Salary)
FROM sqltutorial.employeedemographics emp
JOIN sqltutorial.employeesalary sal
	ON emp.EmployeeID = sal.EmployeeID
GROUP BY JobTitle
)

SELECT * FROM temp_Employee2
```

---

**String Functions + Use Cases _(TRIM, LTRIM, RTRIM, Replace, Substring, Upper, Lower)_**

```sql
# ------ Trim, LTRIM, RTRIM ------
Select EmployeeID, TRIM(EmployeeID) as IDTRIM
From EmployeeErrors

Select EmployeeID, LTRIM(EmployeeID) as IDTRIM
From EmployeeErrors

Select EmployeeID, RTRIM(EmployeeID) as IDTRIM
From EmployeeErrors

# ------ Replace ------
Select LastName, REPLACE(LastName, '- Fired', '') as LastNameFixed
From EmployeeErrors

# ------ Substring ------
Select Substring(err.FirstName,1,3), Substring(dem.FirstName,1,3), Substring(err.LastName,1,3), Substring(dem.LastName,1,3)
FROM EmployeeErrors err
JOIN EmployeeDemographics dem
	on Substring(err.FirstName,1,3) = Substring(dem.FirstName,1,3)
	and Substring(err.LastName,1,3) = Substring(dem.LastName,1,3)
	
# ------ UPPER & LOWER ------
Select firstname, LOWER(firstname)
from EmployeeErrors

Select Firstname, UPPER(FirstName)
from EmployeeErrors
```

---

**Stored Procedures:** Es un grupo de declaraciones de SQL que se crean y almacenan en la BDD. Puede aceptar parámetros de entrada, lo que significa que se puede usar muchas veces por diferentes usuarios en la red.

```sql
CREATE PROCEDURE TEST () #MySQL no acepta este formato
AS 
Select *
From EmployeeDemographics
```

---

**Subqueries o Inner queries**

```sql
# ------ Subquery en Select ------
Select EmployeeID, Salary, (Select AVG(Salary) From employeesalary) as AllAvgSalary
From employeesalary

# ------ Subquery en From ------
Select a.EmployeeID, AllAvgSalary
From (Select EmployeeID, Salary, AVG(Salary) over () as AllAvgSalary
		From employeesalary) a
		
# ------ Subquery en Where ------
Select EmployeeID, JobTitle, Salary
From employeesalary
Where EmployeeID in (
	Select EmployeeID
    From employeedemographics
    Where Age > 30)
```