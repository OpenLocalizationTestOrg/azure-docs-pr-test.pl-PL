---
title: "Połącz Arduino (C) do platformy Azure IoT — Rozwiązywanie problemów z | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z strony Adafruit piór M0 sieci Wi-Fi Arduino środowisko"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Rozwiązywanie problemów z arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 3bb369da9148300a80e7d351522a4d908e926996
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting"></a>Rozwiązywanie problemów
## <a name="hardware-issues"></a>Problemy ze sprzętem
Aby uzyskać informacje o rozwiązywaniu typowych problemów na tablicy Adafruit piór M0 sieci Wi-Fi Arduino, zobacz [oficjalnego stronę rozwiązywania problemów](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).

## <a name="nodejs-package-issues"></a>Problemy z pakietu node.js
### <a name="no-response-during-gulp-tasks"></a>Brak odpowiedzi podczas gulp zadań
Jeśli wystąpią problemy z działaniem gulp zadań, możesz dodać `--verbose` opcji do debugowania. Spróbuj zakończenie bieżącego zadania gulp przy użyciu `Ctrl + C`, a następnie uruchom następujące polecenie w oknie konsoli, aby wyświetlić komunikaty debugowania. Szczegółowe komunikaty o błędach mogą zobaczyć w danych wyjściowych konsoli.

```bash
gulp --verbose
```

Lub możesz dodać `--listen` do otwarcia portu szeregowego do informacji dziennika urządzenia wyjściowego.

```bash
gulp --listen
``` 

### <a name="npm-issues"></a>Problemy z NPM
Spróbuj zaktualizować pakiet NPM przy użyciu następującego polecenia:

```bash
npm install -g npm
```

Jeśli problem nadal występuje, zostaw komentarz na końcu tego artykułu lub utworzyć problem GitHub w naszym [repozytorium przykładowej][sample-repository].

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

* *Zarządzanie tożsamościami urządzenia* obsługiwać i zarządzać nim urządzeń zarejestrowanych w usłudze Centrum IoT.
* *Odbieranie urządzenia do chmury* , można monitorować wiadomości wysyłane z urządzenia do Centrum IoT.
* *Wyślij chmury do urządzenia* tak wiadomości można wysyłać do urządzenia z Centrum IoT.

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
[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](http://storageexplorer.com) jest aplikacją autonomiczną firmy Microsoft, który służy do pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux. Za pomocą tego narzędzia, możesz nawiązać połączenia z tabeli i wyświetlać dane w nim. To narzędzie służy do rozwiązywania problemów związanych z usługą Azure Storage.

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md