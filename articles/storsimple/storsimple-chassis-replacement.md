---
title: "Podstawa montażowa aaaReplace na urządzeniu z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooremove i Zamień hello obudowy StorSimple obudowy podstawowego lub EBOD obudowy."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="a1c47-103">Zastąp podstawę hello na urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="a1c47-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="a1c47-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a1c47-104">Overview</span></span>
<span data-ttu-id="a1c47-105">Ten samouczek wyjaśnia sposób tooremove i Zastąp podstawę urządzenia z serii StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="a1c47-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="a1c47-106">model Hello StorSimple 8100 to urządzenie jednej obudowie (wspólnej obudowie), hello 8600 jest urządzeniem podwójną obudowy (dwie obudowy).</span><span class="sxs-lookup"><span data-stu-id="a1c47-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="a1c47-107">W przypadku modelu 8600 są potencjalnie dwóch obudowy, które może nie działać na urządzeniu hello: hello podstawę dla podstawowego obudowa hello lub hello podstawę dla hello EBOD obudowy.</span><span class="sxs-lookup"><span data-stu-id="a1c47-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="a1c47-108">W obu przypadkach hello zastępczy podstawę, która jest dostarczany przez firmę Microsoft jest pusta.</span><span class="sxs-lookup"><span data-stu-id="a1c47-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="a1c47-109">Nie zasilania i chłodzenia modułów (PCMs), moduły kontrolera stacje dysków półprzewodnikowych (SSD), dysków twardych (HDD) lub EBOD moduły będą dołączone.</span><span class="sxs-lookup"><span data-stu-id="a1c47-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1c47-110">Przed usuwanie i zastępowanie hello obudowy, przejrzyj hello bezpieczeństwa informacji w [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="a1c47-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-chassis"></a><span data-ttu-id="a1c47-111">Usuń hello obudowy</span><span class="sxs-lookup"><span data-stu-id="a1c47-111">Remove hello chassis</span></span>
<span data-ttu-id="a1c47-112">Wykonaj następujące kroki tooremove hello obudowy na urządzeniu StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="a1c47-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="a1c47-113">tooremove podstawę</span><span class="sxs-lookup"><span data-stu-id="a1c47-113">tooremove a chassis</span></span>
1. <span data-ttu-id="a1c47-114">Upewnij się, urządzenia StorSimple hello jest zamknięta i odłączone od wszystkich źródeł zasilania hello.</span><span class="sxs-lookup"><span data-stu-id="a1c47-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="a1c47-115">Usuń wszystkie hello sieci i kabli SAS, jeśli ma to zastosowanie.</span><span class="sxs-lookup"><span data-stu-id="a1c47-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="a1c47-116">Usuń jednostkę hello z hello stojaku.</span><span class="sxs-lookup"><span data-stu-id="a1c47-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="a1c47-117">Usuń poszczególnych dysków hello i zanotuj hello miejsc, w których są usuwane.</span><span class="sxs-lookup"><span data-stu-id="a1c47-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="a1c47-118">Aby uzyskać więcej informacji, zobacz [Usuń dysk hello](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="a1c47-118">For more information, see [Remove hello disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="a1c47-119">Na powitania obudowa EBOD (jeśli jest to hello podstawę, która nie powiodła się) Usuń hello EBOD kontrolera modułów.</span><span class="sxs-lookup"><span data-stu-id="a1c47-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="a1c47-120">Aby uzyskać więcej informacji, zobacz [usunąć kontroler EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="a1c47-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span> 
   
    <span data-ttu-id="a1c47-121">Na powitania obudowa głównej (jeśli jest to hello podstawę, która nie powiodła się), Usuń kontrolery hello i pamiętaj hello miejsc, w których są usuwane.</span><span class="sxs-lookup"><span data-stu-id="a1c47-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="a1c47-122">Aby uzyskać więcej informacji, zobacz [usunąć kontroler](storsimple-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="a1c47-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="a1c47-123">Zainstaluj hello obudowy</span><span class="sxs-lookup"><span data-stu-id="a1c47-123">Install hello chassis</span></span>
<span data-ttu-id="a1c47-124">Wykonaj następujące kroki tooinstall hello obudowy na urządzeniu StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="a1c47-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="a1c47-125">tooinstall podstawę</span><span class="sxs-lookup"><span data-stu-id="a1c47-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="a1c47-126">Zainstaluj obudowy hello w stojaku hello.</span><span class="sxs-lookup"><span data-stu-id="a1c47-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="a1c47-127">Aby uzyskać więcej informacji, zobacz [urządzenia w stojaku do urządzenia 8100 StorSimple](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) lub [urządzenia w stojaku do urządzenia 8600 StorSimple](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="a1c47-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="a1c47-128">Po obudowy hello jest zainstalowany w stojaku hello, zainstalować moduły kontrolera hello w powitalne sam umieszcza poprzednio były zainstalowane w.</span><span class="sxs-lookup"><span data-stu-id="a1c47-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="a1c47-129">Zainstaluj hello dysków w hello sam umieszcza i gniazd poprzednio były zainstalowane w.</span><span class="sxs-lookup"><span data-stu-id="a1c47-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1c47-130">Firma Microsoft zaleca, aby najpierw zainstalować hello dyski SSD w gniazdach hello, a następnie zainstaluj hello dysków twardych.</span><span class="sxs-lookup"><span data-stu-id="a1c47-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
   > 
   > 
4. <span data-ttu-id="a1c47-131">Z urządzeniem hello zamontowane w stojaku hello i zainstalowane składniki hello Połącz źródła urządzenia toohello odpowiednie uprawnienia i Włącz hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a1c47-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="a1c47-132">Aby uzyskać więcej informacji, zobacz [Podłączanie kabli do urządzenia StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) lub [Podłączanie kabli do urządzenia StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="a1c47-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1c47-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a1c47-133">Next steps</span></span>
<span data-ttu-id="a1c47-134">Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="a1c47-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

