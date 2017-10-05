---
title: "Edison firmy Intel (węzeł) nawiązania połączenia platformy Azure IoT — lekcji 4: Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d54dd4a13ed87152fb6c039f38a5ffe8b4470df9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a>Rozwiązywanie problemów
## <a name="hardware-issues"></a>Problemy ze sprzętem
Aby uzyskać informacje o rozwiązywaniu typowych problemów na Intel Edison, zobacz [oficjalnego stronę rozwiązywania problemów](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Problemy z pakietu node.js
### <a name="no-response-during-gulp-tasks"></a>Brak odpowiedzi podczas gulp zadań
Jeśli wystąpią problemy z działaniem gulp zadań, możesz dodać `--verbose` opcji do debugowania. Spróbuj zakończenie bieżącego zadania gulp przy użyciu `Ctrl + C`, a następnie uruchom następujące polecenie w oknie konsoli, aby wyświetlić komunikaty debugowania. Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>Problemy z NPM
Spróbuj zaktualizować pakiet NPM przy użyciu następującego polecenia:

```bash
npm install -g npm
```

Jeśli problem nadal występuje, zostaw komentarz na końcu tego artykułu lub utworzyć problem GitHub w naszym [repozytorium przykładowej][sample-repository].

## <a name="remote-debugging"></a>Debugowanie zdalne

### <a name="run-the-sample-application-in-debug-mode"></a>Uruchom przykładową aplikację w trybie debugowania

```bash
gulp run --debug
```

Gdy aparat debugowania jest gotowy, powinno być możliwe wyświetlić ```Debugger listening on port 5858``` z danych wyjściowych konsoli.

### <a name="configure-vs-code-to-connect-to-the-remote-device"></a>Skonfiguruj kodzie VS do nawiązania połączenia z urządzeniem zdalnym

Otwórz **debugowania** panelu z lewej strony.

Kliknij zielony **Rozpocznij debugowanie** przycisk (F5). Zostaną otwarte w kodzie VS **launch.json** pliku, który należy zaktualizować.

Aktualizacja **launch.json** pliku o następującej zawartości, Zastąp `[device hostname or IP address]` z nazwą hosta lub adres IP rzeczywistego urządzenia.  

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

### <a name="attach-to-the-remote-application"></a>Dołączanie do zdalnej aplikacji

Kliknij zielony **Rozpocznij debugowanie** (F5) znajdujący się i korzystać z debugowania.

Możesz przeczytać [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) Aby dowiedzieć się więcej na temat debugera.

![Zdalne debugowanie interakcyjne](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Problemy z wiersza polecenia platformy Azure
Interfejs wiersza polecenia platformy Azure (Azure CLI) jest kompilacji w wersji zapoznawczej. Wyszukaj rozwiązanie w [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) poszukiwanie rozwiązania. Spróbuj uaktualnić wiersza polecenia platformy Azure do najnowszej wersji, gdy nie działają polecenia, zgodnie z oczekiwaniami.

Jeśli wystąpią usterek za pomocą narzędzia plików [problem](https://github.com/Azure/azure-cli/issues) w **problemów** sekcji repozytorium GitHub.

Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania", uruchom następujące polecenie, aby uaktualnić narzędzie pip do najnowsza wersja.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemy z instalacją Python
### <a name="legacy-installation-issues-macos"></a>Problemy z instalacją starszej wersji (system macOS)
Podczas instalowania **pip**, błąd uprawnień jest generowany, gdy starszych pakietów, które są instalowane z **su** uprawnienia. Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany. Niektóre **pip** pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień. Rozwiązanie, to usuń te pakiety zainstalowane przez główny. Aby zakończyć to zadanie, wykonaj następujące kroki:

1. Przejdź do: /usr/local/lib/python2.7/site-packages
2. Utwórz listę pakietów przez główny:`ls -l | grep root`
3. Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`
4. Zainstaluj ponownie Python.

## <a name="azure-iot-hub-issues"></a>Problemy z Centrum IoT Azure
Jeśli użytkownik został pomyślnie zainicjowano obsługę administracyjną Centrum Azure IoT z `azure-cli`, i wymagają narzędzia do zarządzania urządzeniami, łączących się z Centrum IoT, spróbuj następujących narzędzi:

### <a name="device-explorer"></a>Eksplorator urządzenia
[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy się z Centrum IoT na platformie Azure. Komunikuje się z następującymi [punkty końcowe Centrum IoT](iot-hub-devguide.md):

- _Zarządzanie tożsamościami urządzenia_ obsługiwać i zarządzać nim urządzeń zarejestrowanych w usłudze Centrum IoT.
- _Odbieranie urządzenia do chmury_ , można monitorować wiadomości wysyłane z urządzenia do Centrum IoT.
- _Wyślij chmury do urządzenia_ tak wiadomości można wysyłać do urządzenia z Centrum IoT.

Konfigurowanie sieci `IoT hub connection string` w to narzędzie, aby korzystać z jego możliwości.

### <a name="iot-hub-explorer"></a>Centrum IoT Explorer
[Centrum IoT Explorer](https://github.com/Azure/iothub-explorer) to przykładowe narzędzie interfejsu wiersza polecenia dla wielu platform do zarządzania klientami urządzeń. Można użyć narzędzia do zarządzania urządzeniami w rejestrze tożsamości, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.

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

## <a name="azure-storage-issues"></a>Problemy z usługą Azure storage
[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, który służy do pracy z [usługi Azure Storage](https://azure.microsoft.com/en-us/services/storage/) dane dotyczące systemu Windows, system macOS i Linux. Za pomocą tego narzędzia, możesz nawiązać połączenia z tabeli i wyświetlać dane w nim. To narzędzie służy do rozwiązywania problemów związanych z usługą Azure Storage.

## <a name="next-steps"></a>Następne kroki
Ta strona zawiera tylko najczęściej występujących problemów Intel Edison zestawu. Aby zgłosić problemy dotyczące rozwiązywania problemów można także pozostawić dolnej komentarze.

Wróć do [wprowadzenie Edison firmy Intel (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started