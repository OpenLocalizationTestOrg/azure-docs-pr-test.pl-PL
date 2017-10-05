---
title: "Nawiązać Pi malina (węzeł) Azure IoT — lekcji 3: uruchamianie przykładowych | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowej aplikacji do malina Pi 3, który wysyła wiadomości do Centrum IoT i miganie LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "BLINK doprowadziły pi chmury, doprowadziły migania z chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1c03283ee276a954f822d6eca5f0a3d5f93ec64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="09ca5-104">Uruchom przykładową aplikację do wysyłania wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="09ca5-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="09ca5-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="09ca5-105">What you will do</span></span>
<span data-ttu-id="09ca5-106">W tym artykule opisano sposób wdrażania i uruchom przykładową aplikację na malina Pi 3, który wysyła wiadomości do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="09ca5-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="09ca5-107">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="09ca5-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="09ca5-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="09ca5-108">What you will learn</span></span>
<span data-ttu-id="09ca5-109">Zostanie sposób użycia narzędzia gulp do wdrożenia i uruchomienia przykładowej aplikacji Node.js na Pi.</span><span class="sxs-lookup"><span data-stu-id="09ca5-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="09ca5-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="09ca5-110">What you need</span></span>
* <span data-ttu-id="09ca5-111">Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenia aplikacji funkcji platformy Azure i konto magazynu do przetwarzania i przechowywania wiadomości Centrum IoT](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="09ca5-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="09ca5-112">Pobrać parametry połączenia koncentratora i urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="09ca5-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="09ca5-113">Ciąg połączenia urządzenia jest używany przez Twoje Pi nawiązać połączenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="09ca5-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="09ca5-114">Ciąg połączenia Centrum IoT jest używany do nawiązania połączenia w rejestrze tożsamości w Centrum IoT do zarządzania urządzeniami, które mogą nawiązać połączenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="09ca5-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="09ca5-115">Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="09ca5-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="09ca5-116">Użyj `iot-sample` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="09ca5-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="09ca5-117">Pobierz ciąg połączenia Centrum IoT, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="09ca5-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="09ca5-118">`{my hub name}`jest to nazwa określona podczas tworzenia Centrum IoT i zarejestrowana Pi.</span><span class="sxs-lookup"><span data-stu-id="09ca5-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="09ca5-119">Pobierz ciąg połączenia urządzenia, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="09ca5-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="09ca5-120">Użyj `myraspberrypi` jako wartość `{device id}` Jeśli wartości nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="09ca5-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="09ca5-121">Skonfiguruj połączenie z urządzeniem</span><span class="sxs-lookup"><span data-stu-id="09ca5-121">Configure the device connection</span></span>
1. <span data-ttu-id="09ca5-122">Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="09ca5-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="09ca5-123">Otwórz plik konfiguracji urządzenia `config-raspberrypi.json` w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="09ca5-123">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="09ca5-125">Wprowadź następujące elementy zastępcze w `config-raspberrypi.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="09ca5-125">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="09ca5-126">Zastąp **[urządzenia nazwa hosta lub adres IP]** z urządzenia IP adres lub nazwa hosta uzyskanego od `device-discovery-cli` lub wartość dziedziczone po skonfigurowaniu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="09ca5-126">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="09ca5-127">Zastąp **[parametry połączenia urządzenia IoT]** z `device connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="09ca5-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="09ca5-128">Zastąp **[parametry połączenia Centrum IoT]** z `iot hub connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="09ca5-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="09ca5-129">Aktualizacja `config-raspberrypi.json` plików, dzięki czemu można wdrożyć przykładowej aplikacji z komputera.</span><span class="sxs-lookup"><span data-stu-id="09ca5-129">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="09ca5-130">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="09ca5-130">Deploy and run the sample application</span></span>
<span data-ttu-id="09ca5-131">Wdrażanie i uruchamianie przykładowej aplikacji na Pi, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="09ca5-131">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="09ca5-132">Sprawdź, czy działa przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="09ca5-132">Verify that the sample application works</span></span>
<span data-ttu-id="09ca5-133">Powinny pojawić się LED, który jest podłączony do Pi migający co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="09ca5-133">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="09ca5-134">Za każdym razem, gdy LED miga, przykładowej aplikacji wysyła komunikat do Centrum IoT i sprawdza, czy wiadomość została pomyślnie wysłana do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="09ca5-134">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="09ca5-135">Ponadto każdy komunikat odebrany przez Centrum IoT jest drukowany w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="09ca5-135">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="09ca5-136">Przykładowa aplikacja kończy się automatycznie po wysłaniu wiadomości 20.</span><span class="sxs-lookup"><span data-stu-id="09ca5-136">The sample application terminates automatically after sending 20 messages.</span></span>

![Przykładowa aplikacja z wysłanych i odebranych komunikatów](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="09ca5-138">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="09ca5-138">Summary</span></span>
<span data-ttu-id="09ca5-139">Został wdrożony i Uruchom nowe migania przykładową aplikację na Pi do wysyłania wiadomości urządzenia do chmury do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="09ca5-139">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="09ca5-140">Teraz można monitorować wiadomości, ponieważ są one zapisywane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="09ca5-140">You can now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09ca5-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="09ca5-141">Next steps</span></span>
[<span data-ttu-id="09ca5-142">Odczytywanie wiadomości utrwalane w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="09ca5-142">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

