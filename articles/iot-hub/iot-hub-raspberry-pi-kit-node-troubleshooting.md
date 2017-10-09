---
title: "TooAzure Connect Raspberry pi (C) IoT — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony dla środowiska Node.js Pi malina hello"
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
ms.openlocfilehash: 8f0807104550e8e53a132f7741564b33f1db17ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Rozwiązywanie problemów
## <a name="hardware-issues"></a>Problemy ze sprzętem
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>Aplikacja Hello działa prawidłowo, ale hello LED nie jest migający
Ten problem jest zawsze powiązane toohardware obwodu łączności. Użyj następującego kroki problemy tooidentify hello:

1. Sprawdź, czy wybrano poprawną hello **interfejs GPIO** na tablicy. Witaj dwie powinny być **GND interfejs GPIO (numer Pin 6)** i **04 interfejs GPIO (7 kodu Pin)**.
2. Sprawdź, czy bieguna hello z Twojej LED jest poprawna. etap dłużej Hello powinny wskazywać hello **dodatnią**, szczytową numeru pin.
3. Użyj hello **3, 3V przypiąć** i **GND Pin** malina Pi 3. Pi należy traktować jako hello zasilania kontrolera domeny. Sprawdź, czy ten hello LED działa prawidłowo.

![Specyfikacja LED](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Innych problemów ze sprzętem
Uzyskać informacji na temat rozwiązywania typowych problemów 3 Pi malina, zobacz hello [oficjalnego stronę rozwiązywania problemów](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Problemy z pakietu node.js
### <a name="no-response-during-gulp-tasks"></a>Brak odpowiedzi podczas gulp zadań
Jeśli wystąpią problemy w uruchomionych zadań gulp, możesz dodać hello `--verbose` opcji do debugowania. Spróbuj tooterminate bieżące gulp zadania przy użyciu klawiszy Ctrl + C, a następnie uruchom następujące polecenie w konsoli okna toosee debugowania wiadomości powitania. Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemy dotyczące odnajdywania urządzenia
Aby uzyskać pomoc w rozwiązywaniu typowych problemów z hello `devdisco` polecenia, sprawdź hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>problemy z npm
Spróbuj tooupdate pakietu npm, za pomocą następującego polecenia hello:

```bash
npm install -g npm
```

Jeśli hello problem nadal występuje, komentarz na końcu tego artykułu hello lub utworzyć problem GitHub w naszym [repozytorium przykładowej](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-getting-started).

## <a name="remote-debugging"></a>Debugowanie zdalne
### <a name="run-hello-sample-application-in-debug-mode"></a>Uruchom hello przykładową aplikację w trybie debugowania
```bash
gulp run --debug
```

Gdy aparat debugowania hello jest gotowy, powinny pojawić się ```Debugger listening on port 5858``` w danych wyjściowych konsoli hello.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Skonfiguruj urządzenie zdalne programu Visual Studio Code tooconnect toohello
1. Otwórz hello **debugowania** panelu na powitania po lewej stronie.
2. Kliknij zielony hello **Rozpocznij debugowanie** przycisk (F5). Visual Studio Code otwiera plik launch.json.
3. Plik launch.json hello aktualizacji z powitania po zawartości. Zastąp `[device hostname or IP address]` z hello rzeczywistego urządzenia IP adres lub nazwę hosta.

> [!NOTE]
> toolearn więcej informacji na temat hello Visual Studio debugowanie, można znaleźć zbyt[debugowania w programie Visual Studio Code](https://code.visualstudio.com/Docs/editor/debugging#_launchjson-attributes).


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

### <a name="attach-toohello-remote-application"></a>Dołącz toohello aplikacji zdalnej
Kliknij zielony hello **Rozpocznij debugowanie** debugowania toostart przycisk (F5).

Odczyt [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn więcej informacji na temat hello debugera.

![Zdalne debugowanie interakcyjne](media/iot-hub-raspberry-pi-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problemy z interfejsu wiersza polecenia platformy Azure
Interfejs wiersza polecenia platformy Azure (Azure CLI) Hello jest kompilacji w wersji zapoznawczej. tooseek rozwiązania, można użyć hello [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Jeśli wystąpią usterek za pomocą narzędzia hello pliku [problem](https://github.com/Azure/azure-cli/issues) w hello **problemów** sekcji hello repozytorium GitHub.

Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

## <a name="python-installation-issues"></a>Problemy z instalacją Python
### <a name="legacy-installation-issues-macos"></a>Problemy z instalacją starszej wersji (system macOS)
Podczas instalowania narzędzia pip, podczas instalowania starszej pakiety z zostanie zgłoszony błąd uprawnień **su** uprawnienia. Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany. Niektóre narzędzia pip pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień hello. Witaj rozwiązania jest tooremove pakiety zainstalowane w katalogu głównego. To zadanie służy powitania po toocomplete kroki:

1. Przejdź do: /usr/local/lib/python2.7/site-packages
2. Lista pakietów utworzone przez główny:`ls -l | grep root`
3. Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`
4. Zainstaluj ponownie Python.

## <a name="azure-iot-hub-issues"></a>Problemy z Centrum IoT Azure
Jeśli pomyślnie zostały udostępnione Centrum Azure IoT z wiersza polecenia platformy Azure i trzeba urządzeń hello toomanage narzędzia, łączących tooyour Centrum IoT, spróbuj hello następujących narzędzi.

### <a name="device-explorer"></a>Eksplorator urządzenia
Witaj [explorer urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) narzędzie działa na komputerze lokalnym systemu Windows i łączy tooyour Centrum IoT na platformie Azure. Komunikuje się ona z następujących hello [punkty końcowe Centrum IoT](iot-hub-devguide.md):


* *Zarządzanie tożsamościami urządzenia* tooprovision i zarządzanie nimi urządzeń zarejestrowanych w usłudze Centrum IoT.
* *Odbieranie urządzenia do chmury* , można monitorować wiadomości wysyłane z Centrum IoT tooyour urządzenia.
* *Wyślij chmury do urządzenia* , możesz wysłać wiadomości tooyour urządzenia z Centrum IoT.

Konfigurowanie parametrów połączenia Centrum IoT w ramach tego narzędzia toouse jego możliwości.

### <a name="iothub-explorer"></a>Eksplorator Centrum iothub
[Centrum iothub explorer](https://github.com/Azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia dla wielu platform próbki toomanage urządzeń. Można użyć hello narzędzia toomanage hello urządzeń w rejestrze tożsamości hello, monitorować urządzenia do chmury wiadomości i wysyłać chmury do urządzenia.

tooinstall hello najnowszej wersji (wstępna) hello Centrum iothub explorer narzędzia, uruchom następujące polecenie w wierszu polecenia środowiska hello:

```bash
npm install -g iothub-explorer@latest
```

Można użyć następującego polecenia, które tooget dodatkową pomoc na temat wszystkich hello polecenia Eksploratora Centrum iothub i ich parametry hello:

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Azure Portal
Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure. Można także toouse hello [portalu Azure](../azure-portal-overview.md) toohelp obsługę administracyjną, zarządzanie i debugowanie zasobów platformy Azure.

## <a name="azure-storage-issues"></a>Problemy z usługą Azure Storage
[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, w której można toowork z danymi usługi Azure Storage w systemie Windows, macOS i Linux. Za pomocą tego narzędzia, możesz łączyć tooyour tabeli i wyświetlać dane hello w nim. Służy to narzędzie tootroubleshoot problemów związanych z magazynu Azure.

