---
title: "aaaCreate SQL Data Warehouse przy użyciu języka TSQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Azure SQL Data Warehouse przy użyciu języka TSQL"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a>Tworzenie bazy danych w usłudze SQL Data Warehouse przy użyciu języka Transact-SQL (TSQL)
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

W tym artykule opisano, jak toocreate SQL Data Warehouse przy użyciu T-SQL.

## <a name="prerequisites"></a>Wymagania wstępne
Rozpoczęto tooget, potrzebne są:

* **Konto platformy Azure**: odwiedź [bezpłatnej wersji próbnej Azure] [ Azure Free Trial] lub [MSDN Azure środków] [ MSDN Azure Credits] toocreate konta.
* **Serwer SQL Azure**: Zobacz [tworzenie serwera logicznego bazy danych SQL Azure z hello Azure Portal] [tworzenie serwera logicznego bazy danych SQL Azure z hello Azure Portal] lub [tworzenie serwera logicznego bazy danych SQL Azure przy użyciu programu PowerShell] [Utwórz Azure SQL Serwera logicznego bazy danych przy użyciu programu PowerShell] Aby uzyskać więcej informacji.
* **Grupa zasobów**: Użyj hello zasobów w tej samej grupy jako serwer Azure SQL, lub zobacz [jak toocreate grupę zasobów][how toocreate a resource group].
* **Środowisko tooexecute T-SQL**: można użyć [programu Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], lub [SSMS] [ SSMS] tooexecute T-SQL.

> [!NOTE]
> Utworzenie bazy danych w usłudze SQL Data Warehouse może skutkować powstaniem nowej usługi płatnej.  Aby uzyskać więcej informacji o cenach, zobacz [Cennik usługi SQL Data Warehouse][SQL Data Warehouse pricing].
>
>

## <a name="create-a-database-with-visual-studio"></a>Tworzenie bazy danych przy użyciu programu Visual Studio
Jeśli nowy tooVisual Studio, zobacz artykuł hello [zapytań usługi Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].  toostart, Otwórz Eksplorator obiektów SQL Server w programie Visual Studio i połącz toohello serwera, który będzie hostem bazy danych SQL Data Warehouse.  Po nawiązaniu połączenia można utworzyć magazynu danych SQL, uruchamiając następujące polecenie SQL przed hello hello **wzorca** bazy danych.  To polecenie tworzy hello bazy danych MySqlDwDb z celem usługi DW400 i umożliwić hello bazy danych toogrow tooa maksymalnego rozmiaru 10 TB.

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a>Tworzenie bazy danych przy użyciu narzędzia sqlcmd
Alternatywnie możesz uruchomić hello hello tego samego polecenia przy użyciu narzędzia sqlcmd, uruchamiając następujące polecenie w wierszu polecenia.

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

Sortowanie domyślne Hello, gdy nie określono jest sortowania SQL_Latin1_General_CP1_CI_AS.  Witaj `MAXSIZE` może mieć wartość od 250 GB do 240 TB.  Witaj `SERVICE_OBJECTIVE` może mieć wartość od DW100 do DW2000 [DWU][DWU].  Lista wszystkich prawidłowych wartości dokumentacji hello MSDN dla [CREATE DATABASE][CREATE DATABASE].  Zarówno hello MAXSIZE i SERVICE_OBJECTIVE może zostać zmieniony z [ALTER DATABASE] [ ALTER DATABASE] polecenia T-SQL.  Witaj sortowania bazy danych nie można zmienić po jego utworzeniu.   Należy zachować ostrożność podczas zmieniania hello SERVICE_OBJECTIVE podczas zmieniania DWU powoduje ponowne uruchomienie usług, który anuluje wszystkie bieżące zapytania.  Zmiana parametru MAXSIZE nie powoduje ponownego uruchamiania usług, ponieważ jest to tylko prosta operacja na metadanych.

## <a name="next-steps"></a>Następne kroki
Po zakończeniu SQL Data Warehouse inicjowania obsługi można [załadować przykładowe dane] [ load sample data] lub zbyt poznać sposób[opracowanie][develop], [załadować][load], lub [migracji][migrate].

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
