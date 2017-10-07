---
title: "Zarządzanie urządzeniami IoT z Centrum iothub explorer aaaAzure | Dokumentacja firmy Microsoft"
description: "Narzędzie hello Centrum iothub explorer interfejsu wiersza polecenia do zarządzania urządzeniami Centrum IoT Azure, metody bezpośredniego hello i opcje zarządzania żądaną właściwości Witaj dwie."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Zarządzanie urządzeniami iot platformy Azure, zarządzanie urządzeniami Centrum azure iot, urządzenia iot zarządzania, zarządzanie urządzeniami Centrum iot"
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="6d566-104">Użyj Eksploratora Centrum iothub do zarządzania urządzeniami Centrum IoT Azure</span><span class="sxs-lookup"><span data-stu-id="6d566-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="6d566-106">[Centrum iothub explorer](https://github.com/azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia uruchamianego w tożsamości urządzenia toomanage komputera hosta w rejestrze Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6d566-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer toomanage device identities in your IoT hub registry.</span></span> <span data-ttu-id="6d566-107">Pochodzi on z opcji zarządzania, których można używać tooperform różnych zadań.</span><span class="sxs-lookup"><span data-stu-id="6d566-107">It comes with management options that you can use tooperform various tasks.</span></span>

| <span data-ttu-id="6d566-108">Opcja zarządzania</span><span class="sxs-lookup"><span data-stu-id="6d566-108">Management option</span></span>          | <span data-ttu-id="6d566-109">Zadanie</span><span class="sxs-lookup"><span data-stu-id="6d566-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6d566-110">Metody bezpośrednie</span><span class="sxs-lookup"><span data-stu-id="6d566-110">Direct methods</span></span>             | <span data-ttu-id="6d566-111">Zwiększanie działania, takie jak uruchamianie lub zatrzymywanie wysyłania wiadomości i ponownego uruchamiania urządzenia hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6d566-111">Make a device act such as starting or stopping sending messages or rebooting hello device.</span></span>                                        |
| <span data-ttu-id="6d566-112">Żądany dwie właściwości</span><span class="sxs-lookup"><span data-stu-id="6d566-112">Twin desired properties</span></span>    | <span data-ttu-id="6d566-113">Wprowadzone urządzenia do określonych stanach, takie jak ustawianie toogreen LED lub ustawienie telemetrii hello wysłać too30 interwał w minutach.</span><span class="sxs-lookup"><span data-stu-id="6d566-113">Put a device into certain states, such as setting an LED toogreen or setting hello telemetry send interval too30 minutes.</span></span>         |
| <span data-ttu-id="6d566-114">Dwie zgłoszone właściwości</span><span class="sxs-lookup"><span data-stu-id="6d566-114">Twin reported properties</span></span>   | <span data-ttu-id="6d566-115">Pobierz hello zgłosiła stan urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6d566-115">Get hello reported state of a device.</span></span> <span data-ttu-id="6d566-116">Na przykład urządzenie hello zgłasza powitalne LED jest teraz migający.</span><span class="sxs-lookup"><span data-stu-id="6d566-116">For example, hello device reports hello LED is blinking now.</span></span>                                    |
| <span data-ttu-id="6d566-117">Dwie tagów</span><span class="sxs-lookup"><span data-stu-id="6d566-117">Twin tags</span></span>                  | <span data-ttu-id="6d566-118">Przechowywania metadanych specyficznych dla urządzeń w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="6d566-118">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="6d566-119">Na przykład hello lokalizacja wdrożenia automaty maszyny.</span><span class="sxs-lookup"><span data-stu-id="6d566-119">For example, hello deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="6d566-120">Komunikaty chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="6d566-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="6d566-121">Wyślij powiadomienia tooa urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6d566-121">Send notifications tooa device.</span></span> <span data-ttu-id="6d566-122">Na przykład "jest bardzo prawdopodobne toorain dzisiaj.</span><span class="sxs-lookup"><span data-stu-id="6d566-122">For example, "It is very likely toorain today.</span></span> <span data-ttu-id="6d566-123">Nie zapomnij toobring parasola."</span><span class="sxs-lookup"><span data-stu-id="6d566-123">Don't forget toobring an umbrella."</span></span>              |
| <span data-ttu-id="6d566-124">Urządzenie dwie zapytań</span><span class="sxs-lookup"><span data-stu-id="6d566-124">Device twin queries</span></span>        | <span data-ttu-id="6d566-125">Wszystkie urządzenia twins tooretrieve zapytania z dowolnego warunki, np. zidentyfikowanie urządzenia hello, które są dostępne do użycia.</span><span class="sxs-lookup"><span data-stu-id="6d566-125">Query all device twins tooretrieve those with arbitrary conditions, such as identifying hello devices that are available for use.</span></span> |

