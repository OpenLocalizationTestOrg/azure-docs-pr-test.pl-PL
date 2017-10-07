---
title: "Connect Intel Edison (C) tooAzure IoT — Lekcja 1: Konfigurowanie urządzenia | Dokumentacja firmy Microsoft"
description: "Konfigurowanie Intel Edison do pierwszego użycia."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino Konfigurowanie, Połącz arduino toopc, arduino Instalatora, arduino tablicy"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5e06e06f1fcea02086e95742804f82cfcb8e265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="31cb5-104">Konfigurowanie sieci Edison Intel</span><span class="sxs-lookup"><span data-stu-id="31cb5-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="31cb5-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="31cb5-105">What you will do</span></span>
<span data-ttu-id="31cb5-106">Konfigurowanie Intel Edison do użycia po raz pierwszy przez łączenie tablicy hello, włączanie go i instalowanie konfiguracji narzędzia tooyour pulpitu systemu operacyjnego tooflash Edison w oprogramowaniu układowym, ustaw hasło i podłącz go tooWi-Fi.</span><span class="sxs-lookup"><span data-stu-id="31cb5-106">Configure Intel Edison for first-time use by assembling hello board, powering it up and installing configuration tool tooyour desktop OS tooflash Edison's firmware, set its password and connect it tooWi-Fi.</span></span> <span data-ttu-id="31cb5-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="31cb5-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="31cb5-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="31cb5-108">What you will learn</span></span>
<span data-ttu-id="31cb5-109">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="31cb5-109">In this article, you will learn:</span></span>

