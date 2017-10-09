---
title: "urządzenie serii StorSimple 8000 aaaUse podsumowania | Dokumentacja firmy Microsoft"
description: "Opisuje urządzenie usługi Menedżer StorSimple urządzenia hello podsumowania i w jaki sposób toouse on tooview magazynu metryki i inicjatorów połączonych i Znajdź hello numer seryjny i IQN."
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="559d0-103">Używanie urządzenia hello podsumowania w usłudze Menedżer StorSimple urządzenia</span><span class="sxs-lookup"><span data-stu-id="559d0-103">Use hello device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="559d0-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="559d0-104">Overview</span></span>
<span data-ttu-id="559d0-105">Blok podsumowania urządzenia StorSimple Hello zawiera przegląd informacji dla określonego urządzenia StorSimple, natomiast toohello usługi podsumowania bloku, który zawiera informacje o wszystkich urządzeniach hello zawarte w rozwiązaniu Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="559d0-105">hello StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast toohello service summary blade, which gives you information about all hello devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="559d0-106">Podsumowanie bloku urządzenia Hello zawiera widok podsumowania urządzenia serii StorSimple 8000, który jest zarejestrowany z danym urządzeniem Menedżer StorSimple, wyróżnianie tych problemów z urządzeniami, które wymagają uwagi administratora systemu.</span><span class="sxs-lookup"><span data-stu-id="559d0-106">hello device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="559d0-107">W tym samouczku wprowadza hello urządzenia podsumowania bloku, opisano hello zawartości i funkcji oraz opisano hello zadania, które można wykonać z poziomu tego bloku.</span><span class="sxs-lookup"><span data-stu-id="559d0-107">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="559d0-108">Podsumowanie bloku urządzenia Hello Wyświetla hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="559d0-108">hello device summary blade displays hello following information:</span></span>