<span data-ttu-id="6d566-126">Aby uzyskać szczegółowe informacje na temat różnic hello oraz wskazówki dotyczące używania tych opcji, zobacz [wskazówki komunikację urządzenia do chmury](iot-hub-devguide-d2c-guidance.md) i [wskazówki dotyczące komunikacji chmury do urządzenia](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="6d566-126">For more detailed explanation on hello differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6d566-127">Bliźniacze reprezentacje urządzeń to dokumenty JSON, które przechowują informacje o stanie urządzenia (metadane, konfiguracje i warunki).</span><span class="sxs-lookup"><span data-stu-id="6d566-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="6d566-128">Centrum IoT utrzymuje dwie urządzenia, dla każdego urządzenia, które łączy tooit.</span><span class="sxs-lookup"><span data-stu-id="6d566-128">IoT Hub persists a device twin for each device that connects tooit.</span></span> <span data-ttu-id="6d566-129">Aby uzyskać więcej informacji na temat twins urządzenia, zobacz [wprowadzenie twins urządzenia](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="6d566-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6d566-130">Omawiane zagadnienia</span><span class="sxs-lookup"><span data-stu-id="6d566-130">What you learn</span></span>

<span data-ttu-id="6d566-131">Dowiedz się, za pomocą Eksploratora Centrum iothub z różnymi opcjami zarządzania na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="6d566-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6d566-132">Co zrobić</span><span class="sxs-lookup"><span data-stu-id="6d566-132">What you do</span></span>

<span data-ttu-id="6d566-133">Uruchom Eksploratora Centrum iothub z różnymi opcjami zarządzania.</span><span class="sxs-lookup"><span data-stu-id="6d566-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6d566-134">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="6d566-134">What you need</span></span>

- <span data-ttu-id="6d566-135">Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje hello następujące wymagania:</span><span class="sxs-lookup"><span data-stu-id="6d566-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="6d566-136">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d566-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="6d566-137">Centrum Azure IoT w ramach Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6d566-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="6d566-138">Aplikacja klienta, która wysyła komunikaty tooyour Azure IoT hub.</span><span class="sxs-lookup"><span data-stu-id="6d566-138">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="6d566-139">Upewnij się, że urządzenie korzysta z aplikacji klienckiej hello w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="6d566-139">Make sure your device is running with hello client application during this tutorial.</span></span>
- <span data-ttu-id="6d566-140">Centrum iothub Eksploratorze [zainstalować explorer Centrum iothub](https://github.com/azure/iothub-explorer) na komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="6d566-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-tooyour-iot-hub"></a><span data-ttu-id="6d566-141">Połącz tooyour Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="6d566-141">Connect tooyour IoT hub</span></span>

<span data-ttu-id="6d566-142">Połącz Centrum IoT tooyour, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d566-142">Connect tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="6d566-143">Użyj Eksploratora Centrum iothub za pomocą metod bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="6d566-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="6d566-144">Wywołanie hello `start` metoda hello urządzenia aplikacji toosend wiadomości tooyour Centrum IoT, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d566-144">Invoke hello `start` method in hello device app toosend messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="6d566-145">Wywołanie hello `stop` metody hello urządzenia aplikacji toostop wysyłania wiadomości Centrum IoT tooyour, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d566-145">Invoke hello `stop` method in hello device app toostop sending messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="6d566-146">Użyj Centrum iothub explorer z właściwościami żądany przez dwie</span><span class="sxs-lookup"><span data-stu-id="6d566-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="6d566-147">Ustaw interwał żądanej właściwości = 3000, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d566-147">Set a desired property interval = 3000 by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="6d566-148">Ta właściwość może zostać odczytany przez urządzenie.</span><span class="sxs-lookup"><span data-stu-id="6d566-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="6d566-149">Użyj Centrum iothub explorer z właściwościami zgłoszonego przez dwie</span><span class="sxs-lookup"><span data-stu-id="6d566-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="6d566-150">Pobierz hello zgłoszone właściwości urządzenia hello uruchamiając hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6d566-150">Get hello reported properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="6d566-151">Jedna z właściwości hello jest $metadata. $lastUpdated która zawiera hello ostatniego to urządzenie wysyła i odbiera komunikat.</span><span class="sxs-lookup"><span data-stu-id="6d566-151">One of hello properties is $metadata.$lastUpdated which shows hello last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="6d566-152">Użyj Eksploratora Centrum iothub tagów w dwie</span><span class="sxs-lookup"><span data-stu-id="6d566-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="6d566-153">Wyświetl hello tagów i właściwości urządzenia hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d566-153">Display hello tags and properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="6d566-154">Dodaj rolę pola = urządzenie toohello temperatury i wilgotności, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d566-154">Add a field role = temperature&humidity toohello device by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="6d566-155">Użyj Centrum iothub explorer z komunikatami z chmury do urządzenia</span><span class="sxs-lookup"><span data-stu-id="6d566-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="6d566-156">Wyślij urządzenia toohello komunikat "Hello World", uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d566-156">Send a "Hello World" message toohello device by running hello following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="6d566-157">Zobacz [Użyj Eksploratora Centrum iothub toosend i odbieranie komunikatów między urządzeniem a Centrum IoT](iot-hub-explorer-cloud-device-messaging.md) dla scenariusza rzeczywistego użycia tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="6d566-157">See [Use iothub-explorer toosend and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="6d566-158">Użyj Centrum iothub explorer z zapytaniami twins urządzenia</span><span class="sxs-lookup"><span data-stu-id="6d566-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="6d566-159">Zapytanie urządzeń przy użyciu tagu roli = "temperatury i wilgotności", uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d566-159">Query devices with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="6d566-160">Wszystkie urządzenia z wyjątkiem tych z tagiem roli zapytania = "temperatury i wilgotności", uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="6d566-160">Query all devices except those with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="6d566-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d566-161">Next steps</span></span>

<span data-ttu-id="6d566-162">Znasz już jak toouse Centrum iothub-explorer z różnymi opcjami zarządzania.</span><span class="sxs-lookup"><span data-stu-id="6d566-162">You've learned how toouse iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
