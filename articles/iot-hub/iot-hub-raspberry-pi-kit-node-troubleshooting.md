---
title: "Połącz malinowe Pi (C) do platformy Azure IoT — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony dla środowiska Node.js Pi malina"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "problemy z iot, internet rzeczy problemów"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 22cf50dc-8206-42a2-a1fc-f75fa85135fa
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9058068972ddbb674d3cd159948835dc88c4451
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a>Rozwiązywanie problemów
## <a name="hardware-issues"></a>Problemy ze sprzętem
### <a name="the-application-runs-well-but-the-led-is-not-blinking"></a>Aplikacja działa prawidłowo, ale nie jest migający LED
Ten problem dotyczy zawsze łączności obwodu sprzętu. Wykonaj następujące kroki, aby zidentyfikować problemy:

1. Sprawdź, czy wybrano poprawny **interfejs GPIO** na tablicy. Dwa porty powinna być **GND interfejs GPIO (numer Pin 6)** i **04 interfejs GPIO (7 kodu Pin)**.
2. Sprawdź, czy bieguna z Twojej LED jest poprawna. Etap dłużej powinny wskazywać **dodatnią**, szczytową numeru pin.
3. Użyj **3, 3V przypiąć** i **GND Pin** na malina Pi 3. Pi należy traktować jako potęgi kontrolera domeny. Sprawdź, czy LED działa prawidłowo.

![Specyfikacja LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Innych problemów ze sprzętem
Uzyskać informacji na temat rozwiązywania typowych problemów 3 Pi malina, zobacz [oficjalnego stronę rozwiązywania problemów](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Problemy z pakietu node.js
### <a name="no-response-during-gulp-tasks"></a>Brak odpowiedzi podczas gulp zadań
Jeśli wystąpią problemy z uruchomionych zadań gulp, można dodać `--verbose` opcji do debugowania. Spróbuj zakończenie bieżącego zadania gulp przy użyciu klawiszy Ctrl + C, a następnie uruchom następujące polecenie w oknie konsoli wyświetlić komunikaty debugowania. Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemy dotyczące odnajdywania urządzenia
Aby uzyskać pomoc w rozwiązywaniu typowych problemów z `devdisco` polecenia, wyboru [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>problemy z npm
Spróbuj zaktualizować pakiet npm za pomocą następującego polecenia:

```bash
npm install -g npm
```

Jeśli problem nadal występuje, zostaw komentarz na końcu tego artykułu lub utworzyć problem GitHub w naszym [repozytorium przykładowej](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).

## <a name="remote-debugging"></a>Debugowanie zdalne
### <a name="run-the-sample-application-in-debug-mode"></a>Uruchom przykładową aplikację w trybie debugowania
```bash
gulp run --debug
```

Gdy aparat debugowania jest gotowy, powinny pojawić się ```Debugger listening on port 5858``` w danych wyjściowych konsoli.

### <a name="configure-visual-studio-code-to-connect-to-the-remote-device"></a>Konfigurowanie programu Visual Studio Code do nawiązania połączenia z urządzeniem zdalnym
1. Otwórz **debugowania** panelu po lewej stronie.
2. Kliknij zielony **Rozpocznij debugowanie** przycisk (F5). Visual Studio Code otwiera plik launch.json.
3. Zaktualizuj plik launch.json o następującej zawartości. Zastąp `[device hostname or IP address]` z rzeczywistego urządzenia IP adres lub nazwę hosta.

> [!NOTE]
> Aby dowiedzieć się więcej na temat debugowania programu Visual Studio, zapoznaj się [debugowania w programie Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).


```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": null
        }
    ]
}
```

![Konfiguracja zdalnego debugowania](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-to-the-remote-application"></a>Dołączanie do zdalnej aplikacji
Kliknij zielony **Rozpocznij debugowanie** przycisk (F5) można rozpocząć debugowania.

Odczyt [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) Aby dowiedzieć się więcej na temat debugera.

![Zdalne debugowanie interakcyjne](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problemy z interfejsu wiersza polecenia platformy Azure
Interfejs wiersza polecenia platformy Azure (Azure CLI) jest kompilacji w wersji zapoznawczej. Aby wyszukiwać rozwiązania, można użyć [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Jeśli wystąpią usterek za pomocą narzędzia plików [problem](https://github.com/Azure/azure-cli/issues) w **problemów** sekcji repozytorium GitHub.

Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

## <a name="python-installation-issues"></a>Problemy z instalacją Python
### <a name="legacy-installation-issues-macos"></a>Problemy z instalacją starszej wersji (system macOS)
Podczas instalowania narzędzia pip, podczas instalowania starszej pakiety z zostanie zgłoszony błąd uprawnień **su** uprawnienia. Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany. Niektóre narzędzia pip pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień. Rozwiązanie, to usuń te pakiety zainstalowane przez główny. Aby zakończyć to zadanie, wykonaj następujące kroki:

1. Przejdź do: /usr/local/lib/python2.7/site-packages
2. Lista pakietów utworzone przez główny:`ls -l | grep root`
3. Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`
4. Zainstaluj ponownie Python.

## <a name="azure-iot-hub-issues"></a>Problemy z Centrum IoT Azure
Jeśli pomyślnie zostały udostępnione Centrum Azure IoT z wiersza polecenia platformy Azure i należy to narzędzie do zarządzania urządzeniami, łączących się z Centrum IoT, spróbuj następujących narzędzi.

### <a name="device-explorer"></a>Eksplorator urządzenia
[Explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) narzędzie działa na komputerze lokalnym systemu Windows i łączy się z Centrum IoT na platformie Azure. Komunikuje się z następującymi [punkty końcowe Centrum IoT](iot-hub-devguide.md):


* *Zarządzanie tożsamościami urządzenia* obsługiwać i zarządzać nim urządzeń zarejestrowanych w usłudze Centrum IoT.
* *Odbieranie urządzenia do chmury* , można monitorować wiadomości wysyłane z urządzenia do Centrum IoT.
* *Wyślij chmury do urządzenia* tak wiadomości można wysyłać do urządzenia z Centrum IoT.

Konfigurowanie parametrów połączenia Centrum IoT w to narzędzie, aby korzystać z jego możliwości.

### <a name="iothub-explorer"></a>Eksplorator Centrum iothub
[Centrum iothub explorer](https://github.com/Azure/iothub-explorer) to przykładowe narzędzie interfejsu wiersza polecenia dla wielu platform do zarządzania urządzeniami. Można użyć narzędzia do zarządzania urządzeniami w rejestrze tożsamości, monitorować urządzenia do chmury wiadomości i wysyłanie komunikatów chmury do urządzenia.

Aby zainstalować najnowszą wersję (wstępna) narzędzia Centrum iothub explorer, uruchom następujące polecenie w wierszu polecenia środowiska:

```bash
npm install -g iothub-explorer@latest
```

Aby uzyskać dodatkową pomoc dotyczącą poleceń Centrum iothub explorer i ich parametry służy następujące polecenie:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Azure Portal
Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure. Można także użyć [portalu Azure](../azure-portal-overview.md) świadczenia pomocy, zarządzanie i debugowania zasobów platformy Azure.

## <a name="azure-storage-issues"></a>Problemy z usługą Azure Storage
[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, który służy do pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux. Za pomocą tego narzędzia, możesz nawiązać połączenia z tabeli i wyświetlać dane w nim. To narzędzie służy do rozwiązywania problemów związanych z usługą Azure Storage.

