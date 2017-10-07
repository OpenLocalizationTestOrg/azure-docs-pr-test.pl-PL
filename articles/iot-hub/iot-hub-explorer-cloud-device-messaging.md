---
title: "urządzenie chmury Azure IoT Hub aaaManage wiadomości z Centrum iothub explorer | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello Centrum iothub explorer interfejsu wiersza polecenia narzędzia toomonitor urządzenia toocloud (D2C) wiadomości i wysyłać chmury toodevice (C2D) w usłudze Azure IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Centrum iothub Eksploratorze chmury urządzenia wiadomości, toodevice chmury Centrum iot, chmury toodevice obsługi wiadomości"
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="0f376-104">Użyj Eksploratora Centrum iothub toosend i odbieranie komunikatów między urządzeniem a Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="0f376-104">Use iothub-explorer toosend and receive messages between your device and IoT Hub</span></span>

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="0f376-106">[Centrum iothub explorer](https://github.com/azure/iothub-explorer) ma kilka poleceń, który ułatwia zarządzanie Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0f376-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="0f376-107">Ten samouczek koncentruje się na temat toosend explorer Centrum iothub toouse i odbieranie komunikatów między urządzeniem i Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0f376-107">This tutorial focuses on how toouse iothub-explorer toosend and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0f376-108">Co dowiesz się</span><span class="sxs-lookup"><span data-stu-id="0f376-108">What you will learn</span></span>

<span data-ttu-id="0f376-109">Dowiesz się, jak toouse explorer Centrum iothub toomonitor urządzenia do chmury wiadomości i toosend wiadomości chmury do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0f376-109">You learn how toouse iothub-explorer toomonitor device-to-cloud messages and toosend cloud-to-device messages.</span></span> <span data-ttu-id="0f376-110">Komunikaty urządzenia do chmury można dane czujników, że urządzenie zbiera dane, a następnie wysyła tooyour Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0f376-110">Device-to-cloud messages could be sensor data that your device collects and then sends tooyour IoT hub.</span></span> <span data-ttu-id="0f376-111">Komunikaty chmury do urządzenia może być poleceń Centrum IoT i wysyła tooblink urządzenia tooyour LED, który jest tooyour podłączonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="0f376-111">Cloud-to-device messages could be commands that your IoT hub sends tooyour device tooblink an LED that is connected tooyour device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="0f376-112">Będzie wykonywać</span><span class="sxs-lookup"><span data-stu-id="0f376-112">What you will do</span></span>

- <span data-ttu-id="0f376-113">Użyj Eksploratora Centrum iothub toomonitor urządzenia do chmury wiadomości.</span><span class="sxs-lookup"><span data-stu-id="0f376-113">Use iothub-explorer toomonitor device-to-cloud messages.</span></span>
- <span data-ttu-id="0f376-114">Użyj Eksploratora Centrum iothub toosend chmury do urządzenia wiadomości.</span><span class="sxs-lookup"><span data-stu-id="0f376-114">Use iothub-explorer toosend cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0f376-115">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="0f376-115">What you need</span></span>

- <span data-ttu-id="0f376-116">Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="0f376-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="0f376-117">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0f376-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="0f376-118">Centrum Azure IoT w ramach Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0f376-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="0f376-119">Aplikacja klienta, która wysyła komunikaty tooyour Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="0f376-119">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="0f376-120">Eksplorator Centrum iothub.</span><span class="sxs-lookup"><span data-stu-id="0f376-120">iothub-explorer.</span></span> <span data-ttu-id="0f376-121">([Zainstalować explorer Centrum iothub](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="0f376-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="0f376-122">Monitorowanie wiadomości urządzenia do chmury</span><span class="sxs-lookup"><span data-stu-id="0f376-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="0f376-123">toomonitor wiadomości, które są wysyłane z Centrum IoT tooyour urządzenie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0f376-123">toomonitor messages that are sent from your device tooyour IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="0f376-124">Otwórz okno konsoli.</span><span class="sxs-lookup"><span data-stu-id="0f376-124">Open a console window.</span></span>
1. <span data-ttu-id="0f376-125">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0f376-125">Run hello following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="0f376-126">Pobierz `<device-id>` i `<IoTHubConnectionString>` z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0f376-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="0f376-127">Upewnij się, że po zakończeniu samouczka poprzedniej hello.</span><span class="sxs-lookup"><span data-stu-id="0f376-127">Make sure you've finished hello previous tutorial.</span></span> <span data-ttu-id="0f376-128">Możesz toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` Jeśli masz `HostName`, `SharedAccessKeyName` i `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="0f376-128">Or you can try toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="0f376-129">Wysyłanie komunikatów z chmury do urządzeń</span><span class="sxs-lookup"><span data-stu-id="0f376-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="0f376-130">toosend wiadomości z urządzenia tooyour Centrum IoT, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0f376-130">toosend a message from your IoT hub tooyour device, follow these steps:</span></span>

1. <span data-ttu-id="0f376-131">Otwórz okno konsoli.</span><span class="sxs-lookup"><span data-stu-id="0f376-131">Open a console window.</span></span>
1. <span data-ttu-id="0f376-132">Uruchom sesję w Centrum IoT, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0f376-132">Start a session on your IoT hub by running hello following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="0f376-133">Wyślij komunikat tooyour urządzenia, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="0f376-133">Send a message tooyour device by running hello following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="0f376-134">polecenie Hello miga hello LED tooyour podłączonych urządzeń i wysyła urządzenia tooyour wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="0f376-134">hello command blinks hello LED that is connected tooyour device and sends hello message tooyour device.</span></span>

> [!Note]
> <span data-ttu-id="0f376-135">Nie istnieje potrzeba dla toosend urządzenia hello Centrum IoT potwierdzenia oddzielne polecenie tooyour wstecz po otrzymaniu wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="0f376-135">There is no need for hello device toosend a separate ack command back tooyour IoT hub upon receiving hello message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f376-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0f376-136">Next steps</span></span>

<span data-ttu-id="0f376-137">Znasz już jak toomonitor urządzenia do chmury wiadomości i wysyłanie komunikatów chmury do urządzenia między urządzenia IoT i Centrum IoT Azure.</span><span class="sxs-lookup"><span data-stu-id="0f376-137">You’ve learned how toomonitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
