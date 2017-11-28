---
title: "toocloud aaaESP8266 — Połącz ESP8266 HUZZAH piór tooAzure Centrum IoT | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toosetup i połącz toosend danych toohello chmury Azure platforma Adafruit piór HUZZAH ESP8266 tooAzure Centrum IoT na jej w tym samouczku."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="62625-103">Połącz tooAzure Adafruit piór HUZZAH ESP8266 Centrum IoT w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="62625-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Połączenie między DHT22 ESP8266 HUZZAH piór i Centrum IoT](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="62625-105">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="62625-105">What you do</span></span>


<span data-ttu-id="62625-106">Połącz Centrum IoT tooan Adafruit piór HUZZAH ESP8266 utworzony.</span><span class="sxs-lookup"><span data-stu-id="62625-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="62625-107">Następnie możesz uruchomić przykładową aplikację na ESP8266 toocollect hello temperatury i wilgotności danych z czujnika DHT22.</span><span class="sxs-lookup"><span data-stu-id="62625-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="62625-108">Ponadto możesz wysłać Centrum IoT tooyour danych czujnika hello.</span><span class="sxs-lookup"><span data-stu-id="62625-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="62625-109">Jeśli używasz innych tablice ESP8266 nadal należy wykonać te kroki tooconnect on tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="62625-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="62625-110">W zależności od tablicy hello ESP8266 używasz, może być konieczne tooreconfigure hello `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="62625-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="62625-111">Na przykład, jeśli używasz ESP8266 z AI Thinker, można zmienić go z `0` zbyt`2`.</span><span class="sxs-lookup"><span data-stu-id="62625-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="62625-112">Nie masz jeszcze zestawu?</span><span class="sxs-lookup"><span data-stu-id="62625-112">Don't have a kit yet?</span></span> <span data-ttu-id="62625-113">Uzyskanie hello [witryny sieci Web Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="62625-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="62625-114">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="62625-114">What you learn</span></span>

* <span data-ttu-id="62625-115">Jak toocreate Centrum IoT i rejestrowanie urządzenia dla ESP8266 HUZZAH piór</span><span class="sxs-lookup"><span data-stu-id="62625-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="62625-116">Jak tooconnect ESP8266 HUZZAH piór z czujnika hello i komputera</span><span class="sxs-lookup"><span data-stu-id="62625-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="62625-117">Jak dane czujników toocollect uruchamiając przykładową aplikację na ESP8266 HUZZAH piór</span><span class="sxs-lookup"><span data-stu-id="62625-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="62625-118">Jak toosend hello Centrum IoT tooyour danych czujnika</span><span class="sxs-lookup"><span data-stu-id="62625-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="62625-119">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="62625-119">What you need</span></span>

![Części potrzebne w samouczku hello](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="62625-121">toocomplete tej operacji, należy po części z Twojej piór HUZZAH ESP8266 Starter Kit hello:</span><span class="sxs-lookup"><span data-stu-id="62625-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="62625-122">Witaj tablicy ESP8266 HUZZAH piór</span><span class="sxs-lookup"><span data-stu-id="62625-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="62625-123">TooType Micro USB kabla A USB</span><span class="sxs-lookup"><span data-stu-id="62625-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="62625-124">Należy również następujące elementy dla środowiska deweloperskiego hello:</span><span class="sxs-lookup"><span data-stu-id="62625-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="62625-125">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="62625-125">An active Azure subscription.</span></span> <span data-ttu-id="62625-126">Jeśli nie masz konta platformy Azure, [utworzyć bezpłatne konto próbne Azure](https://azure.microsoft.com/free/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="62625-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="62625-127">Mac lub komputera z systemem Windows lub Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="62625-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="62625-128">Sieci bezprzewodowej dla tooconnect ESP8266 HUZZAH piór do.</span><span class="sxs-lookup"><span data-stu-id="62625-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="62625-129">Internet połączenia toodownload hello narzędzia do konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="62625-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="62625-130">[Arduino IDE](https://www.arduino.cc/en/main/software) wersji 1.6.8 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="62625-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="62625-131">Starszych wersjach nie działają z hello AzureIoT biblioteki.</span><span class="sxs-lookup"><span data-stu-id="62625-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="62625-132">Witaj następujące elementy są opcjonalne w przypadku, gdy nie masz czujnika.</span><span class="sxs-lookup"><span data-stu-id="62625-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="62625-133">Istnieje również opcja hello przy użyciu danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="62625-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="62625-134">Czujnik temperatury i wilgotności Adafruit DHT22</span><span class="sxs-lookup"><span data-stu-id="62625-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="62625-135">Breadboard</span><span class="sxs-lookup"><span data-stu-id="62625-135">A breadboard</span></span>
* <span data-ttu-id="62625-136">Przewodów zworek M/M</span><span class="sxs-lookup"><span data-stu-id="62625-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="62625-137">Uzyskuj dostęp do ESP8266 HUZZAH piór hello czujników i komputera</span><span class="sxs-lookup"><span data-stu-id="62625-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="62625-138">W tej sekcji można podłączyć hello czujników tooyour tablicy.</span><span class="sxs-lookup"><span data-stu-id="62625-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="62625-139">Następnie podłącz w komputerze tooyour urządzenia dla dalszego użytku.</span><span class="sxs-lookup"><span data-stu-id="62625-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="62625-140">Połącz DHT22 temperatury i wilgotności czujnik tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="62625-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="62625-141">Użyj hello breadboard i zworek przewodów toomake hello połączenia w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="62625-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="62625-142">Jeśli nie masz czujnika, Pomiń tę sekcję, ponieważ można użyć danych czujnika symulowane.</span><span class="sxs-lookup"><span data-stu-id="62625-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Odwołanie do połączenia](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="62625-144">Czujnik numery PIN użyć hello następujących połączeń:</span><span class="sxs-lookup"><span data-stu-id="62625-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="62625-145">Start (czujnik)</span><span class="sxs-lookup"><span data-stu-id="62625-145">Start (Sensor)</span></span>           | <span data-ttu-id="62625-146">Końcowy (tablica)</span><span class="sxs-lookup"><span data-stu-id="62625-146">End (Board)</span></span>           | <span data-ttu-id="62625-147">Kolor kabel</span><span class="sxs-lookup"><span data-stu-id="62625-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="62625-148">VDD (Pin 31F)</span><span class="sxs-lookup"><span data-stu-id="62625-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="62625-149">3V (przypiąć 58H)</span><span class="sxs-lookup"><span data-stu-id="62625-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="62625-150">Czerwony kabel</span><span class="sxs-lookup"><span data-stu-id="62625-150">Red cable</span></span>     |
| <span data-ttu-id="62625-151">DANE (Pin 32F)</span><span class="sxs-lookup"><span data-stu-id="62625-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="62625-152">Interfejs GPIO 2 (Pin 46A)</span><span class="sxs-lookup"><span data-stu-id="62625-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="62625-153">Niebieski kabel</span><span class="sxs-lookup"><span data-stu-id="62625-153">Blue cable</span></span>    |
| <span data-ttu-id="62625-154">GND (Pin 34F)</span><span class="sxs-lookup"><span data-stu-id="62625-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="62625-155">GND (PIn 56I)</span><span class="sxs-lookup"><span data-stu-id="62625-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="62625-156">Czarne kabel</span><span class="sxs-lookup"><span data-stu-id="62625-156">Black cable</span></span>   |

<span data-ttu-id="62625-157">Aby uzyskać więcej informacji, zobacz [Instalatora czujnik Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) i [wyprowadzenia Adafruit piór HUZZAH Esp8266 styków](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="62625-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="62625-158">Teraz ESP8266 Huzzah Twojego piór powinny być połączone z czujnika pracy.</span><span class="sxs-lookup"><span data-stu-id="62625-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Uzyskuj DHT22 Huzzah piór](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="62625-160">Podłącz komputer tooyour ESP8266 HUZZAH piór</span><span class="sxs-lookup"><span data-stu-id="62625-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="62625-161">Jak pokazano w następnym, należy użyć hello Micro USB tooType A USB kabel tooconnect ESP8266 HUZZAH piór tooyour komputera.</span><span class="sxs-lookup"><span data-stu-id="62625-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![Podłącz komputer tooyour Huzzah piór](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="62625-163">Dodaj uprawnienia portu szeregowego (tylko Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="62625-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="62625-164">Jeśli używasz Ubuntu, upewnij się, że masz toooperate uprawnienia hello na powitania USB portu z piór HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="62625-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="62625-165">tooadd uprawnienia portu szeregowego, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="62625-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="62625-166">Uruchom następujące polecenia w terminalu hello:</span><span class="sxs-lookup"><span data-stu-id="62625-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="62625-167">Pojawia się jeden z następujących danych wyjściowych hello:</span><span class="sxs-lookup"><span data-stu-id="62625-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="62625-168">crw-rw---xxxxxxxx uucp głównego 1</span><span class="sxs-lookup"><span data-stu-id="62625-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="62625-169">crw-rw---xxxxxxxx inicjowania połączeń głównego 1</span><span class="sxs-lookup"><span data-stu-id="62625-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="62625-170">W danych wyjściowych hello, zwróć uwagę, że `uucp` lub `dialout` jest nazwa właściciela grupy hello hello portu USB.</span><span class="sxs-lookup"><span data-stu-id="62625-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="62625-171">Dodaj grupę toohello użytkowników hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="62625-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="62625-172">`<group-owner-name>`jest nazwa właściciela grupy hello uzyskanego w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="62625-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="62625-173">`<username>`to nazwa użytkownika Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="62625-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="62625-174">Wylogować się z Ubuntu, a następnie zaloguj ponownie na powitania tooappear zmiany.</span><span class="sxs-lookup"><span data-stu-id="62625-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="62625-175">Zbierać dane czujników oraz wysyłać je tooyour Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="62625-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="62625-176">W tej sekcji Wdróż i uruchom przykładową aplikację na ESP8266 HUZZAH piór.</span><span class="sxs-lookup"><span data-stu-id="62625-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="62625-177">Hello przykładowej aplikacji miganie hello LED na ESP8266 HUZZAH piór i wysyła hello temperatury i wilgotności dane zbierane z hello DHT22 czujnik tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="62625-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="62625-178">Pobierz hello przykładowej aplikacji z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="62625-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="62625-179">Witaj przykładowej aplikacji znajduje się w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="62625-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="62625-180">Klonuj repozytorium przykładowej hello, zawierający hello przykładowej aplikacji z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="62625-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="62625-181">repozytorium przykładowej hello tooclone, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="62625-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="62625-182">Otwórz wiersz polecenia lub okno terminalu.</span><span class="sxs-lookup"><span data-stu-id="62625-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="62625-183">Przejdź tooa folder docelowy toobe aplikacji przykładowej hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="62625-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="62625-184">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="62625-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="62625-185">Instalacja pakietu powitania dla ESP8266 HUZZAH piór w Arduino IDE hello:</span><span class="sxs-lookup"><span data-stu-id="62625-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="62625-186">Otwórz folder hello przechowywania hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62625-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="62625-187">Otwórz plik app.ino hello w folderze aplikacji hello hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="62625-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Otwórz aplikację przykładową hello w Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="62625-189">W hello Arduino IDE, kliknij przycisk **pliku** > **preferencje**.</span><span class="sxs-lookup"><span data-stu-id="62625-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="62625-190">W hello **preferencje** okna dialogowego, kliknij przycisk Dalej toohello ikona hello **dodatkowych adresów URL Menedżera tablice** pole.</span><span class="sxs-lookup"><span data-stu-id="62625-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="62625-191">W oknie podręcznym hello, wprowadź hello następującego adresu URL, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="62625-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Adres url pakietu tooa punktu Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="62625-193">W hello **preferencji** okno dialogowe, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="62625-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="62625-194">Kliknij przycisk **narzędzia** > **tablicy** > **Menedżera tablice**, a następnie wyszukaj esp8266.</span><span class="sxs-lookup"><span data-stu-id="62625-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="62625-195">Tablice Menedżera wskazuje, że ESP8266 przy użyciu wersji 2.2.0 lub nowszej jest zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="62625-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Pakiet esp8266 Hello jest zainstalowany](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="62625-197">Kliknij przycisk **narzędzia** > **tablicy** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="62625-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="62625-198">Zainstaluj wymagane biblioteki</span><span class="sxs-lookup"><span data-stu-id="62625-198">Install necessary libraries</span></span>

1. <span data-ttu-id="62625-199">W hello Arduino IDE, kliknij przycisk **szkicu** > **obejmują biblioteki** > **zarządzanie bibliotekami**.</span><span class="sxs-lookup"><span data-stu-id="62625-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="62625-200">Wyszukiwanie hello następujące nazwy bibliotek jeden po drugim.</span><span class="sxs-lookup"><span data-stu-id="62625-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="62625-201">Dla każdej biblioteki można znaleźć, kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="62625-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="62625-202">Nie masz rzeczywistych czujnik DHT22?</span><span class="sxs-lookup"><span data-stu-id="62625-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="62625-203">Hello przykładowej aplikacji można symulować danych temperatury i wilgotności, w przypadku, gdy nie ma rzeczywistego czujnik DHT22.</span><span class="sxs-lookup"><span data-stu-id="62625-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="62625-204">tooset zapasowych danych toouse symulowane hello przykładowej aplikacji, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="62625-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="62625-205">Otwórz hello `config.h` pliku w hello `app` folderu.</span><span class="sxs-lookup"><span data-stu-id="62625-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="62625-206">Znajdź powitania po wierszu kodu i zmień wartość hello z `false` zbyt`true`:</span><span class="sxs-lookup"><span data-stu-id="62625-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Konfigurowanie hello przykładowych aplikacji toouse symulowane danych](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="62625-208">Zapisz plik hello z `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="62625-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="62625-209">Wdrażanie hello przykładowej aplikacji tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="62625-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="62625-210">W hello Arduino IDE, kliknij przycisk **narzędzie** > **portu**, a następnie kliknij przycisk portu szeregowego hello ESP8266 HUZZAH piór.</span><span class="sxs-lookup"><span data-stu-id="62625-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="62625-211">Kliknij przycisk **szkicu** > **przekazać** toobuild i wdrażanie hello przykładowej aplikacji tooFeather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="62625-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="62625-212">Wprowadź swoje poświadczenia</span><span class="sxs-lookup"><span data-stu-id="62625-212">Enter your credentials</span></span>

