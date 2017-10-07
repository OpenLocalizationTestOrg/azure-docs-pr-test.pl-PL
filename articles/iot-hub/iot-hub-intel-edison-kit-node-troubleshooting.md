---
title: "Połącz Edison firmy Intel (węzeł) tooAzure IoT - 4 lekcji: Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony dla środowiska Intel Edison Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Rozwiązywanie problemów z arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Rozwiązywanie problemów
## <a name="hardware-issues"></a>Problemy ze sprzętem
Aby uzyskać informacje o rozwiązywaniu typowych problemów na Intel Edison, zobacz hello [oficjalnego stronę rozwiązywania problemów](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Problemy z pakietu node.js
### <a name="no-response-during-gulp-tasks"></a>Brak odpowiedzi podczas gulp zadań
Jeśli wystąpią problemy z działaniem gulp zadania, można dodać hello `--verbose` opcji do debugowania. Spróbuj tooterminate bieżące gulp zadania przy użyciu `Ctrl + C`, a następnie hello uruchom następujące polecenie w wiadomości debugowania toosee okna konsoli. Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>Problemy z NPM
Spróbuj tooupdate pakietu NPM z hello następujące polecenie:

```bash
npm install -g npm
```

Jeśli hello problem nadal występuje, komentarz na końcu tego artykułu hello lub utworzyć problem GitHub w naszym [repozytorium przykładowej][sample-repository].

## <a name="remote-debugging"></a>Debugowanie zdalne

### <a name="run-hello-sample-application-in-debug-mode"></a>Uruchom hello przykładową aplikację w trybie debugowania

```bash
gulp run --debug
```

Gdy aparat debugowania hello jest gotowy, powinno być możliwe toosee ```Debugger listening on port 5858``` z hello dane wyjściowe z konsoli.

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a>Skonfiguruj urządzenie zdalne toohello tooconnect kodzie VS

Otwórz hello **debugowania** panelu powitania po lewej stronie.

Kliknij zielony hello **Rozpocznij debugowanie** przycisk (F5). Zostaną otwarte w kodzie VS **launch.json** pliku, który należy tooupdate.

Aktualizacja hello **launch.json** zawartość pliku z następującego hello, Zastąp `[device hostname or IP address]` z adresu IP rzeczywistego urządzenia hello lub nazwy hosta.  

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

![Konfiguracja zdalnego debugowania](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Dołącz toohello aplikacji zdalnej

Kliknij zielony hello **Rozpocznij debugowanie** (F5) znajdujący się i korzystać z debugowania.

Możesz przeczytać [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn więcej informacji na temat hello debugera.

![Zdalne debugowanie interakcyjne](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problemy z wiersza polecenia platformy Azure
Interfejs wiersza polecenia platformy Azure (Azure CLI) Hello jest kompilacji w wersji zapoznawczej. Wyszukaj rozwiązanie w hello [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek rozwiązań. Spróbuj tooupgrade interfejsu wiersza polecenia Azure toolatest wersji, gdy nie działają polecenia, zgodnie z oczekiwaniami.

Jeśli wystąpią usterek za pomocą narzędzia hello pliku [problem](https://github.com/Azure/azure-cli/issues) w hello **problemów** sekcji hello repozytorium GitHub.

Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania hello", należy hello uruchom następujące polecenie tooupgrade pip toolastest wersji.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemy z instalacją Python
### <a name="legacy-installation-issues-macos"></a>Problemy z instalacją starszej wersji (system macOS)
Podczas instalowania **pip**, błąd uprawnień jest generowany, gdy starszych pakietów, które są instalowane z **su** uprawnienia. Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany. Niektóre **pip** pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień hello. Witaj rozwiązania jest tooremove pakiety zainstalowane w katalogu głównego. To zadanie służy powitania po toocomplete kroki:

1. Przejdź do: /usr/local/lib/python2.7/site-packages
2. Utwórz listę pakietów przez główny:`ls -l | grep root`
3. Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`
4. Zainstaluj ponownie Python.

## <a name="azure-iot-hub-issues"></a>Problemy z Centrum IoT Azure
Jeśli użytkownik został pomyślnie zainicjowano obsługę administracyjną Centrum Azure IoT z `azure-cli`, i wymagają urządzeń hello toomanage narzędzia, łączących tooyour Centrum IoT, spróbuj hello następujące narzędzia:

### <a name="device-explorer"></a>Eksplorator urządzenia
[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy tooyour Centrum IoT na platformie Azure. Komunikuje się ona z następujących hello [punkty końcowe Centrum IoT](iot-hub-devguide.md):

- _Zarządzanie tożsamościami urządzenia_ tooprovision i zarządzanie nimi urządzeń zarejestrowanych w usłudze Centrum IoT.
- _Odbieranie urządzenia do chmury_ , można monitorować wiadomości wysyłane z Centrum IoT tooyour urządzenia.
- _Wyślij chmury do urządzenia_ , możesz wysłać wiadomości tooyour urządzenia z Centrum IoT.

Konfigurowanie sieci `IoT hub connection string` w ramach tego narzędzia toouse jego możliwości.

### <a name="iot-hub-explorer"></a>Centrum IoT Explorer
[Centrum IoT Explorer](https://github.com/Azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia dla wielu platform próbki toomanage urządzeń klientów. Można użyć hello narzędzia toomanage hello urządzeń w rejestrze tożsamości hello, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.

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

## <a name="azure-storage-issues"></a>Problemy z usługą Azure storage
[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, które umożliwiają toowork z [usługi Azure Storage](https://azure.microsoft.com/en-us/services/storage/) dane dotyczące systemu Windows, system macOS i Linux. Za pomocą tego narzędzia, możesz łączyć tooyour tabeli i wyświetlać dane hello w nim. Służy to narzędzie tootroubleshoot problemów związanych z magazynu Azure.

## <a name="next-steps"></a>Następne kroki
Ta strona zawiera tylko hello najbardziej typowe problemy z zestawu Intel Edison. Można także pozostawić komentarze dolnej tooreport problemów dotyczących rozwiązywania problemów.

Wróć za[wprowadzenie Edison firmy Intel (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started