---
title: "M0 toocloud: połączenia Wi-Fi piór M0 tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset Konfigurowanie i połączenia sieci Wi-Fi Adafruit piór M0 tooAzure Centrum IoT toosend danych toohello chmury Azure platforma w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="f4162-103">Połączenia sieci Wi-Fi Adafruit piór M0 tooAzure Centrum IoT w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="f4162-103">Connect Adafruit Feather M0 WiFi tooAzure IoT Hub in hello cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Połączenie między BME280, M0 piór sieci Wi-Fi i Centrum IoT](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="f4162-105">W tym samouczku Rozpocznij od uczenia hello podstawowe informacje dotyczące pracy z tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="f4162-105">In this tutorial, you begin by learning hello basics of working with your Arduino board.</span></span> <span data-ttu-id="f4162-106">Następnie dowiesz się, jak połączyć tooseamlessly chmury toohello urządzeń przy użyciu [Centrum IoT Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f4162-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="f4162-107">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="f4162-107">What you do</span></span>

<span data-ttu-id="f4162-108">Połącz Centrum IoT tooan Adafruit piór M0 sieci Wi-Fi, który utworzono.</span><span class="sxs-lookup"><span data-stu-id="f4162-108">Connect Adafruit Feather M0 WiFi tooan IoT hub that you create.</span></span> <span data-ttu-id="f4162-109">Następnie można uruchomić przykładową aplikację na M0 sieci Wi-Fi toocollect hello temperatury i wilgotności danych z BME280.</span><span class="sxs-lookup"><span data-stu-id="f4162-109">Then you run a sample application on M0 WiFi toocollect hello temperature and humidity data from a BME280.</span></span> <span data-ttu-id="f4162-110">Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.</span><span class="sxs-lookup"><span data-stu-id="f4162-110">Finally, you send hello sensor data tooyour IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="f4162-111">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="f4162-111">What you learn</span></span>

* <span data-ttu-id="f4162-112">Jak toocreate Centrum IoT i rejestrowanie urządzenia dla M0 piór sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="f4162-112">How toocreate an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="f4162-113">Jak tooconnect M0 piór sieci Wi-Fi z czujnika hello i komputera</span><span class="sxs-lookup"><span data-stu-id="f4162-113">How tooconnect Feather M0 WiFi with hello sensor and your computer</span></span>
* <span data-ttu-id="f4162-114">Jak dane czujników toocollect uruchamiając przykładową aplikację na M0 piór sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="f4162-114">How toocollect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="f4162-115">Jak toosend hello Centrum IoT tooyour danych czujnika</span><span class="sxs-lookup"><span data-stu-id="f4162-115">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f4162-116">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="f4162-116">What you need</span></span>

