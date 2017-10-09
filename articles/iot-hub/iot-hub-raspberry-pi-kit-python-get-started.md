---
title: "aaaRaspberry Pi toocloud (Python) - Połącz Pi malina tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz Pi malina tooAzure Centrum IoT platformy Pi malina toosend danych toohello chmury Azure w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure iot malinowe pi malinowe pi iot hub malinowe pi wysyłania danych toocloud malinowe pi toocloud"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a><span data-ttu-id="403c3-104">Połącz tooAzure Pi malina Centrum IoT (Python)</span><span class="sxs-lookup"><span data-stu-id="403c3-104">Connect Raspberry Pi tooAzure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="403c3-105">W tym samouczku Rozpocznij od uczenia hello podstawowe informacje dotyczące pracy z Pi malina, który działa Raspbian.</span><span class="sxs-lookup"><span data-stu-id="403c3-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="403c3-106">Następnie dowiesz się, jak połączyć tooseamlessly chmury toohello urządzeń przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="403c3-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="403c3-107">Dla przykładów Windows 10 IoT Core Przejdź toohello [Centrum deweloperów systemu Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="403c3-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="403c3-108">Nie masz jeszcze zestawu?</span><span class="sxs-lookup"><span data-stu-id="403c3-108">Don't have a kit yet?</span></span> <span data-ttu-id="403c3-109">Spróbuj [symulatora online Pi malina](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="403c3-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="403c3-110">Lub kupowanie nowej kit [tutaj](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="403c3-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="403c3-111">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="403c3-111">What you do</span></span>

* <span data-ttu-id="403c3-112">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="403c3-112">Create an IoT hub.</span></span>
* <span data-ttu-id="403c3-113">Zarejestruj urządzenie pi w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="403c3-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="403c3-114">Instalator malinowe Pi.</span><span class="sxs-lookup"><span data-stu-id="403c3-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="403c3-115">Uruchom przykładową aplikację w Centrum IoT tooyour danych czujnika toosend Pi.</span><span class="sxs-lookup"><span data-stu-id="403c3-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="403c3-116">Połącz Centrum IoT tooan Pi malina utworzony.</span><span class="sxs-lookup"><span data-stu-id="403c3-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="403c3-117">Następnie możesz uruchomić przykładową aplikację na Pi toocollect temperatury i wilgotności danych z czujnika BME280.</span><span class="sxs-lookup"><span data-stu-id="403c3-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="403c3-118">Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.</span><span class="sxs-lookup"><span data-stu-id="403c3-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="403c3-119">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="403c3-119">What you learn</span></span>

* <span data-ttu-id="403c3-120">Jak toocreate Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="403c3-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="403c3-121">Jak tooconnect Pi z czujnika BME280.</span><span class="sxs-lookup"><span data-stu-id="403c3-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="403c3-122">Jak dane czujników toocollect uruchamiając przykładową aplikację na Pi.</span><span class="sxs-lookup"><span data-stu-id="403c3-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="403c3-123">Jak Centrum IoT tooyour danych czujnika toosend.</span><span class="sxs-lookup"><span data-stu-id="403c3-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="403c3-124">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="403c3-124">What you need</span></span>

![Co jest potrzebne](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="403c3-126">Witaj malina Pi 2 lub 3 Pi malina tablicy.</span><span class="sxs-lookup"><span data-stu-id="403c3-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="403c3-127">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="403c3-127">An active Azure subscription.</span></span> <span data-ttu-id="403c3-128">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="403c3-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="403c3-129">Monitor, klawiatura USB i myszy łączących tooPi.</span><span class="sxs-lookup"><span data-stu-id="403c3-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="403c3-130">Mac lub komputer z systemem Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="403c3-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="403c3-131">Połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="403c3-131">An Internet connection.</span></span>
* <span data-ttu-id="403c3-132">16 GB lub powyżej karty microSD.</span><span class="sxs-lookup"><span data-stu-id="403c3-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="403c3-133">USB SD karty sieciowej lub microSD karty tooburn hello obraz systemu operacyjnego na karcie microSD hello.</span><span class="sxs-lookup"><span data-stu-id="403c3-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="403c3-134">5 volt potęgą 2-amp dostarczyć hello stopy 6 micro kabla USB.</span><span class="sxs-lookup"><span data-stu-id="403c3-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="403c3-135">Witaj, następujące elementy są opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="403c3-135">hello following items are optional:</span></span>

* <span data-ttu-id="403c3-136">Złożony Adafruit BME280 temperatury, wykorzystania i wilgotności czujnika.</span><span class="sxs-lookup"><span data-stu-id="403c3-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="403c3-137">Breadboard.</span><span class="sxs-lookup"><span data-stu-id="403c3-137">A breadboard.</span></span>
* <span data-ttu-id="403c3-138">6 F/M zworek przewodów.</span><span class="sxs-lookup"><span data-stu-id="403c3-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="403c3-139">Rozproszona LED 10 mm.</span><span class="sxs-lookup"><span data-stu-id="403c3-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="403c3-140">Te elementy są opcjonalne, ponieważ obsługa przykładowy kod hello symulowane danych czujnika.</span><span class="sxs-lookup"><span data-stu-id="403c3-140">These items are optional because hello code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="403c3-141">Konfigurowanie Pi malina</span><span class="sxs-lookup"><span data-stu-id="403c3-141">Set up Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="403c3-142">Instalowanie systemu operacyjnego Raspbian hello pi</span><span class="sxs-lookup"><span data-stu-id="403c3-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="403c3-143">Przygotuj karty microSD hello instalacji hello Raspbian obrazu.</span><span class="sxs-lookup"><span data-stu-id="403c3-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="403c3-144">Pobierz Raspbian.</span><span class="sxs-lookup"><span data-stu-id="403c3-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="403c3-145">[Pobierz Joasia Raspbian z pulpitem](https://www.raspberrypi.org/downloads/raspbian/) (pliku .zip hello).</span><span class="sxs-lookup"><span data-stu-id="403c3-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="403c3-146">Wyodrębnij hello Raspbian obrazu tooa folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="403c3-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="403c3-147">Instalowanie karty microSD toohello Raspbian.</span><span class="sxs-lookup"><span data-stu-id="403c3-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="403c3-148">[Pobierz i zainstaluj narzędzie palnika karty Etcher SD hello](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="403c3-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="403c3-149">Uruchom Etcher i wybierz hello Raspbian obrazu, który został wyodrębniony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="403c3-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="403c3-150">Wybierz dysk karty microSD hello.</span><span class="sxs-lookup"><span data-stu-id="403c3-150">Select hello microSD card drive.</span></span> <span data-ttu-id="403c3-151">Należy pamiętać, że Etcher może już wybrane hello poprawnego dysku.</span><span class="sxs-lookup"><span data-stu-id="403c3-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="403c3-152">Kliknij kartę microSD toohello Raspbian Flash tooinstall.</span><span class="sxs-lookup"><span data-stu-id="403c3-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="403c3-153">Karta microSD hello należy usunąć z komputera po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="403c3-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="403c3-154">Jest karta microSD hello bezpieczne tooremove bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karta microSD powitania po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="403c3-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="403c3-155">Włóż kartę microSD hello do Pi.</span><span class="sxs-lookup"><span data-stu-id="403c3-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="403c3-156">Włącz SSH i I2C</span><span class="sxs-lookup"><span data-stu-id="403c3-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="403c3-157">Połącz Pi toohello monitora, klawiatury i myszy, uruchom Pi, a następnie zaloguj Raspbian przy użyciu `pi` hello nazwy użytkownika i `raspberry` jako hello hasła.</span><span class="sxs-lookup"><span data-stu-id="403c3-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="403c3-158">Kliknij ikonę malinowe hello > **preferencje** > **malina Pi konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="403c3-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Witaj Raspbian preferencji menu](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="403c3-160">Na powitania **interfejsów** ustaw **I2C** i **SSH** za**włączyć**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="403c3-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="403c3-161">Jeśli nie masz fizycznych czujników i danych czujnika toouse symulowane, ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="403c3-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Włącz I2C i SSH na malinowe Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="403c3-163">tooenable SSH i I2C można znaleźć więcej dokumentacji na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) i [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="403c3-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="403c3-164">Połącz hello czujnik tooPi</span><span class="sxs-lookup"><span data-stu-id="403c3-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="403c3-165">Użyj hello breadboard i zworek przewodów tooconnect LED i BME280 tooPi.</span><span class="sxs-lookup"><span data-stu-id="403c3-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="403c3-166">Jeśli nie masz czujnik hello [pominąć tę sekcję](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="403c3-166">If you don’t have hello sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Witaj Pi malina i czujnik połączenia](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="403c3-168">Czujnik Hello BME280 może zbierać dane temperatury i wilgotności.</span><span class="sxs-lookup"><span data-stu-id="403c3-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="403c3-169">I hello LED będzie blink w przypadku komunikacji między urządzenia i hello chmury.</span><span class="sxs-lookup"><span data-stu-id="403c3-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="403c3-170">Czujnik numery PIN użyć hello następujących połączeń:</span><span class="sxs-lookup"><span data-stu-id="403c3-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="403c3-171">Uruchom (czujnik & LED)</span><span class="sxs-lookup"><span data-stu-id="403c3-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="403c3-172">Końcowy (tablica)</span><span class="sxs-lookup"><span data-stu-id="403c3-172">End (Board)</span></span>            | <span data-ttu-id="403c3-173">Kolor kabel</span><span class="sxs-lookup"><span data-stu-id="403c3-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="403c3-174">VDD (Pin: 5 GB/S)</span><span class="sxs-lookup"><span data-stu-id="403c3-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="403c3-175">3, 3V PWR (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="403c3-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="403c3-176">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="403c3-176">White cable</span></span>   |
| <span data-ttu-id="403c3-177">GND (Pin 7 GB/S)</span><span class="sxs-lookup"><span data-stu-id="403c3-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="403c3-178">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="403c3-178">GND (Pin 6)</span></span>            | <span data-ttu-id="403c3-179">Brązowy kabel</span><span class="sxs-lookup"><span data-stu-id="403c3-179">Brown cable</span></span>   |
| <span data-ttu-id="403c3-180">SDI (Pin 10 GB/S)</span><span class="sxs-lookup"><span data-stu-id="403c3-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="403c3-181">I2C1 SDA (Pin 3)</span><span class="sxs-lookup"><span data-stu-id="403c3-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="403c3-182">Czerwony kabel</span><span class="sxs-lookup"><span data-stu-id="403c3-182">Red cable</span></span>     |
| <span data-ttu-id="403c3-183">SCK (Pin 8 GB/S)</span><span class="sxs-lookup"><span data-stu-id="403c3-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="403c3-184">I2C1 SCL (Pin 5)</span><span class="sxs-lookup"><span data-stu-id="403c3-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="403c3-185">Kabel pomarańczowy</span><span class="sxs-lookup"><span data-stu-id="403c3-185">Orange cable</span></span>  |
| <span data-ttu-id="403c3-186">VDD LED (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="403c3-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="403c3-187">Interfejs GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="403c3-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="403c3-188">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="403c3-188">White cable</span></span>   |
| <span data-ttu-id="403c3-189">GND LED (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="403c3-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="403c3-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="403c3-190">GND (Pin 20)</span></span>           | <span data-ttu-id="403c3-191">Czarne kabel</span><span class="sxs-lookup"><span data-stu-id="403c3-191">Black cable</span></span>   |

<span data-ttu-id="403c3-192">Kliknij przycisk tooview [malina Pi 2 i 3 mapowania kodu Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) użytkownikowi.</span><span class="sxs-lookup"><span data-stu-id="403c3-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="403c3-193">Po nawiązaniu połączenia pomyślnie tooyour BME280 Pi malina, należy go jak poniżej obrazu.</span><span class="sxs-lookup"><span data-stu-id="403c3-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi połączonych i BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="403c3-195">Łączenie z siecią toohello Pi</span><span class="sxs-lookup"><span data-stu-id="403c3-195">Connect Pi toohello network</span></span>

<span data-ttu-id="403c3-196">Włącz Pi przy użyciu kabla USB micro hello i hello zasilania.</span><span class="sxs-lookup"><span data-stu-id="403c3-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="403c3-197">Użyj hello Ethernet kabel tooconnect Pi tooyour przewodowej sieci lub wykonaj hello [instrukcji hello Foundation Pi malina](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect sieci bezprzewodowej tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="403c3-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="403c3-198">Po Twoje Pi został pomyślnie połączono toohello sieci, należy tootake wiadomości powitania [adres IP Twojego Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="403c3-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Toowired połączonych sieci](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="403c3-200">Upewnij się, że Pi jest połączonych toohello sam sieci jako komputera.</span><span class="sxs-lookup"><span data-stu-id="403c3-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="403c3-201">Na przykład, jeśli komputer jest połączony tooa sieci bezprzewodowej podczas Pi jest połączonych tooa ich z przewodową siecią, może nie być wyświetlana hello IP adres hello devdisco w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="403c3-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="403c3-202">Uruchom przykładową aplikację na Pi</span><span class="sxs-lookup"><span data-stu-id="403c3-202">Run a sample application on Pi</span></span>

### <a name="install-hello-prerequisite-packages"></a><span data-ttu-id="403c3-203">Zainstaluj wstępnie wymagane pakiety hello</span><span class="sxs-lookup"><span data-stu-id="403c3-203">Install hello prerequisite packages</span></span>

<span data-ttu-id="403c3-204">Użyj jednej z hello poniższych klientów SSH z tooyour tooconnect Pi malina Twojego hosta komputera.</span><span class="sxs-lookup"><span data-stu-id="403c3-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
   
   <span data-ttu-id="403c3-205">**Użytkownicy systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="403c3-205">**Windows Users**</span></span>
   1. <span data-ttu-id="403c3-206">Pobierz i zainstaluj [PuTTY](http://www.putty.org/) dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="403c3-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="403c3-207">Skopiuj adres IP hello sekcji Pi do hello hosta nazwę (lub adres IP) i wybierz SSH jako hello typu połączenia.</span><span class="sxs-lookup"><span data-stu-id="403c3-207">Copy hello IP address of your Pi into hello Host name (or IP address) section and select SSH as hello connection type.</span></span>
   
   
   <span data-ttu-id="403c3-208">**Mac i Ubuntu użytkowników**</span><span class="sxs-lookup"><span data-stu-id="403c3-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="403c3-209">Przy użyciu wbudowanego klienta SSH hello na Ubuntu lub macOS.</span><span class="sxs-lookup"><span data-stu-id="403c3-209">Use hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="403c3-210">Może być konieczne toorun `ssh pi@<ip address of pi>` tooconnect Pi za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="403c3-210">You might need toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="403c3-211">Witaj domyślna nazwa użytkownika to `pi` , a hasło hello jest `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="403c3-211">hello default username is `pi` , and hello password is `raspberry`.</span></span>


### <a name="configure-hello-sample-application"></a><span data-ttu-id="403c3-212">Skonfiguruj hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="403c3-212">Configure hello sample application</span></span>

1. <span data-ttu-id="403c3-213">Klonowanie hello przykładowej aplikacji, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="403c3-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="403c3-214">Otwórz plik konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="403c3-214">Open hello config file by running hello following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="403c3-215">Istnieje 5 makra w tym pliku mogą configurate.</span><span class="sxs-lookup"><span data-stu-id="403c3-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="403c3-216">Witaj najpierw jest `MESSAGE_TIMESPAN`, który definiuje hello interwał (w milisekundach) między dwa komunikaty, które wysyłają toocloud.</span><span class="sxs-lookup"><span data-stu-id="403c3-216">hello first one is `MESSAGE_TIMESPAN`, which defines hello time interval (in milliseconds) between two messages that send toocloud.</span></span> <span data-ttu-id="403c3-217">Witaj drugi `SIMULATED_DATA`, czyli wartość logiczną parametru czy toouse symulowane dane czujników, czy nie.</span><span class="sxs-lookup"><span data-stu-id="403c3-217">hello second one `SIMULATED_DATA`, which is a Boolean value for whether toouse simulated sensor data or not.</span></span> <span data-ttu-id="403c3-218">`I2C_ADDRESS`to hello I2C adres, który jest połączony z czujnika BME280.</span><span class="sxs-lookup"><span data-stu-id="403c3-218">`I2C_ADDRESS` is hello I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="403c3-219">`GPIO_PIN_ADDRESS`jest adresem interfejs GPIO powitania dla Twojego LED.</span><span class="sxs-lookup"><span data-stu-id="403c3-219">`GPIO_PIN_ADDRESS` is hello GPIO address for your LED.</span></span> <span data-ttu-id="403c3-220">Witaj ostatnio jest `BLINK_TIMESPAN`, która zdefiniowana hello timespan po włączeniu LED sieci w milisekundach.</span><span class="sxs-lookup"><span data-stu-id="403c3-220">hello last one is `BLINK_TIMESPAN`, which defined hello timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="403c3-221">Jeśli użytkownik **nie ma czujnik hello**Ustaw hello `SIMULATED_DATA` wartość zbyt`True` toomake hello przykładowej aplikacji tworzenia i używania danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="403c3-221">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`True` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="403c3-222">Zapisz i zamknij naciskając formantu O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="403c3-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="403c3-223">Tworzenie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="403c3-223">Build and run hello sample application</span></span>

1. <span data-ttu-id="403c3-224">Tworzenie aplikacji przykładowej hello, uruchamiając następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="403c3-224">Build hello sample application by running hello following command.</span></span> <span data-ttu-id="403c3-225">Ponieważ hello Azure IoT SDK dla języka Python otoki u góry hello Azure IoT urządzenia C w zestawie SDK, konieczne będzie toocompile hello C biblioteki lub wymagają toogenerate hello Python biblioteki z kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="403c3-225">Because hello Azure IoT SDKs for Python are wrappers on top of hello Azure IoT Device C SDK, you will need toocompile hello C libraries if you want or need toogenerate hello Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="403c3-226">Można również określić, że chcesz używać wersji hello `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="403c3-226">You can also specify hello version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="403c3-227">Po uruchomieniu skryptu bez parametru skryptu hello automatycznie wykryje hello wersji języka python zainstalowany (Sekwencja wyszukiwania 2.7 -> 3.4 -> 3.5).</span><span class="sxs-lookup"><span data-stu-id="403c3-227">If you run script without parameter, hello script will automatically detect hello version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="403c3-228">Upewnij się, że wersji języka Python śledzi spójne podczas tworzenia i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="403c3-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="403c3-229">Na kompilowanie biblioteki klienta Python hello (iothub_client.so) na urządzeniami z systemem Linux, które mają mniej niż 1GB pamięci RAM, mogą pojawić kompilacji gromadzą 98% podczas kompilowania iothub_client_python.cpp, jak pokazano poniżej `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="403c3-229">On building hello Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="403c3-230">Jeśli napotkasz ten problem, sprawdź zużycia pamięci hello hello urządzeniami przy użyciu `free -m command` w innym oknie terminali w tym czasie.</span><span class="sxs-lookup"><span data-stu-id="403c3-230">If you run into this issue, check hello memory consumption of hello device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="403c3-231">Jeśli używasz Brak pamięci podczas kompilowania pliku iothub_client_python.cpp, może być tootemporarily zwiększyć tooget obszar wymiany hello dostępnej pamięci toosuccessfully kompilacji Biblioteka zestawu SDK urządzenia hello Python po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="403c3-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have tootemporarily increase hello swap space tooget more available memory toosuccessfully build hello Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="403c3-232">Uruchom aplikację przykładową hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="403c3-232">Run hello sample application by running hello following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="403c3-233">Upewnij się, możesz kopiowania i wklejania ciąg połączenia urządzenia hello w apostrofy hello.</span><span class="sxs-lookup"><span data-stu-id="403c3-233">Make sure you copy-paste hello device connection string into hello single quotes.</span></span> <span data-ttu-id="403c3-234">A jeśli używasz hello python 3, a następnie można użyć polecenia hello `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="403c3-234">And if you use hello python 3, then you can use hello command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="403c3-235">Powinien pojawić się następujące hello output, że pokazuje hello wiadomości powitania i danych czujnika, które są wysyłane tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="403c3-235">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

   ![Dane wyjściowe - wysyłane z Centrum IoT tooyour Pi malina dane czujników](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="403c3-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="403c3-237">Next steps</span></span>

<span data-ttu-id="403c3-238">Uruchomiono przykładowych danych czujnika toocollect aplikacji i wysyłać je tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="403c3-238">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span> <span data-ttu-id="403c3-239">wiadomości powitania toosee Twojego Pi malina został wysłany tooyour IoT hub lub wysyłania wiadomości tooyour Pi malina za pomocą interfejsu wiersza polecenia, zobacz hello [Zarządzaj chmury urządzenia wiadomości z Centrum iothub explorer samouczek](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="403c3-239">toosee hello messages that your Raspberry Pi has sent tooyour IoT hub or send messages tooyour Raspberry Pi in a command line interface, see hello [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
