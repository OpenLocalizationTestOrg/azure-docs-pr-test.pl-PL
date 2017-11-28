---
title: "Tryb failover StorSimple, odzyskiwania po awarii dla urządzeń z serii 8000 | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie pracy awaryjnej urządzenia StorSimple na tym samym urządzeniu."
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
ms.openlocfilehash: acc8929dc3476e9590e8e4d9526b38b7c0719570
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-your-storsimple-physical-device-to-same-device"></a><span data-ttu-id="a5d9b-103">Tryb failover urządzenia fizycznego StorSimple na tym samym urządzeniu</span><span class="sxs-lookup"><span data-stu-id="a5d9b-103">Fail over your StorSimple physical device to same device</span></span>

## <a name="overview"></a><span data-ttu-id="a5d9b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a5d9b-104">Overview</span></span>

<span data-ttu-id="a5d9b-105">W tym samouczku opisano kroki wymagane do pracy awaryjnej urządzenia fizycznego serii StorSimple 8000 do samego siebie w przypadku awarii.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to itself if there is a disaster.</span></span> <span data-ttu-id="a5d9b-106">StorSimple korzysta z funkcji trybu failover urządzenia do migracji danych z urządzenia fizycznego źródła w centrum danych do innego urządzenia fizycznego.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="a5d9b-107">Wskazówki zawarte w tym samouczku dotyczą z serii StorSimple 8000 fizyczne urządzenia z wersjami oprogramowania aktualizacji 3 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="a5d9b-108">Aby dowiedzieć się więcej o pracy awaryjnej urządzenia i sposobu ich wykorzystywania odzyskiwania po awarii, przejdź do [trybu Failover i odzyskiwania po awarii dla urządzeń z serii StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="a5d9b-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="a5d9b-109">Aby tryb failover na inne urządzenie fizyczne urządzenia fizycznego, przejdź do [awaryjnej w tym samym urządzeniu fizycznym StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="a5d9b-109">To fail over a physical device to another physical device, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="a5d9b-110">Aby przełączyć urządzenia fizycznego StorSimple na urządzeniu chmury StorSimple, przejdź do [funkcjonować w trybie awaryjnym urządzenia chmury StorSimple](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="a5d9b-110">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a5d9b-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a5d9b-111">Prerequisites</span></span>

- <span data-ttu-id="a5d9b-112">Upewnij się, należy przejrzeć zagadnienia dotyczące urządzenia trybu failover.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="a5d9b-113">Aby uzyskać więcej informacji, przejdź do [typowe kwestie dotyczące pracy w trybie failover urządzenia](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="a5d9b-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-to-fail-over-to-the-same-device"></a><span data-ttu-id="a5d9b-114">Kroki, aby przełączyć się na tym samym urządzeniu</span><span class="sxs-lookup"><span data-stu-id="a5d9b-114">Steps to fail over to the same device</span></span>

<span data-ttu-id="a5d9b-115">Wykonaj następujące kroki, aby przełączyć się na tym samym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-115">Perform the following steps if you need to fail over to the same device.</span></span>

1. <span data-ttu-id="a5d9b-116">Twórz migawki chmurze wszystkie woluminy w urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-116">Take cloud snapshots of all the volumes in your device.</span></span> <span data-ttu-id="a5d9b-117">Aby uzyskać więcej informacji, przejdź do [usługi StorSimple za pomocą Menedżera urządzeń do tworzenia kopii zapasowych](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="a5d9b-117">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="a5d9b-118">Resetować urządzenie do ustawień fabrycznych.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-118">Reset your device to factory defaults.</span></span> <span data-ttu-id="a5d9b-119">Postępuj zgodnie z instrukcjami szczegółowe [sposób resetowania urządzenia StorSimple do domyślnych ustawień fabrycznych](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="a5d9b-119">Follow the detailed instructions in [how to reset a StorSimple device to factory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="a5d9b-120">Przejdź do usługi Menedżer StorSimple urządzenia, a następnie wybierz **urządzeń**.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-120">Go to the StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="a5d9b-121">W **urządzeń** bloku starego urządzenia powinny być widoczne jako **Offline**.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-121">In the **Devices** blade, the old device should show as **Offline**.</span></span>

    ![Urządzenia źródłowego w trybie offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="a5d9b-123">Skonfiguruj urządzenie i zarejestruj go ponownie przy użyciu usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="a5d9b-124">Nowo zarejestrowane urządzenia powinny być widoczne jako **przejść do konfigurowania**.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-124">The newly registered device should show as **Ready to set up**.</span></span> <span data-ttu-id="a5d9b-125">Nazwę urządzenia dla nowego urządzenia jest taka sama jak starym urządzeniem, ale dołączony liczb, aby wskazać, czy przywrócić ustawienia fabryczne i ponownie zarejestrować urządzenie.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-125">The device name for the new device is the same as the old device but appended with a numeral to indicate that the device was reset to factory default and registered again.</span></span>

    ![Nowo zarejestrowanym urządzeniu przejść do konfigurowania](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="a5d9b-127">Nowe urządzenia należy przeprowadzić konfigurację urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-127">For the new device, complete the device setup.</span></span> <span data-ttu-id="a5d9b-128">Aby uzyskać więcej informacji, przejdź do [krok 4: przeprowadzenie minimalnej konfiguracji urządzenia](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="a5d9b-128">For more information, go to [Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="a5d9b-129">Na **urządzeń** bloku zmiany stanu urządzenia **Online**.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-129">On the **Devices** blade, the status of the device changes to **Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a5d9b-130">**Najpierw Zakończ minimalną konfigurację lub programu DR może zakończyć się niepowodzeniem.**</span><span class="sxs-lookup"><span data-stu-id="a5d9b-130">**Complete the minimum configuration first, or your DR may fail.**</span></span>

    ![Nowo zarejestrowanym urządzeniem w trybie online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="a5d9b-132">Wybierz urządzenie stary (stan w trybie offline), a następnie na pasku poleceń kliknij **awaryjnie**.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-132">Select the old device (status offline) and from the command bar, click **Fail over**.</span></span> <span data-ttu-id="a5d9b-133">W **awaryjnie** bloku, wybierz starym urządzeniem jako źródło i określ urządzenie docelowe jako nowo zarejestrowanym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-133">In the **Fail over** blade, select old device as the source and specify the target device as the newly registered device.</span></span>

    ![Podsumowanie trybu failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="a5d9b-135">Aby uzyskać szczegółowe instrukcje, zapoznaj się [przełączyć do innego urządzenia fizycznego](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="a5d9b-135">For detailed instructions, refer to [Fail over to another physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="a5d9b-136">Tworzone jest zadanie przywracania urządzenia można monitorować z **zadania** bloku.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-136">A device restore job is created that you can monitor from the **Jobs** blade.</span></span>

8. <span data-ttu-id="a5d9b-137">Po pomyślnym ukończeniu zadania dostępu do nowego urządzenia i przejdź do **kontenery woluminów** bloku.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-137">After the job has successfully completed, access the new device and navigate to the **Volume containers** blade.</span></span> <span data-ttu-id="a5d9b-138">Sprawdź, czy wszystkie kontenery woluminów z urządzenia starego zostały zmigrowane do nowych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-138">Verify that all the volume containers from the old device have migrated to the new device.</span></span>

   ![Kontenery woluminów migracji](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="a5d9b-140">Po zakończeniu pracy awaryjnej można zdezaktywować i usunąć stary urządzenie z portalu.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-140">After the failover is complete, you can deactivate and delete the old device from the portal.</span></span> <span data-ttu-id="a5d9b-141">Wybierz starego urządzenia (w trybie offline), kliknij prawym przyciskiem myszy, a następnie wybierz **Dezaktywuj**.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-141">Select the old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="a5d9b-142">Po dezaktywacji urządzenia, stan urządzenia jest aktualizowana.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-142">After the device is deactivated, the status of the device is updated.</span></span>

     ![Urządzenia źródłowego dezaktywowany](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="a5d9b-144">Wybierz dezaktywować urządzenie, kliknij prawym przyciskiem myszy, a następnie wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-144">Select the deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="a5d9b-145">Spowoduje to usunięcie urządzenia z listy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="a5d9b-145">This deletes the device from the list of devices.</span></span>

    ![Urządzenia źródłowego usunięte](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="a5d9b-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a5d9b-147">Next steps</span></span>

* <span data-ttu-id="a5d9b-148">Po wykonaniu trybu failover, konieczne może być [dezaktywację lub usunięcie urządzenia StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="a5d9b-148">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="a5d9b-149">Aby uzyskać informacje o sposobie używania usługi Menedżer StorSimple urządzeń, przejdź do [zarządzać urządzenia StorSimple przy użyciu usługi Menedżer StorSimple urządzenia](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a5d9b-149">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

