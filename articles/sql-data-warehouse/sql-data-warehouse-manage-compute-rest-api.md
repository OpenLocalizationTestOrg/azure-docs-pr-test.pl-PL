---
title: "aaaPause, wznowić, skalować REST w usłudze Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Zarządzanie moc obliczeniową w usłudze SQL Data Warehouse REST, T-SQL i programu PowerShell."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 21de7337-9356-49bb-a6eb-06c1beeba2c4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 07/25/2017
ms.author: elbutter
ms.openlocfilehash: fc867febb118fb5c86c2637a41b232076021b95d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a><span data-ttu-id="68be3-103">Zarządzanie energią obliczeniowych w magazynie danych SQL Azure (REST)</span><span class="sxs-lookup"><span data-stu-id="68be3-103">Manage compute power in Azure SQL Data Warehouse (REST)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="68be3-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="68be3-104">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="68be3-105">Portal</span><span class="sxs-lookup"><span data-stu-id="68be3-105">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="68be3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="68be3-106">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="68be3-107">REST</span><span class="sxs-lookup"><span data-stu-id="68be3-107">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="68be3-108">TSQL</span><span class="sxs-lookup"><span data-stu-id="68be3-108">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="68be3-109">Moc obliczeniową skali</span><span class="sxs-lookup"><span data-stu-id="68be3-109">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="68be3-110">Witaj toochange jednostek dwu, użyj hello [Tworzenie lub aktualizacja bazy danych] [ Create or Update Database] interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="68be3-110">toochange hello DWUs, use hello [Create or Update Database][Create or Update Database] REST API.</span></span> <span data-ttu-id="68be3-111">Witaj poniższy przykład przedstawia hello usługi poziomu celu tooDW1000 dla bazy danych hello MySQLDW, która jest hostowana na serwerze MyServer.</span><span class="sxs-lookup"><span data-stu-id="68be3-111">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW which is hosted on server MyServer.</span></span> <span data-ttu-id="68be3-112">Serwer Hello jest w grupie zasobów platformy Azure o nazwie ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="68be3-112">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
PATCH https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01-preview HTTP/1.1
Content-Type: application/json; charset=UTF-8

{
    "properties": {
        "requestedServiceObjectiveName": DW1000
    }
}
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="68be3-113">Wstrzymaj obliczeń</span><span class="sxs-lookup"><span data-stu-id="68be3-113">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="68be3-114">toopause bazy danych, użyj hello [bazy danych wstrzymania] [ Pause Database] interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="68be3-114">toopause a database, use hello [Pause Database][Pause Database] REST API.</span></span> <span data-ttu-id="68be3-115">Witaj poniższy przykład wstrzymuje bazy danych o nazwie Database02 znajdującej się na serwerze o nazwie Serwer01.</span><span class="sxs-lookup"><span data-stu-id="68be3-115">hello following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="68be3-116">Serwer Hello jest w grupie zasobów platformy Azure o nazwie ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="68be3-116">hello server is in an Azure resource group named ResourceGroup1.</span></span>

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="68be3-117">Wznów obliczeń</span><span class="sxs-lookup"><span data-stu-id="68be3-117">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="68be3-118">toostart bazy danych, użyj hello [wznowienia bazy danych] [ Resume Database] interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="68be3-118">toostart a database, use hello [Resume Database][Resume Database] REST API.</span></span> <span data-ttu-id="68be3-119">Witaj poniższy przykład uruchamia bazy danych o nazwie Database02 znajdującej się na serwerze o nazwie Serwer01.</span><span class="sxs-lookup"><span data-stu-id="68be3-119">hello following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="68be3-120">Serwer Hello jest w grupie zasobów platformy Azure o nazwie ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="68be3-120">hello server is in an Azure resource group named ResourceGroup1.</span></span> 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a><span data-ttu-id="68be3-121">Sprawdź stan bazy danych</span><span class="sxs-lookup"><span data-stu-id="68be3-121">Check database state</span></span>

```
GET https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Sql/servers/{server-name}/databases/{database-name}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="68be3-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="68be3-122">Next steps</span></span>
<span data-ttu-id="68be3-123">Inne zadania zarządzania, zobacz [omówienie zarządzania][Management overview].</span><span class="sxs-lookup"><span data-stu-id="68be3-123">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Pause Database]: https://msdn.microsoft.com/library/azure/mt718817.aspx
[Resume Database]: https://msdn.microsoft.com/library/azure/mt718820.aspx
[Create or Update Database]: https://msdn.microsoft.com/library/azure/mt163685.aspx

<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
