---
title: "Symulowane urządzenie & Azure IoT bramy - lekcji 3: uruchamianie aplikacji przykładowych | Dokumentacja firmy Microsoft"
description: "Uruchom symulowane urządzenie przykładowej aplikacji toosend temperatury danych tooyour Centrum IoT"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: toocloud danych
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="e46dc-104">Konfigurowanie i uruchamianie aplikacji przykładowej symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="e46dc-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e46dc-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="e46dc-105">What you will do</span></span>

- <span data-ttu-id="e46dc-106">Repozytorium przykładowej hello klonowania.</span><span class="sxs-lookup"><span data-stu-id="e46dc-106">Clone hello sample repository.</span></span>
- <span data-ttu-id="e46dc-107">Użyj hello Azure CLI tooget informacje o Twoich Centrum IoT i urządzenia logicznego symulowane urządzenie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e46dc-107">Use hello Azure CLI tooget your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="e46dc-108">Skonfiguruj i uruchom hello symulowane urządzenie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e46dc-108">Configure and run hello simulated device sample application.</span></span>

<span data-ttu-id="e46dc-109">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e46dc-109">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e46dc-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="e46dc-110">What you will learn</span></span>

<span data-ttu-id="e46dc-111">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="e46dc-111">In this article, you will learn:</span></span>

- <span data-ttu-id="e46dc-112">Jak tooconfigure i wykonywania hello symulowane urządzenie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e46dc-112">How tooconfigure and run hello simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e46dc-113">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="e46dc-113">What you need</span></span>

<span data-ttu-id="e46dc-114">Pomyślnie zakończono</span><span class="sxs-lookup"><span data-stu-id="e46dc-114">You must have successfully completed</span></span>

- <span data-ttu-id="e46dc-115">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)</span><span class="sxs-lookup"><span data-stu-id="e46dc-115">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="e46dc-116">Klonowanie hello próbki repozytorium toohello hosta</span><span class="sxs-lookup"><span data-stu-id="e46dc-116">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="e46dc-117">repozytorium przykładowej hello tooclone, wykonaj następujące kroki na komputerze hosta hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-117">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="e46dc-118">Otwórz wiersz polecenia w systemie Windows lub Otwórz terminal macOS lub Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e46dc-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="e46dc-119">Uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-119">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a><span data-ttu-id="e46dc-120">Skonfiguruj hello symulowane urządzenie i NUC Twojego</span><span class="sxs-lookup"><span data-stu-id="e46dc-120">Configure hello simulated device and your NUC</span></span>

1. <span data-ttu-id="e46dc-121">Plik konfiguracji Otwórz hello `config.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-121">Open hello configuration file `config.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="e46dc-122">Zastąp `"has_sensortag": true` z`"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="e46dc-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Nie masz urządzenia Sensor tag analizy czasowej konfiguracji](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="e46dc-124">Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-124">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="e46dc-125">Otwórz `config-gateway.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-125">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="e46dc-126">Znajdź powitania po wierszu kodu i Zastąp `[device hostname or IP address]` z adresu IP adres lub nazwę hosta hello Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="e46dc-126">Locate hello following line of code and replace `[device hostname or IP address]` with IP address or host name of hello Intel NUC.</span></span>
   <span data-ttu-id="e46dc-127">![Zrzut ekranu przedstawiający konfiguracji bramy](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="e46dc-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="e46dc-128">Pobierz ciąg połączenia hello urządzenia logicznego centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e46dc-128">Get hello connection string of your IoT hub logical device</span></span>

<span data-ttu-id="e46dc-129">Witaj tooget parametry połączenia Centrum Azure IoT urządzenia logicznego, uruchom następujące polecenie na komputerze hosta hello hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-129">tooget hello Azure IoT hub connection string of your logical device, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="e46dc-130">`{IoT hub name}`jest hello nazwę Centrum IoT, który został użyty.</span><span class="sxs-lookup"><span data-stu-id="e46dc-130">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="e46dc-131">Użyj bramy iot jako wartość hello `{resource group name}` i użyj mydevice jako wartość hello `{device id}` nie zmiany wartości hello Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="e46dc-131">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="e46dc-132">Skonfiguruj hello symulowane urządzenie chmury przekazywania przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="e46dc-132">Configure hello simulated device cloud upload sample application</span></span>

<span data-ttu-id="e46dc-133">tooconfigure i wykonywania hello symulowane urządzenie chmury przekazać przykładowej aplikacji, wykonaj następujące kroki na komputerze hosta hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-133">tooconfigure and run hello simulated device cloud upload sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="e46dc-134">Otwórz `config-sensortag.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-134">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Zrzut ekranu przedstawiający Sensor tag konfiguracji](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="e46dc-136">Wprowadź następujące elementy zastępcze w kodzie hello hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-136">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="e46dc-137">Zastąp `[IoT hub name]` o nazwie Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="e46dc-137">Replace `[IoT hub name]` with hello IoT hub name.</span></span>
   - <span data-ttu-id="e46dc-138">Zastąp `[IoT device connection string]` z ciągu połączenia hello urządzenia logicznego centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e46dc-138">Replace `[IoT device connection string]` with hello connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="e46dc-139">Uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e46dc-139">Run hello application.</span></span>

   <span data-ttu-id="e46dc-140">Wdrażanie i uruchamianie aplikacji hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-140">Deploy and run hello application by running hello following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a><span data-ttu-id="e46dc-141">Weryfikowanie działania aplikacji przykładowej hello</span><span class="sxs-lookup"><span data-stu-id="e46dc-141">Verify hello sample application works</span></span>

<span data-ttu-id="e46dc-142">Teraz powinny być widoczne dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="e46dc-142">You should now see output like hello following:</span></span>

![Symulowane urządzenie przykładowej aplikacji w danych wyjściowych](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="e46dc-144">Aplikacja Hello wysyła Centrum IoT tooyour danych temperatury, który jest ważny przez 40 sekund.</span><span class="sxs-lookup"><span data-stu-id="e46dc-144">hello application sends temperature data tooyour IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="e46dc-145">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e46dc-145">Summary</span></span>

<span data-ttu-id="e46dc-146">Pomyślnie skonfigurowano i wykonywania hello symulowane urządzenie chmury przekazywania przykładowej aplikacji, która wysyła Centrum IoT tooyour danych z symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="e46dc-146">You've successfully configured and run hello simulated device cloud upload sample application which sends data tooyour IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e46dc-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e46dc-147">Next steps</span></span>
<span data-ttu-id="e46dc-148">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) (Odczytywanie komunikatów z centrum IoT Hub)</span><span class="sxs-lookup"><span data-stu-id="e46dc-148">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>