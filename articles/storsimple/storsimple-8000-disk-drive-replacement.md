---
title: "Zamień na dysku w urządzeniu serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak zastąpić na dysku w StorSimple obudowa podstawowego lub obudowa EBOD."
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
ms.openlocfilehash: bb259b626ecd4dcbaa8f1c465f1ece4516aa8881
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-8000-series-device"></a><span data-ttu-id="0168e-103">Zamień na urządzeniu z serii StorSimple 8000 dysku</span><span class="sxs-lookup"><span data-stu-id="0168e-103">Replace a disk drive on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="0168e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0168e-104">Overview</span></span>
<span data-ttu-id="0168e-105">Ten samouczek wyjaśnia, jak zostanie usunięty i zastąpiony nieprawidłowe działanie lub uszkodzonego dysku twardego na urządzeniu Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0168e-105">This tutorial explains how you can remove and replace a malfunctioning or failed hard disk drive on a Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="0168e-106">Aby zastąpić dysk, musisz:</span><span class="sxs-lookup"><span data-stu-id="0168e-106">To replace a disk drive, you need to:</span></span>

* <span data-ttu-id="0168e-107">Odłączyć antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="0168e-107">Disengage the antitamper lock</span></span>
* <span data-ttu-id="0168e-108">Usuń dysk</span><span class="sxs-lookup"><span data-stu-id="0168e-108">Remove the disk drive</span></span>
* <span data-ttu-id="0168e-109">Zainstaluj dysk zastępczy</span><span class="sxs-lookup"><span data-stu-id="0168e-109">Install the replacement disk drive</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0168e-110">Przed usunięcie i zastąpienie stacji dysków, zapoznaj się z informacjami bezpieczeństwa w [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="0168e-110">Before removing and replacing a disk drive, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>
 

## <a name="disengage-the-antitamper-lock"></a><span data-ttu-id="0168e-111">Odłączyć antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="0168e-111">Disengage the antitamper lock</span></span>
<span data-ttu-id="0168e-112">Ta procedura wyjaśnia, jak antitamper blokad na urządzeniu StorSimple może być urządzenie włączone lub wyłączone podczas zastępowania dysków.</span><span class="sxs-lookup"><span data-stu-id="0168e-112">This procedure explains how the antitamper locks on your StorSimple device can be engaged or disengaged when you replace the disk drives.</span></span> <span data-ttu-id="0168e-113">Antitamper blokady są zainstalowane w uchwytach operatora dysku, i są one dostępne za pośrednictwem małych otwarcie w sekcji zatrzaśnięcia uchwytu.</span><span class="sxs-lookup"><span data-stu-id="0168e-113">The antitamper locks are fitted in the drive carrier handles, and they are accessed through a small aperture in the latch section of the handle.</span></span> <span data-ttu-id="0168e-114">Dyski są dostarczane z ustawioną pozycji blokady blokad.</span><span class="sxs-lookup"><span data-stu-id="0168e-114">Drives are supplied with the locks set to the locked position.</span></span>

