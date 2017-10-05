---
title: "Skalowanie zadania usługi analiza strumienia w celu zwiększenia przepływności | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skalować zadania usługi analiza strumienia Konfigurowanie partycji wejściowych, dostosowywanie definicji zapytania i ustawiając zadania jednostki przesyłania strumieniowego."
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
ms.openlocfilehash: ab894976c72ea3785d7f58e51b3dd64511e1e8e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="scale-azure-stream-analytics-jobs-to-increase-stream-data-processing-throughput"></a>Skalowanie zadania usługi analiza strumienia Azure w celu zwiększenia przepływności przetwarzania danych strumienia
W tym artykule przedstawiono sposób dostrajania Stream Analytics zapytanie w celu zwiększenia przepływności zadań przesyłania strumieniowego usługi Analytics. Dowiesz się, jak skalowanie zadania usługi analiza strumienia przez konfigurowanie partycji wejściowych, dostosowywanie definicji zapytania analytics i obliczanie i ustawiania zadania *jednostki przesyłania strumieniowego* (SUs). 

## <a name="what-are-the-parts-of-a-stream-analytics-job"></a>Co to są elementy zadania Stream Analytics?
Definicji zadania Stream Analytics zawiera dane wejściowe, zapytań i danych wyjściowych. Dane wejściowe są, gdy zadanie odczytuje strumienia danych z. Zapytanie jest używany do transformacji strumienia danych wejściowych, a dane wyjściowe są, gdy zadanie wysyła wyników zadania do.  

Zadanie wymaga co najmniej jedno źródło danych wejściowych do strumieniowego przesyłania danych. Źródło dla wejścia strumienia danych mogą być przechowywane w Centrum zdarzeń platformy Azure lub w magazynie obiektów blob Azure. Aby uzyskać więcej informacji, zobacz [wprowadzenie do usługi Azure Stream Analytics](stream-analytics-introduction.md) i [rozpocząć korzystanie z usługi Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).

## <a name="partitions-in-event-hubs-and-azure-storage"></a>Partycje w centra zdarzeń i magazynu systemu Azure
Skalowanie zadania Stream Analytics korzysta z partycjami w danych wejściowych lub wyjściowych. Partycjonowanie umożliwia dzielenia danych na podzestawy oparte na kluczu partycji. Proces, który używa danych (na przykład zadanie analizy przesyłania strumieniowego) może wykorzystywać i zapisać różnych partycji równolegle, co zwiększa przepustowość. Podczas pracy z analizy przesyłania strumieniowego, możesz korzystać z partycjonowania usługi event hubs i w magazynie obiektów Blob. 

Aby uzyskać więcej informacji o partycjach zobacz następujące artykuły:

