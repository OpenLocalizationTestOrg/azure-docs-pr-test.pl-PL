---
title: "Pi malinowe do chmury (Node.js) - Połącz Pi malina z Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Pi malina nawiązać połączenia z Centrum IoT Azure pi malina do wysyłania danych do chmury platformy Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "pi Azure iot malinowe, Centrum iot malinowe pi, pi malinowe wysyłania danych do chmury, malinowe pi do chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="0cdb0-104">Pi malinowe nawiązać połączenia z Centrum IoT Azure (Node.js)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="0cdb0-105">W tym samouczku Rozpocznij od uczenia podstawy pracy z Pi malina, który działa Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="0cdb0-106">Następnie Dowiedz się jak bezproblemowo połączyć z urządzenia do chmury przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="0cdb0-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="0cdb0-107">Dla przykładów Windows 10 IoT Core, przejdź do [Centrum deweloperów systemu Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="0cdb0-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="0cdb0-108">Nie masz jeszcze zestawu?</span><span class="sxs-lookup"><span data-stu-id="0cdb0-108">Don't have a kit yet?</span></span> <span data-ttu-id="0cdb0-109">Spróbuj [emulatora malina Pi 3](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="0cdb0-109">Try the [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="0cdb0-110">Lub kupowanie nowej kit [tutaj](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="0cdb0-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="0cdb0-111">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="0cdb0-111">What you do</span></span>

* <span data-ttu-id="0cdb0-112">Instalator malinowe Pi.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="0cdb0-113">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-113">Create an IoT hub.</span></span>
* <span data-ttu-id="0cdb0-114">Zarejestruj urządzenie pi w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="0cdb0-115">Uruchom przykładową aplikację na Pi do wysyłania danych czujnika do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="0cdb0-116">Pi malina nawiązać połączenia z Centrum IoT utworzony.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="0cdb0-117">Następnie uruchom przykładową aplikację na Pi do zbierania danych temperatury i wilgotności z czujnika BME280.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="0cdb0-118">Ponadto użytkownik wysyła dane czujników do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="0cdb0-119">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="0cdb0-119">What you learn</span></span>

* <span data-ttu-id="0cdb0-120">Sposób tworzenia Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="0cdb0-121">Jak nawiązać połączenia z czujnika BME280 Pi.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="0cdb0-122">Jak zbierać dane czujników, uruchamiając przykładową aplikację na Pi.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="0cdb0-123">Jak wysyłać dane czujników do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0cdb0-124">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="0cdb0-124">What you need</span></span>

