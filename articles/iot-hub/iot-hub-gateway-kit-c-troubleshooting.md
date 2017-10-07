---
title: "Sensor tag urządzenia & brama IoT Azure — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony Intel NUC bramy"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "problemy z iot, internet rzeczy problemów"
ROBOTS: NOINDEX
ms.assetid: 5f742c38-0e33-465a-9a0d-1e41e8d17187
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed6812c60412afb615012e3d694051d009b149a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Rozwiązywanie problemów

## <a name="hardware-issues"></a>Problemy ze sprzętem

### <a name="ti-sensortag-cannot-be-connected"></a>Nie można połączyć analizy czasowej Sensor tag

problemy z łącznością Sensor tag tootroubleshoot, użyj hello [aplikacji Sensor tag](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).

### <a name="have-an-issue-with-intel-nuc"></a>Występuje problem z Intel NUC

tootroubleshoot rozruchu problemów, zapoznaj się zbyt[problemów rozruchu nie na Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).

problemy z systemem operacyjnym tootroubleshoot, można znaleźć zbyt[problemów systemu operacyjnego na Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).

tootroubleshoot inne problemy, zapoznaj się zbyt[Blink i sygnalizuje kodów dla Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).

## <a name="nodejs-package-issues"></a>Problemy z pakietu node.js

### <a name="no-response-during-gulp-tasks"></a>Brak odpowiedzi podczas gulp zadań

Jeśli wystąpią problemy w uruchomionych zadań gulp, możesz dodać hello `--verbose` opcji do debugowania. Spróbuj tooterminate bieżące gulp zadania przy użyciu `Ctrl + C`, a następnie hello uruchom następujące polecenie w wiadomości debugowania toosee okna konsoli. Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Problemy dotyczące odnajdywania urządzenia

Aby uzyskać pomoc w rozwiązywaniu typowych problemów z hello `discover-sensortag` polecenia, sprawdź hello [strona typu wiki](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).

### <a name="npm-issues"></a>problemy z npm

Spróbuj tooupdate pakietu npm, uruchamiając następujące polecenie hello:

```bash
npm install -g npm
```

Jeśli hello problem nadal występuje, komentarz na końcu tego artykułu hello lub utworzyć problem GitHub w naszym [repozytorium przykładowej](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).

## <a name="remote-debugging"></a>Debugowanie zdalne
> Poniżej instrukcje są przeznaczone do debugowania skryptów node.js używanych w tym samouczku.
### <a name="run-hello-sample-application-in-debug-mode"></a>Uruchom hello przykładową aplikację w trybie debugowania

Uruchom hello przykładową aplikację w trybie debugowania, uruchamiając następujące polecenie hello:

```bash
gulp run --debug
```

Gdy aparat debugowania hello jest gotowy, powinny pojawić się `Debugger listening on port 5858` w danych wyjściowych konsoli hello.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Skonfiguruj urządzenie zdalne programu Visual Studio Code tooconnect toohello

