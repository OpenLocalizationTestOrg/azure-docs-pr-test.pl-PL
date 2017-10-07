---
title: "Urządzeń Sensor tag & bramy IoT Azure - Lekcja 3: odczytywać wiadomości | Dokumentacja firmy Microsoft"
description: "Uruchom przykładowy kod w wiadomości powitania tooread komputera hosta z Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dane w chmurze hello, zbierania danych w chmurze, usługi w chmurze iot, dane iot"
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
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="e8cf2-104">Odczytywanie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e8cf2-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="e8cf2-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="e8cf2-105">What you will do</span></span>

- <span data-ttu-id="e8cf2-106">Uruchom przykładowy kod na hoście komputer tooread komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="e8cf2-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="e8cf2-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="e8cf2-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="e8cf2-108">What you will learn</span></span>

<span data-ttu-id="e8cf2-109">Jak toouse hello system gulp narzędzie tooread komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e8cf2-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="e8cf2-110">What you need</span></span>

- <span data-ttu-id="e8cf2-111">Witaj cz przykładowej aplikacji, który został przeprowadzony pomyślnie lekcji 3.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-111">hello BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="e8cf2-112">Pobrać parametry połączenia koncentratora i urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="e8cf2-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="e8cf2-113">ciąg połączenia urządzenia Hello jest używany przez Centrum IoT tooyour tooconnect urządzeń (Sensor tag analizy czasowej lub symulowane urządzenie).</span><span class="sxs-lookup"><span data-stu-id="e8cf2-113">hello device connection string is used by your device (TI SensorTag or simulated device) tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="e8cf2-114">Parametry połączenia Centrum IoT Hello jest rejestru tożsamości toohello tooconnect używanych w urządzeniami hello toomanage Centrum IoT, które są dozwolone Centrum IoT tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="e8cf2-115">Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e8cf2-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="e8cf2-116">Użyj `iot-gateway` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
- <span data-ttu-id="e8cf2-117">Pobierz ciąg połączenia Centrum IoT hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="e8cf2-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="e8cf2-118">`{my hub name}`to nazwa hello określony Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="e8cf2-119">Skonfiguruj połączenie z urządzeniem hello hello przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="e8cf2-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="e8cf2-120">Plik konfiguracji urządzenia hello aktualizacji `config-azure.json` tak, aby można było odczytać wiadomości z Centrum IoT na komputerze hosta.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-120">Update hello device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="e8cf2-121">toodo, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e8cf2-121">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="e8cf2-122">Otwórz `config-azure.json` w programie Visual Studio Code, uruchamiając następujące polecenie w oknie konsoli hello:</span><span class="sxs-lookup"><span data-stu-id="e8cf2-122">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="e8cf2-123">Wprowadź następujące elementy zastępcze w hello hello `config-azure.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="e8cf2-123">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![Zrzut ekranu przedstawiający konfiguracji platformy azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="e8cf2-125">Zastąp `[IoT hub connection string]` z hello ciąg połączenia Centrum IoT, który został uzyskany.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-125">Replace `[IoT hub connection string]` with hello IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="e8cf2-126">Odczytywanie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e8cf2-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="e8cf2-127">Jeśli Sensor tag analizy czasowej, upewnij się, że już włączone Twoje Sensor tag.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="e8cf2-128">Uruchom hello bramy przykładowej aplikacji i odczytać Centrum IoT wiadomości powitania następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e8cf2-128">Run hello gateway sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="e8cf2-129">polecenie Hello uruchamia hello cz przykładowej aplikacji, która odczytuje i pakietów danych temperatury Sensor tag lub symulowane urządzenie i wysyła Centrum IoT tooyour wiadomość hello co 2 sekundy.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-129">hello command runs hello BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends hello message tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="e8cf2-130">Spowoduje również utworzenie wiadomość hello tooreceive procesu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-130">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="e8cf2-131">wiadomości powitania, które są wysyłane i odebranych znajdują się wszystkie wyświetlane natychmiast na powitania sam oknie w konsoli hello komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-131">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="e8cf2-132">wystąpienie aplikacji przykładowej Hello zakończy się automatycznie w 40 sekund.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-132">hello sample application instance will terminate automatically in 40 seconds.</span></span>

![Cz przykładową aplikację z wysłanych i odebranych komunikatów](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="e8cf2-134">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="e8cf2-134">Summary</span></span>

<span data-ttu-id="e8cf2-135">Uruchomieniu tooread kod przykładowy wiadomości z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-135">You've run a sample code tooread messages from your IoT hub.</span></span> <span data-ttu-id="e8cf2-136">Wszystko jest gotowe tooread hello wiadomości, które są przechowywane w magazynie tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e8cf2-136">You're ready tooread hello messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8cf2-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8cf2-137">Next steps</span></span>
<span data-ttu-id="e8cf2-138">[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md) (Tworzenie aplikacji funkcji platformy Azure i konta usługi Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="e8cf2-138">[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)</span></span>


