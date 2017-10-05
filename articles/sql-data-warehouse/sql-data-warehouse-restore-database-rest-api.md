---
title: "Przywróć magazyn danych Azure SQL (interfejsu API REST) | Dokumentacja firmy Microsoft"
description: "Interfejs API REST zadania przywracania usługi Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 8656607611e7518e42b51b91774f55abec15c228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="83df9-103">Przywróć magazyn danych Azure SQL (interfejsu API REST)</span><span class="sxs-lookup"><span data-stu-id="83df9-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="83df9-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="83df9-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="83df9-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="83df9-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="83df9-106">[Środowiska PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="83df9-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="83df9-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="83df9-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="83df9-108">W tym artykule dowiesz się, jak przywrócić Azure SQL Data Warehouse przy użyciu interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="83df9-108">In this article you will learn how to restore an Azure SQL Data Warehouse using the REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="83df9-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="83df9-109">Before you begin</span></span>
<span data-ttu-id="83df9-110">**Sprawdź, czy pojemność jednostek dtu w warstwie.**</span><span class="sxs-lookup"><span data-stu-id="83df9-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="83df9-111">Każdy magazyn danych SQL jest obsługiwana przez serwer SQL (np. myserver.database.windows.net), który ma domyślnego przydziału jednostek dtu w warstwie.</span><span class="sxs-lookup"><span data-stu-id="83df9-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="83df9-112">Zanim będzie można przywrócić magazyn danych SQL, upewnij się, że program SQL server ma wystarczającą ilość pozostałych limit przydziału jednostek DTU dla przywracanej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="83df9-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="83df9-113">Aby dowiedzieć się, jak można obliczyć jednostek dtu w warstwie potrzebne również z prośbami więcej jednostek dtu w warstwie, zobacz [żądanie zmiany limitu przydziału jednostek dtu w warstwie][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="83df9-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="83df9-114">Przywróć bazę danych aktywnej lub wstrzymana</span><span class="sxs-lookup"><span data-stu-id="83df9-114">Restore an active or paused database</span></span>
<span data-ttu-id="83df9-115">Przywracanie bazy danych:</span><span class="sxs-lookup"><span data-stu-id="83df9-115">To restore a database:</span></span>

1. <span data-ttu-id="83df9-116">Pobierz listę punktów przywracania bazy danych przy użyciu operacji punkty przywracania bazy danych Get.</span><span class="sxs-lookup"><span data-stu-id="83df9-116">Get the list of database restore points using the Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="83df9-117">Rozpocznij przywracania przy użyciu [żądanie przywracania bazy danych utwórz] [ Create database restore request] operacji.</span><span class="sxs-lookup"><span data-stu-id="83df9-117">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="83df9-118">Śledź stan przywracania przy użyciu [operacji stan bazy danych] [ Database operation status] operacji.</span><span class="sxs-lookup"><span data-stu-id="83df9-118">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="83df9-119">Po ukończeniu przywracania można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="83df9-119">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="83df9-120">Przywracanie usuniętej bazy danych</span><span class="sxs-lookup"><span data-stu-id="83df9-120">Restore a deleted database</span></span>
<span data-ttu-id="83df9-121">Aby przywrócić usunięte bazy danych:</span><span class="sxs-lookup"><span data-stu-id="83df9-121">To restore a deleted database:</span></span>

1. <span data-ttu-id="83df9-122">Lista wszystkich dostępnych usuniętych baz danych przy użyciu [listy dostępnych porzucić bazy danych] [ List restorable dropped databases] operacji.</span><span class="sxs-lookup"><span data-stu-id="83df9-122">List all of your restorable deleted databases by using the [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="83df9-123">Szczegółowe informacje dla usuniętej bazy danych, aby przywrócić za pomocą [Get dostępnych porzucić bazy danych] [ Get restorable dropped database] operacji.</span><span class="sxs-lookup"><span data-stu-id="83df9-123">Get the details for the deleted database you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="83df9-124">Rozpocznij przywracania przy użyciu [żądanie przywracania bazy danych utwórz] [ Create database restore request] operacji.</span><span class="sxs-lookup"><span data-stu-id="83df9-124">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="83df9-125">Śledź stan przywracania przy użyciu [operacji stan bazy danych] [ Database operation status] operacji.</span><span class="sxs-lookup"><span data-stu-id="83df9-125">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="83df9-126">Aby skonfigurować bazę danych, po ukończeniu przywracania, zobacz [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="83df9-126">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="83df9-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="83df9-127">Next steps</span></span>
<span data-ttu-id="83df9-128">Aby dowiedzieć się więcej o funkcjach ciągłości biznesowej wersji bazy danych SQL Azure, przeczytaj [omówienie ciągłości działalności biznesowej usługi Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="83df9-128">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
