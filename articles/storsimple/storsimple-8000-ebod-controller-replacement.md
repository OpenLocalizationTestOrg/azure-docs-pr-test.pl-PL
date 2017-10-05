---
title: "Zastąp kontrolera StorSimple 8600 EBOD | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak usunąć i Zastąp jeden lub oba kontrolerów EBOD na urządzeniu StorSimple 8600."
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
ms.openlocfilehash: 45699c267d1009c4884dd164fd3f2950d6d5f555
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="23e36-103">Zastąp kontrolera EBOD na urządzeniu StorSimple</span><span class="sxs-lookup"><span data-stu-id="23e36-103">Replace an EBOD controller on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="23e36-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="23e36-104">Overview</span></span>
<span data-ttu-id="23e36-105">W tym samouczku wyjaśniono, jak zastąpić uszkodzony moduł kontrolera EBOD na urządzeniu Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="23e36-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="23e36-106">Aby zastąpić moduł kontrolera EBOD, musisz:</span><span class="sxs-lookup"><span data-stu-id="23e36-106">To replace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="23e36-107">Usunąć uszkodzony kontroler EBOD</span><span class="sxs-lookup"><span data-stu-id="23e36-107">Remove the faulty EBOD controller</span></span>
* <span data-ttu-id="23e36-108">Instalowanie nowego kontrolera EBOD</span><span class="sxs-lookup"><span data-stu-id="23e36-108">Install a new EBOD controller</span></span>

<span data-ttu-id="23e36-109">Przed rozpoczęciem należy wziąć pod uwagę następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="23e36-109">Consider the following information before you begin:</span></span>

* <span data-ttu-id="23e36-110">Puste EBOD moduły muszą być wstawiane do wszystkich miejsc nieużywane.</span><span class="sxs-lookup"><span data-stu-id="23e36-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="23e36-111">Obudowa nie zostanie poprawnie cool, jeśli gnieździe pozostanie otwarte.</span><span class="sxs-lookup"><span data-stu-id="23e36-111">The enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="23e36-112">Kontroler EBOD jest wyłączania i można go usunąć ani zastąpić.</span><span class="sxs-lookup"><span data-stu-id="23e36-112">The EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="23e36-113">Nie usuwaj modułu nie powiodło się, dopóki nie uzyskasz zastępczy.</span><span class="sxs-lookup"><span data-stu-id="23e36-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="23e36-114">Po zainicjowaniu procesu wymiany musi zakończyć w ciągu 10 minut.</span><span class="sxs-lookup"><span data-stu-id="23e36-114">When you initiate the replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23e36-115">Przed próbą należy usunąć lub zamienić dowolny składnik StorSimple, upewnij się, należy przejrzeć [bezpieczeństwa ikona konwencje](storsimple-safety.md#safety-icon-conventions) i innych [środki ostrożności](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="23e36-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="23e36-116">Usuwanie kontrolera EBOD</span><span class="sxs-lookup"><span data-stu-id="23e36-116">Remove an EBOD controller</span></span>
<span data-ttu-id="23e36-117">Przed zastąpieniem modułu kontrolera EBOD w urządzeniu StorSimple, upewnij się, że inny moduł kontrolera EBOD jest aktywne i uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="23e36-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span></span> <span data-ttu-id="23e36-118">Poniższe procedury i tabela wyjaśniono, jak usunąć moduł kontrolera EBOD.</span><span class="sxs-lookup"><span data-stu-id="23e36-118">The following procedure and table explain how to remove the EBOD controller module.</span></span>

