---
title: "Zarządzanie zasadami tworzenia kopii zapasowej StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak można użyć usługi Menedżer StorSimple do tworzenia i zarządzania ręcznego tworzenia kopii zapasowych, harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: c1e9d5d0450bab5d371aafb40fd7c5920d39dfdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies"></a><span data-ttu-id="dcd9a-103">Zarządzanie zasadami tworzenia kopii zapasowej przy użyciu usługi Menedżer StorSimple</span><span class="sxs-lookup"><span data-stu-id="dcd9a-103">Use the StorSimple Manager service to manage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="dcd9a-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="dcd9a-104">Overview</span></span>
<span data-ttu-id="dcd9a-105">W tym samouczku wyjaśniono, jak używać usługi Menedżer StorSimple **zasad tworzenia kopii zapasowych** strony do kontroli procesów tworzenia kopii zapasowej i przechowywania kopii zapasowych dla woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="dcd9a-106">Zawiera również opis jak zakończyć ręczne kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="dcd9a-107">**Zasad tworzenia kopii zapasowych** strona umożliwia zarządzanie zasadami tworzenia kopii zapasowej i zaplanować lokalne i migawki w chmurze.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-107">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="dcd9a-108">(Zasad tworzenia kopii zapasowych służą do konfigurowania harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych dla kolekcji woluminów). Zasady tworzenia kopii zapasowych umożliwiają utworzenie migawki wiele woluminów jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-108">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="dcd9a-109">Oznacza to, że kopie zapasowe utworzone przez zasady tworzenia kopii zapasowej będzie spójna w razie awarii kopie.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-109">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="dcd9a-110">Ta strona zawiera listę zasad tworzenia kopii zapasowych, ich typy skojarzone woluminy, liczbę kopii zapasowych przechowywane i możliwość włączenia tych zasad.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-110">This page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="dcd9a-111">**Zasad tworzenia kopii zapasowych** strony można też filtrować istniejących zasad tworzenia kopii zapasowych przez jedną lub więcej z następujących pól:</span><span class="sxs-lookup"><span data-stu-id="dcd9a-111">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="dcd9a-112">**Nazwa zasad** — Nazwa skojarzona z zasadami.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-112">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="dcd9a-113">Różne typy zasad:</span><span class="sxs-lookup"><span data-stu-id="dcd9a-113">The different types of policies include:</span></span>
  
  * <span data-ttu-id="dcd9a-114">Zaplanowane zasady, które są jawnie utworzone przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-114">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="dcd9a-115">Automatyczne zasady, które są tworzone podczas domyślnego tworzenia kopii zapasowej dla tej opcji wolumin został włączony w czasie tworzenia woluminu.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-115">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="dcd9a-116">Te zasady są nazywane jako VolumeName_Default, gdzie nazwa woluminu odnosi się do nazwy woluminu StorSimple skonfigurowany przez użytkownika w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-116">These policies are named as VolumeName_Default where Volume name refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="dcd9a-117">Zasady automatycznego spowodować codzienne migawki w chmurze od chwili urządzenia 22:30.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-117">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="dcd9a-118">Zasady importowane, które zostały pierwotnie utworzone w programie StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-118">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="dcd9a-119">Mają one znacznik hosta StorSimple Snapshot Manager, które zasady zostały zaimportowane z.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-119">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="dcd9a-120">**Woluminy** — woluminy skojarzonych z zasadami.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-120">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="dcd9a-121">Wszystkie woluminy, które są skojarzone z zasadami tworzenia kopii zapasowej są grupowane razem, gdy kopie zapasowe są tworzone.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-121">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="dcd9a-122">**Ostatnia kopia zapasowa pomyślnie** — Data i godzina ostatniej pomyślnej kopii zapasowej, która została wykonana z tymi zasadami.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-122">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="dcd9a-123">**Następną kopią zapasową** — Data i godzina następnej zaplanowanej kopii zapasowej będą inicjowane przez te zasady.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-123">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="dcd9a-124">**Harmonogramy** — liczba harmonogramów skojarzonych z zasadami tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-124">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="dcd9a-125">Często używane operacje, które można wykonywać na tej stronie są:</span><span class="sxs-lookup"><span data-stu-id="dcd9a-125">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="dcd9a-126">Dodawanie zasad kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="dcd9a-126">Add a backup policy</span></span> 
