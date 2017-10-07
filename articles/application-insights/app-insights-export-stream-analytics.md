---
title: "za pomocą usługi Stream Analytics z usługi Azure Application Insights aaaExport | Dokumentacja firmy Microsoft"
description: "Analiza strumienia stale można przekształcać, filtrów i hello dane trasy, możesz wyeksportować z usługi Application Insights."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a>Użyj usługi Stream Analytics tooprocess wyeksportowane dane z usługi Application Insights
[Usługa Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) jest idealne narzędzie hello przetwarzania danych [wyeksportowany z usługi Application Insights](app-insights-export-telemetry.md). Analiza strumienia może pobierają dane z różnych źródeł. Go przekształcić i filtrowanie danych hello, a następnie przesłać go tooa różnych sink.

W tym przykładzie utworzymy Adapter pobiera dane z usługi Application Insights, zmiana nazwy i przetwarza niektórych pól hello, która powoduje przekazanie w potoku go do usługi Power BI.

> [!WARNING]
> Są znacznie lepsze i łatwiejsze [zalecane sposoby toodisplay dane usługi Application Insights w usłudze Power BI](app-insights-export-power-bi.md). Witaj ścieżka przedstawione w tym miejscu jest po prostu tooillustrate przykład sposobu tooprocess eksportowania danych.
> 
> 

