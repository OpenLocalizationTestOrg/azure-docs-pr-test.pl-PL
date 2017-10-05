---
title: "Zastąp PCM na urządzeniu z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak usunięty i zastąpiony zasilania i chłodzenia modułu (PCM) na urządzeniu StorSimple"
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 7d181e6e434c998573dbea4b541cfacf7a28ee66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="49847-103">Zamień na urządzeniu StorSimple zasilania i chłodzenia modułu</span><span class="sxs-lookup"><span data-stu-id="49847-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="49847-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="49847-104">Overview</span></span>
<span data-ttu-id="49847-105">Zasilania i chłodzenia modułu (PCM) w urządzeniu Microsoft Azure StorSimple składa się z źródła zasilania i chłodzenia wentylatory, które są kontrolowane przez serwer podstawowy i obudowy EBOD.</span><span class="sxs-lookup"><span data-stu-id="49847-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span></span> <span data-ttu-id="49847-106">Istnieje tylko jeden model PCM, który jest certyfikowany do każdej obudowy.</span><span class="sxs-lookup"><span data-stu-id="49847-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="49847-107">Obudowa podstawowy jest certyfikowany do 764 W PCM i obudowy EBOD jest certyfikowany do 580 W PCM.</span><span class="sxs-lookup"><span data-stu-id="49847-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="49847-108">Mimo że PCMs obudowa podstawowego i obudowy EBOD są różne, procedura zastępczy jest taka sama.</span><span class="sxs-lookup"><span data-stu-id="49847-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span></span>

