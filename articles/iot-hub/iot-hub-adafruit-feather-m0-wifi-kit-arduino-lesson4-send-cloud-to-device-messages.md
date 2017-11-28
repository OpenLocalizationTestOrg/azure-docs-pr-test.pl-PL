---
title: "Connect Arduino (C) tooAzure IoT - 4 lekcji: chmury do urządzenia | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja działa na komunikaty przychodzące Adafruit piór M0 sieci Wi-Fi i monitorów z Centrum IoT. Nowe zadanie gulp wysyła komunikaty tooAdafruit M0 piór sieci Wi-Fi z Twojej hello tooblink Centrum IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Formant arduino doprowadziły z sieci web, kontroli arduino przeprowadzony za pośrednictwem sieci web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="57729-105">Uruchom tooreceive aplikacji przykładowej wiadomości chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="57729-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="57729-106">W tym artykule na tablicy Adafruit piór M0 sieci Wi-Fi Arduino wdrażania przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="57729-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="57729-107">aplikacja przykładowa Hello monitoruje komunikaty przychodzące z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="57729-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="57729-108">Można również uruchomić zadanie gulp na tooyour wiadomości tablicy Arduino Twojego komputera toosend z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="57729-108">You also run a gulp task on your computer toosend messages tooyour Arduino board from your IoT hub.</span></span> <span data-ttu-id="57729-109">Gdy hello Przykładowa aplikacja odbiera wiadomości powitania, miga hello LED.</span><span class="sxs-lookup"><span data-stu-id="57729-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="57729-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="57729-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="57729-111">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="57729-111">What you will do</span></span>
* <span data-ttu-id="57729-112">Połącz Centrum IoT tooyour hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="57729-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="57729-113">Wdrażanie i uruchamianie hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="57729-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="57729-114">Wysyłanie wiadomości z Twojej IoT hub tooyour Arduino tablicy tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="57729-114">Send messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="57729-115">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="57729-115">What you will learn</span></span>
<span data-ttu-id="57729-116">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="57729-116">In this article, you will learn:</span></span>
* <span data-ttu-id="57729-117">Jak komunikaty przychodzące toomonitor z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="57729-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="57729-118">Jak chmury urządzenia toosend komunikaty z sieci tooyour Centrum IoT Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="57729-118">How toosend cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="57729-119">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="57729-119">What you need</span></span>
* <span data-ttu-id="57729-120">Tablicy Arduino, skonfigurować do używania.</span><span class="sxs-lookup"><span data-stu-id="57729-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="57729-121">toolearn tooset się tablicy Arduino, zobacz temat [Skonfiguruj urządzenie][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="57729-121">toolearn how tooset up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="57729-122">Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57729-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="57729-123">toolearn jak toocreate Centrum IoT, zobacz [utworzenie Centrum IoT Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="57729-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="57729-124">Połącz z Centrum IoT tooyour hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="57729-124">Connect hello sample application tooyour IoT hub</span></span>

