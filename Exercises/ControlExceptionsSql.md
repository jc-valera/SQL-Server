    
    Name:                   ControlExceptionsSql.md
    Author:                 Juan Carlos Valera Velazquez
    Proyect:                Practices
    Creation:               25/03/2024
    Last Modification:      25/03/2014
    
    Modify by:              Juan Carlos Valera Velazquez
    Description:            In this file we start to create some excercises to practice some
                            control execptions

## Crea una base de datos la cual tendra una tabla con dos campos
    
~~~~sql
USE master
GO

CREATE DATABASE SqlServerTest
GO

USE SqlServerTest
GO

CREATE TABLE SqlTest(
	Id INT IDENTITY,
	NameUser VARCHAR(50)
)
GO
~~~~

### Creada esa base y esa tabla crea un stored procedure el cual inserte un registro en la tabla creada y tenga como valor de retorno el id que se acaba de insertar, de iguamanera el stored procedure debe controlar las excepciones en caso de error y en caso de algun error debera almacenar dicho error en una tabla llamada History_Errors


~~~~sql

CREATE TABLE History_Errors(
	Id INT IDENTITY,
	ErrorNumber INT,
	ErrorMessage VARCHAR(MAX),
	ProcedureName VARCHAR(200),
	LineNumber INT,
	DateError DATETIME
)

CREATE PROCEDURE sp_SaveTestOutput
	@NameUser VARCHAR(50),

	@Id INT OUTPUT
AS
BEGIN TRANSACTION

	BEGIN TRY

		INSERT INTO SqlTest (NameUser) VALUES (@NameUser);
		--SELECT @Id = MAX(Id) FROM Students
		SELECT @Id = SCOPE_IDENTITY();

		COMMIT TRANSACTION

	END TRY

BEGIN CATCH

ROLLBACK TRANSACTION

	INSERT INTO History_Errors
	SELECT ERROR_NUMBER() AS ErrorNumber,
		ERROR_MESSAGE() AS ErrorMessage,
		ERROR_PROCEDURE() AS ProcedureName,
		ERROR_LINE() AS LineNumber,
		GETDATE() AS DateError

END CATCH;

~~~~

### Ejecuta el stored procedure antes creado y verifica el id retornado

~~~~sql

DECLARE @Id_Output INT

EXECUTE sp_SaveTestOutput 'ABEL', @Id = @Id_Output OUTPUT

SELECT @Id_Output AS Id

~~~~

### Realiza un error intencionado el cual debera almacenarce en la tabla History_Errors
