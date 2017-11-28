---
title: "Blok podsumowania urządzenia wirtualnego tablicy aaaStorSimple | Dokumentacja firmy Microsoft"
description: "Zawiera opis bloku podsumowania urządzenia hello Menedżera urządzeń StorSimple i jak toouse go kondycji hello toomonitor macierzy wirtualne StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 3649eaac8a924a772f310a809ddf9706e912157a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-blade-for-storsimple-device-manager-connected-toostorsimple-virtual-array"></a><span data-ttu-id="8ad1e-103">Podsumowanie bloku urządzenia hello Użyj Menedżera urządzeń StorSimple połączone tooStorSimple wirtualnego tablicy</span><span class="sxs-lookup"><span data-stu-id="8ad1e-103">Use hello device summary blade for StorSimple Device Manager connected tooStorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="8ad1e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8ad1e-104">Overview</span></span>

<span data-ttu-id="8ad1e-105">Blok urządzenia StorSimple Menedżera urządzeń Hello zawiera widok podsumowania tablicy wirtualnego StorSimple, która jest zarejestrowana przy użyciu danego StorSimple Menedżera urządzeń, wyróżnianie tych problemów z urządzeniami, które wymagają uwagi administratora systemu.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-105">hello StorSimple Device Manager device blade provides a summary view of a StorSimple Virtual Array that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="8ad1e-106">W tym samouczku wprowadza hello urządzenia podsumowania bloku, opisano hello zawartości i funkcji oraz opisano hello zadania, które można wykonać z poziomu tego bloku.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-106">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="8ad1e-107">Podsumowanie bloku urządzenia Hello Wyświetla hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="8ad1e-107">hello device summary blade displays hello following information:</span></span>

