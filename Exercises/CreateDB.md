
    Name:                   CreateDB.md
    Author:                 Juan Carlos Valera Velazquez
    Proyect:                Practices
    Creation:               31/01/2024
    Last Modification:      31/01/2024
    
    Modify by:              Juan Carlos Valera Velazquez
    
    Description:            
    In this case we start to create a simple steps to create table and some basic store procedure 

### Instruccion para crear una base de datos en SQL Server

~~~~sql
CREATE DATABASE [Nombre_tabla]
~~~~

### Instruccion para crear una tabal en SQL Server

~~~~sql
CREATE TABLE Users(
    Id INT IDENTITY(1,1) NOT NULL,
    Name VARCHAR(255) NOT NULL,
    LastName VARCHAR(255) NOT NULL,
    Age INT,
    DateBirth DATE

    CONSTRAINT PK_Users_UsersId PRIMARY KEY(Id)
)
~~~~

### Instruccion para crear un store procedure que inserte un registro

~~~~sql
CREATE PROCEDURE sp_CreateUser
    @Name VARCHAR(255),
    @LastName VARCHAR(255),
    @Age INT,
    @DateBirth DATE
AS
BEGIN
    INSERT INTO Users (Name, LastName, Age, DateBirth)
    VALUES (@Name, @LastName, @Age, @DateBirth)
END

~~~~

### Instruccion para crear un store procedure que obtenga los registros

~~~~sql
CREATE PROCEDURE sp_GetUsers
AS
BEGIN
    SELECT *
    FROM Users
END
~~~~

### Instruccion para crear un store procedure que actualice un registro

~~~~sql
CREATE PROCEDURE sp_UpdateUser
    @Id INT,
    @Name VARCHAR(255),
    @LastName VARCHAR(255),
    @Age INT,
    @BirthDate DATE
AS
BEGIN
    UPDATE Users
    SET Name = @Name,
        LastName = @LatName,
        Age = @Age,
        BirthDate = @BirthDate
    WHERE
        Id = @Id
END
~~~~

### Instruccion para crear un store procedure que elimine un registro

~~~~sql
CREATE PROCEDURE sp_DeleteUser
    @Id INT
AS
BEGIN
    DELETE FROM Users WHERE Id = @Id
END
~~~~

### Instruccion para ejecutar un stored procedure 

~~~~sql
EXEC sp_CreateUser @Name = 'Carlos', @LastName = 'Valera', @Age = 38 @BirthDate = '1984-01-01'
~~~~