<span data-ttu-id="49847-109">Ten samouczek wyjaśnia, jak:</span><span class="sxs-lookup"><span data-stu-id="49847-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="49847-110">Usuń PCM</span><span class="sxs-lookup"><span data-stu-id="49847-110">Remove a PCM</span></span>
* <span data-ttu-id="49847-111">Zainstaluj serwer zamienny PCM</span><span class="sxs-lookup"><span data-stu-id="49847-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49847-112">Przed usunięcie i zastąpienie PCM, zapoznaj się z informacjami bezpieczeństwa w [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="49847-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="49847-113">Aby zastąpić PCM</span><span class="sxs-lookup"><span data-stu-id="49847-113">Before you replace a PCM</span></span>
<span data-ttu-id="49847-114">Należy pamiętać o następujących istotne problemy przed wymianą programu PCM:</span><span class="sxs-lookup"><span data-stu-id="49847-114">Be aware of the following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="49847-115">W przypadku niepowodzenia zasilania PCM pozostaw zainstalowany moduł uszkodzony, ale usunąć przewód zasilający.</span><span class="sxs-lookup"><span data-stu-id="49847-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span></span> <span data-ttu-id="49847-116">Wentylator będzie otrzymywać zasilania obudowa i podaj odpowiednie chłodzenia w dalszym ciągu.</span><span class="sxs-lookup"><span data-stu-id="49847-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span></span> <span data-ttu-id="49847-117">W przypadku niepowodzenia wentylatora PCM wymaga zastąpienia natychmiast.</span><span class="sxs-lookup"><span data-stu-id="49847-117">If the fan fails, the PCM needs to be replaced immediately.</span></span>
* <span data-ttu-id="49847-118">Przed usunięciem PCM, odłącz zasilanie z PCM wyłączając przełącznika głównego (o ile istnieje) lub usuwając fizycznie przewód zasilający.</span><span class="sxs-lookup"><span data-stu-id="49847-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span></span> <span data-ttu-id="49847-119">Zawiera ostrzeżenie w systemie, czy wyłączania zasilania jest bezpośrednie.</span><span class="sxs-lookup"><span data-stu-id="49847-119">This provides a warning to your system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="49847-120">Upewnij się, że inne PCM funkcjonalności systemu ciągłej operacji przed wymianą PCM uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="49847-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span></span> <span data-ttu-id="49847-121">Błędny PCM muszą zostać zastąpione pełnej funkcjonalności PCM tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="49847-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="49847-122">Zastąpienie modułu PCM zajmuje tylko kilka minut, ale musi zostać ukończone w ciągu 10 minut usunięcia PCM nie powiodło się, aby zapobiec przegrzaniu.</span><span class="sxs-lookup"><span data-stu-id="49847-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span></span>
* <span data-ttu-id="49847-123">Zauważ, że zastępczy 764 modułów W PCM fabrycznej nie zawierać modułu baterii kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="49847-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span></span> <span data-ttu-id="49847-124">Należy usunąć baterii z programu PCM uszkodzony i wstawić go w module zastępczy przed wykonaniem zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="49847-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span></span> <span data-ttu-id="49847-125">Aby uzyskać więcej informacji, zobacz temat jak [usuwanie i wstawianie modułu baterii kopii zapasowej](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="49847-125">For more information, see how to [remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="49847-126">Usuń PCM</span><span class="sxs-lookup"><span data-stu-id="49847-126">Remove a PCM</span></span>
<span data-ttu-id="49847-127">Wykonaj te instrukcje, gdy wszystko będzie gotowe do usunięcia z urządzenia Microsoft Azure StorSimple zasilania i chłodzenia modułu (PCM).</span><span class="sxs-lookup"><span data-stu-id="49847-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="49847-128">Przed usunięciem programu PCM, sprawdź, czy poprawne zastąpienia (764 T dla obudowa podstawowego) lub 580 W przypadku obudowy EBOD.</span><span class="sxs-lookup"><span data-stu-id="49847-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span></span>

#### <a name="to-remove-a-pcm"></a><span data-ttu-id="49847-129">Aby usunąć PCM</span><span class="sxs-lookup"><span data-stu-id="49847-129">To remove a PCM</span></span>
1. <span data-ttu-id="49847-130">W klasycznym portalu Azure, kliknij przycisk **Ustawienia > Monitor > kondycji sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="49847-130">In the Azure classic portal, click **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="49847-131">Sprawdź stan poszczególnych składników PCM w obszarze **udostępnione składniki** do określenia, na które PCM nie powiodła się:</span><span class="sxs-lookup"><span data-stu-id="49847-131">Check the status of the PCM components under **Shared components** to identify which PCM has failed:</span></span>
   
   * <span data-ttu-id="49847-132">Jeśli zasilacz w PCM 0 nie powiodło się. stan **zasilacz w PCM 0** czerwony.</span><span class="sxs-lookup"><span data-stu-id="49847-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="49847-133">Jeśli zasilacz PCM 1 nie powiodło się. stan **zasilacz 1 PCM** czerwony.</span><span class="sxs-lookup"><span data-stu-id="49847-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="49847-134">Jeśli wentylator PCM 1 nie powiodło się. stan albo **chłodzenia 0 dla PCM 0** lub **chłodzenia 1 dla PCM 0** czerwony.</span><span class="sxs-lookup"><span data-stu-id="49847-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="49847-135">Znajdź niepowodzenia PCM z tyłu obudowy podstawowego.</span><span class="sxs-lookup"><span data-stu-id="49847-135">Locate the failed PCM on the back of the primary enclosure.</span></span> <span data-ttu-id="49847-136">Jeśli używasz modelu 8600 określić podstawowy obudowa za wyświetlany na panelu przednim wyświetlacz numer identyfikacyjny jednostki systemu.</span><span class="sxs-lookup"><span data-stu-id="49847-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span></span> <span data-ttu-id="49847-137">Wartość domyślna to identyfikator jednostki wyświetlany na głównej obudowy **00**, a wartość domyślna to identyfikator jednostki wyświetlany na obudowę EBOD **01**.</span><span class="sxs-lookup"><span data-stu-id="49847-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span></span> <span data-ttu-id="49847-138">Poniższy diagram i tabeli opisano na panelu przednim wyświetlacz.</span><span class="sxs-lookup"><span data-stu-id="49847-138">The following diagram and table explain the front panel of the LED display.</span></span>
   
    ![Identyfikator systemu na panelu przednim OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="49847-140">**Rysunek 1** panelu przodu urządzenia</span><span class="sxs-lookup"><span data-stu-id="49847-140">**Figure 1** Front panel of the device</span></span>  
   
   | <span data-ttu-id="49847-141">Etykieta</span><span class="sxs-lookup"><span data-stu-id="49847-141">Label</span></span> | <span data-ttu-id="49847-142">Opis</span><span class="sxs-lookup"><span data-stu-id="49847-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="49847-143">1</span><span class="sxs-lookup"><span data-stu-id="49847-143">1</span></span> |<span data-ttu-id="49847-144">Przycisk wyciszenia</span><span class="sxs-lookup"><span data-stu-id="49847-144">Mute button</span></span> |
   | <span data-ttu-id="49847-145">2</span><span class="sxs-lookup"><span data-stu-id="49847-145">2</span></span> |<span data-ttu-id="49847-146">Zasilania systemu</span><span class="sxs-lookup"><span data-stu-id="49847-146">System power</span></span> |
   | <span data-ttu-id="49847-147">3</span><span class="sxs-lookup"><span data-stu-id="49847-147">3</span></span> |<span data-ttu-id="49847-148">Błąd modułu</span><span class="sxs-lookup"><span data-stu-id="49847-148">Module fault</span></span> |
   | <span data-ttu-id="49847-149">4</span><span class="sxs-lookup"><span data-stu-id="49847-149">4</span></span> |<span data-ttu-id="49847-150">Błąd logiczny</span><span class="sxs-lookup"><span data-stu-id="49847-150">Logical fault</span></span> |
   | <span data-ttu-id="49847-151">5</span><span class="sxs-lookup"><span data-stu-id="49847-151">5</span></span> |<span data-ttu-id="49847-152">Wyświetlanie Identyfikatora jednostki</span><span class="sxs-lookup"><span data-stu-id="49847-152">Unit ID display</span></span> |
3. <span data-ttu-id="49847-153">Monitorowania wskaźnika LED tyłu obudowy głównej mogą służyć do identyfikowania PCM uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="49847-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span></span> <span data-ttu-id="49847-154">Zobacz następujące diagram i tabeli na sposób używania LED zlokalizować PCM uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="49847-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span></span> <span data-ttu-id="49847-155">Na przykład jeśli LED odpowiadający **wentylator się nie powieść** jest włączone, wentylatora nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="49847-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span></span> <span data-ttu-id="49847-156">Podobnie jeśli LED odpowiadający **AC niepowodzenie** jest włączone, zasilania nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="49847-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span></span> 
   
    ![Płyty montażowej wskaźnika monitorowania urządzenia PCM LED](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="49847-158">**Rysunek 2** PCM z powrotem z wskaźnik LED</span><span class="sxs-lookup"><span data-stu-id="49847-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="49847-159">Etykieta</span><span class="sxs-lookup"><span data-stu-id="49847-159">Label</span></span> | <span data-ttu-id="49847-160">Opis</span><span class="sxs-lookup"><span data-stu-id="49847-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="49847-161">1</span><span class="sxs-lookup"><span data-stu-id="49847-161">1</span></span> |<span data-ttu-id="49847-162">Ak awarii zasilania</span><span class="sxs-lookup"><span data-stu-id="49847-162">AC power failure</span></span> |
   | <span data-ttu-id="49847-163">2</span><span class="sxs-lookup"><span data-stu-id="49847-163">2</span></span> |<span data-ttu-id="49847-164">Wentylator awarii</span><span class="sxs-lookup"><span data-stu-id="49847-164">Fan failure</span></span> |
   | <span data-ttu-id="49847-165">3</span><span class="sxs-lookup"><span data-stu-id="49847-165">3</span></span> |<span data-ttu-id="49847-166">Uszkodzenia</span><span class="sxs-lookup"><span data-stu-id="49847-166">Battery fault</span></span> |
   | <span data-ttu-id="49847-167">4</span><span class="sxs-lookup"><span data-stu-id="49847-167">4</span></span> |<span data-ttu-id="49847-168">PCM OK</span><span class="sxs-lookup"><span data-stu-id="49847-168">PCM OK</span></span> |
   | <span data-ttu-id="49847-169">5</span><span class="sxs-lookup"><span data-stu-id="49847-169">5</span></span> |<span data-ttu-id="49847-170">Kontroler domeny awarii zasilania</span><span class="sxs-lookup"><span data-stu-id="49847-170">DC power failure</span></span> |
   | <span data-ttu-id="49847-171">6</span><span class="sxs-lookup"><span data-stu-id="49847-171">6</span></span> |<span data-ttu-id="49847-172">Baterii dobrej kondycji</span><span class="sxs-lookup"><span data-stu-id="49847-172">Battery healthy</span></span> |
4. <span data-ttu-id="49847-173">Zapoznaj się z poniższym diagramie tyłu urządzenia StorSimple można znaleźć modułu PCM.</span><span class="sxs-lookup"><span data-stu-id="49847-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span></span> <span data-ttu-id="49847-174">PCM 0 jest po lewej stronie i PCM 1 jest po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="49847-174">PCM 0 is on the left and PCM 1 is on the right.</span></span> <span data-ttu-id="49847-175">Tabela poniżej wyjaśniono modułów.</span><span class="sxs-lookup"><span data-stu-id="49847-175">The table that follows explains the modules.</span></span>
   
     ![Płyty montażowej urządzenia podstawowego obudowy modułów](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="49847-177">**Rysunek 3** obu urządzenia z wtyczki</span><span class="sxs-lookup"><span data-stu-id="49847-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="49847-178">Etykieta</span><span class="sxs-lookup"><span data-stu-id="49847-178">Label</span></span> | <span data-ttu-id="49847-179">Opis</span><span class="sxs-lookup"><span data-stu-id="49847-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="49847-180">1</span><span class="sxs-lookup"><span data-stu-id="49847-180">1</span></span> |<span data-ttu-id="49847-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="49847-181">PCM 0</span></span> |
   | <span data-ttu-id="49847-182">2</span><span class="sxs-lookup"><span data-stu-id="49847-182">2</span></span> |<span data-ttu-id="49847-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="49847-183">PCM 1</span></span> |
   | <span data-ttu-id="49847-184">3</span><span class="sxs-lookup"><span data-stu-id="49847-184">3</span></span> |<span data-ttu-id="49847-185">Kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="49847-185">Controller 0</span></span> |
   | <span data-ttu-id="49847-186">4</span><span class="sxs-lookup"><span data-stu-id="49847-186">4</span></span> |<span data-ttu-id="49847-187">Kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="49847-187">Controller 1</span></span> |
5. <span data-ttu-id="49847-188">Wyłącz PCM uszkodzony i odłącz przewód zasilający dostaw.</span><span class="sxs-lookup"><span data-stu-id="49847-188">Turn off the faulty PCM and disconnect the power supply cord.</span></span> <span data-ttu-id="49847-189">Można teraz usunąć PCM.</span><span class="sxs-lookup"><span data-stu-id="49847-189">You can now remove the PCM.</span></span>
6. <span data-ttu-id="49847-190">Ujmij zatrzaśnięcia i po stronie dojście PCM między thumb i wskazującym i zmieścić je, aby otworzyć uchwytu.</span><span class="sxs-lookup"><span data-stu-id="49847-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span></span>
   
    ![Otwierania PCM dojścia](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="49847-192">**Rysunek 4** Otwieranie dojścia PCM</span><span class="sxs-lookup"><span data-stu-id="49847-192">**Figure 4** Opening the PCM handle</span></span>
7. <span data-ttu-id="49847-193">Dojście wygodne do trzymania i Usuń PCM.</span><span class="sxs-lookup"><span data-stu-id="49847-193">Grip the handle and remove the PCM.</span></span>
   
    ![Usuwanie urządzenia PCM](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="49847-195">**Rysunek 5** usuwanie PCM</span><span class="sxs-lookup"><span data-stu-id="49847-195">**Figure 5** Removing the PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="49847-196">Zainstaluj serwer zamienny PCM</span><span class="sxs-lookup"><span data-stu-id="49847-196">Install a replacement PCM</span></span>
<span data-ttu-id="49847-197">Wykonaj te instrukcje, aby zainstalować PCM w urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="49847-197">Follow these instructions to install a PCM in your StorSimple device.</span></span> <span data-ttu-id="49847-198">Upewnij się, że włożono moduł baterii kopii zapasowej przed instalacją zastąpienia PCM (dotyczy tylko 764 PCMs W).</span><span class="sxs-lookup"><span data-stu-id="49847-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span></span> <span data-ttu-id="49847-199">Aby uzyskać więcej informacji, zobacz temat jak [usuwanie i wstawianie modułu baterii kopii zapasowej](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="49847-199">For more information, see how to [remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

#### <a name="to-install-a-pcm"></a><span data-ttu-id="49847-200">Aby zainstalować PCM</span><span class="sxs-lookup"><span data-stu-id="49847-200">To install a PCM</span></span>
1. <span data-ttu-id="49847-201">Sprawdź, czy masz poprawne zastępuje PCM ten załącznik.</span><span class="sxs-lookup"><span data-stu-id="49847-201">Verify that you have the correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="49847-202">Podstawowy Obudowa musi 764 W PCM i obudowy EBOD musi 580 W PCM.</span><span class="sxs-lookup"><span data-stu-id="49847-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="49847-203">Nie należy próbować użyć 580 PCM W w obudowie podstawowego lub 764 PCM W w obudowie EBOD.</span><span class="sxs-lookup"><span data-stu-id="49847-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span></span> <span data-ttu-id="49847-204">Na poniższej ilustracji przedstawiono where zidentyfikować te informacje na etykiecie, który jest dołączony do PCM.</span><span class="sxs-lookup"><span data-stu-id="49847-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span></span>
   
    ![Etykieta PCM urządzenia](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="49847-206">**Rysunek 6** PCM etykiety</span><span class="sxs-lookup"><span data-stu-id="49847-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="49847-207">Sprawdź, czy uszkodzenie obudowy, ze szczególnym uwzględnieniem łączników.</span><span class="sxs-lookup"><span data-stu-id="49847-207">Check for damage to the enclosure, paying particular attention to the connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="49847-208">**Nie należy instalować moduł, jeśli zgięte żadnych kodów PIN łącznika.**</span><span class="sxs-lookup"><span data-stu-id="49847-208">**Do not install the module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="49847-209">Z uchwytem PCM w pozycji otwarcia Przesuń modułu do obudowy.</span><span class="sxs-lookup"><span data-stu-id="49847-209">With the PCM handle in the open position, slide the module into the enclosure.</span></span>
   
    ![Instalowanie urządzenia PCM](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="49847-211">**Rysunek 7** instalowanie PCM</span><span class="sxs-lookup"><span data-stu-id="49847-211">**Figure 7** Installing the PCM</span></span>
4. <span data-ttu-id="49847-212">Ręcznie zamknąć dojścia PCM.</span><span class="sxs-lookup"><span data-stu-id="49847-212">Manually close the PCM handle.</span></span> <span data-ttu-id="49847-213">Kliknięcie usłyszeć jako angażujący zatrzaśnięcia dojścia.</span><span class="sxs-lookup"><span data-stu-id="49847-213">You should hear a click as the handle latch engages.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="49847-214">Aby upewnić się, że numery PIN łącznika ma zaangażowane, ostrożnie można holownik uchwyt bez zwolnienia zatrzaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="49847-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span></span> <span data-ttu-id="49847-215">PCM slajdów wychodzących, oznacza, że zatrzaśnięcia został zamknięty przed zaangażowane łączników.</span><span class="sxs-lookup"><span data-stu-id="49847-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span></span>
   
5. <span data-ttu-id="49847-216">Podłącz kable zasilania do źródła zasilania i PCM.</span><span class="sxs-lookup"><span data-stu-id="49847-216">Connect the power cables to the power source and to the PCM.</span></span>
6. <span data-ttu-id="49847-217">Zabezpiecz naprężenia bele zwolnienia.</span><span class="sxs-lookup"><span data-stu-id="49847-217">Secure the strain relief bales.</span></span>
7. <span data-ttu-id="49847-218">Włącz PCM.</span><span class="sxs-lookup"><span data-stu-id="49847-218">Turn on the PCM.</span></span>
8. <span data-ttu-id="49847-219">Sprawdź, czy zastąpienia zakończyła się pomyślnie: w portalu Azure usługi Menedżer StorSimple urządzeń, przejdź do urządzenia, a następnie do **Ustawienia > Monitor > kondycji sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="49847-219">Verify that the replacement was successful: in the Azure portal of your StorSimple Device Manager service, navigate to your device and then to **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="49847-220">W obszarze **udostępnione składniki**, stan PCM powinna być zielona.</span><span class="sxs-lookup"><span data-stu-id="49847-220">Under the **Shared components**, the status of the PCM should be green.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="49847-221">Może upłynąć kilka minut, aż do zastąpienia PCM całkowicie zainicjować.</span><span class="sxs-lookup"><span data-stu-id="49847-221">It may take a few minutes for the replacement PCM to completely initialize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="49847-222">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="49847-222">Next steps</span></span>
<span data-ttu-id="49847-223">Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="49847-223">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

