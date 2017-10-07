---
title: "aaaReplace PCM na urządzeniu z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooremove i Zamień hello zasilania i chłodzenia modułu (PCM) na urządzeniu StorSimple"
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
ms.openlocfilehash: 474fd09787c5361a81efda4de74356027ac60f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="b3164-103">Zamień na urządzeniu StorSimple zasilania i chłodzenia modułu</span><span class="sxs-lookup"><span data-stu-id="b3164-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="b3164-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b3164-104">Overview</span></span>
<span data-ttu-id="b3164-105">Hello zasilania i chłodzenia modułu (PCM) w urządzeniu Microsoft Azure StorSimple składa się z źródła zasilania i chłodzenia wentylatory, które są kontrolowane przez hello podstawowego i obudowy EBOD.</span><span class="sxs-lookup"><span data-stu-id="b3164-105">hello Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through hello primary and EBOD enclosures.</span></span> <span data-ttu-id="b3164-106">Istnieje tylko jeden model PCM, który jest certyfikowany do każdej obudowy.</span><span class="sxs-lookup"><span data-stu-id="b3164-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="b3164-107">Obudowa głównej Hello jest certyfikowany do 764 W PCM i obudowy EBOD hello jest certyfikowany do 580 W PCM.</span><span class="sxs-lookup"><span data-stu-id="b3164-107">hello primary enclosure is certified for a 764 W PCM and hello EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="b3164-108">Mimo że hello PCMs obudowa głównej hello i obudowy EBOD hello są różne, hello zastępczy procedura jest identyczna.</span><span class="sxs-lookup"><span data-stu-id="b3164-108">Although hello PCMs for hello primary enclosure and hello EBOD enclosure are different, hello replacement procedure is identical.</span></span>

