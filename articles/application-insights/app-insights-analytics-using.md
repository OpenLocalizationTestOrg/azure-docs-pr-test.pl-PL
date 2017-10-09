---
title: "aaaUsing Analytics — narzędzie wyszukiwania zaawansowanego hello Azure Application Insights | Dokumentacja firmy Microsoft"
description: "Przy użyciu hello Analytics, hello wydajne diagnostycznych narzędzie do wyszukiwania usługi Application insights. "
services: application-insights
documentationcenter: 
author: danhadari
manager: carmonm
ms.assetid: c3b34430-f592-4c32-b900-e9f50ca096b3
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6e0246848457db368c57d08c47b5bf73f4e5e3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-analytics-in-application-insights"></a>Za pomocą analizy w usłudze Application Insights
[Analiza](app-insights-analytics.md) to funkcja wyszukiwania zaawansowanego hello [usługi Application Insights](app-insights-overview.md). Te strony opisano język zapytań usługi Analiza dzienników.

* **[Obejrzyj klip wideo wprowadzenia hello](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Przetestuj Analytics na naszych danych symulowane](https://analytics.applicationinsights.io/demo)**  aplikacji nie jest jeszcze wysyłania danych tooApplication szczegółowych informacji.

## <a name="open-analytics"></a>Otwórz analityka
Macierzysty zasobów aplikacji w usłudze Application Insights kliknij Analytics.

![Otwórz portal.azure.com otworzyć zasobu usługi Application Insights, a następnie kliknij przycisk Analytics.](./media/app-insights-analytics-using/001.png)

Samouczek wbudowanego Hello daje sugestii dotyczących co można zrobić.

Brak [szerszej samouczek tutaj](app-insights-analytics-tour.md).

## <a name="query-your-telemetry"></a>Zapytanie telemetrii
### <a name="write-a-query"></a>Napisz zapytanie
![Wyświetlanie schematu](./media/app-insights-analytics-using/150.png)

Zaczyna się od nazwy hello dowolnego hello tabel wymienionych po lewej stronie powitania (lub hello [zakres](https://docs.loganalytics.io/queryLanguage/query_language_rangeoperator.html) lub [Unii](https://docs.loganalytics.io/queryLanguage/query_language_unionoperator.html) operatory). Użyj `|` toocreate a planowanej sprzedaży [operatory](https://docs.loganalytics.io/learn/cheatsheets/useful_operators.html). 

IntelliSense wyświetla hello operatory i hello elementy wyrażenia, których można użyć. Kliknij ikonę informacji o hello (lub naciśnij klawisze CTRL + SPACJA) tooget dłuższy opis i przykłady toouse każdego elementu.

Zobacz hello [samouczek języka Analytics](app-insights-analytics-tour.md) i [materiały referencyjne dotyczące języka](app-insights-analytics-reference.md).

### <a name="run-a-query"></a>Uruchamianie zapytania
![Wykonanie kwerendy](./media/app-insights-analytics-using/130.png)

1. Pojedynczy podziały wierszy można użyć w zapytaniu.
2. Umieść kursor hello wewnątrz lub na końcu hello hello zapytania, które chcesz toorun.
3. Sprawdź hello przedział czasu zapytania. (Można zmienić lub zmienić, umieszczając w niej własnych [ `where...timestamp...` ](https://docs.loganalytics.io/concepts/concepts_datatypes_timespan.html) klauzuli w zapytaniu.)
3. Kliknij przycisk Przejdź toorun hello zapytania.
4. Nie umieszczaj pustych wierszy w zapytaniu. Kilka zapytań rozdzielonych można przechowywać w jedną kartę zapytanie, rozdzielając je puste wiersze. Uruchamia tylko zapytania hello ma hello kursora.

### <a name="save-a-query"></a>Zapisz zapytanie
![Zapisywanie zapytania](./media/app-insights-analytics-using/140.png)

1. Zapisz bieżący plik zapytania hello.
2. Otwórz plik zapisanego zapytania.
3. Utwórz nowy plik zapytania.

## <a name="see-hello-details"></a>Zobacz szczegóły hello
Rozwiń wszystkie wiersze w toosee wyniki hello jego pełną listę właściwości. Można rozwinąć wszystkie właściwości, która jest wartością strukturalnych — na przykład, niestandardowe wymiary lub stosu hello w Wystąpił wyjątek.

![Rozwiń węzeł wiersza](./media/app-insights-analytics-using/070.png)

## <a name="arrange-hello-results"></a>Rozmieść hello wyników
Można sortować, filtrowanie, z podziałem na strony i hello wyniki zwracane z kwerendy grupy.

> [!NOTE]
> Sortowanie, grupowanie i filtrowanie w przeglądarce hello nie ponownie uruchom zapytanie. Rozmieszczanie one tylko hello wyników zwróconych przez zapytanie ostatniego. 
> 
> tooperform te zadania na serwerze hello przed hello są zwracane, zapisać zapytanie z hello [sortowania](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html), [Podsumuj](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) i [gdzie](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) operatorów.
> 
> 

Wybierz kolumny hello jak jak toosee, przeciągnij toorearrange nagłówki kolumn, a zmiany rozmiaru kolumn przez przeciąganie ich obramowania.

![Rozmieść kolumn](./media/app-insights-analytics-using/030.png)

### <a name="sort-and-filter-items"></a>Sortowanie i filtrowanie elementów
Sortuj wyniki, klikając hello nagłówek kolumny. Kliknij ponownie przycisk toosort hello w inny sposób, i kliknij przycisk innej godziny toorevert toohello oryginalnego kolejność zwracanych przez zapytanie.

Użyj toonarrow ikonę filtru hello wyszukiwania.

![Sortowanie i filtrowanie kolumn](./media/app-insights-analytics-using/040.png)

### <a name="group-items"></a>Grupowanie elementów
toosort przez więcej niż jedną kolumnę, za pomocą grupowania. Najpierw go włączyć, a następnie przeciągnij nagłówków kolumn na powitania miejsce powyżej hello tabeli.

![Grupa](./media/app-insights-analytics-using/060.png)

### <a name="missing-some-results"></a>Brakuje niektórych wyników?

Jeśli uważasz, że nie występują wszystkie wyniki hello oczekiwane, istnieje kilka możliwych przyczyn.

* **Filtr zakresu czasu**. Domyślnie będzie widoczne są tylko wyniki z hello ostatnich 24 godzin. Brak automatyczny filtr, który ogranicza zakres hello wyników, które są pobierane z tabel źródłowych hello. 

    Jednak można zmienić zakres czasowy hello filtru przy użyciu menu rozwijanego hello.

    Lub zakresu automatycznego hello można zastąpić, umieszczając w niej własnych [ `where  ... timestamp ...` klauzuli](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) do zapytania. Na przykład:

    `requests | where timestamp > ago('2d')`

* **Limit wyników**. Ma limitu 10 wierszy k na powitania wyniki zwrócone z hello portalu. Ostrzeżenie pokazuje, jeśli można przejść, przekraczając hello limit. Jeśli tak się stanie, sortowanie wyników w tabeli hello zawsze niewidoczne wszystkie hello rzeczywiste pierwszego lub ostatniego wyniki. 

    Należy dobrze tooavoid naciśnięcie hello limit. Użyj filtru zakresu czasu hello lub używać operatorów, takich jak:

  * [100 najpopularniejszych przez sygnatury czasowej](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) 
  * [podejmij 100](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html)
  * [Podsumowanie](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html) 
  * [gdzie sygnatury czasowej > ago(3d)](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html)

(Więcej niż 10 KB wierszy chcesz? Należy rozważyć użycie [eksportu ciągłego](app-insights-export-telemetry.md) zamiast tego. Analiza jest przeznaczona dla analizy, a nie podczas pobierania danych pierwotnych).

## <a name="diagrams"></a>Diagramy
Wybierz typ hello diagramu, który chcesz:

![Wybierz typ diagramu](./media/app-insights-analytics-using/230.png)

Jeśli masz kilka kolumn prawego typów hello można hello x i osi y i kolumnę wymiary toosplit hello wyniki według.

Domyślnie wyniki są początkowo wyświetlane jako tabelę i ręcznie wybrać hello diagramu. Można używać hello [renderowania dyrektywy](https://docs.loganalytics.io/queryLanguage/query_language_renderoperator.html) na końcu hello tooselect zapytania diagramu.

### <a name="analytics-diagnostics"></a>Diagnostyka analityka


Na timechart przypadku nagłego kolekcji lub krok danych, mogą pojawić się zaznaczony punkt hello wiersza. Oznacza to, Diagnostyka Analytics zidentyfikowane kombinację właściwości, które odfiltrowywania hello nagła zmiana. Kliknij przycisk tooget punktu hello bardziej szczegółowo na powitania filtru i toosee hello filtrowana wersja. To może pomóc w zidentyfikowaniu jaka zmiana spowodowane hello. 

[Dowiedz się więcej o diagnostyce analityka](app-insights-analytics-diagnostics.md)


![Diagnostyka analityka](./media/app-insights-analytics-using/analytics-diagnostics.png)

## <a name="pin-toodashboard"></a>Toodashboard numeru PIN
Można przypiąć diagramu lub tabeli tooone z Twojej [udostępnionych pulpitów nawigacyjnych](app-insights-dashboards.md) — wystarczy kliknąć hello numeru pin. (Może być konieczne zbyt[uaktualniania aplikacji przez cennik pakietu](app-insights-pricing.md) tooturn tę funkcję.) 

![Kliknij polecenie Przypnij hello](./media/app-insights-analytics-using/pin-01.png)

Oznacza to, że podczas Podsumowując toohelp pulpitu nawigacyjnego, można monitorować wydajność hello lub użycia usług sieci web można dołączyć dość złożone analizy obok hello innych metryk. 

Na pulpicie nawigacyjnym toohello tabeli można przypiąć, jeśli ma cztery lub mniejszą liczbę kolumn. Tylko hello górne siedmiu wiersze są wyświetlane.

### <a name="dashboard-refresh"></a>Odświeżanie pulpitu nawigacyjnego
pulpit nawigacyjny toohello wykresu przypięty Hello jest automatycznie odświeżany przez ponowne uruchomienie zapytania hello co około godzin. Można także kliknąć przycisk Odśwież hello.

### <a name="automatic-simplifications"></a>Automatyczne uproszczenia

Niektórych uproszczenia są stosowane tooa wykresu po przypięciu tooa pulpitu nawigacyjnego.

**Czas ograniczeń:** zapytania są automatycznie ograniczony toohello w ciągu ostatnich 14 dni. Hello efekt jest hello takie same jak, jeśli kwerenda zawiera `where timestamp > ago(14d)`.

**Ograniczenie liczby bin:** podczas wyświetlania wykresu, który ma wiele odrębny bins (zazwyczaj wykresu słupkowego) hello mniej bins wypełnione automatycznie są pogrupowane w jednej "inne" bin. Na przykład tego zapytania:

    requests | summarize count_search = count() by client_CountryOrRegion

wygląda następująco w module analiz:

![Wykres z tail długa](./media/app-insights-analytics-using/pin-07.png)

Jednak gdy przypiąć pulpitu nawigacyjnego tooa go wygląda następująco:

![Wykres z ograniczoną bins](./media/app-insights-analytics-using/pin-08.png)

## <a name="export-tooexcel"></a>TooExcel eksportu
Po uruchomieniu kwerendy, można pobrać pliku CSV. Kliknij przycisk **wyeksportować Excel**.

## <a name="export-toopower-bi"></a>Eksportuj tooPower analizy Biznesowej
Umieść kursor hello w zapytaniu i wybierz polecenie **wyeksportować usługi Power BI**.

![Eksportowanie z tooPower Analytics analizy Biznesowej](./media/app-insights-analytics-using/240.png)

Możesz uruchomić hello zapytania w usłudze Power BI. Możesz ustawić toorefresh zgodnie z harmonogramem.

Usługa Power BI można tworzyć pulpity nawigacyjne, które zbieranie danych z różnych źródeł.

[Więcej informacji na temat eksportowania tooPower analizy Biznesowej](app-insights-export-power-bi.md)

## <a name="deep-link"></a>Głębokie łącze

Uzyskaj link w obszarze **eksportu, link udziału** wysłanie tooanother użytkownika. Podany użytkownik hello ma [grupy zasobów tooyour dostępu](app-insights-resources-roles-access-control.md), hello kwerendy będą otwierane w hello interfejsu użytkownika analizy.

(Łącze hello hello tekst zapytania jest umieszczany po "? q =" gzip skompresowane i algorytmem base-64. Można napisać kod toogenerate głębokiego łącza musisz zapewnić toousers. Jednak zalecane jest sposób toorun Analytics z kodu za pomocą hello hello [interfejsu API REST](https://dev.applicationinsights.io/).)


## <a name="automation"></a>Automatyzacja

Użyj hello [interfejsu API REST dostępu do danych](https://dev.applicationinsights.io/) toorun Analytics zapytania. [Na przykład](https://dev.applicationinsights.io/apiexplorer/query?appId=DEMO_APP&apiKey=DEMO_KEY&query=requests%0A%7C%20where%20timestamp%20%3E%3D%20ago%2824h%29%0A%7C%20count) (przy użyciu programu PowerShell):

```PS
curl "https://api.applicationinsights.io/beta/apps/DEMO_APP/query?query=requests%7C%20where%20timestamp%20%3E%3D%20ago(24h)%7C%20count" -H "x-api-key: DEMO_KEY"
```

W odróżnieniu od hello interfejsu użytkownika analizy hello interfejsu API REST nie powoduje automatycznego dodania kwerendy tooyour ograniczenia sygnatury czasowej. Pamiętaj, aby tooadd własne klauzuli where, tooavoid Uzyskiwanie dużych odpowiedzi.



## <a name="import-data"></a>Importowanie danych

Dane można zaimportować z pliku CSV. Zwykle jest tooimport dane statyczne, które można połączyć z tabelami z telemetrii. 

Na przykład uwierzytelnionym użytkownikom są oznaczane w obrębie telemetrii alias lub zaciemnionego identyfikator, można zaimportować tabelę, która mapuje nazwy tooreal aliasy. Wykonując sprzężenie na dane telemetryczne żądania hello, można zidentyfikować użytkowników według ich rzeczywistym nazw w raportach analizy hello.

### <a name="define-your-data-schema"></a>Zdefiniuj schemat danych

1. Kliknij przycisk **ustawienia** (u góry po lewej), a następnie **źródeł danych**. 
2. Dodawanie źródła danych, postępując zgodnie z instrukcjami hello. Jesteś zadawane toosupply próbkę danych hello, który powinien zawierać co najmniej 10 wierszy. Następnie poprawić hello schematu.

Określa źródło danych, które można następnie użyć tooimport poszczególnych tabel.

### <a name="import-a-table"></a>Importowanie tabeli

1. Otwórz z definicji źródła danych z listy hello.
2. Kliknij przycisk "Przekaż" i wykonaj hello instrukcje tooupload hello tabeli. Obejmuje to tooa wywołania interfejsu API REST i dlatego jest łatwe tooautomate. 

Tabela jest teraz dostępna do użycia w zapytaniach Analytics. Zostanie wyświetlony na analityka 

### <a name="use-hello-table"></a>Tabela hello

Załóżmy, że Twoje definicji źródła danych jest nazywany `usermap`, i ma dwa pola `realName` i `user_AuthenticatedId`. Witaj `requests` tabeli również zawiera pole o nazwie `user_AuthenticatedId`, więc jest łatwe toojoin je:

```AIQL

    requests
    | where notempty(user_AuthenticatedId) | take 10
    | join kind=leftouter ( usermap ) on user_AuthenticatedId 
```
Witaj tabeli wynikowej żądań ma dodatkowe kolumny `realName`.

### <a name="import-from-logstash"></a>Importuj z LogStash

Jeśli używasz [LogStash](https://www.elastic.co/guide/en/logstash/current/getting-started-with-logstash.html), można użyć tooquery analizy dzienników. Użyj hello [wtyczkę, która powoduje przekazanie w potoku danych do analizy](https://github.com/Microsoft/logstash-output-application-insights). 

## <a name="video"></a>Połączenia wideo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

