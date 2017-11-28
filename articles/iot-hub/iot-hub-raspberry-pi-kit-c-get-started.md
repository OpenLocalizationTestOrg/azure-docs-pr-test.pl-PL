---
title: "aaaRaspberry Pi toocloud (C) - Połącz Pi malina tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz Pi malina tooAzure Centrum IoT platformy Pi malina toosend danych toohello chmury Azure w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot malinowe pi malinowe pi iot hub malinowe pi wysyłania danych toocloud malinowe pi toocloud"
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a><span data-ttu-id="0c3d8-104">Połącz Pi malina tooAzure IoT Hub (C)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-104">Connect Raspberry Pi tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="0c3d8-105">W tym samouczku Rozpocznij od uczenia hello podstawowe informacje dotyczące pracy z Pi malina, który działa Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="0c3d8-106">Następnie dowiesz się, jak połączyć tooseamlessly chmury toohello urządzeń przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="0c3d8-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="0c3d8-107">Dla przykładów Windows 10 IoT Core Przejdź toohello [Centrum deweloperów systemu Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="0c3d8-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="0c3d8-108">Nie masz jeszcze zestawu?</span><span class="sxs-lookup"><span data-stu-id="0c3d8-108">Don't have a kit yet?</span></span> <span data-ttu-id="0c3d8-109">Spróbuj [symulatora online Pi malina](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0c3d8-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="0c3d8-110">Lub kupowanie nowej kit [tutaj](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="0c3d8-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="0c3d8-111">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="0c3d8-111">What you do</span></span>

* <span data-ttu-id="0c3d8-112">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-112">Create an IoT hub.</span></span>
* <span data-ttu-id="0c3d8-113">Zarejestruj urządzenie pi w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="0c3d8-114">Instalator malinowe Pi.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="0c3d8-115">Uruchom przykładową aplikację w Centrum IoT tooyour danych czujnika toosend Pi.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="0c3d8-116">Połącz Centrum IoT tooan Pi malina utworzony.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="0c3d8-117">Następnie możesz uruchomić przykładową aplikację na Pi toocollect temperatury i wilgotności danych z czujnika BME280.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="0c3d8-118">Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="0c3d8-119">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="0c3d8-119">What you learn</span></span>

* <span data-ttu-id="0c3d8-120">Jak toocreate Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="0c3d8-121">Jak tooconnect Pi z czujnika BME280.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="0c3d8-122">Jak dane czujników toocollect uruchamiając przykładową aplikację na Pi.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="0c3d8-123">Jak Centrum IoT tooyour danych czujnika toosend.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0c3d8-124">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="0c3d8-124">What you need</span></span>

![Co jest potrzebne](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="0c3d8-126">Witaj malina Pi 2 lub 3 Pi malina tablicy.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="0c3d8-127">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-127">An active Azure subscription.</span></span> <span data-ttu-id="0c3d8-128">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="0c3d8-129">Monitor, klawiatura USB i myszy łączących tooPi.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="0c3d8-130">Mac lub komputer z systemem Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="0c3d8-131">Połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-131">An Internet connection.</span></span>
* <span data-ttu-id="0c3d8-132">16 GB lub powyżej karty microSD.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="0c3d8-133">USB SD karty sieciowej lub microSD karty tooburn hello obraz systemu operacyjnego na karcie microSD hello.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="0c3d8-134">5 volt potęgą 2-amp dostarczyć hello stopy 6 micro kabla USB.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="0c3d8-135">Witaj, następujące elementy są opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="0c3d8-135">hello following items are optional:</span></span>

* <span data-ttu-id="0c3d8-136">Złożony Adafruit BME280 temperatury, wykorzystania i wilgotności czujnika.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="0c3d8-137">Breadboard.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-137">A breadboard.</span></span>
* <span data-ttu-id="0c3d8-138">6 F/M zworek przewodów.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="0c3d8-139">Rozproszona LED 10 mm.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="0c3d8-140">Te elementy są opcjonalne, ponieważ obsługa przykładowy kod hello symulowane danych czujnika.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="0c3d8-141">Konfiguracja malinowe Pi</span><span class="sxs-lookup"><span data-stu-id="0c3d8-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="0c3d8-142">Instalowanie systemu operacyjnego Raspbian hello pi</span><span class="sxs-lookup"><span data-stu-id="0c3d8-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="0c3d8-143">Przygotuj karty microSD hello instalacji hello Raspbian obrazu.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="0c3d8-144">Pobierz Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="0c3d8-145">[Pobierz Joasia Raspbian z pulpitem](https://www.raspberrypi.org/downloads/raspbian/) (pliku .zip hello).</span><span class="sxs-lookup"><span data-stu-id="0c3d8-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="0c3d8-146">Wyodrębnij hello Raspbian obrazu tooa folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="0c3d8-147">Instalowanie karty microSD toohello Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="0c3d8-148">[Pobierz i zainstaluj narzędzie palnika karty Etcher SD hello](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="0c3d8-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="0c3d8-149">Uruchom Etcher i wybierz hello Raspbian obrazu, który został wyodrębniony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="0c3d8-150">Wybierz dysk karty microSD hello.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-150">Select hello microSD card drive.</span></span> <span data-ttu-id="0c3d8-151">Należy pamiętać, że Etcher może już wybrane hello poprawnego dysku.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="0c3d8-152">Kliknij kartę microSD toohello Raspbian Flash tooinstall.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="0c3d8-153">Karta microSD hello należy usunąć z komputera po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="0c3d8-154">Jest karta microSD hello bezpieczne tooremove bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karta microSD powitania po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="0c3d8-155">Włóż kartę microSD hello do Pi.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-spi"></a><span data-ttu-id="0c3d8-156">Włącz SSH i SPI</span><span class="sxs-lookup"><span data-stu-id="0c3d8-156">Enable SSH and SPI</span></span>

1. <span data-ttu-id="0c3d8-157">Połącz Pi toohello monitora, klawiatury i myszy, uruchom Pi, a następnie zaloguj Raspbian przy użyciu `pi` hello nazwy użytkownika i `raspberry` jako hello hasła.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="0c3d8-158">Kliknij ikonę malinowe hello > **preferencje** > **malina Pi konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Witaj Raspbian preferencji menu](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="0c3d8-160">Na powitania **interfejsów** ustaw **SPI** i **SSH** za**włączyć**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-160">On hello **Interfaces** tab, set **SPI** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="0c3d8-161">Jeśli nie masz fizycznych czujników i danych czujnika toouse symulowane, ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Włącz SPI i SSH na malinowe Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="0c3d8-163">tooenable SSH i SPI, można znaleźć więcej dokumentacji na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) i [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="0c3d8-163">tooenable SSH and SPI, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="0c3d8-164">Połącz hello czujnik tooPi</span><span class="sxs-lookup"><span data-stu-id="0c3d8-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="0c3d8-165">Użyj hello breadboard i zworek przewodów tooconnect LED i BME280 tooPi.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="0c3d8-166">Jeśli nie masz czujnik hello [pominąć tę sekcję](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="0c3d8-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Witaj Pi malina i czujnik połączenia](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="0c3d8-168">Czujnik Hello BME280 może zbierać dane temperatury i wilgotności.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="0c3d8-169">I hello LED będzie blink w przypadku komunikacji między urządzenia i hello chmury.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="0c3d8-170">Czujnik numery PIN użyć hello następujących połączeń:</span><span class="sxs-lookup"><span data-stu-id="0c3d8-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="0c3d8-171">Uruchom (czujnik & LED)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="0c3d8-172">Końcowy (tablica)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-172">End (Board)</span></span>            | <span data-ttu-id="0c3d8-173">Kolor kabel</span><span class="sxs-lookup"><span data-stu-id="0c3d8-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="0c3d8-174">VDD LED (Pin: 5 GB/S)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-174">LED VDD (Pin 5G)</span></span>         | <span data-ttu-id="0c3d8-175">Interfejs GPIO 4 (Pin 7)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-175">GPIO 4 (Pin 7)</span></span>         | <span data-ttu-id="0c3d8-176">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="0c3d8-176">White cable</span></span>   |
| <span data-ttu-id="0c3d8-177">GND LED (Pin 6 GB/S)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-177">LED GND (Pin 6G)</span></span>         | <span data-ttu-id="0c3d8-178">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-178">GND (Pin 6)</span></span>            | <span data-ttu-id="0c3d8-179">Czarne kabel</span><span class="sxs-lookup"><span data-stu-id="0c3d8-179">Black cable</span></span>   |
| <span data-ttu-id="0c3d8-180">VDD (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-180">VDD (Pin 18F)</span></span>            | <span data-ttu-id="0c3d8-181">3, 3V PWR (Pin 17)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-181">3.3V PWR (Pin 17)</span></span>      | <span data-ttu-id="0c3d8-182">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="0c3d8-182">White cable</span></span>   |
| <span data-ttu-id="0c3d8-183">GND (Pin 20F)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-183">GND (Pin 20F)</span></span>            | <span data-ttu-id="0c3d8-184">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-184">GND (Pin 20)</span></span>           | <span data-ttu-id="0c3d8-185">Czarne kabel</span><span class="sxs-lookup"><span data-stu-id="0c3d8-185">Black cable</span></span>   |
| <span data-ttu-id="0c3d8-186">SCK (Pin 21F)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-186">SCK (Pin 21F)</span></span>            | <span data-ttu-id="0c3d8-187">SPI0 SCLK (Pin 23)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-187">SPI0 SCLK (Pin 23)</span></span>     | <span data-ttu-id="0c3d8-188">Kabel pomarańczowy</span><span class="sxs-lookup"><span data-stu-id="0c3d8-188">Orange cable</span></span>  |
| <span data-ttu-id="0c3d8-189">SDO (Pin 22F)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-189">SDO (Pin 22F)</span></span>            | <span data-ttu-id="0c3d8-190">SPI0 MISO (Pin 21)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-190">SPI0 MISO (Pin 21)</span></span>     | <span data-ttu-id="0c3d8-191">Żółty kabel</span><span class="sxs-lookup"><span data-stu-id="0c3d8-191">Yellow cable</span></span>  |
| <span data-ttu-id="0c3d8-192">SDI (Pin 23F)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-192">SDI (Pin 23F)</span></span>            | <span data-ttu-id="0c3d8-193">SPI0 MOSI (Pin 19)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-193">SPI0 MOSI (Pin 19)</span></span>     | <span data-ttu-id="0c3d8-194">Zielony kabel</span><span class="sxs-lookup"><span data-stu-id="0c3d8-194">Green cable</span></span>   |
| <span data-ttu-id="0c3d8-195">CS (Pin 24F)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-195">CS (Pin 24F)</span></span>             | <span data-ttu-id="0c3d8-196">SPI0 CS (Pin 24)</span><span class="sxs-lookup"><span data-stu-id="0c3d8-196">SPI0 CS (Pin 24)</span></span>       | <span data-ttu-id="0c3d8-197">Niebieski kabel</span><span class="sxs-lookup"><span data-stu-id="0c3d8-197">Blue cable</span></span>    |

<span data-ttu-id="0c3d8-198">Kliknij przycisk tooview [malina Pi 2 i 3 mapowania kodu Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) użytkownikowi.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-198">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="0c3d8-199">Po nawiązaniu połączenia pomyślnie tooyour BME280 Pi malina, należy go jak poniżej obrazu.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-199">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi połączonych i BME280](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="0c3d8-201">Łączenie z siecią toohello Pi</span><span class="sxs-lookup"><span data-stu-id="0c3d8-201">Connect Pi toohello network</span></span>

<span data-ttu-id="0c3d8-202">Włącz Pi przy użyciu kabla USB micro hello i hello zasilania.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-202">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="0c3d8-203">Użyj hello Ethernet kabel tooconnect Pi tooyour przewodowej sieci lub wykonaj hello [instrukcji hello Foundation Pi malina](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect sieci bezprzewodowej tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-203">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="0c3d8-204">Po Twoje Pi został pomyślnie połączono toohello sieci, należy tootake wiadomości powitania [adres IP Twojego Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="0c3d8-204">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Toowired połączonych sieci](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="0c3d8-206">Uruchom przykładową aplikację na Pi</span><span class="sxs-lookup"><span data-stu-id="0c3d8-206">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="0c3d8-207">Zainstaluj wstępnie wymagane pakiety hello</span><span class="sxs-lookup"><span data-stu-id="0c3d8-207">Install hello prerequisite packages</span></span>

1. <span data-ttu-id="0c3d8-208">Użyj jednej z hello poniższych klientów SSH z tooyour tooconnect Pi malina Twojego hosta komputera.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-208">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="0c3d8-209">**Użytkownicy systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="0c3d8-209">**Windows Users**</span></span>
   1. <span data-ttu-id="0c3d8-210">Pobierz i zainstaluj [PuTTY](http://www.putty.org/) dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-210">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="0c3d8-211">Skopiuj adres IP hello sekcji Pi do hello hosta nazwę (lub adres IP) i wybierz SSH jako hello typu połączenia.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-211">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![Programu puTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="0c3d8-213">**Mac i Ubuntu użytkowników**</span><span class="sxs-lookup"><span data-stu-id="0c3d8-213">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="0c3d8-214">Przy użyciu wbudowanego klienta SSH hello na Ubuntu lub macOS.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-214">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="0c3d8-215">Może być konieczne toorun `ssh pi@<ip address of pi>` tooconnect Pi za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-215">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="0c3d8-216">Witaj domyślna nazwa użytkownika to `pi` , a hasło hello jest `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-216">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="0c3d8-217">Instalowanie wymagań wstępnych pakietów hello hello zestawu SDK usługi Microsoft Azure IoT urządzenia C i Cmake, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="0c3d8-217">Install hello prerequisite packages for hello Microsoft Azure IoT Device SDK for C and Cmake by running hello following commands:</span></span>

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-hello-sample-application"></a><span data-ttu-id="0c3d8-218">Skonfiguruj hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="0c3d8-218">Configure hello sample application</span></span>

1. <span data-ttu-id="0c3d8-219">Klonowanie hello przykładowej aplikacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0c3d8-219">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. <span data-ttu-id="0c3d8-220">Otwórz plik konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="0c3d8-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Plik konfiguracji](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   <span data-ttu-id="0c3d8-222">Istnieją dwa makra w tym pliku mogą configurate.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="0c3d8-223">Witaj najpierw jest `INTERVAL`, który definiuje hello interwał (w milisekundach) między dwa komunikaty, które wysyłają toocloud.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-223">hello first one is `INTERVAL`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="0c3d8-224">Witaj drugi `SIMULATED_DATA`, czyli wartość logiczną parametru czy toouse symulowane dane czujników, czy nie.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="0c3d8-225">Jeśli użytkownik **nie ma czujnik hello**Ustaw hello `SIMULATED_DATA` wartość zbyt`1` toomake hello przykładowej aplikacji tworzenia i używania danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="0c3d8-226">Zapisz i zamknij naciskając formantu O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="0c3d8-227">Tworzenie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="0c3d8-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="0c3d8-228">Tworzenie aplikacji przykładowej hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0c3d8-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Dane wyjściowe kompilacji](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. <span data-ttu-id="0c3d8-230">Uruchom aplikację przykładową hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0c3d8-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="0c3d8-231">Upewnij się, możesz kopiowania i wklejania ciąg połączenia urządzenia hello w apostrofy hello.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="0c3d8-232">Powinien pojawić się następujące hello output, że pokazuje hello wiadomości powitania i danych czujnika, które są wysyłane tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Dane wyjściowe - wysyłane z Centrum IoT tooyour Pi malina dane czujników](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="0c3d8-234">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0c3d8-234">Next steps</span></span>

<span data-ttu-id="0c3d8-235">Uruchomiono przykładowych danych czujnika toocollect aplikacji i wysyłać je tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0c3d8-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="0c3d8-236">wiadomości powitania toosee Twojego Pi malina został wysłany tooyour IoT hub lub wysyłania wiadomości tooyour Pi malina za pomocą interfejsu wiersza polecenia, zobacz hello [Zarządzaj chmury urządzenia wiadomości z Centrum iothub explorer samouczek](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="0c3d8-236">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
