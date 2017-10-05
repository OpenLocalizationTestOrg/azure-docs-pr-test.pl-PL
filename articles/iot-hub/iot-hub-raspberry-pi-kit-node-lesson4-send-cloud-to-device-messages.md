---
featureFlags: usabilla
title: "Pi malinowe (węzeł) nawiązania połączenia platformy Azure IoT — lekcji 4: chmury do urządzenia | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja działa na Pi i monitoruje komunikaty przychodzące z Centrum IoT. Nowe zadanie gulp wysyła komunikaty do Pi z Centrum IoT miga LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "chmury do urządzenia, wiadomości z chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b8e9e51391f9b6737762b3404658297ab4c82783
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-the-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="5454d-105">Uruchom przykładową aplikację do odbierania wiadomości chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="5454d-105">Run the sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="5454d-106">W tym artykule wdrożono przykładową aplikację na malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="5454d-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="5454d-107">Przykładowa aplikacja monitoruje komunikaty przychodzące z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5454d-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="5454d-108">Można również uruchomić zadanie gulp na komputerze do wysyłania komunikatów do Pi z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5454d-108">You also run a gulp task on your computer to send messages to Pi from your IoT hub.</span></span> <span data-ttu-id="5454d-109">Gdy przykładowa aplikacja odbiera komunikaty, miga LED.</span><span class="sxs-lookup"><span data-stu-id="5454d-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="5454d-110">Jeśli masz problemy z poszukiwanie rozwiązania na [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5454d-110">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5454d-111">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="5454d-111">What you will do</span></span>
* <span data-ttu-id="5454d-112">Połącz przykładowej aplikacji do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5454d-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="5454d-113">Wdrażanie i uruchamianie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5454d-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="5454d-114">Wysyłanie wiadomości z Centrum IoT do Pi miga LED.</span><span class="sxs-lookup"><span data-stu-id="5454d-114">Send messages from your IoT hub to Pi to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5454d-115">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="5454d-115">What you will learn</span></span>
<span data-ttu-id="5454d-116">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="5454d-116">In this article, you will learn:</span></span>
* <span data-ttu-id="5454d-117">Jak monitorować komunikaty przychodzące z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="5454d-117">How to monitor incoming messages from your IoT hub</span></span>
* <span data-ttu-id="5454d-118">Sposób wysyłania komunikatów chmury do urządzenia z Centrum IoT do Pi.</span><span class="sxs-lookup"><span data-stu-id="5454d-118">How to send cloud-to-device messages from your IoT hub to Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5454d-119">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="5454d-119">What you need</span></span>
* <span data-ttu-id="5454d-120">Malinowe Pi 3, skonfigurować do używania.</span><span class="sxs-lookup"><span data-stu-id="5454d-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="5454d-121">Aby dowiedzieć się, jak skonfigurować Pi, zobacz [Skonfiguruj urządzenie](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="5454d-121">To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="5454d-122">Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5454d-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="5454d-123">Aby dowiedzieć się, jak utworzyć Centrum IoT, zobacz [utworzenie Centrum IoT i zarejestruj malina Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="5454d-123">To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="5454d-124">Połącz przykładowej aplikacji do Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="5454d-124">Connect the sample application to your IoT hub</span></span>
1. <span data-ttu-id="5454d-125">Upewnij się, że jesteś w folderze repozytorium `iot-hub-node-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="5454d-125">Make sure that you're in the repo folder `iot-hub-node-raspberrypi-getting-started`.</span></span> <span data-ttu-id="5454d-126">Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="5454d-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
   
   <span data-ttu-id="5454d-127">Powiadomienie `app.js` w pliku `app` podfolderu.</span><span class="sxs-lookup"><span data-stu-id="5454d-127">Notice the `app.js` file in the `app` subfolder.</span></span> <span data-ttu-id="5454d-128">`app.js` Plik jest plikiem źródła klucza, który zawiera kod umożliwiający monitorowanie komunikatów przychodzących z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5454d-128">The `app.js` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="5454d-129">`blinkLED` LED miga funkcji.</span><span class="sxs-lookup"><span data-stu-id="5454d-129">The `blinkLED` function blinks the LED.</span></span>
   
   ![Struktura repozytorium w przykładowej aplikacji](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. <span data-ttu-id="5454d-131">Inicjowanie pliku konfiguracji za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="5454d-131">Initialize the configuration file by using the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
   
   <span data-ttu-id="5454d-132">Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) na tym komputerze są dziedziczone wszystkie konfiguracje, więc możesz przejść do zadań, wdrażanie i uruchamianie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5454d-132">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to the task of deploying and running the sample application.</span></span> <span data-ttu-id="5454d-133">Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) na innym komputerze, należy zastąpić symbole zastępcze w `config-raspberrypi.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="5454d-133">If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file.</span></span> <span data-ttu-id="5454d-134">`config-raspberrypi.json` Plik znajduje się w podfolderze folderu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="5454d-134">The `config-raspberrypi.json` file is in the subfolder of your home folder.</span></span>
   
   ![Zawartość pliku konfiguracji raspberrypi.json](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="5454d-136">Zastąp **[urządzenia nazwa hosta lub adres IP]** o adresie IP Pi lub nazwę hosta, który można uzyskać, uruchamiając `devdisco list --eth` polecenia.</span><span class="sxs-lookup"><span data-stu-id="5454d-136">Replace **[device hostname or IP address]** with the IP address of Pi or the host name that you get by running the `devdisco list --eth` command.</span></span>
* <span data-ttu-id="5454d-137">Zastąp **[parametry połączenia urządzenia IoT]** z parametrami połączenia urządzenia, który można uzyskać, uruchamiając `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="5454d-137">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="5454d-138">Zastąp **[parametry połączenia Centrum IoT]** z parametrami połączenia Centrum IoT, który można uzyskać, uruchamiając `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="5454d-138">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="5454d-139">Uruchom **system gulp instalacji narzędzia** oraz, jeśli nie zostało to jeszcze zrobione, Lekcja 1.</span><span class="sxs-lookup"><span data-stu-id="5454d-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="5454d-140">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="5454d-140">Deploy and run the sample application</span></span>
<span data-ttu-id="5454d-141">Wdrażanie i uruchamianie przykładowej aplikacji na Pi, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5454d-141">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="5454d-142">Polecenie wdraża przykładowej aplikacji do Pi.</span><span class="sxs-lookup"><span data-stu-id="5454d-142">The command deploys the sample application to Pi.</span></span> <span data-ttu-id="5454d-143">Następnie uruchomi aplikację na Pi i oddzielnych zadań na komputerze hosta do wysyłania wiadomości migania 20 do Pi z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5454d-143">Then, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.</span></span>

<span data-ttu-id="5454d-144">Po uruchomieniu aplikacji przykładowej, rozpoczyna nasłuchiwanie wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5454d-144">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="5454d-145">W tym samym czasie zadań gulp wysyła kilka "blink" wiadomości z Centrum IoT do Pi.</span><span class="sxs-lookup"><span data-stu-id="5454d-145">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi.</span></span> <span data-ttu-id="5454d-146">Dla każdego komunikatu migania odbierająca Pi wywołuje przykładowej aplikacji `blinkLED` funkcja miga LED.</span><span class="sxs-lookup"><span data-stu-id="5454d-146">For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="5454d-147">Powinny pojawić się migania LED co dwie sekundy zadań gulp wyśle 20 komunikatów z Centrum IoT do Pi.</span><span class="sxs-lookup"><span data-stu-id="5454d-147">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi.</span></span> <span data-ttu-id="5454d-148">Ostatnią jest komunikat "stop", która określa, że aplikacja przestanie działać.</span><span class="sxs-lookup"><span data-stu-id="5454d-148">The last one is a "stop" message that tells the application to stop running.</span></span>

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a><span data-ttu-id="5454d-150">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="5454d-150">Summary</span></span>
<span data-ttu-id="5454d-151">Na Pi miga LED zostało pomyślnie wysłane wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="5454d-151">You’ve successfully sent messages from your IoT hub to Pi to blink the LED.</span></span> <span data-ttu-id="5454d-152">Następne zadanie jest opcjonalne: Zmień włączenia i wyłączenia zachowanie LED.</span><span class="sxs-lookup"><span data-stu-id="5454d-152">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5454d-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5454d-153">Next steps</span></span>
[<span data-ttu-id="5454d-154">Zmień włączenia i wyłączenia zachowanie LED</span><span class="sxs-lookup"><span data-stu-id="5454d-154">Change the on and off behavior of the LED</span></span>](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

