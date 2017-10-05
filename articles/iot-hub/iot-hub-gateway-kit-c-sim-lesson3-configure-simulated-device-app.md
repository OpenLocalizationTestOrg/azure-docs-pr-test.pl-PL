---
title: "Symulowane urządzenie & Azure IoT bramy - lekcji 3: uruchamianie aplikacji przykładowych | Dokumentacja firmy Microsoft"
description: "Uruchom przykładową aplikację symulowane urządzenie do przesyłania danych temperatury do Centrum IoT"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: dane w chmurze
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Konfigurowanie i uruchamianie aplikacji przykładowej symulowane urządzenie

## <a name="what-you-will-do"></a>Będzie wykonywać

- Klonuj repozytorium przykładowej.
- Użyj interfejsu wiersza polecenia Azure, aby uzyskać informacje o Twoich Centrum IoT i urządzenia logicznego symulowane urządzenie przykładowej aplikacji. Skonfiguruj i uruchom przykładową aplikację symulowane urządzenie.

Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

W tym artykule dowiesz się:

- Jak skonfigurować i uruchomić aplikację przykładową symulowane urządzenie.

## <a name="what-you-need"></a>Co jest potrzebne

Pomyślnie zakończono

- [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)

## <a name="clone-the-sample-repository-to-the-host-computer"></a>Klonuj repozytorium przykładowej do komputera hosta

Klonowanie repozytorium przykładowej, wykonaj następujące kroki na komputerze-hoście:

1. Otwórz wiersz polecenia w systemie Windows lub Otwórz terminal macOS lub Ubuntu.
2. Uruchom następujące polecenia:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a>Skonfiguruj symulowane urządzenie i NUC Twojego

1. Otwórz plik konfiguracji `config.json` w programie Visual Studio Code, uruchamiając następujące polecenie:

   ```bash
   code config.json
   ```

2. Zastąp `"has_sensortag": true` z`"has_sensortag": false`

   ![Nie masz urządzenia Sensor tag analizy czasowej konfiguracji](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Otwórz `config-gateway.json` w programie Visual Studio Code, uruchamiając następujące polecenie:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Znajdź następujący wiersz kodu i Zastąp `[device hostname or IP address]` z adresu IP adres lub nazwę hosta Intel NUC.
   ![Zrzut ekranu przedstawiający konfiguracji bramy](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a>Pobierz ciąg połączenia urządzenia logicznego centrum IoT

Można pobrać ciągu połączenia Centrum Azure IoT urządzenia logicznego, uruchom następujące polecenie na komputerze-hoście:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`jest to nazwa Centrum IoT użyty. Użyj bramy iot jako wartość `{resource group name}` i użyj mydevice jako wartość `{device id}` nie zmiany wartości Lekcja 2.

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a>Skonfiguruj symulowane urządzenie chmury przekazywania przykładowej aplikacji

Aby skonfigurować i uruchomić symulowane urządzenie chmury przekazywania przykładowej aplikacji, wykonaj następujące kroki na komputerze-hoście:

1. Otwórz `config-sensortag.json` w programie Visual Studio Code, uruchamiając następujące polecenie:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Zrzut ekranu przedstawiający Sensor tag konfiguracji](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Wprowadź następujące elementy zastępcze w kodzie:
   - Zastąp `[IoT hub name]` nazwą Centrum IoT.
   - Zastąp `[IoT device connection string]` z parametrami połączenia urządzenia logicznego centrum IoT.

3. Uruchom aplikację.

   Wdrażanie i uruchamianie aplikacji, uruchamiając następujące polecenie:

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a>Weryfikowanie działania aplikacji przykładowych

Teraz powinny być widoczne dane wyjściowe podobne do następujących:

![Symulowane urządzenie przykładowej aplikacji w danych wyjściowych](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

Aplikacja wysyła dane temperatury Centrum IoT, który jest ważny przez 40 sekund.

## <a name="summary"></a>Podsumowanie

Pomyślnie zostały skonfigurowane i uruchomić aplikacji przykładowej przekazywania Chmury symulowane urządzenie, który wysyła dane do Centrum IoT z symulowane urządzenie.

## <a name="next-steps"></a>Następne kroki
[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) (Odczytywanie komunikatów z centrum IoT Hub)