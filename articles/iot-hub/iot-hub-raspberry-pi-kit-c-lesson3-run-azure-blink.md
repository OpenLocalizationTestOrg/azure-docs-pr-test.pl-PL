---
title: "Connect Raspberry pi (C) tooAzure IoT — lekcji 3: uruchamianie przykładowych | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowych aplikacji tooRaspberry Pi 3, która wysyła Centrum IoT tooyour wiadomości i miganie hello LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "BLINK doprowadziły pi chmury, doprowadziły migania z chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="4996c-104">Uruchom toosend aplikacji przykładowej wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="4996c-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="4996c-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="4996c-105">What you will do</span></span>
<span data-ttu-id="4996c-106">W tym artykule opisano sposób toodeploy i uruchom przykładową aplikację na malina Pi 3, który wysyła wiadomości tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4996c-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="4996c-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4996c-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4996c-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="4996c-108">What you will learn</span></span>
<span data-ttu-id="4996c-109">Dowiesz się, jak toouse hello system gulp toodeploy narzędzia i uruchomić hello przykładowej aplikacji Node.js na Pi.</span><span class="sxs-lookup"><span data-stu-id="4996c-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4996c-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="4996c-110">What you need</span></span>
* <span data-ttu-id="4996c-111">Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenie aplikacji funkcji platformy Azure i magazynu konta tooprocess i Magazyn Centrum IoT wiadomości](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="4996c-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="4996c-112">Pobrać parametry połączenia koncentratora i urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="4996c-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="4996c-113">ciąg połączenia urządzenia Hello jest używany przez Centrum IoT tooyour tooconnect Pi.</span><span class="sxs-lookup"><span data-stu-id="4996c-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="4996c-114">Parametry połączenia Centrum IoT Hello jest rejestru tożsamości toohello tooconnect używanych w urządzeniami hello toomanage Centrum IoT, które są dozwolone Centrum IoT tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="4996c-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="4996c-115">Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4996c-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="4996c-116">Użyj `iot-sample` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="4996c-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="4996c-117">Pobierz ciąg połączenia Centrum IoT hello, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4996c-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="4996c-118">`{my hub name}`to nazwa hello określone podczas tworzenia Centrum IoT i zarejestrowana Pi.</span><span class="sxs-lookup"><span data-stu-id="4996c-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="4996c-119">Pobierz ciąg połączenia urządzenia hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4996c-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="4996c-120">Użyj `myraspberrypi` jako wartość hello `{device id}` Jeśli hello wartość nie zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="4996c-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="4996c-121">Skonfiguruj połączenie z urządzeniem hello</span><span class="sxs-lookup"><span data-stu-id="4996c-121">Configure hello device connection</span></span>
1. <span data-ttu-id="4996c-122">Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="4996c-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="4996c-123">Uruchom **system gulp instalacji narzędzia** oraz, jeśli nie zostało to jeszcze zrobione, Lekcja 1.</span><span class="sxs-lookup"><span data-stu-id="4996c-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="4996c-124">Plik konfiguracji urządzenia Otwórz hello `config-raspberrypi.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4996c-124">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="4996c-126">Wprowadź następujące elementy zastępcze w hello hello `config-raspberrypi.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="4996c-126">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="4996c-127">Zastąp **[urządzenia nazwa hosta lub adres IP]** z hello urządzenia IP adres lub nazwa hosta otrzymano z `device-discovery-cli` lub z wartością hello dziedziczone po skonfigurowaniu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4996c-127">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="4996c-128">Zastąp **[parametry połączenia urządzenia IoT]** z hello `device connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="4996c-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="4996c-129">Zastąp **[parametry połączenia Centrum IoT]** z hello `iot hub connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="4996c-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="4996c-130">Nie ma potrzeby `azure_storage_connection_string` w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="4996c-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="4996c-131">Zachować, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="4996c-131">Keep it as is.</span></span>

<span data-ttu-id="4996c-132">Aktualizacja hello `config-raspberrypi.json` plików, dzięki czemu można wdrożyć hello przykładowej aplikacji z komputera.</span><span class="sxs-lookup"><span data-stu-id="4996c-132">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="4996c-133">Wdrażanie i uruchamianie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="4996c-133">Deploy and run hello sample application</span></span>
<span data-ttu-id="4996c-134">Wdrażanie i uruchamianie aplikacji przykładowej hello na Pi, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="4996c-134">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="4996c-135">Sprawdź, czy działa hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="4996c-135">Verify that hello sample application works</span></span>
<span data-ttu-id="4996c-136">Powinny pojawić się hello LED, który jest połączony tooPi migający co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="4996c-136">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="4996c-137">Za każdym razem, gdy hello LED miga, hello przykładowej aplikacji wysyła z Centrum IoT tooyour wiadomości i sprawdza, czy tę wiadomość hello została pomyślnie wysłana tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="4996c-137">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="4996c-138">Ponadto każdy komunikat odebrany przez Centrum IoT hello jest drukowany w oknie konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="4996c-138">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="4996c-139">Witaj przykładowej aplikacji kończy się automatycznie po wysłaniu wiadomości 20.</span><span class="sxs-lookup"><span data-stu-id="4996c-139">hello sample application terminates automatically after sending 20 messages.</span></span>

![Przykładowa aplikacja z wysłanych i odebranych komunikatów](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="4996c-141">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="4996c-141">Summary</span></span>
<span data-ttu-id="4996c-142">Zostały wdrożone i uruchom hello nowe migania przykładowej aplikacji w Centrum IoT tooyour Pi toosend wiadomości urządzenia do chmury.</span><span class="sxs-lookup"><span data-stu-id="4996c-142">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="4996c-143">Jak są one zapisywane na koncie magazynu toohello teraz monitorować wiadomości.</span><span class="sxs-lookup"><span data-stu-id="4996c-143">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4996c-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4996c-144">Next steps</span></span>
[<span data-ttu-id="4996c-145">Odczytywanie wiadomości utrwalane w magazynie Azure</span><span class="sxs-lookup"><span data-stu-id="4996c-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

