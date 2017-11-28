---
title: "Pi malinowe do chmury (Python) - Połącz Pi malina z Centrum IoT Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować i Pi malina nawiązać połączenia z Centrum IoT Azure pi malina do wysyłania danych do platformy w chmurze platformy Azure, w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "pi Azure iot malinowe, Centrum iot malinowe pi, pi malinowe wysyłania danych do chmury, malinowe pi do chmury"
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 1b1a9dc960846cbc15ce09d0fd106e1492937439
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-python"></a><span data-ttu-id="35b23-104">Pi malinowe nawiązać połączenia z Centrum IoT Azure (Python)</span><span class="sxs-lookup"><span data-stu-id="35b23-104">Connect Raspberry Pi to Azure IoT Hub (Python)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="35b23-105">W tym samouczku Rozpocznij od uczenia podstawy pracy z Pi malina, który działa Raspbian.</span><span class="sxs-lookup"><span data-stu-id="35b23-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="35b23-106">Następnie Dowiedz się jak bezproblemowo połączyć z urządzenia do chmury przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="35b23-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="35b23-107">Dla przykładów Windows 10 IoT Core, przejdź do [Centrum deweloperów systemu Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="35b23-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="35b23-108">Nie masz jeszcze zestawu?</span><span class="sxs-lookup"><span data-stu-id="35b23-108">Don't have a kit yet?</span></span> <span data-ttu-id="35b23-109">Spróbuj [symulatora online Pi malina](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="35b23-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="35b23-110">Lub kupowanie nowej kit [tutaj](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="35b23-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="35b23-111">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="35b23-111">What you do</span></span>

* <span data-ttu-id="35b23-112">Tworzenie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="35b23-112">Create an IoT hub.</span></span>
* <span data-ttu-id="35b23-113">Zarejestruj urządzenie pi w Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="35b23-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="35b23-114">Instalator malinowe Pi.</span><span class="sxs-lookup"><span data-stu-id="35b23-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="35b23-115">Uruchom przykładową aplikację na Pi do wysyłania danych czujnika do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="35b23-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="35b23-116">Pi malina nawiązać połączenia z Centrum IoT utworzony.</span><span class="sxs-lookup"><span data-stu-id="35b23-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="35b23-117">Następnie uruchom przykładową aplikację na Pi do zbierania danych temperatury i wilgotności z czujnika BME280.</span><span class="sxs-lookup"><span data-stu-id="35b23-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="35b23-118">Ponadto użytkownik wysyła dane czujników do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="35b23-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="35b23-119">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="35b23-119">What you learn</span></span>

* <span data-ttu-id="35b23-120">Sposób tworzenia Centrum Azure IoT i uzyskać nowy ciąg połączenia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="35b23-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="35b23-121">Jak nawiązać połączenia z czujnika BME280 Pi.</span><span class="sxs-lookup"><span data-stu-id="35b23-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="35b23-122">Jak zbierać dane czujników, uruchamiając przykładową aplikację na Pi.</span><span class="sxs-lookup"><span data-stu-id="35b23-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="35b23-123">Jak wysyłać dane czujników do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="35b23-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="35b23-124">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="35b23-124">What you need</span></span>