1. <span data-ttu-id="57729-125">Upewnij się, że jesteś w folderze repozytorium hello `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="57729-125">Make sure that you're in hello repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="57729-126">Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="57729-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="57729-127">Powiadomienie hello `app.ino` pliku w hello `app` podfolderu.</span><span class="sxs-lookup"><span data-stu-id="57729-127">Notice hello `app.ino` file in hello `app` subfolder.</span></span> <span data-ttu-id="57729-128">Witaj `app.ino` plik jest plikiem klucza źródła hello, zawierający hello kodu toomonitor komunikaty przychodzące hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="57729-128">hello `app.ino` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="57729-129">Witaj `blinkLED` funkcja miganie hello LED.</span><span class="sxs-lookup"><span data-stu-id="57729-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Struktura repozytorium w hello przykładowej aplikacji][repo-structure]

2. <span data-ttu-id="57729-131">Uzyskaj hello portu szeregowego hello urządzenia z hello urządzenia odnajdywania interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="57729-131">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="57729-132">Należy wyświetlone informacje podobne następujących toohello i Znajdź hello usb COM port tablicy Arduino:</span><span class="sxs-lookup"><span data-stu-id="57729-132">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Odnajdywanie urządzeń][device-discovery]

3. <span data-ttu-id="57729-134">Witaj Otwórz plik `config.json` w folderze lekcji hello i wartości wejściowych hello hello znaleziono numer portu COM:</span><span class="sxs-lookup"><span data-stu-id="57729-134">Open hello file `config.json` in hello lesson folder and input hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > <span data-ttu-id="57729-136">Dla portu hello COM, na platformie systemu Windows ma hello format `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="57729-136">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="57729-137">System macOS lub Ubuntu zostanie rozpoczęty z `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="57729-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="57729-138">Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="57729-138">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="57729-139">Wprowadź następujące elementy zastępcze w hello hello `config-arduino.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="57729-139">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   <span data-ttu-id="57729-140">Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na tym komputerze, wszystkie konfiguracje hello są dziedziczone, można pominąć hello krok toohello zadania wdrażania i uruchomiona hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="57729-140">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="57729-141">Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na innym komputerze, należy symbole zastępcze hello tooreplace w hello `config-arduino.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="57729-141">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-arduino.json` file.</span></span> <span data-ttu-id="57729-142">Witaj `config-arduino.json` plik znajduje się w podfolderze hello folderu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="57729-142">hello `config-arduino.json` file is in hello subfolder of your home folder.</span></span>

   ![Zawartość pliku config arduino.json hello][config-arduino-json]

   * <span data-ttu-id="57729-144">Zastąp **[SSID sieci Wi-Fi]** o identyfikatorze SSID sieci Wi-Fi, który połączony toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="57729-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="57729-145">Zastąp **[sieci Wi-Fi hasło]** hasła sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="57729-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="57729-146">Jeśli sieci Wi-Fi nie wymagają hasła, należy usunąć ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="57729-146">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="57729-147">Zastąp **[parametry połączenia urządzenia IoT]** z hello parametry połączenia urządzenia, które można uzyskać, uruchamiając hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="57729-147">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="57729-148">Zastąp **[parametry połączenia Centrum IoT]** z hello parametry połączenia Centrum IoT, które można uzyskać, uruchamiając hello `az iot hub show-connection-string --name {my hub name}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="57729-148">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="57729-149">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="57729-149">Deploy and run hello sample application</span></span>
<span data-ttu-id="57729-150">Wdrażanie i uruchamianie aplikacji przykładowej hello na tablicy Arduino, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="57729-150">Deploy and run hello sample application on your Arduino board by running hello following commands:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="57729-151">polecenie gulp Hello wdraża hello przykładowej aplikacji tooyour Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="57729-151">hello gulp command deploys hello sample application tooyour Arduino board.</span></span> <span data-ttu-id="57729-152">Następnie uruchomieniu aplikacji hello na tablicy Arduino i oddzielnych zadań na hoście komputera toosend 20 migania wiadomości tooyour Arduino tablicy z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="57729-152">Then, it runs hello application on your Arduino board and a separate task on your host computer toosend 20 blink messages tooyour Arduino board from your IoT hub.</span></span>

<span data-ttu-id="57729-153">Po uruchomieniu aplikacji przykładowej hello rozpoczyna nasłuchiwanie toomessages z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="57729-153">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="57729-154">W tym samym czasie hello gulp zadań wysyła komunikaty "blink" z Twojej tooyour Centrum IoT Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="57729-154">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="57729-155">Dla każdej wiadomości migania hello tablicy odbiera, hello przykładowej aplikacji wywołuje hello `blinkLED` funkcja tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="57729-155">For each blink message that hello board receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="57729-156">Powinny pojawić się hello LED blink co dwie sekundy zadań gulp hello wyśle 20 komunikatów z Twojej tooyour Centrum IoT Arduino tablicy.</span><span class="sxs-lookup"><span data-stu-id="57729-156">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="57729-157">Hello ostatnio jedna jest zatrzymuje aplikacji hello komunikat "stop".</span><span class="sxs-lookup"><span data-stu-id="57729-157">hello last one is a "stop" message that stops hello application from running.</span></span>

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości][sample-application]

## <a name="summary"></a><span data-ttu-id="57729-159">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="57729-159">Summary</span></span>
<span data-ttu-id="57729-160">Zostało pomyślnie wysłane wiadomości z Twojej IoT hub tooyour Arduino tablicy tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="57729-160">You’ve successfully sent messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="57729-161">następne zadanie Hello jest opcjonalny: Zmień hello włączać i wyłączać zachowanie hello LED.</span><span class="sxs-lookup"><span data-stu-id="57729-161">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57729-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57729-162">Next steps</span></span>
<span data-ttu-id="57729-163">[Zmień hello włączać i wyłączać zachowanie hello LED][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="57729-163">[Change hello on and off behavior of hello LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md