* <span data-ttu-id="31cb5-110">Jak płycie tooassemble Edison i włączenie go w górę.</span><span class="sxs-lookup"><span data-stu-id="31cb5-110">How tooassemble Edison board and power it up.</span></span>
* <span data-ttu-id="31cb5-111">Jak tooflash Edison oprogramowania układowego, ustaw hasło i połączenia sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="31cb5-111">How tooflash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="31cb5-112">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="31cb5-112">What you need</span></span>
<span data-ttu-id="31cb5-113">toocomplete tej operacji, należy po części z Twojej firmy Intel Edison Starter Kit hello:</span><span class="sxs-lookup"><span data-stu-id="31cb5-113">toocomplete this operation, you need hello following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="31cb5-114">Moduł Intel® Edison</span><span class="sxs-lookup"><span data-stu-id="31cb5-114">Intel® Edison module</span></span>
* <span data-ttu-id="31cb5-115">Karty rozszerzeń Arduino</span><span class="sxs-lookup"><span data-stu-id="31cb5-115">Arduino expansion board</span></span>
* <span data-ttu-id="31cb5-116">Paski rozdzielacza lub śruby zawarte w pakiecie hello, w tym cztery zestawy śruby i tworzywa odstępników i dwie śruby toofasten hello modułu toohello rozszerzenia tablicy.</span><span class="sxs-lookup"><span data-stu-id="31cb5-116">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="31cb5-117">TooType Micro B kabla A USB</span><span class="sxs-lookup"><span data-stu-id="31cb5-117">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="31cb5-118">Zasilacz prądu (DC).</span><span class="sxs-lookup"><span data-stu-id="31cb5-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="31cb5-119">Zasilacza powinny być sklasyfikowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="31cb5-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="31cb5-120">7-15V KONTROLERA DOMENY</span><span class="sxs-lookup"><span data-stu-id="31cb5-120">7-15V DC</span></span>
  - <span data-ttu-id="31cb5-121">Co najmniej 1500mA</span><span class="sxs-lookup"><span data-stu-id="31cb5-121">At least 1500mA</span></span>
  - <span data-ttu-id="31cb5-122">numer pin center/wewnętrzny Hello powinna być bieguna dodatnie hello hello zasilania</span><span class="sxs-lookup"><span data-stu-id="31cb5-122">hello center/inner pin should be hello positive pole of hello power supply</span></span>

  ![Elementy w zestawie początkowy](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="31cb5-124">Wymagane są również:</span><span class="sxs-lookup"><span data-stu-id="31cb5-124">You also need:</span></span>

* <span data-ttu-id="31cb5-125">Komputer z systemem Windows, Mac lub Linux.</span><span class="sxs-lookup"><span data-stu-id="31cb5-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="31cb5-126">Połączenia bezprzewodowego tooconnect Edison do.</span><span class="sxs-lookup"><span data-stu-id="31cb5-126">A wireless connection for Edison tooconnect to.</span></span>
* <span data-ttu-id="31cb5-127">Internet połączenia toodownload narzędzie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="31cb5-127">An Internet connection toodownload configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="31cb5-128">Złóż tablicy</span><span class="sxs-lookup"><span data-stu-id="31cb5-128">Assemble your board</span></span>

<span data-ttu-id="31cb5-129">Ta sekcja zawiera kroki tooattach Intel® Edison modułu tooyour rozszerzenia tablicy.</span><span class="sxs-lookup"><span data-stu-id="31cb5-129">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="31cb5-130">Umieść hello Intel® Edison modułu w ramach konspektu hello białe na tablicy rozszerzenia, wyrównywanie hello luk w hello module z śruby hello na powitania rozszerzenia tablicy.</span><span class="sxs-lookup"><span data-stu-id="31cb5-130">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="31cb5-131">Naciśnij modułu hello poniżej słowa hello `What will you make?` dopóki uważasz, że bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="31cb5-131">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![Złóż tablicy 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="31cb5-133">Użyj karty rozszerzeń toohello hello dwa szesnastkowych poziomie NTS (zawarte w pakiecie hello) toosecure hello modułu.</span><span class="sxs-lookup"><span data-stu-id="31cb5-133">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![Złóż tablicy 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="31cb5-135">Wstaw śruby w jednej z czterech luk rogu hello na powitania rozszerzenia tablicy.</span><span class="sxs-lookup"><span data-stu-id="31cb5-135">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="31cb5-136">Skręcenie i zwiększyć jedną hello białe plastikowe odstępników na powitania gwintowanym.</span><span class="sxs-lookup"><span data-stu-id="31cb5-136">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![Złóż tablicy 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="31cb5-138">Powtórz te czynności dla hello innych odstępników trzy rogu.</span><span class="sxs-lookup"><span data-stu-id="31cb5-138">Repeat for hello other three corner spacers.</span></span>

   ![Złóż tablicy 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="31cb5-140">Teraz budowy tablicy.</span><span class="sxs-lookup"><span data-stu-id="31cb5-140">Now your board is assembled.</span></span>

   ![złożony tablicy](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="31cb5-142">Włącz Edison</span><span class="sxs-lookup"><span data-stu-id="31cb5-142">Power up Edison</span></span>

1. <span data-ttu-id="31cb5-143">Dołącz hello zasilania.</span><span class="sxs-lookup"><span data-stu-id="31cb5-143">Plug in hello power supply.</span></span>

   ![Podłącz zasilacz](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="31cb5-145">Zielona LED (oznaczony DS1 na powitania karty rozszerzeń Arduino *) powinien podświetlony i pozostać podświetlone.</span><span class="sxs-lookup"><span data-stu-id="31cb5-145">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="31cb5-146">Poczekaj na jedną minutę na powitania tablicy toofinish rozruch.</span><span class="sxs-lookup"><span data-stu-id="31cb5-146">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31cb5-147">Jeśli nie masz zasilacz kontrolera domeny, można nadal zasilania hello tablicy za pośrednictwem portu USB.</span><span class="sxs-lookup"><span data-stu-id="31cb5-147">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="31cb5-148">Zobacz `Connect Edison tooyour computer` sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="31cb5-148">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="31cb5-149">Włączanie tablicy w ten sposób może spowodować nieprzewidywalne zachowanie z tablicy, szczególnie w przypadku, gdy przy użyciu sieci Wi-Fi lub zwiększają motors.</span><span class="sxs-lookup"><span data-stu-id="31cb5-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="31cb5-150">Podłącz komputer tooyour Edison</span><span class="sxs-lookup"><span data-stu-id="31cb5-150">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="31cb5-151">Przełącz dół mikroprzełącznika hello kierunku Witaj dwie micro portów USB, dzięki czemu Edison jest w trybie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="31cb5-151">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="31cb5-152">Różnice między trybu urządzenia ani hosta, odwołanie [tutaj](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="31cb5-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Przełącz mikroprzełącznika hello w dół](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="31cb5-154">Podłącz kabel USB micro hello do portu USB micro najwyższego hello.</span><span class="sxs-lookup"><span data-stu-id="31cb5-154">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Górny micro portu USB](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="31cb5-156">Plug hello drugiej, kabel USB do komputera.</span><span class="sxs-lookup"><span data-stu-id="31cb5-156">Plug hello other end of USB cable into your computer.</span></span>

   ![Komputer USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="31cb5-158">Będzie wiadomo, że tablicy jest w pełni zainicjowany, gdy komputer instaluje nowy dysk (podobne jak w przypadku Wstawianie karta SD do komputera).</span><span class="sxs-lookup"><span data-stu-id="31cb5-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="31cb5-159">Pobierz i uruchom narzędzie konfiguracji hello</span><span class="sxs-lookup"><span data-stu-id="31cb5-159">Download and run hello configuration tool</span></span>
<span data-ttu-id="31cb5-160">Pobierz najnowsze narzędzia konfiguracji hello z [to łącze](https://software.intel.com/en-us/iot/hardware/edison/downloads) kategorii hello `Installers` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="31cb5-160">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="31cb5-161">Wykonaj hello narzędzia i postępuj zgodnie z jego na ekranie instrukcjami, klikając przycisk Dalej, w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="31cb5-161">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="31cb5-162">Oprogramowanie układowe Flash</span><span class="sxs-lookup"><span data-stu-id="31cb5-162">Flash firmware</span></span>
1. <span data-ttu-id="31cb5-163">Na powitania `Set up options` kliknij `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="31cb5-163">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="31cb5-164">Wybierz hello tooflash obrazu na tablicy, wykonując jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="31cb5-164">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="31cb5-165">toodownload i flash tablicy o hello najnowszego oprogramowania układowego obraz dostępne z firmy Intel, wybierz `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="31cb5-165">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="31cb5-166">Wybierz tablicy z obrazem, który został zapisany już na komputerze, tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="31cb5-166">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="31cb5-167">Przeglądaj tooand hello wybierz obraz ma tooflash tooyour tablicy.</span><span class="sxs-lookup"><span data-stu-id="31cb5-167">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="31cb5-168">Narzędzie Instalatora Hello podejmie tooflash tablicy.</span><span class="sxs-lookup"><span data-stu-id="31cb5-168">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="31cb5-169">cały proces miga Hello może trwać too10 minut.</span><span class="sxs-lookup"><span data-stu-id="31cb5-169">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="31cb5-170">Ustaw hasło</span><span class="sxs-lookup"><span data-stu-id="31cb5-170">Set password</span></span>
1. <span data-ttu-id="31cb5-171">Na powitania `Set up options` kliknij `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="31cb5-171">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="31cb5-172">Można ustawić niestandardową nazwę tablicy Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="31cb5-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="31cb5-173">Jest to opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="31cb5-173">This is optional.</span></span>
3. <span data-ttu-id="31cb5-174">Wpisz hasło do tablicy, a następnie kliknij przycisk `Set password`.</span><span class="sxs-lookup"><span data-stu-id="31cb5-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="31cb5-175">Oznacz hello hasła, które jest później używany w dół.</span><span class="sxs-lookup"><span data-stu-id="31cb5-175">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="31cb5-176">Połączenia sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="31cb5-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="31cb5-177">Na powitania `Set up options` kliknij `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="31cb5-177">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="31cb5-178">Poczekaj zapasowej minutę tooone jako użytkownika skanowania komputera dostępnych sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="31cb5-178">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="31cb5-179">Z hello `Detected Networks` listy rozwijanej wybierz sieci.</span><span class="sxs-lookup"><span data-stu-id="31cb5-179">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="31cb5-180">Z hello `Security` listy rozwijanej, wybierz hello sieci typu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="31cb5-180">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="31cb5-181">Udostępnić informacje logowania i hasło, a następnie kliknij przycisk `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="31cb5-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="31cb5-182">Oznacz dół hello adres IP, który jest później używany.</span><span class="sxs-lookup"><span data-stu-id="31cb5-182">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="31cb5-183">Upewnij się, że Edison jest połączonych toohello sam sieci jako komputera.</span><span class="sxs-lookup"><span data-stu-id="31cb5-183">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="31cb5-184">Komputer łączy tooyour Edison przy użyciu adresu IP hello.</span><span class="sxs-lookup"><span data-stu-id="31cb5-184">Your computer connects tooyour Edison by using hello IP address.</span></span>

<span data-ttu-id="31cb5-185">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="31cb5-185">Congratulations!</span></span> <span data-ttu-id="31cb5-186">Pomyślnie skonfigurowano Edison.</span><span class="sxs-lookup"><span data-stu-id="31cb5-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="31cb5-187">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="31cb5-187">Summary</span></span>
<span data-ttu-id="31cb5-188">W tym artykule kiedy znasz już jak tooassemble hello tablicy Edison, flash jego oprogramowania układowego, ustawienia hasła i podłącz go tooWi-Fi za pomocą narzędzia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="31cb5-188">In this article, you’ve learned how tooassemble hello Edison board, flash its firmware, setup password and connect it tooWi-Fi by using configuration tool.</span></span> <span data-ttu-id="31cb5-189">Należy pamiętać, że powitalne LED jeszcze nie podświetlony.</span><span class="sxs-lookup"><span data-stu-id="31cb5-189">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="31cb5-190">następne zadanie Hello jest tooinstall hello niezbędne narzędzia i oprogramowania w ramach przygotowań do uruchomienia na Edison przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="31cb5-190">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31cb5-191">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="31cb5-191">Next steps</span></span>
<span data-ttu-id="31cb5-192">[Pobierz narzędzia hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="31cb5-192">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md