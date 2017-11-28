---
title: "Urządzeń Sensor tag & bramy IoT Azure - Lekcja 3: uruchamianie aplikacji przykładowych | Dokumentacja firmy Microsoft"
description: "Uruchom cz przykładowych aplikacji tooreceive danych z Sensor tag cz i z Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Cz aplikacji, czujnik Monitoruj aplikację, zbierania danych czujnika, danych z czujników, toocloud danych czujnika"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a><span data-ttu-id="eec09-104">Konfigurowanie i uruchamianie cz przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="eec09-104">Configure and run a BLE sample application</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="eec09-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="eec09-105">What you will do</span></span>

- <span data-ttu-id="eec09-106">Repozytorium przykładowej hello klonowania.</span><span class="sxs-lookup"><span data-stu-id="eec09-106">Clone hello sample repository.</span></span> 
- <span data-ttu-id="eec09-107">Konfigurowanie hello łączność między Sensor tag i Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eec09-107">Set up hello connectivity between SensorTag and Intel NUC.</span></span> 
- <span data-ttu-id="eec09-108">Użyj hello Azure CLI tooget informacje o Twoich Centrum IoT i Sensor tag przykładową aplikację cz (Bluetooth energii niski).</span><span class="sxs-lookup"><span data-stu-id="eec09-108">Use hello Azure CLI tooget your IoT hub and SensorTag information for a BLE(Bluetooth Low Energy) sample application.</span></span> <span data-ttu-id="eec09-109">Skonfiguruj i uruchom hello cz przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eec09-109">And configure and run hello BLE sample application.</span></span> 

<span data-ttu-id="eec09-110">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="eec09-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="eec09-111">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="eec09-111">What you will learn</span></span>

<span data-ttu-id="eec09-112">W tym artykule dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="eec09-112">In this article, you will learn:</span></span>

- <span data-ttu-id="eec09-113">Jak tooconfigure i wykonywania hello cz przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eec09-113">How tooconfigure and run hello BLE sample application.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eec09-114">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="eec09-114">What you need</span></span>

<span data-ttu-id="eec09-115">Pomyślnie zakończono</span><span class="sxs-lookup"><span data-stu-id="eec09-115">You must have successfully completed</span></span>

