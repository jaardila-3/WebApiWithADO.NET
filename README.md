# WebApiWithADO.NET
PROYECTO CON ADO.NET Y SQLSERVER

**************SCRIPTS SQL SERVER******************
**CREAR DB AND TABLE**
use master
go
IF NOT EXISTS(SELECT name FROM master.dbo.sysdatabases WHERE NAME = 'DBPRUEBAS')
CREATE DATABASE DBPRUEBAS

GO 

USE DBPRUEBAS

GO

if not exists (SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = 'dbo' AND TABLE_NAME = 'USUARIO')
create table USUARIO(
IdUsuario int primary key identity(1,1),
DocumentoIdentidad varchar(60),
Nombres varchar(60),
Telefono varchar(60),
Correo varchar(60),
Ciudad varchar(60),
FechaRegistro datetime default getdate()
)

go

select * from dbo.USUARIO
**INSERTAR DATOS**
USE [DBPRUEBAS]
GO
SET IDENTITY_INSERT [dbo].[USUARIO] ON 

INSERT [dbo].[USUARIO] ([IdUsuario], [DocumentoIdentidad], [Nombres], [Telefono], [Correo], [Ciudad]) VALUES (1, N'32504112', N'Regina', N'690577998', N'blandit.mattis@eratvolutpat.edu', N'Rae Lakes')
INSERT [dbo].[USUARIO] ([IdUsuario], [DocumentoIdentidad], [Nombres], [Telefono], [Correo], [Ciudad]) VALUES (2, N'20427780', N'Macy', N'270411465', N'interdum@id.net', N'Treppo Carnico')
INSERT [dbo].[USUARIO] ([IdUsuario], [DocumentoIdentidad], [Nombres], [Telefono], [Correo], [Ciudad]) VALUES (3, N'47714668', N'Sophia', N'757428589', N'mattis.semper.dui@nibhPhasellusnulla.net', N'Levin')
INSERT [dbo].[USUARIO] ([IdUsuario], [DocumentoIdentidad], [Nombres], [Telefono], [Correo], [Ciudad]) VALUES (4, N'32493629', N'Rhiannon', N'794799685', N'posuere@Morbinon.edu', N'Hearst')
INSERT [dbo].[USUARIO] ([IdUsuario], [DocumentoIdentidad], [Nombres], [Telefono], [Correo], [Ciudad]) VALUES (5, N'22383970', N'Aubrey', N'711648390', N'odio@arcuVestibulumante.edu', N'Baltasound')

SET IDENTITY_INSERT [dbo].[USUARIO] OFF

**CREAR PROCEDIMIENTOS**
go
use DBPRUEBAS
go
--************************ VALIDAMOS SI EXISTE EL PROCEDIMIENTO ************************--

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'usp_registrar')
DROP PROCEDURE usp_registrar

go

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'usp_modificar')
DROP PROCEDURE usp_modificar

go

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'usp_obtener')
DROP PROCEDURE usp_obtener

go

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'usp_listar')
DROP PROCEDURE usp_obtener

go

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'usp_eliminar')
DROP PROCEDURE usp_eliminar

go

--************************ PROCEDIMIENTOS PARA CREAR ************************--
create procedure usp_registrar(
@documentoidentidad varchar(60),
@nombres varchar(60),
@telefono varchar(60),
@correo varchar(60),
@ciudad varchar(60)
)
as
begin

insert into USUARIO(DocumentoIdentidad,Nombres,Telefono,Correo,Ciudad)
values
(
@documentoidentidad,
@nombres,
@telefono,
@correo,
@ciudad
)

end


go

create procedure usp_modificar(
@idusuario int,
@documentoidentidad varchar(60),
@nombres varchar(60),
@telefono varchar(60),
@correo varchar(60),
@ciudad varchar(60)
)
as
begin

update USUARIO set 
DocumentoIdentidad = @documentoidentidad,
Nombres = @nombres,
Telefono = @telefono,
Correo = @correo,
Ciudad = @ciudad
where IdUsuario = @idusuario

end

go

create procedure usp_obtener(@idusuario int)
as
begin

select * from usuario where IdUsuario = @idusuario
end

go
create procedure usp_listar
as
begin

select * from usuario
end


go

go

create procedure usp_eliminar(
@idusuario int
)
as
begin

delete from usuario where IdUsuario = @idusuario

end

go
