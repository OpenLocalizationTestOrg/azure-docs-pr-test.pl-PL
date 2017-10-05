---
title: "Nawiązać Edison firmy Intel (węzeł) Azure IoT — lekcji 3: wysyłanie komunikatów | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowej aplikacji do Edison firmy Intel, który wysyła wiadomości do Centrum IoT i miganie LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "usługi w chmurze iot arduino wysyłania danych do chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 1b3b1074-f4d4-42ac-b32c-55f18b304b44
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d4b520b9a1852a285b1e10b5b35447a54313af9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="db32d-104">Uruchom przykładową aplikację do wysyłania wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="db32d-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="db32d-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="db32d-105">What you will do</span></span>
<span data-ttu-id="db32d-106">W tym artykule opisano sposób wdrażania i uruchom przykładową aplikację na Edison firmy Intel, który wysyła wiadomości do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="db32d-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="db32d-107">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="db32d-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="db32d-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="db32d-108">What you will learn</span></span>
<span data-ttu-id="db32d-109">Zostanie sposób użycia narzędzia gulp do wdrożenia i uruchomienia przykładowej aplikacji C na Edison.</span><span class="sxs-lookup"><span data-stu-id="db32d-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="db32d-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="db32d-110">What you need</span></span>
* <span data-ttu-id="db32d-111">Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenia aplikacji funkcji platformy Azure i konto magazynu do przetwarzania i przechowywania wiadomości Centrum IoT][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="db32d-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="db32d-112">Pobrać parametry połączenia koncentratora i urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="db32d-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="db32d-113">Ciąg połączenia urządzenia jest używany do nawiązania Edison Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="db32d-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="db32d-114">Parametry połączenia Centrum IoT jest używany do nawiązania połączenia tożsamości tego urządzenia, który reprezentuje Edison w Centrum IoT Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="db32d-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="db32d-115">Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="db32d-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="db32d-116">Użyj `iot-sample` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="db32d-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="db32d-117">Pobierz ciąg połączenia Centrum IoT, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="db32d-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="db32d-118">`{my hub name}`jest to nazwa określona podczas tworzenia Centrum IoT i zarejestrowana Edison.</span><span class="sxs-lookup"><span data-stu-id="db32d-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="db32d-119">Pobierz ciąg połączenia urządzenia, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="db32d-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="db32d-120">Użyj `myinteledison` jako wartość `{device id}` Jeśli wartości nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="db32d-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="db32d-121">Skonfiguruj połączenie z urządzeniem</span><span class="sxs-lookup"><span data-stu-id="db32d-121">Configure the device connection</span></span>
1. <span data-ttu-id="db32d-122">Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="db32d-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```

2. <span data-ttu-id="db32d-123">Otwórz plik konfiguracji urządzenia `config-edison.json` w programie Visual Studio Code, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="db32d-123">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![Config.JSON](media/iot-hub-intel-edison-lessons/lesson3/config.png)
3. <span data-ttu-id="db32d-125">Wprowadź następujące elementy zastępcze w `config-edison.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="db32d-125">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="db32d-126">Zastąp **[urządzenia nazwa hosta lub adres IP]** z adresu IP urządzenia, które są oznaczone w dół, podczas konfigurowania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="db32d-126">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="db32d-127">Zastąp **[parametry połączenia urządzenia IoT]** z `device connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="db32d-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="db32d-128">Zastąp **[parametry połączenia Centrum IoT]** z `iot hub connection string` uzyskaną.</span><span class="sxs-lookup"><span data-stu-id="db32d-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="db32d-129">Nie ma potrzeby `azure_storage_connection_string` w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="db32d-129">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="db32d-130">Zachować, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="db32d-130">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="db32d-131">Wdrażanie i uruchamianie przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="db32d-131">Deploy and run the sample application</span></span>
<span data-ttu-id="db32d-132">Wdrażanie i uruchamianie przykładowej aplikacji na Edison, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="db32d-132">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="db32d-133">Sprawdź, czy działa przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="db32d-133">Verify that the sample application works</span></span>
<span data-ttu-id="db32d-134">Powinny pojawić się LED, która jest połączona z Edison migający co dwie sekundy.</span><span class="sxs-lookup"><span data-stu-id="db32d-134">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="db32d-135">Za każdym razem, gdy LED miga, przykładowej aplikacji wysyła komunikat do Centrum IoT i sprawdza, czy wiadomość została pomyślnie wysłana do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="db32d-135">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="db32d-136">Ponadto każdy komunikat odebrany przez Centrum IoT jest drukowany w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="db32d-136">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="db32d-137">Przykładowa aplikacja kończy się automatycznie po wysłaniu wiadomości 20.</span><span class="sxs-lookup"><span data-stu-id="db32d-137">The sample application terminates automatically after sending 20 messages.</span></span>

![Przykładowa aplikacja z wysłanych i odebranych komunikatów][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="db32d-139">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="db32d-139">Summary</span></span>
<span data-ttu-id="db32d-140">Został wdrożony i Uruchom nowe migania przykładową aplikację na Edison do wysyłania wiadomości urządzenia do chmury do Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="db32d-140">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="db32d-141">Wiadomości jest teraz monitorować, ponieważ są one zapisywane na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="db32d-141">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db32d-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="db32d-142">Next steps</span></span>
<span data-ttu-id="db32d-143">[Odczytywanie wiadomości utrwalane w magazynie Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="db32d-143">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-node-lesson3-read-table-storage.md