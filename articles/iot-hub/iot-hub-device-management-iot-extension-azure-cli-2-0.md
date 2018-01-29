---
title: "Azure IoT zarządzania urządzeniami z rozszerzeniem IoT Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Użyj rozszerzenia IoT Azure CLI 2.0 narzędzia do zarządzania urządzeniami Centrum IoT Azure, bezpośrednie metod i opcje zarządzania żądaną właściwości dwie."
services: iot-hub
documentationcenter: 
author: chrissie926
manager: timlt
tags: 
keywords: "Zarządzanie urządzeniami iot platformy Azure, zarządzanie urządzeniami Centrum azure iot, urządzenia iot zarządzania, zarządzanie urządzeniami Centrum iot"
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/16/2018
ms.author: menchi
ms.openlocfilehash: 760a6a30513308aa59c5e253e3b91e28cf9e3241
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/18/2018
---
# <a name="use-the-iot-extension-for-azure-cli-20-for-azure-iot-hub-device-management"></a>Użyj rozszerzenia IoT 2.0 interfejsu wiersza polecenia platformy Azure do zarządzania urządzeniami Centrum IoT Azure

![Diagram end-to-end](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

[Rozszerzenie IoT Azure CLI 2.0](https://github.com/Azure/azure-iot-cli-extension) to nowe open source rozszerzenia IoT, który dodaje do możliwości [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview?view=azure-cli-latest) zawiera polecenia do interakcji z usługi Azure resource manager i zarządzanie punktami końcowymi. Azure CLI 2.0 zawiera polecenia do interakcji z usługi Azure resource manager i zarządzanie punktami końcowymi. Na przykład służy 2.0 interfejsu wiersza polecenia platformy Azure do utworzenia maszyny Wirtualnej platformy Azure lub Centrum IoT. Rozszerzenia interfejsu wiersza polecenia umożliwia usługą platformy Azure rozszerzyć nadanie wiersza polecenia platformy Azure, dostęp do dodatkowych możliwości specyficznych dla usług. Rozszerzenie IoT udostępnia deweloperom IoT wiersza polecenia możliwości Centrum IoT, krawędzi IoT i inicjowania obsługi usługi IoT Hub urządzeń.

| Opcja zarządzania          | Zadanie                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Metody bezpośrednie             | Należy skonfigurować urządzenie działania, takie jak uruchamianie lub zatrzymywanie wysyłania wiadomości i ponownego uruchamiania urządzenia.                                        |
| Żądany dwie właściwości    | Umieść urządzenia do określonych stanach, takie jak ustawienie LED zielony lub ustawienie interwału wysyłania danych telemetrycznych do 30 minut.         |
| Dwie zgłoszone właściwości   | Pobierz stan zgłoszonego urządzenia. Na przykład urządzenie zgłasza, że LED jest teraz migający.                                    |
| Dwie tagów                  | Przechowywane metadane dotyczące urządzeń w chmurze. Na przykład lokalizacja wdrożenia automaty maszyny.                         |
| Urządzenie dwie zapytań        | Wyślij zapytanie do wszystkich urządzeń twins można pobrać z dowolnego warunki, np. zidentyfikowanie urządzenia, które są dostępne do użycia. |

Aby uzyskać bardziej szczegółowe wyjaśnienia dotyczące różnic oraz wskazówki dotyczące używania tych opcji, zobacz [wskazówki komunikację urządzenia do chmury](iot-hub-devguide-d2c-guidance.md) i [wskazówki dotyczące komunikacji chmury do urządzenia](iot-hub-devguide-c2d-guidance.md).

> [!NOTE]
> Bliźniacze reprezentacje urządzeń to dokumenty JSON, które przechowują informacje o stanie urządzenia (metadane, konfiguracje i warunki). Centrum IoT utrzymuje dwie urządzenia, dla każdego urządzenia, które nawiązuje z nim połączenie. Aby uzyskać więcej informacji na temat twins urządzenia, zobacz [wprowadzenie twins urządzenia](iot-hub-node-node-twin-getstarted.md).

## <a name="what-you-learn"></a>Omawiane zagadnienia

Dowiedz się, przy użyciu rozszerzenia IoT Azure CLI 2.0 z różnymi opcjami zarządzania na komputerze deweloperskim.

## <a name="what-you-do"></a>Co zrobić

Uruchom Azure CLI w wersji 2.0 i rozszerzenia IoT Azure CLI 2.0 z różnymi opcjami zarządzania.

## <a name="what-you-need"></a>Co jest potrzebne

- Samouczek [skonfigurować Twoje urządzenie](iot-hub-raspberry-pi-kit-node-get-started.md) ukończone, która obejmuje następujące wymagania:
  - Aktywna subskrypcja platformy Azure.
  - Centrum Azure IoT w ramach Twojej subskrypcji.
  - Aplikacja klienta, która wysyła komunikaty do Centrum Azure IoT.

- Upewnij się, że urządzenie korzysta z aplikacji klienckiej, w tym samouczku.

- [Python 2.7x lub Python 3.x](https://www.python.org/downloads/)

- Zainstaluj interfejs wiersza polecenia platformy Azure 2.0. Prostym sposobem instalowania w systemie Windows jest pobranie i zainstalowanie [MSI](https://aka.ms/InstallAzureCliWindows). Można również postępuj zgodnie z instrukcjami instalacji [Microsoft Docs](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) można skonfigurować 2.0 interfejsu wiersza polecenia platformy Azure w danym środowisku. Co najmniej w wersji 2.0 interfejsu wiersza polecenia platformy Azure musi być 2.0.24 lub nowszej. Użyj `az –version` do sprawdzania poprawności. 

- Zainstaluj rozszerzenie IoT. Najprostszym sposobem jest uruchomienie `az extension add --name azure-cli-iot-ext`. [Plik readme rozszerzenia IoT](https://github.com/Azure/azure-iot-cli-extension/blob/master/README.md) opisano kilka sposobów, aby zainstalować to rozszerzenie.


## <a name="login-to-your-azure-account"></a>Zaloguj się do konta platformy Azure

Nazwa logowania do konta platformy Azure, uruchamiając następujące polecenie:

```bash
az login
```

## <a name="use-the-iot-extension-for-azure-cli-20-with-direct-methods"></a>Użyj rozszerzenia IoT Azure CLI 2.0 za pomocą metod bezpośredniego

```bash
az iot hub invoke-device-method --device-id <your device id> --hub-name <your hub name> --method-name <the method name> --method-payload <the method payload>
```

## <a name="use-the-iot-extension-for-azure-cli-20-with-twins-desired-properties"></a>Za pomocą rozszerzenia IoT Azure CLI 2.0 dwie w odpowiednich właściwościach

Ustaw interwał żądanej właściwości = 3000, uruchamiając następujące polecenie:

```bash
az iot hub device-twin update -n <your hub name> -d <your device id> --set properties.desired.interval = 3000
```

Tej właściwości można odczytać z urządzenia.

## <a name="use-the-iot-extension-for-azure-cli-20-with-twins-reported-properties"></a>Używane rozszerzenie IoT Azure CLI 2.0 z właściwościami zgłoszonego przez dwie

Pobierz właściwości zgłoszonego urządzenia, uruchamiając następujące polecenie:

```bash
az iot hub device-twin update -n <your hub name> -d <your device id> --set properties.reported.interval = 3000
```

Jedna z właściwości jest $metadata. $lastUpdated przedstawiającego urządzenie tym czas ostatniego wysłania lub odebrania wiadomości.

## <a name="use-the-iot-extension-for-azure-cli-20-with-twins-tags"></a>Używane rozszerzenie IoT Azure CLI 2.0 tagów w dwie

Wyświetlanie znaczników i właściwości urządzenia, uruchamiając następujące polecenie:

```bash
az iot hub device-twin show --hub-name <your hub name> --device-id <your device id>
```

Dodaj rolę pola = temperatury i wilgotności na urządzeniu, uruchamiając następujące polecenie:

```bash
az iot hub device-twin update --hub-name <your hub name> --device-id <your device id> --set tags = '{"role":"temperature&humidity"}}'
```

## <a name="use-the-iot-extension-for-azure-cli-20-with-device-twins-queries"></a>Użyj rozszerzenia IoT Azure CLI 2.0 z zapytaniami twins urządzenia

Zapytanie urządzeń przy użyciu tagu roli = "temperatury i wilgotności", uruchamiając następujące polecenie:

```bash
az iot hub query --hub-name <your hub name> --query-command "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

Wszystkie urządzenia z wyjątkiem tych z tagiem roli zapytania = "temperatury i wilgotności", uruchamiając następujące polecenie:

```bash
az iot hub query --hub-name <your hub name> --query-command "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a>Kolejne kroki

Kiedy znasz już jak monitorować urządzenia do chmury wiadomości i wysyłanie komunikatów chmury do urządzenia między urządzenia IoT i Centrum IoT Azure.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]