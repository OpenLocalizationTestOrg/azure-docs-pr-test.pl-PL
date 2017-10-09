---
title: "aaaReplace dysku na urządzeniu z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak tooreplace dysku wpływają na obudowę głównej StorSimple lub obudowa EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 073/2017
ms.author: alkohli
ms.openlocfilehash: 09c1bf5e97adf54a609a868e921351bc63e00a83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="11e9f-103">Zamień na urządzeniu z serii StorSimple 8000 dysku</span><span class="sxs-lookup"><span data-stu-id="11e9f-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="11e9f-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="11e9f-104">Overview</span></span>
<span data-ttu-id="11e9f-105">Ten samouczek wyjaśnia, jak zostanie usunięty i zastąpiony nieprawidłowe działanie lub uszkodzonego dysku twardego na urządzeniu Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="11e9f-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="11e9f-106">tooreplace dysku, musisz:</span><span class="sxs-lookup"><span data-stu-id="11e9f-106">tooreplace a disk drive, you need to:</span></span>

* <span data-ttu-id="11e9f-107">Odłączyć hello antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="11e9f-107">Disengage hello antitamper lock</span></span>
* <span data-ttu-id="11e9f-108">Usuń dysk hello</span><span class="sxs-lookup"><span data-stu-id="11e9f-108">Remove hello disk drive</span></span>
* <span data-ttu-id="11e9f-109">Zainstaluj hello wymiany dysku</span><span class="sxs-lookup"><span data-stu-id="11e9f-109">Install hello replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11e9f-110">Przed usunięcie i zastąpienie dysku, przejrzyj hello bezpieczeństwa informacji w [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="11e9f-110">Before removing and replacing a disk drive, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-hello-antitamper-lock"></a><span data-ttu-id="11e9f-111">Odłączyć hello antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="11e9f-111">Disengage hello antitamper lock</span></span>
<span data-ttu-id="11e9f-112">Ta procedura wyjaśnia sposób hello antitamper blokad na urządzeniu StorSimple można zaangażowane lub odłączony podczas zastępowania hello dysków.</span><span class="sxs-lookup"><span data-stu-id="11e9f-112">This procedure explains how hello antitamper locks on your StorSimple device can be engaged or disengaged when you replace hello disk drives.</span></span> <span data-ttu-id="11e9f-113">blokady antitamper Hello są zainstalowane w uchwytach operatora dysku hello i są one dostępne za pośrednictwem małych otwarcie w sekcji zatrzaśnięcia hello hello dojścia.</span><span class="sxs-lookup"><span data-stu-id="11e9f-113">hello antitamper locks are fitted in hello drive carrier handles, and they are accessed through a small aperture in hello latch section of hello handle.</span></span> <span data-ttu-id="11e9f-114">Dyski są dostarczane z hello blokad zestaw toohello zablokowany pozycji.</span><span class="sxs-lookup"><span data-stu-id="11e9f-114">Drives are supplied with hello locks set toohello locked position.</span></span>

