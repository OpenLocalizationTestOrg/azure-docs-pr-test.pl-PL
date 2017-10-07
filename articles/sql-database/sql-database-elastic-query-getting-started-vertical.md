---
title: "aaaGet wprowadzenie do zapytań między bazami danych (partycjonowanie pionowe) | Dokumentacja firmy Microsoft"
description: jak toouse zapytania elastycznej bazy danych w pionie na partycje baz danych
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
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="3e244-103">Wprowadzenie do zapytań między bazami danych (partycjonowanie pionowe) (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="3e244-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="3e244-104">Zapytanie elastycznej bazy danych (wersja zapoznawcza) w bazie danych SQL Azure umożliwia toorun zapytania T-SQL, obejmującej wiele baz danych przy użyciu pojedynczy punkt połączenia.</span><span class="sxs-lookup"><span data-stu-id="3e244-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="3e244-105">Ten temat dotyczy zbyt[w pionie na partycje baz danych](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="3e244-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="3e244-106">Po zakończeniu zostanie: Dowiedz się, jak tooconfigure i używanie usługi Azure SQL Database tooperform wysyła zapytanie do tego zakresu wielu powiązanych baz danych.</span><span class="sxs-lookup"><span data-stu-id="3e244-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="3e244-107">Aby uzyskać więcej informacji na temat hello elastycznej bazy danych zapytania funkcji, zobacz [bazy danych SQL Azure elastycznej bazy danych zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e244-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3e244-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3e244-108">Prerequisites</span></span>

<span data-ttu-id="3e244-109">Musi mieć uprawnienie ALTER ANY zewnętrznego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3e244-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="3e244-110">To uprawnienie jest dołączany hello uprawnienie ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="3e244-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="3e244-111">Uprawnienia ALTER ANY zewnętrznego źródła danych są wymagane toorefer toohello podstawowego źródła danych.</span><span class="sxs-lookup"><span data-stu-id="3e244-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="3e244-112">Utwórz hello przykładowe bazy danych</span><span class="sxs-lookup"><span data-stu-id="3e244-112">Create hello sample databases</span></span>
<span data-ttu-id="3e244-113">toostart z, potrzebujemy toocreate dwóch baz danych, **klientów** i **zamówień**, hello w tych samych lub różnych serwerów logicznych.</span><span class="sxs-lookup"><span data-stu-id="3e244-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="3e244-114">Wykonanie następującego zapytania na powitania hello **zamówień** hello toocreate bazy danych **OrderInformation** tabeli i dane wejściowe hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="3e244-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="3e244-115">Teraz, wykonaj następujące zapytanie na powitania **klientów** hello toocreate bazy danych **CustomerInformation** tabeli i dane wejściowe hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="3e244-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="3e244-116">Tworzenie obiektów bazy danych</span><span class="sxs-lookup"><span data-stu-id="3e244-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="3e244-117">Baza danych o zakresie klucz główny i poświadczenia</span><span class="sxs-lookup"><span data-stu-id="3e244-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="3e244-118">Otwórz program SQL Server Management Studio lub SQL Server Data Tools w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3e244-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="3e244-119">Połączenia bazy danych zamówień toohello i wykonaj hello następujące polecenia T-SQL:</span><span class="sxs-lookup"><span data-stu-id="3e244-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="3e244-120">Hello "username" i "password" powinny być hello nazwy użytkownika i hasło używane toologin do bazy danych klientom Witaj.</span><span class="sxs-lookup"><span data-stu-id="3e244-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="3e244-121">Uwierzytelnianie przy użyciu usługi Azure Active Directory z zapytaniami elastyczne nie jest obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3e244-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="3e244-122">Zewnętrzne źródła danych</span><span class="sxs-lookup"><span data-stu-id="3e244-122">External data sources</span></span>
<span data-ttu-id="3e244-123">toocreate zewnętrznego źródła danych, wykonaj następujące polecenia w bazie danych zamówień hello hello:</span><span class="sxs-lookup"><span data-stu-id="3e244-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="3e244-124">Tabele zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="3e244-124">External tables</span></span>
<span data-ttu-id="3e244-125">Tworzenie tabeli zewnętrznej w bazie danych zamówień hello, odpowiadającego hello definicji tabeli CustomerInformation hello:</span><span class="sxs-lookup"><span data-stu-id="3e244-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="3e244-126">Wykonywanie przykładowego zapytania T-SQL elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="3e244-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="3e244-127">Po zdefiniowaniu zewnętrznym źródle danych i tabel zewnętrznych można teraz używać tooquery T-SQL tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="3e244-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="3e244-128">Wykonaj tę kwerendę w bazie danych zamówień hello:</span><span class="sxs-lookup"><span data-stu-id="3e244-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="3e244-129">Koszty</span><span class="sxs-lookup"><span data-stu-id="3e244-129">Cost</span></span>
<span data-ttu-id="3e244-130">Obecnie funkcja kwerendy hello elastycznej bazy danych jest uwzględniony w koszt hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3e244-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="3e244-131">Aby uzyskać informacje o cenach zobacz [cennik usługi SQL Database](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="3e244-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3e244-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3e244-132">Next steps</span></span>

* <span data-ttu-id="3e244-133">Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3e244-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="3e244-134">Dla zapytań dotyczących danych pionowo podzielonym na partycje i składnię i przykład, zobacz [zapytań w pionie na partycje danych)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="3e244-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="3e244-135">Samouczek poziomych partycji (dzielenia na fragmenty), zobacz [wprowadzenie elastycznej zapytania poziome partycjonowania (dzielenia na fragmenty)](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="3e244-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="3e244-136">Dla zapytań dotyczących danych poziomie podzielonym na partycje i składnię i przykład, zobacz [zapytań w poziomie na partycje danych)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="3e244-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="3e244-137">Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="3e244-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>