![Co jest potrzebne](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

* <span data-ttu-id="35b23-126">Malina Pi 2 lub 3 Pi malina tablicy.</span><span class="sxs-lookup"><span data-stu-id="35b23-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="35b23-127">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="35b23-127">An active Azure subscription.</span></span> <span data-ttu-id="35b23-128">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="35b23-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="35b23-129">Monitor, klawiatura USB i myszy łączący się Pi.</span><span class="sxs-lookup"><span data-stu-id="35b23-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="35b23-130">Mac lub komputer z systemem Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="35b23-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="35b23-131">Połączenie internetowe.</span><span class="sxs-lookup"><span data-stu-id="35b23-131">An Internet connection.</span></span>
* <span data-ttu-id="35b23-132">16 GB lub powyżej karty microSD.</span><span class="sxs-lookup"><span data-stu-id="35b23-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="35b23-133">USB-karty sieciowej lub microSD na kartach SD Nagraj obraz systemu operacyjnego na karcie microSD.</span><span class="sxs-lookup"><span data-stu-id="35b23-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="35b23-134">5 volt potęgą 2-amp dostarczyć stopy 6 micro kabel USB.</span><span class="sxs-lookup"><span data-stu-id="35b23-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="35b23-135">Opcjonalne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="35b23-135">The following items are optional:</span></span>

* <span data-ttu-id="35b23-136">Złożony Adafruit BME280 temperatury, wykorzystania i wilgotności czujnika.</span><span class="sxs-lookup"><span data-stu-id="35b23-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="35b23-137">Breadboard.</span><span class="sxs-lookup"><span data-stu-id="35b23-137">A breadboard.</span></span>
* <span data-ttu-id="35b23-138">6 F/M zworek przewodów.</span><span class="sxs-lookup"><span data-stu-id="35b23-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="35b23-139">Rozproszona LED 10 mm.</span><span class="sxs-lookup"><span data-stu-id="35b23-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="35b23-140">Te elementy są opcjonalne, ponieważ dane czujników symulowane obsługi próbki kodu.</span><span class="sxs-lookup"><span data-stu-id="35b23-140">These items are optional because the code sample support simulated sensor data.</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="set-up-raspberry-pi"></a><span data-ttu-id="35b23-141">Konfigurowanie Pi malina</span><span class="sxs-lookup"><span data-stu-id="35b23-141">Set up Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="35b23-142">Instalowanie systemu operacyjnego Raspbian pi</span><span class="sxs-lookup"><span data-stu-id="35b23-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="35b23-143">Przygotuj karty microSD instalacji obrazu Raspbian.</span><span class="sxs-lookup"><span data-stu-id="35b23-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="35b23-144">Pobierz Raspbian.</span><span class="sxs-lookup"><span data-stu-id="35b23-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="35b23-145">[Pobierz Joasia Raspbian z pulpitem](https://www.raspberrypi.org/downloads/raspbian/) (pliku .zip).</span><span class="sxs-lookup"><span data-stu-id="35b23-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="35b23-146">Wyodrębnij obrazu Raspbian do folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="35b23-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="35b23-147">Zainstaluj Raspbian karty microSD.</span><span class="sxs-lookup"><span data-stu-id="35b23-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="35b23-148">[Pobierz i zainstaluj narzędzie palnika karty Etcher SD](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="35b23-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="35b23-149">Uruchom Etcher i wybierz obraz Raspbian, który został wyodrębniony w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="35b23-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="35b23-150">Wybierz dysk karty microSD.</span><span class="sxs-lookup"><span data-stu-id="35b23-150">Select the microSD card drive.</span></span> <span data-ttu-id="35b23-151">Należy pamiętać, że Etcher może już wybrane poprawnego dysku.</span><span class="sxs-lookup"><span data-stu-id="35b23-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="35b23-152">Kliknij przycisk Flash instalowanie Raspbian karty microSD.</span><span class="sxs-lookup"><span data-stu-id="35b23-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="35b23-153">Karta microSD należy usunąć z komputera po zakończeniu instalacji.</span><span class="sxs-lookup"><span data-stu-id="35b23-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="35b23-154">Jest bezpiecznie usunąć karta microSD bezpośrednio, ponieważ Etcher automatycznie wysuwa lub odinstalowuje karty microSD po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="35b23-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="35b23-155">Włóż kartę microSD do Pi.</span><span class="sxs-lookup"><span data-stu-id="35b23-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="35b23-156">Włącz SSH i I2C</span><span class="sxs-lookup"><span data-stu-id="35b23-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="35b23-157">Pi nawiązać monitora, klawiatury i myszy, uruchom Pi, a następnie zaloguj Raspbian przy użyciu `pi` jako nazwy użytkownika i `raspberry` jako hasło.</span><span class="sxs-lookup"><span data-stu-id="35b23-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="35b23-158">Kliknij ikonę malinowe > **preferencje** > **malina Pi konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="35b23-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![Menu Preferencje Raspbian](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="35b23-160">Na **interfejsów** ustaw **I2C** i **SSH** do **włączyć**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="35b23-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="35b23-161">Jeśli nie masz fizycznych czujników i chcesz użyć danych czujnika symulowane, ten krok jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="35b23-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Włącz I2C i SSH na malinowe Pi](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="35b23-163">Aby włączyć SSH i I2C, można znaleźć więcej dokumentacji na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) i [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span><span class="sxs-lookup"><span data-stu-id="35b23-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="35b23-164">Połącz z czujnika do Pi</span><span class="sxs-lookup"><span data-stu-id="35b23-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="35b23-165">Użyj przewodów breadboard i zworek LED i nawiązywać BME280 Pi w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="35b23-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="35b23-166">Jeśli nie masz czujnika, [pominąć tę sekcję](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="35b23-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![Pi malina i czujnik połączenia](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="35b23-168">Czujnik BME280 może zbierać dane temperatury i wilgotności.</span><span class="sxs-lookup"><span data-stu-id="35b23-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="35b23-169">I LED będzie blink w przypadku braku komunikacji między urządzeniem i chmurą.</span><span class="sxs-lookup"><span data-stu-id="35b23-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="35b23-170">Czujnik numery PIN można użyć następujących połączeń:</span><span class="sxs-lookup"><span data-stu-id="35b23-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="35b23-171">Uruchom (czujnik & LED)</span><span class="sxs-lookup"><span data-stu-id="35b23-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="35b23-172">Końcowy (tablica)</span><span class="sxs-lookup"><span data-stu-id="35b23-172">End (Board)</span></span>            | <span data-ttu-id="35b23-173">Kolor kabel</span><span class="sxs-lookup"><span data-stu-id="35b23-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="35b23-174">VDD (Pin: 5 GB/S)</span><span class="sxs-lookup"><span data-stu-id="35b23-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="35b23-175">3, 3V PWR (Pin 1)</span><span class="sxs-lookup"><span data-stu-id="35b23-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="35b23-176">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="35b23-176">White cable</span></span>   |
| <span data-ttu-id="35b23-177">GND (Pin 7 GB/S)</span><span class="sxs-lookup"><span data-stu-id="35b23-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="35b23-178">GND (Pin 6)</span><span class="sxs-lookup"><span data-stu-id="35b23-178">GND (Pin 6)</span></span>            | <span data-ttu-id="35b23-179">Brązowy kabel</span><span class="sxs-lookup"><span data-stu-id="35b23-179">Brown cable</span></span>   |
| <span data-ttu-id="35b23-180">SDI (Pin 10 GB/S)</span><span class="sxs-lookup"><span data-stu-id="35b23-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="35b23-181">I2C1 SDA (Pin 3)</span><span class="sxs-lookup"><span data-stu-id="35b23-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="35b23-182">Czerwony kabel</span><span class="sxs-lookup"><span data-stu-id="35b23-182">Red cable</span></span>     |
| <span data-ttu-id="35b23-183">SCK (Pin 8 GB/S)</span><span class="sxs-lookup"><span data-stu-id="35b23-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="35b23-184">I2C1 SCL (Pin 5)</span><span class="sxs-lookup"><span data-stu-id="35b23-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="35b23-185">Kabel pomarańczowy</span><span class="sxs-lookup"><span data-stu-id="35b23-185">Orange cable</span></span>  |
| <span data-ttu-id="35b23-186">VDD LED (Pin 18F)</span><span class="sxs-lookup"><span data-stu-id="35b23-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="35b23-187">Interfejs GPIO 24 (Pin 18)</span><span class="sxs-lookup"><span data-stu-id="35b23-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="35b23-188">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="35b23-188">White cable</span></span>   |
| <span data-ttu-id="35b23-189">GND LED (Pin 17F)</span><span class="sxs-lookup"><span data-stu-id="35b23-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="35b23-190">GND (Pin 20)</span><span class="sxs-lookup"><span data-stu-id="35b23-190">GND (Pin 20)</span></span>           | <span data-ttu-id="35b23-191">Czarne kabel</span><span class="sxs-lookup"><span data-stu-id="35b23-191">Black cable</span></span>   |

<span data-ttu-id="35b23-192">Kliknij, aby wyświetlić [malina Pi 2 i 3 mapowania kodu Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) użytkownikowi.</span><span class="sxs-lookup"><span data-stu-id="35b23-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="35b23-193">Po pomyślnie nawiązano połączenie BME280 Twojego Pi malina, należy go jak poniżej obrazu.</span><span class="sxs-lookup"><span data-stu-id="35b23-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi połączonych i BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="35b23-195">Połączenie z siecią Pi</span><span class="sxs-lookup"><span data-stu-id="35b23-195">Connect Pi to the network</span></span>

<span data-ttu-id="35b23-196">Włącz Pi przy użyciu micro kabla USB i zasilania.</span><span class="sxs-lookup"><span data-stu-id="35b23-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="35b23-197">Łączenie Pi sieci przewodowej lub wykonaj przy użyciu kabla Ethernet [instrukcji Foundation Pi malina](https://www.raspberrypi.org/learning/software-guide/wifi/) do nawiązania połączenia z siecią bezprzewodową Pi.</span><span class="sxs-lookup"><span data-stu-id="35b23-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="35b23-198">Po Twoje Pi została pomyślnie podłączona do sieci, należy pamiętać o [adres IP Twojego Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="35b23-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Podłączony do sieci przewodowej](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="35b23-200">Upewnij się, że Pi jest podłączony do sieci z komputera.</span><span class="sxs-lookup"><span data-stu-id="35b23-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="35b23-201">Na przykład jeśli komputer jest połączony z siecią bezprzewodową, gdy Pi jest połączony z siecią przewodową, może nie być wyświetlana w danych wyjściowych devdisco adres IP.</span><span class="sxs-lookup"><span data-stu-id="35b23-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="35b23-202">Uruchom przykładową aplikację na Pi</span><span class="sxs-lookup"><span data-stu-id="35b23-202">Run a sample application on Pi</span></span>

### <a name="install-the-prerequisite-packages"></a><span data-ttu-id="35b23-203">Zainstaluj wstępnie wymagane pakiety</span><span class="sxs-lookup"><span data-stu-id="35b23-203">Install the prerequisite packages</span></span>

<span data-ttu-id="35b23-204">Aby nawiązać połączenie z Pi malina, użyj jednej z następujących klientów SSH z komputera hosta.</span><span class="sxs-lookup"><span data-stu-id="35b23-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="35b23-205">**Użytkownicy systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="35b23-205">**Windows Users**</span></span>
   1. <span data-ttu-id="35b23-206">Pobierz i zainstaluj [PuTTY](http://www.putty.org/) dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="35b23-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="35b23-207">Skopiuj adres IP z sekcji Pi na nazwę hosta (lub adres IP) i wybierz typ połączenia SSH.</span><span class="sxs-lookup"><span data-stu-id="35b23-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   
   <span data-ttu-id="35b23-208">**Mac i Ubuntu użytkowników**</span><span class="sxs-lookup"><span data-stu-id="35b23-208">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="35b23-209">Ubuntu lub macOS, korzystając z wbudowanego klienta SSH.</span><span class="sxs-lookup"><span data-stu-id="35b23-209">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="35b23-210">Może być konieczne uruchomienie `ssh pi@<ip address of pi>` nawiązać Pi za pośrednictwem protokołu SSH.</span><span class="sxs-lookup"><span data-stu-id="35b23-210">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="35b23-211">Domyślna nazwa użytkownika to `pi` , a hasło to `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="35b23-211">The default username is `pi` , and the password is `raspberry`.</span></span>


### <a name="configure-the-sample-application"></a><span data-ttu-id="35b23-212">Konfigurowanie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="35b23-212">Configure the sample application</span></span>

1. <span data-ttu-id="35b23-213">Klonowanie przykładowej aplikacji, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="35b23-213">Clone the sample application by running the following command:</span></span>

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. <span data-ttu-id="35b23-214">Otwórz plik konfiguracji, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="35b23-214">Open the config file by running the following commands:</span></span>

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   <span data-ttu-id="35b23-215">Istnieje 5 makra w tym pliku mogą configurate.</span><span class="sxs-lookup"><span data-stu-id="35b23-215">There are 5 macros in this file you can configurate.</span></span> <span data-ttu-id="35b23-216">Pierwsza z nich jest `MESSAGE_TIMESPAN`, która określa przedział czasu (w milisekundach) między dwa komunikaty, które wysyłają do chmury.</span><span class="sxs-lookup"><span data-stu-id="35b23-216">The first one is `MESSAGE_TIMESPAN`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="35b23-217">Drugi `SIMULATED_DATA`, która jest wartość logiczna, czy należy użyć danych czujnika symulowane lub nie.</span><span class="sxs-lookup"><span data-stu-id="35b23-217">The second one `SIMULATED_DATA`, which is a Boolean value for whether to use simulated sensor data or not.</span></span> <span data-ttu-id="35b23-218">`I2C_ADDRESS`jest to adres I2C, które z czujnika BME280 jest połączony.</span><span class="sxs-lookup"><span data-stu-id="35b23-218">`I2C_ADDRESS` is the I2C address which your BME280 sensor is connected.</span></span> <span data-ttu-id="35b23-219">`GPIO_PIN_ADDRESS`jest to adres interfejs GPIO dla Twojego LED.</span><span class="sxs-lookup"><span data-stu-id="35b23-219">`GPIO_PIN_ADDRESS` is the GPIO address for your LED.</span></span> <span data-ttu-id="35b23-220">Jest ostatnim blokiem `BLINK_TIMESPAN`, który zdefiniowany zakres czasu, po włączeniu LED sieci w milisekundach.</span><span class="sxs-lookup"><span data-stu-id="35b23-220">The last one is `BLINK_TIMESPAN`, which defined the timespan when your LED is turned on in milliseconds.</span></span>

   <span data-ttu-id="35b23-221">Jeśli użytkownik **nie ma czujnika**, ustaw `SIMULATED_DATA` do wartości `True` dokonanie przykładowej aplikacji, tworzenia i używania danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="35b23-221">If you **don't have the sensor**, set the `SIMULATED_DATA` value to `True` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="35b23-222">Zapisz i zamknij naciskając formantu O > Enter > Control X.</span><span class="sxs-lookup"><span data-stu-id="35b23-222">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-the-sample-application"></a><span data-ttu-id="35b23-223">Tworzenie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="35b23-223">Build and run the sample application</span></span>

1. <span data-ttu-id="35b23-224">Tworzenie przykładowej aplikacji, uruchamiając następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="35b23-224">Build the sample application by running the following command.</span></span> <span data-ttu-id="35b23-225">Ponieważ zestawy IoT Azure SDK dla języka Python otoki u góry zestawu SDK usługi Azure IoT urządzenia C, należy skompilować bibliotek C lub należy wygenerować biblioteki języka Python z kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="35b23-225">Because the Azure IoT SDKs for Python are wrappers on top of the Azure IoT Device C SDK, you will need to compile the C libraries if you want or need to generate the Python libraries from source code.</span></span>

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   <span data-ttu-id="35b23-226">Można również określić, że wersja ma uruchamiając `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span><span class="sxs-lookup"><span data-stu-id="35b23-226">You can also specify the version you want by running `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`.</span></span> <span data-ttu-id="35b23-227">Po uruchomieniu skryptu bez parametru skrypt będzie automatycznie wykrywał wersji języka Python zainstalowany (Sekwencja wyszukiwania 2.7 -> 3.4 -> 3.5).</span><span class="sxs-lookup"><span data-stu-id="35b23-227">If you run script without parameter, the script will automatically detect the version of python installed (Search sequence 2.7->3.4->3.5).</span></span> <span data-ttu-id="35b23-228">Upewnij się, że wersji języka Python śledzi spójne podczas tworzenia i uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="35b23-228">Make sure your Python version keeps consistent during building and running.</span></span> 
   
   > [!NOTE] 
   <span data-ttu-id="35b23-229">W bibliotece klienta języka Python (iothub_client.so) korzystając z urządzeniami z systemem Linux, które mają mniej niż 1GB pamięci RAM, mogą pojawić kompilacji gromadzą 98% podczas kompilowania iothub_client_python.cpp, jak pokazano poniżej `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span><span class="sxs-lookup"><span data-stu-id="35b23-229">On building the Python client library (iothub_client.so) on Linux devices that have less than 1GB RAM, you may see build getting stuck at 98% while building iothub_client_python.cpp as shown below `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`.</span></span> <span data-ttu-id="35b23-230">Jeśli napotkasz ten problem, sprawdź zużycia pamięci urządzeniami przy użyciu `free -m command` w innym oknie terminali w tym czasie.</span><span class="sxs-lookup"><span data-stu-id="35b23-230">If you run into this issue, check the memory consumption of the device using `free -m command` in another terminal window during that time.</span></span> <span data-ttu-id="35b23-231">Jeśli używasz Brak pamięci podczas kompilowania pliku iothub_client_python.cpp, może być konieczne tymczasowo Zwiększ obszar wymiany, aby uzyskać więcej dostępnej pamięci, aby pomyślnie skompilować urządzenia klienckie Python Biblioteka zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="35b23-231">If you are running out of memory while compiling iothub_client_python.cpp file, you may have to temporarily increase the swap space to get more available memory to successfully build the Python client-side device SDK library.</span></span>
   
1. <span data-ttu-id="35b23-232">Uruchom przykładową aplikację, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="35b23-232">Run the sample application by running the following command:</span></span>

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="35b23-233">Upewnij się, możesz kopiowania i wklejania ciąg połączenia urządzenia w pojedynczy cudzysłów.</span><span class="sxs-lookup"><span data-stu-id="35b23-233">Make sure you copy-paste the device connection string into the single quotes.</span></span> <span data-ttu-id="35b23-234">A jeśli używasz języka python 3, a następnie użyć polecenia `python3 app.py '<your Azure IoT hub device connection string>'`.</span><span class="sxs-lookup"><span data-stu-id="35b23-234">And if you use the python 3, then you can use the command `python3 app.py '<your Azure IoT hub device connection string>'`.</span></span>


   <span data-ttu-id="35b23-235">Powinny zostać wyświetlone następujące dane wyjściowe, który zawiera dane czujników i komunikaty, które są wysyłane do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="35b23-235">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

   ![Dane wyjściowe — dane czujników wysłanych z Pi malina Centrum IoT](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a><span data-ttu-id="35b23-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35b23-237">Next steps</span></span>

<span data-ttu-id="35b23-238">Uruchomiono przykładowej aplikacji do zbierania danych czujników i wysyłania go do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="35b23-238">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="35b23-239">Wyświetlanie komunikatów wysłanych z Pi malina do IoT koncentratora lub wysłania wiadomości do Twojej Pi malina za pomocą interfejsu wiersza polecenia, zobacz [Zarządzaj chmury urządzenia wiadomości z Centrum iothub explorer samouczek](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="35b23-239">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
