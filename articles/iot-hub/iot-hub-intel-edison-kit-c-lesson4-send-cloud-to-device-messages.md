---
title: 'Connect Intel Edison (C) tooAzure IoT - 4 lekcji: komunikaty | Dokumentacja firmy Microsoft'
description: "Przykładowa aplikacja działa na Edison i monitoruje komunikaty przychodzące z Centrum IoT. Nowe zadanie gulp wysyła komunikaty tooEdison z Twojej hello tooblink Centrum IoT LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Formant arduino doprowadziły z sieci web, kontroli arduino przeprowadzony za pośrednictwem sieci web"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 820d38f3-d3b8-4249-9e2b-f1b9b771e62f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f0424506ff755e0b9514684787b37584d406d320
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Uruchom tooreceive aplikacji przykładowej wiadomości chmury do urządzenia
W tym artykule wdrożono przykładową aplikację na Intel Edison. aplikacja przykładowa Hello monitoruje komunikaty przychodzące z Centrum IoT. Można również uruchomić zadanie gulp na tooEdison wiadomości toosend Twojego komputera z Centrum IoT. Gdy hello Przykładowa aplikacja odbiera wiadomości powitania, miga hello LED. Jeśli masz problemy, poszukaj rozwiązania na powitania [Rozwiązywanie problemów z strony][troubleshooting].

## <a name="what-you-will-do"></a>Będzie wykonywać
* Połącz Centrum IoT tooyour hello przykładowej aplikacji.
* Wdrażanie i uruchamianie hello przykładowej aplikacji.
* Wysyłanie wiadomości z Twojej IoT hub tooEdison tooblink hello LED.

## <a name="what-you-will-learn"></a>Co dowiesz się
W tym artykule dowiesz się:
* Jak komunikaty przychodzące toomonitor z Centrum IoT.
* Jak chmury urządzenia toosend komunikaty z sieci tooEdison Centrum IoT.

## <a name="what-you-need"></a>Co jest potrzebne
* Edison firmy Intel, skonfigurować do używania. toolearn tooset się Edison, zobacz temat [Skonfiguruj urządzenie][configure-your-device].
* Centrum IoT, która jest tworzona w Twojej subskrypcji platformy Azure. toolearn jak toocreate Centrum IoT, zobacz [utworzenie Centrum IoT Azure][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Połącz z Centrum IoT tooyour hello przykładowej aplikacji
1. Upewnij się, że jesteś w folderze repozytorium hello `iot-hub-c-edison-getting-started`. Otwórz hello przykładowej aplikacji w programie Visual Studio Code, uruchamiając następujące polecenia hello:

   ```bash
   cd Lesson4
   code .
   ```

   Plik Hello w hello `app` podfolder jest plik źródłowy klucza hello, który zawiera komunikaty przychodzące toomonitor kodu hello z Centrum IoT hello. Witaj `blinkLED` funkcja miganie hello LED.

   ![Struktura repozytorium w hello przykładowej aplikacji][repo-structure]
2. Inicjowanie pliku konfiguracji hello, uruchamiając następujące polecenia hello:

   ```bash
   npm install
   gulp init
   ```

   Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na tym komputerze, wszystkie konfiguracje hello są dziedziczone, można pominąć hello krok toohello zadania wdrażania i uruchomiona hello przykładowej aplikacji. Jeśli ukończono kroki hello [Tworzenie funkcji platformy Azure aplikacji i konto magazynu] [ create-an-azure-function-app-and-storage-account] na innym komputerze, należy symbole zastępcze hello tooreplace w hello `config-edison.json` pliku. Witaj `config-edison.json` plik znajduje się w podfolderze hello folderu macierzystego.

   ![Zawartość pliku config edison.json hello](media/iot-hub-intel-edison-lessons/lesson4/config-edison.png)

   * Zastąp **[urządzenia nazwa hosta lub adres IP]** z adresu IP urządzenia hello oznaczone w dół, podczas konfigurowania urządzenia.
   * Zastąp **[parametry połączenia urządzenia IoT]** z hello parametry połączenia urządzenia, które można uzyskać, uruchamiając hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` polecenia.
   * Zastąp **[parametry połączenia Centrum IoT]** z hello parametry połączenia Centrum IoT, które można uzyskać, uruchamiając hello `az iot hub show-connection-string --name {my hub name}` polecenia.

   > [!NOTE]
   > Uruchom **system gulp instalacji narzędzia** oraz, jeśli nie zostało to jeszcze zrobione, Lekcja 1.

## <a name="deploy-and-run-hello-sample-application"></a>Wdrażanie i uruchamianie hello przykładowej aplikacji
Wdrażanie i uruchamianie aplikacji przykładowej hello na Edison, uruchamiając następujące polecenia hello:

```bash
gulp deploy && gulp run
```

polecenie gulp Hello wdraża hello przykładowej aplikacji tooEdison. Następnie uruchomieniu aplikacji hello na Edison i oddzielnych zadań na hoście tooEdison wiadomości migania toosend 20 komputera z Centrum IoT.

Po uruchomieniu aplikacji przykładowej hello rozpoczyna nasłuchiwanie toomessages z Centrum IoT. W tym samym czasie hello gulp zadań wysyła komunikaty "blink" z Twojej tooEdison Centrum IoT. Dla każdego komunikatu migania odbierająca Edison hello przykładowej aplikacji wywołuje hello `blinkLED` funkcja tooblink hello LED.

Powinny pojawić się migania LED hello co dwie sekundy jako hello system gulp zadań wysyła 20 komunikatów z Twojej tooEdison Centrum IoT. Hello ostatnio jedna jest zatrzymuje aplikacji hello komunikat "stop".

![Przykładowa aplikacja z system gulp polecenia i blink wiadomości][gulp-command-and-blink-messages]

## <a name="summary"></a>Podsumowanie
Zostało pomyślnie wysłane wiadomości z Twojej IoT hub tooEdison tooblink hello LED. następne zadanie Hello jest opcjonalny: Zmień hello włączać i wyłączać zachowanie hello LED.

## <a name="next-steps"></a>Następne kroki
[Zmień hello włączać i wyłączać zachowanie hello LED][change-the-on-and-off-behavior-of-the-led]

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[configure-your-device]: iot-hub-intel-edison-kit-c-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-intel-edison-lessons/lesson4/repo_structure_c.png
[create-an-azure-function-app-and-storage-account]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[gulp-command-and-blink-messages]: media/iot-hub-intel-edison-lessons/lesson4/gulp_blink_c.png
[change-the-on-and-off-behavior-of-the-led]: iot-hub-intel-edison-kit-c-lesson4-change-led-behavior.md