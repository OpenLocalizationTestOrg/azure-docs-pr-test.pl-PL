---
title: "Symulowane urządzenie & Azure IoT bramy - lekcji 3: odczytywać wiadomości | Dokumentacja firmy Microsoft"
description: "Uruchom przykładowy kod w wiadomości powitania tooread komputera hosta z Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dane w chmurze hello, zbierania danych w chmurze, usługi w chmurze iot, dane iot"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="64a10-104">Odczytywanie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="64a10-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="64a10-105">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="64a10-105">What you will do</span></span>

- <span data-ttu-id="64a10-106">Uruchom przykładowy kod na hoście komputer tooread komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="64a10-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="64a10-107">Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="64a10-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="64a10-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="64a10-108">What you will learn</span></span>

<span data-ttu-id="64a10-109">Jak toouse hello system gulp narzędzie tooread komunikaty z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="64a10-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="64a10-110">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="64a10-110">What you need</span></span>

- <span data-ttu-id="64a10-111">Przykładowe symulowane urządzenie Hello w [Konfigurowanie i uruchamianie Chmury symulowane urządzenie przekazać przykładowej aplikacji](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="64a10-111">hello simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="64a10-112">Pobrać parametry połączenia koncentratora i urządzenia IoT</span><span class="sxs-lookup"><span data-stu-id="64a10-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="64a10-113">ciąg połączenia urządzenia Hello jest używany przez Centrum IoT tooyour tooconnect symulowane urządzenie.</span><span class="sxs-lookup"><span data-stu-id="64a10-113">hello device connection string is used by your simulated device tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="64a10-114">Parametry połączenia Centrum IoT Hello jest rejestru tożsamości toohello tooconnect używanych w urządzeniami hello toomanage Centrum IoT, które są dozwolone Centrum IoT tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="64a10-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="64a10-115">Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="64a10-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="64a10-116">Użyj `iot-gateway` jako wartość hello `{resource group name}` nie zostały wprowadzone zmiany.</span><span class="sxs-lookup"><span data-stu-id="64a10-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="64a10-117">Pobierz ciąg połączenia Centrum IoT hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="64a10-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="64a10-118">`{my hub name}`to nazwa hello określony Lekcja 2.</span><span class="sxs-lookup"><span data-stu-id="64a10-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="64a10-119">Skonfiguruj połączenie z urządzeniem hello hello przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="64a10-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="64a10-120">Aktualizacja konfiguracji IoT hub i urządzenia połączenia w `config-azure.json` , wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="64a10-120">Update IoT hub and device connection configurations in `config-azure.json` by performing hello following steps:</span></span>

1. <span data-ttu-id="64a10-121">Otwórz `config-azure.json` w programie Visual Studio Code, uruchamiając następujące polecenie w oknie konsoli hello:</span><span class="sxs-lookup"><span data-stu-id="64a10-121">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="64a10-122">Wprowadź następujące elementy zastępcze w hello hello `config-azure.json` pliku:</span><span class="sxs-lookup"><span data-stu-id="64a10-122">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![Zrzut ekranu przedstawiający konfiguracji platformy azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="64a10-124">Zastąp `[IoT hub connection string]` z hello parametry połączenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="64a10-124">Replace `[IoT hub connection string]` with hello IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="64a10-125">Odczytywanie wiadomości z Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="64a10-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="64a10-126">Uruchom hello symulowane urządzenie przykładowej aplikacji i odczytać Centrum IoT wiadomości powitania następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="64a10-126">Run hello simulated device sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="64a10-127">polecenie Hello uruchamia aplikacji hello, który wysyła wiadomości tooyour IoT hub co 2 sekundy.</span><span class="sxs-lookup"><span data-stu-id="64a10-127">hello command runs hello application that sends messages tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="64a10-128">Spowoduje również utworzenie wiadomość hello tooreceive procesu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="64a10-128">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="64a10-129">wiadomości powitania, które są wysyłane i odebranych znajdują się wszystkie wyświetlane natychmiast na powitania sam oknie w konsoli hello komputera-hosta.</span><span class="sxs-lookup"><span data-stu-id="64a10-129">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="64a10-130">Aplikacja Hello zakończy działanie w 40 sekund.</span><span class="sxs-lookup"><span data-stu-id="64a10-130">hello application will exit in 40 seconds.</span></span>

![Symulowane przykładową aplikację z wysłane i odebrane wiadomości](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="64a10-132">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="64a10-132">Summary</span></span>

<span data-ttu-id="64a10-133">Pomyślnie uruchomiono Centrum IoT tooyour danych toosend hello przykładowej aplikacji z symulowanego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="64a10-133">You've successfully run hello sample application toosend data tooyour IoT hub with simulated device.</span></span> <span data-ttu-id="64a10-134">Wiadomości powitania, które zostały wysłane do Centrum IoT tooyour również zostały przeczytane.</span><span class="sxs-lookup"><span data-stu-id="64a10-134">You've also read hello messages that have been sent tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64a10-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64a10-135">Next steps</span></span>
<span data-ttu-id="64a10-136">[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md) (Tworzenie aplikacji funkcji platformy Azure i konta usługi Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="64a10-136">[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)</span></span>


