---
title: "aaaStorSimple przejścia w tryb failover tooa odzyskiwania po awarii urządzenia chmury StorSimple | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toofail za pośrednictwem sieci tooa urządzenie fizyczne serii StorSimple 8000 chmury urządzenia."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a><span data-ttu-id="5e467-103">Tryb failover tooyour urządzenia chmury StorSimple</span><span class="sxs-lookup"><span data-stu-id="5e467-103">Fail over tooyour StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="5e467-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="5e467-104">Overview</span></span>

<span data-ttu-id="5e467-105">W tym samouczku opisano toofail wymagane kroki hello za pośrednictwem tooa urządzenia fizycznego StorSimple 8000 serii StorSimple urządzenia chmury, w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="5e467-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooa StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="5e467-106">StorSimple używa hello urządzenia trybu failover funkcji toomigrate danych z urządzenia fizycznego źródła w hello datacenter tooa urządzenia chmury działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5e467-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooa cloud appliance running in Azure.</span></span> <span data-ttu-id="5e467-107">wskazówki Hello w tym samouczku dotyczy urządzeń fizycznych serii tooStorSimple 8000 oraz chmury urządzenia z wersjami oprogramowania aktualizacji, 3 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="5e467-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="5e467-108">toolearn więcej informacji na temat trybu failover urządzeń i jak jest używane toorecover po awarii, przejdź zbyt[trybu Failover i odzyskiwania po awarii dla urządzeń z serii StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="5e467-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="5e467-109">toofail przez urządzenie fizyczne tooanother urządzenia fizycznego StorSimple Przejdź zbyt[awaryjnie urządzenia fizycznego StorSimple tooa](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="5e467-109">toofail over a StorSimple physical device tooanother physical device, go too[Fail over tooa StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="5e467-110">toofail za pośrednictwem tooitself urządzeń, przejdź zbyt[awaryjnie toohello takie same urządzenia fizycznego StorSimple](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="5e467-110">toofail over a device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e467-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5e467-111">Prerequisites</span></span>

- <span data-ttu-id="5e467-112">Upewnij się, należy przejrzeć hello zagadnienia dotyczące urządzenia trybu failover.</span><span class="sxs-lookup"><span data-stu-id="5e467-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="5e467-113">Aby uzyskać więcej informacji, przejdź zbyt[typowe kwestie dotyczące pracy w trybie failover urządzenia](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="5e467-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="5e467-114">Muszą mieć urządzenia chmury StorSimple utworzeniu i skonfigurowaniu przed uruchomieniem tej procedury.</span><span class="sxs-lookup"><span data-stu-id="5e467-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="5e467-115">Jeśli uruchomienia aktualizacji oprogramowania w wersji 3 lub później, należy rozważyć użycie urządzenia 8020 chmury dla hello odzyskiwania po awarii.</span><span class="sxs-lookup"><span data-stu-id="5e467-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for hello DR.</span></span> <span data-ttu-id="5e467-116">Witaj model 8020 ma 64 TB i używa magazyn w warstwie Premium.</span><span class="sxs-lookup"><span data-stu-id="5e467-116">hello 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="5e467-117">Aby uzyskać więcej informacji, przejdź zbyt[wdrażanie i zarządzanie nimi urządzenia chmury StorSimple](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="5e467-117">For more information, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-toofail-over-tooa-cloud-appliance"></a><span data-ttu-id="5e467-118">Kroki toofail za pośrednictwem urządzenia do chmury tooa</span><span class="sxs-lookup"><span data-stu-id="5e467-118">Steps toofail over tooa cloud appliance</span></span>

<span data-ttu-id="5e467-119">Wykonaj następujące kroki toorestore hello urządzenia tooa docelowego urządzenia chmury StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="5e467-119">Perform hello following steps toorestore hello device tooa target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="5e467-120">Sprawdź, czy ten kontener woluminów hello żądane toofail za pośrednictwem skojarzone migawki w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5e467-120">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="5e467-121">Aby uzyskać więcej informacji, przejdź zbyt[kopii zapasowych toocreate usługi StorSimple za pomocą Menedżera urządzeń](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="5e467-121">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="5e467-122">Przejdź tooyour usługi Menedżer StorSimple urządzenie i kliknij polecenie **urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="5e467-122">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="5e467-123">W hello **urządzeń** bloku, przejdź toohello listy urządzeń połączonych z usługą.</span><span class="sxs-lookup"><span data-stu-id="5e467-123">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="5e467-124">![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="5e467-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="5e467-125">Wybierz, a następnie kliknij przycisk urządzenia źródłowego.</span><span class="sxs-lookup"><span data-stu-id="5e467-125">Select and click your source device.</span></span> <span data-ttu-id="5e467-126">urządzenia źródłowego Hello ma hello kontenery woluminów, które mają toofail za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="5e467-126">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="5e467-127">Przejdź za**Ustawienia > kontenery woluminów**.</span><span class="sxs-lookup"><span data-stu-id="5e467-127">Go too**Settings > Volume Containers**.</span></span>

    ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="5e467-129">Wybierz kontener woluminów za pośrednictwem urządzenia tooanother chcesz toofail.</span><span class="sxs-lookup"><span data-stu-id="5e467-129">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="5e467-130">Kliknij przycisk Lista kontenera woluminów hello hello toodisplay woluminów, w tym kontenerze.</span><span class="sxs-lookup"><span data-stu-id="5e467-130">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="5e467-131">Wybierz wolumin, kliknij prawym przyciskiem myszy i kliknij przycisk **Przełącz do trybu Offline** tootake hello woluminu w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="5e467-131">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span>

    ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="5e467-133">Powtórz ten proces dla wszystkich woluminów hello w hello kontenera woluminów.</span><span class="sxs-lookup"><span data-stu-id="5e467-133">Repeat this process for all hello volumes in hello volume container.</span></span>

     ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="5e467-135">Hello Powtórz poprzedni krok dla wszystkich hello kontenery woluminów chcesz toofail za pośrednictwem tooanother urządzenia.</span><span class="sxs-lookup"><span data-stu-id="5e467-135">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>

7. <span data-ttu-id="5e467-136">Przejdź wstecz toohello **urządzeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="5e467-136">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="5e467-137">Na pasku poleceń hello, kliknij **awaryjnie**.</span><span class="sxs-lookup"><span data-stu-id="5e467-137">From hello command bar, click **Fail over**.</span></span>

    ![Kliknij opcję niepowodzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="5e467-139">W hello **awaryjnie** blok, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5e467-139">In hello **Fail over** blade, perform hello following steps:</span></span>
   
    1. <span data-ttu-id="5e467-140">Kliknij przycisk **źródła**.</span><span class="sxs-lookup"><span data-stu-id="5e467-140">Click **Source**.</span></span> <span data-ttu-id="5e467-141">Wybierz toofail kontenery woluminów hello za pośrednictwem.</span><span class="sxs-lookup"><span data-stu-id="5e467-141">Select hello volume containers toofail over.</span></span> <span data-ttu-id="5e467-142">**Tylko hello kontenery woluminów z migawkami skojarzonej chmury i woluminy w trybie offline są wyświetlane.**</span><span class="sxs-lookup"><span data-stu-id="5e467-142">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="5e467-143">![Wybierz źródło](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="5e467-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="5e467-144">Kliknij przycisk **docelowej**.</span><span class="sxs-lookup"><span data-stu-id="5e467-144">Click **Target**.</span></span> <span data-ttu-id="5e467-145">Wybierz urządzenia chmury docelowy z listy rozwijanej hello dostępnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="5e467-145">Select a target cloud appliance from hello dropdown list of available devices.</span></span> <span data-ttu-id="5e467-146">**Tylko urządzenia hello, które mają wystarczającą pojemność tooaccommodate źródła kontenery woluminów są wyświetlane na liście hello.**</span><span class="sxs-lookup"><span data-stu-id="5e467-146">**Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.**</span></span>

        ![Wybierz element docelowy](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="5e467-148">Przejrzyj ustawienia trybu failover hello w obszarze **Podsumowanie** i wybierz hello wyboru wskazujące, że woluminy hello w kontenerach wybranego woluminu w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="5e467-148">Review hello failover settings under **Summary** and select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> 

        ![Przejrzyj ustawienia trybu failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="5e467-150">Tworzone jest zadanie trybu failover.</span><span class="sxs-lookup"><span data-stu-id="5e467-150">A failover job is created.</span></span> <span data-ttu-id="5e467-151">tryb failover hello toomonitor zadania, kliknij przycisk hello powiadomienie o zadaniu.</span><span class="sxs-lookup"><span data-stu-id="5e467-151">toomonitor hello failover job, click hello job notification.</span></span>

    ![Monitor, zadanie trybu failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="5e467-153">Po zakończeniu pracy awaryjnej hello, przejdź wstecz toohello **urządzeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="5e467-153">After hello failover is completed, go back toohello **Devices** blade.</span></span>

    1. <span data-ttu-id="5e467-154">Wybierz urządzenie hello, używany jako docelowy hello hello pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="5e467-154">Select hello device that was used as hello target for hello failover.</span></span>

       ![Wybierz urządzenie](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="5e467-156">Kliknij przycisk **kontenery woluminów**.</span><span class="sxs-lookup"><span data-stu-id="5e467-156">Click **Volume Containers**.</span></span> <span data-ttu-id="5e467-157">Wszystkie kontenery woluminów hello, wraz z woluminów hello ze starym urządzeniem hello, powinien być wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="5e467-157">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       <span data-ttu-id="5e467-158">Kontener woluminów hello, który przejścia w tryb failover jest przypięty lokalnie woluminów, woluminy są nie powiodła się za pośrednictwem jako woluminy warstwowe.</span><span class="sxs-lookup"><span data-stu-id="5e467-158">If hello volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="5e467-159">Woluminów przypiętych lokalnie nie są obsługiwane na urządzeniu z StorSimple w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5e467-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Kontenery woluminów docelowego widoku](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="5e467-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e467-161">Next steps</span></span>

* <span data-ttu-id="5e467-162">Po wykonaniu trybu failover może być konieczne zbyt[dezaktywację lub usunięcie urządzenia StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="5e467-162">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="5e467-163">Informacje dotyczące sposobu toouse hello Menedżera urządzeń StorSimple usługi znajduje się zbyt[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="5e467-163">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

