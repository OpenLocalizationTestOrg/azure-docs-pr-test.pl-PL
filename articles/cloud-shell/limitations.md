---
title: "Ograniczenia powłoki chmury Azure | Dokumentacja firmy Microsoft"
description: "Omówienie ograniczenia powłoki chmury Azure"
services: azure
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 01/17/2018
ms.author: juluk
ms.openlocfilehash: 7e498582d78d2807070c943dfd838dd9efeb4ed2
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/18/2018
---
# <a name="limitations-of-azure-cloud-shell"></a>Ograniczenia powłoki w chmurze Azure

Powłoka chmury Azure ma następujące znane ograniczenia:

## <a name="general-limitations"></a>Ogólne ograniczenia

### <a name="system-state-and-persistence"></a>Stan systemu i trwałości

Komputer udostępniający sesję powłoki chmury jest tymczasowy i zostanie odtworzony po sesja jest nieaktywny przez 20 minut. Chmura powłoki wymaga udziału plików na platformę Azure ma zostać zainstalowany. W związku z tym subskrypcja musi mieć możliwość skonfigurowany dostęp powłoka chmury zasobów magazynu. Inne zagadnienia dotyczące obejmują:

* Z magazynem zainstalowanym, tylko zmiany w `clouddrive` katalogu są zachowywane. W Bash Twoje `$Home` katalogu również jest trwały.
* Udziały plików platformy Azure może być instalowany tylko z poziomu programu [przypisane region](persisting-shell-storage.md#mount-a-new-clouddrive).
  * W Bash, uruchom `env` można znaleźć w Twoim regionie Ustaw jako `ACC_LOCATION`.
* Usługa pliki Azure obsługuje tylko lokalnie nadmiarowego magazynu i kont magazynu geograficznie nadmiarowego.

### <a name="browser-support"></a>Obsługa przeglądarek

Powłoka chmura obsługuje najnowsze wersje Microsoft Edge, programu Microsoft Internet Explorer, Google Chrome, Mozilla Firefox i Apple Safari. Przeglądarka Safari w trybie prywatnym nie jest obsługiwane.

### <a name="copy-and-paste"></a>Kopiowanie i wklejanie

[!include [copy-paste](../../includes/cloud-shell-copy-paste.md)]

### <a name="for-a-given-user-only-one-shell-can-be-active"></a>Dla danego użytkownika mogą być aktywne tylko jedno powłoki

Użytkownicy mogą uruchamiać tylko jeden typ powłoki w czasie, albo **Bash** lub **PowerShell**. Jednak może istnieć wiele wystąpień uruchomione w tym samym czasie Bash lub programu PowerShell. Wymiany między Bash lub środowiska PowerShell powoduje, że chmury powłoki, aby ponownie uruchomić, które mają zakończenie istniejącej sesji.

### <a name="usage-limits"></a>Limity użycia

Powłoka chmury jest przeznaczony dla przypadków użycia interaktywnego. W związku z tym wszystkie długotrwałe nieinterakcyjnym sesje zostaną zakończone bez ostrzeżenia.

## <a name="bash-limitations"></a>Ograniczenia bash

### <a name="user-permissions"></a>Uprawnienia użytkowników

Uprawnienia zostały ustawione jako normalnych użytkowników bez dostępu do operacji sudo. Każda instalacja poza Twojej `$Home` katalogu nie jest trwały.

### <a name="clouddrive-smb-limited-permissions"></a>Clouddrive SMB ograniczone uprawnienia
Niektórych poleceń w `clouddrive` katalogu, takie jak `git clone`, nie ma odpowiednich uprawnień do odczytu/zapisu niektórych plików. Jeśli zostanie osiągnięty ten problem, spróbuj uruchomić go z Twojego `$Home` katalogu, który nie ma ograniczenia SMB.

### <a name="editing-bashrc"></a>Edytowanie .bashrc

Mają ostrożność w przypadku edycji .bashrc w ten sposób może spowodować nieoczekiwane błędy w chmurze powłoki.

### <a name="bashhistory"></a>.bash_history

Historię poleceń bash może być niespójna z powodu przerw w działaniu sesję powłoki chmury lub równoczesnych sesji.

## <a name="powershell-limitations"></a>Ograniczenia programu PowerShell

### <a name="slow-startup-time"></a>Czas uruchamiania powolne

PowerShell w powłoce chmury Azure (wersja zapoznawcza) może potrwać do 60 sekund zainicjować wersji zapoznawczej.

### <a name="no-home-directory-persistence"></a>Trwałość katalogu No $Home

Dane zapisywane w `$Home` przez dowolną aplikację (takich jak: git, vim i inne) nie zachowywane między sesjami programu PowerShell. Obejście tego problemu [widoczną w tym miejscu](troubleshooting.md#powershell-resolutions).

### <a name="default-file-location-when-created-from-azure-drive"></a>Domyślna lokalizacja pliku podczas tworzenia dysku platformy Azure:

Za pomocą poleceń cmdlet programu PowerShell, użytkownicy nie można utworzyć plików w obszarze dysku platformy Azure. Podczas tworzenia nowych plików przy użyciu innych narzędzi, takich jak vim lub nano, pliki są domyślnie zapisywane do folderu C:\Users. 

### <a name="gui-applications-are-not-supported"></a>Graficzny interfejs użytkownika aplikacji nie są obsługiwane.

Jeśli użytkownik uruchamia polecenia, które mogą utworzyć okno dialogowe systemu Windows, takich jak `Connect-AzureAD` lub `Login-AzureRMAccount`, takich jak jedną zobaczy komunikat o błędzie: `Unable to load DLL 'IEFRAME.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)`.

## <a name="next-steps"></a>Kolejne kroki

[Rozwiązywanie problemów z powłoki chmury](troubleshooting.md) <br>
[Przewodnik Szybki start po powłoce Bash](quickstart.md) <br>
[Przewodnik Szybki start po programie PowerShell](quickstart-powershell.md)
