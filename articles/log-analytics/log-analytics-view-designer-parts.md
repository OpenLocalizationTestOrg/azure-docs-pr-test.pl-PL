---
title: "Odwołanie aaaPart Widok projektanta w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "Widok projektanta w analizy dzienników umożliwia toocreate niestandardowe widoki konsoli OMS hello zawierających różne wizualizacje danych w repozytorium OMS hello. Ten artykuł zawiera odwołanie hello ustawienia dla każdego z dostępnych toouse części wizualizacji hello w niestandardowych widoków."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 5718d620-b96e-4d33-8616-e127ee9379c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 6a19a451cf4cefd2fa5c94e6f61d812c4f820f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-visualization-part-reference"></a>Odwołanie do części wizualizacji Projektant widoków analizy dziennika
Witaj Widok projektanta w analizy dzienników umożliwia toocreate niestandardowe widoki w konsoli OMS hello zawierających różne wizualizacje danych z repozytorium OMS hello. Ten artykuł zawiera odwołanie hello ustawienia dla każdego z dostępnych toouse części wizualizacji hello w niestandardowych widoków.

Inne artykuły, które są dostępne dla projektanta widoku są następujące:

* [Wyświetl projektanta](log-analytics-view-designer.md) — omówienie hello Projektant widoków i procedur tworzenia i edytowania widoków niestandardowych.
* [Kafelek odwołanie](log-analytics-view-designer-tiles.md) — odwołanie hello ustawienia dla każdego z hello Kafelki toouse dostępne w niestandardowych widoków.

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie zapytania we wszystkich widokach musi być napisana w hello [nowy język kwerendy](https://go.microsoft.com/fwlink/?linkid=856078).  Wszystkie widoki, które zostały utworzone przed uaktualniono hello obszaru roboczego będzie automtically przekonwertować.

Witaj poniższej tabeli opisano hello różnych typów kafelków, które są dostępne w hello Widok projektanta.  Poniższe rozdziały zawierają Hello opis każdego typu kafelka w szczegółów i ich właściwości.

| Typ widoku | Opis |
|:--- |:--- |
| [Listy zapytań](#list-of-queries-part) |Wyświetla listę dziennika zapytania wyszukiwania.  Witaj użytkownik może kliknąć na każdym toodisplay zapytania wyniki. |
| [Liczba & listy](#number-amp-list-part) |Nagłówek ma jeden przedstawiający liczbę rekordów z zapytania wyszukiwania dziennika.  Lista przedstawia hello top dziesięć wyniki zapytania z Wykres wskazujący hello względne wartości liczbowej lub zmian w czasie. |
| [Dwie liczb & listy](#two-numbers-amp-list-part) |Nagłówek ma dwie liczby przedstawiający liczba rekordów dziennika oddzielne zapytania wyszukiwania.  Lista przedstawia hello top dziesięć wyniki zapytania z Wykres wskazujący hello względne wartości liczbowej lub zmian w czasie. |
| [Pierścień & listy](#donut-amp-list-part) |Nagłówek Wyświetla jeden numer podsumowanie z kolumną wartości w zapytaniu dziennika.  pierścień Hello graficznie wyświetla wyniki hello top trzy rekordów. |
| [Dwóch osiach czasu & listy](#two-timelines-amp-list-part) |Podsumowanie nagłówka wyświetla hello wyniki zapytań dwóch dziennika w czasie, gdy wykresy kolumnowe z objaśnienia wyświetlanie jeden numer z kolumną wartości w zapytaniu dziennika.  Lista przedstawia hello top dziesięć wyniki zapytania z Wykres wskazujący hello względne wartości liczbowej lub zmian w czasie. |
| [Informacje](#information-part) |Nagłówek Wyświetla tekst statyczny oraz opcjonalnie łącza.  Lista zawiera jeden lub więcej elementów z tekst statyczny oraz tytułu. |
| [Wykres liniowy, objaśnienia & listy](#line-chart-callout-amp-list-part) |Nagłówek Wyświetla wykres liniowy z wielu serii w wyniku zapytania dziennika przez czas i objaśnienie z podsumowaniem wartości.  Lista przedstawia hello top dziesięć wyniki zapytania z Wykres wskazujący hello względne wartości liczbowej lub zmian w czasie. |
| [Wykres liniowy i listę](#line-chart-amp-list-part) |Nagłówek przedstawia wykres liniowy z wielu serii w wyniku zapytania dziennika wraz z upływem czasu.  Lista przedstawia hello top dziesięć wyniki zapytania z Wykres wskazujący hello względne wartości liczbowej lub zmian w czasie. |
| [Stos część wykresów wiersza](#stack-of-line-charts-part) |Wyświetla trzech oddzielnych wierszach wykresów z wielu serii w wyniku zapytania dziennika wraz z upływem czasu. |

## <a name="list-of-queries-part"></a>Listę części zapytania
Wyświetla listę dziennika zapytania wyszukiwania.  Witaj użytkownik może kliknąć na każdym toodisplay zapytania wyniki.  Widok Hello domyślnie zawierają pojedynczego zapytania i kliknięcie **+ zapytania** tooadd dodatkowych zapytań.

![Lista Widok kwerendy](media/log-analytics-view-designer/view-list-queries.png)

| Ustawienie | Opis |
|:--- |:--- |
| **Ogólne** | |
| Tytuł |Tekst toodisplay u góry hello hello widoku. |
| Nowa grupa |Wybierz toocreate nową grupę w widoku hello, zaczynając od hello bieżący widok. |
| Wstępnie wybrane filtry |Rozdzielana przecinkami lista właściwości tooinclude w okienku po lewej stronie filtru hello po wybraniu użytkownika hello zapytania. |
| Tryb renderowania |Wyświetlane, gdy zostanie wybrane zapytanie hello widok początkowy.  Witaj użytkownik może wybrać wszystkie widoki dostępne po otwarciu hello zapytania. |
| **Zapytania** | |
| Zapytania wyszukiwania |Toorun zapytania. |
| Przyjazna nazwa |Opisowa nazwa hello zapytania toodisplay toohello użytkownika. |

## <a name="number--list-part"></a>Listy i numer części
Nagłówek ma jeden przedstawiający liczbę rekordów z zapytania wyszukiwania dziennika.  Lista przedstawia hello top dziesięć wyniki zapytania z Wykres wskazujący hello względne wartości liczbowej lub zmian w czasie.

![Lista Widok kwerendy](media/log-analytics-view-designer/view-number-list.png)

| Ustawienie | Opis |
|:--- |:--- |
| **Ogólne** | |
| Tytuł grupy |Tekst toodisplay u góry hello hello widoku. |
| Nowa grupa |Wybierz toocreate nową grupę w widoku hello, zaczynając od hello bieżący widok. |
| Ikona |Obraz pliku toodisplay dalej toohello wynik w nagłówku hello. |
| Użyj ikony |Wybierz toohave hello ikonę wyświetlania. |
| **Tytuł** | |
| Legenda |Tekst toodisplay u góry hello hello nagłówka. |
| Zapytanie |Zapytanie toorun hello nagłówka.  Liczba Hello hello liczbę rekordów zwróconych przez zapytanie hello będą wyświetlane. |
| **Lista** | |
| Zapytanie |Zapytanie toorun hello listy.  Witaj pierwszych dwóch właściwości dla hello pierwszych dziesięciu rekordów w wynikach hello będą wyświetlane.  Hello pierwszy właściwość powinna być tekst wartość i hello drugi wartość liczbową.  Paski są tworzone automatycznie na podstawie względnej wartości kolumny liczbowej hello hello.<br><br>Polecenie hello sortowania w hello zapytania toosort hello rekordy hello liście.  Witaj, użytkownik może kliknąć Zobacz wszystkie hello toorun zapytań i zwrócić wszystkie rekordy. |
| Ukryj wykresu |Wybierz toodisable hello wykres toohello prawej hello kolumny liczbowej. |
| Włącz wykresy przebiegu w czasie |Wybierz wykres przebiegu w czasie toodisplay zamiast poziomy pasek.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Kolor |Kolor słupków hello lub wykresy przebiegu w czasie. |
| Nazwa i wartość separatora |Ogranicznik pojedynczy znak, jeśli właściwość text hello tooparse do wielu wartości.  Zobacz [typowe ustawienia](#name-value-separator) szczegółowe informacje. |
| Zapytanie nawigacji |Zapytanie toorun po wybraniu przez użytkownika hello element na liście hello.  Zobacz [typowe ustawienia](#navigation-query) szczegółowe informacje. |
| **Lista** |**> Tytuły kolumn** |
| Nazwa |Tekst toodisplay u góry hello hello pierwszą kolumnę hello listy. |
| Wartość |Tekst toodisplay u góry hello hello drugiej kolumny hello listy. |
| **Lista** |**> Progi** |
| Włącz progi |Wybierz tooenable progów.  Zobacz [typowe ustawienia](#thresholds) szczegółowe informacje. |

## <a name="two-numbers--list-part"></a>Dwie liczby i listy
Nagłówek ma dwie liczby przedstawiający liczba rekordów dziennika oddzielne zapytania wyszukiwania.  Lista przedstawia hello top dziesięć wyniki zapytania z Wykres wskazujący hello względne wartości liczbowej lub zmian w czasie.

![Dwie liczby i widok listy](media/log-analytics-view-designer/view-two-numbers-list.png)

| Ustawienie | Opis |
|:--- |:--- |
| **Ogólne** | |
| Tytuł grupy |Tekst toodisplay u góry hello hello widoku. |
| Nowa grupa |Wybierz toocreate nową grupę w widoku hello, zaczynając od hello bieżący widok. |
| Ikona |Obraz pliku toodisplay dalej toohello wynik w nagłówku hello. |
| Użyj ikony |Wybierz toohave hello ikonę wyświetlania. |
| **Tytuł** | |
| Legenda |Tekst toodisplay u góry hello hello nagłówka. |
| Zapytanie |Zapytanie toorun hello nagłówka.  Liczba Hello hello liczbę rekordów zwróconych przez zapytanie hello będą wyświetlane. |
| **Lista** | |
| Zapytanie |Zapytanie toorun hello listy.  Witaj pierwszych dwóch właściwości dla hello pierwszych dziesięciu rekordów w wynikach hello będą wyświetlane.  Hello pierwszy właściwość powinna być tekst wartość i hello drugi wartość liczbową.  Paski są tworzone automatycznie na podstawie względnej wartości kolumny liczbowej hello hello.<br><br>Polecenie hello sortowania w hello zapytania toosort hello rekordy hello liście.  Witaj, użytkownik może kliknąć Zobacz wszystkie hello toorun zapytań i zwrócić wszystkie rekordy. |
| Ukryj wykresu |Wybierz toodisable hello wykres toohello prawej hello kolumny liczbowej. |
| Włącz wykresy przebiegu w czasie |Wybierz wykres przebiegu w czasie toodisplay zamiast poziomy pasek.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Kolor |Kolor słupków hello lub wykresy przebiegu w czasie. |
| Operacja |Operacja tooperform dla hello przebiegu w czasie.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Nazwa i wartość separatora |Ogranicznik pojedynczy znak, jeśli właściwość text hello tooparse do wielu wartości.  Zobacz [typowe ustawienia](#name-value-separator) szczegółowe informacje. |
| Zapytanie nawigacji |Zapytanie toorun po wybraniu przez użytkownika hello element na liście hello.  Zobacz [typowe ustawienia](#navigation-query) szczegółowe informacje. |
| **Lista** |**> Tytuły kolumn** |
| Nazwa |Tekst toodisplay u góry hello hello pierwszą kolumnę hello listy. |
| Wartość |Tekst toodisplay u góry hello hello drugiej kolumny hello listy. |
| **Lista** |**> Progi** |
| Włącz progi |Wybierz tooenable progów.  Zobacz [typowe ustawienia](#thresholds) szczegółowe informacje. |

## <a name="donut--list-part"></a>Część pierścień & listy
Nagłówek Wyświetla jeden numer podsumowanie z kolumną wartości w zapytaniu dziennika.  pierścień Hello graficznie wyświetla wyniki hello top trzy rekordów.

![Widok listy i pierścień](media/log-analytics-view-designer/view-donut-list.png)

| Ustawienie | Opis |
|:--- |:--- |
| **Ogólne** | |
| Tytuł grupy |Toodisplay tekst u góry hello hello kafelka. |
| Nowa grupa |Wybierz toocreate nową grupę w widoku hello, zaczynając od hello bieżący widok. |
| Ikona |Obraz pliku toodisplay dalej toohello wynik w nagłówku hello. |
| Użyj ikony |Wybierz toohave hello ikonę wyświetlania. |
| **Nagłówek** | |
| Tytuł |Tekst toodisplay u góry hello hello nagłówka. |
| Podtytuł |Toodisplay tekstu w obszarze hello tytuł u góry hello hello nagłówka. |
| **Pierścień** | |
| Zapytanie |Toorun zapytania dla hello pierścień.  Hello pierwszy właściwość powinna być tekst wartość i hello drugi wartość liczbową. |
| **Pierścień** |**> Centrum** |
| Tekst |Toodisplay tekst w kolumnie wartość hello wewnątrz hello pierścień. |
| Operacja |Witaj tooperform operacji na powitania wartość właściwości toosummarize tooa pojedynczą wartość.<br><br>-Sumy: Określanie hello wszystkich rekordów.<br>— Procent: Procent hello rekordów zwróconych przez wartości hello **powoduje wartości używana podczas operacji centrum** toohello całkowita liczba rekordów w zapytaniu hello. |
| Wynik wartości używana podczas operacji Centrum |Opcjonalnie kliknij hello tooadd znak plus, co najmniej jedna wartość.  Hello wyniki zapytania hello będzie ograniczona toorecords z wartościami właściwości hello, które określisz.  Jeśli wartości nie zostaną dodane, wszystkie rekordy zostaną uwzględnione w hello zapytania. |
| **Dodatkowe opcje** |**> Kolory** |
| Kolor 1<br>Kolor 2<br>Kolor 3 |Wybierz kolor hello hello hello wartości wyświetlane w hello pierścień. |
| **Dodatkowe opcje** |**> Mapowanie kolorów zaawansowane** |
| Wartość pola |Nazwa typu hello toodisplay pola go jako inny kolor, jeśli znajduje się on w hello pierścień. |
| Kolor |Wybierz kolor hello hello unikatowe pole. |
| **Lista** | |
| Zapytanie |Zapytanie toorun hello listy.  Liczba Hello hello liczbę rekordów zwróconych przez zapytanie hello będą wyświetlane. |
| Ukryj wykresu |Wybierz toodisable hello wykres toohello prawej hello kolumny liczbowej. |
| Włącz wykresy przebiegu w czasie |Wybierz wykres przebiegu w czasie toodisplay zamiast poziomy pasek.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Kolor |Kolor słupków hello lub wykresy przebiegu w czasie. |
| Operacja |Operacja tooperform dla hello przebiegu w czasie.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Nazwa i wartość separatora |Ogranicznik pojedynczy znak, jeśli właściwość text hello tooparse do wielu wartości.  Zobacz [typowe ustawienia](#name-value-separator) szczegółowe informacje. |
| Zapytanie nawigacji |Zapytanie toorun po wybraniu przez użytkownika hello element na liście hello.  Zobacz [typowe ustawienia](#navigation-query) szczegółowe informacje. |
| **Lista** |**> Tytuły kolumn** |
| Nazwa |Tekst toodisplay u góry hello hello pierwszą kolumnę hello listy. |
| Wartość |Tekst toodisplay u góry hello hello drugiej kolumny hello listy. |
| **Lista** |**> Progi** |
| Włącz progi |Wybierz tooenable progów.  Zobacz [typowe ustawienia](#thresholds) szczegółowe informacje. |

## <a name="two-timelines--list-part"></a>Dwie części listy i osi czasu
Podsumowanie nagłówka wyświetla hello wyniki zapytań dwóch dziennika w czasie, gdy wykresy kolumnowe z objaśnienia wyświetlanie jeden numer z kolumną wartości w zapytaniu dziennika.  Lista przedstawia hello top dziesięć wyniki zapytania z Wykres wskazujący hello względne wartości liczbowej lub zmian w czasie.

![Wyświetlanie dwóch osiach czasu & listy](media/log-analytics-view-designer/view-two-timelines-list.png)

| Ustawienie | Opis |
|:--- |:--- |
| **Ogólne** | |
| Tytuł grupy |Toodisplay tekst u góry hello hello kafelka. |
| Nowa grupa |Wybierz toocreate nową grupę w widoku hello, zaczynając od hello bieżący widok. |
| Ikona |Obraz pliku toodisplay dalej toohello wynik w nagłówku hello. |
| Użyj ikony |Wybierz toohave hello ikonę wyświetlania. |
| **Najpierw wykresu<br>drugie wykresu** | |
| Legenda |Toodisplay tekstu w obszarze objaśnienia hello hello pierwszy serii. |
| Kolor |Kolor toouse kolumn hello hello serii. |
| Zapytanie |Zapytanie toorun hello pierwszy serii.  Liczba Hello hello liczba rekordów przez każdego interwału czasu będą reprezentowane przez hello wykresu kolumn. |
| Operacja |Witaj tooperform operacji na powitania wartość właściwości toosummarize tooa pojedynczą wartość dla hello objaśnienia.<br><br>— Suma: Suma hello wartość ze wszystkich rekordów.<br>— Średnia: Średnia hello wartości ze wszystkich rekordów.<br>-Ostatniej próbki: Wartość od ostatniego interwału hello objęte hello wykresu.<br>— Próbki pierwszy: Wartość z pierwszy interwał hello objęte hello wykresu.<br>-Liczba: Liczba wszystkich rekordów zwróconych przez zapytanie hello. |
| **Lista** | |
| Zapytanie |Zapytanie toorun hello listy.  Liczba Hello hello liczbę rekordów zwróconych przez zapytanie hello będą wyświetlane. |
| Ukryj wykresu |Wybierz toodisable hello wykres toohello prawej hello kolumny liczbowej. |
| Włącz wykresy przebiegu w czasie |Wybierz wykres przebiegu w czasie toodisplay zamiast poziomy pasek.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Kolor |Kolor słupków hello lub wykresy przebiegu w czasie. |
| Operacja |Operacja tooperform dla hello przebiegu w czasie.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Zapytanie nawigacji |Zapytanie toorun po wybraniu przez użytkownika hello element na liście hello.  Zobacz [typowe ustawienia](#navigation-query) szczegółowe informacje. |
| **Lista** |**> Tytuły kolumn** |
| Nazwa |Tekst toodisplay u góry hello hello pierwszą kolumnę hello listy. |
| Wartość |Tekst toodisplay u góry hello hello drugiej kolumny hello listy. |
| **Lista** |**> Progi** |
| Włącz progi |Wybierz tooenable progów.  Zobacz [typowe ustawienia](#thresholds) szczegółowe informacje. |

## <a name="information-part"></a>Część informacji
Nagłówek Wyświetla tekst statyczny oraz opcjonalnie łącza.  Lista zawiera jeden lub więcej elementów z tekst statyczny oraz tytułu.

![Wyświetlanie informacji](media/log-analytics-view-designer/view-information.png)

| Ustawienie | Opis |
|:--- |:--- |
| **Ogólne** | |
| Tytuł grupy |Toodisplay tekst u góry hello hello kafelka. |
| Nowa grupa |Wybierz toocreate nową grupę w widoku hello, zaczynając od hello bieżący widok. |
| Kolor |Kolor tła nagłówka hello. |
| **Nagłówek** | |
| Image (Obraz) |Obraz pliku toodisplay w nagłówku hello. |
| Etykieta |Toodisplay tekst w nagłówku hello. |
| **Nagłówek** |**> Link** |
| Etykieta |Tekst łącza. |
| Url |Adres URL dla łącza. |
| **Elementy informacji** | |
| Tytuł |Toodisplay tekstu tytułu poszczególnych elementów. |
| Zawartość |Tekst toodisplay dla każdego elementu. |

## <a name="line-chart-callout--list-part"></a>Wykres liniowy, objaśnienia & part listy
Nagłówek Wyświetla wykres liniowy z wielu serii w wyniku zapytania dziennika przez czas i objaśnienie z podsumowaniem wartości.  Lista przedstawia hello top dziesięć wyniki zapytania z Wykres wskazujący hello względne wartości liczbowej lub zmian w czasie.

![Wykres liniowy, objaśnienia i widok listy](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Ustawienie | Opis |
|:--- |:--- |
| **Ogólne** | |
| Tytuł grupy |Toodisplay tekst u góry hello hello kafelka. |
| Nowa grupa |Wybierz toocreate nową grupę w widoku hello, zaczynając od hello bieżący widok. |
| Ikona |Obraz pliku toodisplay dalej toohello wynik w nagłówku hello. |
| Użyj ikony |Wybierz toohave hello ikonę wyświetlania. |
| **Nagłówek** | |
| Tytuł |Tekst toodisplay u góry hello hello nagłówka. |
| Podtytuł |Toodisplay tekstu w obszarze hello tytuł u góry hello hello nagłówka. |
| **Wykres liniowy** | |
| Zapytanie |Zapytanie toorun hello linii wykresu.  Hello pierwszy właściwość powinna być tekst wartość i hello drugi wartość liczbową.  Jest to zazwyczaj kwerendę, która używa hello **miary** wyniki toosummarize słów kluczowych.  Jeśli zapytanie hello używa hello **interwał** — słowo kluczowe, a następnie hello osi x wykresu hello użyje tego przedziału czasu.  Jeśli zapytanie hello nie obejmuje hello **interwał** — słowo kluczowe, a następnie co godzinę interwały są używane do hello osi x. |
| **Wykres liniowy** |**> Objaśnienie** |
| Tytuł objaśnienia |Tekst toodisplay powyżej hello objaśnienia wartości. |
| Nazwa serii |Wartość właściwości toouse serii hello hello objaśnienia wartości.  W przypadku serii wszystkie rekordy z kwerendy hello są używane. |
| Operacja |Witaj tooperform operacji na powitania wartość właściwości toosummarize tooa pojedynczą wartość dla hello objaśnienia.<br><br>— Średnia: Średnia hello wartości ze wszystkich rekordów.<br>— Count Liczba wszystkich rekordów zwróconych przez zapytanie hello.<br>-Ostatniej próbki: Wartość od ostatniego interwału hello objęte hello wykresu.<br>-Max: Wartość maksymalna z interwały powitania objęte hello wykresu.<br>-Min: Wartość minimalna z interwały powitania objęte hello wykresu.<br>— Suma: Suma hello wartość ze wszystkich rekordów. |
| **Wykres liniowy** |**> Oś Y** |
| Użyj skali logarytmicznej |Wybierz toouse skali logarytmicznej dla hello osi y. |
| Jednostki |Określ jednostki hello hello wartości zwróconych przez zapytanie hello.  Te informacje są używane toodisplay etykiety na wykresie hello wskazujący hello typy wartości i opcjonalnie do konwersji wartości hello.  Hello typ jednostki określa kategorię hello hello jednostki i definiuje wartości hello bieżącego typu jednostki, które są dostępne.  Jeśli wybierzesz wartość w hello toothen konwersji liczbowych wartości są konwertowane hello bieżącej jednostki typu toohello przekonwertować tootype. |
| Etykiety niestandardowej |Tekst toodisplay hello osi Y dalej toohello etykiety dla typu jednostki hello.  Jeśli etykieta nie jest określony, wyświetlany jest tylko typ jednostki hello. |
| **Lista** | |
| Zapytanie |Zapytanie toorun hello listy.  Liczba Hello hello liczbę rekordów zwróconych przez zapytanie hello będą wyświetlane. |
| Ukryj wykresu |Wybierz toodisable hello wykres toohello prawej hello kolumny liczbowej. |
| Włącz wykresy przebiegu w czasie |Wybierz wykres przebiegu w czasie toodisplay zamiast poziomy pasek.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Kolor |Kolor słupków hello lub wykresy przebiegu w czasie. |
| Operacja |Operacja tooperform dla hello przebiegu w czasie.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Nazwa i wartość separatora |Ogranicznik pojedynczy znak, jeśli właściwość text hello tooparse do wielu wartości.  Zobacz [typowe ustawienia](#name-value-separator) szczegółowe informacje. |
| Zapytanie nawigacji |Zapytanie toorun po wybraniu przez użytkownika hello element na liście hello.  Zobacz [typowe ustawienia](#navigation-query) szczegółowe informacje. |
| **Lista** |**> Tytuły kolumn** |
| Nazwa |Tekst toodisplay u góry hello hello pierwszą kolumnę hello listy. |
| Wartość |Tekst toodisplay u góry hello hello drugiej kolumny hello listy. |
| **Lista** |**> Progi** |
| Włącz progi |Wybierz tooenable progów.  Zobacz [typowe ustawienia](#thresholds) szczegółowe informacje. |

## <a name="line-chart--list-part"></a>Część wiersza wykresu & listy
Nagłówek przedstawia wykres liniowy z wielu serii w wyniku zapytania dziennika wraz z upływem czasu.  Lista przedstawia hello top dziesięć wyniki zapytania z Wykres wskazujący hello względne wartości liczbowej lub zmian w czasie.

![Widok wykresu & listy wiersza](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Ustawienie | Opis |
|:--- |:--- |
| **Ogólne** | |
| Tytuł grupy |Toodisplay tekst u góry hello hello kafelka. |
| Nowa grupa |Wybierz toocreate nową grupę w widoku hello, zaczynając od hello bieżący widok. |
| Ikona |Obraz pliku toodisplay dalej toohello wynik w nagłówku hello. |
| Użyj ikony |Wybierz toohave hello ikonę wyświetlania. |
| **Nagłówek** | |
| Tytuł |Tekst toodisplay u góry hello hello nagłówka. |
| Podtytuł |Toodisplay tekstu w obszarze hello tytuł u góry hello hello nagłówka. |
| **Wykres liniowy** | |
| Zapytanie |Zapytanie toorun hello linii wykresu.  Hello pierwszy właściwość powinna być tekst wartość i hello drugi wartość liczbową.  Jest to zazwyczaj kwerendę, która używa hello **miary** wyniki toosummarize słów kluczowych.  Jeśli zapytanie hello używa hello **interwał** — słowo kluczowe, a następnie hello osi x wykresu hello użyje tego przedziału czasu.  Jeśli zapytanie hello nie obejmuje hello **interwał** — słowo kluczowe, a następnie co godzinę interwały są używane do hello osi x. |
| **Wykres liniowy** |**> Oś Y** |
| Użyj skali logarytmicznej |Wybierz toouse skali logarytmicznej dla hello osi y. |
| Jednostki |Określ jednostki hello hello wartości zwróconych przez zapytanie hello.  Te informacje są używane toodisplay etykiety na wykresie hello wskazujący hello typy wartości i opcjonalnie do konwersji wartości hello.  Hello typ jednostki określa kategorię hello hello jednostki i definiuje wartości hello bieżącego typu jednostki, które są dostępne.  Jeśli wybierzesz wartość w hello toothen konwersji liczbowych wartości są konwertowane hello bieżącej jednostki typu toohello przekonwertować tootype. |
| Etykiety niestandardowej |Tekst toodisplay hello osi Y dalej toohello etykiety dla typu jednostki hello.  Jeśli etykieta nie jest określony, wyświetlany jest tylko typ jednostki hello. |
| **Lista** | |
| Zapytanie |Zapytanie toorun hello listy.  Liczba Hello hello liczbę rekordów zwróconych przez zapytanie hello będą wyświetlane. |
| Ukryj wykresu |Wybierz toodisable hello wykres toohello prawej hello kolumny liczbowej. |
| Włącz wykresy przebiegu w czasie |Wybierz wykres przebiegu w czasie toodisplay zamiast poziomy pasek.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Kolor |Kolor słupków hello lub wykresy przebiegu w czasie. |
| Operacja |Operacja tooperform dla hello przebiegu w czasie.  Zobacz [typowe ustawienia](#sparklines) szczegółowe informacje. |
| Nazwa i wartość separatora |Ogranicznik pojedynczy znak, jeśli właściwość text hello tooparse do wielu wartości.  Zobacz [typowe ustawienia](#name-value-separator) szczegółowe informacje. |
| Zapytanie nawigacji |Zapytanie toorun po wybraniu przez użytkownika hello element na liście hello.  Zobacz [typowe ustawienia](#navigation-query) szczegółowe informacje. |
| **Lista** |**> Tytuły kolumn** |
| Nazwa |Tekst toodisplay u góry hello hello pierwszą kolumnę hello listy. |
| Wartość |Tekst toodisplay u góry hello hello drugiej kolumny hello listy. |
| **Lista** |**> Progi** |
| Włącz progi |Wybierz tooenable progów.  Zobacz [typowe ustawienia](#thresholds) szczegółowe informacje. |

## <a name="stack-of-line-charts-part"></a>Stos część wykresów wiersza
Wyświetla trzech oddzielnych wierszach wykresów z wielu serii w wyniku zapytania dziennika wraz z upływem czasu.

![Stos wykresy liniowe](media/log-analytics-view-designer/view-stack-line-charts.png)

| Ustawienie | Opis |
|:--- |:--- |
| **Ogólne** | |
| Tytuł grupy |Toodisplay tekst u góry hello hello kafelka. |
| Nowa grupa |Wybierz toocreate nową grupę w widoku hello, zaczynając od hello bieżący widok. |
| Ikona |Obraz pliku toodisplay dalej toohello wynik w nagłówku hello. |
| **Wykres 1<br>wykresu 2<br>wykresu 3** |**> Nagłówek** |
| Tytuł |Tekst toodisplay u góry hello hello wykresu. |
| Podtytuł |Toodisplay tekstu w obszarze hello tytuł u góry hello hello wykresu. |
| **Wykres 1<br>wykresu 2<br>wykresu 3** |**Wykres liniowy** |
| Zapytanie |Zapytanie toorun hello linii wykresu.  Hello pierwszy właściwość powinna być tekst wartość i hello drugi wartość liczbową.  Jest to zazwyczaj kwerendę, która używa hello **miary** wyniki toosummarize słów kluczowych.  Jeśli zapytanie hello używa hello **interwał** — słowo kluczowe, a następnie hello osi x wykresu hello użyje tego przedziału czasu.  Jeśli zapytanie hello nie obejmuje hello **interwał** — słowo kluczowe, a następnie co godzinę interwały są używane do hello osi x. |
| **Wykres** |**> Oś Y** |
| Użyj skali logarytmicznej |Wybierz toouse skali logarytmicznej dla hello osi y. |
| Jednostki |Określ jednostki hello hello wartości zwróconych przez zapytanie hello.  Te informacje są używane toodisplay etykiety na wykresie hello wskazujący hello typy wartości i opcjonalnie do konwersji wartości hello.  Hello typ jednostki określa kategorię hello hello jednostki i definiuje wartości hello bieżącego typu jednostki, które są dostępne.  Jeśli wybierzesz wartość w hello toothen konwersji liczbowych wartości są konwertowane hello bieżącej jednostki typu toohello przekonwertować tootype. |
| Etykiety niestandardowej |Tekst toodisplay hello osi Y dalej toohello etykiety dla typu jednostki hello.  Jeśli etykieta nie jest określony, wyświetlany jest tylko typ jednostki hello. |

## <a name="common-settings"></a>Typowe ustawienia
Hello w następujących sekcjach opisano części wizualizacji tooseveral typowe ustawienia.

### <a name="name-value-separator">Nazwa i wartość separatora</a>
Ogranicznik pojedynczy znak, jeśli właściwość text hello tooparse w wyniku zapytania listy do wielu wartości.  Jeśli zostanie określony ogranicznik, możesz podać nazwy dla każdego pola rozdzielonych hello sam ogranicznik w polu Nazwa hello.

Rozważmy na przykład właściwość o nazwie *lokalizacji* który dostępnych wartości takich jak *41 budowania Redmond* i *Bellevue Building12*.  Można określić — hello nazwy i wartości separatora i *budowania miast* dla hello nazwy.  Spowoduje to Przeanalizuj wartość każdej w dwie właściwości o nazwie *miasta* i *budynku*.

### <a name="navigation-query">Zapytanie nawigacji</a>
Zapytanie toorun po wybraniu przez użytkownika hello element na liście hello.  Użyj *{wybranego elementu}* tooinclude hello składnia elementu hello wybrano użytkownika.

Na przykład jeśli hello zapytania ma kolumnę o nazwie *komputera* zapytanie nawigacji hello *{wybranego elementu}*, zapytania, takie jak *komputer = "Mój komputer"* będzie można uruchamiać, gdy Użytkownik Hello wybrany komputer.  Jeśli zapytanie nawigacji hello jest *typu = zdarzeń {wybranego elementu}* następnie hello zapytania *typu = zdarzeń komputer = "Mój komputer"* zostanie uruchomione.

### <a name="sparklines">Wykresy przebiegu w czasie</a>
Wykres przebiegu w czasie jest wykres liniowy małych, która ilustruje hello wartość wpisu listy wraz z upływem czasu.  Wizualizacja składników z listy możesz wybrać względnej wartości liczbowej hello toodisplay poziomym paskiem wskazującą, czy wykres przebiegu w czasie jej wartość wskazującą, w czasie.

Witaj w poniższej tabeli opisano ustawienia powitania dla wykresy przebiegu w czasie.

| Ustawienie | Opis |
|:--- |:--- |
| Włącz wykresy przebiegu w czasie |Wybierz wykres przebiegu w czasie toodisplay zamiast poziomy pasek. |
| Operacja |Wykresy przebiegu w czasie są włączone, to hello tooperform operacja dla każdej właściwości w hello listy toocalculate hello wartości hello przebiegu w czasie.<br><br>-Ostatniej próbki: Ostatnia wartość hello serii przedziałach czasu hello.<br>-Max: Wartość maksymalna hello serii przedziałach czasu hello.<br>-Min: Wartość minimalna hello serii przedziałach czasu hello.<br>— Suma: Suma wartości serii hello przedziałach czasu hello.<br>-Podsumowanie: Używa hello tego samego polecenia miary hello kwerendy w nagłówku hello. |

### <a name="thresholds">Progi</a>
Progi pozwalają toodisplay ikona kolorowy następny element tooeach na liście, umożliwiając szybkie wizualnej elementów, które przekracza określoną wartość, lub mieścić się w określonym zakresie.  Na przykład można wyświetlić zieloną ikonę dla elementów z dozwolonej wartości, żółty, jeśli wartość hello jest zakresu, który wyświetla ostrzeżenie i czerwony, w razie przekroczenia wartości błędu.

Po włączeniu progi dla części, należy określić co najmniej jeden progów.  Jeśli wartość elementu hello jest większa niż wartość progowa i niższa niż wartość progowa dalej hello, używana jest koloru.  Jeśli element hello jest większa niż wartość progowa następnie najwyższy, tego koloru zostanie ustawiona.   

Każdy zestaw próg ma jeden próg o wartości **domyślne**.  Jest to kolor hello ustawiony w przypadku przekroczenia żadnych innych wartości.  Można dodawać i usuwać progów, klikając hello  **+**  lub **x** przycisku.

Witaj w poniższej tabeli opisano hello ustawienia progów.

| Ustawienie | Opis |
|:--- |:--- |
| Włącz progi |Wybierz toodisplay toohello ikonę Kolor rogu każdej wartości wskazującą jego progi względną toospecified kondycji. |
| Nazwa |Wartość progowa hello tooidentify nazwy. |
| Próg |Wartość progu hello.  kolor toohello hello przekroczenia wartości elementu hello najwyższą wartość progowa jest zestaw kolorów kondycji powitania dla każdego elementu listy.  Istnieje jeden domyślny próg będący hello koloru w przypadku przekroczenia wartości progowych, nie. |
| Kolor |Kolor hello wartość progową. |

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) toosupport hello zapytań w częściach wizualizacji.
