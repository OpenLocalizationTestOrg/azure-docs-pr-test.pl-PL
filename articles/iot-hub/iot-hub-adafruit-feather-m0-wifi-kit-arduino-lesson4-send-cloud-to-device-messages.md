---
title: "Nawiązać Arduino (C) Azure IoT — lekcji 4: chmury do urządzenia | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja działa na komunikaty przychodzące Adafruit piór M0 sieci Wi-Fi i monitorów z Centrum IoT. Nowe zadanie gulp wysyła komunikaty do Adafruit piór M0 sieci Wi-Fi z Centrum IoT miga LED."
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
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="de6d4-105">Uruchom przykładową aplikację do odbierania wiadomości chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="de6d4-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="de6d4-106">W tym artykule na tablicy Adafruit piór M0 sieci Wi-Fi Arduino wdrażania przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de6d4-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="de6d4-107">Przykładowa aplikacja monitoruje komunikaty przychodzące z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="de6d4-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="de6d4-108">Można również uruchomić zadanie gulp na komputerze do wysyłania komunikatów do tablicy Arduino z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="de6d4-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span></span> <span data-ttu-id="de6d4-109">Gdy przykładowa aplikacja odbiera komunikaty, miga LED.</span><span class="sxs-lookup"><span data-stu-id="de6d4-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="de6d4-110">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="de6d4-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="de6d4-111">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="de6d4-111">What you will do</span></span>
* <span data-ttu-id="de6d4-112">Połącz przykładowej aplikacji do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="de6d4-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="de6d4-113">Wdrażanie i uruchamianie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de6d4-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="de6d4-114">Wysyłanie wiadomości z Centrum IoT do tablicy Arduino miga LED.</span><span class="sxs-lookup"><span data-stu-id="de6d4-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="de6d4-115">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="de6d4-115">What you will learn</span></span>
<span data-ttu-id="de6d4-116">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="de6d4-116">In this article, you will learn:</span></span>
* <span data-ttu-id="de6d4-117">Jak monitorować komunikaty przychodzące z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="de6d4-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="de6d4-118">Sposób wysyłania komunikatów chmury do urządzenia z Centrum IoT do tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="de6d4-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="de6d4-119">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="de6d4-119">What you need</span></span>
* <span data-ttu-id="de6d4-120">Tablicy Arduino, skonfigurować do używania.</span><span class="sxs-lookup"><span data-stu-id="de6d4-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="de6d4-121">Aby dowiedzieć się, jak skonfigurować tablicy Arduino, zobacz [Skonfiguruj urządzenie][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="de6d4-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="de6d4-122">Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="de6d4-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="de6d4-123">Aby dowiedzieć się, jak utworzyć Centrum IoT, zobacz [utworzenie Centrum IoT Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="de6d4-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="de6d4-124">Połącz przykładowej aplikacji do Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="de6d4-124">Connect the sample application to your IoT hub</span></span>