#### <a name="toounlock-hello-antitamper-lock"></a><span data-ttu-id="11e9f-115">toounlock hello antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="11e9f-115">toounlock hello antitamper lock</span></span>
1. <span data-ttu-id="11e9f-116">Starannie wstawić hello blokady klucza ("tamperproof" T10 śrubokręt, otrzymany od firmy Microsoft) do otwarcie hello w uchwyt hello i jego gniazda.</span><span class="sxs-lookup"><span data-stu-id="11e9f-116">Carefully insert hello lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into hello aperture in hello handle and into its socket.</span></span> 
   
   <span data-ttu-id="11e9f-117">Jeśli blokady antitamper hello jest aktywna, hello red wskaźnika jest widoczne w otwarcie hello.</span><span class="sxs-lookup"><span data-stu-id="11e9f-117">If hello antitamper lock is activated, hello red indicator is visible in hello aperture.</span></span>
  
    ![Zablokowane dysku](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="11e9f-119">**Rysunek 1** blokady przed wykrycie zaangażowane</span><span class="sxs-lookup"><span data-stu-id="11e9f-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="11e9f-120">Etykieta</span><span class="sxs-lookup"><span data-stu-id="11e9f-120">Label</span></span> | <span data-ttu-id="11e9f-121">Opis</span><span class="sxs-lookup"><span data-stu-id="11e9f-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="11e9f-122">1</span><span class="sxs-lookup"><span data-stu-id="11e9f-122">1</span></span> |<span data-ttu-id="11e9f-123">Otwarcie wskaźnika</span><span class="sxs-lookup"><span data-stu-id="11e9f-123">Indicator aperture</span></span> |
   | <span data-ttu-id="11e9f-124">2</span><span class="sxs-lookup"><span data-stu-id="11e9f-124">2</span></span> |<span data-ttu-id="11e9f-125">Antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="11e9f-125">Antitamper lock</span></span> |
2. <span data-ttu-id="11e9f-126">Obróć hello klucz, w przeciwnym kierunku, dopóki hello czerwony wskaźnik nie jest widoczna w otwarcie hello powyżej hello klucza.</span><span class="sxs-lookup"><span data-stu-id="11e9f-126">Rotate hello key in an anticlockwise direction until hello red indicator is not visible in hello aperture above hello key.</span></span>
3. <span data-ttu-id="11e9f-127">Usuń klucz hello.</span><span class="sxs-lookup"><span data-stu-id="11e9f-127">Remove hello key.</span></span>
   
    ![Odblokowany dysku](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="11e9f-129">**Rysunek 2** odblokowany dysku</span><span class="sxs-lookup"><span data-stu-id="11e9f-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="11e9f-130">można teraz usunąć Hello dysku.</span><span class="sxs-lookup"><span data-stu-id="11e9f-130">hello disk drive can now be removed.</span></span>

<span data-ttu-id="11e9f-131">Wykonaj kroki hello w odwrotnej tooengage hello blokady.</span><span class="sxs-lookup"><span data-stu-id="11e9f-131">Follow hello steps in reverse tooengage hello lock.</span></span>

## <a name="remove-hello-disk-drive"></a><span data-ttu-id="11e9f-132">Usuń dysk hello</span><span class="sxs-lookup"><span data-stu-id="11e9f-132">Remove hello disk drive</span></span>
<span data-ttu-id="11e9f-133">Urządzenia StorSimple obsługuje konfiguracji RAID 10 przypominającej magazynu spacji.</span><span class="sxs-lookup"><span data-stu-id="11e9f-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="11e9f-134">Oznacza to, że aplikacja może działać normalnie z jednego dysku nie powiodło się, dysków półprzewodnikowych (SSD), lub dysku twardego dysku (HDD).</span><span class="sxs-lookup"><span data-stu-id="11e9f-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="11e9f-135">Jeśli w systemie jest więcej niż jednego dysku nie powiodło się, nie należy usuwać więcej niż jeden dysków SSD i HDD z systemu hello w dowolnym momencie w czasie.</span><span class="sxs-lookup"><span data-stu-id="11e9f-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from hello system at any point in time.</span></span> <span data-ttu-id="11e9f-136">W ten sposób może spowodować utratę danych.</span><span class="sxs-lookup"><span data-stu-id="11e9f-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="11e9f-137">Upewnij się, umieść zastępczy dysków SSD w miejscu, które wcześniej zawierało dysków SSD.</span><span class="sxs-lookup"><span data-stu-id="11e9f-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="11e9f-138">Podobnie umieść zastępczy dysk twardy w miejscu, które wcześniej zawierało dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="11e9f-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="11e9f-139">W portalu Azure hello, miejsc są ponumerowane od 0 – 11.</span><span class="sxs-lookup"><span data-stu-id="11e9f-139">In hello Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="11e9f-140">W związku z tym jeśli hello portal pokazuje, że dysk w gnieździe 2 nie powiodło się na urządzeniu hello szukać hello uszkodzony dysk w gnieździe trzeci powitania od góry powitania po lewej.</span><span class="sxs-lookup"><span data-stu-id="11e9f-140">Therefore, if hello portal shows that a disk in slot 2 has failed, on hello device, look for hello failed disk in hello third slot from hello top left.</span></span>
> 
> 

<span data-ttu-id="11e9f-141">Dyski można usunięty i zastąpiony podczas hello systemu.</span><span class="sxs-lookup"><span data-stu-id="11e9f-141">Drives can be removed and replaced while hello system is operating.</span></span>

#### <a name="tooremove-a-drive"></a><span data-ttu-id="11e9f-142">tooremove dysku</span><span class="sxs-lookup"><span data-stu-id="11e9f-142">tooremove a drive</span></span>
1. <span data-ttu-id="11e9f-143">tooidentify hello dysku w hello portalu Azure Przejdź tooyour urządzenia nie powiodła się **Ustawienia > kondycji sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="11e9f-143">tooidentify hello failed disk, in hello Azure portal, go tooyour device **Settings > Hardware health**.</span></span> <span data-ttu-id="11e9f-144">Ponieważ dysk może zakończyć się niepowodzeniem w obudowie głównej hello i/lub w obudowie EBOD (Jeśli używasz modelu 8600), przyjrzeć się stan hello hello dyski w obszarze **udostępnione składniki** i w obszarze **EBOD udostępnione składniki** .</span><span class="sxs-lookup"><span data-stu-id="11e9f-144">Because a disk can fail in hello primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at hello status of hello disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="11e9f-145">Uszkodzony dysk w każdej obudowie będą wyświetlane z czerwonym oznaczeniem stanu.</span><span class="sxs-lookup"><span data-stu-id="11e9f-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="11e9f-146">Zlokalizuj hello dysków z przodu hello obudowa głównej hello lub hello EBOD obudowy.</span><span class="sxs-lookup"><span data-stu-id="11e9f-146">Locate hello drives in hello front of hello primary enclosure or hello EBOD enclosure.</span></span> 
3. <span data-ttu-id="11e9f-147">Jeśli dysk hello jest odblokowany, przejdź toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="11e9f-147">If hello disk is unlocked, proceed toohello next step.</span></span> <span data-ttu-id="11e9f-148">Jeśli dysk hello jest zablokowany, odblokuj go, wykonując procedurę hello w [odłączyć blokady antitamper hello](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="11e9f-148">If hello disk is locked, unlock it by following hello procedure in [Disengage hello antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="11e9f-149">Naciśnij klawisz hello czarnym zatrzaśnięć hello dysku operator modułu i ściąganie hello dysku operator uchwytu wylogowanie i optymalizacji z przodu hello hello obudowy.</span><span class="sxs-lookup"><span data-stu-id="11e9f-149">Press hello black latch on hello drive carrier module and pull hello drive carrier handle out and away from hello front of hello chassis.</span></span>
   
    ![Zwolnienie uchwytu dysku](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="11e9f-151">**Rysunek 3** zwolnienie hello dysku dojścia</span><span class="sxs-lookup"><span data-stu-id="11e9f-151">**Figure 3** Releasing hello drive handle</span></span>
5. <span data-ttu-id="11e9f-152">Podczas pełni rozszerzania hello dysku operator uchwytu, przesuń operatora dysku hello poza hello obudowy.</span><span class="sxs-lookup"><span data-stu-id="11e9f-152">When hello drive carrier handle is fully extended, slide hello drive carrier out of hello chassis.</span></span> 
   
    ![Przedłużanie dysku z dysku](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="11e9f-154">**Rysunek 4** przedłużanie hello dysku poza hello operatora</span><span class="sxs-lookup"><span data-stu-id="11e9f-154">**Figure 4** Sliding hello disk drive out of hello carrier</span></span>

## <a name="install-hello-replacement-disk-drive"></a><span data-ttu-id="11e9f-155">Zainstaluj hello wymiany dysku</span><span class="sxs-lookup"><span data-stu-id="11e9f-155">Install hello replacement disk drive</span></span>
<span data-ttu-id="11e9f-156">Po dysku nie powiodło się w urządzeniu StorSimple i usunięto go, wykonaj tooreplace tej procedury za pomocą nowego dysku.</span><span class="sxs-lookup"><span data-stu-id="11e9f-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure tooreplace it with a new drive.</span></span>

#### <a name="tooinsert-a-drive"></a><span data-ttu-id="11e9f-157">tooinsert dysku</span><span class="sxs-lookup"><span data-stu-id="11e9f-157">tooinsert a drive</span></span>
1. <span data-ttu-id="11e9f-158">Upewnij się, że dojście operatora dysku hello pełni zostanie rozszerzony, jak pokazano w powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="11e9f-158">Ensure hello drive carrier handle is fully extended, as shown in hello following image.</span></span>
   
    ![Dysk z dojściem rozszerzone](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="11e9f-160">**Rysunek 5** dysku z dojściem rozszerzone</span><span class="sxs-lookup"><span data-stu-id="11e9f-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="11e9f-161">Slajd hello dysk nośnika końca hello w obudowie hello.</span><span class="sxs-lookup"><span data-stu-id="11e9f-161">Slide hello drive carrier all hello way into hello chassis.</span></span>
   
    ![Przedłużanie dysku na dysk nośnika](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="11e9f-163">**Rysunek 6** ruchomej hello dysku operatora w obudowie hello</span><span class="sxs-lookup"><span data-stu-id="11e9f-163">**Figure 6**  Sliding hello drive carrier into hello chassis</span></span>
3. <span data-ttu-id="11e9f-164">Z hello dysku operatora hello wstawiony, zamknij dysk nośnika dojściem podczas kontynuowanie toopush hello dysk nośnika do hello obudowy, dopóki hello dysku operator uchwytu przyciąganie w stanie zablokowanym.</span><span class="sxs-lookup"><span data-stu-id="11e9f-164">With hello drive carrier inserted, close hello drive carrier handle while continuing toopush hello drive carrier into hello chassis, until hello drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="11e9f-165">Użyj hello blokady klucz dostarczony przez dojście operatora hello toosecure firmy Microsoft (tamperproof Torx śrubokręt) w miejscu przez włączenie gwintowanym blokady hello Włącz kwartału z ruchem wskazówek zegara.</span><span class="sxs-lookup"><span data-stu-id="11e9f-165">Use hello lock key that was provided by Microsoft (tamperproof Torx screwdriver) toosecure hello carrier handle into place by turning hello lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="11e9f-166">Sprawdź, czy zastąpienia hello zakończyło się pomyślnie i działa hello dysku.</span><span class="sxs-lookup"><span data-stu-id="11e9f-166">Verify that hello replacement was successful and hello drive is operational.</span></span> <span data-ttu-id="11e9f-167">Dostęp do portalu Azure hello i przejdź za**ustawienia** > **kondycji sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="11e9f-167">Access hello Azure portal and navigate too**Settings** > **Hardware health**.</span></span> <span data-ttu-id="11e9f-168">W obszarze **udostępnione składniki** lub **EBOD udostępnione składniki**, stan dysku hello powinna być zielona, wskazujący, że jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="11e9f-168">Under **Shared components** or **EBOD shared components**, hello drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="11e9f-169">Może upłynąć kilka godzin tooturn stan dysku hello zielonego po wymianie hello.</span><span class="sxs-lookup"><span data-stu-id="11e9f-169">It may take several hours for hello disk status tooturn green after hello replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="11e9f-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="11e9f-170">Next steps</span></span>
<span data-ttu-id="11e9f-171">Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="11e9f-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