#### <a name="to-remove-an-ebod-module"></a><span data-ttu-id="23e36-119">Aby usunąć moduł EBOD</span><span class="sxs-lookup"><span data-stu-id="23e36-119">To remove an EBOD module</span></span>
1. <span data-ttu-id="23e36-120">Otwórz Azure portal.</span><span class="sxs-lookup"><span data-stu-id="23e36-120">Open the Azure portal.</span></span>
2. <span data-ttu-id="23e36-121">Przejdź do urządzenia, a następnie przejdź do **ustawienia** > **kondycji sprzętu**i sprawdź, czy stan LED dla aktywnego modułu kontrolera EBOD jest zielony oraz LED kontrolera EBOD nie powiodło się Moduł jest czerwony.</span><span class="sxs-lookup"><span data-stu-id="23e36-121">Go to your device and navigate to **Settings** > **Hardware health**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="23e36-122">Znajdź moduł kontrolera EBOD nie powiodło się z tyłu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="23e36-122">Locate the failed EBOD controller module at the back of the device.</span></span>
4. <span data-ttu-id="23e36-123">Usuń kable łączące EBOD modułu kontrolera do kontrolera przed zmianą modułu EBOD z systemu.</span><span class="sxs-lookup"><span data-stu-id="23e36-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span></span>
5. <span data-ttu-id="23e36-124">Zanotuj dokładne port SAS EBOD moduł kontrolera, który był połączony z kontrolerem.</span><span class="sxs-lookup"><span data-stu-id="23e36-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span></span> <span data-ttu-id="23e36-125">Trzeba będzie przywrócić system do tej konfiguracji po zastąpienie modułu EBOD.</span><span class="sxs-lookup"><span data-stu-id="23e36-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="23e36-126">Zazwyczaj jest to Port A, który jest oznaczony jako **hosta w** na poniższym diagramie.</span><span class="sxs-lookup"><span data-stu-id="23e36-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span></span>
   
    ![Kontroler IDE EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="23e36-128">**Rysunek 1** EBOD z powrotem modułu</span><span class="sxs-lookup"><span data-stu-id="23e36-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="23e36-129">Etykieta</span><span class="sxs-lookup"><span data-stu-id="23e36-129">Label</span></span> | <span data-ttu-id="23e36-130">Opis</span><span class="sxs-lookup"><span data-stu-id="23e36-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="23e36-131">1</span><span class="sxs-lookup"><span data-stu-id="23e36-131">1</span></span> |<span data-ttu-id="23e36-132">Diodę LED awarii</span><span class="sxs-lookup"><span data-stu-id="23e36-132">Fault LED</span></span> |
   | <span data-ttu-id="23e36-133">2</span><span class="sxs-lookup"><span data-stu-id="23e36-133">2</span></span> |<span data-ttu-id="23e36-134">Power LED</span><span class="sxs-lookup"><span data-stu-id="23e36-134">Power LED</span></span> |
   | <span data-ttu-id="23e36-135">3</span><span class="sxs-lookup"><span data-stu-id="23e36-135">3</span></span> |<span data-ttu-id="23e36-136">Złączy SAS</span><span class="sxs-lookup"><span data-stu-id="23e36-136">SAS connectors</span></span> |
   | <span data-ttu-id="23e36-137">4</span><span class="sxs-lookup"><span data-stu-id="23e36-137">4</span></span> |<span data-ttu-id="23e36-138">LED SAS</span><span class="sxs-lookup"><span data-stu-id="23e36-138">SAS LEDs</span></span> |
   | <span data-ttu-id="23e36-139">5</span><span class="sxs-lookup"><span data-stu-id="23e36-139">5</span></span> |<span data-ttu-id="23e36-140">Porty szeregowe fabryki wyłącznie do użytku</span><span class="sxs-lookup"><span data-stu-id="23e36-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="23e36-141">6</span><span class="sxs-lookup"><span data-stu-id="23e36-141">6</span></span> |<span data-ttu-id="23e36-142">Port (hosta)</span><span class="sxs-lookup"><span data-stu-id="23e36-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="23e36-143">7</span><span class="sxs-lookup"><span data-stu-id="23e36-143">7</span></span> |<span data-ttu-id="23e36-144">Port B (Host out)</span><span class="sxs-lookup"><span data-stu-id="23e36-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="23e36-145">8</span><span class="sxs-lookup"><span data-stu-id="23e36-145">8</span></span> |<span data-ttu-id="23e36-146">Port C (tylko w przypadku używania fabryki)</span><span class="sxs-lookup"><span data-stu-id="23e36-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="23e36-147">Instalowanie nowego kontrolera EBOD</span><span class="sxs-lookup"><span data-stu-id="23e36-147">Install a new EBOD controller</span></span>
<span data-ttu-id="23e36-148">Poniższe procedury i tabela wyjaśniono, jak zainstalować moduł kontrolera EBOD w urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="23e36-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span></span>

#### <a name="to-install-an-ebod-controller"></a><span data-ttu-id="23e36-149">Aby zainstalować kontroler EBOD</span><span class="sxs-lookup"><span data-stu-id="23e36-149">To install an EBOD controller</span></span>
1. <span data-ttu-id="23e36-150">Sprawdź urządzenie EBOD za szkody, szczególnie w celu łącznika interfejsu.</span><span class="sxs-lookup"><span data-stu-id="23e36-150">Check the EBOD device for damage, especially to the interface connector.</span></span> <span data-ttu-id="23e36-151">Nie należy instalować na nowy kontroler EBOD, jeśli zgięte żadnych kodów PIN.</span><span class="sxs-lookup"><span data-stu-id="23e36-151">Do not install the new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="23e36-152">Z zamków w pozycji otwarcia dopóki Uwzględnij zamków slajd modułu do obudowy.</span><span class="sxs-lookup"><span data-stu-id="23e36-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span></span>
   
    ![Instalowanie kontrolera EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="23e36-154">**Rysunek 2** Instalowanie modułu kontrolera EBOD</span><span class="sxs-lookup"><span data-stu-id="23e36-154">**Figure 2**  Installing the EBOD controller module</span></span>
3. <span data-ttu-id="23e36-155">Zamknij zatrzaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="23e36-155">Close the latch.</span></span> <span data-ttu-id="23e36-156">Kliknięcie usłyszeć jako angażujący zatrzaśnięcia.</span><span class="sxs-lookup"><span data-stu-id="23e36-156">You should hear a click as the latch engages.</span></span>
   
    ![Zwalnianie zatrzaśnięcia EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="23e36-158">**Rysunek 3** zamknięcia EBOD zatrzaśnięcia modułu</span><span class="sxs-lookup"><span data-stu-id="23e36-158">**Figure 3**  Closing the EBOD module latch</span></span>
4. <span data-ttu-id="23e36-159">Ponownie podłącz kable.</span><span class="sxs-lookup"><span data-stu-id="23e36-159">Reconnect the cables.</span></span> <span data-ttu-id="23e36-160">Użyj dokładnej konfiguracji, która została użyta przed zastąpienia.</span><span class="sxs-lookup"><span data-stu-id="23e36-160">Use the exact configuration that was present before the replacement.</span></span> <span data-ttu-id="23e36-161">Zobacz poniższy diagram i tabela zawiera szczegółowe informacje o sposobie Podłącz kable.</span><span class="sxs-lookup"><span data-stu-id="23e36-161">See the following diagram and table for details about how to connect the cables.</span></span>
   
    ![Podłączanie kabli do urządzenia 4U zasilania](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="23e36-163">**Rysunek 4**.</span><span class="sxs-lookup"><span data-stu-id="23e36-163">**Figure 4**.</span></span> <span data-ttu-id="23e36-164">Ponownie podłączyć kable</span><span class="sxs-lookup"><span data-stu-id="23e36-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="23e36-165">Etykieta</span><span class="sxs-lookup"><span data-stu-id="23e36-165">Label</span></span> | <span data-ttu-id="23e36-166">Opis</span><span class="sxs-lookup"><span data-stu-id="23e36-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="23e36-167">1</span><span class="sxs-lookup"><span data-stu-id="23e36-167">1</span></span> |<span data-ttu-id="23e36-168">Obudowa podstawowego</span><span class="sxs-lookup"><span data-stu-id="23e36-168">Primary enclosure</span></span> |
   | <span data-ttu-id="23e36-169">2</span><span class="sxs-lookup"><span data-stu-id="23e36-169">2</span></span> |<span data-ttu-id="23e36-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="23e36-170">PCM 0</span></span> |
   | <span data-ttu-id="23e36-171">3</span><span class="sxs-lookup"><span data-stu-id="23e36-171">3</span></span> |<span data-ttu-id="23e36-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="23e36-172">PCM 1</span></span> |
   | <span data-ttu-id="23e36-173">4</span><span class="sxs-lookup"><span data-stu-id="23e36-173">4</span></span> |<span data-ttu-id="23e36-174">Kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="23e36-174">Controller 0</span></span> |
   | <span data-ttu-id="23e36-175">5</span><span class="sxs-lookup"><span data-stu-id="23e36-175">5</span></span> |<span data-ttu-id="23e36-176">Kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="23e36-176">Controller 1</span></span> |
   | <span data-ttu-id="23e36-177">6</span><span class="sxs-lookup"><span data-stu-id="23e36-177">6</span></span> |<span data-ttu-id="23e36-178">EBOD kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="23e36-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="23e36-179">7</span><span class="sxs-lookup"><span data-stu-id="23e36-179">7</span></span> |<span data-ttu-id="23e36-180">EBOD kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="23e36-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="23e36-181">8</span><span class="sxs-lookup"><span data-stu-id="23e36-181">8</span></span> |<span data-ttu-id="23e36-182">Obudowa EBOD</span><span class="sxs-lookup"><span data-stu-id="23e36-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="23e36-183">9</span><span class="sxs-lookup"><span data-stu-id="23e36-183">9</span></span> |<span data-ttu-id="23e36-184">Jednostki dystrybucji zasilania</span><span class="sxs-lookup"><span data-stu-id="23e36-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="23e36-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="23e36-185">Next steps</span></span>
<span data-ttu-id="23e36-186">Dowiedz się więcej o [wymiana składników sprzętowych StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="23e36-186">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