1. <span data-ttu-id="de6d4-125">Upewnij się, że jesteś w folderze repozytorium `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="de6d4-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="de6d4-126">Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="de6d4-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="de6d4-127">Powiadomienie `app.ino` w pliku `app` podfolderu.</span><span class="sxs-lookup"><span data-stu-id="de6d4-127">Notice the `app.ino` file in the `app` subfolder.</span></span> <span data-ttu-id="de6d4-128">`app.ino` Plik jest plikiem źródła klucza, który zawiera kod umożliwiający monitorowanie komunikatów przychodzących z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="de6d4-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="de6d4-129">`blinkLED` LED miga funkcji.</span><span class="sxs-lookup"><span data-stu-id="de6d4-129">The `blinkLED` function blinks the LED.</span></span>

   ![Struktura repozytorium w przykładowej aplikacji][repo-structure]

2. <span data-ttu-id="de6d4-131">Uzyskaj portu szeregowego urządzenia z odnajdywania urządzenia interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="de6d4-131">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="de6d4-132">Należy wyświetlić dane wyjściowe podobne do następujących i Znajdź usb COM port tablicy Arduino:</span><span class="sxs-lookup"><span data-stu-id="de6d4-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Odnajdywanie urządzeń][device-discovery]

3. <span data-ttu-id="de6d4-134">Otwórz plik `config.json` w folderze lekcji i dane wejściowe wartość znaleziony numer portu COM:</span><span class="sxs-lookup"><span data-stu-id="de6d4-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > <span data-ttu-id="de6d4-136">Dla portu COM na platformie systemu Windows ma format `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="de6d4-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="de6d4-137">System macOS lub Ubuntu zostanie rozpoczęty z `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="de6d4-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="de6d4-138">Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="de6d4-138">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="de6d4-139">Wprowadź następujące elementy zastępcze w `config-arduino.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="de6d4-139">Make the following replacements in the `config-arduino.json` file:</span></span>

   <span data-ttu-id="de6d4-140">Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na tym komputerze, wszystkie konfiguracje są dziedziczone, można pominąć krok do zadania, wdrażanie i uruchamianie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="de6d4-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="de6d4-141">Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na innym komputerze, należy zastąpić symbole zastępcze w `config-arduino.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="de6d4-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span></span> <span data-ttu-id="de6d4-142">`config-arduino.json` Plik znajduje się w podfolderze folderu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="de6d4-142">The `config-arduino.json` file is in the subfolder of your home folder.</span></span>

   ![Zawartość pliku konfiguracji arduino.json][config-arduino-json]

   * <span data-ttu-id="de6d4-144">Zastąp **[SSID sieci Wi-Fi]** o identyfikatorze SSID sieci Wi-Fi, który jest połączony z Internetem.</span><span class="sxs-lookup"><span data-stu-id="de6d4-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="de6d4-145">Zastąp **[sieci Wi-Fi hasło]** hasła sieci Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="de6d4-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="de6d4-146">Jeśli sieci Wi-Fi nie wymagają hasła, należy usunąć ciąg.</span><span class="sxs-lookup"><span data-stu-id="de6d4-146">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="de6d4-147">Zastąp **[parametry połączenia urządzenia IoT]** z parametrami połączenia urządzenia, który można uzyskać, uruchamiając `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="de6d4-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="de6d4-148">Zastąp **[parametry połączenia Centrum IoT]** z parametrami połączenia Centrum IoT, który można uzyskać, uruchamiając `az iot hub show-connection-string --name {my hub name}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="de6d4-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="de6d4-149">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="de6d4-149">Deploy and run the sample application</span></span>
<span data-ttu-id="de6d4-150">Wdrażanie i uruchamianie przykładowej aplikacji na tablicy Arduino, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="de6d4-150">Deploy and run the sample application on your Arduino board by running the following commands:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="de6d4-151">Polecenie gulp wdraża przykładowej aplikacji do tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="de6d4-151">The gulp command deploys the sample application to your Arduino board.</span></span> <span data-ttu-id="de6d4-152">Następnie uruchomi aplikację na tablicy Arduino i oddzielnych zadań na komputerze hosta do wysyłania wiadomości migania 20 do tablicy Arduino z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="de6d4-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span></span>

<span data-ttu-id="de6d4-153">Po uruchomieniu aplikacji przykładowej, rozpoczyna nasłuchiwanie wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="de6d4-153">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="de6d4-154">W tym samym czasie zadań gulp wysyła komunikaty "blink" z Centrum IoT do tablicy Arduino.</span><span class="sxs-lookup"><span data-stu-id="de6d4-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="de6d4-155">Dla każdego komunikatu migania odbierająca tablicy wywołuje przykładowej aplikacji `blinkLED` funkcja miga LED.</span><span class="sxs-lookup"><span data-stu-id="de6d4-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="de6d4-156">Zadanie gulp wyśle 20 komunikatów z Centrum IoT do tablicy Arduino powinna zostać wyświetlona migania LED co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="de6d4-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="de6d4-157">Komunikat "stop", która kończy działanie aplikacji jest ostatni z nich.</span><span class="sxs-lookup"><span data-stu-id="de6d4-157">The last one is a "stop" message that stops the application from running.</span></span>

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości][sample-application]

## <a name="summary"></a><span data-ttu-id="de6d4-159">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="de6d4-159">Summary</span></span>
<span data-ttu-id="de6d4-160">Na tablicy Arduino miga LED zostało pomyślnie wysłane wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="de6d4-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span></span> <span data-ttu-id="de6d4-161">Następne zadanie jest opcjonalne: Zmień włączenia i wyłączenia zachowanie LED.</span><span class="sxs-lookup"><span data-stu-id="de6d4-161">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de6d4-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="de6d4-162">Next steps</span></span>
<span data-ttu-id="de6d4-163">[Zmień włączenia i wyłączenia zachowanie LED][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="de6d4-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span></span>


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