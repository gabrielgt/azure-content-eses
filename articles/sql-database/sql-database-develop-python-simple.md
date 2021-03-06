<properties
	pageTitle="Conexión a Base de datos SQL mediante Python | Microsoft Azure"
	description="Este tema muestra un ejemplo de código Pyton que puede usar para conectarse a la base de datos SQL de Azure."
	services="sql-database"
	documentationCenter=""
	authors="meet-bhagdev"
	manager="jhubbard"
	editor=""/>


<tags
	ms.service="sql-database"
	ms.workload="drivers"
	ms.tgt_pltfrm="na"
	ms.devlang="python"
	ms.topic="article"
	ms.date="06/16/2016"
	ms.author="meetb"/>


# Conexión a Base de datos SQL mediante Python


[AZURE.INCLUDE [sql-database-develop-includes-selector-language-platform-depth](../../includes/sql-database-develop-includes-selector-language-platform-depth.md)]


En este tema se muestra cómo conectarse a una base de datos SQL de Azure y consultarla mediante Python. Puede ejecutar esta muestra desde las plataformas Windows, Ubuntu Linux o Mac.


## Paso 1: Configuración del entorno de desarrollo

[Consulte el artículo Prerequisites for using the pymssql Python Driver for SQL Server (Requisitos previos para usar el controlador pymssql de Python para SQL Server).](https://msdn.microsoft.com/library/mt694094.aspx)

## Paso 2: Creación de una base de datos SQL

Vea la [página de introducción](sql-database-get-started.md) para aprender a crear una base de datos de ejemplo. Es importante seguir las directrices para crear una **plantilla de base de datos de AdventureWorks**. Los ejemplos que se muestran a continuación solo funcionan con el **esquema de AdventureWorks**.

## Paso 3: Obtención de detalles de la conexión

[AZURE.INCLUDE [sql-database-include-connection-string-details-20-portalshots](../../includes/sql-database-include-connection-string-details-20-portalshots.md)]

## Paso 4: ejecución de código de muestra

[Proof of Concept connecting to SQL using Python](http://msdn.microsoft.com/library/mt715796.aspx) (Prueba de concepto que se conecta a SQL con Python)

## Pasos siguientes

* Consulte [Información general de desarrollo de Base de datos SQL](sql-database-develop-overview.md).
* Puede encontrar más información en [Microsoft Python Driver para SQL Server](https://msdn.microsoft.com/library/mt652092.aspx).
* Visite el [Centro para desarrolladores de Python](/develop/python/).

## Recursos adicionales 

* [Modelos de diseño para las aplicaciones SaaS multiinquilino con base de datos SQL de Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* Descubra todas las [funcionalidades de Base de datos SQL](https://azure.microsoft.com/services/sql-database/).

<!---HONumber=AcomDC_0622_2016-->