![Co jest potrzebne](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="0cdb0-126">Malina Pi 2 lub 3 Pi malina tablicy.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="0cdb0-127">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-127">An active Azure subscription.</span></span> <span data-ttu-id="0cdb0-128">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="0cdb0-129">Monitor, klawiatura USB i myszy łączący się Pi.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="0cdb0-130">Mac lub komputer z systemem Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="0cdb0-131">Połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-131">An Internet connection.</span></span>
* <span data-ttu-id="0cdb0-132">16 GB lub powyżej karty microSD.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="0cdb0-133">USB-karty sieciowej lub microSD na kartach SD Nagraj obraz systemu operacyjnego na karcie microSD.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="0cdb0-134">5 volt potęgą 2-amp dostarczyć stopy 6 micro kabel USB.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="0cdb0-135">Opcjonalne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0cdb0-135">The following items are optional:</span></span>

* <span data-ttu-id="0cdb0-136">Złożony Adafruit BME280 temperatury, wykorzystania i wilgotności czujnika.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="0cdb0-137">Breadboard.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-137">A breadboard.</span></span>
* <span data-ttu-id="0cdb0-138">6 F/M zworek przewodów.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="0cdb0-139">Rozproszona LED 10 mm.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="0cdb0-140">Te elementy są opcjonalne, ponieważ dane czujników symulowane obsługi próbki kodu.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="0cdb0-141">Konfiguracja malinowe Pi</span><span class="sxs-lookup"><span data-stu-id="0cdb0-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="0cdb0-142">Instalowanie systemu operacyjnego Raspbian pi</span><span class="sxs-lookup"><span data-stu-id="0cdb0-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="0cdb0-143">Przygotuj karty microSD instalacji obrazu Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="0cdb0-144">Pobierz Raspbian.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="0cdb0-145">[Pobierz Joasia Raspbian z pikseli](https://www.raspberrypi.org/downloads/raspbian/) (pliku .zip).</span><span class="sxs-lookup"><span data-stu-id="0cdb0-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="0cdb0-146">Wyodrębnij obrazu Raspbian do folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="0cdb0-147">Zainstaluj Raspbian karty microSD.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="0cdb0-148">[Pobierz i zainstaluj narzędzie palnika karty Etcher SD](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="0cdb0-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="0cdb0-149">Uruchom Etcher i wybierz obraz Raspbian, który został wyodrębniony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="0cdb0-150">Wybierz dysk karty microSD.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-150">Select the microSD card drive.</span></span> <span data-ttu-id="0cdb0-151">Należy pamiętać, że Etcher może już wybrane poprawnego dysku.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="0cdb0-152">Kliknij przycisk Flash instalowanie Raspbian karty microSD.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="0cdb0-153">Karta microSD należy usunąć z komputera po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="0cdb0-154">Jest bezpiecznie usunąć karta microSD bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karty microSD po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="0cdb0-155">Włóż kartę microSD do Pi.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="0cdb0-156">Włącz SSH i I2C</span><span class="sxs-lookup"><span data-stu-id="0cdb0-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="0cdb0-157">Pi nawiązać monitora, klawiatury i myszy, uruchom Pi, a następnie zaloguj Raspbian przy użyciu `pi` jako nazwy użytkownika i `raspberry` jako hasło.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="0cdb0-158">Kliknij ikonę malinowe > **preferencje** > **malina Pi konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Menu Preferencje Raspbian](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="0cdb0-160">Na **interfejsów** ustaw **I2C** i **SSH** do **włączyć**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="0cdb0-161">Jeśli nie masz fizycznych czujników i chcesz użyć danych czujnika symulowane, ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Włącz I2C i SSH na malinowe Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="0cdb0-163">Aby włączyć SSH i I2C, można znaleźć więcej dokumentacji na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) i [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="0cdb0-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="0cdb0-164">Połącz z czujnika do Pi</span><span class="sxs-lookup"><span data-stu-id="0cdb0-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="0cdb0-165">Użyj przewodów breadboard i zworek LED i nawiązywać BME280 Pi w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="0cdb0-166">Jeśli nie masz czujnika, Pomiń tę sekcję.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-166">If you don’t have the sensor, skip this section.</span></span>

![Pi malina i czujnik połączenia](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="0cdb0-168">Czujnik BME280 może zbierać dane temperatury i wilgotności.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="0cdb0-169">I LED będzie blink w przypadku braku komunikacji między urządzeniem i chmurą.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="0cdb0-170">Czujnik numery PIN można użyć następujących połączeń:</span><span class="sxs-lookup"><span data-stu-id="0cdb0-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="0cdb0-171">Uruchom (czujnik & LED)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="0cdb0-172">Końcowy (tablica)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-172">End (Board)</span></span>            | <span data-ttu-id="0cdb0-173">Kolor kabel</span><span class="sxs-lookup"><span data-stu-id="0cdb0-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="0cdb0-174">VDD (Pin: 5 GB/S)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="0cdb0-175">3, 3V PWR (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="0cdb0-176">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="0cdb0-176">White cable</span></span>   |
| <span data-ttu-id="0cdb0-177">GND (Pin 7 GB/S)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="0cdb0-178">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-178">GND (Pin 6)</span></span>            | <span data-ttu-id="0cdb0-179">Brązowy kabel</span><span class="sxs-lookup"><span data-stu-id="0cdb0-179">Brown cable</span></span>   |
| <span data-ttu-id="0cdb0-180">SCK (Pin 8 GB/S)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="0cdb0-181">I2C1 SDA (Pin 3)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="0cdb0-182">Kabel pomarańczowy</span><span class="sxs-lookup"><span data-stu-id="0cdb0-182">Orange cable</span></span>  |
| <span data-ttu-id="0cdb0-183">SDI (Pin 10 GB/S)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="0cdb0-184">I2C1 SCL (Pin 5)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="0cdb0-185">Czerwony kabel</span><span class="sxs-lookup"><span data-stu-id="0cdb0-185">Red cable</span></span>     |
| <span data-ttu-id="0cdb0-186">VDD LED (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="0cdb0-187">Interfejs GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="0cdb0-188">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="0cdb0-188">White cable</span></span>   |
| <span data-ttu-id="0cdb0-189">GND LED (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="0cdb0-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="0cdb0-190">GND (Pin 20)</span></span>           | <span data-ttu-id="0cdb0-191">Czarne kabel</span><span class="sxs-lookup"><span data-stu-id="0cdb0-191">Black cable</span></span>   |

<span data-ttu-id="0cdb0-192">Kliknij, aby wyświetlić [malina Pi 2 i 3 mapowania kodu Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) użytkownikowi.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="0cdb0-193">Po pomyślnie nawiązano połączenie BME280 Twojego Pi malina, należy go jak poniżej obrazu.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi połączonych i BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="0cdb0-195">Połączenie z siecią Pi</span><span class="sxs-lookup"><span data-stu-id="0cdb0-195">Connect Pi to the network</span></span>

<span data-ttu-id="0cdb0-196">Włącz Pi przy użyciu micro kabla USB i zasilania.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="0cdb0-197">Łączenie Pi sieci przewodowej lub wykonaj przy użyciu kabla Ethernet [instrukcji Foundation Pi malina](https://www.raspberrypi.org/learning/software-guide/wifi/) do nawiązania połączenia z siecią bezprzewodową Pi.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="0cdb0-198">Po Twoje Pi została pomyślnie podłączona do sieci, należy pamiętać o [adres IP Twojego Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="0cdb0-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Podłączony do sieci przewodowej](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="0cdb0-200">Upewnij się, że Pi jest podłączony do sieci z komputera.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="0cdb0-201">Na przykład jeśli komputer jest połączony z siecią bezprzewodową, gdy Pi jest połączony z siecią przewodową, może nie być wyświetlana w danych wyjściowych devdisco adres IP.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="0cdb0-202">Uruchom przykładową aplikację na Pi</span><span class="sxs-lookup"><span data-stu-id="0cdb0-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="0cdb0-203">Sklonuj przykładową aplikację i zainstalować wstępnie wymagane pakiety</span><span class="sxs-lookup"><span data-stu-id="0cdb0-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="0cdb0-204">Aby nawiązać połączenie z Pi malina, użyj jednej z następujących klientów SSH z komputera hosta.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
    - <span data-ttu-id="0cdb0-205">[PuTTY](http://www.putty.org/) dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="0cdb0-206">Należy adres IP Twojego Pi połączenia go za pomocą protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-206">You need the IP address of your Pi to connect it via SSH.</span></span>
    - <span data-ttu-id="0cdb0-207">Wbudowane SSH klient Ubuntu lub macOS.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-207">The built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="0cdb0-208">Być może należy uruchomić `ssh pi@<ip address of pi>` nawiązać Pi za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-208">You might need run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="0cdb0-209">Domyślna nazwa użytkownika to `pi` , a hasło to `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-209">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="0cdb0-210">Zainstaluj z Pi Node.js i NPM.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-210">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="0cdb0-211">Najpierw należy sprawdzić wersji środowiska Node.js przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-211">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="0cdb0-212">Jeśli wersja jest starsza niż 4.x lub nie nie Node.js na Pi następnie uruchom następujące polecenie, aby zainstalować lub zaktualizować Node.js.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-212">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="0cdb0-213">Klonowanie przykładowej aplikacji, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="0cdb0-213">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="0cdb0-214">Za pomocą następującego polecenia, należy zainstalować wszystkie pakiety.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-214">Install all packages by the following command.</span></span> <span data-ttu-id="0cdb0-215">Zawiera urządzenia Azure IoT SDK, czujnik BME280 biblioteki i Biblioteka dołączenie Pi.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="0cdb0-216">Może upłynąć kilka minut na zakończenie tego denpening procesu instalacji na połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-216">It might take several minutes to finish this installation process denpening on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="0cdb0-217">Konfigurowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="0cdb0-217">Configure the sample application</span></span>

1. <span data-ttu-id="0cdb0-218">Otwórz plik konfiguracji, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="0cdb0-218">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Plik konfiguracji](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="0cdb0-220">Istnieją dwa elementy w tym pliku mogą configurate.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="0cdb0-221">Pierwsza z nich jest `interval`, który definiuje odstęp czasu między dwa komunikaty, które wysyłają do chmury.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-221">The first one is `interval`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="0cdb0-222">Drugi `simulatedData`, która jest wartość logiczna, czy należy użyć danych czujnika symulowane lub nie.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-222">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="0cdb0-223">Jeśli użytkownik **nie ma czujnika**, ustaw `simulatedData` do wartości `true` dokonanie przykładowej aplikacji, tworzenia i używania danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-223">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="0cdb0-224">Zapisz i zamknij naciskając formantu O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="0cdb0-225">Uruchom przykładową aplikację</span><span class="sxs-lookup"><span data-stu-id="0cdb0-225">Run the sample application</span></span>

1. <span data-ttu-id="0cdb0-226">Uruchom przykładową aplikację, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="0cdb0-226">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="0cdb0-227">Upewnij się, możesz kopiowania i wklejania ciąg połączenia urządzenia w pojedynczy cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-227">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="0cdb0-228">Powinny zostać wyświetlone następujące dane wyjściowe, który zawiera dane czujników i komunikaty, które są wysyłane do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-228">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Dane wyjściowe — dane czujników wysłanych z Pi malina Centrum IoT](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="0cdb0-230">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0cdb0-230">Next steps</span></span>

<span data-ttu-id="0cdb0-231">Uruchomiono przykładowej aplikacji do zbierania danych czujników i wysyłania go do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0cdb0-231">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]