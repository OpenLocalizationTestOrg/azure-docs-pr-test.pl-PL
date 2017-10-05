---
title: "Nawiązać Edison firmy Intel (węzeł) Azure IoT — 4 lekcji: komunikaty | Dokumentacja firmy Microsoft"
description: "Przykładowa aplikacja działa na Edison i monitoruje komunikaty przychodzące z Centrum IoT. Nowe zadanie gulp wysyła komunikaty do Edison z Centrum IoT miga LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Formant arduino doprowadziły z sieci web, kontroli arduino przeprowadzony za pośrednictwem sieci web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: bc738bf6-e38d-4024-82d7-39b6c2d4bacb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 76ea59acd848f60663a0c821bff42166aac5823a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a>Uruchom przykładową aplikację do odbierania wiadomości chmury do urządzenia
W tym artykule wdrożono przykładową aplikację na Intel Edison. Przykładowa aplikacja monitoruje komunikaty przychodzące z Centrum IoT. Można również uruchomić zadanie gulp na komputerze do wysyłania komunikatów do Edison z Centrum IoT. Gdy przykładowa aplikacja odbiera komunikaty, miga LED. Jeśli masz problemy, poszukaj rozwiązania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-do"></a>Będzie wykonywać
* Połącz przykładowej aplikacji do Centrum IoT.
* Wdrażanie i uruchamianie przykładowej aplikacji.
* Z Centrum IoT Edison miga LED wysyłać wiadomości.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak monitorować komunikaty przychodzące z Centrum IoT.
* Sposób wysyłania komunikatów chmury do urządzenia z Centrum IoT do Edison.

## <a name="what-you-need"></a>Co jest potrzebne
* Edison firmy Intel, skonfigurować do używania. Aby dowiedzieć się, jak skonfigurować Edison, zobacz [Skonfiguruj urządzenie][configure-your-device].
* Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure. Aby dowiedzieć się, jak utworzyć Centrum IoT, zobacz [utworzenie Centrum IoT Azure][create-your-azure-iot-hub].

## <a name="connect-the-sample-application-to-your-iot-hub"></a>Połącz przykładowej aplikacji do Centrum IoT
1. Upewnij się, że jesteś w folderze repozytorium `iot-hub-node-edison-getting-started`. Otwórz przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia:

   ```bash
   cd Lesson4
   code .
   ```

   Plik `app` podfolder jest plik źródłowy klucza, który zawiera kod umożliwiający monitorowanie komunikatów przychodzących z Centrum IoT. `blinkLED` LED miga funkcji.

   ![Struktura repozytorium w przykładowej aplikacji][repo-structure]
2. Inicjowanie pliku konfiguracji, uruchamiając następujące polecenia:

   ```bash
   npm install
   gulp init
   ```

   Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na tym komputerze, wszystkie konfiguracje są dziedziczone, można pominąć krok do zadania, wdrażanie i uruchamianie przykładowej aplikacji. Jeśli ukończono kroki [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na innym komputerze, należy zastąpić symbole zastępcze w `config-edison.json` pliku. `config-edison.json` Plik znajduje się w podfolderze folderu macierzystego.

   ![Zawartość pliku konfiguracji edison.json](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Zastąp **[urządzenia nazwa hosta lub adres IP]** z adresu IP urządzenia, które są oznaczone w dół, podczas konfigurowania urządzenia.
   * Zastąp **[parametry połączenia urządzenia IoT]** z parametrami połączenia urządzenia, który można uzyskać, uruchamiając `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` polecenia.
   * Zastąp **[parametry połączenia Centrum IoT]** z parametrami połączenia Centrum IoT, który można uzyskać, uruchamiając `az iot hub show-connection-string --name {my hub name}` polecenia.

## <a name="deploy-and-run-the-sample-application"></a>Wdrażanie i uruchamianie przykładowej aplikacji
Wdrażanie i uruchamianie przykładowej aplikacji na Edison, uruchamiając następujące polecenia:

```bash
gulp deploy && gulp run
```

Polecenie gulp wdraża przykładowej aplikacji do Edison. Następnie uruchomi aplikację na Edison i oddzielnych zadań na komputerze hosta do wysyłania wiadomości migania 20 do Edison z Centrum IoT.

Po uruchomieniu aplikacji przykładowej, rozpoczyna nasłuchiwanie wiadomości z Centrum IoT. W tym samym czasie zadań gulp wysyła komunikaty "blink" z Centrum IoT do Edison. Dla każdego komunikatu migania odbierająca Edison wywołuje przykładowej aplikacji `blinkLED` funkcja miga LED.

Zadanie gulp wyśle 20 komunikatów z Centrum IoT do Edison powinna zostać wyświetlona migania LED co dwie sekundy. Komunikat "stop", która kończy działanie aplikacji jest ostatni z nich.

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości][gulp-command-and-blink-messages]

## <a name="summary"></a>Podsumowanie
Na Edison miga LED zostało pomyślnie wysłane wiadomości z Centrum IoT. Następne zadanie jest opcjonalne: Zmień włączenia i wyłączenia zachowanie LED.

## <a name="next-steps"></a>Następne kroki
[Zmień włączenia i wyłączenia zachowanie LED][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-node-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-node-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-node-lesson4-change-led-behavior.md