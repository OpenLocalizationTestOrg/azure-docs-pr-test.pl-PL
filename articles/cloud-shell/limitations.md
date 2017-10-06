---
title: "aaaAzure ograniczenia chmury powłoki (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Omówienie ograniczenia powłoki chmury Azure"
services: 
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Ograniczenia powłoki w chmurze Azure
Powłoka chmury Azure ma hello następujące znane ograniczenia:

## <a name="system-state-and-persistence"></a>Stan systemu i trwałości
Witaj maszynę, która udostępnia sesję powłoki chmury jest tymczasowy i zostanie odtworzony po sesja jest nieaktywny przez 20 minut. Chmura powłoki wymaga toobe udziału plików, zainstalowane. W związku z tym subskrypcji musi być tooset stanie się tooaccess zasobów magazynu powłoki chmury. Inne zagadnienia dotyczące obejmują:
* Z magazynem zainstalowanym, tylko zmiany w ramach Twojej `$Home` katalogu lub `clouddrive` katalogu są zachowywane.
* Udziały plików może być instalowany tylko z poziomu programu [przypisane region](persisting-shell-storage.md#mount-a-new-clouddrive).
* Usługa pliki Azure obsługuje tylko lokalnie nadmiarowego magazynu i kont magazynu geograficznie nadmiarowego.

## <a name="user-permissions"></a>Uprawnienia użytkowników
Uprawnienia zostały ustawione jako normalnych użytkowników bez dostępu do operacji sudo. Każda instalacja poza Twojej `$Home` nie zachowa katalogu.
Mimo że hello niektórych poleceń w `clouddrive` katalogu, takie jak `git clone`, nie ma odpowiednich uprawnień, Twoje `$Home` katalogu uprawnień.

## <a name="browser-support"></a>Obsługa przeglądarek
Powłoka chmura obsługuje hello najnowsze wersje Microsoft Edge, programu Microsoft Internet Explorer, Google Chrome, Mozilla Firefox i Apple Safari. Przeglądarka Safari w trybie prywatnym nie jest obsługiwane.

## <a name="copy-and-paste"></a>Kopiowanie i wklejanie
CTRL + C i Ctrl + V nie działają zgodnie z kopiowania/wklejania skróty w powłoce chmury na komputerach z systemem Windows, użyj klawiszy Ctrl + Insert i Shift + Insert toocopy i Wklej odpowiednio.

Kliknij prawym przyciskiem myszy kopiowania i wklejania opcje są także dostępne, ale funkcja Kliknij prawym przyciskiem myszy jest dostęp do Schowka specyficzne dla toobrowser podmiotu.

## <a name="editing-bashrc"></a>Edytowanie .bashrc
Mają ostrożność w przypadku edycji .bashrc w ten sposób może spowodować nieoczekiwane błędy w chmurze powłoki.

## <a name="bashhistory"></a>.bash_history
Historię poleceń bash może być niespójna z powodu przerw w działaniu sesję powłoki chmury lub równoczesnych sesji.

## <a name="usage-limits"></a>Limity użycia
Powłoka chmury jest przeznaczony dla przypadków użycia interaktywnego. W związku z tym wszystkie długotrwałe nieinterakcyjnym sesje zostaną zakończone bez ostrzeżenia.

## <a name="network-connectivity"></a>Połączenie sieciowe
Wszelkie opóźnienia w powłoce chmury jest połączenie z Internetem toolocal podmiotu, powłoki chmury nadal toocarry tooattempt się żadnych instrukcji wysyłane.

## <a name="next-steps"></a>Następne kroki
[Szybki Start powłoki chmury](quickstart.md)