- [<span data-ttu-id="eec09-116">Utwórz Centrum IoT i zarejestruj Sensor tag</span><span class="sxs-lookup"><span data-stu-id="eec09-116">Create an IoT hub and register SensorTag</span></span>](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a><span data-ttu-id="eec09-117">Klonowanie hello próbki repozytorium toohello hosta</span><span class="sxs-lookup"><span data-stu-id="eec09-117">Clone hello sample repository toohello host computer</span></span>

<span data-ttu-id="eec09-118">repozytorium przykładowej hello tooclone, wykonaj następujące kroki na komputerze hosta hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-118">tooclone hello sample repository, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="eec09-119">Otwórz okno wiersza polecenia w systemie Windows lub Otwórz terminal macOS lub Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="eec09-119">Open a Command Prompt window in Windows or open a terminal in macOS or Ubuntu.</span></span>
2. <span data-ttu-id="eec09-120">Uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-120">Run hello following commands:</span></span>

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a><span data-ttu-id="eec09-121">Konfigurowanie hello łączność między Sensor tag i Intel NUC</span><span class="sxs-lookup"><span data-stu-id="eec09-121">Set up hello connectivity between SensorTag and Intel NUC</span></span>

<span data-ttu-id="eec09-122">tooset się hello łączności, wykonaj następujące kroki na komputerze hosta hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-122">tooset up hello connectivity, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="eec09-123">Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-123">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. <span data-ttu-id="eec09-124">Otwórz `config-gateway.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-124">Open `config-gateway.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. <span data-ttu-id="eec09-125">Znajdź powitania po wierszu kodu i Zastąp `[device hostname or IP address]` z hello IP adres lub nazwę hosta Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eec09-125">Locate hello following line of code and replace `[device hostname or IP address]` with hello IP address or host name of Intel NUC.</span></span>
   <span data-ttu-id="eec09-126">![Zrzut ekranu przedstawiający konfiguracji bramy](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span><span class="sxs-lookup"><span data-stu-id="eec09-126">![screenshot of config gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)</span></span>

4. <span data-ttu-id="eec09-127">Zainstaluj narzędzia pomocnika na NUC firmy Intel, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-127">Install helper tools on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp install-tools
   ```

5. <span data-ttu-id="eec09-128">Włącz Sensor tag, naciskając przycisk zasilania hello jako hello poniższej ilustracji, a powinien blink LED hello zielony.</span><span class="sxs-lookup"><span data-stu-id="eec09-128">Turn on SensorTag by pressing hello power button as hello following picture, and hello green LED should blink.</span></span>

   ![Włącz Sensor Tag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. <span data-ttu-id="eec09-130">Skanuj urządzeń Sensor tag, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-130">Scan SensorTag devices by running hello following commands:</span></span>

   ```bash
   gulp discover-sensortag
   ```

7. <span data-ttu-id="eec09-131">Testowanie łączności hello między hello Sensor tag i NUC firmy Intel, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-131">Test hello connectivity between hello SensorTag and Intel NUC by running hello following command:</span></span>

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   <span data-ttu-id="eec09-132">Zastąp `{mac address}` z hello adres MAC, które zostały uzyskane w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="eec09-132">Replace `{mac address}` with hello MAC address that you obtained in hello previous step.</span></span>

## <a name="get-hello-connection-string-of-sensortag"></a><span data-ttu-id="eec09-133">Pobierz ciąg połączenia hello Sensor tag</span><span class="sxs-lookup"><span data-stu-id="eec09-133">Get hello connection string of SensorTag</span></span>

<span data-ttu-id="eec09-134">Witaj tooget parametry połączenia Centrum Azure IoT Sensor tag, uruchom następujące polecenie na komputerze hosta hello hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-134">tooget hello Azure IoT hub connection string of SensorTag, run hello following command on hello host computer:</span></span>

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

<span data-ttu-id="eec09-135">`{IoT hub name}`jest hello nazwę Centrum IoT, który został użyty.</span><span class="sxs-lookup"><span data-stu-id="eec09-135">`{IoT hub name}` is hello IoT hub name that you used.</span></span> <span data-ttu-id="eec09-136">Użyj bramy iot jako wartość hello `{resource group name}` i użyj mydevice jako wartość hello `{device id}` nie zmiany wartości hello Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="eec09-136">Use iot-gateway as hello value of `{resource group name}` and use mydevice as hello value of `{device id}` if you didn't change hello value in Lesson 2.</span></span>

## <a name="configure-hello-ble-sample-application"></a><span data-ttu-id="eec09-137">Skonfiguruj hello cz przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="eec09-137">Configure hello BLE sample application</span></span>

<span data-ttu-id="eec09-138">tooconfigure i wykonywania hello cz przykładowej aplikacji, wykonaj następujące kroki na komputerze hosta hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-138">tooconfigure and run hello BLE sample application, follow these steps on hello host computer:</span></span>

1. <span data-ttu-id="eec09-139">Otwórz `config-sensortag.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-139">Open `config-sensortag.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Zrzut ekranu przedstawiający Sensor tag konfiguracji](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. <span data-ttu-id="eec09-141">Wprowadź następujące elementy zastępcze w kodzie hello hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-141">Make hello following replacements in hello code:</span></span>
   - <span data-ttu-id="eec09-142">Zastąp `[IoT hub name]` o nazwie Centrum IoT hello, który został użyty.</span><span class="sxs-lookup"><span data-stu-id="eec09-142">Replace `[IoT hub name]` with hello IoT hub name that you used.</span></span>
   - <span data-ttu-id="eec09-143">Zastąp `[IoT device connection string]` z ciągu połączenia hello Sensor tag, który został uzyskany.</span><span class="sxs-lookup"><span data-stu-id="eec09-143">Replace `[IoT device connection string]` with hello connection string of SensorTag that you obtained.</span></span>
   - <span data-ttu-id="eec09-144">Zastąp `[device_mac_address]` z hello adres MAC hello Sensor tag, który został uzyskany.</span><span class="sxs-lookup"><span data-stu-id="eec09-144">Replace `[device_mac_address]` with hello MAC address of hello SensorTag that you obtained.</span></span>

3. <span data-ttu-id="eec09-145">Uruchom hello cz przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="eec09-145">Run hello BLE sample application.</span></span>

   <span data-ttu-id="eec09-146">Witaj toorun cz przykładowej aplikacji, wykonaj następujące kroki na komputerze hosta hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-146">toorun hello BLE sample application, follow these steps on hello host computer:</span></span>

   1. <span data-ttu-id="eec09-147">Włącz Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="eec09-147">Turn on SensorTag.</span></span>

   2. <span data-ttu-id="eec09-148">Wdrażanie i uruchamianie aplikacji przykładowej cz hello na Intel NUC, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-148">Deploy and run hello BLE sample application on Intel NUC by running hello following command:</span></span>
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a><span data-ttu-id="eec09-149">Sprawdź, czy działa hello cz przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="eec09-149">Verify that hello BLE sample application works</span></span>

<span data-ttu-id="eec09-150">Powinna pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="eec09-150">You should now see an output like hello following:</span></span>

![Dane wyjściowe aplikacji przykładowej cz](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

<span data-ttu-id="eec09-152">Hello Przykładowa aplikacja przechowuje zbieranie danych temperatury i przesłanie tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="eec09-152">hello sample application keeps collecting temperature data and sent it tooyour IoT hub.</span></span> <span data-ttu-id="eec09-153">Witaj przykładowej aplikacji kończy się automatycznie po wysłaniu 40 sekund.</span><span class="sxs-lookup"><span data-stu-id="eec09-153">hello sample application terminates automatically after sending 40 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="eec09-154">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="eec09-154">Summary</span></span>

<span data-ttu-id="eec09-155">Został pomyślnie skonfigurować hello łączność między Sensor tag i Intel NUC i uruchom cz przykładowej aplikacji, która zbiera i wysyła dane z Centrum IoT tooyour Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="eec09-155">You've successfully set up hello connectivity between SensorTag and Intel NUC, and run a BLE sample application which collects and sends data from SensorTag tooyour IoT hub.</span></span> <span data-ttu-id="eec09-156">Wszystko jest gotowe toolearn jak tooverify, który otrzymał Centrum IoT hello danych.</span><span class="sxs-lookup"><span data-stu-id="eec09-156">You're ready toolearn how tooverify that your IoT hub has received hello data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eec09-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eec09-157">Next steps</span></span>
<span data-ttu-id="eec09-158">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) (Odczytywanie komunikatów z centrum IoT Hub)</span><span class="sxs-lookup"><span data-stu-id="eec09-158">[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)</span></span>