![Części potrzebne w samouczku hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="f4162-118">toocomplete tej operacji, należy powitania po części z Twojej startowy piór M0 sieci Wi-Fi:</span><span class="sxs-lookup"><span data-stu-id="f4162-118">toocomplete this operation, you need hello following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="f4162-119">Witaj tablicy M0 piór sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="f4162-119">hello Feather M0 WiFi board</span></span>
* <span data-ttu-id="f4162-120">TooType Micro USB kabla A USB</span><span class="sxs-lookup"><span data-stu-id="f4162-120">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="f4162-121">Należy również następujące elementy dla środowiska deweloperskiego hello:</span><span class="sxs-lookup"><span data-stu-id="f4162-121">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="f4162-122">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f4162-122">An active Azure subscription.</span></span> <span data-ttu-id="f4162-123">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f4162-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="f4162-124">Mac lub komputera z systemem Windows lub Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f4162-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="f4162-125">Sieć bezprzewodową tooconnect M0 piór sieci Wi-Fi do.</span><span class="sxs-lookup"><span data-stu-id="f4162-125">A wireless network for Feather M0 WiFi tooconnect to.</span></span>
* <span data-ttu-id="f4162-126">Internet połączenia toodownload hello narzędzie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f4162-126">An Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="f4162-127">[Arduino IDE](https://www.arduino.cc/en/main/software) wersji 1.6.8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f4162-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="f4162-128">Starszych wersjach nie działają z biblioteki Azure IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="f4162-128">Earlier versions don't work with hello Azure IoT Hub library.</span></span>

<span data-ttu-id="f4162-129">Jeśli nie masz czujnika hello następujące elementy są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="f4162-129">If you don’t have a sensor, hello following items are optional.</span></span> <span data-ttu-id="f4162-130">Istnieje również opcja hello przy użyciu danych czujnika symulowanego:</span><span class="sxs-lookup"><span data-stu-id="f4162-130">You also have hello option of using simulated sensor data:</span></span>

* <span data-ttu-id="f4162-131">Czujnik temperatury i wilgotności BME280</span><span class="sxs-lookup"><span data-stu-id="f4162-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="f4162-132">Breadboard</span><span class="sxs-lookup"><span data-stu-id="f4162-132">A breadboard</span></span>
* <span data-ttu-id="f4162-133">Przewodów zworek M/M</span><span class="sxs-lookup"><span data-stu-id="f4162-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a><span data-ttu-id="f4162-134">Połącz M0 piór sieci Wi-Fi z czujnika hello i komputera</span><span class="sxs-lookup"><span data-stu-id="f4162-134">Connect Feather M0 WiFi with hello sensor and your computer</span></span>
<span data-ttu-id="f4162-135">W tej sekcji można podłączyć hello czujników tooyour tablicy.</span><span class="sxs-lookup"><span data-stu-id="f4162-135">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="f4162-136">Następnie podłącz w komputerze tooyour urządzenia dla dalszego użytku.</span><span class="sxs-lookup"><span data-stu-id="f4162-136">Then you plug in your device tooyour computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a><span data-ttu-id="f4162-137">Połącz DHT22 temperatury i wilgotności czujnik tooFeather M0 sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="f4162-137">Connect a DHT22 temperature and humidity sensor tooFeather M0 WiFi</span></span>

<span data-ttu-id="f4162-138">Użyj hello breadboard i zworek przewodów toomake hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="f4162-138">Use hello breadboard and jumper wires toomake hello connection.</span></span> <span data-ttu-id="f4162-139">Jeśli nie masz czujnika, Pomiń tę sekcję, ponieważ można użyć danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="f4162-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Odwołanie do połączenia](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="f4162-141">Czujnik numery PIN użyć hello następujących połączeń:</span><span class="sxs-lookup"><span data-stu-id="f4162-141">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="f4162-142">Start (czujnik)</span><span class="sxs-lookup"><span data-stu-id="f4162-142">Start (sensor)</span></span>           | <span data-ttu-id="f4162-143">Końcowy (tablica)</span><span class="sxs-lookup"><span data-stu-id="f4162-143">End (board)</span></span>            | <span data-ttu-id="f4162-144">Kolor kabel</span><span class="sxs-lookup"><span data-stu-id="f4162-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="f4162-145">VDD (Pin 27A)</span><span class="sxs-lookup"><span data-stu-id="f4162-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="f4162-146">3V (3A kodu Pin)</span><span class="sxs-lookup"><span data-stu-id="f4162-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="f4162-147">Czerwony kabel</span><span class="sxs-lookup"><span data-stu-id="f4162-147">Red cable</span></span>     |
| <span data-ttu-id="f4162-148">GND (Pin 29A)</span><span class="sxs-lookup"><span data-stu-id="f4162-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="f4162-149">GND (6A kodu Pin)</span><span class="sxs-lookup"><span data-stu-id="f4162-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="f4162-150">Czarne kabel</span><span class="sxs-lookup"><span data-stu-id="f4162-150">Black cable</span></span>   |
| <span data-ttu-id="f4162-151">SCK (Pin 30A)</span><span class="sxs-lookup"><span data-stu-id="f4162-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="f4162-152">SCK (Pin 12A)</span><span class="sxs-lookup"><span data-stu-id="f4162-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="f4162-153">Żółty kabel</span><span class="sxs-lookup"><span data-stu-id="f4162-153">Yellow cable</span></span>  |
| <span data-ttu-id="f4162-154">SDO (Pin 31A)</span><span class="sxs-lookup"><span data-stu-id="f4162-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="f4162-155">MI (Pin 14A)</span><span class="sxs-lookup"><span data-stu-id="f4162-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="f4162-156">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="f4162-156">White cable</span></span>   |
| <span data-ttu-id="f4162-157">SDI (Pin 32A)</span><span class="sxs-lookup"><span data-stu-id="f4162-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="f4162-158">M0 (Pin 13A)</span><span class="sxs-lookup"><span data-stu-id="f4162-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="f4162-159">Niebieski kabel</span><span class="sxs-lookup"><span data-stu-id="f4162-159">Blue cable</span></span>    |
| <span data-ttu-id="f4162-160">CS (Pin 33A)</span><span class="sxs-lookup"><span data-stu-id="f4162-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="f4162-161">Interfejs GPIO 5 (Pin 15J)</span><span class="sxs-lookup"><span data-stu-id="f4162-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="f4162-162">Kabel pomarańczowy</span><span class="sxs-lookup"><span data-stu-id="f4162-162">Orange cable</span></span>  |

<span data-ttu-id="f4162-163">Aby uzyskać więcej informacji, zobacz [Adafruit BME280 wilgotności + barometryczne wykorzystania podgrupach czujnik temperatury](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) i [wyprowadzenia styków sieci Wi-Fi Adafruit piór M0](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span><span class="sxs-lookup"><span data-stu-id="f4162-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="f4162-164">Teraz sieci Wi-Fi M0 piór powinny być połączone z czujnika pracy.</span><span class="sxs-lookup"><span data-stu-id="f4162-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Uzyskuj DHT22 Huzzah piór](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a><span data-ttu-id="f4162-166">Podłącz komputer tooyour M0 piór sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="f4162-166">Connect Feather M0 WiFi tooyour computer</span></span>

<span data-ttu-id="f4162-167">Użyć hello Micro USB tooType A USB kabel tooconnect M0 piór sieci Wi-Fi tooyour komputera, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="f4162-167">Use hello Micro USB tooType A USB cable tooconnect Feather M0 WiFi tooyour computer, as shown:</span></span>

![Podłącz komputer tooyour Huzzah piór](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="f4162-169">Dodaj uprawnienia portu szeregowego (tylko Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="f4162-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="f4162-170">Jeśli używasz Ubuntu, upewnij się, że masz toooperate uprawnienia hello na powitania USB portu z piór M0 sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="f4162-170">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="f4162-171">tooadd uprawnienia portu szeregowego, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f4162-171">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="f4162-172">W terminalu uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="f4162-172">At a terminal, run hello following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="f4162-173">Pojawia się jeden z następujących danych wyjściowych hello:</span><span class="sxs-lookup"><span data-stu-id="f4162-173">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="f4162-174">crw-rw---xxxxxxxx uucp głównego 1</span><span class="sxs-lookup"><span data-stu-id="f4162-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="f4162-175">crw-rw---xxxxxxxx inicjowania połączeń głównego 1</span><span class="sxs-lookup"><span data-stu-id="f4162-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="f4162-176">W danych wyjściowych hello, zwróć uwagę, że `uucp` lub `dialout` jest nazwa właściciela grupy hello hello portu USB.</span><span class="sxs-lookup"><span data-stu-id="f4162-176">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

2. <span data-ttu-id="f4162-177">tooadd hello toohello grupy użytkowników, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="f4162-177">tooadd hello user toohello group, run hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="f4162-178">W poprzednim kroku hello uzyskać nazwę właściciela grupy hello `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="f4162-178">In hello previous step, you obtained hello group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="f4162-179">Nazwa użytkownika Ubuntu jest `<username>`.</span><span class="sxs-lookup"><span data-stu-id="f4162-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="f4162-180">Dla tooappear zmiany hello Wyloguj się Ubuntu i zaloguj ponownie.</span><span class="sxs-lookup"><span data-stu-id="f4162-180">For hello change tooappear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="f4162-181">Zbierać dane czujników oraz wysyłać je tooyour Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="f4162-181">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="f4162-182">W tej sekcji Wdróż i uruchom przykładową aplikację na M0 piór sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="f4162-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="f4162-183">Witaj przykładowej aplikacji sprawia, że hello migania LED na M0 piór sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="f4162-183">hello sample application makes hello LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="f4162-184">Następnie wysyła hello temperatury i wilgotności dane zbierane z hello BME280 czujnik tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f4162-184">It then sends hello temperature and humidity data collected from hello BME280 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a><span data-ttu-id="f4162-185">Pobierz hello przykładowej aplikacji z usługi GitHub i przygotowanie hello Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="f4162-185">Get hello sample application from GitHub and prepare hello Arduino IDE</span></span>

<span data-ttu-id="f4162-186">Witaj przykładowej aplikacji znajduje się w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f4162-186">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="f4162-187">Klonuj repozytorium przykładowej hello, zawierający hello przykładowej aplikacji z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="f4162-187">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="f4162-188">repozytorium przykładowej hello tooclone, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f4162-188">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="f4162-189">Otwórz wiersz polecenia lub okno terminalu.</span><span class="sxs-lookup"><span data-stu-id="f4162-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="f4162-190">Przejdź tooa folder docelowy toobe aplikacji przykładowej hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="f4162-190">Go tooa folder where you want hello sample application toobe stored.</span></span>
3. <span data-ttu-id="f4162-191">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="f4162-191">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a><span data-ttu-id="f4162-192">Zainstaluj pakiet powitania dla M0 piór sieci Wi-Fi w hello Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="f4162-192">Install hello package for Feather M0 WiFi in hello Arduino IDE</span></span>

1. <span data-ttu-id="f4162-193">Otwórz folder hello przechowywania hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4162-193">Open hello folder where hello sample application is stored.</span></span>

2. <span data-ttu-id="f4162-194">Otwórz plik app.ino hello w folderze aplikacji hello hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="f4162-194">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Otwórz aplikację przykładową hello w Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="f4162-196">Kliknij przycisk **pliku** > **preferencje** (system Windows/Linux) lub **Arduino** > **preferencje** (Mac) i skopiuj i Wklej hello poniższe łącze do hello **dodatkowych adresów URL Menedżera tablice** opcji hello preferencje Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="f4162-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste hello link below into hello **Additional Boards Manager URLs** option in hello Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="f4162-197">Kliknij przycisk **narzędzia** > **tablicy** > **Menedżera tablice**, a następnie zainstaluj hello `Arduino SAMD Boards` wersji `1.6.2` lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f4162-197">Click **Tools** > **Board** > **Boards Manager**, and then install hello `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="f4162-198">Następnie w tym samym oknie Witaj, zainstaluj `Adafruit SAMD Boards` tooadd hello tablicy pliku definicji pakietu.</span><span class="sxs-lookup"><span data-stu-id="f4162-198">Then in hello same window, install `Adafruit SAMD Boards` package tooadd hello board file definitions.</span></span>

   ![Pakiet esp8266 Hello jest zainstalowany](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="f4162-200">Kliknij przycisk **narzędzia** > **tablicy** > **Adafruit M0 sieci Wi-Fi**.</span><span class="sxs-lookup"><span data-stu-id="f4162-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="f4162-201">Zainstaluj sterowniki (tylko dla systemu Windows).</span><span class="sxs-lookup"><span data-stu-id="f4162-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="f4162-202">Po podłączeniu M0 piór sieci Wi-Fi, może być konieczne tooinstall sterownika.</span><span class="sxs-lookup"><span data-stu-id="f4162-202">When you plug in Feather M0 WiFi, you might need tooinstall a driver.</span></span> <span data-ttu-id="f4162-203">Kliknij przycisk [hello łącze na stronie sieci Web hello](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello sterownik Instalatora.</span><span class="sxs-lookup"><span data-stu-id="f4162-203">Click [hello download link on hello webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello driver installer.</span></span> <span data-ttu-id="f4162-204">Wykonaj hello kroki tooinstall hello sterowniki, które mają.</span><span class="sxs-lookup"><span data-stu-id="f4162-204">Follow hello steps tooinstall hello drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="f4162-205">Zainstaluj wymagane biblioteki</span><span class="sxs-lookup"><span data-stu-id="f4162-205">Install necessary libraries</span></span>

1. <span data-ttu-id="f4162-206">W hello Arduino IDE, kliknij przycisk **szkicu** > **obejmują biblioteki** > **zarządzanie bibliotekami**.</span><span class="sxs-lookup"><span data-stu-id="f4162-206">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="f4162-207">Wyszukiwanie hello następujące nazwy bibliotek jeden po drugim.</span><span class="sxs-lookup"><span data-stu-id="f4162-207">Search for hello following library names one by one.</span></span> <span data-ttu-id="f4162-208">Dla każdej biblioteki można znaleźć, kliknij przycisk **zainstalować**:</span><span class="sxs-lookup"><span data-stu-id="f4162-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="f4162-209">Ręcznie zainstaluj `Adafruit_WINC1500`.</span><span class="sxs-lookup"><span data-stu-id="f4162-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="f4162-210">Przejdź za[tej witryny sieci Web](https://github.com/adafruit/Adafruit_WINC1500) i kliknij przycisk **klonowania lub pobierania** > **Pobierz ZIP**.</span><span class="sxs-lookup"><span data-stu-id="f4162-210">Go too[this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="f4162-211">Następnie w środowiskiem IDE Arduino go za**szkicu** > **obejmują biblioteki** > **dodać .zip biblioteki** i Dodaj plik zip hello.</span><span class="sxs-lookup"><span data-stu-id="f4162-211">Then in your Arduino IDE, go too**Sketch** > **Include Library** > **Add .zip Library** and add hello zip file.</span></span>

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="f4162-212">Użyj hello przykładowej aplikacji, jeśli nie masz rzeczywistych czujnik BME280</span><span class="sxs-lookup"><span data-stu-id="f4162-212">Use hello sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="f4162-213">Jeśli nie masz rzeczywistych czujnik BME280 hello przykładowej aplikacji można symulować temperatury i wilgotności danych.</span><span class="sxs-lookup"><span data-stu-id="f4162-213">If you don’t have a real BME280 sensor, hello sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="f4162-214">tooset zapasowych danych toouse symulowane hello przykładowej aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f4162-214">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="f4162-215">Otwórz hello `config.h` pliku w hello `app` folderu.</span><span class="sxs-lookup"><span data-stu-id="f4162-215">Open hello `config.h` file in hello `app` folder.</span></span>

2. <span data-ttu-id="f4162-216">Znajdź powitania po wierszu kodu i zmień wartość hello z `false` zbyt`true`:</span><span class="sxs-lookup"><span data-stu-id="f4162-216">Locate hello following line of code and change hello value from `false` too`true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Konfigurowanie hello przykładowych aplikacji toouse symulowane danych](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="f4162-218">Zapisz plik hello z `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="f4162-218">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a><span data-ttu-id="f4162-219">Wdrażanie hello przykładowej aplikacji tooFeather M0 sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="f4162-219">Deploy hello sample application tooFeather M0 WiFi</span></span>

1. <span data-ttu-id="f4162-220">W hello Arduino IDE, kliknij przycisk **narzędzie** > **portu**, a następnie kliknij przycisk portu szeregowego hello M0 piór sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="f4162-220">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="f4162-221">Kliknij przycisk **szkicu** > **przekazać** toobuild i wdrażanie hello przykładowej aplikacji tooFeather M0 sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="f4162-221">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="f4162-222">Wprowadź swoje poświadczenia</span><span class="sxs-lookup"><span data-stu-id="f4162-222">Enter your credentials</span></span>

<span data-ttu-id="f4162-223">Po pomyślnym ukończeniu przekazywania hello wykonaj te kroki tooenter poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="f4162-223">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="f4162-224">W hello Arduino IDE, kliknij przycisk **narzędzia** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="f4162-224">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="f4162-225">W hello prawym dolnym rogu okna monitora serial hello, wybierz **nie zakończenia wiersza** na liście rozwijanej hello powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="f4162-225">In hello lower-right corner of hello serial monitor window, select **No line ending** in hello drop-down list on hello left.</span></span>
3. <span data-ttu-id="f4162-226">Wybierz **transmisji 115200** na liście rozwijanej hello na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="f4162-226">Select **115200 baud** in hello drop-down list on hello right.</span></span>
4. <span data-ttu-id="f4162-227">W polu wejściowym hello u góry hello, wprowadź hello następujących informacji, jeśli masz pytanie tooprovide i kliknij przycisk **wysyłania**:</span><span class="sxs-lookup"><span data-stu-id="f4162-227">In hello input box at hello top, enter hello following information if you're asked tooprovide it, and click **Send**:</span></span>

   * <span data-ttu-id="f4162-228">Identyfikator SSID sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="f4162-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="f4162-229">Hasło sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="f4162-229">Wi-Fi password</span></span>
   * <span data-ttu-id="f4162-230">Ciąg połączenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="f4162-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="f4162-231">informacje poświadczeń Hello są przechowywane w pamięci EEPROM piór M0 WiFi hello.</span><span class="sxs-lookup"><span data-stu-id="f4162-231">hello credential information is stored in hello EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="f4162-232">Jeśli klikniesz przycisk reset hello na powitania tablicy M0 piór sieci Wi-Fi, hello przykładowej aplikacji pyta użytkownika tooerase hello informacji.</span><span class="sxs-lookup"><span data-stu-id="f4162-232">If you click hello reset button on hello Feather M0 WiFi board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="f4162-233">Wprowadź `Y` tooerase hello informacji.</span><span class="sxs-lookup"><span data-stu-id="f4162-233">Enter `Y` tooerase hello information.</span></span> <span data-ttu-id="f4162-234">Monit tooprovide hello informacji po raz drugi.</span><span class="sxs-lookup"><span data-stu-id="f4162-234">You're asked tooprovide hello information a second time.</span></span>

### <a name="verify-that-hello-sample-application-is-running-successfully"></a><span data-ttu-id="f4162-235">Sprawdź, czy hello Przykładowa aplikacja działa prawidłowo</span><span class="sxs-lookup"><span data-stu-id="f4162-235">Verify that hello sample application is running successfully</span></span>

<span data-ttu-id="f4162-236">Jeśli widzisz hello następujące dane wyjściowe z okna monitora serial hello i hello migający LED na piór M0 Wi-Fi, hello Przykładowa aplikacja działa prawidłowo:</span><span class="sxs-lookup"><span data-stu-id="f4162-236">If you see hello following output from hello serial monitor window and hello blinking LED on Feather M0 WiFi, hello sample application is running successfully:</span></span>

![Ostateczne dane wyjściowe w Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="f4162-238">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f4162-238">Next steps</span></span>

<span data-ttu-id="f4162-239">Pomyślnie połączony Centrum IoT tooyour M0 piór sieci Wi-Fi i wysyłane z Centrum IoT tooyour danych czujnika hello przechwytywane.</span><span class="sxs-lookup"><span data-stu-id="f4162-239">You have successfully connected Feather M0 WiFi tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

