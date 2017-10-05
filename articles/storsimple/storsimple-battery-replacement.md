---
title: "Wymiana baterii urządzenia Microsoft Azure StorSimple | Dokumentacja firmy Microsoft"
description: "Opisuje sposób usunięcia, Zastąp i obsługa modułu baterii kopii zapasowych w urządzeniu StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8b89b3f6851ec9ee0570f551b5407419fdba2d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="f47dc-103">Zastąpienie modułu baterii kopii zapasowych w urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="f47dc-103">Replace the backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="f47dc-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f47dc-104">Overview</span></span>
<span data-ttu-id="f47dc-105">Podstawowy obudowy zasilania i chłodzenia modułu (PCM) na urządzeniu Microsoft Azure StorSimple ma dodatkowe baterii pakietu.</span><span class="sxs-lookup"><span data-stu-id="f47dc-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="f47dc-106">Ten pakiet zawiera zasilania, aby urządzenia StorSimple można zapisać danych w przypadku utraty zasilaniem podstawowego systemu.</span><span class="sxs-lookup"><span data-stu-id="f47dc-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="f47dc-107">Ten pakiet baterii jest określany jako *modułu kopii zapasowej baterii*.</span><span class="sxs-lookup"><span data-stu-id="f47dc-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="f47dc-108">Moduł kopii zapasowej baterii istnieje tylko dla podstawowego obudowa w urządzeniu StorSimple (obudowa EBOD nie zawiera modułu baterii kopii zapasowej).</span><span class="sxs-lookup"><span data-stu-id="f47dc-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="f47dc-109">Ten samouczek wyjaśnia, jak:</span><span class="sxs-lookup"><span data-stu-id="f47dc-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="f47dc-110">Usuń moduł kopii zapasowej baterii</span><span class="sxs-lookup"><span data-stu-id="f47dc-110">Remove the backup battery module</span></span> 
* <span data-ttu-id="f47dc-111">Zainstaluj nowy moduł kopii zapasowej baterii</span><span class="sxs-lookup"><span data-stu-id="f47dc-111">Install a new backup battery module</span></span>
* <span data-ttu-id="f47dc-112">Obsługa modułu kopii zapasowej baterii</span><span class="sxs-lookup"><span data-stu-id="f47dc-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f47dc-113">Przed usuwanie i zastępowanie moduł kopii zapasowej baterii, zapoznaj się z informacjami bezpieczeństwa w [wprowadzenie do wymiany składników sprzętu StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="f47dc-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="f47dc-114">Usuń moduł kopii zapasowej baterii</span><span class="sxs-lookup"><span data-stu-id="f47dc-114">Remove the backup battery module</span></span>
<span data-ttu-id="f47dc-115">Moduł baterii kopii zapasowej dla urządzenia StorSimple jest jednostką replaceable pola.</span><span class="sxs-lookup"><span data-stu-id="f47dc-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="f47dc-116">Przed zainstalowaniem w PCM modułu baterii powinny być przechowywane w oryginalnym opakowaniu.</span><span class="sxs-lookup"><span data-stu-id="f47dc-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="f47dc-117">Wykonaj poniższe kroki, aby usunąć baterii kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="f47dc-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="f47dc-118">Aby usunąć moduł kopii zapasowej baterii</span><span class="sxs-lookup"><span data-stu-id="f47dc-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="f47dc-119">W klasycznym portalu Azure, przejdź do **urządzeń** > **konserwacji** > **stan sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="f47dc-119">In the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="f47dc-120">W obszarze **współużytkowanych składników**, zobaczyć stan baterii.</span><span class="sxs-lookup"><span data-stu-id="f47dc-120">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="f47dc-121">Zidentyfikuj PCM, w którym baterii nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="f47dc-121">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="f47dc-122">Rysunek 1 pokazuje z tyłu urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f47dc-122">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Płyty montażowej urządzenia podstawowego obudowy modułów](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="f47dc-124">**Rysunek 1** obu urządzenie podstawowe przedstawiający modułów PCM i kontrolera</span><span class="sxs-lookup"><span data-stu-id="f47dc-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="f47dc-125">Etykieta</span><span class="sxs-lookup"><span data-stu-id="f47dc-125">Label</span></span> | <span data-ttu-id="f47dc-126">Opis</span><span class="sxs-lookup"><span data-stu-id="f47dc-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f47dc-127">1</span><span class="sxs-lookup"><span data-stu-id="f47dc-127">1</span></span> |<span data-ttu-id="f47dc-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="f47dc-128">PCM 0</span></span> |
   | <span data-ttu-id="f47dc-129">2</span><span class="sxs-lookup"><span data-stu-id="f47dc-129">2</span></span> |<span data-ttu-id="f47dc-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="f47dc-130">PCM 1</span></span> |
   | <span data-ttu-id="f47dc-131">3</span><span class="sxs-lookup"><span data-stu-id="f47dc-131">3</span></span> |<span data-ttu-id="f47dc-132">Kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="f47dc-132">Controller 0</span></span> |
   | <span data-ttu-id="f47dc-133">4</span><span class="sxs-lookup"><span data-stu-id="f47dc-133">4</span></span> |<span data-ttu-id="f47dc-134">Kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="f47dc-134">Controller 1</span></span> |
   
    <span data-ttu-id="f47dc-135">Jak to przedstawiono numer 3 na rysunku 2, monitorowania wskaźnika DOPROWADZIŁY na PCM 0, który odpowiada **uszkodzenia** powinny być włączone.</span><span class="sxs-lookup"><span data-stu-id="f47dc-135">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Montażowa LED wskaźnik monitorowania PCM urządzenia](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="f47dc-137">**Rysunek 2** PCM z powrotem przedstawiający monitorowania wskaźnik LED</span><span class="sxs-lookup"><span data-stu-id="f47dc-137">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="f47dc-138">Etykieta</span><span class="sxs-lookup"><span data-stu-id="f47dc-138">Label</span></span> | <span data-ttu-id="f47dc-139">Opis</span><span class="sxs-lookup"><span data-stu-id="f47dc-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f47dc-140">1</span><span class="sxs-lookup"><span data-stu-id="f47dc-140">1</span></span> |<span data-ttu-id="f47dc-141">Ak awarii zasilania</span><span class="sxs-lookup"><span data-stu-id="f47dc-141">AC power failure</span></span> |
   | <span data-ttu-id="f47dc-142">2</span><span class="sxs-lookup"><span data-stu-id="f47dc-142">2</span></span> |<span data-ttu-id="f47dc-143">Wentylator awarii</span><span class="sxs-lookup"><span data-stu-id="f47dc-143">Fan failure</span></span> |
   | <span data-ttu-id="f47dc-144">3</span><span class="sxs-lookup"><span data-stu-id="f47dc-144">3</span></span> |<span data-ttu-id="f47dc-145">Uszkodzenia</span><span class="sxs-lookup"><span data-stu-id="f47dc-145">Battery fault</span></span> |
   | <span data-ttu-id="f47dc-146">4</span><span class="sxs-lookup"><span data-stu-id="f47dc-146">4</span></span> |<span data-ttu-id="f47dc-147">PCM OK</span><span class="sxs-lookup"><span data-stu-id="f47dc-147">PCM OK</span></span> |
   | <span data-ttu-id="f47dc-148">5</span><span class="sxs-lookup"><span data-stu-id="f47dc-148">5</span></span> |<span data-ttu-id="f47dc-149">Kontroler domeny awarii zasilania</span><span class="sxs-lookup"><span data-stu-id="f47dc-149">DC power failure</span></span> |
   | <span data-ttu-id="f47dc-150">6</span><span class="sxs-lookup"><span data-stu-id="f47dc-150">6</span></span> |<span data-ttu-id="f47dc-151">Baterii dobrej kondycji</span><span class="sxs-lookup"><span data-stu-id="f47dc-151">Battery healthy</span></span> |
3. <span data-ttu-id="f47dc-152">Aby usunąć PCM z baterii nie powiodło się, postępuj zgodnie z instrukcjami [Usuń PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="f47dc-152">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="f47dc-153">Z PCM usunięte Podnieś Obróć uchwytu modułu baterii w górę, wskazane na poniższej ilustracji i umieszczenie jej do Usuń baterii.</span><span class="sxs-lookup"><span data-stu-id="f47dc-153">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![Usuwanie z PCM baterii](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="f47dc-155">**Rysunek 3** usuwanie baterii z PCM</span><span class="sxs-lookup"><span data-stu-id="f47dc-155">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="f47dc-156">Umieść moduł jednostkę field-replaceable unit pakowania.</span><span class="sxs-lookup"><span data-stu-id="f47dc-156">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="f47dc-157">Zwraca wadliwe urządzenie do firmy Microsoft dla odpowiednich obsługi i ich obsługi.</span><span class="sxs-lookup"><span data-stu-id="f47dc-157">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="f47dc-158">Zainstaluj nowy moduł kopii zapasowej baterii</span><span class="sxs-lookup"><span data-stu-id="f47dc-158">Install a new backup battery module</span></span>
<span data-ttu-id="f47dc-159">Wykonaj poniższe kroki, aby zainstalować moduł baterii zastąpienia w PCM w głównej Obudowa urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f47dc-159">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="f47dc-160">Aby zainstalować moduł baterii</span><span class="sxs-lookup"><span data-stu-id="f47dc-160">To install the battery module</span></span>
1. <span data-ttu-id="f47dc-161">Umieść odpowiednią orientację w PCM modułu baterii kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="f47dc-161">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="f47dc-162">Przytrzymaj naciśnięty uchwytu modułu baterii, aż do miejsca łącznika.</span><span class="sxs-lookup"><span data-stu-id="f47dc-162">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="f47dc-163">Zastąpienie PCM w obudowie głównej zgodnie z wytycznymi w [Zastąp zasilania i chłodzenia modułu na urządzeniu StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="f47dc-163">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="f47dc-164">Po zakończeniu zastąpienia, przejdź do **urządzeń** > **konserwacji** > **stan sprzętu** w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f47dc-164">After the replacement is complete, go to **Devices** > **Maintenance** > **Hardware Status** in the Azure classic portal.</span></span> <span data-ttu-id="f47dc-165">Sprawdź stan baterii, aby upewnić się, że Instalacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="f47dc-165">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="f47dc-166">Stan zielony oznacza baterii jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="f47dc-166">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="f47dc-167">Obsługa modułu kopii zapasowej baterii</span><span class="sxs-lookup"><span data-stu-id="f47dc-167">Maintain the backup battery module</span></span>
<span data-ttu-id="f47dc-168">W urządzeniu StorSimple modułu baterii kopii zapasowej zawiera zasilania do kontrolera podczas zdarzenia utraty zasilania.</span><span class="sxs-lookup"><span data-stu-id="f47dc-168">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="f47dc-169">Umożliwia urządzeniu StorSimple można zapisać krytyczne dane przed zamykanie w kontrolowany sposób.</span><span class="sxs-lookup"><span data-stu-id="f47dc-169">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="f47dc-170">Z dwóch baterii pełni obciążona w PCMs systemu może obsługiwać dwa kolejne utraty zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="f47dc-170">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="f47dc-171">W klasycznym portalu Azure **stan sprzętu** na **konserwacji** strony wskazuje, czy działa poprawnie baterii zbliża się koniec życia.</span><span class="sxs-lookup"><span data-stu-id="f47dc-171">In the Azure classic portal, the **Hardware Status** on the **Maintenance** page indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="f47dc-172">Wskazuje stan baterii **baterii w PCM 0** lub **baterii w PCM 1** w obszarze **współużytkowanych składników**.</span><span class="sxs-lookup"><span data-stu-id="f47dc-172">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="f47dc-173">Ta strona będzie wyświetlany **OBNIŻONY** dla zbliża się z eksploatacji, i **nie powiodło się** dla osiągnięto koniec z eksploatacji.</span><span class="sxs-lookup"><span data-stu-id="f47dc-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="f47dc-174">Bateria może raportować **** po prostu zajdzie potrzeba jego naliczane opłaty.</span><span class="sxs-lookup"><span data-stu-id="f47dc-174">The battery can report **FAILED** when it simply needs to be charged.</span></span>
> 
> 

<span data-ttu-id="f47dc-175">Jeśli **OBNIŻONY** pojawi się stan, zaleca się następujące sposobu działania:</span><span class="sxs-lookup"><span data-stu-id="f47dc-175">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="f47dc-176">System może wystąpić ostatnie utraty zasilania lub baterie przeprowadzona okresowej konserwacji.</span><span class="sxs-lookup"><span data-stu-id="f47dc-176">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="f47dc-177">Sprawdź system na 12 godzin przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="f47dc-177">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="f47dc-178">Jeśli stan jest nadal **OBNIŻONY** po 12 godzin ciągłe połączenie AC zasilania z kontrolerami i PCMs uruchomiony, następnie baterii ma zostać zamieniony.</span><span class="sxs-lookup"><span data-stu-id="f47dc-178">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="f47dc-179">Sprawdź [skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) zastępczy modułu baterii kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="f47dc-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="f47dc-180">Jeśli stan jest OK po 12 godzinach, bateria działa i wymagane tylko opłat konserwacji.</span><span class="sxs-lookup"><span data-stu-id="f47dc-180">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="f47dc-181">Jeśli nie został skojarzony utraty zasilaniem, PCM jest włączony i podłączony do zasilania Sieciowego baterii ma zostać zamieniony.</span><span class="sxs-lookup"><span data-stu-id="f47dc-181">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="f47dc-182">[Skontaktuj się z Microsoft Support](storsimple-contact-microsoft-support.md) porządkowania modułu kopii zapasowej baterii zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="f47dc-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f47dc-183">Usuwanie nie powiodło się baterii zgodnie z przepisami krajowych i regionalnych.</span><span class="sxs-lookup"><span data-stu-id="f47dc-183">Dispose of the failed battery according to national and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f47dc-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f47dc-184">Next steps</span></span>
<span data-ttu-id="f47dc-185">Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="f47dc-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

