---
title: "Przywracanie magazynu danych Azure — lokalnych i geograficznie nadmiarowego | Dokumentacja firmy Microsoft"
description: "Omówienie opcji przywracania bazy danych do przywrócenia bazy danych w magazynie danych SQL Azure."
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
ms.openlocfilehash: ea42b7135d0695b66d569095e70bb3d9f8b9594b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="27d34-103">Przywrócenie magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="27d34-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="27d34-104">[Omówienie][Overview]</span><span class="sxs-lookup"><span data-stu-id="27d34-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="27d34-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="27d34-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="27d34-106">[Środowiska PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="27d34-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="27d34-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="27d34-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="27d34-108">Usługi SQL Data Warehouse umożliwia zarówno lokalnych, jak i geograficzne jego awarii magazynu danych w ramach odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="27d34-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="27d34-109">Umożliwia przywrócenie magazynu danych do punktu przywracania w regionie podstawowym kopii zapasowych magazynu danych, lub użyj geograficznie nadmiarowego kopii zapasowych do przywrócenia w innym regionie geograficznym.</span><span class="sxs-lookup"><span data-stu-id="27d34-109">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or use geo-redundant backups to restore to a different geographical region.</span></span> <span data-ttu-id="27d34-110">W tym artykule opisano specyfice przywrócenie magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="27d34-110">This article explains the specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="27d34-111">Co to jest przywrócenie magazynu danych?</span><span class="sxs-lookup"><span data-stu-id="27d34-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="27d34-112">Przywrócenie magazynu danych jest nowy magazyn danych, która jest tworzona na podstawie istniejącej kopii zapasowej lub usunięte dane magazynu.</span><span class="sxs-lookup"><span data-stu-id="27d34-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="27d34-113">W magazynie danych przywróconych ponownie tworzy w magazynie kopii zapasowej danych w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="27d34-113">The restored data warehouse re-creates the backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="27d34-114">Ponieważ Magazyn danych SQL to Rozproszony system, przywracania magazynu danych jest tworzony z wielu plików kopii zapasowej, które są przechowywane w obiektach blob Azure.</span><span class="sxs-lookup"><span data-stu-id="27d34-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="27d34-115">Przywracanie bazy danych jest integralną część każdej strategii odzyskiwania biznesowych, jak ciągłości i odzyskiwaniem po awarii, ponieważ ponownie tworzy dane po przypadkowym uszkodzenia lub usunięcia.</span><span class="sxs-lookup"><span data-stu-id="27d34-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="27d34-116">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="27d34-116">For more information, see:</span></span>

* [<span data-ttu-id="27d34-117">Tworzenie kopii zapasowych SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="27d34-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="27d34-118">Omówienie ciągłości działalności biznesowej</span><span class="sxs-lookup"><span data-stu-id="27d34-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="27d34-119">Punkty przywracania magazynu danych</span><span class="sxs-lookup"><span data-stu-id="27d34-119">Data warehouse restore points</span></span>
<span data-ttu-id="27d34-120">Jako korzyścią z używania usługi Azure Premium Storage SQL Data Warehouse używa migawki obiektu Blob magazynu Azure do kopii zapasowej w magazynie danych podstawowych.</span><span class="sxs-lookup"><span data-stu-id="27d34-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the primary data warehouse.</span></span> <span data-ttu-id="27d34-121">Każda migawka ma punkt przywracania, który reprezentuje uruchomienia migawki.</span><span class="sxs-lookup"><span data-stu-id="27d34-121">Each snapshot has a restore point that represents the time the snapshot started.</span></span> <span data-ttu-id="27d34-122">Aby przywrócić magazynu danych, wybierz punkt przywracania i wydać polecenie restore.</span><span class="sxs-lookup"><span data-stu-id="27d34-122">To restore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="27d34-123">Usługi SQL Data Warehouse zawsze przywrócenie kopii zapasowej do nowego magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="27d34-123">SQL Data Warehouse always restores the backup to a new data warehouse.</span></span> <span data-ttu-id="27d34-124">Możesz zachować w magazynie danych przywróconych i bieżący lub usuń jedno z nich.</span><span class="sxs-lookup"><span data-stu-id="27d34-124">You can either keep the restored data warehouse and the current one, or delete one of them.</span></span> <span data-ttu-id="27d34-125">Jeśli chcesz zamienić bieżącego magazynu danych z magazynem przywróconych danych, można ją zmienić.</span><span class="sxs-lookup"><span data-stu-id="27d34-125">If you want to replace the current data warehouse with the restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="27d34-126">Jeśli trzeba przywrócić hurtowni danych usuniętych lub wstrzymana, możesz [Utwórz bilet pomocy technicznej](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="27d34-126">If you need to restore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore the last available restore point.

Yes, for the next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps the data warehouse and its snapshots for seven days just in case you need the data. After seven days, you won't be able to restore to any of the restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="27d34-127">Przywracanie geograficznie nadmiarowego</span><span class="sxs-lookup"><span data-stu-id="27d34-127">Geo-redundant restore</span></span>
<span data-ttu-id="27d34-128">Magazyn danych można przywrócić na dowolny region obsługujący magazyn danych SQL Azure o takim samym poziomie wydajności wybrany.</span><span class="sxs-lookup"><span data-stu-id="27d34-128">You can restore your data warehouse to any region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="27d34-129">Należy pamiętać, że wartości DWU 9000 i 18000 nie są obsługiwane we wszystkich regionach w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="27d34-129">Please note that 9000 and 18000 DWU are not supported in all regions during the preview.</span></span>

> [!NOTE]
> <span data-ttu-id="27d34-130">Aby wykonać przywracanie geograficznie nadmiarowego musi nie rezygnujesz z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="27d34-130">To perform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="27d34-131">Przywróć osi czasu</span><span class="sxs-lookup"><span data-stu-id="27d34-131">Restore timeline</span></span>
<span data-ttu-id="27d34-132">W ciągu ostatnich siedmiu dni, można przywrócić bazy danych do dowolnego punktu przywracania dostępne.</span><span class="sxs-lookup"><span data-stu-id="27d34-132">You can restore a database to any available restore point within the last seven days.</span></span> <span data-ttu-id="27d34-133">Migawki Uruchom co cztery do ośmiu godzin i są dostępne na siedem dni.</span><span class="sxs-lookup"><span data-stu-id="27d34-133">Snapshots start every four to eight hours and are available for seven days.</span></span> <span data-ttu-id="27d34-134">Gdy migawka jest starsza niż siedmiu dni, wygaśnie i jego punktu przywracania nie jest już dostępny.</span><span class="sxs-lookup"><span data-stu-id="27d34-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="27d34-135">Przywróć kosztów</span><span class="sxs-lookup"><span data-stu-id="27d34-135">Restore costs</span></span>
<span data-ttu-id="27d34-136">Opłata magazynu dla magazynu danych przywróconych jest rozliczane według stawki Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="27d34-136">The storage charge for the restored data warehouse is billed at the Azure Premium Storage rate.</span></span> 

<span data-ttu-id="27d34-137">Jeśli magazynu przywróconych danych zostanie wstrzymana, są naliczane opłaty za magazyn szybkością Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="27d34-137">If you pause a restored data warehouse, you are charged for storage at the Azure Premium Storage rate.</span></span> <span data-ttu-id="27d34-138">Zaletą wstrzymanie jest nie są naliczane opłaty za zasoby obliczeniowe DWU.</span><span class="sxs-lookup"><span data-stu-id="27d34-138">The advantage of pausing is you are not charged for the DWU computing resources.</span></span>

<span data-ttu-id="27d34-139">Aby uzyskać więcej informacji na temat cen usługi SQL Data Warehouse, zobacz [cennik usługi SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="27d34-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="27d34-140">Używa do odtworzenia</span><span class="sxs-lookup"><span data-stu-id="27d34-140">Uses for restore</span></span>
<span data-ttu-id="27d34-141">Podstawowym zastosowaniem przywracania magazynu danych jest odzyskiwanie danych po przypadkowej utraty danych lub uszkodzenia.</span><span class="sxs-lookup"><span data-stu-id="27d34-141">The primary use for data warehouse restore is to recover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="27d34-142">Umożliwia także przywracania magazynu danych do zachowania kopii zapasowej przez ponad siedem dni.</span><span class="sxs-lookup"><span data-stu-id="27d34-142">You can also use data warehouse restore to retain a backup for longer than seven days.</span></span> <span data-ttu-id="27d34-143">Po przywróceniu kopii zapasowej online ma w magazynie danych i rozwiązaniem przez nieokreślony czas w celu ograniczenia kosztów obliczeń.</span><span class="sxs-lookup"><span data-stu-id="27d34-143">Once the backup is restored, you have the data warehouse online and can pause it indefinitely to save compute costs.</span></span> <span data-ttu-id="27d34-144">Opłaty za magazyn szybkością Azure Premium Storage wiąże się z wstrzymanej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="27d34-144">The paused database incurs storage charges at the Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="27d34-145">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="27d34-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="27d34-146">Scenariusze</span><span class="sxs-lookup"><span data-stu-id="27d34-146">Scenarios</span></span>
* <span data-ttu-id="27d34-147">Omówienie ciągłości działalności, można zobaczyć [omówienie ciągłości działalności biznesowej](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="27d34-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="27d34-148">Aby wykonać przywracanie magazynu danych, Przywróć przy użyciu:</span><span class="sxs-lookup"><span data-stu-id="27d34-148">To perform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="27d34-149">Azure portalu, zobacz [przywrócić hurtowni danych przy użyciu portalu Azure](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="27d34-149">Azure portal, see [Restore a data warehouse using the Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="27d34-150">Polecenia cmdlet programu PowerShell, zobacz [przywrócić hurtowni danych przy użyciu poleceń cmdlet programu PowerShell](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="27d34-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="27d34-151">Interfejsy API REST, zobacz [przywrócić hurtowni danych przy użyciu interfejsów API REST](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="27d34-151">REST APIs, see [Restore a data warehouse using the REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

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
