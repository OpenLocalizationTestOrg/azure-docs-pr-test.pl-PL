---
title: "Connect Raspberry pi (C) tooAzure IoT - 4 lekcji: chmury do urządzenia | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja działa na Pi i monitoruje komunikaty przychodzące z Centrum IoT. Nowe zadanie gulp wysyła komunikaty tooPi z Twojej hello tooblink Centrum IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "toodevice chmury, wiadomości z chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: fcbc0dd0-cae3-47b0-8e58-240e4f406f75
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5596bf3a83c21f2bd54b2f83e2a8fdad7a608b94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="98fb3-105">Uruchom tooreceive aplikacji przykładowej wiadomości chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="98fb3-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="98fb3-106">W tym artykule wdrożono przykładową aplikację na malina Pi 3.</span><span class="sxs-lookup"><span data-stu-id="98fb3-106">In this article, you deploy a sample application on Raspberry Pi 3.</span></span> <span data-ttu-id="98fb3-107">aplikacja przykładowa Hello monitoruje komunikaty przychodzące z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98fb3-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="98fb3-108">Można również uruchomić zadanie gulp na tooPi wiadomości toosend Twojego komputera z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98fb3-108">You also run a gulp task on your computer toosend messages tooPi from your IoT hub.</span></span> <span data-ttu-id="98fb3-109">Gdy hello Przykładowa aplikacja odbiera wiadomości powitania, miga hello LED.</span><span class="sxs-lookup"><span data-stu-id="98fb3-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="98fb3-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="98fb3-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="98fb3-111">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="98fb3-111">What you will do</span></span>
* <span data-ttu-id="98fb3-112">Połącz Centrum IoT tooyour hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98fb3-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="98fb3-113">Wdrażanie i uruchamianie hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98fb3-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="98fb3-114">Wysyłanie wiadomości z Twojej IoT hub tooPi tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="98fb3-114">Send messages from your IoT hub tooPi tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="98fb3-115">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="98fb3-115">What you will learn</span></span>
<span data-ttu-id="98fb3-116">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="98fb3-116">In this article, you will learn:</span></span>
* <span data-ttu-id="98fb3-117">Jak komunikaty przychodzące toomonitor z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98fb3-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="98fb3-118">Jak chmury urządzenia toosend komunikaty z sieci tooPi Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98fb3-118">How toosend cloud-to-device messages from your IoT hub tooPi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="98fb3-119">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="98fb3-119">What you need</span></span>
* <span data-ttu-id="98fb3-120">Malinowe Pi 3, skonfigurować do używania.</span><span class="sxs-lookup"><span data-stu-id="98fb3-120">Raspberry Pi 3, set up for use.</span></span> <span data-ttu-id="98fb3-121">toolearn tooset się Pi, zobacz temat [Skonfiguruj urządzenie](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span><span class="sxs-lookup"><span data-stu-id="98fb3-121">toolearn how tooset up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-c-lesson1-configure-your-device.md).</span></span>
* <span data-ttu-id="98fb3-122">Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="98fb3-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="98fb3-123">toolearn jak toocreate Centrum IoT, zobacz [utworzenie Centrum IoT i zarejestruj malina Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="98fb3-123">toolearn how toocreate your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-c-lesson2-prepare-azure-iot-hub.md).</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="98fb3-124">Połącz z Centrum IoT tooyour hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="98fb3-124">Connect hello sample application tooyour IoT hub</span></span>
1. <span data-ttu-id="98fb3-125">Upewnij się, że jesteś w folderze repozytorium hello `iot-hub-c-raspberrypi-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="98fb3-125">Make sure that you're in hello repo folder `iot-hub-c-raspberrypi-getting-started`.</span></span> <span data-ttu-id="98fb3-126">Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="98fb3-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="98fb3-127">Powiadomienie hello `app.c` pliku w hello `app` podfolderu.</span><span class="sxs-lookup"><span data-stu-id="98fb3-127">Notice hello `app.c` file in hello `app` subfolder.</span></span> <span data-ttu-id="98fb3-128">Witaj `app.c` plik jest plikiem klucza źródła hello, zawierający hello kodu toomonitor komunikaty przychodzące hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98fb3-128">hello `app.c` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="98fb3-129">Witaj `blinkLED` funkcja miganie hello LED.</span><span class="sxs-lookup"><span data-stu-id="98fb3-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Struktura repozytorium w hello przykładowej aplikacji](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure_c.png)
2. <span data-ttu-id="98fb3-131">Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="98fb3-131">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

   <span data-ttu-id="98fb3-132">Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) na tym komputerze, wszystkie konfiguracje hello są dziedziczone, można pominąć zadań toohello toostep wdrażanie i uruchamianie hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98fb3-132">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on this computer, all hello configurations are inherited, so you can skip toostep toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="98fb3-133">Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) na innym komputerze, należy symbole zastępcze hello tooreplace w hello `config-raspberrypi.json` pliku.</span><span class="sxs-lookup"><span data-stu-id="98fb3-133">If you completed hello steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md) on a different computer, you need tooreplace hello placeholders in hello `config-raspberrypi.json` file.</span></span> <span data-ttu-id="98fb3-134">Witaj `config-raspberrypi.json` plik znajduje się w podfolderze hello folderu macierzystego.</span><span class="sxs-lookup"><span data-stu-id="98fb3-134">hello `config-raspberrypi.json` file is in hello subfolder of your home folder.</span></span>

   ![Zawartość pliku config raspberrypi.json hello](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* <span data-ttu-id="98fb3-136">Zastąp **[urządzenia nazwa hosta lub adres IP]** z jego Pi IP adres lub nazwę hosta, który można uzyskać, uruchamiając hello `devdisco list --eth` polecenia.</span><span class="sxs-lookup"><span data-stu-id="98fb3-136">Replace **[device hostname or IP address]** with Pi’s IP address or host name that you get by running hello `devdisco list --eth` command.</span></span>
* <span data-ttu-id="98fb3-137">Zastąp **[parametry połączenia urządzenia IoT]** z hello parametry połączenia urządzenia, które można uzyskać, uruchamiając hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="98fb3-137">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.</span></span>
* <span data-ttu-id="98fb3-138">Zastąp **[parametry połączenia Centrum IoT]** z hello parametry połączenia Centrum IoT, które można uzyskać, uruchamiając hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` polecenia.</span><span class="sxs-lookup"><span data-stu-id="98fb3-138">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.</span></span>

