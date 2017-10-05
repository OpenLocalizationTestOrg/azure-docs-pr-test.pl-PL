---
title: "Zarządzanie zasadami tworzenia kopii zapasowej serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak można użyć usługi Menedżer StorSimple urządzenia do tworzenia i zarządzania ręcznego tworzenia kopii zapasowych, harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych na urządzeniu z serii StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 569dbfdeb7dcd526cb5a54b487ea1bfb59b13cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-in-azure-portal-to-manage-backup-policies"></a><span data-ttu-id="a727a-103">Użyj usługi Menedżer StorSimple urządzenia w portalu Azure do zarządzania zasadami tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="a727a-103">Use the StorSimple Device Manager service in Azure portal to manage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="a727a-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a727a-104">Overview</span></span>

<span data-ttu-id="a727a-105">W tym samouczku wyjaśniono, jak używać usługi Menedżer StorSimple urządzenia **kopii zapasowej zasad** bloku do kontroli procesów tworzenia kopii zapasowej i przechowywania kopii zapasowych dla woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a727a-105">This tutorial explains how to use the StorSimple Device Manager service **Backup policy** blade to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="a727a-106">Zawiera również opis jak zakończyć ręczne kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="a727a-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="a727a-107">Podczas wykonywania kopii zapasowej woluminu, można utworzyć migawki lokalnej lub migawka w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a727a-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="a727a-108">W przypadku wykonywania kopii zapasowej woluminu przypiętego lokalnie, zaleca się określenie migawka w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a727a-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="a727a-109">Biorąc dużą liczbę lokalnych migawek woluminu przypiętego lokalnie, w połączeniu z zestawu danych, który ma wiele zmian spowoduje w sytuacji, w którym można szybko uruchomić poza lokalne miejsce.</span><span class="sxs-lookup"><span data-stu-id="a727a-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="a727a-110">Jeśli zdecydujesz się na lokalnych migawek, zaleca się zająć mniej migawki codziennych kopii zapasowych ostatniego stanu, należy zachować je na dzień, a następnie usunąć je.</span><span class="sxs-lookup"><span data-stu-id="a727a-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="a727a-111">Podczas wykonywania migawki woluminu przypiętego lokalnie chmury kopiujesz tylko zmienione dane w chmurze, gdzie jest deduplikowany i skompresowane.</span><span class="sxs-lookup"><span data-stu-id="a727a-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span>

## <a name="the-backup-policy-blade"></a><span data-ttu-id="a727a-112">Blok zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="a727a-112">The Backup policy blade</span></span>

<span data-ttu-id="a727a-113">**Kopii zapasowej zasad** bloku dla urządzenia StorSimple umożliwia zarządzanie zasadami tworzenia kopii zapasowej i zaplanować lokalne i migawki w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a727a-113">The **Backup policy** blade for your StorSimple device allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="a727a-114">Zasady tworzenia kopii zapasowych umożliwiają skonfigurowanie harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych dla kolekcji woluminów.</span><span class="sxs-lookup"><span data-stu-id="a727a-114">Backup policies are used to configure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="a727a-115">Zasady tworzenia kopii zapasowych umożliwiają utworzenie migawki wiele woluminów jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="a727a-115">Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="a727a-116">Oznacza to, że kopie zapasowe utworzone przez zasady tworzenia kopii zapasowej będzie spójna w razie awarii kopie.</span><span class="sxs-lookup"><span data-stu-id="a727a-116">This means that the backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="a727a-117">Tabelarycznej listę zasad tworzenia kopii zapasowych można też filtrować istniejących zasad tworzenia kopii zapasowych przez jedną lub więcej z następujących pól:</span><span class="sxs-lookup"><span data-stu-id="a727a-117">The backup policies tabular listing also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="a727a-118">**Nazwa zasad** — Nazwa skojarzona z zasadami.</span><span class="sxs-lookup"><span data-stu-id="a727a-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="a727a-119">Różne typy zasad:</span><span class="sxs-lookup"><span data-stu-id="a727a-119">The different types of policies include:</span></span>

  * <span data-ttu-id="a727a-120">Zaplanowane zasady, które są jawnie utworzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a727a-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="a727a-121">Zasady importowane, które zostały pierwotnie utworzone w programie StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="a727a-121">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="a727a-122">Mają one znacznik hosta StorSimple Snapshot Manager, które zasady zostały zaimportowane z.</span><span class="sxs-lookup"><span data-stu-id="a727a-122">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a727a-123">Automatyczne lub domyślne zasady tworzenia kopii zapasowej nie są już włączone w czasie tworzenia woluminu.</span><span class="sxs-lookup"><span data-stu-id="a727a-123">Automatic or default backup policies are no longer enabled at the time of volume creation.</span></span>

