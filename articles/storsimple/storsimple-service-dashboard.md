---
title: "pulpit nawigacyjny usługi Menedżera aaaStorSimple | Dokumentacja firmy Microsoft"
description: "Zawiera opis pulpit nawigacyjny usługi Menedżer StorSimple hello i jak toouse on toomonitor hello kondycji rozwiązania StorSimple."
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a>Pulpit nawigacyjny usługi Menedżer StorSimple hello
## <a name="overview"></a>Omówienie
Strona pulpitu nawigacyjnego usługi Menedżer StorSimple Hello zawiera widok podsumowania wszystkich urządzeń hello, które są połączone toohello usługi Menedżer StorSimple, wyróżnianie tych, które wymagają uwagi administratora systemu. W tym samouczku wprowadza hello strony pulpitu nawigacyjnego, opisano hello zawartości pulpitu nawigacyjnego i funkcji oraz opisano hello zadania, które można wykonywać na tej stronie.

![Pulpit nawigacyjny usług](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

pulpit nawigacyjny usługi Menedżer StorSimple Hello Wyświetla hello następujących informacji:

* W hello **wykresu** widoczny obszar wykresu hello metryki istotne dla urządzeń. Można wyświetlić magazynu głównego hello (lokalnie przypięty i warstwowa) używany przez wszystkie hello urządzenia, a także magazynu w chmurze hello używane przez urządzenia w danym okresie czasu. Formanty hello w hello prawym górnym rogu toospecify wykresu hello przedział czasu 1 tydzień, 1-miesięcznego, 3-miesięczna lub 1 rok.
* Witaj **przegląd wykorzystania** pokazuje hello głównej pamięci masowej, udostępniane i używane przez wszystkie urządzenia względną toohello całkowita magazynu jest dostępna dla wszystkich urządzeń. **Zainicjowano obsługę administracyjną** odwołuje się toohello ilość pamięci, która jest gotowa i przydzielona do użycia, podczas gdy **używane** odwołuje się toousage woluminów, tak jak to pokazano inicjatorzy hello, które są urządzenia połączone toohello.
* Witaj **alerty** obszaru zawiera migawkę wszystkie aktywne alerty hello na wszystkich urządzeniach hello, pogrupowane według ważności alertu. Kliknięcie poziom ważności hello otwiera hello **alerty** strony, zakresami tooshow alertów. Na powitania **alerty** strony, możesz kliknąć poszczególne tooview alertu dodatkowych szczegółów na temat tego alertu, w tym wszystkie zalecane działania. Można także wyczyścić hello alert, jeśli hello problem został rozwiązany.
* Witaj **zadania** obszaru zawiera migawkę ostatnich zadań dla wszystkich urządzeń, które są połączone tooyour usługi. Istnieją linki, które można użyć toolook na zadania, które są obecnie w toku, które nie powiodło się hello w ostatnich 24 godzinach lub te, które są zaplanowane toorun w hello następne 24 godziny.
* Witaj **szybkiego dostępu** obszaru zawiera przydatne informacje, takie jak stan usługi, liczba urządzeń toohello połączone usługi, lokalizację usługi hello i szczegóły subskrypcji hello, który jest skojarzony z usługą hello. Istnieje również dziennik operacji toohello łącza. Kliknij przycisk hello łącze toosee listę wszystkich ukończone operacje usługi Menedżer StorSimple.

Program hello Menedżer StorSimple usługi Pulpit nawigacyjny strony tooinitiate hello następujące zadania:

* Wyświetl lub ponownie wygenerować klucz rejestracji usługi hello.
* Zmień hello klucza szyfrowania danych usługi.
* Wyświetl dzienniki operacji hello.

## <a name="view-or-regenerate-hello-service-registration-key"></a>Wyświetl lub ponownie wygenerować klucz rejestracji usługi hello
klucz rejestracji usługi Hello jest tooregister używane urządzenia Microsoft Azure StorSimple przy użyciu usługi Menedżer StorSimple hello, aby hello urządzenie pojawi się hello klasycznego portalu Azure, aby uzyskać dalsze akcje zarządzania. klucz Hello jest utworzony na powitania pierwsze urządzenie i udostępniać hello pozostałe urządzenia.

Kliknięcie przycisku **klucz rejestracji** (u dołu hello strony hello) otwiera hello **klucz rejestracji usługi** okno dialogowe, w których możesz wykonywać albo Kopiuj hello bieżącej usługi rejestracji klucza toohello Schowka lub Wygeneruj ponownie klucz rejestracji usługi hello.

Trwa ponowne generowanie klucza hello nie ma wpływu na wcześniej zarejestrowane urządzenia: wpływa na powitania tylko te urządzenia, które są zarejestrowane w usłudze hello po klucz hello zostanie ponownie wygenerowany.

Aby uzyskać więcej informacji na temat przeglądania i za Generowanie hello usługi rejestracji kluczy, przejdź[Pobierz klucz rejestracji usługi hello](storsimple-manage-service.md#get-the-service-registration-key).

## <a name="change-hello-service-data-encryption-key"></a>Klucz szyfrowania danych usługi hello zmiany
Klucze szyfrowania danych usługi są używane tooencrypt klienta poufnych danych, takich jak poświadczeń konta magazynu, które są wysyłane z urządzenia StorSimple toohello usługi Menedżer StorSimple. Konieczne będzie toochange te klucze okresowo Jeśli Twoja organizacja IT zasady rotacją kluczy w urządzeniach magazynujących hello. Witaj proces zmiany klucza może być nieznacznie różnić w zależności od tego, czy istnieje jednego lub wielu urządzeniach zarządzanych przez hello usługi Menedżer StorSimple.

Zmiana klucza szyfrowania danych usługi hello jest procesem krok 3:

1. Przy użyciu hello klasycznego portalu Azure, zezwolić urządzeniu toochange hello klucza szyfrowania danych usługi.
2. Przy użyciu programu Windows PowerShell dla urządzenia StorSimple, inicjują zmiany klucza szyfrowania danych usługi hello.
3. Jeśli masz więcej niż jedno urządzenie StorSimple, należy zaktualizować klucz szyfrowania danych usługi hello na powitania innych urządzeń.

Witaj poniższych krokach opisano proces hello przerzucania klucza szyfrowania danych usługi hello.

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a>Wyświetl dzienniki operacji hello
Witaj dzienniki operacji można wyświetlić, klikając łącze dzienniki operacji hello dostępne w hello **szybkiego dostępu** okienku hello pulpitu nawigacyjnego. Spowoduje to przejście zarządzania toohello stronę usługi, którym można filtrować i zobacz hello rejestruje określonych tooyour usługi Menedżer StorSimple.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak za[Rozwiązywanie problemów z urządzeniem StorSimple](storsimple-troubleshoot-operational-device.md).
* Dowiedz się więcej o tym, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).

