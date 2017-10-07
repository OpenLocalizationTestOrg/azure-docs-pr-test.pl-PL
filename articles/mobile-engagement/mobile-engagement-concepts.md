---
title: "Pojęcia dotyczące usługi Engagement aaaMobile | Dokumentacja firmy Microsoft"
description: "Pojęcia dotyczące usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8d19abd1-0a6c-4772-9fa5-5e99980ac5da
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 5aa7f28c00cd641a36a6e040c6b13d802ea6ae41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-concepts"></a>Pojęcia dotyczące usługi Azure Mobile Engagement
Usługa Mobile Engagement definiuje kilka pojęć wspólnych tooall obsługiwane platformy. W tym artykule krótko opisano te pojęcia.

Ten artykuł stanowi dobry początek, jeśli są nowe tooMobile zaangażowania. Upewnij się, że tooread hello dokumentacji toohello określonych platform używanego, również, ponieważ pozwoli to uściślić pojęcia hello opisane w tym artykule i więcej informacji i przykłady także możliwych ograniczeniach.

## <a name="devices-and-users"></a>Urządzenia i użytkownicy
Usługa Mobile Engagement identyfikuje użytkowników, generując unikatowy identyfikator dla każdego urządzenia. Ten identyfikator jest określany hello identyfikator urządzenia (lub `deviceid`). Jest on generowany w taki sposób, że wszystkie aplikacje uruchomione hello takie same urządzenia udziału hello sam identyfikator urządzenia.

Oznacza to, że usługa Mobile Engagement traktuje jednego urządzenia toobelong tooexactly jednego użytkownika, a w związku z tym użytkownicy i urządzenia stanowią równoważne pojęcia.

## <a name="sessions-and-activities"></a>Sesje i działania
Sesja stanowi jedno użycie aplikacji hello wykonywane przez użytkownika, od użytkownika hello hello w czasie rozpoczęcia korzystania, dopóki hello zatrzymuje użytkownika.

Działanie stanowi jedno użycie danej części podrzędnej aplikacji hello przez jednego użytkownika (jest to zazwyczaj ekran, ale może być toohello cokolwiek odpowiedniej aplikacji).

Użytkownik może wykonywać tylko jedno działanie naraz.

Działanie jest identyfikowane przez nazwę (ograniczoną too64 znaków) i opcjonalnie mogą mieć osadzone dodatkowe dane (w hello limit to 1024 bajty).

Sesje są automatycznie obliczane na podstawie hello sekwencji działań wykonywanych przez użytkowników. Sesja rozpoczyna się, gdy hello użytkownik rozpoczyna swoje pierwsze działanie i zatrzymywana, gdy użytkownik kończy swoje ostatnie działanie. Oznacza to, że sesja nie jest konieczne toobe jawnie rozpoczynana ani zatrzymywana. Zamiast tego ma miejsce jawne rozpoczynanie i zatrzymywanie działań. Jeśli nie zostanie zgłoszone żadne działanie, nie zostanie zgłoszona żadna sesja.

## <a name="events"></a>Zdarzenia
Zdarzenia są używane tooreport akcje błyskawicznych (na przykład naciśniętego przycisku lub artykułu przeczytanego przez użytkowników).

Zdarzenie może być powiązane toohello bieżącej sesji, tooa uruchomienia zadania, lub może być zdarzenie autonomicznych.

Zdarzenie jest identyfikowane przez nazwę (ograniczoną too64 znaków) i opcjonalnie mogą mieć osadzone dodatkowe dane (w hello limit to 1024 bajty).

## <a name="error"></a>Błąd
Błędy są używane tooreport problemów poprawnie wykrytych przez aplikację hello (na przykład nieprawidłowych akcji użytkownika lub niepowodzeń wywołania interfejsu API).

Błąd może być powiązane toohello bieżącej sesji, tooa uruchomienia zadania, lub może być błąd autonomicznego.

Wystąpił błąd jest identyfikowane przez nazwę (ograniczoną too64 znaków) i opcjonalnie mogą mieć osadzone dodatkowe dane (w hello limit to 1024 bajty).

## <a name="job"></a>Zadanie
Zadania są używane tooreport akcji mających czas trwania (takie jak czas trwania wywołań interfejsu API, Wyświetl czas reklam, czas trwania zadania w tle lub czas trwania akcji użytkowników).

