---
title: "Dezaktywuj i Usuń Microsoft Azure StorSimple wirtualnego tablicą | Dokumentacja firmy Microsoft"
description: "Opisuje sposób usuwania urządzenia StorSimple z usługi najpierw dezaktywowanie go, a następnie usuwając go."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 8dea36f92b034f8c6cdb6875634848d37f4c6606
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="d61ac-103">Dezaktywuj i Usuń macierz wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="d61ac-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="d61ac-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d61ac-104">Overview</span></span>

<span data-ttu-id="d61ac-105">Po dezaktywowaniu tablicą wirtualnego StorSimple przerwaniu połączenia między urządzeniem i odpowiedniej usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d61ac-105">When you deactivate a StorSimple Virtual Array, you break the connection between the device and the corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="d61ac-106">Ten samouczek wyjaśnia, jak:</span><span class="sxs-lookup"><span data-stu-id="d61ac-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="d61ac-107">Dezaktywować urządzenie</span><span class="sxs-lookup"><span data-stu-id="d61ac-107">Deactivate a device</span></span> 
* <span data-ttu-id="d61ac-108">Usuwanie urządzenia dezaktywowany</span><span class="sxs-lookup"><span data-stu-id="d61ac-108">Delete a deactivated device</span></span>

<span data-ttu-id="d61ac-109">Informacje przedstawione w tym artykule dotyczą tylko tablice wirtualnego StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d61ac-109">The information in this article applies to StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="d61ac-110">Informacje w serii 8000, przejdź do sposobu [dezaktywację lub usunięcie urządzenia](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="d61ac-110">For information on 8000 series, go to how to [deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-to-deactivate"></a><span data-ttu-id="d61ac-111">Kiedy należy dezaktywować?</span><span class="sxs-lookup"><span data-stu-id="d61ac-111">When to deactivate?</span></span>

<span data-ttu-id="d61ac-112">Dezaktywacja jest operacją trwałe i nie można cofnąć.</span><span class="sxs-lookup"><span data-stu-id="d61ac-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="d61ac-113">Nie można zarejestrować ponownie dezaktywować urządzenie w usłudze Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d61ac-113">You cannot register a deactivated device with the StorSimple Device Manager service again.</span></span> <span data-ttu-id="d61ac-114">Może być konieczne, Dezaktywuj i Usuń macierz wirtualnego StorSimple w następujących scenariuszach:</span><span class="sxs-lookup"><span data-stu-id="d61ac-114">You may need to deactivate and delete a StorSimple Virtual Array in the following scenarios:</span></span>

