---
title: aaaManage zasad tworzenia kopii zapasowej StorSimple | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak używać toocreate usługi Menedżer StorSimple hello i zarządzanie ręcznego tworzenia kopii zapasowych, harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych."
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
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a><span data-ttu-id="6ff7e-103">Użyj zasad tworzenia kopii zapasowych toomanage usługi Menedżer StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="6ff7e-103">Use hello StorSimple Manager service toomanage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="6ff7e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6ff7e-104">Overview</span></span>
<span data-ttu-id="6ff7e-105">W tym samouczku opisano, jak toouse hello usługi Menedżer StorSimple **zasad tworzenia kopii zapasowych** strony toocontrol procesów tworzenia kopii zapasowej i przechowywania kopii zapasowych dla woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="6ff7e-106">Opisano również sposób toocomplete ręcznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="6ff7e-107">Witaj **zasad tworzenia kopii zapasowych** strony można toomanage zasad tworzenia kopii zapasowych oraz harmonogram lokalne i migawki w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-107">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="6ff7e-108">(Zasady tworzenia kopii zapasowej są używane tooconfigure harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych dla kolekcji woluminów). Zasady tworzenia kopii zapasowych umożliwiają tootake migawkę wiele woluminów jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-108">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="6ff7e-109">Oznacza to, że hello kopii zapasowych utworzonych przez zasady tworzenia kopii zapasowej będzie spójna w razie awarii kopie.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-109">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="6ff7e-110">Ta strona wyświetla hello zasad tworzenia kopii zapasowych, ich typów, hello skojarzone woluminy, hello liczbę kopii zapasowych przechowywane i hello tooenable opcji tych zasad.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-110">This page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="6ff7e-111">Witaj **zasad tworzenia kopii zapasowych** strony można też hello toofilter istniejących zasad tworzenia kopii zapasowych przez jedną lub więcej hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="6ff7e-111">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="6ff7e-112">**Nazwa zasad** — Witaj nazwy skojarzonej z zasadami hello.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-112">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="6ff7e-113">Witaj różne typy zasad:</span><span class="sxs-lookup"><span data-stu-id="6ff7e-113">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="6ff7e-114">Zaplanowane zasady, które jawnie są tworzone przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-114">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="6ff7e-115">Automatyczne zasady, które są tworzone, gdy hello domyślnego tworzenia kopii zapasowej dla tej opcji wolumin został włączony w czasie hello tworzenia woluminu.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-115">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="6ff7e-116">Te zasady są nazywane jako VolumeName_Default, gdzie nazwa woluminu odwołuje się nazwa toohello hello woluminu StorSimple skonfigurowany przez użytkownika hello w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-116">These policies are named as VolumeName_Default where Volume name refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="6ff7e-117">zasady automatycznego Hello spowodować codzienne migawki w chmurze od chwili urządzenia 22:30.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-117">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="6ff7e-118">Zaimportować zasady, które zostały pierwotnie utworzone w hello StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-118">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="6ff7e-119">Mają one znacznik hello StorSimple Snapshot Manager hosta, które hello zasady zostały zaimportowane z.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-119">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="6ff7e-120">**Woluminy** — Witaj woluminów skojarzonych z zasadami hello.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-120">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="6ff7e-121">Wszystkie woluminy hello skojarzonej z zasadami tworzenia kopii zapasowej są grupowane razem, gdy kopie zapasowe są tworzone.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-121">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="6ff7e-122">**Ostatnia kopia zapasowa pomyślnie** — hello Data i godzina hello ostatniego pomyślnego kopii zapasowej, która została wykonana z tymi zasadami.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-122">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="6ff7e-123">**Następną kopią zapasową** — hello Data i godzina hello następnego zaplanowanego tworzenia kopii zapasowej będą inicjowane przez te zasady.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-123">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="6ff7e-124">**Harmonogramy** — Witaj Liczba skojarzonych z zasadami tworzenia kopii zapasowej hello harmonogramów.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-124">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="6ff7e-125">operacje Hello często używane, które można wykonywać na tej stronie są:</span><span class="sxs-lookup"><span data-stu-id="6ff7e-125">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="6ff7e-126">Dodawanie zasad kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="6ff7e-126">Add a backup policy</span></span> 
* <span data-ttu-id="6ff7e-127">Dodaj lub zmodyfikuj harmonogram</span><span class="sxs-lookup"><span data-stu-id="6ff7e-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="6ff7e-128">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="6ff7e-128">Delete a backup policy</span></span> 
* <span data-ttu-id="6ff7e-129">Wykonaj kopię zapasową ręczne</span><span class="sxs-lookup"><span data-stu-id="6ff7e-129">Take a manual backup</span></span> 
* <span data-ttu-id="6ff7e-130">Tworzenie niestandardowych zasad tworzenia kopii zapasowej z wieloma woluminami i harmonogramów</span><span class="sxs-lookup"><span data-stu-id="6ff7e-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="6ff7e-131">Dodawanie zasad kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="6ff7e-131">Add a backup policy</span></span>
<span data-ttu-id="6ff7e-132">Dodaj zasady tworzenia kopii zapasowej tooautomatically Harmonogram kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-132">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="6ff7e-133">Wykonaj następujące kroki w klasycznym portalu Azure tooadd zasad tworzenia kopii zapasowej dla urządzenia StorSimple hello hello.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-133">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="6ff7e-134">Po dodaniu hello zasad można określić harmonogramu (zobacz [Dodaj lub zmodyfikuj harmonogram](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="6ff7e-134">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="6ff7e-135">![Zobacz film](./media/storsimple-manage-backup-policies/Video_icon.png) **Zobacz film**</span><span class="sxs-lookup"><span data-stu-id="6ff7e-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="6ff7e-136">toowatch film wideo przedstawiający sposób toocreate lokalnie lub w chmurze kopii zapasowej zasad, kliknij przycisk [tutaj](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="6ff7e-136">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="6ff7e-137">Dodaj lub zmodyfikuj harmonogram</span><span class="sxs-lookup"><span data-stu-id="6ff7e-137">Add or modify a schedule</span></span>
<span data-ttu-id="6ff7e-138">Można dodać lub zmodyfikować harmonogram, który jest dołączony tooan istniejących zasad tworzenia kopii zapasowej na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-138">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="6ff7e-139">Wykonaj następujące kroki w hello Azure classic portal tooadd hello lub zmodyfikować harmonogram.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-139">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="6ff7e-140">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="6ff7e-140">Delete a backup policy</span></span>
<span data-ttu-id="6ff7e-141">Wykonaj następujące kroki w hello klasycznego portalu Azure toodelete zasady tworzenia kopii zapasowych w urządzeniu StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-141">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="6ff7e-142">Wykonaj kopię zapasową ręczne</span><span class="sxs-lookup"><span data-stu-id="6ff7e-142">Take a manual backup</span></span>
<span data-ttu-id="6ff7e-143">Wykonaj następujące kroki w hello klasycznego portalu Azure toocreate na żądanie (ręcznie) kopię zapasową pojedynczego woluminu hello.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-143">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="6ff7e-144">Tworzenie niestandardowych zasad tworzenia kopii zapasowej z wieloma woluminami i harmonogramów</span><span class="sxs-lookup"><span data-stu-id="6ff7e-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="6ff7e-145">Wykonaj następujące kroki w klasycznym portalu Azure toocreate niestandardowych zasad tworzenia kopii zapasowej, który zawiera wiele woluminów i harmonogramy hello hello.</span><span class="sxs-lookup"><span data-stu-id="6ff7e-145">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="6ff7e-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ff7e-146">Next steps</span></span>
<span data-ttu-id="6ff7e-147">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6ff7e-147">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

