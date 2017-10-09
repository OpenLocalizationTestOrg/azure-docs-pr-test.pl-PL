---
title: "aaaReplace dysku na urządzeniu StorSimple | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak tooreplace dysku wpływają na obudowę głównej StorSimple lub obudowa EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d2c78a6d951b0f00ac42e74a34cf1bc83952a3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a><span data-ttu-id="82304-103">Zamień na dysku w urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="82304-103">Replace a disk drive on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="82304-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="82304-104">Overview</span></span>
<span data-ttu-id="82304-105">Ten samouczek wyjaśnia, jak zostanie usunięty i zastąpiony nieprawidłowe działanie lub uszkodzonego dysku twardego na urządzeniu Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="82304-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="82304-106">tooreplace dysku, musisz:</span><span class="sxs-lookup"><span data-stu-id="82304-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="82304-107">Odłączyć hello antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="82304-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="82304-108">Usuń dysk hello</span><span class="sxs-lookup"><span data-stu-id="82304-108">Remove hello disk drive</span></span>
* <span data-ttu-id="82304-109">Zainstaluj hello wymiany dysku</span><span class="sxs-lookup"><span data-stu-id="82304-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82304-110">Przed usunięcie i zastąpienie dysku, przejrzyj hello bezpieczeństwa informacji w [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="82304-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="82304-111">Odłączyć hello antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="82304-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="82304-112">Ta procedura wyjaśnia sposób hello antitamper blokad na urządzeniu StorSimple można zaangażowane lub odłączony podczas zastępowania hello dysków.</span><span class="sxs-lookup"><span data-stu-id="82304-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="82304-113">blokady antitamper Hello są zainstalowane w uchwytach operatora dysku hello i są one dostępne za pośrednictwem małych otwarcie w sekcji zatrzaśnięcia hello hello dojścia.</span><span class="sxs-lookup"><span data-stu-id="82304-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="82304-114">Dyski są dostarczane z hello blokad zestaw toohello zablokowany pozycji.</span><span class="sxs-lookup"><span data-stu-id="82304-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="82304-115">toounlock hello antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="82304-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="82304-116">Starannie wstawić hello blokady klucza ("tamperproof" T10 śrubokręt, otrzymany od firmy Microsoft) do otwarcie hello w uchwyt hello i jego gniazda.</span><span class="sxs-lookup"><span data-stu-id="82304-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="82304-117">Jeśli blokady antitamper hello jest aktywna, hello red wskaźnika jest widoczne w otwarcie hello.</span><span class="sxs-lookup"><span data-stu-id="82304-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
   > 
   > 
   
    ![Zablokowane dysku](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="82304-119">**Rysunek 1** blokady przed wykrycie zaangażowane</span><span class="sxs-lookup"><span data-stu-id="82304-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="82304-120">Etykieta</span><span class="sxs-lookup"><span data-stu-id="82304-120">Label</span></span> | <span data-ttu-id="82304-121">Opis</span><span class="sxs-lookup"><span data-stu-id="82304-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="82304-122">1</span><span class="sxs-lookup"><span data-stu-id="82304-122">1</span></span> |<span data-ttu-id="82304-123">Otwarcie wskaźnika</span><span class="sxs-lookup"><span data-stu-id="82304-123">Indicator aperture</span></span> |
   | <span data-ttu-id="82304-124">2</span><span class="sxs-lookup"><span data-stu-id="82304-124">2</span></span> |<span data-ttu-id="82304-125">Antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="82304-125">Antitamper lock</span></span> |
2. <span data-ttu-id="82304-126">Obróć hello klucz, w przeciwnym kierunku, dopóki hello czerwony wskaźnik nie jest widoczna w otwarcie hello powyżej hello klucza.</span><span class="sxs-lookup"><span data-stu-id="82304-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="82304-127">Usuń klucz hello.</span><span class="sxs-lookup"><span data-stu-id="82304-127">Remove hello key.</span></span>
   
    ![Odblokowany dysku](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="82304-129">**Rysunek 2** odblokowany dysku</span><span class="sxs-lookup"><span data-stu-id="82304-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="82304-130">można teraz usunąć Hello dysku.</span><span class="sxs-lookup"><span data-stu-id="82304-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="82304-131">Wykonaj kroki hello w odwrotnej tooengage hello blokady.</span><span class="sxs-lookup"><span data-stu-id="82304-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="82304-132">Usuń dysk hello</span><span class="sxs-lookup"><span data-stu-id="82304-132">Remove hello disk drive</span></span>
<span data-ttu-id="82304-133">Urządzenia StorSimple obsługuje konfiguracji RAID 10 przypominającej magazynu spacji.</span><span class="sxs-lookup"><span data-stu-id="82304-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="82304-134">Oznacza to, że aplikacja może działać normalnie z jednego dysku nie powiodło się, dysków półprzewodnikowych (SSD), lub dysku twardego dysku (HDD).</span><span class="sxs-lookup"><span data-stu-id="82304-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="82304-135">Jeśli w systemie jest więcej niż jednego dysku nie powiodło się, nie należy usuwać więcej niż jeden dysków SSD i HDD z systemu hello w dowolnym momencie w czasie.</span><span class="sxs-lookup"><span data-stu-id="82304-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="82304-136">W ten sposób może spowodować utratę danych.</span><span class="sxs-lookup"><span data-stu-id="82304-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="82304-137">Upewnij się, umieść zastępczy dysków SSD w miejscu, które wcześniej zawierało dysków SSD.</span><span class="sxs-lookup"><span data-stu-id="82304-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="82304-138">Podobnie umieść zastępczy dysk twardy w miejscu, które wcześniej zawierało dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="82304-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="82304-139">W hello klasycznego portalu Azure, miejsc są ponumerowane od 0 – 11.</span><span class="sxs-lookup"><span data-stu-id="82304-139">In hello Azure classic portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="82304-140">W związku z tym jeśli hello portal pokazuje, że dysk w gnieździe 2 nie powiodło się na urządzeniu hello szukać hello uszkodzony dysk w gnieździe trzeci powitania od góry powitania po lewej.</span><span class="sxs-lookup"><span data-stu-id="82304-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="82304-141">Dyski można usunięty i zastąpiony podczas hello systemu.</span><span class="sxs-lookup"><span data-stu-id="82304-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="82304-142">tooremove dysku</span><span class="sxs-lookup"><span data-stu-id="82304-142">tooremove a drive</span></span>
1. <span data-ttu-id="82304-143">tooidentify hello uszkodzonym dysku, w hello klasycznego portalu Azure, przejdź zbyt**urządzeń** > **konserwacji** > **stan sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="82304-143">tooidentify hello failed disk, in hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="82304-144">Ponieważ dysk może zakończyć się niepowodzeniem w obudowie głównej hello i/lub w obudowie EBOD (Jeśli używasz modelu 8600), przyjrzeć się stan hello hello dyski w obszarze **współużytkowanych składników** i w obszarze **EBOD obudowa współużytkowanych składników**.</span><span class="sxs-lookup"><span data-stu-id="82304-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared Components** and under **EBOD enclosure Shared Components**.</span></span> <span data-ttu-id="82304-145">Uszkodzony dysk w każdej obudowie będą wyświetlane z czerwonym oznaczeniem stanu.</span><span class="sxs-lookup"><span data-stu-id="82304-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="82304-146">Zlokalizuj hello dysków z przodu hello obudowa głównej hello lub hello EBOD obudowy.</span><span class="sxs-lookup"><span data-stu-id="82304-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="82304-147">Jeśli dysk hello jest odblokowany, przejdź toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="82304-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="82304-148">Jeśli dysk hello jest zablokowany, odblokuj go, wykonując procedurę hello w [odłączyć blokady antitamper hello](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="82304-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="82304-149">Naciśnij klawisz hello czarnym zatrzaśnięć hello dysku operator modułu i ściąganie hello dysku operator uchwytu wylogowanie i optymalizacji z przodu hello hello obudowy.</span><span class="sxs-lookup"><span data-stu-id="82304-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span> 
   
    ![Zwolnienie uchwytu dysku](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="82304-151">**Rysunek 3** zwolnienie hello dysku dojścia</span><span class="sxs-lookup"><span data-stu-id="82304-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="82304-152">Podczas pełni rozszerzania hello dysku operator uchwytu, przesuń operatora dysku hello poza hello obudowy.</span><span class="sxs-lookup"><span data-stu-id="82304-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![Przedłużanie dysku z dysku](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="82304-154">**Rysunek 4** przedłużanie hello dysku poza hello operatora</span><span class="sxs-lookup"><span data-stu-id="82304-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="82304-155">Zainstaluj hello wymiany dysku</span><span class="sxs-lookup"><span data-stu-id="82304-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="82304-156">Po dysku nie powiodło się w urządzeniu StorSimple i usunięto go, wykonaj tooreplace tej procedury za pomocą nowego dysku.</span><span class="sxs-lookup"><span data-stu-id="82304-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="82304-157">tooinsert dysku</span><span class="sxs-lookup"><span data-stu-id="82304-157">tooinsert a drive</span></span>
1. <span data-ttu-id="82304-158">Upewnij się, że dojście operatora dysku hello pełni zostanie rozszerzony, jak pokazano w powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="82304-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![Dysk z dojściem rozszerzone](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="82304-160">**Rysunek 5** dysku z dojściem rozszerzone</span><span class="sxs-lookup"><span data-stu-id="82304-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="82304-161">Slajd hello dysk nośnika końca hello w obudowie hello.</span><span class="sxs-lookup"><span data-stu-id="82304-161">Slide hello drive carrier all hello way into hello chassis.</span></span> 
   
    ![Przedłużanie dysku na dysk nośnika](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="82304-163">**Rysunek 6** ruchomej hello dysku operatora w obudowie hello</span><span class="sxs-lookup"><span data-stu-id="82304-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="82304-164">Z hello dysku operatora hello wstawiony, zamknij dysk nośnika dojściem podczas kontynuowanie toopush hello dysk nośnika do hello obudowy, dopóki hello dysku operator uchwytu przyciąganie w stanie zablokowanym.</span><span class="sxs-lookup"><span data-stu-id="82304-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="82304-165">Użyj hello blokady klucz dostarczony przez dojście operatora hello toosecure firmy Microsoft (tamperproof Torx śrubokręt) w miejscu przez włączenie gwintowanym blokady hello Włącz kwartału z ruchem wskazówek zegara.</span><span class="sxs-lookup"><span data-stu-id="82304-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="82304-166">Sprawdź, czy zastąpienia hello zakończyło się pomyślnie i działa hello dysku przez uzyskanie dostępu do hello klasycznego portalu Azure i nawigacja zbyt**konserwacji** > **stan sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="82304-166">Verify that hello replacement was successful and hello drive is operational by accessing hello Azure classic portal and navigating too**Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="82304-167">W obszarze **współużytkowanych składników** lub **składniki udostępnione obudowy EBOD**, stan dysku hello powinna być zielona, wskazujący, że jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="82304-167">Under **Shared Components** or **EBOD enclosure Shared Components**, hello drive status should be green, indicating that it is healthy.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="82304-168">Może upłynąć kilka godzin tooturn stan dysku hello zielonego po wymianie hello.</span><span class="sxs-lookup"><span data-stu-id="82304-168">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="82304-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="82304-169">Next steps</span></span>
<span data-ttu-id="82304-170">Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="82304-170">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

