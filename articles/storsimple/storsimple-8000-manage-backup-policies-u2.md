---
title: zasady tworzenia kopii zapasowej serii StorSimple 8000 aaaManage | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak używać toocreate usługi Menedżer StorSimple urządzenia hello i zarządzanie ręcznego tworzenia kopii zapasowych, harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych na urządzeniu z serii StorSimple 8000."
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
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a><span data-ttu-id="cfdc0-103">Użyj usługi Menedżer StorSimple urządzenia hello w toomanage portalu Azure zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cfdc0-103">Use hello StorSimple Device Manager service in Azure portal toomanage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="cfdc0-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cfdc0-104">Overview</span></span>

<span data-ttu-id="cfdc0-105">W tym samouczku opisano, jak toouse hello usługi Menedżer StorSimple urządzenia **kopii zapasowej zasad** procesów tworzenia kopii zapasowej toocontrol bloku i przechowywania kopii zapasowych dla woluminów StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-105">This tutorial explains how toouse hello StorSimple Device Manager service **Backup policy** blade toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="cfdc0-106">Opisano również sposób toocomplete ręcznego tworzenia kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="cfdc0-107">Podczas wykonywania kopii zapasowej woluminu można toocreate migawka lokalna i migawka w chmurze.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="cfdc0-108">W przypadku wykonywania kopii zapasowej woluminu przypiętego lokalnie, zaleca się określenie migawka w chmurze.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="cfdc0-109">Biorąc dużą liczbę lokalnych migawek woluminu przypiętego lokalnie, w połączeniu z zestawu danych, który ma wiele zmian spowoduje w sytuacji, w którym można szybko uruchomić poza lokalne miejsce.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="cfdc0-110">Jeśli wybierzesz tootake migawki lokalne, zaleca się zająć mniej tooback migawki codziennych hello ostatniego stanu, zachować je na dzień, a następnie usuń je.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="cfdc0-111">Podczas wykonywania migawki chmury woluminu przypiętego lokalnie, możesz skopiować tylko zmienione hello danych toohello w chmurze, gdzie jest deduplikowany i skompresowane.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span>

## <a name="hello-backup-policy-blade"></a><span data-ttu-id="cfdc0-112">Blok zasady tworzenia kopii zapasowej Hello</span><span class="sxs-lookup"><span data-stu-id="cfdc0-112">hello Backup policy blade</span></span>

<span data-ttu-id="cfdc0-113">Witaj **kopii zapasowej zasad** bloku dla urządzenia StorSimple umożliwia toomanage zasad tworzenia kopii zapasowych oraz harmonogram lokalne i migawki w chmurze.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-113">hello **Backup policy** blade for your StorSimple device allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="cfdc0-114">Zasady tworzenia kopii zapasowej są używane tooconfigure harmonogramy tworzenia kopii zapasowej i przechowywania kopii zapasowych dla kolekcji woluminów.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-114">Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="cfdc0-115">Zasady tworzenia kopii zapasowych umożliwiają tootake migawkę wiele woluminów jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-115">Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="cfdc0-116">Oznacza to, że hello kopii zapasowych utworzonych przez zasady tworzenia kopii zapasowej będzie spójna w razie awarii kopie.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-116">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="cfdc0-117">tabelarycznej listę zasad tworzenia kopii zapasowych Hello umożliwia także możesz toofilter hello istniejących zasad tworzenia kopii zapasowych przez jedną lub więcej hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="cfdc0-117">hello backup policies tabular listing also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="cfdc0-118">**Nazwa zasad** — Witaj nazwy skojarzonej z zasadami hello.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="cfdc0-119">Witaj różne typy zasad:</span><span class="sxs-lookup"><span data-stu-id="cfdc0-119">hello different types of policies include:</span></span>

  * <span data-ttu-id="cfdc0-120">Zaplanowane zasady, które jawnie są tworzone przez użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="cfdc0-121">Zaimportować zasady, które zostały pierwotnie utworzone w hello StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-121">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="cfdc0-122">Mają one znacznik hello StorSimple Snapshot Manager hosta, które hello zasady zostały zaimportowane z.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-122">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="cfdc0-123">Automatyczne lub domyślne zasady tworzenia kopii zapasowej nie są już włączone w czasie hello tworzenia woluminu.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-123">Automatic or default backup policies are no longer enabled at hello time of volume creation.</span></span>