> [!NOTE]
> <span data-ttu-id="98fb3-139">Uruchom **system gulp instalacji narzędzia** oraz, jeśli nie zostało to jeszcze zrobione, Lekcja 1.</span><span class="sxs-lookup"><span data-stu-id="98fb3-139">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="98fb3-140">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="98fb3-140">Deploy and run hello sample application</span></span>
<span data-ttu-id="98fb3-141">Wdrażanie i uruchamianie aplikacji przykładowej hello na Pi, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="98fb3-141">Deploy and run hello sample application on Pi by running hello following commands:</span></span>

```
gulp deploy && gulp run
```

<span data-ttu-id="98fb3-142">Uruchamia polecenie gulp Hello najpierw hello zadań instalacji narzędzi.</span><span class="sxs-lookup"><span data-stu-id="98fb3-142">hello gulp command runs hello install-tools task first.</span></span> <span data-ttu-id="98fb3-143">Następnie wdraża hello przykładowej aplikacji tooPi.</span><span class="sxs-lookup"><span data-stu-id="98fb3-143">Then it deploys hello sample application tooPi.</span></span> <span data-ttu-id="98fb3-144">Na koniec uruchomieniu aplikacji hello na Pi i oddzielnych zadań na hoście tooPi wiadomości migania toosend 20 komputera z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98fb3-144">Finally, it runs hello application on Pi and a separate task on your host computer toosend 20 blink messages tooPi from your IoT hub.</span></span>

<span data-ttu-id="98fb3-145">Po uruchomieniu aplikacji przykładowej hello rozpoczyna nasłuchiwanie toomessages z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98fb3-145">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="98fb3-146">W tym samym czasie hello gulp zadań wysyła komunikaty "blink" z Twojej tooPi Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98fb3-146">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooPi.</span></span> <span data-ttu-id="98fb3-147">Dla każdego komunikatu migania odbierająca Pi hello przykładowej aplikacji wywołuje hello `blinkLED` funkcja tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="98fb3-147">For each blink message that Pi receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="98fb3-148">Powinny pojawić się migania LED hello co dwie sekundy jako hello system gulp zadań wysyła 20 komunikatów z Twojej tooPi Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="98fb3-148">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooPi.</span></span> <span data-ttu-id="98fb3-149">Hello ostatnio jedna jest zatrzymuje aplikacji hello komunikat "stop".</span><span class="sxs-lookup"><span data-stu-id="98fb3-149">hello last one is a "stop" message that stops hello application from running.</span></span>

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink_c.png)

## <a name="summary"></a><span data-ttu-id="98fb3-151">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="98fb3-151">Summary</span></span>
<span data-ttu-id="98fb3-152">Zostało pomyślnie wysłane wiadomości z Twojej IoT hub tooPi tooblink hello LED.</span><span class="sxs-lookup"><span data-stu-id="98fb3-152">You’ve successfully sent messages from your IoT hub tooPi tooblink hello LED.</span></span> <span data-ttu-id="98fb3-153">następne zadanie Hello jest opcjonalny: Zmień hello włączać i wyłączać zachowanie hello LED.</span><span class="sxs-lookup"><span data-stu-id="98fb3-153">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98fb3-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98fb3-154">Next steps</span></span>
[<span data-ttu-id="98fb3-155">Zmień hello włączać i wyłączać zachowanie hello LED</span><span class="sxs-lookup"><span data-stu-id="98fb3-155">Change hello on and off behavior of hello LED</span></span>](iot-hub-raspberry-pi-kit-c-lesson4-change-led-behavior.md)