<span data-ttu-id="62625-213">Po pomyślnym ukończeniu przekazywania hello wykonaj te kroki tooenter poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="62625-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="62625-214">W hello Arduino IDE, kliknij przycisk **narzędzia** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="62625-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="62625-215">W oknie Monitora serial hello Zwróć uwagę hello dwóch list rozwijanych w hello prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="62625-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="62625-216">Wybierz **nie zakończenia wiersza** powitania po lewej stronie listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="62625-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="62625-217">Wybierz **transmisji 115200** dla hello bezpośrednio z listy.</span><span class="sxs-lookup"><span data-stu-id="62625-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="62625-218">W polu wejściowym hello znajdujący się u góry okna monitora serial hello hello, wprowadź hello następujących informacji, jeśli zostanie wyświetlona prośba tooprovide je, a następnie kliknij przycisk **wysyłania**.</span><span class="sxs-lookup"><span data-stu-id="62625-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="62625-219">Identyfikator SSID sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="62625-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="62625-220">Hasło sieci Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="62625-220">Wi-Fi password</span></span>
   * <span data-ttu-id="62625-221">Ciąg połączenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="62625-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="62625-222">informacje poświadczeń Hello są przechowywane w pamięci EEPROM piór HUZZAH ESP8266 hello.</span><span class="sxs-lookup"><span data-stu-id="62625-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="62625-223">Jeśli klikniesz przycisk reset hello na powitania tablicy ESP8266 HUZZAH piór hello przykładowej aplikacji pyta użytkownika tooerase hello informacji.</span><span class="sxs-lookup"><span data-stu-id="62625-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="62625-224">Wprowadź `Y` informacji hello toohave wymazane.</span><span class="sxs-lookup"><span data-stu-id="62625-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="62625-225">Zostanie wyświetlona prośba tooprovide hello informacji po raz drugi.</span><span class="sxs-lookup"><span data-stu-id="62625-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="62625-226">Sprawdź, czy hello Przykładowa aplikacja działa prawidłowo</span><span class="sxs-lookup"><span data-stu-id="62625-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="62625-227">Jeśli widzisz hello następujące dane wyjściowe z okna monitora serial hello i hello migający LED na piór HUZZAH ESP8266, hello Przykładowa aplikacja działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="62625-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Ostateczne dane wyjściowe w Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="62625-229">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62625-229">Next steps</span></span>

<span data-ttu-id="62625-230">Pomyślnie połączony z Centrum IoT tooyour ESP8266 HUZZAH piór i wysyłane z Centrum IoT tooyour danych czujnika hello przechwytywane.</span><span class="sxs-lookup"><span data-stu-id="62625-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

