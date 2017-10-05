---
title: "Urządzeń Sensor tag & bramy IoT Azure - Lekcja 3: odczytywać wiadomości | Dokumentacja firmy Microsoft"
description: "Przykładowy kod należy uruchomić na komputerze hosta, aby odczytać wiadomości z Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dane w chmurze, zbierania danych w chmurze, usługi w chmurze iot, dane iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 45f3595c4848d5c283cdf95604adf8d2c8d6a809
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="9ffa1-104">Odczytywanie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="9ffa1-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="9ffa1-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="9ffa1-105">What you will do</span></span>

- <span data-ttu-id="9ffa1-106">Przykładowy kod należy uruchomić na komputerze hosta, aby odczytać wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="9ffa1-107">Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9ffa1-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9ffa1-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="9ffa1-108">What you will learn</span></span>

<span data-ttu-id="9ffa1-109">Jak używać narzędzia gulp odczytać wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9ffa1-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="9ffa1-110">What you need</span></span>

- <span data-ttu-id="9ffa1-111">Przykładowej aplikacji cz, który został przeprowadzony pomyślnie lekcji 3.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-111">The BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="9ffa1-112">Pobrać parametry połączenia koncentratora i urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="9ffa1-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="9ffa1-113">Ciąg połączenia urządzenia jest używany przez urządzenie (Sensor tag analizy czasowej lub symulowane urządzenie) nawiązywania połączenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-113">The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub.</span></span> <span data-ttu-id="9ffa1-114">Ciąg połączenia Centrum IoT jest używany do nawiązania połączenia w rejestrze tożsamości w Centrum IoT do zarządzania urządzeniami, które mogą nawiązać połączenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="9ffa1-115">Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9ffa1-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="9ffa1-116">Użyj `iot-gateway` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.</span></span>
- <span data-ttu-id="9ffa1-117">Pobierz ciąg połączenia Centrum IoT, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9ffa1-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="9ffa1-118">`{my hub name}`jest to nazwa określona w Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="9ffa1-119">Skonfiguruj połączenie z urządzeniem przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="9ffa1-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="9ffa1-120">Aktualizuj plik konfiguracji urządzenia `config-azure.json` tak, aby można było odczytać wiadomości z Centrum IoT na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-120">Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="9ffa1-121">Aby to zrobić, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9ffa1-121">To do this, follow these steps:</span></span>

1. <span data-ttu-id="9ffa1-122">Otwórz `config-azure.json` w programie Visual Studio Code, uruchamiając następujące polecenie w oknie konsoli:</span><span class="sxs-lookup"><span data-stu-id="9ffa1-122">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="9ffa1-123">Wprowadź następujące elementy zastępcze w `config-azure.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="9ffa1-123">Make the following replacements in the `config-azure.json` file:</span></span>

   ![Zrzut ekranu przedstawiający konfiguracji platformy azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="9ffa1-125">Zastąp `[IoT hub connection string]` uzyskany ciągu połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-125">Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="9ffa1-126">Odczytywanie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="9ffa1-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="9ffa1-127">Jeśli Sensor tag analizy czasowej, upewnij się, że już włączone Twoje Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="9ffa1-128">Uruchom przykładową aplikację bramy i odczytywać Centrum IoT wiadomości za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="9ffa1-128">Run the gateway sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="9ffa1-129">Polecenie jest uruchamiane cz przykładowej aplikacji, która odczytuje i pakietów danych temperatury Sensor tag lub symulowane urządzenie i wysyła wiadomość do Centrum IoT co 2 sekundy.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-129">The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="9ffa1-130">Spowoduje również utworzenie proces podrzędny do odbierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-130">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="9ffa1-131">Komunikaty, które są wysyłane i odebranych są wszystkie natychmiast wyświetlane na tym samym oknie konsoli w komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-131">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="9ffa1-132">Wystąpienie aplikacji przykładowej zakończy się automatycznie w 40 sekund.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-132">The sample application instance will terminate automatically in 40 seconds.</span></span>

![Cz przykładową aplikację z wysłanych i odebranych komunikatów](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="9ffa1-134">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="9ffa1-134">Summary</span></span>

<span data-ttu-id="9ffa1-135">Uruchomiono przykładowy kod, aby odczytać wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-135">You've run a sample code to read messages from your IoT hub.</span></span> <span data-ttu-id="9ffa1-136">Wszystko jest gotowe do odczytu wiadomości, które są przechowywane w magazynie tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9ffa1-136">You're ready to read the messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ffa1-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ffa1-137">Next steps</span></span>
<span data-ttu-id="9ffa1-138">[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md) (Tworzenie aplikacji funkcji platformy Azure i konta usługi Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="9ffa1-138">[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>


