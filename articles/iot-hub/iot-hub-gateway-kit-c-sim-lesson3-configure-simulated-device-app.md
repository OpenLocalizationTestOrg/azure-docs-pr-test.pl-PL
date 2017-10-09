---
title: "Symulowane urządzenie & Azure IoT bramy - lekcji 3: uruchamianie aplikacji przykładowych | Dokumentacja firmy Microsoft"
description: "Uruchom symulowane urządzenie przykładowej aplikacji toosend temperatury danych tooyour Centrum IoT"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: toocloud danych
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
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Konfigurowanie i uruchamianie aplikacji przykładowej symulowane urządzenie

## <a name="what-you-will-do"></a>Będzie wykonywać

- Repozytorium przykładowej hello klonowania.
- Użyj hello Azure CLI tooget informacje o Twoich Centrum IoT i urządzenia logicznego symulowane urządzenie przykładowej aplikacji. Skonfiguruj i uruchom hello symulowane urządzenie przykładowej aplikacji.

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

W tym artykule dowiesz się:

- Jak tooconfigure i wykonywania hello symulowane urządzenie przykładowej aplikacji.

## <a name="what-you-need"></a>Co jest potrzebne

Pomyślnie zakończono

- [Create an IoT hub and register your device](iot-hub-gateway-kit-c-sim-lesson2-register-device.md) (Tworzenie centrum IoT Hub i rejestrowanie urządzenia)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Klonowanie hello próbki repozytorium toohello hosta

repozytorium przykładowej hello tooclone, wykonaj następujące kroki na komputerze hosta hello:

1. Otwórz wiersz polecenia w systemie Windows lub Otwórz terminal macOS lub Ubuntu.
2. Uruchom następujące polecenia hello:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a>Skonfiguruj hello symulowane urządzenie i NUC Twojego

1. Plik konfiguracji Otwórz hello `config.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:

   ```bash
   code config.json
   ```

2. Zastąp `"has_sensortag": true` z`"has_sensortag": false`

   ![Nie masz urządzenia Sensor tag analizy czasowej konfiguracji](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Otwórz `config-gateway.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Znajdź powitania po wierszu kodu i Zastąp `[device hostname or IP address]` z adresu IP adres lub nazwę hosta hello Intel NUC.
   ![Zrzut ekranu przedstawiający konfiguracji bramy](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a>Pobierz ciąg połączenia hello urządzenia logicznego centrum IoT

Witaj tooget parametry połączenia Centrum Azure IoT urządzenia logicznego, uruchom następujące polecenie na komputerze hosta hello hello:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`jest hello nazwę Centrum IoT, który został użyty. Użyj bramy iot jako wartość hello `{resource group name}` i użyj mydevice jako wartość hello `{device id}` nie zmiany wartości hello Lekcja 2.

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a>Skonfiguruj hello symulowane urządzenie chmury przekazywania przykładowej aplikacji

tooconfigure i wykonywania hello symulowane urządzenie chmury przekazać przykładowej aplikacji, wykonaj następujące kroki na komputerze hosta hello:

1. Otwórz `config-sensortag.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Zrzut ekranu przedstawiający Sensor tag konfiguracji](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Wprowadź następujące elementy zastępcze w kodzie hello hello:
   - Zastąp `[IoT hub name]` o nazwie Centrum IoT hello.
   - Zastąp `[IoT device connection string]` z ciągu połączenia hello urządzenia logicznego centrum IoT.

3. Uruchamianie aplikacji hello.

   Wdrażanie i uruchamianie aplikacji hello, uruchamiając następujące polecenie hello:

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a>Weryfikowanie działania aplikacji przykładowej hello

Teraz powinny być widoczne dane wyjściowe podobne do następujących hello:

![Symulowane urządzenie przykładowej aplikacji w danych wyjściowych](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

Aplikacja Hello wysyła Centrum IoT tooyour danych temperatury, który jest ważny przez 40 sekund.

## <a name="summary"></a>Podsumowanie

Pomyślnie skonfigurowano i wykonywania hello symulowane urządzenie chmury przekazywania przykładowej aplikacji, która wysyła Centrum IoT tooyour danych z symulowane urządzenie.

## <a name="next-steps"></a>Następne kroki
[Read messages from your IoT hub](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md) (Odczytywanie komunikatów z centrum IoT Hub)