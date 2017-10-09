---
title: "Connect Raspberry pi (C) tooAzure IoT — lekcji 3: uruchamianie przykładowych | Dokumentacja firmy Microsoft"
description: "Wdrażanie i uruchamianie przykładowych aplikacji tooRaspberry Pi 3, która wysyła Centrum IoT tooyour wiadomości i miganie hello LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "BLINK doprowadziły pi chmury, doprowadziły migania z chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Uruchom toosend aplikacji przykładowej wiadomości urządzenia do chmury
## <a name="what-you-will-do"></a>Będzie wykonywać
W tym artykule opisano sposób toodeploy i uruchom przykładową aplikację na malina Pi 3, który wysyła wiadomości tooyour Centrum IoT. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Co dowiesz się
Dowiesz się, jak toouse hello system gulp toodeploy narzędzia i uruchomić hello przykładowej aplikacji Node.js na Pi.

## <a name="what-you-need"></a>Co jest potrzebne
* Przed rozpoczęciem tego zadania musi pomyślnie ukończył [tworzenie aplikacji funkcji platformy Azure i magazynu konta tooprocess i Magazyn Centrum IoT wiadomości](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Pobrać parametry połączenia koncentratora i urządzenia IoT
ciąg połączenia urządzenia Hello jest używany przez Centrum IoT tooyour tooconnect Pi. Parametry połączenia Centrum IoT Hello jest rejestru tożsamości toohello tooconnect używanych w urządzeniami hello toomanage Centrum IoT, które są dozwolone Centrum IoT tooyour tooconnect. 

* Lista z centra IoT w grupie zasobów, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:

```bash
az iot hub list -g iot-sample --query [].name
```

Użyj `iot-sample` jako wartość hello `{resource group name}` Jeśli hello wartość nie zostanie zmieniona.

* Pobierz ciąg połączenia Centrum IoT hello, uruchamiając następujące polecenie z wiersza polecenia platformy Azure hello:

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

`{my hub name}`to nazwa hello określone podczas tworzenia Centrum IoT i zarejestrowana Pi.

* Pobierz ciąg połączenia urządzenia hello, uruchamiając następujące polecenie hello:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

Użyj `myraspberrypi` jako wartość hello `{device id}` Jeśli hello wartość nie zostanie zmieniona.

## <a name="configure-hello-device-connection"></a>Skonfiguruj połączenie z urządzeniem hello
1. Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> Uruchom **system gulp instalacji narzędzia** oraz, jeśli nie zostało to jeszcze zrobione, Lekcja 1.

2. Plik konfiguracji urządzenia Otwórz hello `config-raspberrypi.json` w programie Visual Studio Code, uruchamiając następujące polecenie hello:
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![Config.JSON](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. Wprowadź następujące elementy zastępcze w hello hello `config-raspberrypi.json` pliku:
   
   * Zastąp **[urządzenia nazwa hosta lub adres IP]** z hello urządzenia IP adres lub nazwa hosta otrzymano z `device-discovery-cli` lub z wartością hello dziedziczone po skonfigurowaniu urządzenia.
   * Zastąp **[parametry połączenia urządzenia IoT]** z hello `device connection string` uzyskaną.
   * Zastąp **[parametry połączenia Centrum IoT]** z hello `iot hub connection string` uzyskaną.

> [!NOTE]
> Nie ma potrzeby `azure_storage_connection_string` w tym artykule. Zachować, ponieważ jest.

Aktualizacja hello `config-raspberrypi.json` plików, dzięki czemu można wdrożyć hello przykładowej aplikacji z komputera.

## <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello na Pi, uruchamiając następujące polecenie hello:

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a>Sprawdź, czy działa hello przykładowej aplikacji
Powinny pojawić się hello LED, który jest połączony tooPi migający co dwie sekundy. Za każdym razem, gdy hello LED miga, hello przykładowej aplikacji wysyła z Centrum IoT tooyour wiadomości i sprawdza, czy tę wiadomość hello została pomyślnie wysłana tooyour Centrum IoT. Ponadto każdy komunikat odebrany przez Centrum IoT hello jest drukowany w oknie konsoli hello. Witaj przykładowej aplikacji kończy się automatycznie po wysłaniu wiadomości 20.

![Przykładowa aplikacja z wysłanych i odebranych komunikatów](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a>Podsumowanie
Zostały wdrożone i uruchom hello nowe migania przykładowej aplikacji w Centrum IoT tooyour Pi toosend wiadomości urządzenia do chmury. Jak są one zapisywane na koncie magazynu toohello teraz monitorować wiadomości.

## <a name="next-steps"></a>Następne kroki
[Odczytywanie wiadomości utrwalane w magazynie Azure](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

