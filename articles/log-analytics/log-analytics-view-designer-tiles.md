---
title: "Odwołanie aaaTile Widok projektanta w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "Widok projektanta w analizy dzienników umożliwia toocreate niestandardowe widoki konsoli OMS hello zawierających różne wizualizacje danych w repozytorium OMS hello. Ten artykuł zawiera odwołanie hello ustawienia dla każdego z hello toouse dostępne Kafelki w niestandardowych widoków."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 41787c8f-6c13-4520-b0d3-5d3d84fcf142
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 4706abb16b8a3719f5dbe8c89cd61739391ab8f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-tile-reference"></a>Odwołanie kafelka Projektant widoków analizy dziennika
Hello Widok projektanta w analizy dzienników umożliwia toocreate niestandardowe widoki konsoli OMS hello zawierających różne wizualizacje danych w repozytorium OMS hello. Ten artykuł zawiera odwołanie hello ustawienia dla każdego z hello toouse dostępne Kafelki w niestandardowych widoków.

Inne artykuły, które są dostępne dla projektanta widoku są następujące:

* [Wyświetl projektanta](log-analytics-view-designer.md) — omówienie hello Projektant widoków i procedur tworzenia i edytowania widoków niestandardowych.
* [Odwołanie do części wizualizacji](log-analytics-view-designer-parts.md) — odwołanie hello ustawienia dla każdego z hello Kafelki toouse dostępne w niestandardowych widoków.

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie zapytania we wszystkich widokach musi być napisana w hello [nowy język kwerendy](https://go.microsoft.com/fwlink/?linkid=856078).  Wszystkie widoki, które zostały utworzone przed uaktualniono hello obszaru roboczego będzie automtically przekonwertować.

Witaj poniższej tabeli wymieniono hello różnych typów kafelków, które są dostępne w hello Widok projektanta.  Poniższe rozdziały zawierają Hello opis każdego typu kafelka w szczegółów i ich właściwości.

| Kafelek | Opis |
|:--- |:--- |
| [Numer](#number-tile) |Numer pojedynczego przedstawiający liczby rekordów w wyniku zapytania. |
| [Dwóch liczb](#two-numbers-tile) |Wyświetlanie liczby rekordów z dwóch różnych zapytań dwóch liczb pojedynczego. |
| [Pierścień](#donut-tile) |Wykres pierścieniowy przedstawiający na podstawie zapytania w Centrum hello podsumowania wartość. |
| [Wykres liniowy & objaśnienia](#line-chart-amp-callout-tile) |Wykres liniowy, na podstawie zapytania i objaśnienie z wartością podsumowania. |
| [Wykres liniowy](#line-chart-tile) |Wykres liniowy, na podstawie zapytania. |
| [Dwóch osiach czasu](#two-timelines-tile) |Wykres kolumnowy z dwóch serii, każda oparta na osobne zapytania. |

## <a name="number-tile"></a>Liczba kafelka
Witaj **numer** kafelka Wyświetla jeden numer przedstawiający hello liczbę rekordów z zapytaniem dziennika i etykiety.

![Liczba kafelka](media/log-analytics-view-designer/tile-number.png)

| Ustawienie | Opis |
|:--- |:--- |
| Nazwa |Toodisplay tekst u góry hello hello kafelka. |
| Opis |Tekst toodisplay pod nazwą kafelka hello. |
| **Kafelek** | |
| Legenda |Toodisplay tekstu w obszarze hello wartość. |
| Zapytanie |Toorun zapytania.  Liczba Hello hello liczbę rekordów zwróconych przez zapytanie hello będą wyświetlane. |
| **Zaawansowane** |**> Weryfikacja przepływu danych** |
| Enabled (Włączony) |Wybierz, jeśli Weryfikacja przepływu danych powinno być włączone dla kafelka hello.  Oferuje komunikat alternatywnego, jeśli dane nie są dostępne dla hello kafelka.  Jest to najczęściej używanymi tooprovide komunikat okresie hello tymczasowego podczas widoku hello jest zainstalowany i danych jest dostępne. |
| Zapytanie |Zapytania toorun toocheck, jeśli dane są dostępne do wyświetlenia hello.  Jeśli hello zapytanie nie zwróciło żadnych wyników, zamiast wartości hello z hello główne zapytanie zostanie wyświetlony komunikat. |
| Komunikat |Toodisplay komunikat, jeśli hello przepływu danych weryfikacji zapytanie zwraca żadnych danych.  Jeśli podasz żaden komunikat *wykonywania oceny* jest wyświetlany. |


## <a name="two-numbers-tile"></a>Kafelek dwóch liczb
Witaj **dwa numer** kafelka zawiera dwie liczb przedstawiający hello liczba rekordy z dwóch różnych dziennika zapytań i etykiety dla każdego.

![Kafelek dwóch liczb](media/log-analytics-view-designer/tile-two-numbers.png)

| Ustawienie | Opis |
|:--- |:--- |
| Nazwa |Toodisplay tekst u góry hello hello kafelka. |
| Opis |Tekst toodisplay pod nazwą kafelka hello. |
| **Pierwszy Kafelek** | |
| Legenda |Toodisplay tekstu w obszarze hello wartość. |
| Zapytanie |Toorun zapytania.  Liczba Hello hello liczbę rekordów zwróconych przez zapytanie hello będą wyświetlane. |
| **Drugi kafelka** | |
| Legenda |Toodisplay tekstu w obszarze hello wartość. |
| Zapytanie |Toorun zapytania.  Liczba Hello hello liczbę rekordów zwróconych przez zapytanie hello będą wyświetlane. |
| **Zaawansowane** |**> Weryfikacja przepływu danych** |
| Enabled (Włączony) |Wybierz, jeśli Weryfikacja przepływu danych powinno być włączone dla kafelka hello.  Oferuje komunikat alternatywnego, jeśli dane nie są dostępne dla hello kafelka.  Jest to najczęściej używanymi tooprovide komunikat okresie hello tymczasowego podczas widoku hello jest zainstalowany i danych jest dostępne. |
| Zapytanie |Zapytania toorun toocheck, jeśli dane są dostępne do wyświetlenia hello.  Jeśli hello zapytanie nie zwróciło żadnych wyników, zamiast wartości hello z hello główne zapytanie zostanie wyświetlony komunikat. |
| Komunikat |Toodisplay komunikat, jeśli hello przepływu danych weryfikacji zapytanie zwraca żadnych danych.  Jeśli podasz żaden komunikat *wykonywania oceny* jest wyświetlany. |


## <a name="donut-tile"></a>Pierścień kafelka
Witaj **pierścień** kafelka Wyświetla jeden numer podsumowanie z kolumną wartości w zapytaniu dziennika.  pierścień Hello graficznie wyświetla wyniki hello top trzy rekordów.

![Pierścień kafelka](media/log-analytics-view-designer/tile-donut.png)

| Ustawienie | Opis |
|:--- |:--- |
| Nazwa |Toodisplay tekst u góry hello hello kafelka. |
| Opis |Tekst toodisplay pod nazwą kafelka hello. |
| **Pierścień** | |
| Zapytanie |Toorun zapytania dla hello pierścień.  Hello pierwszy właściwość powinna być tekst wartość i hello drugi wartość liczbową.  Jest to zazwyczaj kwerendę, która używa hello **miary** wyniki toosummarize słów kluczowych. |
| **Pierścień** |**> Centrum** |
| Tekst |Toodisplay tekst w kolumnie wartość hello wewnątrz hello pierścień. |
| Operacja |Witaj tooperform operacji na powitania wartość właściwości toosummarize tooa pojedynczą wartość.<br><br>— Suma: Określanie hello wszystkich rekordów z hello wartości właściwości.<br>-Procent: Procent wartości hello sumowane z rekordów z toohello wartości właściwości hello sumowane wartości wszystkich rekordów. |
| Wynik wartości używana podczas operacji Centrum |Opcjonalnie kliknij hello tooadd znak plus, co najmniej jedna wartość.  Hello wyniki zapytania hello będzie ograniczona toorecords z wartościami właściwości hello, które określisz.  Jeśli wartości nie zostaną dodane, niż wszystkie rekordy są uwzględniane w hello zapytania. |
| **Pierścień** |**> Dodatkowe opcje** |
| Kolory |Witaj toodisplay kolor dla każdego z trzech właściwości top hello.  Kolory alternatywny toospecify na określone wartości właściwości, następnie użyć zaawansowane mapowanie kolorów. |
| Mapowanie kolorów zaawansowane |Wyświetla kolor określone wartości właściwości.  Jeśli podaną wartość hello hello trzy pierwsze, a następnie Alternatywny kolor hello jest wyświetlany zamiast Kolor standardowy hello.  Jeśli nie ma właściwości hello hello trzy pierwsze, a następnie hello kolor nie jest wyświetlany. |
| **Zaawansowane** |**> Weryfikacja przepływu danych** |
| Enabled (Włączony) |Wybierz, jeśli Weryfikacja przepływu danych powinno być włączone dla kafelka hello.  Oferuje komunikat alternatywnego, jeśli dane nie są dostępne dla hello kafelka.  Jest to najczęściej używanymi tooprovide komunikat okresie hello tymczasowego podczas widoku hello jest zainstalowany i danych jest dostępne. |
| Zapytanie |Zapytania toorun toocheck, jeśli dane są dostępne do wyświetlenia hello.  Jeśli hello zapytanie nie zwróciło żadnych wyników, zamiast wartości hello z hello główne zapytanie zostanie wyświetlony komunikat. |
| Komunikat |Toodisplay komunikat, jeśli hello przepływu danych weryfikacji zapytanie zwraca żadnych danych.  Jeśli podasz żaden komunikat *wykonywania oceny* jest wyświetlany. |


## <a name="line-chart-tile"></a>Kafelek wykresu wiersza
Witaj **wykres liniowy** kafelka Wyświetla wykres liniowy z wielu serii w wyniku zapytania dziennika wraz z upływem czasu.  

![Wykres liniowy & objaśnienia kafelka](media/log-analytics-view-designer/tile-line-chart.png)

| Ustawienie | Opis |
|:--- |:--- |
| Nazwa |Toodisplay tekst u góry hello hello kafelka. |
| Opis |Tekst toodisplay pod nazwą kafelka hello. |
| **Wykres liniowy** | |
| Zapytanie |Zapytanie toorun hello linii wykresu.  Hello pierwszy właściwość powinna być tekst wartość i hello drugi wartość liczbową.  Jest to zazwyczaj kwerendę, która używa hello **miary** wyniki toosummarize słów kluczowych.  Jeśli zapytanie hello używa hello **interwał** — słowo kluczowe, a następnie hello osi x wykresu hello użyje tego przedziału czasu.  Jeśli zapytanie hello nie obejmuje hello **interwał** — słowo kluczowe, a następnie co godzinę interwały są używane do hello osi x. |
| **Wykres liniowy** |**> Oś Y** |
| Użyj skali logarytmicznej |Wybierz toouse skali logarytmicznej dla hello osi y. |
| Jednostki |Określ jednostki hello hello wartości zwróconych przez zapytanie hello.  Te informacje są używane toodisplay etykiety na wykresie hello wskazujący hello typy wartości i opcjonalnie do konwersji wartości hello.  Witaj **typ jednostki** określa kategorię hello hello jednostki i definiuje hello **bieżący typ jednostki** wartości, które są dostępne.  W przypadku wybrania wartości w **Konwertuj na** , a następnie wartości liczbowych hello są konwertowane hello **bieżącej jednostce** wpisz toohello **przekonwertować** typu. |
| Etykiety niestandardowej |Tekst toodisplay hello osi Y dalej toohello etykiety dla typu jednostki hello.  Jeśli etykieta nie jest określony, wyświetlany jest tylko typ jednostki hello. |
| **Zaawansowane** |**> Weryfikacja przepływu danych** |
| Enabled (Włączony) |Wybierz, jeśli Weryfikacja przepływu danych powinno być włączone dla kafelka hello.  Oferuje komunikat alternatywnego, jeśli dane nie są dostępne dla hello kafelka.  Jest to najczęściej używanymi tooprovide komunikat okresie hello tymczasowego podczas widoku hello jest zainstalowany i danych jest dostępne. |
| Zapytanie |Zapytania toorun toocheck, jeśli dane są dostępne do wyświetlenia hello.  Jeśli hello zapytanie nie zwróciło żadnych wyników, zamiast wartości hello z hello główne zapytanie zostanie wyświetlony komunikat. |
| Komunikat |Toodisplay komunikat, jeśli hello przepływu danych weryfikacji zapytanie zwraca żadnych danych.  Jeśli podasz żaden komunikat *wykonywania oceny* jest wyświetlany. |


## <a name="line-chart--callout-tile"></a>Kafelek linii objaśnienia & wykresu
Witaj **linii objaśnienia & wykresu** kafelka przedstawia wykres liniowy z wielu serii w wyniku zapytania dziennika przez godzinę i objaśnienie z podsumowaniem wartość.  

![Wykres liniowy & objaśnienia kafelka](media/log-analytics-view-designer/tile-line-chart-callout.png)

| Ustawienie | Opis |
|:--- |:--- |
| Nazwa |Toodisplay tekst u góry hello hello kafelka. |
| Opis |Tekst toodisplay pod nazwą kafelka hello. |
| **Wykres liniowy** | |
| Zapytanie |Zapytanie toorun hello linii wykresu.  Hello pierwszy właściwość powinna być tekst wartość i hello drugi wartość liczbową.  Jest to zazwyczaj kwerendę, która używa hello **miary** wyniki toosummarize słów kluczowych.  Jeśli zapytanie hello używa hello **interwał** — słowo kluczowe, a następnie hello osi x wykresu hello użyje tego przedziału czasu.  Jeśli zapytanie hello nie obejmuje hello **interwał** — słowo kluczowe, a następnie co godzinę interwały są używane do hello osi x. |
| **Wykres liniowy** |**> Objaśnienie** |
| Objaśnienie |Toodisplay tekstu tytułu powyżej hello objaśnienia wartości. |
| Nazwa serii |Wartość właściwości toouse serii hello hello objaśnienia wartości.  W przypadku serii wszystkie rekordy z kwerendy hello są używane. |
| Operacja |Witaj tooperform operacji na powitania wartość właściwości toosummarize tooa pojedynczą wartość dla hello objaśnienia.<br>— Średnia: Średnia hello wartości ze wszystkich rekordów.<br><br>-Liczba: Liczba wszystkich rekordów zwróconych przez zapytanie hello.<br>-Ostatniej próbki: Wartość od ostatniego interwału hello objęte hello wykresu.<br>-Max: Wartość maksymalna z interwały powitania objęte hello wykresu.<br>-Min: Wartość minimalna z interwały powitania objęte hello wykresu.<br>— Suma: Suma hello wartość ze wszystkich rekordów. |
| **Wykres liniowy** |**> Oś Y** |
| Użyj skali logarytmicznej |Wybierz toouse skali logarytmicznej dla hello osi y. |
| Jednostki |Określ jednostki hello hello wartości zwróconych przez zapytanie hello.  Te informacje są używane toodisplay etykiety na wykresie hello wskazujący hello typy wartości i opcjonalnie do konwersji wartości hello.  Witaj **typ jednostki** określa kategorię hello hello jednostki i definiuje hello **bieżący typ jednostki** wartości, które są dostępne.  W przypadku wybrania wartości w **Konwertuj na** , a następnie wartości liczbowych hello są konwertowane hello **bieżącej jednostce** wpisz toohello **przekonwertować** typu. |
| Etykiety niestandardowej |Tekst toodisplay hello osi Y dalej toohello etykiety dla typu jednostki hello.  Jeśli etykieta nie jest określony, wyświetlany jest tylko typ jednostki hello. |
| **Zaawansowane** |**> Weryfikacja przepływu danych** |
| Enabled (Włączony) |Wybierz, jeśli Weryfikacja przepływu danych powinno być włączone dla kafelka hello.  Oferuje komunikat alternatywnego, jeśli dane nie są dostępne dla hello kafelka.  Jest to najczęściej używanymi tooprovide komunikat okresie hello tymczasowego podczas widoku hello jest zainstalowany i danych jest dostępne. |
| Zapytanie |Zapytania toorun toocheck, jeśli dane są dostępne do wyświetlenia hello.  Jeśli hello zapytanie nie zwróciło żadnych wyników, zamiast wartości hello z hello główne zapytanie zostanie wyświetlony komunikat. |
| Komunikat |Toodisplay komunikat, jeśli hello przepływu danych weryfikacji zapytanie zwraca żadnych danych.  Jeśli podasz żaden komunikat *wykonywania oceny* jest wyświetlany. |


## <a name="two-timelines-tile"></a>Kafelek dwóch osiach czasu
Witaj **dwóch osiach czasu** kafelka wyświetla wyniki hello dwa zapytania dziennika w czasie, gdy wykresy kolumnowe.  Objaśnienie jest wyświetlany dla każdej serii.  

![Kafelek dwóch osiach czasu](media/log-analytics-view-designer/tile-two-timelines.png)

| Ustawienie | Opis |
|:--- |:--- |
| Nazwa |Toodisplay tekst u góry hello hello kafelka. |
| Opis |Tekst toodisplay pod nazwą kafelka hello. |
| Pierwszy wykres | |
| Legenda |Toodisplay tekstu w obszarze objaśnienia hello hello pierwszy serii. |
| Kolor |Kolor toouse kolumn hello hello pierwszej serii. |
| Wykres zapytania |Zapytanie toorun hello pierwszy serii.  Liczba Hello hello liczba rekordów przez każdego interwału czasu będą reprezentowane przez hello wykresu kolumn. |
| Operacja |Witaj tooperform operacji na powitania wartość właściwości toosummarize tooa pojedynczą wartość dla hello objaśnienia.<br><br>— Średnia: Średnia hello wartości ze wszystkich rekordów.<br>-Liczba: Liczba wszystkich rekordów zwróconych przez zapytanie hello.<br>-Ostatniej próbki: Wartość od ostatniego interwału hello objęte hello wykresu.<br>-Max: Wartość maksymalna z interwały powitania objęte hello wykresu. |
| **Drugi wykresu** | |
| Legenda |Toodisplay tekstu w obszarze objaśnienia hello hello drugi serii. |
| Kolor |Kolor toouse hello kolumn w drugiej serii hello. |
| Wykres zapytania |Zapytanie toorun hello drugi serii.  Liczba Hello hello liczba rekordów przez każdego interwału czasu będą reprezentowane przez hello wykresu kolumn. |
| Operacja |Witaj tooperform operacji na powitania wartość właściwości toosummarize tooa pojedynczą wartość dla hello objaśnienia.<br><br>— Średnia: Średnia hello wartości ze wszystkich rekordów.<br>-Liczba: Liczba wszystkich rekordów zwróconych przez zapytanie hello.<br>-Ostatniej próbki: Wartość od ostatniego interwału hello objęte hello wykresu.<br>-Max: Wartość maksymalna z interwały powitania objęte hello wykresu. |
| **Zaawansowane** |**> Weryfikacja przepływu danych** |
| Enabled (Włączony) |Wybierz, jeśli Weryfikacja przepływu danych powinno być włączone dla kafelka hello.  Oferuje komunikat alternatywnego, jeśli dane nie są dostępne dla hello kafelka.  Jest to najczęściej używanymi tooprovide komunikat okresie hello tymczasowego podczas widoku hello jest zainstalowany i danych jest dostępne. |
| Zapytanie |Zapytania toorun toocheck, jeśli dane są dostępne do wyświetlenia hello.  Jeśli hello zapytanie nie zwróciło żadnych wyników, zamiast wartości hello z hello główne zapytanie zostanie wyświetlony komunikat. |
| Komunikat |Toodisplay komunikat, jeśli hello przepływu danych weryfikacji zapytanie zwraca żadnych danych.  Jeśli podasz żaden komunikat *wykonywania oceny* jest wyświetlany. |


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) toosupport hello zapytania na kafelkach.
* Dodaj [części wizualizacji](log-analytics-view-designer-parts.md) tooyour widok niestandardowy.