1. Otwórz hello **debugowania** panelu na powitania po lewej stronie.
2. Kliknij zielony hello **Rozpocznij debugowanie** przycisk (F5). Zostanie otwarty w programie Visual Studio Code `launch.json` pliku.
3. Aktualizacja hello `launch.json` pliku z powitania po zawartości. Zastąp `[device hostname or IP address]` z hello rzeczywistego urządzenia IP adres lub nazwę hosta.

   ``` json
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
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Konfiguracja zdalnego debugowania](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Dołącz toohello aplikacji zdalnej

Kliknij zielony hello **Rozpocznij debugowanie** debugowania toostart przycisk (F5).

Odczyt [JavaScript w kodzie VS](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn więcej informacji na temat hello debugera.

![Debugowanie cz próbki](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a>Problemy z interfejsu wiersza polecenia platformy Azure

Interfejs wiersza polecenia platformy Azure (Azure CLI) Hello jest kompilacji w wersji zapoznawczej. tooseek rozwiązania, można użyć hello [Przewodnik instalowania wersji zapoznawczej](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

Jeśli wystąpią usterek za pomocą narzędzia hello pliku [problem](https://github.com/Azure/azure-cli/issues) w hello **problemów** sekcji hello repozytorium GitHub.

Aby uzyskać pomoc w rozwiązywaniu typowych problemów, sprawdź hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

Jeśli spełniasz "Nie można odnaleźć wersji, który spełnia wymagania hello", należy hello uruchom następujące polecenie tooupgrade pip toolastest wersji.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Problemy z instalacją Python

### <a name="legacy-installation-issues-macos"></a>Problemy z instalacją starszej wersji (system macOS)

Podczas instalowania narzędzia pip, podczas instalowania starszej pakiety z zostanie zgłoszony błąd uprawnień **su** uprawnienia. Ta sytuacja występuje, ponieważ poprzednich instalacji języka Python za pomocą brew (macOS) nie został całkowicie odinstalowany. Niektóre narzędzia pip pakiety z poprzedniej instalacji zostały utworzone przez główny, co powoduje, że błąd uprawnień hello. Witaj rozwiązania jest tooremove pakiety zainstalowane w katalogu głównego. To zadanie służy powitania po toocomplete kroki:

1. Przejdź za`/usr/local/lib/python2.7/site-packages`
2. Lista pakietów utworzone przez główny:`ls -l | grep root`
3. Odinstaluj pakiety z kroku 2:`sudo rm -rf {package name}`
4. Zainstaluj ponownie Python.

## <a name="azure-iot-hub-issues"></a>Problemy z Centrum IoT Azure

Jeśli pomyślnie zostały udostępnione Centrum Azure IoT z hello wiersza polecenia platformy Azure i trzeba urządzeń hello toomanage narzędzia, łączących tooyour Centrum IoT, spróbuj hello następujących narzędzi.

### <a name="device-explorer"></a>Eksplorator urządzenia

[Eksplorator urządzenia](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) działa na komputerze lokalnym systemu Windows i łączy tooyour Centrum IoT na platformie Azure. Komunikuje się ona z następujących hello [punkty końcowe Centrum IoT](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):

- Tooprovision zarządzania tożsamości urządzenia i zarządzanie nimi urządzeń zarejestrowanych w usłudze Centrum IoT.
- Otrzymywać urządzenia do chmury, więc można monitorować wiadomości wysyłane z Centrum IoT tooyour urządzenia.
- Wyślij chmury do urządzenia, więc można wysłać wiadomości tooyour urządzenia z Centrum IoT.

Konfigurowanie parametrów połączenia Centrum IoT w ramach tego narzędzia toouse jego możliwości.

### <a name="iothub-explorer"></a>Eksplorator Centrum iothub

[Centrum iothub explorer](https://github.com/Azure/iothub-explorer) to narzędzie interfejsu wiersza polecenia dla wielu platform próbki toomanage urządzeń klientów. Można użyć hello narzędzia toomanage hello urządzeń w rejestrze tożsamości hello, monitorować urządzenia do chmury wiadomości i wysyłanie poleceń z chmury do urządzenia.

tooinstall hello najnowszej () wersji wstępnej narzędzia Centrum iothub explorer hello, uruchom następujące polecenie hello:

```bash
npm install -g iothub-explorer@latest
```

tooget dodatkową pomoc na temat wszystkich hello Centrum iothub explorer poleceń i ich parametrów, uruchom następujące polecenie hello:

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a>Witaj portalu Azure

Pełne środowisko CLI ułatwia tworzenie i zarządzanie nimi wszystkich zasobów na platformie Azure. Można także toouse hello [portalu Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp obsługę administracyjną, zarządzanie i debugowanie zasobów platformy Azure.

## <a name="azure-storage-issues"></a>Problemy z usługą Azure Storage

[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com/) jest aplikacją autonomiczną firmy Microsoft, w której można toowork z danymi usługi Azure Storage w systemie Windows, macOS i Linux. Za pomocą tego narzędzia, możesz łączyć tooyour tabeli i wyświetlać dane hello w nim. Służy to narzędzie tootroubleshoot problemów związanych z magazynu Azure.
