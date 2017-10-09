---
title: "aaaReplace baterii na urządzeniu serii Microsoft Azure StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooremove, Zastąp i obsługa modułu kopii zapasowej baterii hello na urządzeniu StorSimple."
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
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="82033-103">Zastąp hello modułu baterii kopii zapasowych w urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="82033-103">Replace hello backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="82033-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="82033-104">Overview</span></span>
<span data-ttu-id="82033-105">obudowy głównej Hello zasilania i chłodzenia modułu (PCM) na urządzeniu Microsoft Azure StorSimple ma dodatkowe baterii pakietu.</span><span class="sxs-lookup"><span data-stu-id="82033-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="82033-106">Ten pakiet zawiera zasilania, dzięki czemu hello urządzenia StorSimple można zapisać danych w przypadku utraty AC zasilania toohello głównej obudowy.</span><span class="sxs-lookup"><span data-stu-id="82033-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="82033-107">Ten pakiet baterii jest hello określonego tooas *modułu kopii zapasowej baterii*.</span><span class="sxs-lookup"><span data-stu-id="82033-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="82033-108">Moduł kopii zapasowej baterii Hello istnieje tylko dla podstawowego obudowa hello w urządzeniu StorSimple (hello obudowa EBOD nie zawiera modułu baterii kopii zapasowej).</span><span class="sxs-lookup"><span data-stu-id="82033-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="82033-109">Ten samouczek wyjaśnia, jak:</span><span class="sxs-lookup"><span data-stu-id="82033-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="82033-110">Usuń moduł kopii zapasowej baterii hello</span><span class="sxs-lookup"><span data-stu-id="82033-110">Remove hello backup battery module</span></span>
* <span data-ttu-id="82033-111">Zainstaluj nowy moduł kopii zapasowej baterii</span><span class="sxs-lookup"><span data-stu-id="82033-111">Install a new backup battery module</span></span>
* <span data-ttu-id="82033-112">Obsługa modułu kopii zapasowej baterii hello</span><span class="sxs-lookup"><span data-stu-id="82033-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82033-113">Przed usuwanie i zastępowanie moduł kopii zapasowej baterii, przejrzyj informacje bezpieczeństwa hello w hello [wymiana składników sprzętowych tooStorSimple wprowadzenie](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="82033-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="82033-114">Usuń moduł kopii zapasowej baterii hello</span><span class="sxs-lookup"><span data-stu-id="82033-114">Remove hello backup battery module</span></span>
<span data-ttu-id="82033-115">Hello modułu baterii kopii zapasowej dla urządzenia StorSimple jest jednostką replaceable pola.</span><span class="sxs-lookup"><span data-stu-id="82033-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="82033-116">Przed zainstalowaniem w hello PCM modułu baterii hello powinny być przechowywane w oryginalnym opakowaniu.</span><span class="sxs-lookup"><span data-stu-id="82033-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="82033-117">Wykonaj następujące kroki tooremove hello kopii zapasowej baterii hello.</span><span class="sxs-lookup"><span data-stu-id="82033-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="82033-118">Moduł kopii zapasowej baterii hello tooremove</span><span class="sxs-lookup"><span data-stu-id="82033-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="82033-119">W hello portalu Azure Przejdź bloku usługi Menedżer StorSimple urządzenia tooyour.</span><span class="sxs-lookup"><span data-stu-id="82033-119">In hello Azure portal, go tooyour StorSimple Device Manager service blade.</span></span> <span data-ttu-id="82033-120">Przejdź za**urządzeń** , a następnie wybierz urządzenie z listy urządzeń hello.</span><span class="sxs-lookup"><span data-stu-id="82033-120">Go too**Devices** and then select your device from hello list of devices.</span></span> <span data-ttu-id="82033-121">Przejdź za**Monitor** > **kondycji sprzętu**.</span><span class="sxs-lookup"><span data-stu-id="82033-121">Navigate too**Monitor** > **Hardware health**.</span></span> <span data-ttu-id="82033-122">W obszarze **współużytkowanych składników**, przyjrzeć się stan hello hello baterii.</span><span class="sxs-lookup"><span data-stu-id="82033-122">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="82033-123">Zidentyfikuj PCM hello, w których hello baterii nie powiodła się.</span><span class="sxs-lookup"><span data-stu-id="82033-123">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="82033-124">Rysunek 1 pokazuje hello obu hello urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="82033-124">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Płyty montażowej urządzenia podstawowego obudowy modułów](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="82033-126">**Rysunek 1** obu urządzenie podstawowe przedstawiający modułów PCM i kontrolera</span><span class="sxs-lookup"><span data-stu-id="82033-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="82033-127">Etykieta</span><span class="sxs-lookup"><span data-stu-id="82033-127">Label</span></span> | <span data-ttu-id="82033-128">Opis</span><span class="sxs-lookup"><span data-stu-id="82033-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="82033-129">1</span><span class="sxs-lookup"><span data-stu-id="82033-129">1</span></span> |<span data-ttu-id="82033-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="82033-130">PCM 0</span></span> |
   | <span data-ttu-id="82033-131">2</span><span class="sxs-lookup"><span data-stu-id="82033-131">2</span></span> |<span data-ttu-id="82033-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="82033-132">PCM 1</span></span> |
   | <span data-ttu-id="82033-133">3</span><span class="sxs-lookup"><span data-stu-id="82033-133">3</span></span> |<span data-ttu-id="82033-134">Kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="82033-134">Controller 0</span></span> |
   | <span data-ttu-id="82033-135">4</span><span class="sxs-lookup"><span data-stu-id="82033-135">4</span></span> |<span data-ttu-id="82033-136">Kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="82033-136">Controller 1</span></span> |
   
    <span data-ttu-id="82033-137">Jak pokazano numerem 3 hello na rysunku 2, hello monitorowania wskaźnik DOPROWADZIŁY na PCM 0, który odpowiada za**uszkodzenia** powinny być włączone.</span><span class="sxs-lookup"><span data-stu-id="82033-137">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Montażowa LED wskaźnik monitorowania PCM urządzenia](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="82033-139">**Rysunek 2** hello przedstawiający PCM z powrotem monitorowania wskaźników</span><span class="sxs-lookup"><span data-stu-id="82033-139">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="82033-140">Etykieta</span><span class="sxs-lookup"><span data-stu-id="82033-140">Label</span></span> | <span data-ttu-id="82033-141">Opis</span><span class="sxs-lookup"><span data-stu-id="82033-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="82033-142">1</span><span class="sxs-lookup"><span data-stu-id="82033-142">1</span></span> |<span data-ttu-id="82033-143">Ak awarii zasilania</span><span class="sxs-lookup"><span data-stu-id="82033-143">AC power failure</span></span> |
   | <span data-ttu-id="82033-144">2</span><span class="sxs-lookup"><span data-stu-id="82033-144">2</span></span> |<span data-ttu-id="82033-145">Wentylator awarii</span><span class="sxs-lookup"><span data-stu-id="82033-145">Fan failure</span></span> |
   | <span data-ttu-id="82033-146">3</span><span class="sxs-lookup"><span data-stu-id="82033-146">3</span></span> |<span data-ttu-id="82033-147">Uszkodzenia</span><span class="sxs-lookup"><span data-stu-id="82033-147">Battery fault</span></span> |
   | <span data-ttu-id="82033-148">4</span><span class="sxs-lookup"><span data-stu-id="82033-148">4</span></span> |<span data-ttu-id="82033-149">PCM OK</span><span class="sxs-lookup"><span data-stu-id="82033-149">PCM OK</span></span> |
   | <span data-ttu-id="82033-150">5</span><span class="sxs-lookup"><span data-stu-id="82033-150">5</span></span> |<span data-ttu-id="82033-151">Kontroler domeny awarii zasilania</span><span class="sxs-lookup"><span data-stu-id="82033-151">DC power failure</span></span> |
   | <span data-ttu-id="82033-152">6</span><span class="sxs-lookup"><span data-stu-id="82033-152">6</span></span> |<span data-ttu-id="82033-153">Baterii dobrej kondycji</span><span class="sxs-lookup"><span data-stu-id="82033-153">Battery healthy</span></span> |
3. <span data-ttu-id="82033-154">Witaj tooremove PCM z baterii nie powiodło się, wykonaj kroki hello w [Usuń PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="82033-154">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="82033-155">Hello PCM usunięte, przyrostu i baterii hello Obróć moduł obsługi górę wskazane powitania po rysunek, a obudowach go tooremove hello baterii.</span><span class="sxs-lookup"><span data-stu-id="82033-155">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Usuwanie z PCM baterii](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="82033-157">**Rysunek 3** usuwanie baterii hello z hello PCM</span><span class="sxs-lookup"><span data-stu-id="82033-157">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="82033-158">Moduł hello miejsce w jednostce replaceable pola hello pakowania.</span><span class="sxs-lookup"><span data-stu-id="82033-158">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="82033-159">Zwróć hello tooMicrosoft urządzenie do właściwego obsługi i obsługi.</span><span class="sxs-lookup"><span data-stu-id="82033-159">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="82033-160">Zainstaluj nowy moduł kopii zapasowej baterii</span><span class="sxs-lookup"><span data-stu-id="82033-160">Install a new backup battery module</span></span>
<span data-ttu-id="82033-161">Wykonaj następujące kroki tooinstall hello zastępczy baterii modułu w hello PCM w obudowie głównej hello urządzenia StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="82033-161">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="82033-162">Moduł baterii hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="82033-162">tooinstall hello battery module</span></span>
1. <span data-ttu-id="82033-163">Umieść moduł kopii zapasowej baterii hello hello odpowiednią orientację w hello PCM.</span><span class="sxs-lookup"><span data-stu-id="82033-163">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="82033-164">Naciśnij klawisz hello baterii modułu obsługi wszystkich hello sposób tooseat hello łącznika.</span><span class="sxs-lookup"><span data-stu-id="82033-164">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="82033-165">Zastąp hello PCM w obudowie głównej hello przez następujące wytyczne hello w [Zastąp zasilania i chłodzenia modułu na urządzeniu StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="82033-165">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="82033-166">Po zakończeniu hello zastąpienie go tooyour urządzenia, a następnie przejdź zbyt**Monitor** > **kondycji sprzętu** w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="82033-166">After hello replacement is complete, go tooyour device and then go too**Monitor** > **Hardware health** in hello Azure portal.</span></span> <span data-ttu-id="82033-167">Sprawdź stan hello hello baterii toomake się upewnić, że hello instalacja zakończyła się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="82033-167">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="82033-168">Stan zielony oznacza baterii hello jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="82033-168">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="82033-169">Obsługa modułu kopii zapasowej baterii hello</span><span class="sxs-lookup"><span data-stu-id="82033-169">Maintain hello backup battery module</span></span>
<span data-ttu-id="82033-170">W urządzeniu StorSimple hello kopii zapasowej baterii modułu zawiera kontroler toohello energią podczas zdarzenia utraty zasilania.</span><span class="sxs-lookup"><span data-stu-id="82033-170">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="82033-171">Umożliwia hello StorSimple urządzenia toosave krytyczne dane przed tooshutting w dół w kontrolowany sposób.</span><span class="sxs-lookup"><span data-stu-id="82033-171">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="82033-172">Z dwóch baterii pełni obciążona w hello PCMs hello systemu może obsługiwać dwa kolejne utraty zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="82033-172">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="82033-173">W portalu Azure hello, hello **kondycji sprzętu** w obszarze hello **Monitor** bloku wskazuje, czy działa poprawnie baterii hello zbliża się hello z wycofanych.</span><span class="sxs-lookup"><span data-stu-id="82033-173">In hello Azure portal, hello **Hardware health** under hello **Monitor** blade indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="82033-174">Wskazuje stan baterii Hello **baterii w PCM 0** lub **baterii w PCM 1** w obszarze **współużytkowanych składników**.</span><span class="sxs-lookup"><span data-stu-id="82033-174">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="82033-175">Wyświetli ten blok **OBNIŻONY** dla zbliża się z eksploatacji, i **** dla osiągnięto koniec z eksploatacji.</span><span class="sxs-lookup"><span data-stu-id="82033-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="82033-176">zgłosić baterii Hello **** gdy po prostu potrzebuje toobe obciążona.</span><span class="sxs-lookup"><span data-stu-id="82033-176">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>


<span data-ttu-id="82033-177">Jeśli hello **OBNIŻONY** pojawi się stan, firma Microsoft zaleca powitania od sposobu działania:</span><span class="sxs-lookup"><span data-stu-id="82033-177">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="82033-178">Hello system mogła wystąpić ostatnie utraty zasilania lub baterie hello przeprowadzona okresowej konserwacji.</span><span class="sxs-lookup"><span data-stu-id="82033-178">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="82033-179">Sprawdź hello system na 12 godzin przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="82033-179">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="82033-180">Jeśli stan hello jest nadal **OBNIŻONY** po 12 godzin zasilania tooAC stałego połączenia z hello kontrolerów i PCMs uruchomiony, następnie hello poziomie naładowania baterii musi toobe zastąpione.</span><span class="sxs-lookup"><span data-stu-id="82033-180">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="82033-181">Sprawdź [skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md) zastępczy modułu baterii kopii zapasowej.</span><span class="sxs-lookup"><span data-stu-id="82033-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="82033-182">Jeśli stan hello staje się OK po 12 godzinach, baterii hello działa i wymagane tylko opłat konserwacji.</span><span class="sxs-lookup"><span data-stu-id="82033-182">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="82033-183">Jeśli nie nastąpiła skojarzone utraty zasilania Sieciowego i hello PCM jest włączony i podłączony tooAC zasilania, hello poziomie naładowania baterii musi toobe zastąpione.</span><span class="sxs-lookup"><span data-stu-id="82033-183">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="82033-184">[Skontaktuj się z Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder modułu kopii zapasowej baterii zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="82033-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="82033-185">Usuń hello nie baterii zgodnie z toonational i przepisy regionalne.</span><span class="sxs-lookup"><span data-stu-id="82033-185">Dispose of hello failed battery according toonational and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82033-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="82033-186">Next steps</span></span>
<span data-ttu-id="82033-187">Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="82033-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

