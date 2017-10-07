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
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>Wprowadzenie do zapytań między bazami danych (partycjonowanie pionowe) (wersja zapoznawcza)
Zapytanie elastycznej bazy danych (wersja zapoznawcza) w bazie danych SQL Azure umożliwia toorun zapytania T-SQL, obejmującej wiele baz danych przy użyciu pojedynczy punkt połączenia. Ten temat dotyczy zbyt[w pionie na partycje baz danych](sql-database-elastic-query-vertical-partitioning.md).  

Po zakończeniu zostanie: Dowiedz się, jak tooconfigure i używanie usługi Azure SQL Database tooperform wysyła zapytanie do tego zakresu wielu powiązanych baz danych. 

Aby uzyskać więcej informacji na temat hello elastycznej bazy danych zapytania funkcji, zobacz [bazy danych SQL Azure elastycznej bazy danych zapytań — omówienie](sql-database-elastic-query-overview.md). 

## <a name="prerequisites"></a>Wymagania wstępne

Musi mieć uprawnienie ALTER ANY zewnętrznego źródła danych. To uprawnienie jest dołączany hello uprawnienie ALTER DATABASE. Uprawnienia ALTER ANY zewnętrznego źródła danych są wymagane toorefer toohello podstawowego źródła danych.

## <a name="create-hello-sample-databases"></a>Utwórz hello przykładowe bazy danych
toostart z, potrzebujemy toocreate dwóch baz danych, **klientów** i **zamówień**, hello w tych samych lub różnych serwerów logicznych.   

Wykonanie następującego zapytania na powitania hello **zamówień** hello toocreate bazy danych **OrderInformation** tabeli i dane wejściowe hello przykładowych danych. 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

Teraz, wykonaj następujące zapytanie na powitania **klientów** hello toocreate bazy danych **CustomerInformation** tabeli i dane wejściowe hello przykładowych danych. 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>Tworzenie obiektów bazy danych
### <a name="database-scoped-master-key-and-credentials"></a>Baza danych o zakresie klucz główny i poświadczenia
1. Otwórz program SQL Server Management Studio lub SQL Server Data Tools w programie Visual Studio.
2. Połączenia bazy danych zamówień toohello i wykonaj hello następujące polecenia T-SQL:
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    Hello "username" i "password" powinny być hello nazwy użytkownika i hasło używane toologin do bazy danych klientom Witaj.
    Uwierzytelnianie przy użyciu usługi Azure Active Directory z zapytaniami elastyczne nie jest obecnie obsługiwane.

### <a name="external-data-sources"></a>Zewnętrzne źródła danych
toocreate zewnętrznego źródła danych, wykonaj następujące polecenia w bazie danych zamówień hello hello: 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>Tabele zewnętrzne
Tworzenie tabeli zewnętrznej w bazie danych zamówień hello, odpowiadającego hello definicji tabeli CustomerInformation hello:

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Wykonywanie przykładowego zapytania T-SQL elastycznej bazy danych
Po zdefiniowaniu zewnętrznym źródle danych i tabel zewnętrznych można teraz używać tooquery T-SQL tabel zewnętrznych. Wykonaj tę kwerendę w bazie danych zamówień hello: 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>Koszty
Obecnie funkcja kwerendy hello elastycznej bazy danych jest uwzględniony w koszt hello bazy danych SQL Azure.  

Aby uzyskać informacje o cenach zobacz [cennik usługi SQL Database](https://azure.microsoft.com/pricing/details/sql-database). 

## <a name="next-steps"></a>Następne kroki

* Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).
* Dla zapytań dotyczących danych pionowo podzielonym na partycje i składnię i przykład, zobacz [zapytań w pionie na partycje danych)](sql-database-elastic-query-vertical-partitioning.md)
* Samouczek poziomych partycji (dzielenia na fragmenty), zobacz [wprowadzenie elastycznej zapytania poziome partycjonowania (dzielenia na fragmenty)](sql-database-elastic-query-getting-started.md).
* Dla zapytań dotyczących danych poziomie podzielonym na partycje i składnię i przykład, zobacz [zapytań w poziomie na partycje danych)](sql-database-elastic-query-horizontal-partitioning.md)
* Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.