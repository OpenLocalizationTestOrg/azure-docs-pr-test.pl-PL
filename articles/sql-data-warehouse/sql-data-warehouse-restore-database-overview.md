---
title: "Magazyn danych Azure — lokalnych i geograficznie nadmiarowego aaaRestore | Dokumentacja firmy Microsoft"
description: "Przegląd hello opcje przywracania bazy danych do przywrócenia bazy danych w magazynie danych SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="a1ebf-103">Przywrócenie magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="a1ebf-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a1ebf-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="a1ebf-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="a1ebf-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="a1ebf-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="a1ebf-106">[Środowiska PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a1ebf-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="a1ebf-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="a1ebf-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="a1ebf-108">Usługi SQL Data Warehouse umożliwia zarówno lokalnych, jak i geograficzne jego awarii magazynu danych w ramach odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="a1ebf-109">Użyj toorestore przywracania tooa magazynu danych do punktu w regionie podstawowym hello, lub użyj innego regionu geograficznego geograficznie nadmiarowego kopii zapasowych toorestore tooa kopii zapasowych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="a1ebf-110">W tym artykule opisano specyfice hello przywrócenie magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="a1ebf-111">Co to jest przywrócenie magazynu danych?</span><span class="sxs-lookup"><span data-stu-id="a1ebf-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="a1ebf-112">Przywrócenie magazynu danych jest nowy magazyn danych, która jest tworzona na podstawie istniejącej kopii zapasowej lub usunięte dane magazynu.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="a1ebf-113">Magazyn danych przywróconej Hello ponownie tworzy hello magazynu kopii zapasowej danych w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="a1ebf-114">Ponieważ Magazyn danych SQL to Rozproszony system, przywracania magazynu danych jest tworzony z wielu plików kopii zapasowej, które są przechowywane w obiektach blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="a1ebf-115">Przywracanie bazy danych jest integralną część każdej strategii odzyskiwania biznesowych, jak ciągłości i odzyskiwaniem po awarii, ponieważ ponownie tworzy dane po przypadkowym uszkodzenia lub usunięcia.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="a1ebf-116">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="a1ebf-116">For more information, see:</span></span>

* [<span data-ttu-id="a1ebf-117">Tworzenie kopii zapasowych SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a1ebf-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="a1ebf-118">Omówienie ciągłości działalności biznesowej</span><span class="sxs-lookup"><span data-stu-id="a1ebf-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="a1ebf-119">Punkty przywracania magazynu danych</span><span class="sxs-lookup"><span data-stu-id="a1ebf-119">Data warehouse restore points</span></span>
<span data-ttu-id="a1ebf-120">Jako korzyścią z używania usługi Azure Premium Storage SQL Data Warehouse używa obiektu Blob magazynu Azure migawki toobackup hello danych podstawowych magazynu.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="a1ebf-121">Każda migawka ma punkt przywracania, który reprezentuje czas hello migawki hello uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="a1ebf-122">toorestore hurtowni danych, wybierz punkt przywracania i wydać polecenie restore.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="a1ebf-123">Usługi SQL Data Warehouse zawsze przywraca hello kopii zapasowej tooa nowego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="a1ebf-124">Można albo Zachowaj hello przywróconych danych magazyn i hello bieżącą lub usuń jedno z nich.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="a1ebf-125">Jeśli chcesz tooreplace hello bieżąca data warehouse przy użyciu hello przywrócić magazynu danych, zmień jego nazwę.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="a1ebf-126">Jeśli potrzebujesz toorestore hurtowni danych usuniętych lub wstrzymana, możesz [Utwórz bilet pomocy technicznej](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="a1ebf-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="a1ebf-127">Przywracanie geograficznie nadmiarowego</span><span class="sxs-lookup"><span data-stu-id="a1ebf-127">Geo-redundant restore</span></span>
<span data-ttu-id="a1ebf-128">Można przywrócić obsługujący magazyn danych SQL Azure o takim samym poziomie wydajności wybranego regionu tooany magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="a1ebf-129">Należy pamiętać, że DWU 9000 i 18000 nie są obsługiwane we wszystkich regionach hello w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="a1ebf-130">Przywracanie tooperform geograficznie nadmiarowego, który musi nie rezygnujesz z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="a1ebf-131">Przywróć osi czasu</span><span class="sxs-lookup"><span data-stu-id="a1ebf-131">Restore timeline</span></span>
<span data-ttu-id="a1ebf-132">Punkt przywracania dostępne tooany bazy danych w ramach hello można przywrócić w ostatnich siedmiu dni.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="a1ebf-133">Migawki Uruchom co cztery godziny tooeight i są dostępne na siedem dni.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="a1ebf-134">Gdy migawka jest starsza niż siedmiu dni, wygaśnie i jego punktu przywracania nie jest już dostępny.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="a1ebf-135">Przywróć kosztów</span><span class="sxs-lookup"><span data-stu-id="a1ebf-135">Restore costs</span></span>
<span data-ttu-id="a1ebf-136">jest on rozliczany Hello opłat magazynu dla magazynu danych przywróconych hello szybkością hello Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="a1ebf-137">Jeśli magazynu przywróconych danych zostanie wstrzymana, są naliczane opłaty za magazyn szybkością hello Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="a1ebf-138">Zaletą Hello wstrzymanie jest nie są naliczane opłaty dla zasobów obliczeniowych hello DWU.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="a1ebf-139">Aby uzyskać więcej informacji na temat cen usługi SQL Data Warehouse, zobacz [cennik usługi SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="a1ebf-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="a1ebf-140">Używa do odtworzenia</span><span class="sxs-lookup"><span data-stu-id="a1ebf-140">Uses for restore</span></span>
<span data-ttu-id="a1ebf-141">podstawowym zastosowaniem Hello przywracania magazynu danych jest toorecover danych po przypadkowej utraty danych lub uszkodzenia.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="a1ebf-142">Umożliwia także tooretain przywracania magazynu danych kopii zapasowej przez ponad siedem dni.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="a1ebf-143">Po przywróceniu kopii zapasowej hello, masz hello magazynu danych online i można wstrzymać go przez nieograniczony czas toosave obliczeń kosztów.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="a1ebf-144">opłaty za magazyn szybkością hello Azure Premium Storage wiąże się z Hello wstrzymania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a1ebf-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="a1ebf-145">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="a1ebf-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="a1ebf-146">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="a1ebf-146">Scenarios</span></span>
* <span data-ttu-id="a1ebf-147">Omówienie ciągłości działalności, można zobaczyć [omówienie ciągłości działalności biznesowej](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="a1ebf-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="a1ebf-148">tooperform hurtowni danych przywrócenie, przywracania przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="a1ebf-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="a1ebf-149">Azure portalu, zobacz [przywrócić hurtowni danych przy użyciu hello portalu Azure](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a1ebf-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="a1ebf-150">Polecenia cmdlet programu PowerShell, zobacz [przywrócić hurtowni danych przy użyciu poleceń cmdlet programu PowerShell](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a1ebf-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="a1ebf-151">Interfejsy API REST, zobacz [przywrócić hurtowni danych przy użyciu hello interfejsów API REST](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="a1ebf-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
