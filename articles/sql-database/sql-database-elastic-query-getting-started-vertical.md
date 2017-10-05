---
title: "Wprowadzenie do zapytań między bazami danych (partycjonowanie pionowe) | Dokumentacja firmy Microsoft"
description: "jak używać zapytania elastycznej bazy danych z baz danych w pionie podzielonym na partycje"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 17158c4960e9ba9251524659c90af9aec1316774
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="44411-103">Wprowadzenie do zapytań między bazami danych (partycjonowanie pionowe) (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="44411-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="44411-104">Zapytanie elastycznej bazy danych (wersja zapoznawcza) w bazie danych SQL Azure umożliwia uruchamianie zapytania T-SQL, obejmującej wiele baz danych przy użyciu pojedynczy punkt połączenia.</span><span class="sxs-lookup"><span data-stu-id="44411-104">Elastic database query (preview) for Azure SQL Database allows you to run T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="44411-105">Ten temat dotyczy [w pionie na partycje baz danych](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="44411-105">This topic applies to [vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="44411-106">Po zakończeniu zostanie: informacje o sposobie konfigurowania i korzystania z bazy danych SQL Azure do wykonywania zapytań, obejmującej wiele powiązanych baz danych.</span><span class="sxs-lookup"><span data-stu-id="44411-106">When completed, you will: learn how to configure and use an Azure SQL Database to perform queries that span multiple related databases.</span></span> 

<span data-ttu-id="44411-107">Aby uzyskać więcej informacji o funkcji zapytania elastycznej bazy danych, zobacz [bazy danych SQL Azure elastycznej bazy danych zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44411-107">For more information about the elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="44411-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="44411-108">Prerequisites</span></span>

<span data-ttu-id="44411-109">Musi mieć uprawnienie ALTER ANY zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="44411-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="44411-110">To uprawnienie jest dołączany uprawnienie ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="44411-110">This permission is included with the ALTER DATABASE permission.</span></span> <span data-ttu-id="44411-111">Aby odwołać się do źródła danych są potrzebne uprawnienia ALTER ANY zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="44411-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="create-the-sample-databases"></a><span data-ttu-id="44411-112">Tworzenie bazy danych przykładowych</span><span class="sxs-lookup"><span data-stu-id="44411-112">Create the sample databases</span></span>
<span data-ttu-id="44411-113">Do uruchomienia z należy utworzyć dwie bazy danych, **klientów** i **zamówień**, albo w tych samych lub różnych serwerów logicznych.</span><span class="sxs-lookup"><span data-stu-id="44411-113">To start with, we need to create two databases, **Customers** and **Orders**, either in the same or different logical servers.</span></span>   

<span data-ttu-id="44411-114">Wykonaj następujące kwerendy w **zamówień** bazy danych do utworzenia **OrderInformation** tabeli i przykładowych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="44411-114">Execute the following queries on the **Orders** database to create the **OrderInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="44411-115">Teraz, wykonaj następujące zapytanie w **klientów** bazy danych do utworzenia **CustomerInformation** tabeli i przykładowych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="44411-115">Now, execute following query on the **Customers** database to create the **CustomerInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="44411-116">Tworzenie obiektów bazy danych</span><span class="sxs-lookup"><span data-stu-id="44411-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="44411-117">Baza danych o zakresie klucz główny i poświadczenia</span><span class="sxs-lookup"><span data-stu-id="44411-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="44411-118">Otwórz program SQL Server Management Studio lub SQL Server Data Tools w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44411-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="44411-119">Połączenie z bazą danych zleceń i wykonaj następujące polecenia T-SQL:</span><span class="sxs-lookup"><span data-stu-id="44411-119">Connect to the Orders database and execute the following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="44411-120">"Nazwa użytkownika" i "password" powinna być nazwa użytkownika i hasło używane do logowania do bazy danych klientów.</span><span class="sxs-lookup"><span data-stu-id="44411-120">The "username" and "password" should be the username and password used to login into the Customers database.</span></span>
    <span data-ttu-id="44411-121">Uwierzytelnianie przy użyciu usługi Azure Active Directory z zapytaniami elastyczne nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="44411-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="44411-122">Zewnętrzne źródła danych</span><span class="sxs-lookup"><span data-stu-id="44411-122">External data sources</span></span>
<span data-ttu-id="44411-123">Aby utworzyć zewnętrznego źródła danych, uruchom następujące polecenie w bazie danych zleceń:</span><span class="sxs-lookup"><span data-stu-id="44411-123">To create an external data source, execute the following command on the Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="44411-124">Tabele zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="44411-124">External tables</span></span>
<span data-ttu-id="44411-125">Tworzenie tabeli zewnętrznej w bazie danych zamówień odpowiadającego definicja tabeli CustomerInformation:</span><span class="sxs-lookup"><span data-stu-id="44411-125">Create an external table on the Orders database, which matches the definition of the CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="44411-126">Wykonywanie przykładowego zapytania T-SQL elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="44411-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="44411-127">Po zdefiniowaniu zewnętrznym źródle danych i tabele zewnętrzne T-SQL można teraz używać do badania tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="44411-127">Once you have defined your external data source and your external tables you can now use T-SQL to query your external tables.</span></span> <span data-ttu-id="44411-128">Wykonaj tę kwerendę w bazie danych zleceń:</span><span class="sxs-lookup"><span data-stu-id="44411-128">Execute this query on the Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="44411-129">Koszty</span><span class="sxs-lookup"><span data-stu-id="44411-129">Cost</span></span>
<span data-ttu-id="44411-130">Obecnie funkcja zapytania elastycznej bazy danych jest dostępna do kosztu bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="44411-130">Currently, the elastic database query feature is included into the cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="44411-131">Aby uzyskać informacje o cenach zobacz [cennik usługi SQL Database](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="44411-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="44411-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="44411-132">Next steps</span></span>

* <span data-ttu-id="44411-133">Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44411-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="44411-134">Dla zapytań dotyczących danych pionowo podzielonym na partycje i składnię i przykład, zobacz [zapytań w pionie na partycje danych)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="44411-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="44411-135">Samouczek poziomych partycji (dzielenia na fragmenty), zobacz [wprowadzenie elastycznej zapytania poziome partycjonowania (dzielenia na fragmenty)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="44411-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="44411-136">Dla zapytań dotyczących danych poziomie podzielonym na partycje i składnię i przykład, zobacz [zapytań w poziomie na partycje danych)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="44411-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="44411-137">Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="44411-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>