![Pulpit nawigacyjny urządzenia](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a><span data-ttu-id="8ad1e-109">Zarządzanie</span><span class="sxs-lookup"><span data-stu-id="8ad1e-109">Management</span></span>

<span data-ttu-id="8ad1e-110">W bloku urządzenia StorSimple hello zobacz temat hello opcje służące do zarządzania urządzeniem StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-110">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="8ad1e-111">Widzisz polecenia zarządzania hello hello górze bloku hello i po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-111">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="8ad1e-112">Użyj tych opcji tooadd udziały lub woluminy lub tablica wirtualnej w tryb failover.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-112">Use these options tooadd shares or volumes, or update or fail over your virtual array.</span></span>

<span data-ttu-id="8ad1e-113">Witaj obszaru essentials przechwytuje niektóre hello ważne właściwości, takie jak, stan hello, modelu, wersji oprogramowania, jak również toohello łącze **interfejsu użytkownika sieci Web** hello tablicy.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-113">hello essentials area captures some of hello important properties such as, hello status, model, software version as well as a link toohello **Web UI** of hello array.</span></span> <span data-ttu-id="8ad1e-114">Jeśli w sieci wewnętrznej, możesz bezpośrednio uruchomić hello [lokalnego interfejsu użytkownika sieci web](storsimple-ova-web-ui-admin.md) tooadminister tablica wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-114">If you are on an internal network, you can directly launch hello [local web UI](storsimple-ova-web-ui-admin.md) tooadminister your virtual array.</span></span>

![Podstawowe informacje dotyczące urządzeń](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a><span data-ttu-id="8ad1e-116">Podsumowanie urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="8ad1e-116">StorSimple device summary</span></span>

* <span data-ttu-id="8ad1e-117">Witaj **alerty** kafelka zapewnia migawkę wszystkie aktywne alerty hello wirtualnego tablica, pogrupowane według ważności alertu.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-117">hello **Alerts** tile provides a snapshot of all hello active alerts for your virtual array, grouped by alert severity.</span></span> <span data-ttu-id="8ad1e-118">Kliknij przycisk hello kafelka tooopen hello **alerty** bloku, a następnie kliknij przycisk indywidualnym alertów tooview dodatkowe szczegóły dotyczące alertu, wraz ze wszystkimi zalecane akcje.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-118">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="8ad1e-119">Można także wyczyścić hello alert, jeśli hello problem został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-119">You can also clear hello alert if hello issue has been resolved.</span></span>

* <span data-ttu-id="8ad1e-120">Witaj **pojemności** kafelka Wyświetla hello podstawowego magazynu, który zostanie zainicjowana i pozostałych między hello urządzenia wirtualnego względną toohello całkowita ilość miejsca dostępne dla hello takie same.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-120">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello virtual device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="8ad1e-121">**Zainicjowano obsługę administracyjną** odwołuje się toohello ilość miejsca w magazynie, który jest przygotowany i przydzielona do użycia, **pozostała** odwołuje się toohello pozostałych pojemności, które można udostępnić w tym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-121">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> <span data-ttu-id="8ad1e-122">Hello **pozostałych do warstwy** pojemność to hello dostępnej pojemności, który można udostępnić, łącznie z chmury, podczas hello **pozostałych lokalnego** jest pojemność hello pozostały na dyskach hello dołączona toothis wirtualnego Tablica.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-122">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis virtual array.</span></span>

* <span data-ttu-id="8ad1e-123">W hello **użycia** wykresu, można wyświetlić hello magazyn podstawowy używany w tablicy wirtualnych, jak również magazynu w chmurze hello używane za pośrednictwem hello ostatnich 7 dni, hello domyślny okres czasu.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-123">In hello **Usage** chart, you can view hello primary storage used across your virtual array, as well as hello cloud storage consumed  over hello past 7 days, hello default time period.</span></span> <span data-ttu-id="8ad1e-124">Użyj hello **Edytuj** opcji hello prawym górnym rogu toochoose wykresu hello skali innym czasie.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-124">Use hello **Edit** option in hello top-right corner of hello chart toochoose a different time scale.</span></span>

* <span data-ttu-id="8ad1e-125">Witaj **udziałów** lub **woluminów** kafelka zawiera podsumowanie liczby hello udziały lub woluminy w urządzeniu pogrupowane według stanu.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-125">hello **Shares** or **Volumes** tile provides a summary of hello number of shares or volumes in your device grouped by status.</span></span> <span data-ttu-id="8ad1e-126">Kliknij przycisk hello kafelka tooopen hello **udziałów** lub **woluminów** listy bloku, a następnie kliknij na poszczególnych tooview w udziale lub woluminie lub zmodyfikować jego właściwości.</span><span class="sxs-lookup"><span data-stu-id="8ad1e-126">Click hello tile tooopen hello **Shares**  or **Volumes** list blade, and then click on an individual share or volume tooview or modify its properties.</span></span> <span data-ttu-id="8ad1e-127">Aby uzyskać więcej informacji, zobacz temat jak zbyt[Zarządzanie udziałami](storsimple-virtual-array-manage-shares.md) lub [Zarządzanie woluminami](storsimple-virtual-array-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="8ad1e-127">For more information, see how too[manage shares](storsimple-virtual-array-manage-shares.md) or [manage volumes](storsimple-virtual-array-manage-volumes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ad1e-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8ad1e-128">Next steps</span></span>
<span data-ttu-id="8ad1e-129">Instrukcje:</span><span class="sxs-lookup"><span data-stu-id="8ad1e-129">Learn how to:</span></span>
- [<span data-ttu-id="8ad1e-130">Zarządzanie udziałami w macierzy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="8ad1e-130">Manage shares on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-shares.md)
    
- [<span data-ttu-id="8ad1e-131">Zarządzanie woluminami w macierzy wirtualnego StorSimple</span><span class="sxs-lookup"><span data-stu-id="8ad1e-131">Manage volumes on a StorSimple Virtual Array</span></span>](storsimple-virtual-array-manage-volumes.md)

