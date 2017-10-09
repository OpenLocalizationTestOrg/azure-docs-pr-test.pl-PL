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
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="96896-103">Tworzenie bazy danych w usłudze SQL Data Warehouse przy użyciu języka Transact-SQL (TSQL)</span><span class="sxs-lookup"><span data-stu-id="96896-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96896-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="96896-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="96896-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="96896-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="96896-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="96896-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="96896-107">W tym artykule opisano, jak toocreate SQL Data Warehouse przy użyciu T-SQL.</span><span class="sxs-lookup"><span data-stu-id="96896-107">This article shows you how toocreate a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96896-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="96896-108">Prerequisites</span></span>
<span data-ttu-id="96896-109">Rozpoczęto tooget, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="96896-109">tooget started, you need:</span></span>

* <span data-ttu-id="96896-110">**Konto platformy Azure**: odwiedź [bezpłatnej wersji próbnej Azure] [ Azure Free Trial] lub [MSDN Azure środków] [ MSDN Azure Credits] toocreate konta.</span><span class="sxs-lookup"><span data-stu-id="96896-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="96896-111">**Serwer SQL Azure**: Zobacz [tworzenie serwera logicznego bazy danych SQL Azure z hello Azure Portal] [tworzenie serwera logicznego bazy danych SQL Azure z hello Azure Portal] lub [tworzenie serwera logicznego bazy danych SQL Azure przy użyciu programu PowerShell] [Utwórz Azure SQL Serwera logicznego bazy danych przy użyciu programu PowerShell] Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="96896-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with hello Azure Portal][Create an Azure SQL Database logical server with hello Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="96896-112">**Grupa zasobów**: Użyj hello zasobów w tej samej grupy jako serwer Azure SQL, lub zobacz [jak toocreate grupę zasobów][how toocreate a resource group].</span><span class="sxs-lookup"><span data-stu-id="96896-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group][how toocreate a resource group].</span></span>
* <span data-ttu-id="96896-113">**Środowisko tooexecute T-SQL**: można użyć [programu Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], lub [SSMS] [ SSMS] tooexecute T-SQL.</span><span class="sxs-lookup"><span data-stu-id="96896-113">**Environment tooexecute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] tooexecute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="96896-114">Utworzenie bazy danych w usłudze SQL Data Warehouse może skutkować powstaniem nowej usługi płatnej.</span><span class="sxs-lookup"><span data-stu-id="96896-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="96896-115">Aby uzyskać więcej informacji o cenach, zobacz [Cennik usługi SQL Data Warehouse][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="96896-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="96896-116">Tworzenie bazy danych przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="96896-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="96896-117">Jeśli nowy tooVisual Studio, zobacz artykuł hello [zapytań usługi Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="96896-117">If you are new tooVisual Studio, see hello article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="96896-118">toostart, Otwórz Eksplorator obiektów SQL Server w programie Visual Studio i połącz toohello serwera, który będzie hostem bazy danych SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="96896-118">toostart, open SQL Server Object Explorer in Visual Studio and connect toohello server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="96896-119">Po nawiązaniu połączenia można utworzyć magazynu danych SQL, uruchamiając następujące polecenie SQL przed hello hello **wzorca** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="96896-119">Once connected, you can create a SQL Data Warehouse by running hello following SQL command against hello **master** database.</span></span>  <span data-ttu-id="96896-120">To polecenie tworzy hello bazy danych MySqlDwDb z celem usługi DW400 i umożliwić hello bazy danych toogrow tooa maksymalnego rozmiaru 10 TB.</span><span class="sxs-lookup"><span data-stu-id="96896-120">This command creates hello database MySqlDwDb with a Service Objective of DW400 and allow hello database toogrow tooa maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="96896-121">Tworzenie bazy danych przy użyciu narzędzia sqlcmd</span><span class="sxs-lookup"><span data-stu-id="96896-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="96896-122">Alternatywnie możesz uruchomić hello hello tego samego polecenia przy użyciu narzędzia sqlcmd, uruchamiając następujące polecenie w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="96896-122">Alternatively, you can run hello same command with sqlcmd by running hello following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="96896-123">Sortowanie domyślne Hello, gdy nie określono jest sortowania SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="96896-123">hello default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="96896-124">Witaj `MAXSIZE` może mieć wartość od 250 GB do 240 TB.</span><span class="sxs-lookup"><span data-stu-id="96896-124">hello `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="96896-125">Witaj `SERVICE_OBJECTIVE` może mieć wartość od DW100 do DW2000 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="96896-125">hello `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="96896-126">Lista wszystkich prawidłowych wartości dokumentacji hello MSDN dla [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="96896-126">For a list of all valid values, see hello MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="96896-127">Zarówno hello MAXSIZE i SERVICE_OBJECTIVE może zostać zmieniony z [ALTER DATABASE] [ ALTER DATABASE] polecenia T-SQL.</span><span class="sxs-lookup"><span data-stu-id="96896-127">Both hello MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="96896-128">Witaj sortowania bazy danych nie można zmienić po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="96896-128">hello collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="96896-129">Należy zachować ostrożność podczas zmieniania hello SERVICE_OBJECTIVE podczas zmieniania DWU powoduje ponowne uruchomienie usług, który anuluje wszystkie bieżące zapytania.</span><span class="sxs-lookup"><span data-stu-id="96896-129">Caution should be used when changing hello SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="96896-130">Zmiana parametru MAXSIZE nie powoduje ponownego uruchamiania usług, ponieważ jest to tylko prosta operacja na metadanych.</span><span class="sxs-lookup"><span data-stu-id="96896-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96896-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96896-131">Next steps</span></span>
<span data-ttu-id="96896-132">Po zakończeniu SQL Data Warehouse inicjowania obsługi można [załadować przykładowe dane] [ load sample data] lub zbyt poznać sposób[opracowanie][develop], [załadować][load], lub [migracji][migrate].</span><span class="sxs-lookup"><span data-stu-id="96896-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

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
