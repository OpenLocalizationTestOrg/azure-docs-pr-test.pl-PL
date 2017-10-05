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
# <a name="read-messages-from-your-iot-hub"></a>Odczytywanie wiadomości z Centrum IoT

## <a name="what-you-will-do"></a>Będzie wykonywać

- Przykładowy kod należy uruchomić na komputerze hosta, aby odczytać wiadomości z Centrum IoT.

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

Jak używać narzędzia gulp odczytać wiadomości z Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne

- Przykładowej aplikacji cz, który został przeprowadzony pomyślnie lekcji 3.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Pobrać parametry połączenia koncentratora i urządzenia IoT

Ciąg połączenia urządzenia jest używany przez urządzenie (Sensor tag analizy czasowej lub symulowane urządzenie) nawiązywania połączenia z Centrum IoT. Ciąg połączenia Centrum IoT jest używany do nawiązania połączenia w rejestrze tożsamości w Centrum IoT do zarządzania urządzeniami, które mogą nawiązać połączenia z Centrum IoT.

- Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Użyj `iot-gateway` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.
- Pobierz ciąg połączenia Centrum IoT, uruchamiając następujące polecenie:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`jest to nazwa określona w Lekcja 2.

## <a name="configure-the-device-connection-for-the-sample-code"></a>Skonfiguruj połączenie z urządzeniem przykładowy kod

Aktualizuj plik konfiguracji urządzenia `config-azure.json` tak, aby można było odczytać wiadomości z Centrum IoT na komputerze hosta. Aby to zrobić, wykonaj następujące kroki:

1. Otwórz `config-azure.json` w programie Visual Studio Code, uruchamiając następujące polecenie w oknie konsoli:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Wprowadź następujące elementy zastępcze w `config-azure.json` pliku:

   ![Zrzut ekranu przedstawiający konfiguracji platformy azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Zastąp `[IoT hub connection string]` uzyskany ciągu połączenia Centrum IoT.

## <a name="read-messages-from-your-iot-hub"></a>Odczytywanie wiadomości z Centrum IoT

Jeśli Sensor tag analizy czasowej, upewnij się, że już włączone Twoje Sensor tag. Uruchom przykładową aplikację bramy i odczytywać Centrum IoT wiadomości za pomocą następującego polecenia:

```bash
gulp run --iot-hub
```

Polecenie jest uruchamiane cz przykładowej aplikacji, która odczytuje i pakietów danych temperatury Sensor tag lub symulowane urządzenie i wysyła wiadomość do Centrum IoT co 2 sekundy. Spowoduje również utworzenie proces podrzędny do odbierania wiadomości.

Komunikaty, które są wysyłane i odebranych są wszystkie natychmiast wyświetlane na tym samym oknie konsoli w komputerze hosta. Wystąpienie aplikacji przykładowej zakończy się automatycznie w 40 sekund.

![Cz przykładową aplikację z wysłanych i odebranych komunikatów](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a>Podsumowanie

Uruchomiono przykładowy kod, aby odczytać wiadomości z Centrum IoT. Wszystko jest gotowe do odczytu wiadomości, które są przechowywane w magazynie tabeli platformy Azure.

## <a name="next-steps"></a>Następne kroki
[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md) (Tworzenie aplikacji funkcji platformy Azure i konta usługi Azure Storage)


