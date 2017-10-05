---
featureFlags: usabilla
title: "Pi malinowe (węzeł) nawiązania połączenia platformy Azure IoT — lekcji 4: chmury do urządzenia | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja działa na Pi i monitoruje komunikaty przychodzące z Centrum IoT. Nowe zadanie gulp wysyła komunikaty do Pi z Centrum IoT miga LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "chmury do urządzenia, wiadomości z chmury"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b8e9e51391f9b6737762b3404658297ab4c82783
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="run-the-sample-application-to-receive-cloud-to-device-messages"></a>Uruchom przykładową aplikację do odbierania wiadomości chmury do urządzenia
W tym artykule wdrożono przykładową aplikację na malina Pi 3. Przykładowa aplikacja monitoruje komunikaty przychodzące z Centrum IoT. Można również uruchomić zadanie gulp na komputerze do wysyłania komunikatów do Pi z Centrum IoT. Gdy przykładowa aplikacja odbiera komunikaty, miga LED. Jeśli masz problemy z poszukiwanie rozwiązania na [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-do"></a>Będzie wykonywać
* Połącz przykładowej aplikacji do Centrum IoT.
* Wdrażanie i uruchamianie przykładowej aplikacji.
* Wysyłanie wiadomości z Centrum IoT do Pi miga LED.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak monitorować komunikaty przychodzące z Centrum IoT
* Sposób wysyłania komunikatów chmury do urządzenia z Centrum IoT do Pi.

## <a name="what-you-need"></a>Co jest potrzebne
* Malinowe Pi 3, skonfigurować do używania. Aby dowiedzieć się, jak skonfigurować Pi, zobacz [Skonfiguruj urządzenie](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).
* Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure. Aby dowiedzieć się, jak utworzyć Centrum IoT, zobacz [utworzenie Centrum IoT i zarejestruj malina Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-the-sample-application-to-your-iot-hub"></a>Połącz przykładowej aplikacji do Centrum IoT
1. Upewnij się, że jesteś w folderze repozytorium `iot-hub-node-raspberrypi-getting-started`. Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:
   
   ```bash
   cd Lesson4
   code .
   ```
   
   Powiadomienie `app.js` w pliku `app` podfolderu. `app.js` Plik jest plikiem źródła klucza, który zawiera kod umożliwiający monitorowanie komunikatów przychodzących z Centrum IoT. `blinkLED` LED miga funkcji.
   
   ![Struktura repozytorium w przykładowej aplikacji](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. Inicjowanie pliku konfiguracji za pomocą następujących poleceń:
   
   ```bash
   npm install
   gulp init
   ```
   
   Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) na tym komputerze są dziedziczone wszystkie konfiguracje, więc możesz przejść do zadań, wdrażanie i uruchamianie przykładowej aplikacji. Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) na innym komputerze, należy zastąpić symbole zastępcze w `config-raspberrypi.json` pliku. `config-raspberrypi.json` Plik znajduje się w podfolderze folderu macierzystego.
   
   ![Zawartość pliku konfiguracji raspberrypi.json](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Zastąp **[urządzenia nazwa hosta lub adres IP]** o adresie IP Pi lub nazwę hosta, który można uzyskać, uruchamiając `devdisco list --eth` polecenia.
* Zastąp **[parametry połączenia urządzenia IoT]** z parametrami połączenia urządzenia, który można uzyskać, uruchamiając `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` polecenia.
* Zastąp **[parametry połączenia Centrum IoT]** z parametrami połączenia Centrum IoT, który można uzyskać, uruchamiając `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` polecenia.

> [!NOTE]
> Uruchom **system gulp instalacji narzędzia** oraz, jeśli nie zostało to jeszcze zrobione, Lekcja 1.

## <a name="deploy-and-run-the-sample-application"></a>Wdrażanie i uruchamianie przykładowej aplikacji
Wdrażanie i uruchamianie przykładowej aplikacji na Pi, uruchamiając następujące polecenie:

```bash
gulp deploy && gulp run
```

Polecenie wdraża przykładowej aplikacji do Pi. Następnie uruchomi aplikację na Pi i oddzielnych zadań na komputerze hosta do wysyłania wiadomości migania 20 do Pi z Centrum IoT.

Po uruchomieniu aplikacji przykładowej, rozpoczyna nasłuchiwanie wiadomości z Centrum IoT. W tym samym czasie zadań gulp wysyła kilka "blink" wiadomości z Centrum IoT do Pi. Dla każdego komunikatu migania odbierająca Pi wywołuje przykładowej aplikacji `blinkLED` funkcja miga LED.

Powinny pojawić się migania LED co dwie sekundy zadań gulp wyśle 20 komunikatów z Centrum IoT do Pi. Ostatnią jest komunikat "stop", która określa, że aplikacja przestanie działać.

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a>Podsumowanie
Na Pi miga LED zostało pomyślnie wysłane wiadomości z Centrum IoT. Następne zadanie jest opcjonalne: Zmień włączenia i wyłączenia zachowanie LED.

## <a name="next-steps"></a>Następne kroki
[Zmień włączenia i wyłączenia zachowanie LED](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

