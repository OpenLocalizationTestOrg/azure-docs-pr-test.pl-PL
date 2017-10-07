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
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a>Użyj Eksploratora Centrum iothub do zarządzania urządzeniami Centrum IoT Azure

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[Centrum iothub explorer](https://github.com/azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia uruchamianego w tożsamości urządzenia toomanage komputera hosta w rejestrze Centrum IoT. Pochodzi on z opcji zarządzania, których można używać tooperform różnych zadań.

| Opcja zarządzania          | Zadanie                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Metody bezpośrednie             | Zwiększanie działania, takie jak uruchamianie lub zatrzymywanie wysyłania wiadomości i ponownego uruchamiania urządzenia hello urządzenia.                                        |
| Żądany dwie właściwości    | Wprowadzone urządzenia do określonych stanach, takie jak ustawianie toogreen LED lub ustawienie telemetrii hello wysłać too30 interwał w minutach.         |
| Dwie zgłoszone właściwości   | Pobierz hello zgłosiła stan urządzenia. Na przykład urządzenie hello zgłasza powitalne LED jest teraz migający.                                    |
| Dwie tagów                  | Przechowywania metadanych specyficznych dla urządzeń w chmurze hello. Na przykład hello lokalizacja wdrożenia automaty maszyny.                         |
| Komunikaty chmury do urządzenia   | Wyślij powiadomienia tooa urządzenia. Na przykład "jest bardzo prawdopodobne toorain dzisiaj. Nie zapomnij toobring parasola."              |
| Urządzenie dwie zapytań        | Wszystkie urządzenia twins tooretrieve zapytania z dowolnego warunki, np. zidentyfikowanie urządzenia hello, które są dostępne do użycia. |

Aby uzyskać szczegółowe informacje na temat różnic hello oraz wskazówki dotyczące używania tych opcji, zobacz [wskazówki komunikację urządzenia do chmury](iot-hub-devguide-d2c-guidance.md) i [wskazówki dotyczące komunikacji chmury do urządzenia](iot-hub-devguide-c2d-guidance.md).

> [!NOTE]
> Bliźniacze reprezentacje urządzeń to dokumenty JSON, które przechowują informacje o stanie urządzenia (metadane, konfiguracje i warunki). Centrum IoT utrzymuje dwie urządzenia, dla każdego urządzenia, które łączy tooit. Aby uzyskać więcej informacji na temat twins urządzenia, zobacz [wprowadzenie twins urządzenia](iot-hub-node-node-twin-getstarted.md).

## <a name="what-you-learn"></a>Omawiane zagadnienia

Dowiedz się, za pomocą Eksploratora Centrum iothub z różnymi opcjami zarządzania na komputerze deweloperskim.

## <a name="what-you-do"></a>Co zrobić

Uruchom Eksploratora Centrum iothub z różnymi opcjami zarządzania.

## <a name="what-you-need"></a>Co jest potrzebne

- Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje hello następujące wymagania:
  - Aktywna subskrypcja platformy Azure.
  - Centrum Azure IoT w ramach Twojej subskrypcji.
  - Aplikacja klienta, która wysyła komunikaty tooyour Azure IoT hub.
- Upewnij się, że urządzenie korzysta z aplikacji klienckiej hello w tym samouczku.
- Centrum iothub Eksploratorze [zainstalować explorer Centrum iothub](https://github.com/azure/iothub-explorer) na komputerze deweloperskim.

## <a name="connect-tooyour-iot-hub"></a>Połącz tooyour Centrum IoT

Połącz Centrum IoT tooyour, uruchamiając następujące polecenie hello:

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a>Użyj Eksploratora Centrum iothub za pomocą metod bezpośredniego

Wywołanie hello `start` metoda hello urządzenia aplikacji toosend wiadomości tooyour Centrum IoT, uruchamiając następujące polecenie hello:

```bash
iothub-explorer device-method <your device Id> start
```

Wywołanie hello `stop` metody hello urządzenia aplikacji toostop wysyłania wiadomości Centrum IoT tooyour, uruchamiając następujące polecenie hello:

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a>Użyj Centrum iothub explorer z właściwościami żądany przez dwie

Ustaw interwał żądanej właściwości = 3000, uruchamiając następujące polecenie hello:

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

Ta właściwość może zostać odczytany przez urządzenie.

## <a name="use-iothub-explorer-with-twins-reported-properties"></a>Użyj Centrum iothub explorer z właściwościami zgłoszonego przez dwie

Pobierz hello zgłoszone właściwości urządzenia hello uruchamiając hello następujące polecenie:

```bash
iothub-explorer get-twin <your device id>
```

Jedna z właściwości hello jest $metadata. $lastUpdated która zawiera hello ostatniego to urządzenie wysyła i odbiera komunikat.

## <a name="use-iothub-explorer-with-twins-tags"></a>Użyj Eksploratora Centrum iothub tagów w dwie

Wyświetl hello tagów i właściwości urządzenia hello, uruchamiając następujące polecenie hello:

```bash
iothub-explorer get-twin <your device id>
```

Dodaj rolę pola = urządzenie toohello temperatury i wilgotności, uruchamiając następujące polecenie hello:

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a>Użyj Centrum iothub explorer z komunikatami z chmury do urządzenia

Wyślij urządzenia toohello komunikat "Hello World", uruchamiając następujące polecenie hello:

```bash
iothub-explorer send <device-id> "Hello World"
```

Zobacz [Użyj Eksploratora Centrum iothub toosend i odbieranie komunikatów między urządzeniem a Centrum IoT](iot-hub-explorer-cloud-device-messaging.md) dla scenariusza rzeczywistego użycia tego polecenia.

## <a name="use-iothub-explorer-with-device-twins-queries"></a>Użyj Centrum iothub explorer z zapytaniami twins urządzenia

Zapytanie urządzeń przy użyciu tagu roli = "temperatury i wilgotności", uruchamiając następujące polecenie hello:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

Wszystkie urządzenia z wyjątkiem tych z tagiem roli zapytania = "temperatury i wilgotności", uruchamiając następujące polecenie hello:

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>Następne kroki

Znasz już jak toouse Centrum iothub-explorer z różnymi opcjami zarządzania.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
