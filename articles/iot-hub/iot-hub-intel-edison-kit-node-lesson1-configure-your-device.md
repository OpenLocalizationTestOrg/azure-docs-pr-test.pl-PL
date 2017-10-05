---
title: "Nawiązać Edison firmy Intel (węzeł) Azure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie Intel Edison do pierwszego użycia."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino ustawienie nawiązać arduino komputerów, arduino Instalatora, arduino tablicy"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 87bf3a917af096e43a43a2143afa4bf43a72d7fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="1a8a1-104">Konfigurowanie sieci Edison Intel</span><span class="sxs-lookup"><span data-stu-id="1a8a1-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1a8a1-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="1a8a1-105">What you will do</span></span>
<span data-ttu-id="1a8a1-106">Konfigurowanie Intel Edison do użycia po raz pierwszy przez łączenie tablicy go podłączone do zasilania i instalacja narzędzia do konfiguracji pulpitu system operacyjny do flash Edison w oprogramowaniu układowym, ustaw hasło i połącz ją z sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="1a8a1-107">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="1a8a1-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1a8a1-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="1a8a1-108">What you will learn</span></span>
<span data-ttu-id="1a8a1-109">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="1a8a1-109">In this article, you will learn:</span></span>

* <span data-ttu-id="1a8a1-110">Jak utworzyć Edison tablicy i włączenie go w górę.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="1a8a1-111">Jak flash Edison w oprogramowaniu układowym, ustaw hasło i połączenia sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1a8a1-112">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="1a8a1-112">What you need</span></span>
<span data-ttu-id="1a8a1-113">Aby wykonać tę operację, potrzebne następujące elementy z Twojej firmy Intel Edison Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="1a8a1-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="1a8a1-114">Moduł Intel® Edison</span><span class="sxs-lookup"><span data-stu-id="1a8a1-114">Intel® Edison module</span></span>
* <span data-ttu-id="1a8a1-115">Karty rozszerzeń Arduino</span><span class="sxs-lookup"><span data-stu-id="1a8a1-115">Arduino expansion board</span></span>
* <span data-ttu-id="1a8a1-116">Paski rozdzielacza lub śruby zawarte w pakiecie, łącznie z dwóch śruby aby przyspieszyć modułu do karty rozszerzeń i cztery zestawy śruby i tworzywa odstępników.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="1a8a1-117">B Micro do kabla USB A typu</span><span class="sxs-lookup"><span data-stu-id="1a8a1-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="1a8a1-118">Zasilacz prądu (DC).</span><span class="sxs-lookup"><span data-stu-id="1a8a1-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="1a8a1-119">Zasilacza powinny być sklasyfikowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1a8a1-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="1a8a1-120">7-15V KONTROLERA DOMENY</span><span class="sxs-lookup"><span data-stu-id="1a8a1-120">7-15V DC</span></span>
  - <span data-ttu-id="1a8a1-121">Co najmniej 1500mA</span><span class="sxs-lookup"><span data-stu-id="1a8a1-121">At least 1500mA</span></span>
  - <span data-ttu-id="1a8a1-122">Numer pin center/wewnętrzny powinien być bieguna dodatnie zasilania</span><span class="sxs-lookup"><span data-stu-id="1a8a1-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![Elementy w zestawie początkowy](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="1a8a1-124">Wymagane są również:</span><span class="sxs-lookup"><span data-stu-id="1a8a1-124">You also need:</span></span>

* <span data-ttu-id="1a8a1-125">Komputer z systemem Windows, Mac lub Linux.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="1a8a1-126">Połączenia bezprzewodowego Edison do nawiązania połączenia.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="1a8a1-127">Połączenia internetowego na pobieranie narzędzia do konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="1a8a1-128">Złóż tablicy</span><span class="sxs-lookup"><span data-stu-id="1a8a1-128">Assemble your board</span></span>

