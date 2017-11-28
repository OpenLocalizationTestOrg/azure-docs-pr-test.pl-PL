---
title: aaaRestore magazyn danych SQL Azure (interfejsu API REST) | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="91fa7-103">Przywróć magazyn danych Azure SQL (interfejsu API REST)</span><span class="sxs-lookup"><span data-stu-id="91fa7-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="91fa7-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="91fa7-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="91fa7-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="91fa7-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="91fa7-106">[Środowiska PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="91fa7-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="91fa7-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="91fa7-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="91fa7-108">W tym artykule dowiesz się, jak za pomocą usługi Azure SQL Data Warehouse toorestore hello interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="91fa7-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="91fa7-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="91fa7-109">Before you begin</span></span>
<span data-ttu-id="91fa7-110">**Sprawdź, czy pojemność jednostek dtu w warstwie.**</span><span class="sxs-lookup"><span data-stu-id="91fa7-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="91fa7-111">Każdy magazyn danych SQL jest obsługiwana przez serwer SQL (np. myserver.database.windows.net), który ma domyślnego przydziału jednostek dtu w warstwie.</span><span class="sxs-lookup"><span data-stu-id="91fa7-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="91fa7-112">Zanim będzie można przywrócić SQL Data Warehouse, sprawdź tego hello programu SQL server ma wystarczająco pozostałych limit przydziału jednostek DTU dla przywracanej hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="91fa7-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="91fa7-113">toolearn jak potrzebne toocalculate DTU lub toorequest więcej jednostek dtu w warstwie, zobacz [żądanie zmiany limitu przydziału jednostek dtu w warstwie][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="91fa7-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="91fa7-114">Przywróć bazę danych aktywnej lub wstrzymana</span><span class="sxs-lookup"><span data-stu-id="91fa7-114">Restore an active or paused database</span></span>
<span data-ttu-id="91fa7-115">toorestore bazy danych:</span><span class="sxs-lookup"><span data-stu-id="91fa7-115">toorestore a database:</span></span>

1. <span data-ttu-id="91fa7-116">Pobierz listę hello przy użyciu operacji punkty przywracania bazy danych Get hello punkty przywracania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="91fa7-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="91fa7-117">Rozpocznij przywracania przy użyciu hello [żądanie przywracania bazy danych utwórz] [ Create database restore request] operacji.</span><span class="sxs-lookup"><span data-stu-id="91fa7-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="91fa7-118">Śledzić stan hello przywracania za pomocą hello [operacji stan bazy danych] [ Database operation status] operacji.</span><span class="sxs-lookup"><span data-stu-id="91fa7-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="91fa7-119">Po ukończeniu przywracania hello można skonfigurować odzyskanej bazy danych, wykonując [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="91fa7-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="91fa7-120">Przywracanie usuniętej bazy danych</span><span class="sxs-lookup"><span data-stu-id="91fa7-120">Restore a deleted database</span></span>
<span data-ttu-id="91fa7-121">toorestore usuniętej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="91fa7-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="91fa7-122">Lista wszystkich dostępnych usuniętych baz danych przy użyciu hello [listy dostępnych porzucić bazy danych] [ List restorable dropped databases] operacji.</span><span class="sxs-lookup"><span data-stu-id="91fa7-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="91fa7-123">Uzyskiwanie szczegółów hello hello usunięte bazy danych ma toorestore przy użyciu hello [Get dostępnych porzucić bazy danych] [ Get restorable dropped database] operacji.</span><span class="sxs-lookup"><span data-stu-id="91fa7-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="91fa7-124">Rozpocznij przywracania przy użyciu hello [żądanie przywracania bazy danych utwórz] [ Create database restore request] operacji.</span><span class="sxs-lookup"><span data-stu-id="91fa7-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="91fa7-125">Śledzić stan hello przywracania za pomocą hello [operacji stan bazy danych] [ Database operation status] operacji.</span><span class="sxs-lookup"><span data-stu-id="91fa7-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="91fa7-126">Zobacz bazy danych po zakończeniu przywracania hello tooconfigure [konfiguracji bazy danych po odzyskaniu][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="91fa7-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="91fa7-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91fa7-127">Next steps</span></span>
<span data-ttu-id="91fa7-128">toolearn o funkcjach ciągłości biznesowej hello wersji bazy danych SQL Azure, przeczytaj hello [omówienie ciągłości działalności biznesowej usługi Azure SQL Database][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="91fa7-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