* [Omówienie funkcji usługi Event Hubs](../event-hubs/event-hubs-features.md#partitions)
* [Partycjonowanie danych](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>Jednostki przesyłania strumieniowego (SUs)
Jednostki przesyłania strumieniowego (SUs) reprezentuje zasobów i mocy obliczeniowej, które są wymagane w celu wykonania zadanie usługi analiza strumienia Azure. Jednostki przesyłania strumieniowego to sposób opisywania względnych możliwości obliczeniowych dotyczących przetwarzania na podstawie mieszanego pomiaru wydajności procesora CPU, pamięci i operacji odczytu oraz zapisu. Każdy SU odpowiada około 1 MB/s przepustowości. 

Wybranie liczby SUs są wymagane dla określonego zadania zależy od konfiguracji partycji dla danych wejściowych oraz zapytania zdefiniowanych dla tego zadania. Można wybrać do limitu przydziału w SUs dla zadania. Domyślnie każdej subskrypcji platformy Azure ma limit przydziału wynoszący maksymalnie 50 SUs dla wszystkich zadań analityka w określonym regionie. Aby zwiększyć SUs dla Twojej subskrypcji po przekroczeniu tego przydziału, skontaktuj się z [Microsoft Support](http://support.microsoft.com). Prawidłowe wartości SUs na zadanie to 1, 3, 6 oraz w przyrostach 6.

## <a name="embarrassingly-parallel-jobs"></a>Embarrassingly równoległych zadań
*Embarrassingly równoległych* zadanie jest najbardziej skalowalny scenariusza mamy w Azure Stream Analytics. Jedna partycja danych wejściowych do jednego wystąpienia zapytania łączy się jedną partycję w danych wyjściowych. Równoległość ten ma następujące wymagania:

1. Logika zapytania zależy od tego samego klucza przetwarzanych przez to samo wystąpienie zapytania, należy się upewnić, że zdarzenia przejdź do tej samej partycji dane wejściowe. Usługi event hubs, oznacza to, że dane zdarzeń muszą mieć **PartitionKey** zestawu wartości. Alternatywnie można użyć nadawców podzielonym na partycje. W przypadku magazynu obiektów blob oznacza to, że zdarzenia są wysyłane do tego samego folderu partycji. Jeśli logika zapytania nie wymaga tego samego klucza do przetworzenia przez to samo wystąpienie zapytania, możesz zignorować to wymaganie. Przykładem tego logiki może być prostego zapytania wybierz projekt filtru.  

2. Po danych jest rozmieszczona na stronie wprowadzania, to należy się upewnić, że zapytanie jest podzielona na partycje. Wymaga to użycia **Partition By** wszystkich kroków. Wiele kroków są dozwolone, ale wszystkie muszą podzielone na partycje przy użyciu tego samego klucza. Obecnie, podziału klucza musi być ustawiona na **PartitionId** aby pełni równoległe zadania.  

3. Obecnie tylko centra zdarzeń i magazynu obiektów blob obsługują partycjonowanej danych wyjściowych. W przypadku danych wyjściowych Centrum zdarzeń, należy skonfigurować klucz partycji, który ma być **PartitionId**. Dla danych wyjściowych z magazynu obiektów blob nie trzeba wykonywać żadnych czynności.  

4. Liczby partycji wejściowych musi być równa liczbie partycji danych wyjściowych. Dane wyjściowe z magazynu obiektów blob nie obsługuje obecnie partycji. Ale nie szkodzi, ponieważ dziedziczy ona schemat partycjonowania nadrzędnego zapytania. Poniżej przedstawiono przykładowe wartości partycji, umożliwiających pełni równoległe zadania:  

   * 8 partycje wejściowych Centrum zdarzeń i Centrum zdarzeń 8 output partycji
   * 8 partycje wejściowych Centrum zdarzeń i danych wyjściowych z magazynu obiektów blob  
   * 8 partycje wejściowych magazynu obiektów blob i dane wyjściowe z magazynu obiektów blob  
   * 8 obiektu blob magazynu wejściowego partycji i 8 partycje danych wyjściowych Centrum zdarzeń  

W poniższych sekcjach omówiono niektóre przykładowe scenariusze, które są embarrassingly równoległe.

### <a name="simple-query"></a>Prostego zapytania

* Wejście: Centrum zdarzeń z partycjami 8
* Dane wyjściowe: Centrum zdarzeń z partycjami 8

Zapytanie:

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

To zapytanie jest proste filtru. W związku z tym firma Microsoft nie trzeba martwić partycjonowanie danych wejściowych, który jest wysyłany do Centrum zdarzeń. Należy zauważyć, że kwerenda zawiera **partycji przez PartitionId**, więc jego spełnia wymagania #2 z wcześniej. Dla danych wyjściowych, należy skonfigurować zadania zawiera zestaw klucza partycjonowania do danych wyjściowych Centrum zdarzeń **PartitionId**. Jeden ostatni test jest upewnij się, że liczba partycji wejściowy jest równa liczbie partycji danych wyjściowych.

### <a name="query-with-a-grouping-key"></a>Zapytanie z kluczem grupowania

* Wejście: Centrum zdarzeń z partycjami 8
* Danych wyjściowych: Magazyn obiektów Blob

Zapytanie:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Ta kwerenda zawiera klucz grupowania. W związku z tym samym kluczem musi być przetwarzane przez to samo wystąpienie kwerendy, co oznacza, że zdarzenia musi być wysyłane do Centrum zdarzeń w sposób podzielonym na partycje. Ale klucz, do którego należy używać? **PartitionId** to pojęcie logiczne zadania. Klucz faktycznie Szanujemy jest **TollBoothId**, więc **PartitionKey** musi mieć wartość dane zdarzenia **TollBoothId**. Firma Microsoft to zrobić w zapytaniu przez ustawienie **Partition By** do **PartitionId**. Ponieważ dane wyjściowe magazynu obiektów blob, firma Microsoft nie trzeba martwić się o konfigurowaniu wartość klucza partycji, zgodnie z harmonogramem wymaganie #4.

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

Ta kwerenda zawiera klucz grupowania, więc ten sam klucz musi być przetwarzane przez to samo wystąpienie zapytania. Możemy użyć tej samej strategii co w poprzednim przykładzie. W takim przypadku zapytanie ma wiele kroków. Ma każdego kroku **partycji przez PartitionId**? Tak, aby zapytanie spełnia wymagania #3. Dla danych wyjściowych, należy ustawić klucz partycji **PartitionId**, zgodnie z wcześniejszym opisem. Można zobaczyć, że ma taką samą liczbę partycji jako dane wejściowe.

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>Przykładowe scenariusze, które są *nie* embarrassingly równoległych

W poprzedniej sekcji możemy pokazano kilka scenariuszy embarrassingly równoległych. W tej sekcji omówiono scenariusze, które nie spełniają wszystkie wymagania dotyczące być embarrassingly równoległe. 

### <a name="mismatched-partition-count"></a>Liczba partycji niezgodne
* Wejście: Centrum zdarzeń z partycjami 8
* Dane wyjściowe: Centrum zdarzeń z partycjami 32

W takim przypadku nie ma znaczenia, zapytanie jest. Jeśli liczba partycji wejściowych nie odpowiada liczba partycji danych wyjściowych, topologia nie jest embarrassingly równoległych.

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

Jak widać, drugi etap używa **TollBoothId** jako klucza partycji. Ten krok nie jest taka sama, co w pierwszym kroku i dlatego wymaga do zrobienia losowa. 

W poprzednich przykładach pokazano, niektóre zadania Stream Analytics, które odpowiadają (lub nie) embarrassingly równoległych topologii. Jeśli są one zgodne, mają one potencjalnie maksymalną skalę. Aktualizacje dla zadania, które nie pasują do jednego z tych profilów skalowania wskazówki będą dostępne w przyszłości. Na razie użyj ogólne wskazówki w poniższych sekcjach.

## <a name="calculate-the-maximum-streaming-units-of-a-job"></a>Oblicz maksymalną jednostki zadania przesyłania strumieniowego
Całkowita liczba jednostek przesyłania strumieniowego, które mogą być używane przez zadanie usługi Stream Analytics zależy od liczby kroków w zapytaniu zdefiniowane dla zadania i liczby partycji dla każdego kroku.

### <a name="steps-in-a-query"></a>Kroki w kwerendzie
Kwerenda może mieć jeden lub wiele kroków. Każdy krok jest zdefiniowane przez podzapytania **WITH** — słowo kluczowe. Zapytanie, które znajduje się poza **WITH** — słowo kluczowe (tylko w jednej kwerendzie) również będzie traktowany jako krok, na przykład **wybierz** instrukcji w następującym zapytaniu:

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
> To zapytanie jest omówiona bardziej szczegółowo w dalszej części tego artykułu.
>  

### <a name="partition-a-step"></a>Krok partycji
Partycjonowanie krok wymaga spełnienia następujących warunków:

* Źródło danych wejściowych musi być partycjonowane. 
* **Wybierz** instrukcji zapytania musi odczytywać partycjonowanej źródło danych wejściowych.
* Zapytanie w ramach kroku musi mieć **Partition By** — słowo kluczowe.

Jeśli zapytanie jest podzielona na partycje, zdarzenia wejściowe są przetwarzane i zagregowane w oddzielnej partycji grupy, a dane wyjściowe zdarzenia są generowane dla poszczególnych grup. Jeśli chcesz połączonych agregacja, należy utworzyć drugi etap niepartycjonowany do zagregowania.

### <a name="calculate-the-max-streaming-units-for-a-job"></a>Obliczenia maksymalnej liczby jednostek w zadaniu przesyłania strumieniowego
Wszystkie kroki niepartycjonowany razem można skalować do sześciu jednostki przesyłania strumieniowego (SUs) dla zadania usługi analiza strumienia. Aby dodać SUs, musi być dzielony na partycje kroku. Każda partycja może mieć sześć SUs.

<table border="1">
<tr><th>Zapytanie</th><th>Maksymalna liczba SUs zadania</th></td>

<tr><td>
<ul>
<li>Zapytanie zawiera w jednym kroku.</li>
<li>Krok nie jest podzielona na partycje.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>Strumień danych wejściowych jest podzielona na partycje przez 3.</li>
<li>Zapytanie zawiera w jednym kroku.</li>
<li>Krok jest podzielona na partycje.</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>Zapytanie zawiera dwa kroki.</li>
<li>Żadne kroki są podzielone na partycje.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>Strumień danych wejściowych jest podzielona na partycje przez 3.</li>
<li>Zapytanie zawiera dwa kroki. Wejściowych kroku jest podzielona na partycje, a drugi etap nie.</li>
<li><strong>Wybierz</strong> instrukcji odczytuje z podzielonym na partycje danych wejściowych.</li>
</ul>
</td>
<td>24 (18 partycjonowanej kroki) + 6 niepartycjonowany czynności</td></tr>
</table>

### <a name="examples-of-scaling"></a>Przykłady skalowania

Następujące zapytanie oblicza liczbę samochodów w ramach pośrednictwa stacji przez, który ma trzy tollbooths okna trzy minuty. To zapytanie może być skalowana maksymalnie sześć SUs.

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Aby użyć więcej SUs dla zapytania, musi być podzielony zarówno strumienia danych wejściowych, jak i zapytania. Ponieważ partycji strumień danych jest ustawiona na 3, następujące zmodyfikowanej zapytania mogą być skalowane maksymalnie 18 SUs:

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Zapytanie jest podzielona na partycje, zdarzenia wejściowe są przetwarzane i zagregowane w oddzielnej partycji grup. Dane wyjściowe zdarzenia są także generowane dla poszczególnych grup. Partycjonowanie może powodować pewne nieoczekiwane wyniki podczas **GROUP BY** pole nie jest częścią klucza partycji w strumieniu danych wejściowych. Na przykład **TollBoothId** pole w poprzednich zapytań nie jest klucz partycji **Input1**. Wynik jest, że dane z budki #1 może rozprzestrzeniać się w wielu partycji.

Każdy z **Input1** partycje będą przetwarzane oddzielnie przez Stream Analytics. W związku z tym wiele rekordów liczba samochodów dla tego samego budki w tym samym oknie wirowania zostanie utworzony. Jeśli nie można zmienić klucza partycji wejściowych, można naprawić ten problem, dodając krok z systemem innym niż partycji, jak w poniższym przykładzie:

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

To zapytanie może być skalowana do 24 SUs.

> [!NOTE]
> Jeśli są Sprzęganie dwóch strumieni, upewnij się, że strumienie są dzielone przez klucz partycji kolumny, która służy do tworzenia sprzężenia. Upewnij się również mieć taką samą liczbę partycji w obu strumieni.
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>Konfigurowanie usługi Stream Analytics jednostki przesyłania strumieniowego

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
2. Na liście zasobów można znaleźć zadania usługi analiza strumienia, który chcesz skalować, a następnie otwórz go.
3. W bloku zadania w obszarze **Konfiguruj**, kliknij przycisk **skali**.

    ![Konfiguracja zadania usługi analiza strumienia portalu Azure][img.stream.analytics.preview.portal.settings.scale]

4. Aby ustawić SUs zadania za pomocą suwaka. Zwróć uwagę, że jest ograniczona do określonych ustawień SU.


## <a name="monitor-job-performance"></a>Monitor wydajności zadania
Przy użyciu portalu Azure, można śledzić przepływności zadania:

![Azure Stream Analytics monitorowanie zadań][img.stream.analytics.monitor.job]

Oblicz przepływność oczekiwanego obciążenia. Jeśli przepustowość jest mniejsza niż oczekiwano, dostroić wejściowych partycji, ulepszenia zapytania i dodać SUs do zadania.


## <a name="visualize-stream-analytics-throughput-at-scale-the-raspberry-pi-scenario"></a>Wizualizuj Stream Analytics przepustowość na dużą skalę: w scenariuszu Pi malina
Aby ułatwić zrozumienie, jak skalować zadania usługi analiza strumienia, wykonane eksperyment na podstawie danych wprowadzonych z urządzenia malina Pi. Tego eksperymentu poinformować nas, zobacz wpływu na przepustowość wiele jednostek przesyłania strumieniowego i partycje.

W tym scenariuszu urządzenie wysyła dane czujników (klienci) do Centrum zdarzeń. Przesyłanie strumieniowe Analytics przetwarza dane i wysyła alert ani w statystyce jako dane wyjściowe do innego Centrum zdarzeń. 

Klient wysyła dane czujników w formacie JSON. Dane wyjściowe jest również w formacie JSON. Dane wygląda następująco:

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

Następujące zapytanie służy do wysyłania alertu po wyłączeniu światło:

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>Miara przepływności

W tym kontekście przepływność wynosi ilość danych wejściowych przetworzone przez usługę Stream Analytics w stałej ilości czasu. (Firma Microsoft mierzy przez 10 minut.) Aby uzyskać najlepsze przepływności przetwarzania danych wejściowych, zarówno wejściowego strumienia danych i zapytania zostały podzielone na partycje. Jest dostępna **COUNT()** do mierzenia, ile zdarzenia wejściowe były przetwarzane w kwerendzie. Aby upewnij się, że zadania nie oczekiwał po prostu dla zdarzenia wejściowe przejdzie, każdej partycji Centrum zdarzeń wejściowych został wstępnie ładowane z około 300 MB danych wejściowych.

W poniższej tabeli przedstawiono wyniki, którą widzieliśmy, gdy firma Microsoft zwiększyć liczbę jednostek przesyłania strumieniowego i odpowiadająca mu partycja liczby w usłudze event hubs.  

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

I Wykres ukazuje wizualizacji relacji między usługami SUs i przepływności.

![img.stream.Analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie do usługi Azure Stream Analytics](stream-analytics-introduction.md)
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