![Diagram blokowy eksportu za pośrednictwem SA tooPBI](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a>Tworzenie magazynu na platformie Azure
Eksport ciągły zawsze generuje konto magazynu Azure tooan danych, więc najpierw należy toocreate hello magazynu.

1. Utwórz konto magazynu "klasycznym" w ramach subskrypcji w hello [portalu Azure](https://portal.azure.com).
   
   ![W portalu Azure wybierz opcję Nowy, danych, magazynu](./media/app-insights-export-stream-analytics/030.png)
2. Tworzenie kontenera
   
    ![W hello nowego magazynu wybierz kontenery, kliknij Kafelek kontenery hello, a następnie dodaj](./media/app-insights-export-stream-analytics/040.png)
3. Skopiuj klucz dostępu do magazynu hello
   
    Będzie on potrzebny wkrótce tooset się usługa analiza strumienia wejściowego toohello hello.
   
    ![W magazynie hello Otwórz ustawienia kluczy i kopiować hello podstawowy klucz dostępu](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a>Uruchom magazynu tooAzure eksportu ciągłego
[Eksport ciągły](app-insights-export-telemetry.md) przenosi dane z usługi Application Insights do magazynu Azure.

1. W hello portalu Azure Przejdź zasobu usługi Application Insights toohello utworzone dla aplikacji.
   
    ![Kliknij przycisk Przeglądaj, usługi Application Insights aplikacji](./media/app-insights-export-stream-analytics/050.png)
2. Utwórz eksport ciągły.
   
    ![Wybierz ustawienia, Eksport ciągły](./media/app-insights-export-stream-analytics/060.png)

    Wybierz utworzone wcześniej konto magazynu hello:

    ![Ustaw miejsce docelowe hello eksportu](./media/app-insights-export-stream-analytics/070.png)

    Ustaw hello typy zdarzeń, które mają toosee:

    ![Wybierz typy zdarzeń](./media/app-insights-export-stream-analytics/080.png)

1. Let niektóre dane gromadzone. Zaczekaj i innym użytkownikom za pomocą aplikacji przez pewien czas. Dane telemetryczne wejdzie i zobaczysz statystyczne wykresów w [Eksploratora metryk](app-insights-metrics-explorer.md) i zdarzeń z [diagnostycznych wyszukiwania](app-insights-diagnostic-search.md). 
   
    I ponadto hello danych będzie eksportować tooyour magazynu. 
2. Sprawdź, czy hello wyeksportowane dane. W programie Visual Studio, wybierz **wyświetlić / w chmurze Explorer**i otwórz Azure / magazynu. (Jeśli nie mają tej opcji menu, należy tooinstall hello Azure SDK: Otwórz okno dialogowe Nowy projekt hello a Visual C# / w chmurze / Get Microsoft Azure SDK dla platformy .NET.)
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    Zanotuj hello wspólnej część nazwy ścieżki hello, która jest pochodną klucz nazwy i instrumentacji aplikacji hello. 

Witaj zdarzenia są zapisywane pliki tooblob w formacie JSON. Każdy plik może zawierać co najmniej jednego zdarzenia. Dlatego chcemy dane zdarzeń hello tooread i Filtruj limit pól hello, którą chcemy udostępnić. Wszystkie rodzaje czynności, które firma Microsoft może wykonywać hello danych, ale naszego planu obecnie jest toouse Stream Analytics toopipe hello danych tooPower BI.

## <a name="create-an-azure-stream-analytics-instance"></a>Utwórz wystąpienie usługi Azure Stream Analytics
Z hello [klasycznego portalu Azure](https://manage.windowsazure.com/), wybierz usługę Azure Stream Analytics hello i utworzyć nowe zadanie usługi Stream Analytics:

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

Podczas tworzenia nowego zadania hello rozwiń jego szczegóły:

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a>Ustawianie lokalizacji obiektu blob
Ustaw wprowadzania tootake z obiektu blob z eksportu ciągłego:

![](./media/app-insights-export-stream-analytics/120.png)

Teraz musisz hello podstawowy klucz dostępu z konta magazynu, który wcześniej zapisany. Ustaw jako hello klucz konta magazynu.

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a>Wzorzec prefiksu ścieżki zestawu
![](./media/app-insights-export-stream-analytics/140.png)

**Należy się tooset hello Format daty tooYYYY-MM-DD (z kreskami).**

Witaj wzorzec prefiksu ścieżki Określa, gdzie Stream Analytics znajduje plików wejściowych hello w magazynie hello. Należy tooset on toohow toocorrespond eksportu ciągłego przechowuje dane hello. Ustaw go następująco:

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

W tym przykładzie:

* `webapplication27`to nazwa hello hello zasobu usługi Application Insights **małe litery**.
* `1234...`jest klucz Instrumentacji hello hello zasobu usługi Application Insights **pominięcie łączniki**. 
* `PageViews`Witaj typ danych ma tooanalyze. dostępne typy Hello są zależne od filtru hello, ustawionych w eksportu ciągłego. Sprawdź hello wyeksportowane dane toosee hello innych dostępnych typów i zobacz hello [wyeksportować modelu danych](app-insights-export-data-model.md).
* `/{date}/{time}`wzorzec są zapisywane jako literału.

> [!NOTE]
> Sprawdź, czy hello magazynu toomake się, że ścieżka hello uzyskać prawo.
> 
> 

### <a name="finish-initial-setup"></a>Zakończ początkowej konfiguracji
Upewnij się, format serializacji hello:

![Potwierdź i zamknąć kreatora](./media/app-insights-export-stream-analytics/150.png)

Zamknij kreatora hello i poczekaj, aż hello toocomplete Instalatora.

> [!TIP]
> Użyj hello przykładowe polecenia toodownload niektórych danych. Zachowaj go jako toodebug próbki testu zapytania.
> 
> 

## <a name="set-hello-output"></a>Dane wyjściowe hello zestawu
Teraz wybierz zadanie i ustaw hello danych wyjściowych.

![Wybierz nowy kanał hello, kliknij pozycję dane wyjściowe, Dodaj usługi Power BI](./media/app-insights-export-stream-analytics/160.png)

Podaj Twojej **konto służbowe** tooauthorize tooaccess Stream Analytics zasobu usługi Power BI. Następnie magazynowa nazwę dla danych wyjściowych hello i hello docelowej usługi Power BI w zestawie danych i tabeli.

![Trzy nazwy magazynu](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a>Zestaw hello zapytania
Zapytanie Hello reguluje hello translację toooutput wejściowego.

![Wybierz zadanie hello, a następnie kliknij przycisk zapytanie. Wklej poniższy przykład hello.](./media/app-insights-export-stream-analytics/180.png)

Użyj toocheck funkcja testu hello uzyskanie hello prawo danych wyjściowych. Nadaj hello przykładowych danych, które miały ze strony danych wejściowych hello. 

### <a name="query-toodisplay-counts-of-events"></a>Zapytanie toodisplay liczby zdarzeń
Wklej tego zapytania:

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* dane wejściowe eksportu jest alias hello firma Microsoft udostępniła wejściowego strumienia toohello
* dane wyjściowe pbi jest alias wyjściowy hello zdefiniowanego
* Używamy [zewnętrzne GetElements ZASTOSOWAĆ](https://msdn.microsoft.com/library/azure/dn706229.aspx) ponieważ nazwa zdarzenia hello jest zagnieżdżony arrray JSON. Następnie wybierz opcję pobrania hello hello Nazwa zdarzenia, oraz liczbę hello liczbę wystąpień o tej nazwie w hello przedziale czasu. Witaj [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) klauzuli grupuje elementy hello w okresach czasu wynoszącym 1 minutę.

### <a name="query-toodisplay-metric-values"></a>Wartości metryk toodisplay kwerendy
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* Do czasu zdarzenia hello tooget hello metryki telemetrii i wartość metryki hello bardziej szczegółowy tego zapytania. wartości metryki Hello znajdują się wewnątrz tablicy, więc używamy hello zewnętrzne GetElements Zastosuj wzorzec tooextract hello wierszy. "myMetric" w tym przypadku jest nazwa hello hello metryki. 

### <a name="query-tooinclude-values-of-dimension-properties"></a>Zapytanie tooinclude wartości właściwości wymiaru
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* To zapytanie zawiera wartości właściwości wymiaru hello bez w zależności od określonego wymiaru w stałej indeksu hello wymiaru tablicy.

## <a name="run-hello-job"></a>Uruchom zadanie hello
Możesz wybrać datę w hello poza toostart hello zadania z. 

![Wybierz zadanie hello, a następnie kliknij przycisk zapytanie. Wklej poniższy przykład hello.](./media/app-insights-export-stream-analytics/190.png)

Poczekaj, aż zadanie hello jest uruchomione.

## <a name="see-results-in-power-bi"></a>Zobacz wyniki w usłudze Power BI
> [!WARNING]
> Są znacznie lepsze i łatwiejsze [zalecane sposoby toodisplay dane usługi Application Insights w usłudze Power BI](app-insights-export-power-bi.md). Witaj ścieżka przedstawione w tym miejscu jest po prostu tooillustrate przykład sposobu tooprocess eksportowania danych.
> 
> 

Otwórz usługę Power BI z służbowy konto służbowe i wybierz hello zestawu danych i tabeli, która jest zdefiniowana jako hello dane wyjściowe zadania usługi analiza strumienia hello.

![W usłudze Power BI wybierz pola i zestawu danych.](./media/app-insights-export-stream-analytics/200.png)

Teraz można używać tego zestawu danych, raportów i pulpitów nawigacyjnych w [usługi Power BI](https://powerbi.microsoft.com).

![W usłudze Power BI wybierz pola i zestawu danych.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a>Brak danych?
* Sprawdź, że [format daty hello zestaw](#set-path-prefix-pattern) poprawnie tooYYYY-MM-DD (z kreskami).

## <a name="video"></a>Połączenia wideo
Noam Ben Zeev pokazuje, jak tooprocess wyeksportowane dane przy użyciu usługi Stream Analytics.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a>Następne kroki
* [Eksport ciągły](app-insights-export-telemetry.md)
* [Szczegółowe dane modelu odwołania dla hello typy właściwości i wartości.](app-insights-export-data-model.md)
* [Usługa Application Insights](app-insights-overview.md)