<span data-ttu-id="b3164-109">Ten samouczek wyjaśnia, jak:</span><span class="sxs-lookup"><span data-stu-id="b3164-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="b3164-110">Usuń PCM</span><span class="sxs-lookup"><span data-stu-id="b3164-110">Remove a PCM</span></span>
* <span data-ttu-id="b3164-111">Zainstaluj serwer zamienny PCM</span><span class="sxs-lookup"><span data-stu-id="b3164-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3164-112">Przed usunięcie i zastąpienie PCM, przejrzyj hello bezpieczeństwa informacji w [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b3164-112">Before removing and replacing a PCM, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="b3164-113">Aby zastąpić PCM</span><span class="sxs-lookup"><span data-stu-id="b3164-113">Before you replace a PCM</span></span>
<span data-ttu-id="b3164-114">Należy zwrócić uwagę na następujące istotne problemy przed wymianą programu PCM hello:</span><span class="sxs-lookup"><span data-stu-id="b3164-114">Be aware of hello following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="b3164-115">Zasilacz hello z hello PCM nie powiedzie się, pozostaw hello zainstalowany moduł uszkodzony, ale Usuń hello przewód zasilający.</span><span class="sxs-lookup"><span data-stu-id="b3164-115">If hello power supply of hello PCM fails, leave hello faulty module installed, but remove hello power cord.</span></span> <span data-ttu-id="b3164-116">Wentylator Hello będzie kontynuowana tooreceive zasilania z obudowy hello i kontynuować tooprovide właściwego chłodzenia.</span><span class="sxs-lookup"><span data-stu-id="b3164-116">hello fan will continue tooreceive power from hello enclosure and continue tooprovide proper cooling.</span></span> <span data-ttu-id="b3164-117">W przypadku niepowodzenia wentylator hello hello PCM musi toobe natychmiast zastąpione.</span><span class="sxs-lookup"><span data-stu-id="b3164-117">If hello fan fails, hello PCM needs toobe replaced immediately.</span></span>
* <span data-ttu-id="b3164-118">Przed usunięciem hello PCM, rozłączyć zasilania hello hello PCM wyłączając hello przełącznika głównego (o ile istnieje) lub usuwając fizycznie hello przewód zasilający.</span><span class="sxs-lookup"><span data-stu-id="b3164-118">Before removing hello PCM, disconnect hello power from hello PCM by turning off hello main switch (where present) or by physically removing hello power cord.</span></span> <span data-ttu-id="b3164-119">Zapewnia to system tooyour ostrzeżenie, że wyłączania zasilania jest bezpośrednie.</span><span class="sxs-lookup"><span data-stu-id="b3164-119">This provides a warning tooyour system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="b3164-120">Upewnij się, że inne PCM będzie działać dla tego powitalne nadal działania systemu przed zastępowanie hello PCM uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="b3164-120">Make sure that hello other PCM is functional for continued system operation before replacing hello faulty PCM.</span></span> <span data-ttu-id="b3164-121">Błędny PCM muszą zostać zastąpione pełnej funkcjonalności PCM tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="b3164-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="b3164-122">Zastąpienie modułu PCM zajmuje tylko kilka minut toocomplete, ale musi zostać ukończone w ciągu 10 minut usunięcia przegrzaniu tooprevent PCM hello nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="b3164-122">PCM module replacement takes only few minutes toocomplete, but it must be completed within 10 minutes of removing hello failed PCM tooprevent overheating.</span></span>
* <span data-ttu-id="b3164-123">Należy pamiętać, hello zastępczy 764 W PCM modułów wysłane z fabryki hello nie zawierają hello modułu baterii kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="b3164-123">Note that hello replacement 764 W PCM modules shipped from hello factory do not contain hello backup battery module.</span></span> <span data-ttu-id="b3164-124">Zostanie potrzebuje baterii hello tooremove z programu PCM uszkodzony i wstawić go w hello zastąpienie modułu wcześniejsze tooperforming hello zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="b3164-124">You will need tooremove hello battery from your faulty PCM and then insert it into hello replacement module prior tooperforming hello replacement.</span></span> <span data-ttu-id="b3164-125">Aby uzyskać więcej informacji, zobacz temat jak zbyt[usuwanie i wstawianie modułu baterii kopii zapasowej](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b3164-125">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="b3164-126">Usuń PCM</span><span class="sxs-lookup"><span data-stu-id="b3164-126">Remove a PCM</span></span>
<span data-ttu-id="b3164-127">Wykonaj te instrukcje, gdy są gotowe tooremove zasilania i chłodzenia modułu (PCM) z urządzenia Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b3164-127">Follow these instructions when you are ready tooremove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="b3164-128">Przed usunięciem programu PCM, sprawdź, czy poprawne zastąpienia (764 T dla hello obudowa podstawowego) lub 580 W dla hello EBOD obudowy.</span><span class="sxs-lookup"><span data-stu-id="b3164-128">Before you remove your PCM, verify that you have a correct replacement (764 W for hello primary enclosure or 580 W for hello EBOD enclosure).</span></span>

#### <a name="tooremove-a-pcm"></a><span data-ttu-id="b3164-129">tooremove PCM</span><span class="sxs-lookup"><span data-stu-id="b3164-129">tooremove a PCM</span></span>
1. <span data-ttu-id="b3164-130">W hello klasycznego portalu Azure, kliknij przycisk **Ustawienia > Monitor > kondycji sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="b3164-130">In hello Azure classic portal, click **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="b3164-131">Sprawdź stan hello hello PCM składników w obszarze **udostępnione składniki** tooidentify, który PCM nie powiodła się:</span><span class="sxs-lookup"><span data-stu-id="b3164-131">Check hello status of hello PCM components under **Shared components** tooidentify which PCM has failed:</span></span>
   
   * <span data-ttu-id="b3164-132">Jeśli zasilacz w PCM 0 nie powiodła się, stan hello **zasilacz w PCM 0** czerwony.</span><span class="sxs-lookup"><span data-stu-id="b3164-132">If a power supply in PCM 0 has failed, hello status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="b3164-133">Jeśli zasilacz 1 PCM nie powiodła się, stan hello **zasilacz 1 PCM** czerwony.</span><span class="sxs-lookup"><span data-stu-id="b3164-133">If a power supply in PCM 1 has failed, hello status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="b3164-134">Jeśli wentylator hello PCM 1 nie powiodło się, stan hello **chłodzenia 0 dla PCM 0** lub **chłodzenia 1 dla PCM 0** czerwony.</span><span class="sxs-lookup"><span data-stu-id="b3164-134">If hello fan in PCM 1 has failed, hello status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="b3164-135">Zlokalizuj hello PCM nie powiodło się na powitania kopii hello głównej załącznika.</span><span class="sxs-lookup"><span data-stu-id="b3164-135">Locate hello failed PCM on hello back of hello primary enclosure.</span></span> <span data-ttu-id="b3164-136">Jeśli używasz modelu 8600 zidentyfikować obudowa głównej hello analizując hello numeru identyfikacyjnego jednostki systemu wyświetlane na ekranie panelu przedniego LED hello.</span><span class="sxs-lookup"><span data-stu-id="b3164-136">If you are running an 8600 model, identify hello primary enclosure by looking at hello System Unit Identification Number shown on hello front panel LED display.</span></span> <span data-ttu-id="b3164-137">Witaj domyślny jest wyświetlany na hello obudowa podstawowy identyfikator jednostki **00**, a domyślny hello identyfikator jednostki jest wyświetlany na powitania obudowa EBOD **01**.</span><span class="sxs-lookup"><span data-stu-id="b3164-137">hello default Unit ID displayed on hello primary enclosure is **00**, whereas hello default Unit ID displayed on hello EBOD enclosure is **01**.</span></span> <span data-ttu-id="b3164-138">Hello następujący diagram i tabeli opisano hello panelu przedniego hello LED wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="b3164-138">hello following diagram and table explain hello front panel of hello LED display.</span></span>
   
    ![Identyfikator systemu na panelu przednim OPS](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="b3164-140">**Rysunek 1** panelu przodu hello urządzenia</span><span class="sxs-lookup"><span data-stu-id="b3164-140">**Figure 1** Front panel of hello device</span></span>  
   
   | <span data-ttu-id="b3164-141">Etykieta</span><span class="sxs-lookup"><span data-stu-id="b3164-141">Label</span></span> | <span data-ttu-id="b3164-142">Opis</span><span class="sxs-lookup"><span data-stu-id="b3164-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b3164-143">1</span><span class="sxs-lookup"><span data-stu-id="b3164-143">1</span></span> |<span data-ttu-id="b3164-144">Przycisk wyciszenia</span><span class="sxs-lookup"><span data-stu-id="b3164-144">Mute button</span></span> |
   | <span data-ttu-id="b3164-145">2</span><span class="sxs-lookup"><span data-stu-id="b3164-145">2</span></span> |<span data-ttu-id="b3164-146">Zasilania systemu</span><span class="sxs-lookup"><span data-stu-id="b3164-146">System power</span></span> |
   | <span data-ttu-id="b3164-147">3</span><span class="sxs-lookup"><span data-stu-id="b3164-147">3</span></span> |<span data-ttu-id="b3164-148">Błąd modułu</span><span class="sxs-lookup"><span data-stu-id="b3164-148">Module fault</span></span> |
   | <span data-ttu-id="b3164-149">4</span><span class="sxs-lookup"><span data-stu-id="b3164-149">4</span></span> |<span data-ttu-id="b3164-150">Błąd logiczny</span><span class="sxs-lookup"><span data-stu-id="b3164-150">Logical fault</span></span> |
   | <span data-ttu-id="b3164-151">5</span><span class="sxs-lookup"><span data-stu-id="b3164-151">5</span></span> |<span data-ttu-id="b3164-152">Wyświetlanie Identyfikatora jednostki</span><span class="sxs-lookup"><span data-stu-id="b3164-152">Unit ID display</span></span> |
3. <span data-ttu-id="b3164-153">można także Hello monitorowania LED wskaźnika w hello obu obudowa głównej hello tooidentify hello PCM uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="b3164-153">hello monitoring indicator LEDs in hello back of hello primary enclosure can also be used tooidentify hello faulty PCM.</span></span> <span data-ttu-id="b3164-154">Zobacz następujące hello diagram i jak tabela toounderstand toouse hello LED toolocate hello PCM uszkodzony.</span><span class="sxs-lookup"><span data-stu-id="b3164-154">See hello following diagram and table toounderstand how toouse hello LEDs toolocate hello faulty PCM.</span></span> <span data-ttu-id="b3164-155">Na przykład, jeśli hello DOPROWADZIŁY odpowiedniego toohello **wentylator się nie powieść** jest włączone, wentylator hello nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="b3164-155">For example, if hello LED corresponding toohello **Fan Fail** is lit, hello fan has failed.</span></span> <span data-ttu-id="b3164-156">Podobnie, jeśli hello DOPROWADZIŁY odpowiadającego zbyt**AC niepowodzenie** jest włączone, hello zasilania nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="b3164-156">Likewise, if hello LED corresponding too**AC Fail** is lit, hello power supply has failed.</span></span> 
   
    ![Płyty montażowej wskaźnika monitorowania urządzenia PCM LED](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="b3164-158">**Rysunek 2** PCM z powrotem z wskaźnik LED</span><span class="sxs-lookup"><span data-stu-id="b3164-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="b3164-159">Etykieta</span><span class="sxs-lookup"><span data-stu-id="b3164-159">Label</span></span> | <span data-ttu-id="b3164-160">Opis</span><span class="sxs-lookup"><span data-stu-id="b3164-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b3164-161">1</span><span class="sxs-lookup"><span data-stu-id="b3164-161">1</span></span> |<span data-ttu-id="b3164-162">Ak awarii zasilania</span><span class="sxs-lookup"><span data-stu-id="b3164-162">AC power failure</span></span> |
   | <span data-ttu-id="b3164-163">2</span><span class="sxs-lookup"><span data-stu-id="b3164-163">2</span></span> |<span data-ttu-id="b3164-164">Wentylator awarii</span><span class="sxs-lookup"><span data-stu-id="b3164-164">Fan failure</span></span> |
   | <span data-ttu-id="b3164-165">3</span><span class="sxs-lookup"><span data-stu-id="b3164-165">3</span></span> |<span data-ttu-id="b3164-166">Uszkodzenia</span><span class="sxs-lookup"><span data-stu-id="b3164-166">Battery fault</span></span> |
   | <span data-ttu-id="b3164-167">4</span><span class="sxs-lookup"><span data-stu-id="b3164-167">4</span></span> |<span data-ttu-id="b3164-168">PCM OK</span><span class="sxs-lookup"><span data-stu-id="b3164-168">PCM OK</span></span> |
   | <span data-ttu-id="b3164-169">5</span><span class="sxs-lookup"><span data-stu-id="b3164-169">5</span></span> |<span data-ttu-id="b3164-170">Kontroler domeny awarii zasilania</span><span class="sxs-lookup"><span data-stu-id="b3164-170">DC power failure</span></span> |
   | <span data-ttu-id="b3164-171">6</span><span class="sxs-lookup"><span data-stu-id="b3164-171">6</span></span> |<span data-ttu-id="b3164-172">Baterii dobrej kondycji</span><span class="sxs-lookup"><span data-stu-id="b3164-172">Battery healthy</span></span> |
4. <span data-ttu-id="b3164-173">Zobacz toohello po diagram hello obu hello StorSimple urządzenia toolocate hello nie powiodło się PCM modułu.</span><span class="sxs-lookup"><span data-stu-id="b3164-173">Refer toohello following diagram of hello back of hello StorSimple device toolocate hello failed PCM module.</span></span> <span data-ttu-id="b3164-174">PCM 0 jest po lewej stronie powitania i PCM 1 znajduje się na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="b3164-174">PCM 0 is on hello left and PCM 1 is on hello right.</span></span> <span data-ttu-id="b3164-175">Witaj poniższej tabeli opisano hello modułów.</span><span class="sxs-lookup"><span data-stu-id="b3164-175">hello table that follows explains hello modules.</span></span>
   
     ![Płyty montażowej urządzenia podstawowego obudowy modułów](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="b3164-177">**Rysunek 3** obu urządzenia z wtyczki</span><span class="sxs-lookup"><span data-stu-id="b3164-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="b3164-178">Etykieta</span><span class="sxs-lookup"><span data-stu-id="b3164-178">Label</span></span> | <span data-ttu-id="b3164-179">Opis</span><span class="sxs-lookup"><span data-stu-id="b3164-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b3164-180">1</span><span class="sxs-lookup"><span data-stu-id="b3164-180">1</span></span> |<span data-ttu-id="b3164-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="b3164-181">PCM 0</span></span> |
   | <span data-ttu-id="b3164-182">2</span><span class="sxs-lookup"><span data-stu-id="b3164-182">2</span></span> |<span data-ttu-id="b3164-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="b3164-183">PCM 1</span></span> |
   | <span data-ttu-id="b3164-184">3</span><span class="sxs-lookup"><span data-stu-id="b3164-184">3</span></span> |<span data-ttu-id="b3164-185">Kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="b3164-185">Controller 0</span></span> |
   | <span data-ttu-id="b3164-186">4</span><span class="sxs-lookup"><span data-stu-id="b3164-186">4</span></span> |<span data-ttu-id="b3164-187">Kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="b3164-187">Controller 1</span></span> |
5. <span data-ttu-id="b3164-188">Włącz wylogowywać hello PCM uszkodzony i Odłącz hello zasilający dostaw.</span><span class="sxs-lookup"><span data-stu-id="b3164-188">Turn off hello faulty PCM and disconnect hello power supply cord.</span></span> <span data-ttu-id="b3164-189">Można teraz usunąć hello PCM.</span><span class="sxs-lookup"><span data-stu-id="b3164-189">You can now remove hello PCM.</span></span>
6. <span data-ttu-id="b3164-190">Ujmij zatrzaśnięcia hello i stronie powitania hello PCM obsługi między thumb i wskazującym i zmieścić je razem tooopen hello dojścia.</span><span class="sxs-lookup"><span data-stu-id="b3164-190">Grasp hello latch and hello side of hello PCM handle between your thumb and forefinger, and squeeze them together tooopen hello handle.</span></span>
   
    ![Otwierania PCM dojścia](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="b3164-192">**Rysunek 4** hello otwierania PCM obsługi</span><span class="sxs-lookup"><span data-stu-id="b3164-192">**Figure 4** Opening hello PCM handle</span></span>
7. <span data-ttu-id="b3164-193">Witaj uchwytu obsługi i Usuń hello PCM.</span><span class="sxs-lookup"><span data-stu-id="b3164-193">Grip hello handle and remove hello PCM.</span></span>
   
    ![Usuwanie urządzenia PCM](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="b3164-195">**Rysunek 5** hello usunięcie PCM</span><span class="sxs-lookup"><span data-stu-id="b3164-195">**Figure 5** Removing hello PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="b3164-196">Zainstaluj serwer zamienny PCM</span><span class="sxs-lookup"><span data-stu-id="b3164-196">Install a replacement PCM</span></span>
<span data-ttu-id="b3164-197">Wykonaj te instrukcje tooinstall PCM w urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b3164-197">Follow these instructions tooinstall a PCM in your StorSimple device.</span></span> <span data-ttu-id="b3164-198">Upewnij się, że włożono hello kopii zapasowej baterii modułu wcześniejsze tooinstalling hello zastępczy PCM (dotyczy too764 tylko W PCMs).</span><span class="sxs-lookup"><span data-stu-id="b3164-198">Ensure that you have inserted hello backup battery module prior tooinstalling hello replacement PCM (applies too764 W PCMs only).</span></span> <span data-ttu-id="b3164-199">Aby uzyskać więcej informacji, zobacz temat jak zbyt[usuwanie i wstawianie modułu baterii kopii zapasowej](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b3164-199">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

#### <a name="tooinstall-a-pcm"></a><span data-ttu-id="b3164-200">tooinstall PCM</span><span class="sxs-lookup"><span data-stu-id="b3164-200">tooinstall a PCM</span></span>
1. <span data-ttu-id="b3164-201">Sprawdź, czy hello poprawne zastępuje PCM ten załącznik.</span><span class="sxs-lookup"><span data-stu-id="b3164-201">Verify that you have hello correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="b3164-202">Obudowa głównej Hello musi 764 W PCM i hello EBOD Obudowa musi 580 W PCM.</span><span class="sxs-lookup"><span data-stu-id="b3164-202">hello primary enclosure needs a 764 W PCM and hello EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="b3164-203">Nie powinny podejmować toouse hello 580 PCM W w obudowie głównej hello lub hello 764 PCM W w hello EBOD obudowy.</span><span class="sxs-lookup"><span data-stu-id="b3164-203">You should not attempt toouse hello 580 W PCM in hello Primary enclosure, or hello 764 W PCM in hello EBOD enclosure.</span></span> <span data-ttu-id="b3164-204">powitania po obraz pokazuje, gdzie tooidentify te informacje na powitania etykietę czyli umieszczone toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="b3164-204">hello following image shows where tooidentify this information on hello label that is affixed toohello PCM.</span></span>
   
    ![Etykieta PCM urządzenia](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="b3164-206">**Rysunek 6** PCM etykiety</span><span class="sxs-lookup"><span data-stu-id="b3164-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="b3164-207">Sprawdź, czy obudowa toohello szkody, ze szczególnym uwzględnieniem toohello łączników.</span><span class="sxs-lookup"><span data-stu-id="b3164-207">Check for damage toohello enclosure, paying particular attention toohello connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b3164-208">**Nie należy instalować hello modułu, jeśli zgięte żadnych kodów PIN łącznika.**</span><span class="sxs-lookup"><span data-stu-id="b3164-208">**Do not install hello module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="b3164-209">Otwórz pozycji slajdów hello modułu w obudowie hello hello PCM obsługi w hello.</span><span class="sxs-lookup"><span data-stu-id="b3164-209">With hello PCM handle in hello open position, slide hello module into hello enclosure.</span></span>
   
    ![Instalowanie urządzenia PCM](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="b3164-211">**Rysunek 7** hello instalowanie PCM</span><span class="sxs-lookup"><span data-stu-id="b3164-211">**Figure 7** Installing hello PCM</span></span>
4. <span data-ttu-id="b3164-212">Zamknij ręcznie hello PCM dojścia.</span><span class="sxs-lookup"><span data-stu-id="b3164-212">Manually close hello PCM handle.</span></span> <span data-ttu-id="b3164-213">Kliknięcie usłyszeć jako angażujący hello dojścia zatrzaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="b3164-213">You should hear a click as hello handle latch engages.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b3164-214">tooensure, który hello zaangażowane mają numery PIN, należy ostrożnie holownik na uchwycie hello bez zwolnienia zatrzaśnięcia hello łącznika.</span><span class="sxs-lookup"><span data-stu-id="b3164-214">tooensure that hello connector pins have engaged, you can gently tug on hello handle without releasing hello latch.</span></span> <span data-ttu-id="b3164-215">Jeśli hello PCM slajdów wychodzących, oznacza to, że tego zatrzaśnięcia hello został zamknięty przed zaangażowane hello łączników.</span><span class="sxs-lookup"><span data-stu-id="b3164-215">If hello PCM slides out, it implies that hello latch was closed before hello connectors engaged.</span></span>
   
5. <span data-ttu-id="b3164-216">Połącz źródła zasilania toohello przewodów zasilania hello i toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="b3164-216">Connect hello power cables toohello power source and toohello PCM.</span></span>
6. <span data-ttu-id="b3164-217">Zabezpiecz naprężenia hello bele zwolnienia.</span><span class="sxs-lookup"><span data-stu-id="b3164-217">Secure hello strain relief bales.</span></span>
7. <span data-ttu-id="b3164-218">Włącz hello PCM.</span><span class="sxs-lookup"><span data-stu-id="b3164-218">Turn on hello PCM.</span></span>
8. <span data-ttu-id="b3164-219">Sprawdź pomyślnego zastępczy hello: w portalu Azure usługi Menedżer StorSimple urządzenia hello, przejdź tooyour urządzenia, a następnie zbyt**Ustawienia > Monitor > kondycji sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="b3164-219">Verify that hello replacement was successful: in hello Azure portal of your StorSimple Device Manager service, navigate tooyour device and then too**Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="b3164-220">W obszarze hello **udostępnione składniki**, stan hello hello PCM powinna być zielona.</span><span class="sxs-lookup"><span data-stu-id="b3164-220">Under hello **Shared components**, hello status of hello PCM should be green.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b3164-221">Może upłynąć kilka minut, aż hello zastępczy PCM toocompletely initialize.</span><span class="sxs-lookup"><span data-stu-id="b3164-221">It may take a few minutes for hello replacement PCM toocompletely initialize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3164-222">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3164-222">Next steps</span></span>
<span data-ttu-id="b3164-223">Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="b3164-223">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

