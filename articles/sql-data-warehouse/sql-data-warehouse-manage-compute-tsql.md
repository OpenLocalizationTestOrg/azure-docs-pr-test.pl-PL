---
title: "Wstrzymać, wznowić, skalować T-SQL w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Na wydajność skalowania w poziomie przez dostosowanie wartości dwu zadań Transact-SQL (T-SQL). Zmniejszyć koszty przez skalowanie w trakcie godziny poza szczytem."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 9221d72ecf8ab2ba8b04e4bc97eeef7157817cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="d9c92-104">Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="d9c92-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9c92-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d9c92-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="d9c92-106">Portal</span><span class="sxs-lookup"><span data-stu-id="d9c92-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="d9c92-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9c92-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="d9c92-108">REST</span><span class="sxs-lookup"><span data-stu-id="d9c92-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="d9c92-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="d9c92-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="d9c92-110">Wyświetl bieżące ustawienia Jednostka DWU</span><span class="sxs-lookup"><span data-stu-id="d9c92-110">View current DWU settings</span></span>
<span data-ttu-id="d9c92-111">Aby wyświetlić bieżące ustawienia DWU baz danych:</span><span class="sxs-lookup"><span data-stu-id="d9c92-111">To view the current DWU settings for your databases:</span></span>

1. <span data-ttu-id="d9c92-112">Otwórz Eksplorator obiektów SQL Server w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9c92-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="d9c92-113">Połączenia z bazą danych master, skojarzone z serwera logicznego bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d9c92-113">Connect to the master database associated with the logical SQL Database server.</span></span>
3. <span data-ttu-id="d9c92-114">Wybierz z sys.database_service_objectives dynamiczny widok zarządzania.</span><span class="sxs-lookup"><span data-stu-id="d9c92-114">Select from the sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="d9c92-115">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="d9c92-115">Here is an example:</span></span> 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="d9c92-116">Skalowanie możliwości obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="d9c92-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="d9c92-117">Aby zmienić liczbę jednostek dwu:</span><span class="sxs-lookup"><span data-stu-id="d9c92-117">To change the DWUs:</span></span>

1. <span data-ttu-id="d9c92-118">Połączenia z bazą danych master, skojarzona z serwerem logicznym bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d9c92-118">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="d9c92-119">Użyj [ALTER DATABASE] [ ALTER DATABASE] instrukcji TSQL.</span><span class="sxs-lookup"><span data-stu-id="d9c92-119">Use the [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="d9c92-120">Poniższy przykład ustawia cel poziomu usługi DW1000 MySQLDW bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d9c92-120">The following example sets the service level objective to DW1000 for the database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="d9c92-121">Sprawdzić postęp stanu oraz operacji bazy danych</span><span class="sxs-lookup"><span data-stu-id="d9c92-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="d9c92-122">Połączenia z bazą danych master, skojarzona z serwerem logicznym bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d9c92-122">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="d9c92-123">Przesyłać zapytania, aby sprawdzić stan bazy danych</span><span class="sxs-lookup"><span data-stu-id="d9c92-123">Submit query to check database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="d9c92-124">Przesyłać zapytania, aby sprawdzić stan operacji</span><span class="sxs-lookup"><span data-stu-id="d9c92-124">Submit query to check status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="d9c92-125">Ten widok DMV zwraca informacje o różnych operacji zarządzania na usługą SQL Data Warehouse, takie jak operacji i stan operacji, która będzie IN_PROGRESS lub UKOŃCZONA.</span><span class="sxs-lookup"><span data-stu-id="d9c92-125">This DMV will return information about various management operations on your SQL Data Warehouse such as the operation and the state of the operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="d9c92-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9c92-126">Next steps</span></span>
<span data-ttu-id="d9c92-127">Inne zadania zarządzania, zobacz [omówienie zarządzania][Management overview].</span><span class="sxs-lookup"><span data-stu-id="d9c92-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
