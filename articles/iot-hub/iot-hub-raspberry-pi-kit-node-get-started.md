---
title: "aaaRaspberry Pi toocloud (Node.js) - Połącz Pi malina tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz Pi malina tooAzure Centrum IoT platformy Pi malina toosend danych toohello chmury Azure w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot malinowe pi malinowe pi iot hub malinowe pi wysyłania danych toocloud malinowe pi toocloud"
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57a15ab3984021a9c18ff0aa1316a4d4c6ebdec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a><span data-ttu-id="e8b79-104">Połącz tooAzure Pi malina Centrum IoT (Node.js)</span><span class="sxs-lookup"><span data-stu-id="e8b79-104">Connect Raspberry Pi tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="e8b79-105">W tym samouczku Rozpocznij od uczenia hello podstawowe informacje dotyczące pracy z Pi malina, który działa Raspbian.</span><span class="sxs-lookup"><span data-stu-id="e8b79-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="e8b79-106">Następnie dowiesz się, jak połączyć tooseamlessly chmury toohello urządzeń przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="e8b79-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="e8b79-107">Dla przykładów Windows 10 IoT Core Przejdź toohello [Centrum deweloperów systemu Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="e8b79-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="e8b79-108">Nie masz jeszcze zestawu?</span><span class="sxs-lookup"><span data-stu-id="e8b79-108">Don't have a kit yet?</span></span> <span data-ttu-id="e8b79-109">Spróbuj [symulatora online Pi malina](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e8b79-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="e8b79-110">Lub kupowanie nowej kit [tutaj](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="e8b79-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>


## <a name="what-you-do"></a><span data-ttu-id="e8b79-111">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="e8b79-111">What you do</span></span>

* <span data-ttu-id="e8b79-112">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e8b79-112">Create an IoT hub.</span></span>
* <span data-ttu-id="e8b79-113">Zarejestruj urządzenie pi w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e8b79-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="e8b79-114">Instalator malinowe Pi.</span><span class="sxs-lookup"><span data-stu-id="e8b79-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="e8b79-115">Uruchom przykładową aplikację w Centrum IoT tooyour danych czujnika toosend Pi.</span><span class="sxs-lookup"><span data-stu-id="e8b79-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="e8b79-116">Połącz Centrum IoT tooan Pi malina utworzony.</span><span class="sxs-lookup"><span data-stu-id="e8b79-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="e8b79-117">Następnie możesz uruchomić przykładową aplikację na Pi toocollect temperatury i wilgotności danych z czujnika BME280.</span><span class="sxs-lookup"><span data-stu-id="e8b79-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="e8b79-118">Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.</span><span class="sxs-lookup"><span data-stu-id="e8b79-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="e8b79-119">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="e8b79-119">What you learn</span></span>

* <span data-ttu-id="e8b79-120">Jak toocreate Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e8b79-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="e8b79-121">Jak tooconnect Pi z czujnika BME280.</span><span class="sxs-lookup"><span data-stu-id="e8b79-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="e8b79-122">Jak dane czujników toocollect uruchamiając przykładową aplikację na Pi.</span><span class="sxs-lookup"><span data-stu-id="e8b79-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="e8b79-123">Jak Centrum IoT tooyour danych czujnika toosend.</span><span class="sxs-lookup"><span data-stu-id="e8b79-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e8b79-124">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="e8b79-124">What you need</span></span>

![Co jest potrzebne](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="e8b79-126">Witaj malina Pi 2 lub 3 Pi malina tablicy.</span><span class="sxs-lookup"><span data-stu-id="e8b79-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="e8b79-127">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e8b79-127">An active Azure subscription.</span></span> <span data-ttu-id="e8b79-128">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="e8b79-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="e8b79-129">Monitor, klawiatura USB i myszy łączących tooPi.</span><span class="sxs-lookup"><span data-stu-id="e8b79-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="e8b79-130">Mac lub komputer z systemem Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="e8b79-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="e8b79-131">Połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="e8b79-131">An Internet connection.</span></span>
* <span data-ttu-id="e8b79-132">16 GB lub powyżej karty microSD.</span><span class="sxs-lookup"><span data-stu-id="e8b79-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="e8b79-133">USB SD karty sieciowej lub microSD karty tooburn hello obraz systemu operacyjnego na karcie microSD hello.</span><span class="sxs-lookup"><span data-stu-id="e8b79-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="e8b79-134">5 volt potęgą 2-amp dostarczyć hello stopy 6 micro kabla USB.</span><span class="sxs-lookup"><span data-stu-id="e8b79-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="e8b79-135">Witaj, następujące elementy są opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="e8b79-135">hello following items are optional:</span></span>

* <span data-ttu-id="e8b79-136">Złożony Adafruit BME280 temperatury, wykorzystania i wilgotności czujnika.</span><span class="sxs-lookup"><span data-stu-id="e8b79-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="e8b79-137">Breadboard.</span><span class="sxs-lookup"><span data-stu-id="e8b79-137">A breadboard.</span></span>
* <span data-ttu-id="e8b79-138">6 F/M zworek przewodów.</span><span class="sxs-lookup"><span data-stu-id="e8b79-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="e8b79-139">Rozproszona LED 10 mm.</span><span class="sxs-lookup"><span data-stu-id="e8b79-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="e8b79-140">Te elementy są opcjonalne, ponieważ obsługa przykładowy kod hello symulowane danych czujnika.</span><span class="sxs-lookup"><span data-stu-id="e8b79-140">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="e8b79-141">Konfiguracja malinowe Pi</span><span class="sxs-lookup"><span data-stu-id="e8b79-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="e8b79-142">Instalowanie systemu operacyjnego Raspbian hello pi</span><span class="sxs-lookup"><span data-stu-id="e8b79-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="e8b79-143">Przygotuj karty microSD hello instalacji hello Raspbian obrazu.</span><span class="sxs-lookup"><span data-stu-id="e8b79-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="e8b79-144">Pobierz Raspbian.</span><span class="sxs-lookup"><span data-stu-id="e8b79-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="e8b79-145">[Pobierz Joasia Raspbian z pulpitem](https://www.raspberrypi.org/downloads/raspbian/) (pliku .zip hello).</span><span class="sxs-lookup"><span data-stu-id="e8b79-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="e8b79-146">Wyodrębnij hello Raspbian obrazu tooa folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="e8b79-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="e8b79-147">Instalowanie karty microSD toohello Raspbian.</span><span class="sxs-lookup"><span data-stu-id="e8b79-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="e8b79-148">[Pobierz i zainstaluj narzędzie palnika karty Etcher SD hello](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="e8b79-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="e8b79-149">Uruchom Etcher i wybierz hello Raspbian obrazu, który został wyodrębniony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="e8b79-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="e8b79-150">Wybierz dysk karty microSD hello.</span><span class="sxs-lookup"><span data-stu-id="e8b79-150">Select hello microSD card drive.</span></span> <span data-ttu-id="e8b79-151">Należy pamiętać, że Etcher może już wybrane hello poprawnego dysku.</span><span class="sxs-lookup"><span data-stu-id="e8b79-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="e8b79-152">Kliknij kartę microSD toohello Raspbian Flash tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e8b79-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="e8b79-153">Karta microSD hello należy usunąć z komputera po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="e8b79-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="e8b79-154">Jest karta microSD hello bezpieczne tooremove bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karta microSD powitania po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="e8b79-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="e8b79-155">Włóż kartę microSD hello do Pi.</span><span class="sxs-lookup"><span data-stu-id="e8b79-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="e8b79-156">Włącz SSH i I2C</span><span class="sxs-lookup"><span data-stu-id="e8b79-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="e8b79-157">Połącz Pi toohello monitora, klawiatury i myszy, uruchom Pi, a następnie zaloguj Raspbian przy użyciu `pi` hello nazwy użytkownika i `raspberry` jako hello hasła.</span><span class="sxs-lookup"><span data-stu-id="e8b79-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="e8b79-158">Kliknij ikonę malinowe hello > **preferencje** > **malina Pi konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="e8b79-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Witaj Raspbian preferencji menu](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="e8b79-160">Na powitania **interfejsów** ustaw **I2C** i **SSH** za**włączyć**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8b79-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="e8b79-161">Jeśli nie masz fizycznych czujników i danych czujnika toouse symulowane, ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="e8b79-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Włącz I2C i SSH na malinowe Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="e8b79-163">tooenable SSH i I2C można znaleźć więcej dokumentacji na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) i [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="e8b79-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="e8b79-164">Połącz hello czujnik tooPi</span><span class="sxs-lookup"><span data-stu-id="e8b79-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="e8b79-165">Użyj hello breadboard i zworek przewodów tooconnect LED i BME280 tooPi.</span><span class="sxs-lookup"><span data-stu-id="e8b79-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="e8b79-166">Jeśli nie masz czujnik hello [pominąć tę sekcję](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="e8b79-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Witaj Pi malina i czujnik połączenia](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="e8b79-168">Czujnik Hello BME280 może zbierać dane temperatury i wilgotności.</span><span class="sxs-lookup"><span data-stu-id="e8b79-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="e8b79-169">I hello LED będzie blink w przypadku komunikacji między urządzenia i hello chmury.</span><span class="sxs-lookup"><span data-stu-id="e8b79-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="e8b79-170">Czujnik numery PIN użyć hello następujących połączeń:</span><span class="sxs-lookup"><span data-stu-id="e8b79-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="e8b79-171">Uruchom (czujnik & LED)</span><span class="sxs-lookup"><span data-stu-id="e8b79-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="e8b79-172">Końcowy (tablica)</span><span class="sxs-lookup"><span data-stu-id="e8b79-172">End (Board)</span></span>            | <span data-ttu-id="e8b79-173">Kolor kabel</span><span class="sxs-lookup"><span data-stu-id="e8b79-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="e8b79-174">VDD (Pin: 5 GB/S)</span><span class="sxs-lookup"><span data-stu-id="e8b79-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="e8b79-175">3, 3V PWR (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="e8b79-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="e8b79-176">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="e8b79-176">White cable</span></span>   |
| <span data-ttu-id="e8b79-177">GND (Pin 7 GB/S)</span><span class="sxs-lookup"><span data-stu-id="e8b79-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="e8b79-178">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="e8b79-178">GND (Pin 6)</span></span>            | <span data-ttu-id="e8b79-179">Brązowy kabel</span><span class="sxs-lookup"><span data-stu-id="e8b79-179">Brown cable</span></span>   |
| <span data-ttu-id="e8b79-180">SDI (Pin 10 GB/S)</span><span class="sxs-lookup"><span data-stu-id="e8b79-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="e8b79-181">I2C1 SDA (Pin 3)</span><span class="sxs-lookup"><span data-stu-id="e8b79-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="e8b79-182">Czerwony kabel</span><span class="sxs-lookup"><span data-stu-id="e8b79-182">Red cable</span></span>     |
| <span data-ttu-id="e8b79-183">SCK (Pin 8 GB/S)</span><span class="sxs-lookup"><span data-stu-id="e8b79-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="e8b79-184">I2C1 SCL (Pin 5)</span><span class="sxs-lookup"><span data-stu-id="e8b79-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="e8b79-185">Kabel pomarańczowy</span><span class="sxs-lookup"><span data-stu-id="e8b79-185">Orange cable</span></span>  |
| <span data-ttu-id="e8b79-186">VDD LED (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="e8b79-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="e8b79-187">Interfejs GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="e8b79-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="e8b79-188">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="e8b79-188">White cable</span></span>   |
| <span data-ttu-id="e8b79-189">GND LED (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="e8b79-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="e8b79-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="e8b79-190">GND (Pin 20)</span></span>           | <span data-ttu-id="e8b79-191">Czarne kabel</span><span class="sxs-lookup"><span data-stu-id="e8b79-191">Black cable</span></span>   |

<span data-ttu-id="e8b79-192">Kliknij przycisk tooview [malina Pi 2 i 3 mapowania kodu Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) użytkownikowi.</span><span class="sxs-lookup"><span data-stu-id="e8b79-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="e8b79-193">Po nawiązaniu połączenia pomyślnie tooyour BME280 Pi malina, należy go jak poniżej obrazu.</span><span class="sxs-lookup"><span data-stu-id="e8b79-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi połączonych i BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="e8b79-195">Łączenie z siecią toohello Pi</span><span class="sxs-lookup"><span data-stu-id="e8b79-195">Connect Pi toohello network</span></span>

<span data-ttu-id="e8b79-196">Włącz Pi przy użyciu kabla USB micro hello i hello zasilania.</span><span class="sxs-lookup"><span data-stu-id="e8b79-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="e8b79-197">Użyj hello Ethernet kabel tooconnect Pi tooyour przewodowej sieci lub wykonaj hello [instrukcji hello Foundation Pi malina](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect sieci bezprzewodowej tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="e8b79-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="e8b79-198">Po Twoje Pi został pomyślnie połączono toohello sieci, należy tootake wiadomości powitania [adres IP Twojego Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="e8b79-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Toowired połączonych sieci](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="e8b79-200">Upewnij się, że Pi jest połączonych toohello sam sieci jako komputera.</span><span class="sxs-lookup"><span data-stu-id="e8b79-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="e8b79-201">Na przykład, jeśli komputer jest połączony tooa sieci bezprzewodowej podczas Pi jest połączonych tooa ich z przewodową siecią, może nie być wyświetlana hello IP adres hello devdisco w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="e8b79-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="e8b79-202">Uruchom przykładową aplikację na Pi</span><span class="sxs-lookup"><span data-stu-id="e8b79-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a><span data-ttu-id="e8b79-203">Sklonuj przykładową aplikację i zainstalować wstępnie wymagane pakiety hello</span><span class="sxs-lookup"><span data-stu-id="e8b79-203">Clone sample application and install hello prerequisite packages</span></span>

1. <span data-ttu-id="e8b79-204">Użyj jednej z hello poniższych klientów SSH z tooyour tooconnect Pi malina Twojego hosta komputera.</span><span class="sxs-lookup"><span data-stu-id="e8b79-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="e8b79-205">**Użytkownicy systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="e8b79-205">**Windows Users**</span></span>
   1. <span data-ttu-id="e8b79-206">Pobierz i zainstaluj [PuTTY](http://www.putty.org/) dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="e8b79-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="e8b79-207">Skopiuj adres IP hello sekcji Pi do hello hosta nazwę (lub adres IP) i wybierz SSH jako hello typu połączenia.</span><span class="sxs-lookup"><span data-stu-id="e8b79-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   ![Programu puTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="e8b79-209">**Mac i Ubuntu użytkowników**</span><span class="sxs-lookup"><span data-stu-id="e8b79-209">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="e8b79-210">Przy użyciu wbudowanego klienta SSH hello na Ubuntu lub macOS.</span><span class="sxs-lookup"><span data-stu-id="e8b79-210">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="e8b79-211">Może być konieczne toorun `ssh pi@<ip address of pi>` tooconnect Pi za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="e8b79-211">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="e8b79-212">Witaj domyślna nazwa użytkownika to `pi` , a hasło hello jest `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="e8b79-212">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="e8b79-213">Zainstaluj środowisko Node.js i NPM tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="e8b79-213">Install Node.js and NPM tooyour Pi.</span></span>
   
   <span data-ttu-id="e8b79-214">Najpierw należy sprawdzić środowisko Node.js w wersji z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="e8b79-214">First you should check your Node.js version with hello following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="e8b79-215">Jeśli wersja hello jest starsza niż 4.x lub nie nie Node.js na Twoje Pi, uruchom następujące polecenie tooinstall hello, lub zaktualizuj Node.js.</span><span class="sxs-lookup"><span data-stu-id="e8b79-215">If hello version is lower than 4.x or there is no Node.js on your Pi, then run hello following command tooinstall or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="e8b79-216">Klonowanie hello przykładowej aplikacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e8b79-216">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="e8b79-217">Zainstaluj wszystkie pakiety za hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="e8b79-217">Install all packages by hello following command.</span></span> <span data-ttu-id="e8b79-218">Zawiera urządzenia Azure IoT SDK, czujnik BME280 biblioteki i Biblioteka dołączenie Pi.</span><span class="sxs-lookup"><span data-stu-id="e8b79-218">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="e8b79-219">Może upłynąć kilka minut toofinish tego procesu instalacji, w zależności od połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="e8b79-219">It might take several minutes toofinish this installation process depending on your network connection.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="e8b79-220">Skonfiguruj hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e8b79-220">Configure hello sample application</span></span>

1. <span data-ttu-id="e8b79-221">Otwórz plik konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e8b79-221">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Plik konfiguracji](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="e8b79-223">Istnieją dwa elementy w tym pliku mogą configurate.</span><span class="sxs-lookup"><span data-stu-id="e8b79-223">There are two items in this file you can configurate.</span></span> <span data-ttu-id="e8b79-224">Witaj najpierw jest `interval`, który definiuje hello interwał (w milisekundach) między dwa komunikaty, które wysyłają toocloud.</span><span class="sxs-lookup"><span data-stu-id="e8b79-224">hello first one is `interval`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="e8b79-225">Witaj drugi `simulatedData`, czyli wartość logiczną parametru czy toouse symulowane dane czujników, czy nie.</span><span class="sxs-lookup"><span data-stu-id="e8b79-225">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="e8b79-226">Jeśli użytkownik **nie ma czujnik hello**Ustaw hello `simulatedData` wartość zbyt`true` toomake hello przykładowej aplikacji tworzenia i używania danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="e8b79-226">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="e8b79-227">Zapisz i zamknij naciskając formantu O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="e8b79-227">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="e8b79-228">Uruchom hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e8b79-228">Run hello sample application</span></span>

<span data-ttu-id="e8b79-229">Uruchom aplikację przykładową hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e8b79-229">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="e8b79-230">Upewnij się, możesz kopiowania i wklejania ciąg połączenia urządzenia hello w apostrofy hello.</span><span class="sxs-lookup"><span data-stu-id="e8b79-230">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="e8b79-231">Powinien pojawić się następujące hello output, że pokazuje hello wiadomości powitania i danych czujnika, które są wysyłane tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e8b79-231">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Dane wyjściowe - wysyłane z Centrum IoT tooyour Pi malina dane czujników](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="e8b79-233">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8b79-233">Next steps</span></span>

<span data-ttu-id="e8b79-234">Uruchomiono przykładowych danych czujnika toocollect aplikacji i wysyłać je tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e8b79-234">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="e8b79-235">wiadomości powitania toosee Twojego Pi malina został wysłany tooyour IoT hub lub wysyłania wiadomości tooyour Pi malina za pomocą interfejsu wiersza polecenia, zobacz hello [Zarządzaj chmury urządzenia wiadomości z Centrum iothub explorer samouczek](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="e8b79-235">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
