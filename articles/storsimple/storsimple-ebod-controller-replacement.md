---
title: aaaReplace kontrolera StorSimple EBOD | Dokumentacja firmy Microsoft
description: "Wyjaśniono, jak tooremove i Zastąp jeden lub oba kontrolerów EBOD na urządzeniu StorSimple 8600."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="f6472-103">Zastąp kontrolera EBOD na urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="f6472-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="f6472-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f6472-104">Overview</span></span>
<span data-ttu-id="f6472-105">Ten samouczek wyjaśnia sposób tooreplace uszkodzony moduł kontrolera EBOD na urządzeniu Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f6472-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="f6472-106">tooreplace moduł EBOD kontrolera, należy:</span><span class="sxs-lookup"><span data-stu-id="f6472-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="f6472-107">Usuń hello błędny EBOD kontrolera</span><span class="sxs-lookup"><span data-stu-id="f6472-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="f6472-108">Instalowanie nowego kontrolera EBOD</span><span class="sxs-lookup"><span data-stu-id="f6472-108">Install a new EBOD controller</span></span>

<span data-ttu-id="f6472-109">Należy wziąć pod uwagę następujące informacje, przed rozpoczęciem powitalne:</span><span class="sxs-lookup"><span data-stu-id="f6472-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="f6472-110">Puste EBOD moduły muszą być wstawiane do wszystkich miejsc nieużywane.</span><span class="sxs-lookup"><span data-stu-id="f6472-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="f6472-111">Obudowa Hello nie zostanie poprawnie cool, jeśli gnieździe pozostanie otwarte.</span><span class="sxs-lookup"><span data-stu-id="f6472-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="f6472-112">Kontroler EBOD Hello jest wyłączania i można go usunąć ani zastąpić.</span><span class="sxs-lookup"><span data-stu-id="f6472-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="f6472-113">Nie usuwaj modułu nie powiodło się, dopóki nie uzyskasz zastępczy.</span><span class="sxs-lookup"><span data-stu-id="f6472-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="f6472-114">Po zainicjowaniu procesu wymiany hello musi zakończyć w ciągu 10 minut.</span><span class="sxs-lookup"><span data-stu-id="f6472-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6472-115">Przed podjęciem próby wykonania tooremove lub zamienić dowolny składnik StorSimple, upewnij się, że przeglądu hello [bezpieczeństwa ikona konwencje](storsimple-safety.md#safety-icon-conventions) i innych [środki ostrożności](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="f6472-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="f6472-116">Usuwanie kontrolera EBOD</span><span class="sxs-lookup"><span data-stu-id="f6472-116">Remove an EBOD controller</span></span>
<span data-ttu-id="f6472-117">Przed zastąpienie hello nie powiodło się moduł kontrolera EBOD w urządzeniu StorSimple, upewnij się, że hello inny moduł kontrolera EBOD jest aktywne i uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="f6472-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="f6472-118">Witaj następujące procedura i tabela wyjaśniono, jak tooremove Witaj EBOD moduł kontrolera.</span><span class="sxs-lookup"><span data-stu-id="f6472-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="f6472-119">Moduł EBOD tooremove</span><span class="sxs-lookup"><span data-stu-id="f6472-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="f6472-120">Otwórz hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f6472-120">Open hello Azure classic portal.</span></span>
2. <span data-ttu-id="f6472-121">Przejdź za**urządzeń** > **konserwacji** > **stan sprzętu**i upewnij się, że stan hello hello DOPROWADZIŁA do hello active EBOD Moduł kontrolera jest zielony i hello LED modułu kontrolera EBOD hello nie powiodło się jest czerwony.</span><span class="sxs-lookup"><span data-stu-id="f6472-121">Navigate too**Devices** > **Maintenance** > **Hardware Status**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="f6472-122">Znajdź moduł kontrolera EBOD hello nie powiodło się na powitania obu hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f6472-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="f6472-123">Usuń kable hello, łączące hello EBOD kontrolera modułu toohello kontrolera przed zmianą hello EBOD modułu poza hello systemu.</span><span class="sxs-lookup"><span data-stu-id="f6472-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="f6472-124">Zanotuj hello dokładne portu SAS hello EBOD kontrolera moduł, który został połączony toohello kontrolera.</span><span class="sxs-lookup"><span data-stu-id="f6472-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="f6472-125">Konfiguracja toothis systemu hello toorestore wymagane będzie po Zastąp hello EBOD modułu.</span><span class="sxs-lookup"><span data-stu-id="f6472-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="f6472-126">Zazwyczaj jest to Port A, który jest oznaczony jako **hosta w** w powitania po diagramu.</span><span class="sxs-lookup"><span data-stu-id="f6472-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   > 
   > 
   
    ![Kontroler IDE EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="f6472-128">**Rysunek 1** EBOD z powrotem modułu</span><span class="sxs-lookup"><span data-stu-id="f6472-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="f6472-129">Etykieta</span><span class="sxs-lookup"><span data-stu-id="f6472-129">Label</span></span> | <span data-ttu-id="f6472-130">Opis</span><span class="sxs-lookup"><span data-stu-id="f6472-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f6472-131">1</span><span class="sxs-lookup"><span data-stu-id="f6472-131">1</span></span> |<span data-ttu-id="f6472-132">Diodę LED awarii</span><span class="sxs-lookup"><span data-stu-id="f6472-132">Fault LED</span></span> |
   | <span data-ttu-id="f6472-133">2</span><span class="sxs-lookup"><span data-stu-id="f6472-133">2</span></span> |<span data-ttu-id="f6472-134">Power LED</span><span class="sxs-lookup"><span data-stu-id="f6472-134">Power LED</span></span> |
   | <span data-ttu-id="f6472-135">3</span><span class="sxs-lookup"><span data-stu-id="f6472-135">3</span></span> |<span data-ttu-id="f6472-136">Złączy SAS</span><span class="sxs-lookup"><span data-stu-id="f6472-136">SAS connectors</span></span> |
   | <span data-ttu-id="f6472-137">4</span><span class="sxs-lookup"><span data-stu-id="f6472-137">4</span></span> |<span data-ttu-id="f6472-138">LED SAS</span><span class="sxs-lookup"><span data-stu-id="f6472-138">SAS LEDs</span></span> |
   | <span data-ttu-id="f6472-139">5</span><span class="sxs-lookup"><span data-stu-id="f6472-139">5</span></span> |<span data-ttu-id="f6472-140">Porty szeregowe fabryki wyłącznie do użytku</span><span class="sxs-lookup"><span data-stu-id="f6472-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="f6472-141">6</span><span class="sxs-lookup"><span data-stu-id="f6472-141">6</span></span> |<span data-ttu-id="f6472-142">Port (hosta)</span><span class="sxs-lookup"><span data-stu-id="f6472-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="f6472-143">7</span><span class="sxs-lookup"><span data-stu-id="f6472-143">7</span></span> |<span data-ttu-id="f6472-144">Port B (Host out)</span><span class="sxs-lookup"><span data-stu-id="f6472-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="f6472-145">8</span><span class="sxs-lookup"><span data-stu-id="f6472-145">8</span></span> |<span data-ttu-id="f6472-146">Port C (tylko w przypadku używania fabryki)</span><span class="sxs-lookup"><span data-stu-id="f6472-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="f6472-147">Instalowanie nowego kontrolera EBOD</span><span class="sxs-lookup"><span data-stu-id="f6472-147">Install a new EBOD controller</span></span>
<span data-ttu-id="f6472-148">Hello następujące procedura i tabela wyjaśniają sposób tooinstall moduł kontrolera EBOD w urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f6472-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="f6472-149">tooinstall EBOD kontrolera</span><span class="sxs-lookup"><span data-stu-id="f6472-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="f6472-150">Sprawdź urządzenie EBOD hello za szkody, szczególnie toohello interfejsu łącznika.</span><span class="sxs-lookup"><span data-stu-id="f6472-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="f6472-151">Nie należy instalować hello nowego kontrolera EBOD, jeśli zgięte żadnych kodów PIN.</span><span class="sxs-lookup"><span data-stu-id="f6472-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="f6472-152">Otwórz pozycji, moduł hello slajdów hello obudowy do momentu Uwzględnij zamków hello zamków hello w hello.</span><span class="sxs-lookup"><span data-stu-id="f6472-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![Instalowanie kontrolera EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="f6472-154">**Rysunek 2** instalowanie hello EBOD kontrolera modułu</span><span class="sxs-lookup"><span data-stu-id="f6472-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="f6472-155">Zamknij hello zatrzaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="f6472-155">Close hello latch.</span></span> <span data-ttu-id="f6472-156">Kliknięcie usłyszeć jako angażujący hello zatrzaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="f6472-156">You should hear a click as hello latch engages.</span></span>
   
    ![Zwalnianie zatrzaśnięcia EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="f6472-158">**Rysunek 3** zamknięcie zatrzaśnięcia modułu EBOD hello</span><span class="sxs-lookup"><span data-stu-id="f6472-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="f6472-159">Ponownie podłącz kable hello.</span><span class="sxs-lookup"><span data-stu-id="f6472-159">Reconnect hello cables.</span></span> <span data-ttu-id="f6472-160">Użyj hello dokładnej konfiguracji, która znajdowała się przed hello zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="f6472-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="f6472-161">Zobacz powitania po diagram i tabeli, aby uzyskać szczegółowe informacje o tym, jak tooconnect hello kable.</span><span class="sxs-lookup"><span data-stu-id="f6472-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![Podłączanie kabli do urządzenia 4U zasilania](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="f6472-163">**Rysunek 4**.</span><span class="sxs-lookup"><span data-stu-id="f6472-163">**Figure 4**.</span></span> <span data-ttu-id="f6472-164">Ponownie podłączyć kable</span><span class="sxs-lookup"><span data-stu-id="f6472-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="f6472-165">Etykieta</span><span class="sxs-lookup"><span data-stu-id="f6472-165">Label</span></span> | <span data-ttu-id="f6472-166">Opis</span><span class="sxs-lookup"><span data-stu-id="f6472-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="f6472-167">1</span><span class="sxs-lookup"><span data-stu-id="f6472-167">1</span></span> |<span data-ttu-id="f6472-168">Obudowa podstawowego</span><span class="sxs-lookup"><span data-stu-id="f6472-168">Primary enclosure</span></span> |
   | <span data-ttu-id="f6472-169">2</span><span class="sxs-lookup"><span data-stu-id="f6472-169">2</span></span> |<span data-ttu-id="f6472-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="f6472-170">PCM 0</span></span> |
   | <span data-ttu-id="f6472-171">3</span><span class="sxs-lookup"><span data-stu-id="f6472-171">3</span></span> |<span data-ttu-id="f6472-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="f6472-172">PCM 1</span></span> |
   | <span data-ttu-id="f6472-173">4</span><span class="sxs-lookup"><span data-stu-id="f6472-173">4</span></span> |<span data-ttu-id="f6472-174">Kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="f6472-174">Controller 0</span></span> |
   | <span data-ttu-id="f6472-175">5</span><span class="sxs-lookup"><span data-stu-id="f6472-175">5</span></span> |<span data-ttu-id="f6472-176">Kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="f6472-176">Controller 1</span></span> |
   | <span data-ttu-id="f6472-177">6</span><span class="sxs-lookup"><span data-stu-id="f6472-177">6</span></span> |<span data-ttu-id="f6472-178">EBOD kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="f6472-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="f6472-179">7</span><span class="sxs-lookup"><span data-stu-id="f6472-179">7</span></span> |<span data-ttu-id="f6472-180">EBOD kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="f6472-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="f6472-181">8</span><span class="sxs-lookup"><span data-stu-id="f6472-181">8</span></span> |<span data-ttu-id="f6472-182">Obudowa EBOD</span><span class="sxs-lookup"><span data-stu-id="f6472-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="f6472-183">9</span><span class="sxs-lookup"><span data-stu-id="f6472-183">9</span></span> |<span data-ttu-id="f6472-184">Jednostki dystrybucji zasilania</span><span class="sxs-lookup"><span data-stu-id="f6472-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f6472-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6472-185">Next steps</span></span>
<span data-ttu-id="f6472-186">Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="f6472-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

