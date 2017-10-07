---
title: "Urządzeń Sensor tag & bramy IoT Azure - Lekcja 3: uruchamianie aplikacji przykładowych | Dokumentacja firmy Microsoft"
description: "Uruchom cz przykładowych aplikacji tooreceive danych z Sensor tag cz i z Centrum IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Cz aplikacji, czujnik Monitoruj aplikację, zbierania danych czujnika, danych z czujników, toocloud danych czujnika"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>Konfigurowanie i uruchamianie cz przykładowej aplikacji

## <a name="what-you-will-do"></a>Będzie wykonywać

- Repozytorium przykładowej hello klonowania. 
- Konfigurowanie hello łączność między Sensor tag i Intel NUC. 
- Użyj hello Azure CLI tooget informacje o Twoich Centrum IoT i Sensor tag przykładową aplikację cz (Bluetooth energii niski). Skonfiguruj i uruchom hello cz przykładowej aplikacji. 

Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się

W tym artykule dowiesz się:

- Jak tooconfigure i wykonywania hello cz przykładowej aplikacji.

## <a name="what-you-need"></a>Co jest potrzebne

Pomyślnie zakończono

- [Utwórz Centrum IoT i zarejestruj Sensor tag](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Klonowanie hello próbki repozytorium toohello hosta

repozytorium przykładowej hello tooclone, wykonaj następujące kroki na komputerze hosta hello:

1. Otwórz okno wiersza polecenia w systemie Windows lub Otwórz terminal macOS lub Ubuntu.
2. Uruchom następujące polecenia hello:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a>Konfigurowanie hello łączność między Sensor tag i Intel NUC

tooset się hello łączności, wykonaj następujące kroki na komputerze hosta hello:

1. Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. Otwórz `config-gateway.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. Znajdź powitania po wierszu kodu i Zastąp `[device hostname or IP address]` z hello IP adres lub nazwę hosta Intel NUC.
   ![Zrzut ekranu przedstawiający konfiguracji bramy](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Zainstaluj narzędzia pomocnika na NUC firmy Intel, uruchamiając następujące polecenie hello:

   ```bash
   gulp install-tools
   ```

5. Włącz Sensor tag, naciskając przycisk zasilania hello jako hello poniższej ilustracji, a powinien blink LED hello zielony.

   ![Włącz Sensor Tag](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. Skanuj urządzeń Sensor tag, uruchamiając następujące polecenia hello:

   ```bash
   gulp discover-sensortag
   ```

7. Testowanie łączności hello między hello Sensor tag i NUC firmy Intel, uruchamiając następujące polecenie hello:

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   Zastąp `{mac address}` z hello adres MAC, które zostały uzyskane w poprzednim kroku hello.

## <a name="get-hello-connection-string-of-sensortag"></a>Pobierz ciąg połączenia hello Sensor tag

Witaj tooget parametry połączenia Centrum Azure IoT Sensor tag, uruchom następujące polecenie na komputerze hosta hello hello:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`jest hello nazwę Centrum IoT, który został użyty. Użyj bramy iot jako wartość hello `{resource group name}` i użyj mydevice jako wartość hello `{device id}` nie zmiany wartości hello Lekcja 2.

## <a name="configure-hello-ble-sample-application"></a>Skonfiguruj hello cz przykładowej aplikacji

tooconfigure i wykonywania hello cz przykładowej aplikacji, wykonaj następujące kroki na komputerze hosta hello:

1. Otwórz `config-sensortag.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![Zrzut ekranu przedstawiający Sensor tag konfiguracji](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Wprowadź następujące elementy zastępcze w kodzie hello hello:
   - Zastąp `[IoT hub name]` o nazwie Centrum IoT hello, który został użyty.
   - Zastąp `[IoT device connection string]` z ciągu połączenia hello Sensor tag, który został uzyskany.
   - Zastąp `[device_mac_address]` z hello adres MAC hello Sensor tag, który został uzyskany.

3. Uruchom hello cz przykładowej aplikacji.

   Witaj toorun cz przykładowej aplikacji, wykonaj następujące kroki na komputerze hosta hello:

   1. Włącz Sensor tag.

   2. Wdrażanie i uruchamianie aplikacji przykładowej cz hello na Intel NUC, uruchamiając następujące polecenie hello:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a>Sprawdź, czy działa hello cz przykładowej aplikacji

Powinna pojawić się dane wyjściowe podobne do następujących hello:

![Dane wyjściowe aplikacji przykładowej cz](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

Hello Przykładowa aplikacja przechowuje zbieranie danych temperatury i przesłanie tooyour Centrum IoT. Witaj przykładowej aplikacji kończy się automatycznie po wysłaniu 40 sekund.

## <a name="summary"></a>Podsumowanie

Został pomyślnie skonfigurować hello łączność między Sensor tag i Intel NUC i uruchom cz przykładowej aplikacji, która zbiera i wysyła dane z Centrum IoT tooyour Sensor tag. Wszystko jest gotowe toolearn jak tooverify, który otrzymał Centrum IoT hello danych.

## <a name="next-steps"></a>Następne kroki
[Read messages from your IoT hub](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md) (Odczytywanie komunikatów z centrum IoT Hub)