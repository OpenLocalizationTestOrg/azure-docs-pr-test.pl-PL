---
title: "Przepływność tooincrease zadania usługi analiza strumienia aaaScale | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zadania usługi analiza strumienia tooscale Konfigurowanie partycji wejściowych, dostrajanie hello definicji zapytania i ustawiając zadania jednostki przesyłania strumieniowego."
keywords: "przesyłanie strumieniowe, danych przesyłania strumieniowego przetwarzania danych, dostroić analityka"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a>Skalowanie usługi Azure Stream Analytics zadania tooincrease strumienia przetwarzania danych przepływności
W tym artykule opisano, jak tootune Stream Analytics zapytania tooincrease przepływność dla zadań przesyłania strumieniowego usługi Analytics. Dowiedz się, jak tooscale analiza strumienia zadania przez skonfigurowanie wejściowych partycji, dostrajania analytics hello zapytania definicji i obliczanie i ustawiania zadania *jednostki przesyłania strumieniowego* (SUs). 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a>Co to są hello części zadanie usługi Stream Analytics?
Definicji zadania Stream Analytics zawiera dane wejściowe, zapytań i danych wyjściowych. Dane wejściowe są, gdzie hello zadania odczytuje hello strumień danych. Hello zapytania jest strumienia danych wejściowych hello tootransform używane, a dane wyjściowe hello jest gdzie zadanie hello wysyła hello wyniki zadania do.  

Zadanie wymaga co najmniej jedno źródło danych wejściowych do strumieniowego przesyłania danych. Witaj źródło wejścia strumienia danych mogą być przechowywane w Centrum zdarzeń platformy Azure lub w magazynie obiektów blob Azure. Aby uzyskać więcej informacji, zobacz [tooAzure wprowadzenie Stream Analytics](stream-analytics-introduction.md) i [rozpocząć korzystanie z usługi Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).

## <a name="partitions-in-event-hubs-and-azure-storage"></a>Partycje w centra zdarzeń i magazynu systemu Azure
Skalowanie zadania Stream Analytics korzysta z partycji w hello wejściowych lub wyjściowych. Partycjonowanie umożliwia dzielenia danych na podzestawy oparte na kluczu partycji. Proces, który używa danych hello (na przykład zadanie analizy przesyłania strumieniowego) może wykorzystywać i zapisać różnych partycji równolegle, co zwiększa przepustowość. Podczas pracy z analizy przesyłania strumieniowego, możesz korzystać z partycjonowania usługi event hubs i w magazynie obiektów Blob. 

Aby uzyskać więcej informacji o partycjach zobacz następujące artykuły hello:

