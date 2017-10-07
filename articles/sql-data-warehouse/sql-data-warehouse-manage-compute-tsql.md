---
title: "aaaPause, wznowić, skalować T-SQL w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Transact-SQL (T-SQL) zadań poza tooscale wydajności przez dostosowanie wartości dwu. Zmniejszyć koszty przez skalowanie w trakcie godziny poza szczytem."
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
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="04180-104">Zarządzanie moc obliczeniową w usłudze Azure SQL Data Warehouse (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="04180-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="04180-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="04180-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="04180-106">Portal</span><span class="sxs-lookup"><span data-stu-id="04180-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="04180-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="04180-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="04180-108">REST</span><span class="sxs-lookup"><span data-stu-id="04180-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="04180-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="04180-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="04180-110">Wyświetl bieżące ustawienia Jednostka DWU</span><span class="sxs-lookup"><span data-stu-id="04180-110">View current DWU settings</span></span>
<span data-ttu-id="04180-111">tooview hello bieżącej wartości DWU ustawienia dla baz danych:</span><span class="sxs-lookup"><span data-stu-id="04180-111">tooview hello current DWU settings for your databases:</span></span>

1. <span data-ttu-id="04180-112">Otwórz Eksplorator obiektów SQL Server w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04180-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="04180-113">Połączenie skojarzone z serwera logicznego bazy danych SQL hello bazy danych master toohello.</span><span class="sxs-lookup"><span data-stu-id="04180-113">Connect toohello master database associated with hello logical SQL Database server.</span></span>
3. <span data-ttu-id="04180-114">Wybierz z hello sys.database_service_objectives dynamiczny widok zarządzania.</span><span class="sxs-lookup"><span data-stu-id="04180-114">Select from hello sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="04180-115">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="04180-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="04180-116">Skalowanie możliwości obliczeniowych</span><span class="sxs-lookup"><span data-stu-id="04180-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="04180-117">Witaj toochange jednostek dwu:</span><span class="sxs-lookup"><span data-stu-id="04180-117">toochange hello DWUs:</span></span>

1. <span data-ttu-id="04180-118">Połączenie skojarzone z serwera logicznego bazy danych SQL bazy danych master toohello.</span><span class="sxs-lookup"><span data-stu-id="04180-118">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="04180-119">Użyj hello [ALTER DATABASE] [ ALTER DATABASE] instrukcji TSQL.</span><span class="sxs-lookup"><span data-stu-id="04180-119">Use hello [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="04180-120">Witaj poniższy przykład przedstawia hello usługi poziomu celu tooDW1000 dla bazy danych hello MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="04180-120">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="04180-121">Sprawdzić postęp stanu oraz operacji bazy danych</span><span class="sxs-lookup"><span data-stu-id="04180-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="04180-122">Połączenie skojarzone z serwera logicznego bazy danych SQL bazy danych master toohello.</span><span class="sxs-lookup"><span data-stu-id="04180-122">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="04180-123">Przedstawia stan bazy danych toocheck zapytania</span><span class="sxs-lookup"><span data-stu-id="04180-123">Submit query toocheck database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="04180-124">Przedstawia stan toocheck zapytania operacji</span><span class="sxs-lookup"><span data-stu-id="04180-124">Submit query toocheck status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="04180-125">Ten widok DMV zwraca informacje o różnych operacji zarządzania na usługą SQL Data Warehouse, takich jak stan operacji i hello hello hello operacja, która będzie IN_PROGRESS lub UKOŃCZONA.</span><span class="sxs-lookup"><span data-stu-id="04180-125">This DMV will return information about various management operations on your SQL Data Warehouse such as hello operation and hello state of hello operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="04180-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04180-126">Next steps</span></span>
<span data-ttu-id="04180-127">Inne zadania zarządzania, zobacz [omówienie zarządzania][Management overview].</span><span class="sxs-lookup"><span data-stu-id="04180-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
