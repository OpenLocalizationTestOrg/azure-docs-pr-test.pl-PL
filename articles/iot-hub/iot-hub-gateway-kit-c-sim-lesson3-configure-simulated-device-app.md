---
title: "Symulowane urządzenie & Azure IoT bramy - lekcji 3: uruchamianie aplikacji przykładowych | Dokumentacja firmy Microsoft"
description: "Uruchom przykładową aplikację symulowane urządzenie do przesyłania danych temperatury do Centrum IoT"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dane w chmurze
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
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a><span data-ttu-id="f031a-104">Konfigurowanie i uruchamianie aplikacji przykładowej symulowane urządzenie</span><span class="sxs-lookup"><span data-stu-id="f031a-104">Configure and run a simulated device sample app</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="f031a-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="f031a-105">What you will do</span></span>

- <span data-ttu-id="f031a-106">Klonuj repozytorium przykładowej.</span><span class="sxs-lookup"><span data-stu-id="f031a-106">Clone the sample repository.</span></span>
- <span data-ttu-id="f031a-107">Użyj interfejsu wiersza polecenia Azure, aby uzyskać informacje o Twoich Centrum IoT i urządzenia logicznego symulowane urządzenie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f031a-107">Use the Azure CLI to get your IoT hub and logical device information for simulated device sample application.</span></span> <span data-ttu-id="f031a-108">Skonfiguruj i uruchom przykładową aplikację symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="f031a-108">Configure and run the simulated device sample application.</span></span>

<span data-ttu-id="f031a-109">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="f031a-109">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="f031a-110">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="f031a-110">What you will learn</span></span>

<span data-ttu-id="f031a-111">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="f031a-111">In this article, you will learn:</span></span>

- <span data-ttu-id="f031a-112">Jak skonfigurować i uruchomić aplikację przykładową symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="f031a-112">How to configure and run the simulated device sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f031a-113">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="f031a-113">What you need</span></span>

<span data-ttu-id="f031a-114">Pomyślnie zakończono</span><span class="sxs-lookup"><span data-stu-id="f031a-114">You must have successfully completed</span></span>

- <span data-ttu-id="f031a-115">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)</span><span class="sxs-lookup"><span data-stu-id="f031a-115">[Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)</span></span>

## <a name="clone-the-sample-repository-to-the-host-computer"></a><span data-ttu-id="f031a-116">Klonuj repozytorium przykładowej do komputera hosta</span><span class="sxs-lookup"><span data-stu-id="f031a-116">Clone the sample repository to the host computer</span></span>

<span data-ttu-id="f031a-117">Klonowanie repozytorium przykładowej, wykonaj następujące kroki na komputerze-hoście:</span><span class="sxs-lookup"><span data-stu-id="f031a-117">To clone the sample repository, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="f031a-118">Otwórz wiersz polecenia w systemie Windows lub Otwórz terminal macOS lub Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f031a-118">Open a Command Prompt in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="f031a-119">Uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="f031a-119">Run the following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a><span data-ttu-id="f031a-120">Skonfiguruj symulowane urządzenie i NUC Twojego</span><span class="sxs-lookup"><span data-stu-id="f031a-120">Configure the simulated device and your NUC</span></span>