<span data-ttu-id="1a8a1-129">Ta sekcja zawiera kroki, aby dołączyć modułu Intel® Edison do tablicy rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="1a8a1-130">Umieść modułu Intel® Edison w obrębie białe konspektu na tablicy rozszerzenia, wyrównywanie luk w module z śruby na tablicy rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="1a8a1-131">Naciśnij modułu poniżej słowa `What will you make?` dopóki uważasz, że bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![Złóż tablicy 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="1a8a1-133">Użyj dwóch szesnastkowych poziomie NTS (uwzględniony w pakiecie) do zabezpieczania modułu do karty rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![Złóż tablicy 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="1a8a1-135">Wstaw śruby w jednym z luk narożników na tablicy rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="1a8a1-136">Skręcenie i zwiększyć jedną białe plastikowe odstępników na śrubę.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![Złóż tablicy 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="1a8a1-138">Powtórz dla innych odstępników trzy rogu.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-138">Repeat for the other three corner spacers.</span></span>

   ![Złóż tablicy 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="1a8a1-140">Teraz budowy tablicy.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-140">Now your board is assembled.</span></span>

   ![złożony tablicy](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="1a8a1-142">Włącz Edison</span><span class="sxs-lookup"><span data-stu-id="1a8a1-142">Power up Edison</span></span>

1. <span data-ttu-id="1a8a1-143">Podłącz zasilania.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-143">Plug in the power supply.</span></span>

   ![Podłącz zasilacz](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="1a8a1-145">Zielona LED (oznaczony DS1 na tablicy rozszerzenia Arduino *) powinien podświetlony i pozostać podświetlone.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-145">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="1a8a1-146">Zaczekaj minutę dla tablicy ukończyć rozruch.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1a8a1-147">Jeśli nie masz zasilacz kontrolera domeny, można nadal zasilanie tablicy za pośrednictwem portu USB.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="1a8a1-148">Zobacz `Connect Edison to your computer` sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="1a8a1-149">Włączanie tablicy w ten sposób może spowodować nieprzewidywalne zachowanie z tablicy, szczególnie w przypadku, gdy przy użyciu sieci Wi-Fi lub zwiększają motors.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="1a8a1-150">Łączenie się z komputerem Edison</span><span class="sxs-lookup"><span data-stu-id="1a8a1-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="1a8a1-151">Przełącz dół mikroprzełącznika kierunku dwóch micro portów USB, dzięki czemu Edison jest w trybie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="1a8a1-152">Różnice między trybu urządzenia ani hosta, odwołanie [tutaj](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="1a8a1-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Przełącz mikroprzełącznika w dół](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="1a8a1-154">Podłącz kabel USB micro do górnej micro portu USB.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Górny micro portu USB](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="1a8a1-156">Podłącz drugi koniec kabla USB do komputera.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-156">Plug the other end of USB cable into your computer.</span></span>

   ![Komputer USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="1a8a1-158">Będzie wiadomo, że tablicy jest w pełni zainicjowany, gdy komputer instaluje nowy dysk (podobne jak w przypadku Wstawianie karta SD do komputera).</span><span class="sxs-lookup"><span data-stu-id="1a8a1-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="1a8a1-159">Pobierz i uruchom narzędzie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="1a8a1-159">Download and run the configuration tool</span></span>
<span data-ttu-id="1a8a1-160">Pobierz najnowsze narzędzia konfiguracji z [to łącze](https://software.intel.com/en-us/iot/hardware/edison/downloads) kategorii `Installers` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="1a8a1-161">Wykonywanie narzędzia i postępuj zgodnie z jego na ekranie instrukcjami, klikając przycisk Dalej, w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="1a8a1-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="1a8a1-162">Oprogramowanie układowe Flash</span><span class="sxs-lookup"><span data-stu-id="1a8a1-162">Flash firmware</span></span>
1. <span data-ttu-id="1a8a1-163">Na `Set up options` kliknij `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="1a8a1-164">Wybierz obraz do flash na tablicy, wykonując jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="1a8a1-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="1a8a1-165">Aby pobrać i flash tablicy przy użyciu najnowszej dostępnej w sklepie Intel obrazu oprogramowania układowego, wybierz `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="1a8a1-166">Aby flash tablicy z obrazem, który został zapisany już na komputerze, wybierz `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="1a8a1-167">Wyszukaj i wybierz obraz, który ma być flash do tablicy.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="1a8a1-168">Narzędzie instalacji będzie podejmować próby flash tablicy.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="1a8a1-169">Cały proces miga może potrwać do 10 minut.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="1a8a1-170">Ustaw hasło</span><span class="sxs-lookup"><span data-stu-id="1a8a1-170">Set password</span></span>
1. <span data-ttu-id="1a8a1-171">Na `Set up options` kliknij `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="1a8a1-172">Można ustawić niestandardową nazwę tablicy Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="1a8a1-173">Jest to opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-173">This is optional.</span></span>
3. <span data-ttu-id="1a8a1-174">Wpisz hasło do tablicy, a następnie kliknij przycisk `Set password`.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="1a8a1-175">Oznacz hasła, które jest później używany w dół.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="1a8a1-176">Połączenia sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="1a8a1-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="1a8a1-177">Na `Set up options` kliknij `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="1a8a1-178">Poczekaj maksymalnie jedną minutę, co komputer szuka dostępnych sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="1a8a1-179">Z `Detected Networks` listy rozwijanej wybierz sieci.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="1a8a1-180">Z `Security` listy rozwijanej wybierz typ zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="1a8a1-181">Udostępnić informacje logowania i hasło, a następnie kliknij przycisk `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="1a8a1-182">Zaznacz adres IP, który jest później używany.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="1a8a1-183">Upewnij się, że Edison jest podłączony do sieci z komputera.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="1a8a1-184">Komputer łączy się z Edison przy użyciu adresu IP.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="1a8a1-185">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="1a8a1-185">Congratulations!</span></span> <span data-ttu-id="1a8a1-186">Pomyślnie skonfigurowano Edison.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="1a8a1-187">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="1a8a1-187">Summary</span></span>
<span data-ttu-id="1a8a1-188">W tym artykule kiedy znasz już sposobu łączenia tablicy Edison, flash jego oprogramowania układowego, ustawienia hasła i podłącz go do sieci Wi-Fi za pomocą narzędzia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="1a8a1-189">Należy pamiętać, że jeszcze nie podświetlony LED.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="1a8a1-190">Następne zadanie jest Zainstaluj niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia na Edison przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1a8a1-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a8a1-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1a8a1-191">Next steps</span></span>
<span data-ttu-id="1a8a1-192">[Pobierz narzędzia][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="1a8a1-192">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md