* <span data-ttu-id="a727a-124">**Ostatnia kopia zapasowa pomyślnie** — Data i godzina ostatniej pomyślnej kopii zapasowej, która została wykonana z tymi zasadami.</span><span class="sxs-lookup"><span data-stu-id="a727a-124">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="a727a-125">**Następną kopią zapasową** — Data i godzina następnej zaplanowanej kopii zapasowej będą inicjowane przez te zasady.</span><span class="sxs-lookup"><span data-stu-id="a727a-125">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="a727a-126">**Woluminy** — woluminy skojarzonych z zasadami.</span><span class="sxs-lookup"><span data-stu-id="a727a-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="a727a-127">Wszystkie woluminy, które są skojarzone z zasadami tworzenia kopii zapasowej są grupowane razem, gdy kopie zapasowe są tworzone.</span><span class="sxs-lookup"><span data-stu-id="a727a-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="a727a-128">**Harmonogramy** — liczba harmonogramów skojarzonych z zasadami tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="a727a-128">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="a727a-129">Są często używane operacje, które można wykonywać w odniesieniu do zasady tworzenia kopii zapasowej:</span><span class="sxs-lookup"><span data-stu-id="a727a-129">The frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="a727a-130">Dodawanie zasad kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="a727a-130">Add a backup policy</span></span>
* <span data-ttu-id="a727a-131">Dodaj lub zmodyfikuj harmonogram</span><span class="sxs-lookup"><span data-stu-id="a727a-131">Add or modify a schedule</span></span>
* <span data-ttu-id="a727a-132">Dodawanie lub usuwanie woluminu</span><span class="sxs-lookup"><span data-stu-id="a727a-132">Add or remove a volume</span></span>
* <span data-ttu-id="a727a-133">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="a727a-133">Delete a backup policy</span></span>
* <span data-ttu-id="a727a-134">Wykonaj kopię zapasową ręczne</span><span class="sxs-lookup"><span data-stu-id="a727a-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="a727a-135">Dodawanie zasad kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="a727a-135">Add a backup policy</span></span>

<span data-ttu-id="a727a-136">Dodawanie zasad tworzenia kopii zapasowej, można zaplanować automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="a727a-136">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="a727a-137">Najpierw należy utworzyć wolumin, nie ma żadnych zasad tworzenia kopii zapasowej domyślne skojarzone z woluminu.</span><span class="sxs-lookup"><span data-stu-id="a727a-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="a727a-138">Należy dodać i przypisać zasady tworzenia kopii zapasowej do ochrony danych woluminu.</span><span class="sxs-lookup"><span data-stu-id="a727a-138">You need to add and assign a backup policy to protect volume data.</span></span>

<span data-ttu-id="a727a-139">Wykonaj poniższe kroki w portalu Azure, aby dodać zasady tworzenia kopii zapasowej dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a727a-139">Perform the following steps in the Azure portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="a727a-140">Po dodaniu zasad można określić harmonogramu (zobacz [Dodaj lub zmodyfikuj harmonogram](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="a727a-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="a727a-141">Dodaj lub zmodyfikuj harmonogram</span><span class="sxs-lookup"><span data-stu-id="a727a-141">Add or modify a schedule</span></span>

<span data-ttu-id="a727a-142">Można dodać lub zmodyfikować harmonogram, który jest dołączony do istniejących zasad tworzenia kopii zapasowych w urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a727a-142">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="a727a-143">Wykonaj poniższe kroki w portalu Azure, aby dodać lub zmodyfikować harmonogram.</span><span class="sxs-lookup"><span data-stu-id="a727a-143">Perform the following steps in the Azure portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="a727a-144">Dodawanie lub usuwanie woluminu</span><span class="sxs-lookup"><span data-stu-id="a727a-144">Add or remove a volume</span></span>

<span data-ttu-id="a727a-145">Można dodawać i usuwać przypisane do zasad tworzenia kopii zapasowej na urządzeniu StorSimple woluminu.</span><span class="sxs-lookup"><span data-stu-id="a727a-145">You can add or remove a volume assigned to a backup policy on your StorSimple device.</span></span> <span data-ttu-id="a727a-146">Wykonaj poniższe kroki w portalu Azure, aby dodać lub usunąć wolumin.</span><span class="sxs-lookup"><span data-stu-id="a727a-146">Perform the following steps in the Azure portal to add or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="a727a-147">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="a727a-147">Delete a backup policy</span></span>

<span data-ttu-id="a727a-148">Wykonaj poniższe kroki w portalu Azure, aby usunąć zasady tworzenia kopii zapasowych w urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a727a-148">Perform the following steps in the Azure portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="a727a-149">Wykonaj kopię zapasową ręczne</span><span class="sxs-lookup"><span data-stu-id="a727a-149">Take a manual backup</span></span>

<span data-ttu-id="a727a-150">Wykonaj poniższe kroki w portalu Azure, aby utworzyć kopię zapasową pojedynczego woluminu na żądanie (ręcznie).</span><span class="sxs-lookup"><span data-stu-id="a727a-150">Perform the following steps in the Azure portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="a727a-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a727a-151">Next steps</span></span>

<span data-ttu-id="a727a-152">Dowiedz się więcej o [przy użyciu usługi Menedżer StorSimple urządzenia do administrowania urządzeniem StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a727a-152">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

