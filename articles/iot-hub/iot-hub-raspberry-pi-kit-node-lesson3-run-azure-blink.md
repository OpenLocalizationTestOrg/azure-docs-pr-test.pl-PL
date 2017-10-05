---
title: "Nawiązać Pi malina (węzeł) Azure IoT — lekcji 3: uruchamianie przykładowych | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowej aplikacji do malina Pi 3, który wysyła wiadomości do Centrum IoT i miganie LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "BLINK doprowadziły pi chmury, doprowadziły migania z chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1c03283ee276a954f822d6eca5f0a3d5f93ec64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a>Uruchom przykładową aplikację do wysyłania wiadomości urządzenia do chmury
## <a name="what-you-will-do"></a>Będzie wykonywać
W tym artykule opisano sposób wdrażania i uruchom przykładową aplikację na malina Pi 3, który wysyła wiadomości do Centrum IoT. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
Zostanie sposób użycia narzędzia gulp do wdrożenia i uruchomienia przykładowej aplikacji Node.js na Pi.

## <a name="what-you-need"></a>Co jest potrzebne
* Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenia aplikacji funkcji platformy Azure i konto magazynu do przetwarzania i przechowywania wiadomości Centrum IoT](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Pobrać parametry połączenia koncentratora i urządzenia IoT
Ciąg połączenia urządzenia jest używany przez Twoje Pi nawiązać połączenia z Centrum IoT. Ciąg połączenia Centrum IoT jest używany do nawiązania połączenia w rejestrze tożsamości w Centrum IoT do zarządzania urządzeniami, które mogą nawiązać połączenia z Centrum IoT. 

* Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:

```bash
az iot hub list -g iot-sample --query [].name
```

Użyj `iot-sample` jako wartość `{resource group name}` Jeśli wartości nie można zmienić.

* Pobierz ciąg połączenia Centrum IoT, uruchamiając następujące polecenie z wiersza polecenia platformy Azure:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`jest to nazwa określona podczas tworzenia Centrum IoT i zarejestrowana Pi.

* Pobierz ciąg połączenia urządzenia, uruchamiając następujące polecenie:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Użyj `myraspberrypi` jako wartość `{device id}` Jeśli wartości nie można zmienić.

## <a name="configure-the-device-connection"></a>Skonfiguruj połączenie z urządzeniem
1. Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:
   
   ```bash
   npm install
   gulp init
   ```
2. Otwórz plik konfiguracji urządzenia `config-raspberrypi.json` w programie Visual Studio Code, uruchamiając następujące polecenie:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Wprowadź następujące elementy zastępcze w `config-raspberrypi.json` pliku:
   
   * Zastąp **[urządzenia nazwa hosta lub adres IP]** z urządzenia IP adres lub nazwa hosta uzyskanego od `device-discovery-cli` lub wartość dziedziczone po skonfigurowaniu urządzenia.
   * Zastąp **[parametry połączenia urządzenia IoT]** z `device connection string` uzyskaną.
   * Zastąp **[parametry połączenia Centrum IoT]** z `iot hub connection string` uzyskaną.

Aktualizacja `config-raspberrypi.json` plików, dzięki czemu można wdrożyć przykładowej aplikacji z komputera.

## <a name="deploy-and-run-the-sample-application"></a>Wdrażanie i uruchamianie przykładowej aplikacji
Wdrażanie i uruchamianie przykładowej aplikacji na Pi, uruchamiając następujące polecenie:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a>Sprawdź, czy działa przykładowej aplikacji
Powinny pojawić się LED, który jest podłączony do Pi migający co dwie sekundy. Za każdym razem, gdy LED miga, przykładowej aplikacji wysyła komunikat do Centrum IoT i sprawdza, czy wiadomość została pomyślnie wysłana do Centrum IoT. Ponadto każdy komunikat odebrany przez Centrum IoT jest drukowany w oknie konsoli. Przykładowa aplikacja kończy się automatycznie po wysłaniu wiadomości 20.

![Przykładowa aplikacja z wysłanych i odebranych komunikatów](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a>Podsumowanie
Został wdrożony i Uruchom nowe migania przykładową aplikację na Pi do wysyłania wiadomości urządzenia do chmury do Centrum IoT. Teraz można monitorować wiadomości, ponieważ są one zapisywane na koncie magazynu.

## <a name="next-steps"></a>Następne kroki
[Odczytywanie wiadomości utrwalane w magazynie Azure](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