* <span data-ttu-id="d61ac-115">**Planowana praca awaryjna** : urządzenie jest w trybie online i jest planowane w tryb failover urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d61ac-115">**Planned failover** : Your device is online and you plan to fail over your device.</span></span> <span data-ttu-id="d61ac-116">Jeśli planowane jest uaktualnienie do większych urządzenia, konieczne może być awaryjnie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d61ac-116">If you are planning to upgrade to a larger device, you may need to fail over your device.</span></span> <span data-ttu-id="d61ac-117">Po przekazania własności danych i przejścia w tryb failover, urządzenia są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="d61ac-117">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span></span>
* <span data-ttu-id="d61ac-118">**Nieplanowane przełączenie awaryjne** : urządzenie jest w trybie offline, należy przełączyć na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="d61ac-118">**Unplanned failover** : Your device is offline and you need to fail over the device.</span></span> <span data-ttu-id="d61ac-119">W tym scenariuszu mogą wystąpić podczas awarii, gdy istnieje przerwa w centrum danych i urządzenie podstawowej nie działa.</span><span class="sxs-lookup"><span data-stu-id="d61ac-119">This scenario may occur during a disaster when there is an outage in the datacenter and your primary device is down.</span></span> <span data-ttu-id="d61ac-120">Zaplanuj urządzenia na urządzeniu dodatkowej pracy awaryjnej.</span><span class="sxs-lookup"><span data-stu-id="d61ac-120">You plan to fail over the device to a secondary device.</span></span> <span data-ttu-id="d61ac-121">Po przekazania własności danych i przejścia w tryb failover, urządzenia są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="d61ac-121">After the data ownership is transferred and the failover is complete, the source device is automatically deleted.</span></span>
* <span data-ttu-id="d61ac-122">**Likwidowanie** : Aby zlikwidować urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d61ac-122">**Decommission** : You want to decommission the device.</span></span> <span data-ttu-id="d61ac-123">Należy najpierw dezaktywować urządzenie, a następnie usuń go.</span><span class="sxs-lookup"><span data-stu-id="d61ac-123">This requires you to first deactivate the device and then delete it.</span></span> <span data-ttu-id="d61ac-124">Po dezaktywacji urządzenia może już uzyskać dostępu do żadnych danych, który jest przechowywany lokalnie.</span><span class="sxs-lookup"><span data-stu-id="d61ac-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="d61ac-125">Można jedynie dostępu i odzyskiwanie danych przechowywanych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d61ac-125">You can only access and recover the data stored in the cloud.</span></span> <span data-ttu-id="d61ac-126">Jeśli planujesz przechowywanie danych urządzenia po dezaktywacji, następnie należy podjąć migawkę chmury dla wszystkich danych przed dezaktywacją urządzenia.</span><span class="sxs-lookup"><span data-stu-id="d61ac-126">If you plan to keep the device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="d61ac-127">Ta migawka w chmurze umożliwia odzyskanie wszystkich danych w późniejszym terminie.</span><span class="sxs-lookup"><span data-stu-id="d61ac-127">This cloud snapshot allows you to recover all the data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="d61ac-128">Dezaktywować urządzenie</span><span class="sxs-lookup"><span data-stu-id="d61ac-128">Deactivate a device</span></span>

<span data-ttu-id="d61ac-129">Aby dezaktywować urządzenie, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="d61ac-129">To deactivate your device, perform the following steps.</span></span>

#### <a name="to-deactivate-the-device"></a><span data-ttu-id="d61ac-130">Aby dezaktywować urządzenie</span><span class="sxs-lookup"><span data-stu-id="d61ac-130">To deactivate the device</span></span>