* <span data-ttu-id="cfdc0-124">**Ostatnia kopia zapasowa pomyślnie** — hello Data i godzina hello ostatniego pomyślnego kopii zapasowej, która została wykonana z tymi zasadami.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-124">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="cfdc0-125">**Następną kopią zapasową** — hello Data i godzina hello następnego zaplanowanego tworzenia kopii zapasowej będą inicjowane przez te zasady.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-125">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="cfdc0-126">**Woluminy** — Witaj woluminów skojarzonych z zasadami hello.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="cfdc0-127">Wszystkie woluminy hello skojarzonej z zasadami tworzenia kopii zapasowej są grupowane razem, gdy kopie zapasowe są tworzone.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="cfdc0-128">**Harmonogramy** — Witaj Liczba skojarzonych z zasadami tworzenia kopii zapasowej hello harmonogramów.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-128">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="cfdc0-129">są często używane Hello operacje, które można wykonać dla zasad tworzenia kopii zapasowych:</span><span class="sxs-lookup"><span data-stu-id="cfdc0-129">hello frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="cfdc0-130">Dodawanie zasad kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="cfdc0-130">Add a backup policy</span></span>
* <span data-ttu-id="cfdc0-131">Dodaj lub zmodyfikuj harmonogram</span><span class="sxs-lookup"><span data-stu-id="cfdc0-131">Add or modify a schedule</span></span>
* <span data-ttu-id="cfdc0-132">Dodawanie lub usuwanie woluminu</span><span class="sxs-lookup"><span data-stu-id="cfdc0-132">Add or remove a volume</span></span>
* <span data-ttu-id="cfdc0-133">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cfdc0-133">Delete a backup policy</span></span>
* <span data-ttu-id="cfdc0-134">Wykonaj kopię zapasową ręczne</span><span class="sxs-lookup"><span data-stu-id="cfdc0-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="cfdc0-135">Dodawanie zasad kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="cfdc0-135">Add a backup policy</span></span>

<span data-ttu-id="cfdc0-136">Dodaj zasady tworzenia kopii zapasowej tooautomatically Harmonogram kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-136">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="cfdc0-137">Najpierw należy utworzyć wolumin, nie ma żadnych zasad tworzenia kopii zapasowej domyślne skojarzone z woluminu.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="cfdc0-138">Należy go tooadd i przypisać zasady tworzenia kopii zapasowych danych woluminu tooprotect.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-138">You need tooadd and assign a backup policy tooprotect volume data.</span></span>

<span data-ttu-id="cfdc0-139">Wykonaj następujące kroki w hello tooadd portalu Azure zasady tworzenia kopii zapasowej dla urządzenia StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-139">Perform hello following steps in hello Azure portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="cfdc0-140">Po dodaniu hello zasad można określić harmonogramu (zobacz [Dodaj lub zmodyfikuj harmonogram](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="cfdc0-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="cfdc0-141">Dodaj lub zmodyfikuj harmonogram</span><span class="sxs-lookup"><span data-stu-id="cfdc0-141">Add or modify a schedule</span></span>

<span data-ttu-id="cfdc0-142">Można dodać lub zmodyfikować harmonogram, który jest dołączony tooan istniejących zasad tworzenia kopii zapasowej na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-142">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="cfdc0-143">Wykonaj następujące kroki w hello Azure tooadd portalu hello lub zmodyfikować harmonogram.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-143">Perform hello following steps in hello Azure portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="cfdc0-144">Dodawanie lub usuwanie woluminu</span><span class="sxs-lookup"><span data-stu-id="cfdc0-144">Add or remove a volume</span></span>

<span data-ttu-id="cfdc0-145">Można dodawać i usuwać woluminu przypisane tooa zasady tworzenia kopii zapasowych w urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-145">You can add or remove a volume assigned tooa backup policy on your StorSimple device.</span></span> <span data-ttu-id="cfdc0-146">Wykonaj następujące kroki w hello Azure tooadd portalu hello, lub Usuń wolumin.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-146">Perform hello following steps in hello Azure portal tooadd or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="cfdc0-147">Usuń zasady tworzenia kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="cfdc0-147">Delete a backup policy</span></span>

<span data-ttu-id="cfdc0-148">Wykonaj następujące kroki w hello toodelete portalu Azure zasady tworzenia kopii zapasowych w urządzeniu StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-148">Perform hello following steps in hello Azure portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="cfdc0-149">Wykonaj kopię zapasową ręczne</span><span class="sxs-lookup"><span data-stu-id="cfdc0-149">Take a manual backup</span></span>

<span data-ttu-id="cfdc0-150">Wykonaj następujące kroki w hello toocreate portalu Azure na żądanie (ręcznie) kopię zapasową pojedynczego woluminu hello.</span><span class="sxs-lookup"><span data-stu-id="cfdc0-150">Perform hello following steps in hello Azure portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="cfdc0-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cfdc0-151">Next steps</span></span>

<span data-ttu-id="cfdc0-152">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="cfdc0-152">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

