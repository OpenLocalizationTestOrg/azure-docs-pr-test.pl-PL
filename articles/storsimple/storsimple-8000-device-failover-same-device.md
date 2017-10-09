---
title: "tryb failover aaaStorSimple, odzyskiwania po awarii dla urządzeń z serii 8000 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toofail za pośrednictwem sieci toohello urządzenia StorSimple tego samego urządzenia."
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a><span data-ttu-id="18b0b-103">Tryb failover urządzenia toosame urządzenia fizycznego StorSimple</span><span class="sxs-lookup"><span data-stu-id="18b0b-103">Fail over your StorSimple physical device toosame device</span></span>

## <a name="overview"></a><span data-ttu-id="18b0b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="18b0b-104">Overview</span></span>

<span data-ttu-id="18b0b-105">W tym samouczku opisano toofail wymagane kroki hello za pośrednictwem tooitself urządzenie fizyczne serii StorSimple 8000, w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="18b0b-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooitself if there is a disaster.</span></span> <span data-ttu-id="18b0b-106">StorSimple używa hello urządzenia trybu failover funkcji toomigrate danych z urządzenia fizycznego źródła w hello urządzenie fizyczne tooanother centrum danych.</span><span class="sxs-lookup"><span data-stu-id="18b0b-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="18b0b-107">wskazówki Hello w tym samouczku dotyczy urządzeń fizycznych serii tooStorSimple 8000 wersjami oprogramowania aktualizacji 3 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="18b0b-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="18b0b-108">toolearn więcej informacji na temat trybu failover urządzeń i jak jest używane toorecover po awarii, przejdź zbyt[trybu Failover i odzyskiwania po awarii dla urządzeń z serii StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="18b0b-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="18b0b-109">toofail za pośrednictwem urządzenia fizycznego tooanother urządzenie fizyczne, przejdź zbyt[awaryjnie toohello takie same urządzenia fizycznego StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="18b0b-109">toofail over a physical device tooanother physical device, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="18b0b-110">toofail za pośrednictwem tooa urządzenia fizycznego StorSimple urządzenia chmury StorSimple, przejdź zbyt[awaryjnie tooa urządzenia chmury StorSimple](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="18b0b-110">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="18b0b-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="18b0b-111">Prerequisites</span></span>

- <span data-ttu-id="18b0b-112">Upewnij się, należy przejrzeć hello zagadnienia dotyczące urządzenia trybu failover.</span><span class="sxs-lookup"><span data-stu-id="18b0b-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="18b0b-113">Aby uzyskać więcej informacji, przejdź zbyt[typowe kwestie dotyczące pracy w trybie failover urządzenia](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="18b0b-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-toofail-over-toohello-same-device"></a><span data-ttu-id="18b0b-114">Kroki toofail za pośrednictwem toohello tym samym urządzeniu</span><span class="sxs-lookup"><span data-stu-id="18b0b-114">Steps toofail over toohello same device</span></span>

<span data-ttu-id="18b0b-115">Wykonaj następujące kroki, jeśli wymagana jest toofail toohello hello tego samego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="18b0b-115">Perform hello following steps if you need toofail over toohello same device.</span></span>

1. <span data-ttu-id="18b0b-116">Twórz migawki chmurze wszystkie woluminy hello w urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="18b0b-116">Take cloud snapshots of all hello volumes in your device.</span></span> <span data-ttu-id="18b0b-117">Aby uzyskać więcej informacji, przejdź zbyt[kopii zapasowych toocreate usługi StorSimple za pomocą Menedżera urządzeń](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="18b0b-117">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="18b0b-118">Zresetowanie urządzenia toofactory domyślnych.</span><span class="sxs-lookup"><span data-stu-id="18b0b-118">Reset your device toofactory defaults.</span></span> <span data-ttu-id="18b0b-119">Wykonaj hello szczegółowe instrukcje w [jak tooreset toofactory urządzenia StorSimple domyślne ustawienia](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="18b0b-119">Follow hello detailed instructions in [how tooreset a StorSimple device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="18b0b-120">Przejdź toohello usługi Menedżer urządzeń StorSimple, a następnie wybierz **urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="18b0b-120">Go toohello StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="18b0b-121">W hello **urządzeń** bloku hello starym urządzeniem powinny być widoczne jako **Offline**.</span><span class="sxs-lookup"><span data-stu-id="18b0b-121">In hello **Devices** blade, hello old device should show as **Offline**.</span></span>

    ![Urządzenia źródłowego w trybie offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="18b0b-123">Skonfiguruj urządzenie i zarejestruj go ponownie przy użyciu usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="18b0b-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="18b0b-124">Witaj nowo zarejestrowane urządzenia powinny być widoczne jako **gotowe tooset się**.</span><span class="sxs-lookup"><span data-stu-id="18b0b-124">hello newly registered device should show as **Ready tooset up**.</span></span> <span data-ttu-id="18b0b-125">Nazwa urządzenia Hello nowe urządzenie hello jest hello tak samo jak w starym urządzeniem hello ale dołączony liczb tooindicate urządzenia hello została domyślne toofactory resetowania i ponownie zarejestrowane.</span><span class="sxs-lookup"><span data-stu-id="18b0b-125">hello device name for hello new device is hello same as hello old device but appended with a numeral tooindicate that hello device was reset toofactory default and registered again.</span></span>

    ![Nowo zarejestrowane urządzenia tooset gotowy górę](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="18b0b-127">Dla hello nowe urządzenie wykonaj konfigurację urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="18b0b-127">For hello new device, complete hello device setup.</span></span> <span data-ttu-id="18b0b-128">Aby uzyskać więcej informacji, przejdź zbyt[krok 4: przeprowadzenie minimalnej konfiguracji urządzenia](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="18b0b-128">For more information, go too[Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="18b0b-129">Na powitania **urządzeń** bloku hello stan urządzenia hello zmienia się zbyt**Online**.</span><span class="sxs-lookup"><span data-stu-id="18b0b-129">On hello **Devices** blade, hello status of hello device changes too**Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="18b0b-130">**Najpierw ukończyć powitalnych minimalnej konfiguracji lub programu DR może zakończyć się niepowodzeniem.**</span><span class="sxs-lookup"><span data-stu-id="18b0b-130">**Complete hello minimum configuration first, or your DR may fail.**</span></span>

    ![Nowo zarejestrowanym urządzeniem w trybie online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="18b0b-132">Wybierz urządzenie starego hello (stan w trybie offline), a następnie na pasku poleceń hello, kliknij **awaryjnie**.</span><span class="sxs-lookup"><span data-stu-id="18b0b-132">Select hello old device (status offline) and from hello command bar, click **Fail over**.</span></span> <span data-ttu-id="18b0b-133">W hello **awaryjnie** bloku, wybierz urządzenie starego jako źródło hello i określ urządzenie docelowe hello hello nowo zarejestrowane urządzenia.</span><span class="sxs-lookup"><span data-stu-id="18b0b-133">In hello **Fail over** blade, select old device as hello source and specify hello target device as hello newly registered device.</span></span>

    ![Podsumowanie trybu failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="18b0b-135">Aby uzyskać szczegółowe instrukcje, zobacz zbyt[awaryjnie urządzenie fizyczne tooanother](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="18b0b-135">For detailed instructions, refer too[Fail over tooanother physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="18b0b-136">Tworzone jest zadanie przywracania urządzenia można monitorować z hello **zadania** bloku.</span><span class="sxs-lookup"><span data-stu-id="18b0b-136">A device restore job is created that you can monitor from hello **Jobs** blade.</span></span>

8. <span data-ttu-id="18b0b-137">Po pomyślnym ukończeniu zadania hello dostępu hello nowe urządzenie i przejdź toohello **kontenery woluminów** bloku.</span><span class="sxs-lookup"><span data-stu-id="18b0b-137">After hello job has successfully completed, access hello new device and navigate toohello **Volume containers** blade.</span></span> <span data-ttu-id="18b0b-138">Sprawdź, czy wszystkie kontenery woluminów hello ze starym urządzeniem hello zostały zmigrowane toohello nowe urządzenie.</span><span class="sxs-lookup"><span data-stu-id="18b0b-138">Verify that all hello volume containers from hello old device have migrated toohello new device.</span></span>

   ![Kontenery woluminów migracji](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="18b0b-140">Po zakończeniu pracy awaryjnej hello można zdezaktywować i usunąć hello starego urządzenie z portalu hello.</span><span class="sxs-lookup"><span data-stu-id="18b0b-140">After hello failover is complete, you can deactivate and delete hello old device from hello portal.</span></span> <span data-ttu-id="18b0b-141">Wybierz hello starego urządzenia (w trybie offline), kliknij prawym przyciskiem myszy, a następnie wybierz **Dezaktywuj**.</span><span class="sxs-lookup"><span data-stu-id="18b0b-141">Select hello old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="18b0b-142">Po dezaktywacji urządzenia hello hello stan urządzenia hello jest aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="18b0b-142">After hello device is deactivated, hello status of hello device is updated.</span></span>

     ![Urządzenia źródłowego dezaktywowany](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="18b0b-144">Wybierz hello dezaktywować urządzenie, kliknij prawym przyciskiem myszy, a następnie wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="18b0b-144">Select hello deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="18b0b-145">Spowoduje to usunięcie urządzenia hello hello liście urządzeń.</span><span class="sxs-lookup"><span data-stu-id="18b0b-145">This deletes hello device from hello list of devices.</span></span>

    ![Urządzenia źródłowego usunięte](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="18b0b-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="18b0b-147">Next steps</span></span>

* <span data-ttu-id="18b0b-148">Po wykonaniu trybu failover może być konieczne zbyt[dezaktywację lub usunięcie urządzenia StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="18b0b-148">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="18b0b-149">Informacje dotyczące sposobu toouse hello Menedżera urządzeń StorSimple usługi znajduje się zbyt[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="18b0b-149">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

