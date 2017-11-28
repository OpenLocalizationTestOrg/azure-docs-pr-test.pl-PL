---
title: "aaaIntel Edison toocloud (Node.js) - Połącz Edison Intel tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz Intel Edison tooAzure Centrum IoT platformy Intel Edison toosend danych toohello chmury Azure w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Usługa Azure iot intel edison, intel edison Centrum iot, intel edison wysyłania danych toocloud, intel edison toocloud"
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a><span data-ttu-id="443f6-104">Połącz tooAzure Intel Edison Centrum IoT (Node.js)</span><span class="sxs-lookup"><span data-stu-id="443f6-104">Connect Intel Edison tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="443f6-105">W tym samouczku Rozpocznij od uczenia hello podstawowe informacje dotyczące pracy z Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="443f6-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="443f6-106">Następnie dowiesz się, jak połączyć tooseamlessly chmury toohello urządzeń przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="443f6-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="443f6-107">Nie masz jeszcze zestawu?</span><span class="sxs-lookup"><span data-stu-id="443f6-107">Don't have a kit yet?</span></span> <span data-ttu-id="443f6-108">Uruchom [tutaj](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="443f6-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="443f6-109">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="443f6-109">What you do</span></span>

* <span data-ttu-id="443f6-110">Konfiguracja Intel Edison i i Grove modułów.</span><span class="sxs-lookup"><span data-stu-id="443f6-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="443f6-111">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="443f6-111">Create an IoT hub.</span></span>
* <span data-ttu-id="443f6-112">Zarejestruj urządzenie dla Edison w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="443f6-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="443f6-113">Uruchom przykładową aplikację w Centrum IoT tooyour danych czujnika Edison toosend.</span><span class="sxs-lookup"><span data-stu-id="443f6-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="443f6-114">Połącz Centrum IoT tooan Edison firmy Intel, który utworzono.</span><span class="sxs-lookup"><span data-stu-id="443f6-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="443f6-115">Następnie możesz uruchomić przykładową aplikację na Edison toocollect temperatury i wilgotności danych z czujnika temperatury Grove.</span><span class="sxs-lookup"><span data-stu-id="443f6-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="443f6-116">Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.</span><span class="sxs-lookup"><span data-stu-id="443f6-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="443f6-117">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="443f6-117">What you learn</span></span>

* <span data-ttu-id="443f6-118">Jak toocreate Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="443f6-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="443f6-119">Jak tooconnect Edison z czujnika temperatury Grove.</span><span class="sxs-lookup"><span data-stu-id="443f6-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="443f6-120">Jak toocollect dane czujników, uruchamiając na Edison przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="443f6-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="443f6-121">Jak Centrum IoT tooyour danych czujnika toosend.</span><span class="sxs-lookup"><span data-stu-id="443f6-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="443f6-122">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="443f6-122">What you need</span></span>

