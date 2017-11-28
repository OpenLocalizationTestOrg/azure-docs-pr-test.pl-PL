---
title: "aaaDeactivate i usunąć Microsoft Azure StorSimple wirtualnego tablicą | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooremove urządzenia StorSimple z usługi najpierw dezaktywowanie go, a następnie usuwając go."
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
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="a347b-103">Dezaktywuj i Usuń macierz wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="a347b-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="a347b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a347b-104">Overview</span></span>

<span data-ttu-id="a347b-105">Po dezaktywowaniu tablicą wirtualnego StorSimple, Podziel się hello połączenie między urządzeniem hello a hello odpowiedniej usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a347b-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="a347b-106">Ten samouczek wyjaśnia, jak:</span><span class="sxs-lookup"><span data-stu-id="a347b-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="a347b-107">Dezaktywować urządzenie</span><span class="sxs-lookup"><span data-stu-id="a347b-107">Deactivate a device</span></span> 
* <span data-ttu-id="a347b-108">Usuwanie urządzenia dezaktywowany</span><span class="sxs-lookup"><span data-stu-id="a347b-108">Delete a deactivated device</span></span>

<span data-ttu-id="a347b-109">informacje Hello w tym artykule dotyczą tylko tooStorSimple tablice wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="a347b-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="a347b-110">Informacji o serii 8000, zobaczyć toohow zbyt[dezaktywację lub usunięcie urządzenia](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="a347b-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="a347b-111">Gdy toodeactivate?</span><span class="sxs-lookup"><span data-stu-id="a347b-111">When toodeactivate?</span></span>

<span data-ttu-id="a347b-112">Dezaktywacja jest operacją trwałe i nie można cofnąć.</span><span class="sxs-lookup"><span data-stu-id="a347b-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="a347b-113">Nie można zarejestrować ponownie dezaktywować urządzenie z hello usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a347b-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="a347b-114">Należy może toodeactivate i Usuń macierz wirtualnego StorSimple w hello następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="a347b-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="a347b-115">**Planowana praca awaryjna** : urządzenie jest w trybie online i planujesz toofail przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="a347b-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="a347b-116">Jeśli planujesz tooupgrade tooa większych urządzenia może być konieczne toofail przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="a347b-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="a347b-117">Po przekazania własności danych hello i hello przejścia w tryb failover, urządzenia źródłowego hello są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="a347b-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="a347b-118">**Nieplanowane przełączenie awaryjne** : urządzenie jest w trybie offline, należy toofail za pośrednictwem hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a347b-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="a347b-119">W tym scenariuszu może wystąpić podczas awarii, gdy w centrum danych hello jest awarii i urządzenia podstawowej nie działa.</span><span class="sxs-lookup"><span data-stu-id="a347b-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="a347b-120">Planujesz toofail za pośrednictwem urządzenia pomocniczego tooa hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a347b-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="a347b-121">Po przekazania własności danych hello i hello przejścia w tryb failover, urządzenia źródłowego hello są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="a347b-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="a347b-122">**Likwidowanie** : toodecommission hello urządzenie.</span><span class="sxs-lookup"><span data-stu-id="a347b-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="a347b-123">Wymaga to toofirst dezaktywować urządzenie hello i usuń go.</span><span class="sxs-lookup"><span data-stu-id="a347b-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="a347b-124">Po dezaktywacji urządzenia może już uzyskać dostępu do żadnych danych, który jest przechowywany lokalnie.</span><span class="sxs-lookup"><span data-stu-id="a347b-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="a347b-125">Można tylko dostępu i odzyskiwanie danych hello przechowywanych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="a347b-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="a347b-126">Jeśli planujesz danych urządzenia hello tookeep po dezaktywacji, następnie należy podjąć migawkę chmury dla wszystkich danych przed dezaktywacją urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a347b-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="a347b-127">Ta migawka w chmurze pozwala toorecover hello wszystkich danych, aby w późniejszym terminie.</span><span class="sxs-lookup"><span data-stu-id="a347b-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="a347b-128">Dezaktywować urządzenie</span><span class="sxs-lookup"><span data-stu-id="a347b-128">Deactivate a device</span></span>