1. <span data-ttu-id="d61ac-131">W usłudze, przejdź do **zarządzania > urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="d61ac-131">In your service, go to **Management > Devices**.</span></span> <span data-ttu-id="d61ac-132">W **urządzeń** bloku, kliknij i wybierz urządzenia, które chcesz zdezaktywować.</span><span class="sxs-lookup"><span data-stu-id="d61ac-132">In the **Devices** blade, click and select the device that you wish to deactivate.</span></span>
   
    ![Wybierz urządzenie, aby zdezaktywować](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="d61ac-134">W Twojej **pulpitu nawigacyjnego urządzenia** bloku, kliknij przycisk **... Więcej** i wybierz z listy, **Dezaktywuj**.</span><span class="sxs-lookup"><span data-stu-id="d61ac-134">In your **Device dashboard** blade, click **… More** and from the list, select **Deactivate**.</span></span>
   
    ![Kliknij przycisk Dezaktywuj](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="d61ac-136">W **Dezaktywuj** bloku, wpisz nazwę urządzenia, a następnie kliknij przycisk **Dezaktywuj**.</span><span class="sxs-lookup"><span data-stu-id="d61ac-136">In the **Deactivate** blade, type the device name and then click **Deactivate**.</span></span> 
   
    ![Upewnij się, Dezaktywuj](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="d61ac-138">Proces Dezaktywuj uruchamia i może zająć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="d61ac-138">The deactivate process starts and takes a few minutes to complete.</span></span>
   
    ![Dezaktywuj w toku](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="d61ac-140">Po dezaktywacji Odświeża listę urządzeń.</span><span class="sxs-lookup"><span data-stu-id="d61ac-140">After deactivation, the list of devices refreshes.</span></span>
   
    ![Dezaktywuj ukończone](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="d61ac-142">Można teraz usunąć to urządzenie.</span><span class="sxs-lookup"><span data-stu-id="d61ac-142">You can now delete this device.</span></span>

## <a name="delete-the-device"></a><span data-ttu-id="d61ac-143">Usuwanie urządzenia</span><span class="sxs-lookup"><span data-stu-id="d61ac-143">Delete the device</span></span>

<span data-ttu-id="d61ac-144">Urządzenie ma najpierw są nieaktywne go usunąć.</span><span class="sxs-lookup"><span data-stu-id="d61ac-144">A device has to be first deactivated to delete it.</span></span> <span data-ttu-id="d61ac-145">Usuwanie urządzenia spowoduje usunięcie jej z listy urządzeń połączonych z usługą.</span><span class="sxs-lookup"><span data-stu-id="d61ac-145">Deleting a device removes it from the list of devices connected to the service.</span></span> <span data-ttu-id="d61ac-146">Usługę można zarządzać nie usunięto urządzenie.</span><span class="sxs-lookup"><span data-stu-id="d61ac-146">The service can then no longer manage the deleted device.</span></span> <span data-ttu-id="d61ac-147">Dane skojarzone z danym urządzeniem jednak pozostaje w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d61ac-147">The data associated with the device however remains in the cloud.</span></span> <span data-ttu-id="d61ac-148">Te dane zostały następnie naliczone opłaty.</span><span class="sxs-lookup"><span data-stu-id="d61ac-148">This data then accrues charges.</span></span>

<span data-ttu-id="d61ac-149">Aby usunąć urządzenie, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="d61ac-149">To delete the device, perform the following steps.</span></span>

#### <a name="to-delete-the-device"></a><span data-ttu-id="d61ac-150">Aby usunąć urządzenie</span><span class="sxs-lookup"><span data-stu-id="d61ac-150">To delete the device</span></span>

1. <span data-ttu-id="d61ac-151">W Menedżerze urządzeń StorSimple, przejdź do **zarządzania > urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="d61ac-151">In your StorSimple Device Manager, go to **Management > Devices**.</span></span> <span data-ttu-id="d61ac-152">W **urządzeń** bloku, wybierz dezaktywować urządzenie, które chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="d61ac-152">In the **Devices** blade, select a deactivated device that you wish to delete.</span></span>
2. <span data-ttu-id="d61ac-153">W **pulpitu nawigacyjnego urządzenia** bloku, kliknij przycisk **... Więcej** , a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="d61ac-153">In the **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Wybierz urządzenie, aby usunąć](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="d61ac-155">W **usunąć** bloku, wpisz nazwę urządzenia, aby potwierdzić zamiar usunięcia, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="d61ac-155">In the **Delete** blade, type the name of your device to confirm the deletion and then click **Delete**.</span></span> <span data-ttu-id="d61ac-156">Usunięcie urządzenia nie powoduje usunięcia danych powiązanych z urządzeniem w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d61ac-156">Deleting the device does not delete the cloud data associated with the device.</span></span> 
   
   ![Potwierdzenie usunięcia](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="d61ac-158">Usuwanie uruchamia i może zająć kilka minut.</span><span class="sxs-lookup"><span data-stu-id="d61ac-158">The deletion starts and takes a few minutes to complete.</span></span>
   
   ![Usuwanie w toku](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="d61ac-160">Po usunięciu urządzenia, można wyświetlić zaktualizowaną listę urządzeń.</span><span class="sxs-lookup"><span data-stu-id="d61ac-160">After the device is deleted, you can view the updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d61ac-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d61ac-161">Next steps</span></span>

* <span data-ttu-id="d61ac-162">Aby uzyskać informacje na temat sposobu pracy awaryjnej, przejdź do [trybu Failover i odzyskiwania po awarii macierzy wirtualnego StorSimple](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="d61ac-162">For information on how to fail over, go to [Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="d61ac-163">Aby dowiedzieć się więcej o sposobie używania usługi Menedżer StorSimple urządzeń, przejdź do [zarządzać tablica wirtualnego StorSimple przy użyciu usługi Menedżer StorSimple urządzenia](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d61ac-163">To learn more about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

