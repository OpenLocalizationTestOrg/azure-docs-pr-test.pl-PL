---
featureFlags: usabilla
title: "Połącz Pi malina (węzeł) tooAzure IoT - 4 lekcji: chmury do urządzenia | Dokumentacja firmy Microsoft"
description: "Witaj Przykładowa aplikacja działa na Pi i monitoruje komunikaty przychodzące z Centrum IoT. Nowe zadanie gulp wysyła komunikaty tooPi z Twojej hello tooblink Centrum IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "toodevice chmury, wiadomości z chmury"
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
ms.openlocfilehash: d69ded4e30c27378481ab2a4fb9c5b73be7bd44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-sample-application-tooreceive-cloud-to-device-messages"></a>Uruchom hello przykładowej aplikacji tooreceive chmury do urządzenia wiadomości
W tym artykule wdrożono przykładową aplikację na malina Pi 3. aplikacja przykładowa Hello monitoruje komunikaty przychodzące z Centrum IoT. Można również uruchomić zadanie gulp na tooPi wiadomości toosend Twojego komputera z Centrum IoT. Gdy hello Przykładowa aplikacja odbiera wiadomości powitania, miga hello LED. Jeśli masz problemy z poszukiwanie rozwiązania na powitania [Rozwiązywanie problemów z strony](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-do"></a>Będzie wykonywać
* Połącz Centrum IoT tooyour hello przykładowej aplikacji.
* Wdrażanie i uruchamianie hello przykładowej aplikacji.
* Wysyłanie wiadomości z Twojej IoT hub tooPi tooblink hello LED.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak komunikaty przychodzące toomonitor z Centrum IoT
* Jak chmury urządzenia toosend komunikaty z sieci tooPi Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne
* Malinowe Pi 3, skonfigurować do używania. toolearn tooset się Pi, zobacz temat [Skonfiguruj urządzenie](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).
* Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure. toolearn jak toocreate Centrum IoT, zobacz [utworzenie Centrum IoT i zarejestruj malina Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Połącz z Centrum IoT tooyour hello przykładowej aplikacji
1. Upewnij się, że jesteś w folderze repozytorium hello `iot-hub-node-raspberrypi-getting-started`. Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:
   
   ```bash
   cd Lesson4
   code .
   ```
   
   Powiadomienie hello `app.js` pliku w hello `app` podfolderu. Witaj `app.js` plik jest plikiem klucza źródła hello, zawierający hello kodu toomonitor komunikaty przychodzące hello Centrum IoT. Witaj `blinkLED` funkcja miganie hello LED.
   
   ![Struktura repozytorium w hello przykładowej aplikacji](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. Inicjowanie pliku konfiguracji hello za pomocą hello następującego polecenia:
   
   ```bash
   npm install
   gulp init
   ```
   
   Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) na tym komputerze, wszystkie konfiguracje hello są dziedziczone, można pominąć zadań toohello wdrażanie i uruchamianie hello przykładowej aplikacji. Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) na innym komputerze, należy symbole zastępcze hello tooreplace w hello `config-raspberrypi.json` pliku. Witaj `config-raspberrypi.json` plik znajduje się w podfolderze hello folderu macierzystego.
   
   ![Zawartość pliku config raspberrypi.json hello](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Zastąp **[urządzenia nazwa hosta lub adres IP]** o adresie IP hello Pi lub hello nazwy hosta, który można pobrać przez uruchomienie hello `devdisco list --eth` polecenia.
* Zastąp **[parametry połączenia urządzenia IoT]** z hello parametry połączenia urządzenia, które można uzyskać, uruchamiając hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` polecenia.
* Zastąp **[parametry połączenia Centrum IoT]** z hello parametry połączenia Centrum IoT, które można uzyskać, uruchamiając hello `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` polecenia.

> [!NOTE]
> Uruchom **system gulp instalacji narzędzia** oraz, jeśli nie zostało to jeszcze zrobione, Lekcja 1.

## <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello na Pi, uruchamiając następujące polecenie hello:

```bash
gulp deploy && gulp run
```

polecenie Hello wdraża hello przykładowej aplikacji tooPi. Następnie uruchomieniu aplikacji hello na Pi i oddzielnych zadań na hoście tooPi wiadomości migania toosend 20 komputera z Centrum IoT.

Po uruchomieniu aplikacji przykładowej hello rozpoczyna nasłuchiwanie toomessages z Centrum IoT. W tym samym czasie hello gulp zadań wysyła komunikaty "blink" z Twojej tooPi Centrum IoT. Dla każdego komunikatu migania odbierająca Pi hello przykładowej aplikacji wywołuje hello `blinkLED` funkcja tooblink hello LED.

Powinny pojawić się migania LED hello co dwie sekundy jako hello system gulp zadań wysyła 20 komunikatów z Twojej tooPi Centrum IoT. Hello ostatnio jedną jest "stop" komunikat informujący o toostop aplikacji hello uruchomiona.

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## <a name="summary"></a>Podsumowanie
Zostało pomyślnie wysłane wiadomości z Twojej IoT hub tooPi tooblink hello LED. następne zadanie Hello jest opcjonalny: Zmień hello włączać i wyłączać zachowanie hello LED.

## <a name="next-steps"></a>Następne kroki
[Zmień hello włączać i wyłączać zachowanie hello LED](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