![Podsumowanie bloku urządzenia](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="559d0-110">Pasek poleceń zarządzania</span><span class="sxs-lookup"><span data-stu-id="559d0-110">Management command bar</span></span>

<span data-ttu-id="559d0-111">W bloku urządzenia StorSimple hello zobacz temat hello opcje służące do zarządzania urządzeniem StorSimple.</span><span class="sxs-lookup"><span data-stu-id="559d0-111">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="559d0-112">Widzisz polecenia zarządzania hello hello górze bloku hello i po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="559d0-112">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="559d0-113">Użyj tych opcji tooadd udziały lub woluminy lub urządzenie w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="559d0-113">Use these options tooadd shares or volumes, or update or fail over your device.</span></span>

![Pasek poleceń zarządzania](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="559d0-115">Podstawy</span><span class="sxs-lookup"><span data-stu-id="559d0-115">Essentials</span></span>

<span data-ttu-id="559d0-116">obszar essentials Hello przechwytuje niektórych hello ważne właściwości, takie jak, stan hello, modelu, docelowy IQN i hello wersji oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="559d0-116">hello essentials area captures some of hello important properties such as, hello status, model, target IQN, and hello software version.</span></span> 

![Podstawowe informacje dotyczące urządzeń](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="559d0-118">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="559d0-118">Monitoring</span></span>

* <span data-ttu-id="559d0-119">Witaj **alerty** kafelka zawiera migawkę wszystkich hello aktywne alerty dla danego urządzenia, pogrupowane według ważności alertu.</span><span class="sxs-lookup"><span data-stu-id="559d0-119">hello **Alerts** tile provides a snapshot of all hello active alerts for your device, grouped by alert severity.</span></span>

    ![Kafelek alertu](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="559d0-121">Kliknij przycisk hello kafelka tooopen hello **alerty** bloku, a następnie kliknij przycisk indywidualnym alertów tooview dodatkowe szczegóły dotyczące alertu, wraz ze wszystkimi zalecane akcje.</span><span class="sxs-lookup"><span data-stu-id="559d0-121">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="559d0-122">Można także wyczyścić hello alert, jeśli hello problem został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="559d0-122">You can also clear hello alert if hello issue has been resolved.</span></span>

    ![Kliknij Kafelek alertu](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="559d0-124">Witaj **stanu i kondycji** kafelka zapewnia wgląd w kondycja składnika hello sprzętu dla urządzeń, w tym stan urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="559d0-124">hello **Status and health** tile provides insights into hello hardware component health for a device including hello device status.</span></span> <span data-ttu-id="559d0-125">Stan urządzenia Hello może być w trybie offline, online, dezaktywować lub gotowe tooset aktywne.</span><span class="sxs-lookup"><span data-stu-id="559d0-125">hello device status may be offline, online, deactivated, or ready tooset up.</span></span>

    ![Kafelek stanu i kondycji](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="559d0-127">Witaj **woluminów** kafelka zawiera podsumowanie liczby hello woluminów w urządzeniu pogrupowane według stanu.</span><span class="sxs-lookup"><span data-stu-id="559d0-127">hello **Volumes** tile provides a summary of hello number of volumes in your device grouped by status.</span></span>

    ![Kafelka woluminy](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="559d0-129">Kliknij przycisk hello kafelka tooopen hello **woluminów** listy bloku, a następnie kliknij na tooview poszczególnych woluminów lub zmodyfikować jego właściwości.</span><span class="sxs-lookup"><span data-stu-id="559d0-129">Click hello tile tooopen hello **Volumes** list blade, and then click on an individual volume tooview or modify its properties.</span></span>
    
    ![Kliknij Kafelek woluminów](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="559d0-131">Aby uzyskać więcej informacji, zobacz temat jak zbyt[Zarządzanie woluminami](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="559d0-131">For more information, see how too[manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="559d0-132">W hello **użycia** wykresu, można wyświetlić hello magazynu podstawowy używany przez urządzenia i magazynu w chmurze hello używane za pośrednictwem hello ostatnich 7 dni, hello domyślny okres czasu.</span><span class="sxs-lookup"><span data-stu-id="559d0-132">In hello **Usage** chart, you can view hello primary storage used across your device, and hello cloud storage consumed over hello past 7 days, hello default time period.</span></span>

     ![Kafelek użycie](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="559d0-134">toochoose przedział czasu różnych Użyj hello **Edytuj** opcji w hello prawym górnym rogu wykresu hello.</span><span class="sxs-lookup"><span data-stu-id="559d0-134">toochoose a different time scale, use hello **Edit** option in hello top-right corner of hello chart.</span></span>

     ![Edytuj wykres użycia](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="559d0-136">Na tym wykresie można wyświetlać metryki dla hello głównej pamięci masowej (hello ilość danych zapisanych przez urządzenie tooyour hostów) i hello całkowita liczba zużywane przez urządzenie w danym okresie czasu magazynu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="559d0-136">In this chart, you can view metrics for hello total primary storage (hello amount of data written by hosts tooyour device) and hello total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="559d0-137">W tym kontekście *magazynu głównego* odwołuje się toohello łączną ilość danych zapisanych przez hosta hello i mogą być podzielone przez typ woluminu: *podstawowego do warstwy magazynu* obejmuje zarówno lokalnie przechowywanych danych i danych Chmura toohello warstwowego.</span><span class="sxs-lookup"><span data-stu-id="559d0-137">In this context, *primary storage* refers toohello total amount of data written by hello host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered toohello cloud.</span></span> <span data-ttu-id="559d0-138">*Podstawowy przypięty lokalnie magazynu* zawiera tylko dane przechowywane lokalnie.</span><span class="sxs-lookup"><span data-stu-id="559d0-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="559d0-139">*Magazyn w chmurze*, na hello drugiej, to miara hello łączną ilość danych przechowywanych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="559d0-139">*Cloud storage*, on hello other hand, is a measurement of hello total amount of data stored in hello cloud.</span></span> <span data-ttu-id="559d0-140">Ten magazyn zawiera warstwowych danych i tworzenie kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="559d0-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="559d0-141">Witaj danych przechowywanych w chmurze hello jest deduplikowany i skompresowane magazynu podstawowego wskazuje ilość hello Magazyn używany przed danych hello jest deduplikowany i skompresowane.</span><span class="sxs-lookup"><span data-stu-id="559d0-141">hello data stored in hello cloud is deduplicated and compressed, whereas primary storage indicates hello amount of storage used before hello data is deduplicated and compressed.</span></span> <span data-ttu-id="559d0-142">(Możesz porównać tych dwóch liczb tooget pomysł szybkość kompresji hello). Dla obu lokacji podstawowej i magazynu, hello kwotach są oparte na powitania śledzenia częstotliwości należy skonfigurować w chmurze.</span><span class="sxs-lookup"><span data-stu-id="559d0-142">(You can compare these two numbers tooget an idea of hello compression rate.) For both primary and cloud storage, hello amounts shown are based on hello tracking frequency you configure.</span></span> <span data-ttu-id="559d0-143">Na przykład jeśli częstotliwość tydzień, hello wykresu zawiera dane dla poszczególnych dni w hello poprzedniego tygodnia.</span><span class="sxs-lookup"><span data-stu-id="559d0-143">For example, if you choose a one week frequency, then hello chart shows data for each day in hello previous week.</span></span>

     <span data-ttu-id="559d0-144">toosee hello ilość magazynu w chmurze używane w czasie, wybierz hello **używany Magazyn w CHMURZE** opcji.</span><span class="sxs-lookup"><span data-stu-id="559d0-144">toosee hello amount of cloud storage consumed over time, select hello **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="559d0-145">toosee hello całkowita ilość miejsca, która została zapisana przez hosta hello, wybierz hello **podstawowego do warstwy MAGAZYNU używane** i **głównej LOKALNIE PRZYPIĘTY Magazyn używany** opcje.</span><span class="sxs-lookup"><span data-stu-id="559d0-145">toosee hello total storage that has been written by hello host, select hello **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="559d0-146">Aby uzyskać więcej informacji, zobacz [Użyj hello toomonitor usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="559d0-146">For more information, see [Use hello StorSimple Device Manager service toomonitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="559d0-147">Witaj **pojemności** kafelka Wyświetla hello podstawowego magazynu, który zostanie zainicjowana i pozostałych między hello urządzenia względną toohello całkowita ilość miejsca dostępne dla hello takie same.</span><span class="sxs-lookup"><span data-stu-id="559d0-147">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="559d0-148">**Zainicjowano obsługę administracyjną** odwołuje się toohello ilość miejsca w magazynie, który jest przygotowany i przydzielona do użycia, **pozostała** odwołuje się toohello pozostałych pojemności, które można udostępnić w tym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="559d0-148">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> 

    ![Kafelek użycie](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="559d0-150">Kliknij ten tooview kafelka jak pojemności hello zostanie zainicjowana na woluminach warstwowych i przypiętych lokalnie.</span><span class="sxs-lookup"><span data-stu-id="559d0-150">Click this tile tooview how hello capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="559d0-151">Hello **pozostałych do warstwy** pojemność to hello dostępnej pojemności, który można udostępnić, łącznie z chmury, podczas hello **pozostałych lokalnego** jest pojemność hello pozostały na dyskach hello dołączonego urządzenia toothis.</span><span class="sxs-lookup"><span data-stu-id="559d0-151">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis device.</span></span>

    ![Kliknij wykres użycia](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="559d0-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="559d0-153">Next steps</span></span>
* <span data-ttu-id="559d0-154">Dowiedz się więcej o hello [bloku podsumowania usługi StorSimple](storsimple-8000-service-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="559d0-154">Learn more about hello [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="559d0-155">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="559d0-155">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