#### <a name="to-unlock-the-antitamper-lock"></a><span data-ttu-id="0168e-115">Aby odblokować antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="0168e-115">To unlock the antitamper lock</span></span>
1. <span data-ttu-id="0168e-116">Starannie wstawić klucz blokady ("tamperproof" T10 śrubokręt, otrzymany od firmy Microsoft) do otwarcie w dojście i jego gniazda.</span><span class="sxs-lookup"><span data-stu-id="0168e-116">Carefully insert the lock key (a "tamperproof" T10 screwdriver that Microsoft provided) into the aperture in the handle and into its socket.</span></span> 
   
   <span data-ttu-id="0168e-117">Jeśli włączono antitamper blokady, red wskaźnika jest widoczne w otwarcie.</span><span class="sxs-lookup"><span data-stu-id="0168e-117">If the antitamper lock is activated, the red indicator is visible in the aperture.</span></span>
  
    ![Zablokowane dysku](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    <span data-ttu-id="0168e-119">**Rysunek 1** blokady przed wykrycie zaangażowane</span><span class="sxs-lookup"><span data-stu-id="0168e-119">**Figure 1** Anti-tamper lock engaged</span></span>
   
   | <span data-ttu-id="0168e-120">Etykieta</span><span class="sxs-lookup"><span data-stu-id="0168e-120">Label</span></span> | <span data-ttu-id="0168e-121">Opis</span><span class="sxs-lookup"><span data-stu-id="0168e-121">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="0168e-122">1</span><span class="sxs-lookup"><span data-stu-id="0168e-122">1</span></span> |<span data-ttu-id="0168e-123">Otwarcie wskaźnika</span><span class="sxs-lookup"><span data-stu-id="0168e-123">Indicator aperture</span></span> |
   | <span data-ttu-id="0168e-124">2</span><span class="sxs-lookup"><span data-stu-id="0168e-124">2</span></span> |<span data-ttu-id="0168e-125">Antitamper blokady</span><span class="sxs-lookup"><span data-stu-id="0168e-125">Antitamper lock</span></span> |
2. <span data-ttu-id="0168e-126">Obróć klucz, w przeciwnym kierunku, dopóki czerwony wskaźnik nie jest widoczny w otwarcie powyżej klucza.</span><span class="sxs-lookup"><span data-stu-id="0168e-126">Rotate the key in an anticlockwise direction until the red indicator is not visible in the aperture above the key.</span></span>
3. <span data-ttu-id="0168e-127">Usuń klucz.</span><span class="sxs-lookup"><span data-stu-id="0168e-127">Remove the key.</span></span>
   
    ![Odblokowany dysku](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    <span data-ttu-id="0168e-129">**Rysunek 2** odblokowany dysku</span><span class="sxs-lookup"><span data-stu-id="0168e-129">**Figure 2** Unlocked disk drive</span></span>
4. <span data-ttu-id="0168e-130">Teraz można usunąć dysku.</span><span class="sxs-lookup"><span data-stu-id="0168e-130">The disk drive can now be removed.</span></span>

<span data-ttu-id="0168e-131">Postępuj zgodnie z instrukcjami wstecznego nawiązanie blokady.</span><span class="sxs-lookup"><span data-stu-id="0168e-131">Follow the steps in reverse to engage the lock.</span></span>

## <a name="remove-the-disk-drive"></a><span data-ttu-id="0168e-132">Usuń dysk</span><span class="sxs-lookup"><span data-stu-id="0168e-132">Remove the disk drive</span></span>
<span data-ttu-id="0168e-133">Urządzenia StorSimple obsługuje konfiguracji RAID 10 przypominającej magazynu spacji.</span><span class="sxs-lookup"><span data-stu-id="0168e-133">Your StorSimple device supports a RAID 10-like storage spaces configuration.</span></span> <span data-ttu-id="0168e-134">Oznacza to, że aplikacja może działać normalnie z jednego dysku nie powiodło się, dysków półprzewodnikowych (SSD), lub dysku twardego dysku (HDD).</span><span class="sxs-lookup"><span data-stu-id="0168e-134">This implies that it can operate normally with one failed disk, solid-state drive (SSD), or hard disk drive (HDD).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="0168e-135">Jeśli w systemie jest więcej niż jednego dysku nie powiodło się, nie należy usuwać więcej niż jeden dysków SSD i HDD z systemu w dowolnym momencie w czasie.</span><span class="sxs-lookup"><span data-stu-id="0168e-135">If your system has more than one failed disk, do not remove more than one SSD or HDD from the system at any point in time.</span></span> <span data-ttu-id="0168e-136">W ten sposób może spowodować utratę danych.</span><span class="sxs-lookup"><span data-stu-id="0168e-136">Doing so could result in loss of data.</span></span>
> * <span data-ttu-id="0168e-137">Upewnij się, umieść zastępczy dysków SSD w miejscu, które wcześniej zawierało dysków SSD.</span><span class="sxs-lookup"><span data-stu-id="0168e-137">Make sure that you place a replacement SSD in a slot that previously contained an SSD.</span></span> <span data-ttu-id="0168e-138">Podobnie umieść zastępczy dysk twardy w miejscu, które wcześniej zawierało dysk twardy.</span><span class="sxs-lookup"><span data-stu-id="0168e-138">Similarly, place a replacement HDD in a slot that previously contained an HDD.</span></span>
> * <span data-ttu-id="0168e-139">W portalu Azure gniazda są ponumerowane od 0 – 11.</span><span class="sxs-lookup"><span data-stu-id="0168e-139">In the Azure portal, slots are numbered from 0 – 11.</span></span> <span data-ttu-id="0168e-140">W związku z tym jeśli portalu wskazuje, że dysk w gnieździe 2 nie powiodło się na urządzeniu, poszukaj uszkodzony dysk w gnieździe trzeci od góry po lewej.</span><span class="sxs-lookup"><span data-stu-id="0168e-140">Therefore, if the portal shows that a disk in slot 2 has failed, on the device, look for the failed disk in the third slot from the top left.</span></span>
> 
> 

<span data-ttu-id="0168e-141">Dyski można usunięty i zastąpiony podczas działania systemu.</span><span class="sxs-lookup"><span data-stu-id="0168e-141">Drives can be removed and replaced while the system is operating.</span></span>

#### <a name="to-remove-a-drive"></a><span data-ttu-id="0168e-142">Aby usunąć dysk</span><span class="sxs-lookup"><span data-stu-id="0168e-142">To remove a drive</span></span>
1. <span data-ttu-id="0168e-143">Aby zidentyfikować uszkodzonym dysku, w portalu Azure, przejdź do Twojego urządzenia **Ustawienia > kondycji sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="0168e-143">To identify the failed disk, in the Azure portal, go to your device **Settings > Hardware health**.</span></span> <span data-ttu-id="0168e-144">Ponieważ dysk może zakończyć się niepowodzeniem w obudowie podstawowej i/lub w obudowie EBOD (Jeśli używasz modelu 8600), sprawdź stan dysków w obszarze **udostępnione składniki** i w obszarze **EBOD udostępnione składniki**.</span><span class="sxs-lookup"><span data-stu-id="0168e-144">Because a disk can fail in the primary enclosure and/or in an EBOD enclosure (if you are using a 8600 model), look at the status of the disks under **Shared components** and under **EBOD shared components**.</span></span> <span data-ttu-id="0168e-145">Uszkodzony dysk w każdej obudowie będą wyświetlane z czerwonym oznaczeniem stanu.</span><span class="sxs-lookup"><span data-stu-id="0168e-145">A failed disk in either enclosure will be shown with a red status.</span></span>
2. <span data-ttu-id="0168e-146">Odszukaj dyski przodu obudowy podstawowego lub obudowa EBOD.</span><span class="sxs-lookup"><span data-stu-id="0168e-146">Locate the drives in the front of the primary enclosure or the EBOD enclosure.</span></span> 
3. <span data-ttu-id="0168e-147">Jeśli dysk jest odblokowany, przejdź do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="0168e-147">If the disk is unlocked, proceed to the next step.</span></span> <span data-ttu-id="0168e-148">Jeśli dysk jest zablokowany, odblokuj go, wykonując poniższe kroki w [odłączyć antitamper blokady](#disengage-the-antitamper-lock).</span><span class="sxs-lookup"><span data-stu-id="0168e-148">If the disk is locked, unlock it by following the procedure in [Disengage the antitamper lock](#disengage-the-antitamper-lock).</span></span>
4. <span data-ttu-id="0168e-149">Naciśnij czarny zatrzaśnięcia na dysku modułu operatora i wylogowanie i optymalizacji ściągnięcia dojście operatora dysku z przodu obudowy.</span><span class="sxs-lookup"><span data-stu-id="0168e-149">Press the black latch on the drive carrier module and pull the drive carrier handle out and away from the front of the chassis.</span></span>
   
    ![Zwolnienie uchwytu dysku](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    <span data-ttu-id="0168e-151">**Rysunek 3** zwolnienie uchwytu dysku</span><span class="sxs-lookup"><span data-stu-id="0168e-151">**Figure 3** Releasing the drive handle</span></span>
5. <span data-ttu-id="0168e-152">Gdy uchwyt operatora dysku pełni zostanie rozszerzony, przesuń operatora dysku poza obudowy.</span><span class="sxs-lookup"><span data-stu-id="0168e-152">When the drive carrier handle is fully extended, slide the drive carrier out of the chassis.</span></span> 
   
    ![Przedłużanie dysku z dysku](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    <span data-ttu-id="0168e-154">**Rysunek 4** przedłużanie dysku poza operatora</span><span class="sxs-lookup"><span data-stu-id="0168e-154">**Figure 4** Sliding the disk drive out of the carrier</span></span>

## <a name="install-the-replacement-disk-drive"></a><span data-ttu-id="0168e-155">Zainstaluj dysk zastępczy</span><span class="sxs-lookup"><span data-stu-id="0168e-155">Install the replacement disk drive</span></span>
<span data-ttu-id="0168e-156">Po dysku nie powiodło się w urządzeniu StorSimple i usunięto go, wykonaj poniższą procedurę, aby zamienić go na nowy dysk.</span><span class="sxs-lookup"><span data-stu-id="0168e-156">After a drive has failed in your StorSimple device and you have removed it, follow this procedure to replace it with a new drive.</span></span>

#### <a name="to-insert-a-drive"></a><span data-ttu-id="0168e-157">Aby wstawić dysku</span><span class="sxs-lookup"><span data-stu-id="0168e-157">To insert a drive</span></span>
1. <span data-ttu-id="0168e-158">Upewnij się, że dojście operatora dysku pełni zostanie rozszerzony, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="0168e-158">Ensure the drive carrier handle is fully extended, as shown in the following image.</span></span>
   
    ![Dysk z dojściem rozszerzone](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    <span data-ttu-id="0168e-160">**Rysunek 5** dysku z dojściem rozszerzone</span><span class="sxs-lookup"><span data-stu-id="0168e-160">**Figure 5** Drive with handle extended</span></span>
2. <span data-ttu-id="0168e-161">Przesuń operatora dysku, aż do obudowy.</span><span class="sxs-lookup"><span data-stu-id="0168e-161">Slide the drive carrier all the way into the chassis.</span></span>
   
    ![Przedłużanie dysku na dysk nośnika](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    <span data-ttu-id="0168e-163">**Rysunek 6** przedłużanie operatora dysku do obudowy</span><span class="sxs-lookup"><span data-stu-id="0168e-163">**Figure 6**  Sliding the drive carrier into the chassis</span></span>
3. <span data-ttu-id="0168e-164">Z nośnikiem dysku wstawiony zamknąć dojścia operatora dysku, pozostawiając wypchnąć operatora dysku do obudowy, dopóki dojście operatora dysku przyciąganie w stanie zablokowanym.</span><span class="sxs-lookup"><span data-stu-id="0168e-164">With the drive carrier inserted, close the drive carrier handle while continuing to push the drive carrier into the chassis, until the drive carrier handle snaps into a locked position.</span></span>
4. <span data-ttu-id="0168e-165">Za pomocą klawisza blokady, dostarczony przez firmę Microsoft (tamperproof Torx śrubokręt) do zabezpieczania dojście operatora w miejscu przez włączenie śrubę blokady Włącz kwartału z ruchem wskazówek zegara.</span><span class="sxs-lookup"><span data-stu-id="0168e-165">Use the lock key that was provided by Microsoft (tamperproof Torx screwdriver) to secure the carrier handle into place by turning the lock screw a quarter turn clockwise.</span></span>
5. <span data-ttu-id="0168e-166">Sprawdź, czy zastąpienia zakończyło się pomyślnie i działa dysku.</span><span class="sxs-lookup"><span data-stu-id="0168e-166">Verify that the replacement was successful and the drive is operational.</span></span> <span data-ttu-id="0168e-167">Dostęp do portalu Azure i przejdź do **ustawienia** > **kondycji sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="0168e-167">Access the Azure portal and navigate to **Settings** > **Hardware health**.</span></span> <span data-ttu-id="0168e-168">W obszarze **udostępnione składniki** lub **EBOD udostępnione składniki**, stan dysku powinna być zielona, wskazując, że jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="0168e-168">Under **Shared components** or **EBOD shared components**, the drive status should be green, indicating that it is healthy.</span></span>
<!---Loc Comment: It seems it should say "Device settings > Hardware health" instead of "Settings > Hardware health"---->
   
   > [!NOTE]
   > <span data-ttu-id="0168e-169">Może upłynąć kilka godzin stanu dysku włączyć zielonego po wymianie.</span><span class="sxs-lookup"><span data-stu-id="0168e-169">It may take several hours for the disk status to turn green after the replacement.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="0168e-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0168e-170">Next steps</span></span>
<span data-ttu-id="0168e-171">Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="0168e-171">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