![Co jest potrzebne](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="443f6-124">Witaj Intel Edison tablicy</span><span class="sxs-lookup"><span data-stu-id="443f6-124">hello Intel Edison board</span></span>
* <span data-ttu-id="443f6-125">Karty rozszerzeń Arduino</span><span class="sxs-lookup"><span data-stu-id="443f6-125">Arduino expansion board</span></span>
* <span data-ttu-id="443f6-126">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="443f6-126">An active Azure subscription.</span></span> <span data-ttu-id="443f6-127">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="443f6-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="443f6-128">Mac lub komputer z systemem Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="443f6-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="443f6-129">Połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="443f6-129">An Internet connection.</span></span>
* <span data-ttu-id="443f6-130">TooType Micro B kabla A USB</span><span class="sxs-lookup"><span data-stu-id="443f6-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="443f6-131">Zasilacz prądu (DC).</span><span class="sxs-lookup"><span data-stu-id="443f6-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="443f6-132">Zasilacza powinny być sklasyfikowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="443f6-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="443f6-133">7-15V KONTROLERA DOMENY</span><span class="sxs-lookup"><span data-stu-id="443f6-133">7-15V DC</span></span>
  - <span data-ttu-id="443f6-134">Co najmniej 1500mA</span><span class="sxs-lookup"><span data-stu-id="443f6-134">At least 1500mA</span></span>
  - <span data-ttu-id="443f6-135">numer pin center/wewnętrzny Hello powinna być bieguna dodatnie hello hello zasilania</span><span class="sxs-lookup"><span data-stu-id="443f6-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="443f6-136">Witaj, następujące elementy są opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="443f6-136">hello following items are optional:</span></span>

* <span data-ttu-id="443f6-137">Grove podstawowej tarczy V2</span><span class="sxs-lookup"><span data-stu-id="443f6-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="443f6-138">Grove - czujnik temperatury</span><span class="sxs-lookup"><span data-stu-id="443f6-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="443f6-139">Grove kabel</span><span class="sxs-lookup"><span data-stu-id="443f6-139">Grove Cable</span></span>
* <span data-ttu-id="443f6-140">Paski rozdzielacza lub śruby zawarte w pakiecie hello, w tym cztery zestawy śruby i tworzywa odstępników i dwie śruby toofasten hello modułu toohello rozszerzenia tablicy.</span><span class="sxs-lookup"><span data-stu-id="443f6-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="443f6-141">Te elementy są opcjonalne, ponieważ obsługa przykładowy kod hello symulowane danych czujnika.</span><span class="sxs-lookup"><span data-stu-id="443f6-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="443f6-142">Instalator Edison Intel</span><span class="sxs-lookup"><span data-stu-id="443f6-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="443f6-143">Złóż tablicy</span><span class="sxs-lookup"><span data-stu-id="443f6-143">Assemble your board</span></span>

<span data-ttu-id="443f6-144">Ta sekcja zawiera kroki tooattach Intel® Edison modułu tooyour rozszerzenia tablicy.</span><span class="sxs-lookup"><span data-stu-id="443f6-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="443f6-145">Umieść hello Intel® Edison modułu w ramach konspektu hello białe na tablicy rozszerzenia, wyrównywanie hello luk w hello module z śruby hello na powitania rozszerzenia tablicy.</span><span class="sxs-lookup"><span data-stu-id="443f6-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="443f6-146">Naciśnij modułu hello poniżej słowa hello `What will you make?` dopóki uważasz, że bardzo proste.</span><span class="sxs-lookup"><span data-stu-id="443f6-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![Złóż tablicy 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="443f6-148">Użyj karty rozszerzeń toohello hello dwa szesnastkowych poziomie NTS (zawarte w pakiecie hello) toosecure hello modułu.</span><span class="sxs-lookup"><span data-stu-id="443f6-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![Złóż tablicy 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="443f6-150">Wstaw śruby w jednej z czterech luk rogu hello na powitania rozszerzenia tablicy.</span><span class="sxs-lookup"><span data-stu-id="443f6-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="443f6-151">Skręcenie i zwiększyć jedną hello białe plastikowe odstępników na powitania gwintowanym.</span><span class="sxs-lookup"><span data-stu-id="443f6-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![Złóż tablicy 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="443f6-153">Powtórz te czynności dla hello innych odstępników trzy rogu.</span><span class="sxs-lookup"><span data-stu-id="443f6-153">Repeat for hello other three corner spacers.</span></span>

   ![Złóż tablicy 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="443f6-155">Teraz budowy tablicy.</span><span class="sxs-lookup"><span data-stu-id="443f6-155">Now your board is assembled.</span></span>

   ![złożony tablicy](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="443f6-157">Połącz hello tarczy Base Grove i hello czujnik temperatury</span><span class="sxs-lookup"><span data-stu-id="443f6-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="443f6-158">Umieść hello Grove Base tarczy na tooyour tablicy.</span><span class="sxs-lookup"><span data-stu-id="443f6-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="443f6-159">Upewnij się, że wszystkie numery PIN ściśle są podłączone do tablicy.</span><span class="sxs-lookup"><span data-stu-id="443f6-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Podstawowy tarczy Grove](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="443f6-161">Czujnik temperatury Użyj Grove kabel tooconnect Grove na powitania Grove Base tarczy **A0** portu.</span><span class="sxs-lookup"><span data-stu-id="443f6-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Połącz czujnik tootemperature](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Edison i czujnik połączenia](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="443f6-164">Teraz z czujnika jest gotowa.</span><span class="sxs-lookup"><span data-stu-id="443f6-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="443f6-165">Włącz Edison</span><span class="sxs-lookup"><span data-stu-id="443f6-165">Power up Edison</span></span>

1. <span data-ttu-id="443f6-166">Dołącz hello zasilania.</span><span class="sxs-lookup"><span data-stu-id="443f6-166">Plug in hello power supply.</span></span>

   ![Podłącz zasilacz](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="443f6-168">Zielona LED (oznaczony DS1 na powitania karty rozszerzeń Arduino *) powinien podświetlony i pozostać podświetlone.</span><span class="sxs-lookup"><span data-stu-id="443f6-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="443f6-169">Poczekaj na jedną minutę na powitania tablicy toofinish rozruch.</span><span class="sxs-lookup"><span data-stu-id="443f6-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="443f6-170">Jeśli nie masz zasilacz kontrolera domeny, można nadal zasilania hello tablicy za pośrednictwem portu USB.</span><span class="sxs-lookup"><span data-stu-id="443f6-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="443f6-171">Zobacz `Connect Edison tooyour computer` sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="443f6-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="443f6-172">Włączanie tablicy w ten sposób może spowodować nieprzewidywalne zachowanie z tablicy, szczególnie w przypadku, gdy przy użyciu sieci Wi-Fi lub zwiększają motors.</span><span class="sxs-lookup"><span data-stu-id="443f6-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="443f6-173">Podłącz komputer tooyour Edison</span><span class="sxs-lookup"><span data-stu-id="443f6-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="443f6-174">Przełącz dół mikroprzełącznika hello kierunku Witaj dwie micro portów USB, dzięki czemu Edison jest w trybie urządzenia.</span><span class="sxs-lookup"><span data-stu-id="443f6-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="443f6-175">Różnice między trybu urządzenia ani hosta, odwołanie [tutaj](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="443f6-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Przełącz mikroprzełącznika hello w dół](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="443f6-177">Podłącz kabel USB micro hello do portu USB micro najwyższego hello.</span><span class="sxs-lookup"><span data-stu-id="443f6-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Górny micro portu USB](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="443f6-179">Plug hello drugiej, kabel USB do komputera.</span><span class="sxs-lookup"><span data-stu-id="443f6-179">Plug hello other end of USB cable into your computer.</span></span>

   ![Komputer USB](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="443f6-181">Będzie wiadomo, że tablicy jest w pełni zainicjowany, gdy komputer instaluje nowy dysk (podobne jak w przypadku Wstawianie karta SD do komputera).</span><span class="sxs-lookup"><span data-stu-id="443f6-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="443f6-182">Pobierz i uruchom narzędzie konfiguracji hello</span><span class="sxs-lookup"><span data-stu-id="443f6-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="443f6-183">Pobierz najnowsze narzędzia konfiguracji hello z [to łącze](https://software.intel.com/en-us/iot/hardware/edison/downloads) kategorii hello `Installers` nagłówka.</span><span class="sxs-lookup"><span data-stu-id="443f6-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="443f6-184">Wykonaj hello narzędzia i postępuj zgodnie z jego na ekranie instrukcjami, klikając przycisk Dalej, w razie potrzeby</span><span class="sxs-lookup"><span data-stu-id="443f6-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="443f6-185">Oprogramowanie układowe Flash</span><span class="sxs-lookup"><span data-stu-id="443f6-185">Flash firmware</span></span>
1. <span data-ttu-id="443f6-186">Na powitania `Set up options` kliknij `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="443f6-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="443f6-187">Wybierz hello tooflash obrazu na tablicy, wykonując jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="443f6-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="443f6-188">toodownload i flash tablicy o hello najnowszego oprogramowania układowego obraz dostępne z firmy Intel, wybierz `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="443f6-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="443f6-189">Wybierz tablicy z obrazem, który został zapisany już na komputerze, tooflash `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="443f6-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="443f6-190">Przeglądaj tooand hello wybierz obraz ma tooflash tooyour tablicy.</span><span class="sxs-lookup"><span data-stu-id="443f6-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="443f6-191">Narzędzie Instalatora Hello podejmie tooflash tablicy.</span><span class="sxs-lookup"><span data-stu-id="443f6-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="443f6-192">cały proces miga Hello może trwać too10 minut.</span><span class="sxs-lookup"><span data-stu-id="443f6-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="443f6-193">Ustaw hasło</span><span class="sxs-lookup"><span data-stu-id="443f6-193">Set password</span></span>
1. <span data-ttu-id="443f6-194">Na powitania `Set up options` kliknij `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="443f6-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="443f6-195">Można ustawić niestandardową nazwę tablicy Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="443f6-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="443f6-196">Jest to opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="443f6-196">This is optional.</span></span>
3. <span data-ttu-id="443f6-197">Wpisz hasło do tablicy, a następnie kliknij przycisk `Set password`.</span><span class="sxs-lookup"><span data-stu-id="443f6-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="443f6-198">Oznacz hello hasła, które jest później używany w dół.</span><span class="sxs-lookup"><span data-stu-id="443f6-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="443f6-199">Połączenia sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="443f6-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="443f6-200">Na powitania `Set up options` kliknij `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="443f6-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="443f6-201">Poczekaj zapasowej minutę tooone jako użytkownika skanowania komputera dostępnych sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="443f6-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="443f6-202">Z hello `Detected Networks` listy rozwijanej wybierz sieci.</span><span class="sxs-lookup"><span data-stu-id="443f6-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="443f6-203">Z hello `Security` listy rozwijanej, wybierz hello sieci typu zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="443f6-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="443f6-204">Udostępnić informacje logowania i hasło, a następnie kliknij przycisk `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="443f6-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="443f6-205">Oznacz dół hello adres IP, który jest później używany.</span><span class="sxs-lookup"><span data-stu-id="443f6-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="443f6-206">Upewnij się, że Edison jest połączonych toohello sam sieci jako komputera.</span><span class="sxs-lookup"><span data-stu-id="443f6-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="443f6-207">Komputer łączy tooyour Edison przy użyciu adresu IP hello.</span><span class="sxs-lookup"><span data-stu-id="443f6-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Połącz czujnik tootemperature](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="443f6-209">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="443f6-209">Congratulations!</span></span> <span data-ttu-id="443f6-210">Pomyślnie skonfigurowano Edison.</span><span class="sxs-lookup"><span data-stu-id="443f6-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="443f6-211">Uruchom przykładową aplikację na Intel Edison</span><span class="sxs-lookup"><span data-stu-id="443f6-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="443f6-212">Przygotowanie hello SDK urządzenia IoT Azure</span><span class="sxs-lookup"><span data-stu-id="443f6-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="443f6-213">Użyj jednej z poniższych klientów SSH z tooyour tooconnect Twojego hosta komputera Intel Edison hello.</span><span class="sxs-lookup"><span data-stu-id="443f6-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="443f6-214">adres IP Hello jest z narzędzia do konfiguracji hello oraz hasło hello jest hello jedną ustawione w tym narzędziu.</span><span class="sxs-lookup"><span data-stu-id="443f6-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="443f6-215">[PuTTY](http://www.putty.org/) dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="443f6-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="443f6-216">Witaj wbudowanego klienta SSH Ubuntu lub macOS.</span><span class="sxs-lookup"><span data-stu-id="443f6-216">hello built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="443f6-217">Klonowanie hello przykładowej aplikacji tooyour urządzenia klienckiego.</span><span class="sxs-lookup"><span data-stu-id="443f6-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="443f6-218">Następnie przejdź toohello repozytorium folder toorun hello następujące polecenia tooinstall wszystkich pakietów, może upłynąć lek zagrażający toocomplete minut.</span><span class="sxs-lookup"><span data-stu-id="443f6-218">Then navigate toohello repo folder toorun hello following command tooinstall all packages, it may take serval minutes toocomplete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a><span data-ttu-id="443f6-219">Konfigurowanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="443f6-219">Configure and run hello sample application</span></span>

1. <span data-ttu-id="443f6-220">Otwórz plik konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="443f6-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Plik konfiguracji](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="443f6-222">Istnieją dwa makra w tym pliku mogą configurate.</span><span class="sxs-lookup"><span data-stu-id="443f6-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="443f6-223">Witaj najpierw jest `INTERVAL`, który definiuje dwa komunikaty, które wysyłają toocloud hello interwału.</span><span class="sxs-lookup"><span data-stu-id="443f6-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="443f6-224">Witaj drugi `simulatedData`, czyli wartość logiczną parametru czy toouse symulowane dane czujników, czy nie.</span><span class="sxs-lookup"><span data-stu-id="443f6-224">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="443f6-225">Jeśli użytkownik **nie ma czujnik hello**Ustaw hello `simulatedData` wartość zbyt`true` toomake hello przykładowej aplikacji tworzenia i używania danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="443f6-225">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="443f6-226">Zapisz i zamknij naciskając formantu O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="443f6-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="443f6-227">Uruchom aplikację przykładową hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="443f6-227">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="443f6-228">Upewnij się, możesz kopiowania i wklejania ciąg połączenia urządzenia hello w apostrofy hello.</span><span class="sxs-lookup"><span data-stu-id="443f6-228">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="443f6-229">Powinien pojawić się następujące hello output, że pokazuje hello wiadomości powitania i danych czujnika, które są wysyłane tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="443f6-229">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Dane wyjściowe — dane czujników wysyłane z Centrum IoT tooyour Intel Edison](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="443f6-231">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="443f6-231">Next steps</span></span>

<span data-ttu-id="443f6-232">Uruchomiono przykładowych danych czujnika toocollect aplikacji i wysyłać je tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="443f6-232">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