* [Omówienie funkcji usługi Event Hubs](../event-hubs/event-hubs-features.md#partitions)
* [Partycjonowanie danych](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>Jednostki przesyłania strumieniowego (SUs)
Przesyłanie strumieniowe jednostki (SUs) reprezentuje hello zasobów i przetwarzania danych zasilania, które są wymagane w kolejności tooexecute zadanie usługi analiza strumienia Azure. Usługi SUs zapewniają sposób toodescribe hello względną przetwarzania zdarzeń pojemności oparte na mieszanych pomiarach Procesora, pamięci, Odczyt i zapis stawki. Każdy SU odpowiada tooroughly 1 MB/s przepustowości. 

Wybranie liczby SUs są wymagane dla określonego zadania zależy od hello konfiguracji partycji dla danych wejściowych hello kwerendy hello zdefiniowanej dla hello zadania. Możesz wybrać zapasowej przydziału tooyour w SUs dla zadania. Domyślnie każdej subskrypcji platformy Azure ma przydziału zapasowej SUs too50 dla wszystkich zadań analizy hello w określonym regionie. tooincrease SUs dla subskrypcji przekracza ten limit przydziału, skontaktuj się z [Microsoft Support](http://support.microsoft.com). Prawidłowe wartości SUs na zadanie to 1, 3, 6 oraz w przyrostach 6.

## <a name="embarrassingly-parallel-jobs"></a>Embarrassingly równoległych zadań
*Embarrassingly równoległych* zadania jest scenariusz najbardziej skalowalny hello mamy w Azure Stream Analytics. Łączy jedną partycję hello wejściowych tooone wystąpienia partycji tooone kwerendy hello hello danych wyjściowych. Równoległość ten ma hello następujące wymagania:

1. Logika zapytania jest zależna od hello klucza przetwarzanych przez hello sam kwerendy wystąpienia, należy upewnić się, że zdarzenia hello Przejdź toohello tej samej partycji dane wejściowe. Usługi event hubs, oznacza to, że hello zdarzeń danych muszą mieć hello **PartitionKey** zestawu wartości. Alternatywnie można użyć nadawców podzielonym na partycje. W przypadku magazynu obiektów blob, oznacza to, że hello zdarzenia są wysyłane toohello tego samego folderu partycji. Logiki kwerendy nie wymaga hello klucza toobe przetworzone przez hello sam kwerendy wystąpienia, możesz zignorować to wymaganie. Przykładem tego logiki może być prostego zapytania wybierz projekt filtru.  

2. Po danych hello jest rozmieszczona na powitania strony wejściowej, to należy się upewnić, że zapytanie jest podzielona na partycje. Wymaga to toouse **Partition By** wszystkie kroki hello w. Wiele kroków są dozwolone, ale wszystkie muszą partycjonowanego hello tego samego klucza. Obecnie hello klucz partycjonowania musi ustawić także**PartitionId** aby toobe zadania hello pełni równoległych.  

3. Obecnie tylko centra zdarzeń i magazynu obiektów blob obsługują partycjonowanej danych wyjściowych. W przypadku danych wyjściowych Centrum zdarzeń, należy skonfigurować toobe klucza partycji hello **PartitionId**. Dla danych wyjściowych z magazynu obiektów blob nie masz toodo żadnych czynności.  

4. Hello liczby partycji wejściowy musi być równa hello liczby partycji danych wyjściowych. Dane wyjściowe z magazynu obiektów blob nie obsługuje obecnie partycji. Ale nie szkodzi, ponieważ dziedziczy on hello schemat nadrzędny zapytania hello partycji. Poniżej przedstawiono przykładowe wartości partycji, umożliwiających pełni równoległe zadania:  

   * 8 partycje wejściowych Centrum zdarzeń i Centrum zdarzeń 8 output partycji
   * 8 partycje wejściowych Centrum zdarzeń i danych wyjściowych z magazynu obiektów blob  
   * 8 partycje wejściowych magazynu obiektów blob i dane wyjściowe z magazynu obiektów blob  
   * 8 obiektu blob magazynu wejściowego partycji i 8 partycje danych wyjściowych Centrum zdarzeń  

Witaj poniższych sekcjach omówiono niektóre przykładowe scenariusze, które są embarrassingly równoległe.

### <a name="simple-query"></a>Prostego zapytania

* Wejście: Centrum zdarzeń z partycjami 8
* Dane wyjściowe: Centrum zdarzeń z partycjami 8

Zapytanie:

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

To zapytanie jest proste filtru. W związku z tym nie należy tooworry o partycjonowaniu hello danych wejściowych, który jest wysyłany toohello Centrum zdarzeń. Zwróć uwagę, zawiera zapytania hello **partycji przez PartitionId**, więc jego spełnia wymagania #2 z wcześniej. Dla danych wyjściowych hello, potrzebujemy danych wyjściowych Centrum zdarzeń hello tooconfigure hello zadania toohave hello partycjonowania klucza zestawu, zbyt**PartitionId**. Jeden ostatni test jest toomake się, że hello liczby partycji wejściowy jest równy toohello liczby partycji danych wyjściowych.

### <a name="query-with-a-grouping-key"></a>Zapytanie z kluczem grupowania

* Wejście: Centrum zdarzeń z partycjami 8
* Danych wyjściowych: Magazyn obiektów Blob

Zapytanie:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Ta kwerenda zawiera klucz grupowania. Witaj w związku z tym samym toobe klucza potrzeb przetworzonych przez program hello takie same zapytanie wystąpienia, co oznacza, że zdarzenia musi być wysyłane toohello Centrum zdarzeń w sposób podzielonym na partycje. Ale klucz, do którego należy używać? **PartitionId** to pojęcie logiczne zadania. klucz Hello faktycznie Szanujemy jest **TollBoothId**, więc hello **PartitionKey** musi mieć wartość dane zdarzeń hello **TollBoothId**. Firma Microsoft to zrobić w zapytaniu hello przez ustawienie **Partition By** za**PartitionId**. Ponieważ dane wyjściowe hello jest magazyn obiektów blob, nie musisz tooworry o konfigurowaniu wartość klucza partycji, zgodnie z harmonogramem wymaganie #4.

### <a name="multi-step-query-with-a-grouping-key"></a>Zapytanie wieloetapowych kluczem grupowania
* Wejście: Centrum zdarzeń z partycjami 8
* Dane wyjściowe: Wystąpienie koncentratora zdarzeń z partycjami 8

Zapytanie:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Ta kwerenda zawiera klucz grupowania, więc hello tego samego toobe klucza potrzeb przetworzonych przez program hello tego samego wystąpienia zapytania. Możemy użyć tej samej strategii jak w poprzednim przykładzie hello hello. W takim przypadku hello zapytania ma wiele kroków. Ma każdego kroku **partycji przez PartitionId**? Tak więc zapytania hello spełnia wymagania #3. Dla danych wyjściowych hello, potrzebujemy klucza partycji hello tooset, zbyt**PartitionId**, zgodnie z wcześniejszym opisem. Można zobaczyć, czy ma ona hello tej samej liczby partycji jako dane wejściowe hello.

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>Przykładowe scenariusze, które są *nie* embarrassingly równoległych

W poprzedniej sekcji hello możemy pokazano kilka scenariuszy embarrassingly równoległych. W tej sekcji omówiono scenariusze, które nie spełniają wszystkie hello wymagania toobe embarrassingly równoległych. 

### <a name="mismatched-partition-count"></a>Liczba partycji niezgodne
* Wejście: Centrum zdarzeń z partycjami 8
* Dane wyjściowe: Centrum zdarzeń z partycjami 32

W takim przypadku nie ma znaczenia, jakie zapytanie hello jest. Jeśli liczba partycji wejściowych hello nie odpowiada liczba partycji hello danych wyjściowych, topologii hello nie jest embarrassingly równoległych.

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a>Nie używa usługi event hubs lub magazynu obiektów blob jako dane wyjściowe
* Wejście: Centrum zdarzeń z partycjami 8
* Dane wyjściowe: usługi Power BI

Wyjście usługi Power BI aktualnie nie obsługuje partycjonowanie. Dlatego w tym scenariuszu nie jest embarrassingly równoległych.

### <a name="multi-step-query-with-different-partition-by-values"></a>Zapytanie wieloetapowych o różnych wartościach Partition By
* Wejście: Centrum zdarzeń z partycjami 8
* Dane wyjściowe: Centrum zdarzeń z partycjami 8

Zapytanie:

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Jak widać, drugi etap hello używa **TollBoothId** jako hello klucz partycjonowania. Ten krok jest hello sam nie jako pierwsze hello i dlatego wymaga nam toodo losowa. 

Witaj poprzednich przykładach niektóre zadania usługi analiza strumienia, które są zbyt (lub nie) embarrassingly równoległych topologii. Jeśli są one zgodne, mają możliwość hello maksymalną skalę. Aktualizacje dla zadania, które nie pasują do jednego z tych profilów skalowania wskazówki będą dostępne w przyszłości. Na razie użyj hello ogólne wskazówki w hello następujące sekcje.

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a>Oblicz maksymalną liczbę jednostek przesyłania strumieniowego hello zadania
Hello całkowita liczba jednostek przesyłania strumieniowego, które mogą być używane przez zadanie usługi Stream Analytics zależy od hello liczbę kroków w zapytaniu hello zdefiniowane dla zadania hello i hello liczby partycji dla każdego kroku.

### <a name="steps-in-a-query"></a>Kroki w kwerendzie
Kwerenda może mieć jeden lub wiele kroków. Każdy krok jest zdefiniowane przez hello podzapytania **WITH** — słowo kluczowe. Hello kwerendę, która znajduje się poza hello **WITH** — słowo kluczowe (tylko w jednej kwerendzie) również jest traktowane jako krok, takich jak hello **wybierz** instrukcji w hello następujące zapytania:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

Ta kwerenda zawiera dwa kroki.

> [!NOTE]
> To zapytanie jest omówiona bardziej szczegółowo w dalszej części artykułu hello.
>  

### <a name="partition-a-step"></a>Krok partycji
Partycjonowanie krok wymaga hello następujące warunki:

* musi być dzielony na partycje Hello źródło danych wejściowych. 
* Witaj **wybierz** instrukcji kwerendy hello musi odczytywać partycjonowanej źródło danych wejściowych.
* Zapytanie Hello w ramach kroku hello musi mieć hello **Partition By** — słowo kluczowe.

Gdy zapytanie jest podzielona na partycje, zdarzenia wejściowe hello są przetwarzane i zagregowane w oddzielnej partycji grupy, a dane wyjściowe zdarzenia są generowane dla poszczególnych grup hello. Jeśli chcesz połączonych Agregacja należy utworzyć drugi tooaggregate niepartycjonowany kroku.

### <a name="calculate-hello-max-streaming-units-for-a-job"></a>Oblicz max hello jednostki zadania przesyłania strumieniowego
Wszystkie kroki niepartycjonowany razem można skalować toosix jednostki (SUs) dla zadania usługi analiza strumienia przesyłania strumieniowego. musi być dzielony na partycje SUs tooadd, krok. Każda partycja może mieć sześć SUs.

<table border="1">
<tr><th>Zapytanie</th><th>Maksymalna liczba SUs hello zadania</th></td>

<tr><td>
<ul>
<li>Zapytanie Hello zawiera jeden krok.</li>
<li>Witaj krok nie jest podzielona na partycje.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>strumień danych wejściowych Hello jest podzielona na partycje przez 3.</li>
<li>Zapytanie Hello zawiera jeden krok.</li>
<li>krok Hello jest podzielona na partycje.</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>Zapytanie Hello zawiera dwa kroki.</li>
<li>Żadne czynności hello jest podzielona na partycje.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>strumień danych wejściowych Hello jest podzielona na partycje przez 3.</li>
<li>Zapytanie Hello zawiera dwa kroki. wejściowych kroku Hello jest podzielona na partycje, a drugi etap hello nie.</li>
<li>Witaj <strong>wybierz</strong> instrukcji odczytuje z danych wejściowych hello podzielona na partycje.</li>
</ul>
</td>
<td>24 (18 partycjonowanej kroki) + 6 niepartycjonowany czynności</td></tr>
</table>

### <a name="examples-of-scaling"></a>Przykłady skalowania

Witaj następujące zapytanie oblicza hello liczba samochodów w ramach pośrednictwa stacji przez, który ma trzy tollbooths okna trzy minuty. To zapytanie może być skalowana w górę toosix SUs.

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

toouse więcej SUs dla hello zapytania, zarówno hello strumienia danych wejściowych i musi być dzielony na partycje hello zapytania. Ponieważ partycja strumienia danych hello jest ustawiona too3, hello następujące zmodyfikowanej zapytanie umożliwia skalowanie too18 SUs:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Zapytanie jest podzielona na partycje, zdarzenia wejściowe hello są przetwarzane i zagregowane w oddzielnej partycji grup. Dane wyjściowe zdarzenia są także generowane dla poszczególnych grup hello. Partycjonowanie może powodować pewne nieoczekiwane wyniki hello **GROUP BY** pole nie jest kluczem partycji hello w strumieniu danych wejściowych hello. Na przykład Witaj **TollBoothId** pole w hello poprzednie zapytanie nie jest klucz partycji hello **Input1**. wynik Hello jest hello, że dane z budki #1 mogą rozprzestrzeniać się, w wielu partycji.

Każdy z hello **Input1** partycje będą przetwarzane oddzielnie przez Stream Analytics. W związku z tym wiele rekordów liczby hello samochodu hello tego samego budki w powitalne okno wirowania tego samego zostanie utworzony. Jeśli nie można zmienić klucza partycji wejściowych hello, można naprawić ten problem, dodając krok-partition, tak jak hello poniższy przykład:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

To zapytanie może być skalowana too24 SUs.

> [!NOTE]
> Jeśli są Sprzęganie dwóch strumieni, upewnij się, że strumienie hello są podzielone na partycje według klucza partycji hello kolumny hello użycie toocreate hello sprzężenia. Upewnij się, że masz hello również tej samej liczby partycji w obu strumieni.
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>Konfigurowanie usługi Stream Analytics jednostki przesyłania strumieniowego

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Hello listy zasobów Znajdź zadanie usługi Stream Analytics hello mają tooscale, a następnie otwórz go.
3. W hello zadania bloku, w obszarze **Konfiguruj**, kliknij przycisk **skali**.

    ![Konfiguracja zadania usługi analiza strumienia portalu Azure][img.stream.analytics.preview.portal.settings.scale]

4. Użyj hello suwaka tooset hello SUs hello zadania. Zwróć uwagę, czy ustawienia SU toospecific ograniczone.


## <a name="monitor-job-performance"></a>Monitor wydajności zadania
Witaj portalu Azure można śledzić przepływności hello zadania:

![Azure Stream Analytics monitorowanie zadań][img.stream.analytics.monitor.job]

Oblicz przepływności hello oczekiwano hello obciążenia. Przepływności hello jest mniejsza niż oczekiwano, dostroić hello wejściowych partycji, dostroić hello zapytania i dodać SUs tooyour zadania.


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a>Wizualizuj Stream Analytics przepustowość na dużą skalę: hello Pi malina scenariusza
toohelp zrozumieć, jak skalować zadania usługi analiza strumienia, wykonane eksperyment na podstawie danych wprowadzonych z urządzenia malina Pi. Tego eksperymentu poinformować nas, zobacz hello wpływu na przepustowość wiele jednostek przesyłania strumieniowego i partycje.

W tym scenariuszu urządzenie hello wysyła czujnik danych (klienci) tooan zdarzenia koncentratora. Przesyłanie strumieniowe Analytics przetwarza dane hello i wysyła alert ani w statystyce jako Centrum zdarzeń tooanother danych wyjściowych. 

powitania klienta wysyła dane czujników w formacie JSON. Witaj danych wyjściowych jest również w formacie JSON. dane Hello wygląda następująco:

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

Hello następującego zapytania jest używana toosend alert po wyłączeniu światło:

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>Miara przepływności

W tym kontekście przepływność wynosi hello ilość danych wejściowych przetworzone przez usługę Stream Analytics w stałej ilości czasu. (Firma Microsoft mierzy przez 10 minut.) dane wejściowe tooachieve hello najlepsze przetwarzania przepływności hello, zarówno dane hello strumienia danych wejściowych i zapytania hello zostały podzielone na partycje. Jest dostępna **COUNT()** w toomeasure zapytania hello przetworzono ile zdarzenia wejściowe. czy zadania hello toomake nie oczekiwał po prostu dla zdarzenia wejściowe toocome, każdej partycji Centrum zdarzeń wejściowych hello są załadowane z około 300 MB danych wejściowych.

Witaj poniższej tabeli przedstawiono wyniki hello, którą widzieliśmy, gdy firma Microsoft zwiększyć hello liczbę jednostek przesyłania strumieniowego i odpowiadająca mu partycja hello liczby w usługi event hubs.  

<table border="1">
<tr><th>Partycje wejściowych</th><th>Partycje danych wyjściowych</th><th>Jednostki przesyłania strumieniowego</th><th>Długoterminowa przepustowość
</th></td>

<tr><td>12</td>
<td>12</td>
<td>6</td>
<td>4.06 MB/s</td>
</tr>

<tr><td>12</td>
<td>12</td>
<td>12</td>
<td>8.06 MB/s</td>
</tr>

<tr><td>48</td>
<td>48</td>
<td>48</td>
<td>38.32 MB/s</td>
</tr>

<tr><td>192</td>
<td>192</td>
<td>192</td>
<td>172.67 MB/s</td>
</tr>

<tr><td>480</td>
<td>480</td>
<td>480</td>
<td>454.27 MB/s</td>
</tr>

<tr><td>720</td>
<td>720</td>
<td>720</td>
<td>609.69 MB/s</td>
</tr>
</table>

I hello Wykres ukazuje wizualizacji hello relacji między usługami SUs i przepływności.

![img.stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

