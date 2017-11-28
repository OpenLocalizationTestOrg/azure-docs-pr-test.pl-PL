---
title: "toocloud aaaESP8266 — Połącz deweloperów operacją ESP8266 Sparkfun tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz deweloperów operacją ESP8266 Sparkfun tooAzure Centrum IoT dla niego toosend danych toohello chmury Azure platforma w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="df786-103">Połącz tooAzure Sparkfun ESP8266 operacją deweloperów Centrum IoT w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="df786-103">Connect Sparkfun ESP8266 Thing Dev tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![połączenie między DHT22, co deweloperów i Centrum IoT](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="df786-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="df786-105">What you will do</span></span>

<span data-ttu-id="df786-106">Połącz Centrum IoT tooan Sparkfun ESP8266 operacją deweloperów, zostanie utworzony.</span><span class="sxs-lookup"><span data-stu-id="df786-106">Connect Sparkfun ESP8266 Thing Dev tooan IoT hub you will create.</span></span> <span data-ttu-id="df786-107">Następnie uruchom przykładową aplikację na ESP8266 toocollect temperatury i wilgotności danych z czujnika DHT22.</span><span class="sxs-lookup"><span data-stu-id="df786-107">Then run a sample application on ESP8266 toocollect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="df786-108">Na koniec Wyślij Centrum IoT tooyour danych czujnika hello.</span><span class="sxs-lookup"><span data-stu-id="df786-108">Finally, send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="df786-109">Jeśli używasz innych tablice ESP8266 nadal należy wykonać te kroki tooconnect on tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="df786-109">If you are using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="df786-110">W zależności od tablicy hello ESP8266 używasz, może być konieczne tooreconfigure hello `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="df786-110">Depending on hello ESP8266 board you are using, you may need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="df786-111">Na przykład, jeśli używasz ESP8266 z AI Thinker, możesz zmienić go z `0` zbyt`2`.</span><span class="sxs-lookup"><span data-stu-id="df786-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` too`2`.</span></span> <span data-ttu-id="df786-112">Zestaw nie ma jeszcze?: kliknij [tutaj](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="df786-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="df786-113">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="df786-113">What you will learn</span></span>

* <span data-ttu-id="df786-114">Jak toocreate Centrum IoT i zarejestruj urządzenie na rzecz odchyleń</span><span class="sxs-lookup"><span data-stu-id="df786-114">How toocreate an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="df786-115">Jak tooconnect deweloperów operacją z czujnika hello i komputera.</span><span class="sxs-lookup"><span data-stu-id="df786-115">How tooconnect Thing Dev with hello sensor and your computer.</span></span>
* <span data-ttu-id="df786-116">Jak toocollect dane czujników, uruchamiając na rzecz odchyleń przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="df786-116">How toocollect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="df786-117">Jak toosend hello Centrum IoT tooyour danych czujnika.</span><span class="sxs-lookup"><span data-stu-id="df786-117">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="df786-118">Dane będą potrzebne</span><span class="sxs-lookup"><span data-stu-id="df786-118">What you will need</span></span>

![Części potrzebne w samouczku hello](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="df786-120">toocomplete tej operacji, należy po części z Twojej deweloperów element startowy hello:</span><span class="sxs-lookup"><span data-stu-id="df786-120">toocomplete this operation, you need hello following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="df786-121">Witaj deweloperów operacją ESP8266 Sparkfun tablicy.</span><span class="sxs-lookup"><span data-stu-id="df786-121">hello Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="df786-122">TooType Micro USB kabla A USB.</span><span class="sxs-lookup"><span data-stu-id="df786-122">A Micro USB tooType A USB cable.</span></span>

<span data-ttu-id="df786-123">Należy również następujące powitania dla swojego środowiska programowania:</span><span class="sxs-lookup"><span data-stu-id="df786-123">You also need hello following for your development environment:</span></span>

* <span data-ttu-id="df786-124">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="df786-124">An active Azure subscription.</span></span> <span data-ttu-id="df786-125">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="df786-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="df786-126">Mac lub komputera z systemem Windows lub Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="df786-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="df786-127">Sieci bezprzewodowej dla deweloperów operacją ESP8266 Sparkfun tooconnect do.</span><span class="sxs-lookup"><span data-stu-id="df786-127">Wireless network for Sparkfun ESP8266 Thing Dev tooconnect to.</span></span>
* <span data-ttu-id="df786-128">Internet połączenia toodownload hello narzędzia do konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="df786-128">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="df786-129">[Arduino IDE](https://www.arduino.cc/en/main/software) wersji 1.6.8 (lub nowsza), wcześniejszych wersjach nie będzie działać z biblioteką AzureIoT hello.</span><span class="sxs-lookup"><span data-stu-id="df786-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with hello AzureIoT library.</span></span>

<span data-ttu-id="df786-130">Witaj następujące elementy są opcjonalne w przypadku, gdy nie masz czujnika.</span><span class="sxs-lookup"><span data-stu-id="df786-130">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="df786-131">Istnieje również opcja hello przy użyciu danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="df786-131">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="df786-132">Adafruit DHT22 temperatury i wilgotności czujnika.</span><span class="sxs-lookup"><span data-stu-id="df786-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="df786-133">Breadboard.</span><span class="sxs-lookup"><span data-stu-id="df786-133">A breadboard.</span></span>
* <span data-ttu-id="df786-134">M/M zworek przewodów.</span><span class="sxs-lookup"><span data-stu-id="df786-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a><span data-ttu-id="df786-135">Uzyskuj dostęp do deweloperów operacją ESP8266 hello czujników i komputera</span><span class="sxs-lookup"><span data-stu-id="df786-135">Connect ESP8266 Thing Dev with hello sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a><span data-ttu-id="df786-136">Czujnik temperatury i wilgotności DHT22 połączyć tooESP8266 operacją deweloperów</span><span class="sxs-lookup"><span data-stu-id="df786-136">Connect a DHT22 temperature and humidity sensor tooESP8266 Thing Dev</span></span>

<span data-ttu-id="df786-137">Użyj hello breadboard i zworek przewodów toomake hello połączenia w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="df786-137">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="df786-138">Jeśli nie masz czujnika, Pomiń tę sekcję, ponieważ można użyć danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="df786-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Odwołanie do połączenia](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="df786-140">Dla czujnik numery PIN użyjemy hello następujących połączeń:</span><span class="sxs-lookup"><span data-stu-id="df786-140">For sensor pins, we will use hello following wiring:</span></span>

| <span data-ttu-id="df786-141">Start (czujnik)</span><span class="sxs-lookup"><span data-stu-id="df786-141">Start (Sensor)</span></span>           | <span data-ttu-id="df786-142">Końcowy (tablica)</span><span class="sxs-lookup"><span data-stu-id="df786-142">End (Board)</span></span>           | <span data-ttu-id="df786-143">Kolor kabel</span><span class="sxs-lookup"><span data-stu-id="df786-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="df786-144">VDD (Pin 27F)</span><span class="sxs-lookup"><span data-stu-id="df786-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="df786-145">3V (8A kodu Pin)</span><span class="sxs-lookup"><span data-stu-id="df786-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="df786-146">Czerwony kabel</span><span class="sxs-lookup"><span data-stu-id="df786-146">Red cable</span></span>     |
| <span data-ttu-id="df786-147">DANE (Pin 28F)</span><span class="sxs-lookup"><span data-stu-id="df786-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="df786-148">Interfejs GPIO 2 (9A kodu Pin)</span><span class="sxs-lookup"><span data-stu-id="df786-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="df786-149">Białe kabel</span><span class="sxs-lookup"><span data-stu-id="df786-149">White cable</span></span>    |
| <span data-ttu-id="df786-150">GND (Pin 30F)</span><span class="sxs-lookup"><span data-stu-id="df786-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="df786-151">GND (7J kodu Pin)</span><span class="sxs-lookup"><span data-stu-id="df786-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="df786-152">Czarne kabel</span><span class="sxs-lookup"><span data-stu-id="df786-152">Black cable</span></span>   |


- <span data-ttu-id="df786-153">Aby uzyskać więcej informacji, zobacz: [Instalatora czujnik DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) i [specyfikacji Sparkfun ESP8266 operacją deweloperów](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="df786-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="df786-154">Teraz deweloperów operacją ESP8266 Twojego Sparkfun powinny być połączone z czujnika pracy.</span><span class="sxs-lookup"><span data-stu-id="df786-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![Uzyskuj dht22 ESP8266 operacją deweloperów](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a><span data-ttu-id="df786-156">Podłącz komputer tooyour Sparkfun ESP8266 operacją deweloperów</span><span class="sxs-lookup"><span data-stu-id="df786-156">Connect Sparkfun ESP8266 Thing Dev tooyour computer</span></span>

<span data-ttu-id="df786-157">Użyj hello Micro USB tooType A USB kabel tooconnect deweloperów operacją ESP8266 Sparkfun tooyour komputera w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="df786-157">Use hello Micro USB tooType A USB cable tooconnect Sparkfun ESP8266 Thing Dev tooyour computer as follows.</span></span>

![Podłącz komputer tooyour huzzah piór](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="df786-159">Dodaj uprawnienia portu szeregowego — tylko Ubuntu</span><span class="sxs-lookup"><span data-stu-id="df786-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="df786-160">Jeśli używasz Ubuntu, upewnij się, że zwykłego użytkownika ma toooperate uprawnienia hello na powitania USB portu z Sparkfun ESP8266 operacją odchyleń</span><span class="sxs-lookup"><span data-stu-id="df786-160">If you use Ubuntu, make sure a normal user has hello permissions toooperate on hello USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="df786-161">tooadd portu szeregowego uprawnienia do zwykłego użytkownika, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="df786-161">tooadd serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="df786-162">Uruchom następujące polecenia w terminalu hello:</span><span class="sxs-lookup"><span data-stu-id="df786-162">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="df786-163">Pojawia się jeden z następujących danych wyjściowych hello:</span><span class="sxs-lookup"><span data-stu-id="df786-163">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="df786-164">crw-rw---xxxxxxxx uucp głównego 1</span><span class="sxs-lookup"><span data-stu-id="df786-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="df786-165">crw-rw---xxxxxxxx inicjowania połączeń głównego 1</span><span class="sxs-lookup"><span data-stu-id="df786-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="df786-166">W danych wyjściowych hello zauważyć `uucp` lub `dialout` czyli hello grupy Nazwa właściciela hello portu USB.</span><span class="sxs-lookup"><span data-stu-id="df786-166">In hello output, notice `uucp` or `dialout` that is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="df786-167">Dodaj grupę toohello użytkowników hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="df786-167">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="df786-168">`<group-owner-name>`jest nazwa właściciela grupy hello uzyskanego w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="df786-168">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="df786-169">`<username>`to nazwa użytkownika Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="df786-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="df786-170">Wyloguj się Ubuntu i jego ponowne zalogowanie hello zmiany tootake efektu.</span><span class="sxs-lookup"><span data-stu-id="df786-170">Log out Ubuntu and log in it again for hello change tootake effect.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="df786-171">Zbierać dane czujników oraz wysyłać je tooyour Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="df786-171">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="df786-172">W tej sekcji Wdrażanie i uruchom przykładową aplikację na Sparkfun ESP8266 operacją odchyleń</span><span class="sxs-lookup"><span data-stu-id="df786-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="df786-173">Hello przykładowej aplikacji miganie hello LED na Sparkfun ESP8266 operacją deweloperów i wysyła hello temperatury i wilgotności dane zbierane z hello DHT22 czujnik tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="df786-173">hello sample application blinks hello LED on Sparkfun ESP8266 Thing Dev and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="df786-174">Pobierz hello przykładowej aplikacji z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="df786-174">Get hello sample application from GitHub</span></span>

<span data-ttu-id="df786-175">Witaj przykładowej aplikacji znajduje się w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="df786-175">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="df786-176">Klonuj repozytorium przykładowej hello, zawierający hello przykładowej aplikacji z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="df786-176">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="df786-177">repozytorium przykładowej hello tooclone, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="df786-177">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="df786-178">Otwórz wiersz polecenia lub okno terminalu.</span><span class="sxs-lookup"><span data-stu-id="df786-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="df786-179">Przejdź tooa folder docelowy toobe aplikacji przykładowej hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="df786-179">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="df786-180">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="df786-180">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="df786-181">Instalacja pakietu powitania dla deweloperów operacją ESP8266 Sparkfun w Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="df786-181">Install hello package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="df786-182">Otwórz folder hello przechowywania hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="df786-182">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="df786-183">Otwórz plik app.ino hello w folderze aplikacji hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="df786-183">Open hello app.ino file in hello app folder in Arduino IDE.</span></span>

   ![Otwórz aplikację przykładową hello w arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="df786-185">W hello Arduino IDE, kliknij przycisk **pliku** > **preferencje**.</span><span class="sxs-lookup"><span data-stu-id="df786-185">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="df786-186">W hello **preferencje** okna dialogowego, kliknij przycisk Dalej toohello ikona hello **dodatkowych adresów URL Menedżera tablice** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="df786-186">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="df786-187">W oknie podręcznym hello, wprowadź hello następującego adresu URL, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="df786-187">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![adres url pakietu tooa punktu arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="df786-189">W hello **preferencji** okno dialogowe, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="df786-189">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="df786-190">Kliknij przycisk **narzędzia** > **tablicy** > **Menedżera tablice**, a następnie wyszukaj esp8266.</span><span class="sxs-lookup"><span data-stu-id="df786-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="df786-191">Należy zainstalować ESP8266 przy użyciu wersji 2.2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="df786-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![Pakiet esp8266 Hello jest zainstalowany](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="df786-193">Kliknij przycisk **narzędzia** > **tablicy** > **Sparkfun ESP8266 operacją deweloperów**.</span><span class="sxs-lookup"><span data-stu-id="df786-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="df786-194">Zainstaluj wymagane biblioteki</span><span class="sxs-lookup"><span data-stu-id="df786-194">Install necessary libraries</span></span>

1. <span data-ttu-id="df786-195">W hello Arduino IDE, kliknij przycisk **szkicu** > **obejmują biblioteki** > **zarządzanie bibliotekami**.</span><span class="sxs-lookup"><span data-stu-id="df786-195">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="df786-196">Wyszukiwanie hello następujące nazwy bibliotek jeden po drugim.</span><span class="sxs-lookup"><span data-stu-id="df786-196">Search for hello following library names one by one.</span></span> <span data-ttu-id="df786-197">Dla każdej biblioteki hello możesz znaleźć, kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="df786-197">For each of hello library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="df786-198">Nie masz rzeczywistych czujnik DHT22?</span><span class="sxs-lookup"><span data-stu-id="df786-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="df786-199">Hello przykładowej aplikacji można symulować danych temperatury i wilgotności, w przypadku, gdy nie ma rzeczywistego czujnik DHT22.</span><span class="sxs-lookup"><span data-stu-id="df786-199">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="df786-200">dane toouse symulowane tooenable hello przykładowej aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="df786-200">tooenable hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="df786-201">Otwórz hello `config.h` pliku w hello `app` folderu.</span><span class="sxs-lookup"><span data-stu-id="df786-201">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="df786-202">Znajdź powitania po wierszu kodu i zmień wartość hello z `false` zbyt`true`:</span><span class="sxs-lookup"><span data-stu-id="df786-202">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Konfigurowanie hello przykładowych aplikacji toouse symulowane danych](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="df786-204">Zapisz z `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="df786-204">Save with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a><span data-ttu-id="df786-205">Wdrażanie hello przykładowej aplikacji tooSparkfun ESP8266 operacją deweloperów</span><span class="sxs-lookup"><span data-stu-id="df786-205">Deploy hello sample application tooSparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="df786-206">W hello Arduino IDE, kliknij przycisk **narzędzie** > **portu**, a następnie kliknij przycisk portu szeregowego hello na Sparkfun ESP8266 operacją odchyleń</span><span class="sxs-lookup"><span data-stu-id="df786-206">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="df786-207">Kliknij przycisk **szkicu** > **przekazać** toobuild i wdrażanie hello przykładowej aplikacji tooSparkfun odchyleń operacją ESP8266</span><span class="sxs-lookup"><span data-stu-id="df786-207">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooSparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="df786-208">Jeśli używasz macOS można prawdopodobnie Zobacz hello następujące komunikaty podczas przekazywania.</span><span class="sxs-lookup"><span data-stu-id="df786-208">If you are using macOS you could probably see hello following messages during uploading.</span></span> <span data-ttu-id="df786-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="df786-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="df786-210">Otwórz okno programu ternimal i Zakończ poniżej akcje toosolve ten problem.</span><span class="sxs-lookup"><span data-stu-id="df786-210">Please open your ternimal window and finish below actions toosolve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="df786-211">Wprowadź swoje poświadczenia</span><span class="sxs-lookup"><span data-stu-id="df786-211">Enter your credentials</span></span>

<span data-ttu-id="df786-212">Po pomyślnym ukończeniu przekazywania hello wykonaj tooenter kroki hello poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="df786-212">After hello upload completes successfully, follow hello steps tooenter your credentials:</span></span>

1. <span data-ttu-id="df786-213">W hello Arduino IDE, kliknij przycisk **narzędzia** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="df786-213">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="df786-214">W oknie Monitora serial hello Zwróć uwagę Witaj dwie listy rozwijane na powitania prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="df786-214">In hello serial monitor window, notice hello two drop-down lists on hello bottom right corner.</span></span>
1. <span data-ttu-id="df786-215">Wybierz **nie zakończenia wiersza** powitania po lewej stronie listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="df786-215">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="df786-216">Wybierz **transmisji 115200** dla hello bezpośrednio z listy.</span><span class="sxs-lookup"><span data-stu-id="df786-216">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="df786-217">W polu wejściowym hello znajdujący się u góry okna monitora serial hello hello, wprowadź hello następujących informacji, jeśli zostanie wyświetlona prośba tooprovide je, a następnie kliknij przycisk **wysyłania**.</span><span class="sxs-lookup"><span data-stu-id="df786-217">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="df786-218">Identyfikator SSID sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="df786-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="df786-219">Hasło sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="df786-219">Wi-Fi password</span></span>
   * <span data-ttu-id="df786-220">Ciąg połączenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="df786-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="df786-221">Witaj poświadczeń informacje są przechowywane w pamięci EEPROM z Sparkfun ESP8266 operacją odchyleń hello</span><span class="sxs-lookup"><span data-stu-id="df786-221">hello credential information is stored in hello EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="df786-222">Po kliknięciu przycisku resetowania hello na powitania tablicy Sparkfun ESP8266 operacją deweloperów hello przykładowej aplikacji zapyta, jeśli chcesz uzyskać hello tooerase.</span><span class="sxs-lookup"><span data-stu-id="df786-222">If you click hello reset button on hello Sparkfun ESP8266 Thing Dev board, hello sample application asks you if you want tooerase hello information.</span></span> <span data-ttu-id="df786-223">Wprowadź `Y` informacji hello toohave wymazane, a monit tooprovide hello informacje ponownie.</span><span class="sxs-lookup"><span data-stu-id="df786-223">Enter `Y` toohave hello information erased and you are asked tooprovide hello information again.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="df786-224">Sprawdź, czy hello Przykładowa aplikacja działa prawidłowo</span><span class="sxs-lookup"><span data-stu-id="df786-224">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="df786-225">Jeśli widzisz hello następujące dane wyjściowe z okna monitora serial hello i hello migający LED na Sparkfun ESP8266 operacją deweloperów, hello Przykładowa aplikacja działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="df786-225">If you see hello following output from hello serial monitor window and hello blinking LED on Sparkfun ESP8266 Thing Dev, hello sample application is running successfully.</span></span>

![ostateczne dane wyjściowe w arduino ide](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="df786-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="df786-227">Next steps</span></span>

<span data-ttu-id="df786-228">Pomyślnie połączony z Centrum IoT tooyour Sparkfun ESP8266 operacją deweloperów i wysyłane z Centrum IoT tooyour danych czujnika hello przechwytywane.</span><span class="sxs-lookup"><span data-stu-id="df786-228">You have successfully connected a Sparkfun ESP8266 Thing Dev tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