Zadanie nie jest powiązane tooa sesji, ponieważ zadania mogą być wykonywane w tle hello, bez interakcji użytkownika.

Zadanie jest identyfikowane przez nazwę (ograniczoną too64 znaków) i opcjonalnie mogą mieć osadzone dodatkowe dane (w hello limit to 1024 bajty).

## <a name="crash"></a>Awaria
Awarie są generowane przez hello zestaw SDK usługi Mobile Engagement tooreport aplikacji, którą awarii, gdy problemy niewykryte przez aplikację hello była awarii.

## <a name="application-information"></a>Informacje o aplikacji
Informacje o aplikacji (lub informacje o aplikacji) jest używane tootag użytkowników, czyli tooassociate niektórzy użytkownicy toohello danych aplikacji (jest to podobne tooweb plików cookie, z wyjątkiem tego, że informacje o aplikacji są przechowywane na powitania po stronie serwera na powitania platformy Azure Mobile Engagement).

Informacje o aplikacji mogą być rejestrowane za pomocą hello interfejsu API zestawu Mobile Engagement SDK lub przy użyciu interfejsu API urządzenia platformy Mobile Engagement hello.

Informacje o aplikacji to urządzenie skojarzone tooa pary klucz/wartość. klucz Hello jest nazwa hello informacje o aplikacji hello (ograniczone too64 ASCII litery [a-zA-Z], cyfry [0-9] i znaki podkreślenia [_]). wartość Hello (ograniczone too1024 znaki) może być ciąg, liczbę całkowitą, Data (RRRR MM-dd) lub wartością logiczną (true lub false).

Dowolną liczbę informacji o aplikacji może być skojarzony tooa urządzenia, w ramach limitu hello zdefiniowanego przez warunki cenowe usługi Mobile Engagement hello. Dla danego klucza usługa Mobile Engagement tylko przechowuje informacje o hello najnowszy zestaw wartości (Brak historii). Ustawianie lub zmienianie wartości hello informacji o aplikacji wymusza toore Mobile Engagement — oceny kryteriów odbiorców narzędzia ustawić dla tej aplikacji informacje (jeśli istnieje), co oznacza, że informacje o aplikacji mogą być używane tootrigger wypychań.

## <a name="extra-data"></a>Dodatkowe dane
Dodatkowe dane (dodatki) to dowolne dane, które mogą być dołączone tooevents, błędów, działań i zadań.

Dodatki mają strukturę podobnie tooJSON obiektów: składają się z drzewa par klucz/wartość. Klucze są ograniczone too64 litery ASCII [a-zA-Z], cyfry [0-9] i znaki podkreślenia [_]) i hello całkowity rozmiar dodatków jest ograniczony too1024 znaków (po zakodowaniu w formacie JSON przez zestaw SDK usługi Mobile Engagement hello).

Witaj całe drzewo par klucz/wartość jest przechowywana jako obiekt JSON. Niemniej jednak tylko hello pierwszy poziom par klucz/wartość jest rozkładany toobe bezpośrednio dostępny toosome zaawansowanych funkcji, takich jak segmenty (na przykład można łatwo zdefiniować segment o nazwie "Fani", który składa się z wszystkich użytkowników mających wysyłane co najmniej 10 razy zdarzenie hello o nazwie "wyświetlono_zawartość" z hello dodatkowym kluczem "typ_zawartości" set toohello wartość "scifi" w hello ostatniego miesiąca). W związku z tym zdecydowanie zalecane jest tylko dodatków toosend wprowadzone z prostej listy par klucz/wartość przy użyciu wartości skalarnych (na przykład ciągów, dat, liczb całkowitych lub wartość logiczna).

## <a name="next-steps"></a>Następne kroki
* [Omówienie uniwersalnego zestawu SDK systemu Windows dla usługi Azure Mobile Engagement](mobile-engagement-windows-store-sdk-overview.md)
* [Omówienie zestawu SDK programu Windows Phone Silverlight SDK dla usługi Azure Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)
* [Zestaw SDK systemu iOS dla usługi Azure Mobile Engagement](mobile-engagement-ios-sdk-overview.md)
* [Zestaw SDK systemu Android dla usługi Azure Mobile Engagement](mobile-engagement-android-sdk-overview.md)