1. <span data-ttu-id="f031a-121">Otwórz plik konfiguracji `config.json` w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f031a-121">Open the configuration file `config.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   code config.json
   ```

2. <span data-ttu-id="f031a-122">Zastąp `"has_sensortag": true` z`"has_sensortag": false`</span><span class="sxs-lookup"><span data-stu-id="f031a-122">Replace `"has_sensortag": true` with `"has_sensortag": false`</span></span>

   ![Nie masz urządzenia Sensor tag analizy czasowej konfiguracji](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. <span data-ttu-id="f031a-124">Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="f031a-124">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. <span data-ttu-id="f031a-125">Otwórz `config-gateway.json` w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f031a-125">Open `config-gateway.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. <span data-ttu-id="f031a-126">Znajdź następujący wiersz kodu i Zastąp `[device hostname or IP address]` z adresu IP adres lub nazwę hosta Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="f031a-126">Locate the following line of code and replace `[device hostname or IP address]` with IP address or host name of the Intel NUC.</span></span>
   <span data-ttu-id="f031a-127">![Zrzut ekranu przedstawiający konfiguracji bramy](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="f031a-127">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a><span data-ttu-id="f031a-128">Pobierz ciąg połączenia urządzenia logicznego centrum IoT</span><span class="sxs-lookup"><span data-stu-id="f031a-128">Get the connection string of your IoT hub logical device</span></span>

<span data-ttu-id="f031a-129">Można pobrać ciągu połączenia Centrum Azure IoT urządzenia logicznego, uruchom następujące polecenie na komputerze-hoście:</span><span class="sxs-lookup"><span data-stu-id="f031a-129">To get the Azure IoT hub connection string of your logical device, run the following command on the host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="f031a-130">`{IoT hub name}`jest to nazwa Centrum IoT użyty.</span><span class="sxs-lookup"><span data-stu-id="f031a-130">`{IoT hub name}` is the IoT hub name that you used.</span></span> <span data-ttu-id="f031a-131">Użyj bramy iot jako wartość `{resource group name}` i użyj mydevice jako wartość `{device id}` nie zmiany wartości Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="f031a-131">Use iot-gateway as the value of `{resource group name}` and use mydevice as the value of `{device id}` if you didn't change the value in Lesson 2.</span></span>

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a><span data-ttu-id="f031a-132">Skonfiguruj symulowane urządzenie chmury przekazywania przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="f031a-132">Configure the simulated device cloud upload sample application</span></span>

<span data-ttu-id="f031a-133">Aby skonfigurować i uruchomić symulowane urządzenie chmury przekazywania przykładowej aplikacji, wykonaj następujące kroki na komputerze-hoście:</span><span class="sxs-lookup"><span data-stu-id="f031a-133">To configure and run the simulated device cloud upload sample application, follow these steps on the host computer:</span></span>

1. <span data-ttu-id="f031a-134">Otwórz `config-sensortag.json` w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f031a-134">Open `config-sensortag.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Zrzut ekranu przedstawiający Sensor tag konfiguracji](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. <span data-ttu-id="f031a-136">Wprowadź następujące elementy zastępcze w kodzie:</span><span class="sxs-lookup"><span data-stu-id="f031a-136">Make the following replacements in the code:</span></span>
   - <span data-ttu-id="f031a-137">Zastąp `[IoT hub name]` nazwą Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f031a-137">Replace `[IoT hub name]` with the IoT hub name.</span></span>
   - <span data-ttu-id="f031a-138">Zastąp `[IoT device connection string]` z parametrami połączenia urządzenia logicznego centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="f031a-138">Replace `[IoT device connection string]` with the connection string of your IoT hub logical device.</span></span>

3. <span data-ttu-id="f031a-139">Uruchom aplikację.</span><span class="sxs-lookup"><span data-stu-id="f031a-139">Run the application.</span></span>

   <span data-ttu-id="f031a-140">Wdrażanie i uruchamianie aplikacji, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f031a-140">Deploy and run the application by running the following command:</span></span>

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a><span data-ttu-id="f031a-141">Weryfikowanie działania aplikacji przykładowych</span><span class="sxs-lookup"><span data-stu-id="f031a-141">Verify the sample application works</span></span>

<span data-ttu-id="f031a-142">Teraz powinny być widoczne dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="f031a-142">You should now see output like the following:</span></span>

![Symulowane urządzenie przykładowej aplikacji w danych wyjściowych](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

<span data-ttu-id="f031a-144">Aplikacja wysyła dane temperatury Centrum IoT, który jest ważny przez 40 sekund.</span><span class="sxs-lookup"><span data-stu-id="f031a-144">The application sends temperature data to your IoT hub, which lasts for 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="f031a-145">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f031a-145">Summary</span></span>

<span data-ttu-id="f031a-146">Pomyślnie zostały skonfigurowane i uruchomić aplikacji przykładowej przekazywania Chmury symulowane urządzenie, który wysyła dane do Centrum IoT z symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="f031a-146">You've successfully configured and run the simulated device cloud upload sample application which sends data to your IoT hub with simulated device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f031a-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f031a-147">Next steps</span></span>
<span data-ttu-id="f031a-148">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) (Odczytywanie komunikatów z centrum IoT Hub)</span><span class="sxs-lookup"><span data-stu-id="f031a-148">[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)</span></span>