<span data-ttu-id="a347b-129">toodeactivate urządzenie, wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="a347b-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="a347b-130">toodeactivate hello urządzenia</span><span class="sxs-lookup"><span data-stu-id="a347b-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="a347b-131">W usłudze Przejdź zbyt**zarządzania > urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="a347b-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="a347b-132">W hello **urządzeń** bloku, kliknij i hello wybierz urządzenia, że chcesz toodeactivate.</span><span class="sxs-lookup"><span data-stu-id="a347b-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![Wybierz urządzenie toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="a347b-134">W Twojej **pulpitu nawigacyjnego urządzenia** bloku, kliknij przycisk **... Więcej** i wybierz z listy hello **Dezaktywuj**.</span><span class="sxs-lookup"><span data-stu-id="a347b-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![Kliknij przycisk Dezaktywuj](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="a347b-136">W hello **Dezaktywuj** bloku, nazwy urządzenia hello typu, a następnie kliknij przycisk **Dezaktywuj**.</span><span class="sxs-lookup"><span data-stu-id="a347b-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![Upewnij się, Dezaktywuj](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="a347b-138">Witaj Dezaktywuj uruchamia proces i zajmuje kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a347b-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![Dezaktywuj w toku](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="a347b-140">Po dezaktywacji odświeża hello listy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="a347b-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![Dezaktywuj ukończone](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="a347b-142">Można teraz usunąć to urządzenie.</span><span class="sxs-lookup"><span data-stu-id="a347b-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="a347b-143">Usuwanie urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="a347b-143">Delete hello device</span></span>

<span data-ttu-id="a347b-144">Urządzenie ma pierwszy toodelete dezaktywowane toobe go.</span><span class="sxs-lookup"><span data-stu-id="a347b-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="a347b-145">Usuwanie urządzenia spowoduje usunięcie jej z listy hello usługi toohello podłączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="a347b-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="a347b-146">Usługa Hello można zarządzać już hello usunąć urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a347b-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="a347b-147">dane Hello skojarzone z urządzeniem hello jednak pozostaje w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="a347b-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="a347b-148">Te dane zostały następnie naliczone opłaty.</span><span class="sxs-lookup"><span data-stu-id="a347b-148">This data then accrues charges.</span></span>

<span data-ttu-id="a347b-149">toodelete hello urządzenie, wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="a347b-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="a347b-150">toodelete hello urządzenia</span><span class="sxs-lookup"><span data-stu-id="a347b-150">toodelete hello device</span></span>

1. <span data-ttu-id="a347b-151">W Menedżerze urządzeń StorSimple, przejdź zbyt**zarządzania > urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="a347b-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="a347b-152">W hello **urządzeń** bloku, wybierz dezaktywować urządzenie, że chcesz toodelete.</span><span class="sxs-lookup"><span data-stu-id="a347b-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="a347b-153">W hello **pulpitu nawigacyjnego urządzenia** bloku, kliknij przycisk **... Więcej** , a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="a347b-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Wybierz urządzenie toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="a347b-155">W hello **usunąć** bloku, nazwa typu hello Twoje urządzenie tooconfirm hello usunięcia, a następnie kliknij przycisk **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="a347b-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="a347b-156">Usuwanie urządzenia hello nie powoduje usunięcia danych chmury hello skojarzone z urządzeniem hello.</span><span class="sxs-lookup"><span data-stu-id="a347b-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![Potwierdzenie usunięcia](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="a347b-158">Usuwanie Hello uruchamia i zajmuje kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a347b-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![Usuwanie w toku](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="a347b-160">Po usunięciu urządzenia hello można wyświetlić hello aktualizacji listy urządzeń.</span><span class="sxs-lookup"><span data-stu-id="a347b-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a347b-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a347b-161">Next steps</span></span>

* <span data-ttu-id="a347b-162">Aby uzyskać informacje na temat toofail, przejdź zbyt[trybu Failover i odzyskiwania po awarii macierzy wirtualnego StorSimple](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="a347b-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="a347b-163">więcej informacji o toolearn, jak hello toouse usługi Menedżer StorSimple urządzenia go za[Użyj hello tooadminister usługi Menedżer StorSimple urządzenia wirtualnego StorSimple tablica](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a347b-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

