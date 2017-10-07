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
# <a name="read-messages-from-your-iot-hub"></a>Odczytywanie wiadomości z Centrum IoT

## <a name="what-you-will-do"></a>Będzie wykonywać

- Uruchom przykładowy kod na hoście komputer tooread komunikaty z Centrum IoT.

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

Jak toouse hello system gulp narzędzie tooread komunikaty z Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne

- Witaj cz przykładowej aplikacji, który został przeprowadzony pomyślnie lekcji 3.

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Pobrać parametry połączenia koncentratora i urządzenia IoT

ciąg połączenia urządzenia Hello jest używany przez Centrum IoT tooyour tooconnect urządzeń (Sensor tag analizy czasowej lub symulowane urządzenie). Parametry połączenia Centrum IoT Hello jest rejestru tożsamości toohello tooconnect używanych w urządzeniami hello toomanage Centrum IoT, które są dozwolone Centrum IoT tooyour tooconnect.

- Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie hello:

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   Użyj `iot-gateway` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.
- Pobierz ciąg połączenia Centrum IoT hello, uruchamiając następujące polecenie hello:

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   `{my hub name}`to nazwa hello określony Lekcja 2.

## <a name="configure-hello-device-connection-for-hello-sample-code"></a>Skonfiguruj połączenie z urządzeniem hello hello przykładowy kod

Plik konfiguracji urządzenia hello aktualizacji `config-azure.json` tak, aby można było odczytać wiadomości z Centrum IoT na komputerze hosta. toodo, wykonaj następujące kroki:

1. Otwórz `config-azure.json` w programie Visual Studio Code, uruchamiając następujące polecenie w oknie konsoli hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. Wprowadź następujące elementy zastępcze w hello hello `config-azure.json` pliku:

   ![Zrzut ekranu przedstawiający konfiguracji platformy azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   Zastąp `[IoT hub connection string]` z hello ciąg połączenia Centrum IoT, który został uzyskany.

## <a name="read-messages-from-your-iot-hub"></a>Odczytywanie wiadomości z Centrum IoT

Jeśli Sensor tag analizy czasowej, upewnij się, że już włączone Twoje Sensor tag. Uruchom hello bramy przykładowej aplikacji i odczytać Centrum IoT wiadomości powitania następujące polecenie:

```bash
gulp run --iot-hub
```

polecenie Hello uruchamia hello cz przykładowej aplikacji, która odczytuje i pakietów danych temperatury Sensor tag lub symulowane urządzenie i wysyła Centrum IoT tooyour wiadomość hello co 2 sekundy. Spowoduje również utworzenie wiadomość hello tooreceive procesu podrzędnego.

wiadomości powitania, które są wysyłane i odebranych znajdują się wszystkie wyświetlane natychmiast na powitania sam oknie w konsoli hello komputera-hosta. wystąpienie aplikacji przykładowej Hello zakończy się automatycznie w 40 sekund.

![Cz przykładową aplikację z wysłanych i odebranych komunikatów](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a>Podsumowanie

Uruchomieniu tooread kod przykładowy wiadomości z Centrum IoT. Wszystko jest gotowe tooread hello wiadomości, które są przechowywane w magazynie tabeli platformy Azure.

## <a name="next-steps"></a>Następne kroki
[Create an Azure function app and Azure Storage account](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md) (Tworzenie aplikacji funkcji platformy Azure i konta usługi Azure Storage)