* <span data-ttu-id="dcd9a-127">Dodaj lub zmodyfikuj harmonogram</span><span class="sxs-lookup"><span data-stu-id="dcd9a-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="dcd9a-128">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="dcd9a-128">Delete a backup policy</span></span> 
* <span data-ttu-id="dcd9a-129">Wykonaj kopię zapasową ręczne</span><span class="sxs-lookup"><span data-stu-id="dcd9a-129">Take a manual backup</span></span> 
* <span data-ttu-id="dcd9a-130">Tworzenie niestandardowych zasad tworzenia kopii zapasowej z wieloma woluminami i harmonogramów</span><span class="sxs-lookup"><span data-stu-id="dcd9a-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="dcd9a-131">Dodawanie zasad kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="dcd9a-131">Add a backup policy</span></span>
<span data-ttu-id="dcd9a-132">Dodawanie zasad tworzenia kopii zapasowej, można zaplanować automatyczne kopie zapasowe.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-132">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="dcd9a-133">Wykonaj poniższe kroki w klasycznym portalu Azure, aby dodać zasady tworzenia kopii zapasowej dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-133">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="dcd9a-134">Po dodaniu zasad można określić harmonogramu (zobacz [Dodaj lub zmodyfikuj harmonogram](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="dcd9a-134">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="dcd9a-135">![Zobacz film](./media/storsimple-manage-backup-policies/Video_icon.png) **Zobacz film**</span><span class="sxs-lookup"><span data-stu-id="dcd9a-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="dcd9a-136">Aby obejrzeć film wideo przedstawiający sposób tworzenia lokalnie lub w chmurze zasad tworzenia kopii zapasowej, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="dcd9a-136">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="dcd9a-137">Dodaj lub zmodyfikuj harmonogram</span><span class="sxs-lookup"><span data-stu-id="dcd9a-137">Add or modify a schedule</span></span>
<span data-ttu-id="dcd9a-138">Można dodać lub zmodyfikować harmonogram, który jest dołączony do istniejących zasad tworzenia kopii zapasowych w urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-138">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="dcd9a-139">Wykonaj poniższe kroki w klasycznym portalu Azure, aby dodać lub zmodyfikować harmonogram.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-139">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="dcd9a-140">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="dcd9a-140">Delete a backup policy</span></span>
<span data-ttu-id="dcd9a-141">Wykonaj poniższe kroki w klasycznym portalu Azure, aby usunąć zasady tworzenia kopii zapasowych w urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-141">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="dcd9a-142">Wykonaj kopię zapasową ręczne</span><span class="sxs-lookup"><span data-stu-id="dcd9a-142">Take a manual backup</span></span>
<span data-ttu-id="dcd9a-143">Wykonaj poniższe kroki w klasycznym portalu Azure, aby utworzyć na żądanie (ręcznie) kopię zapasową pojedynczego woluminu.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-143">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="dcd9a-144">Tworzenie niestandardowych zasad tworzenia kopii zapasowej z wieloma woluminami i harmonogramów</span><span class="sxs-lookup"><span data-stu-id="dcd9a-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="dcd9a-145">Wykonaj poniższe kroki w klasycznym portalu Azure, aby utworzyć niestandardowe zasady tworzenia kopii zapasowej, który zawiera wiele woluminów i harmonogramy.</span><span class="sxs-lookup"><span data-stu-id="dcd9a-145">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="dcd9a-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dcd9a-146">Next steps</span></span>
<span data-ttu-id="dcd9a-147">Dowiedz się więcej o [przy użyciu usługi Menedżer StorSimple do administrowania urządzeniem StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="dcd9a-147">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

