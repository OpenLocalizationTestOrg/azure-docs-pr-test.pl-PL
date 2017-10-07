---
title: "aaaQuery przykłady typowych wzorców użycia w Stream Analytics | Dokumentacja firmy Microsoft"
description: "Typowych wzorców zapytań usługi Azure Stream Analytics"
keywords: "Przykłady zapytań"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: jenniehubbard
ms.openlocfilehash: c8f7a8ac661eaf0281f4140b02c42141b73040fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a>Zapytanie przykłady typowych wzorców użycia usługi analiza strumienia
## <a name="introduction"></a>Wprowadzenie
Zapytania w usłudze Azure Stream Analytics są wyrażone według języka przypominającego SQL zapytań. Te zapytania są udokumentowane w hello [materiały referencyjne dotyczące języka zapytań usługi Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) przewodnik. Ten artykuł opisanych rozwiązań tooseveral typowych wzorców zapytań, na podstawie rzeczywistych sytuacji. Jest pracy w toku i kontynuuje toobe zaktualizowano o nowe wzorce w sposób ciągły.

## <a name="query-example-convert-data-types"></a>Przykład zapytania: konwersji typów danych
**Opis elementu**: Definiowanie typów hello właściwości na powitania strumienia wejściowego.
Na przykład wagi samochodu hello pochodzi na powitania strumień wejściowy jako ciągi i musi toobe konwertowane za**INT** tooperform **suma** go.

**Dane wejściowe**:

| Wprowadź | Time | Waga |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |"1000" |
| Honda |2015-01-01T00:00:02.0000000Z |"2000" |

**Dane wyjściowe**:

| Wprowadź | Waga |
| --- | --- |
| Honda |3000 |

**Rozwiązanie**:

    SELECT
        Make,
        SUM(CAST(Weight AS BIGINT)) AS Weight
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**Wyjaśnienie**: Użyj **RZUTOWANIA** instrukcji w hello **wagi** pola toospecify jego typu danych. Lista hello obsługiwane typy danych w [typy danych (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).

## <a name="query-example-use-likenot-like-toodo-pattern-matching"></a>Przykład zapytania: nie podobne podobne toodo dopasowanie wzorca
**Opis elementu**: Sprawdź, czy wartość pola w zdarzeniu hello ze wzorcem niektórych.
Na przykład sprawdzić, czy wynik hello zwraca płyt licencji, które A zaczynać się i kończyć 9.

**Dane wejściowe**:

| Wprowadź | LicensePlate | Time |
| --- | --- | --- |
| Honda |ABC 123 |2015-01-01T00:00:01.0000000Z |
| Toyota |AAA 999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC 369 |2015-01-01T00:00:03.0000000Z |

**Dane wyjściowe**:

| Wprowadź | LicensePlate | Time |
| --- | --- | --- |
| Toyota |AAA 999 |2015-01-01T00:00:02.0000000Z |
| Nissan |ABC 369 |2015-01-01T00:00:03.0000000Z |

**Rozwiązanie**:

    SELECT
        *
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LicensePlate LIKE 'A%9'

**Wyjaśnienie**: Użyj hello **jak** hello toocheck instrukcji **LicensePlate** wartość w polu. Powinna zaczynać A, a następnie mieć dowolny ciąg zawierający zero lub więcej znaków i następnie kończyć 9. 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a>Przykład zapytania: Określ logikę różnych przypadków/wartości (instrukcji CASE)
**Opis elementu**: Podaj innej obliczania pola, na podstawie określonego kryterium.
Na przykład można podać opis ciągu ile samochodów dla hello same należy przekazany z szczególnych przypadkach 1.

**Dane wejściowe**:

| Wprowadź | Time |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Dane wyjściowe**:

| CarsPassed | Time |
| --- | --- | --- |
| 1 Honda |2015-01-01T00:00:10.0000000Z |
| 2 Toyotas |2015-01-01T00:00:10.0000000Z |

**Rozwiązanie**:

    SELECT
        CASE
            WHEN COUNT(*) = 1 THEN CONCAT('1 ', Make)
            ELSE CONCAT(CAST(COUNT(*) AS NVARCHAR(MAX)), ' ', Make, 's')
        END AS CarsPassed,
        System.TimeStamp AS Time
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)

**Wyjaśnienie**: hello **przypadku** klauzuli pozwala nam tooprovide różnych obliczeń, na podstawie kryteriów, niektóre (w tym przypadku hello liczba samochodów hello w oknie agregacji hello).

## <a name="query-example-send-data-toomultiple-outputs"></a>Przykład zapytania: wysyłanie danych wyjściowych toomultiple danych
**Opis elementu**: toomultiple danych wysyłania danych wyjściowych obiektów docelowych w jednym zadaniu.
Na przykład analizować dane oparte na wartościach progowych alertu i wszystkie zdarzenia tooblob magazyn archiwum.

**Dane wejściowe**:

| Wprowadź | Time |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output1**:

| Wprowadź | Time |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Output2**:

| Wprowadź | Time | Licznik |
| --- | --- | --- |
| Toyota |2015-01-01T00:00:10.0000000Z |3 |

**Rozwiązanie**:

    SELECT
        *
    INTO
        ArchiveOutput
    FROM
        Input TIMESTAMP BY Time

    SELECT
        Make,
        System.TimeStamp AS Time,
        COUNT(*) AS [Count]
    INTO
        AlertOutput
    FROM
        Input TIMESTAMP BY Time
    GROUP BY
        Make,
        TumblingWindow(second, 10)
    HAVING
        [Count] >= 3

**Wyjaśnienie**: hello **INTO** klauzuli informuje usługi analiza strumienia, który hello generuje toowrite hello danych toofrom tej instrukcji.
Witaj pierwszego zapytania jest przekazywanie danych hello Otrzymaliśmy wynik tooan nasze konto nazywa się **ArchiveOutput**.
Witaj drugiego zapytania jest niektórych prostych agregacji i filtrowanie i wysyła wyników hello tooa podrzędne system alertów.

Możesz również użyć hello wyniki hello wspólnych wyrażeniach tabel (wyrażeń CTE) Uwaga (takich jak **WITH** instrukcje) w wielu deklaracjach danych wyjściowych. Ta opcja ma hello dodatkowa korzyść otwarcia mniej źródło danych wejściowych toohello czytników.
Na przykład: 

    WITH AllRedCars AS (
        SELECT
            *
        FROM
            Input TIMESTAMP BY Time
        WHERE
            Color = 'red'
    )
    SELECT * INTO HondaOutput FROM AllRedCars WHERE Make = 'Honda'
    SELECT * INTO ToyotaOutput FROM AllRedCars WHERE Make = 'Toyota'

## <a name="query-example-count-unique-values"></a>Przykład zapytania: liczba unikatowych wartości
**Opis elementu**: liczba hello liczbę unikatowych wartości pól wyświetlanych w strumieniu hello w przedziale czasu.
Na przykład ile unikatowy sprawia, że przekazywane stoisku przez hello w oknie 2 sekundy samochodów?

**Dane wejściowe**:

| Wprowadź | Time |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Honda |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |
| Toyota |2015-01-01T00:00:03.0000000Z |

**Dane wyjściowe:**

| Licznik | Time |
| --- | --- |
| 2 |2015-01-01T00:00:02.000Z |
| 1 |2015-01-01T00:00:04.000Z |

**Rozwiązanie:**

````
SELECT
     COUNT(DISTINCT Make) AS CountMake,
     System.TIMESTAMP AS TIME
FROM Input TIMESTAMP BY TIME
GROUP BY 
     TumblingWindow(second, 2)
````


**Wyjaśnienie:**
**COUNT (różne upewnij)** zwraca hello liczbę unikatowych wartości w hello **upewnij** kolumny w przedziale czasu.

## <a name="query-example-determine-if-a-value-has-changed"></a>Przykład zapytania: ustalić, jeśli wartość została zmieniona
**Opis elementu**: przyjrzyj poprzedniej toodetermine wartość, jeśli jest inny niż bieżąca wartość hello.
Na przykład jest hello poprzedniej samochodu na powitania przez drogowej hello przez sam jako bieżący samochodu hello?

**Dane wejściowe**:

| Wprowadź | Time |
| --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Dane wyjściowe**:

| Wprowadź | Time |
| --- | --- |
| Toyota |2015-01-01T00:00:02.0000000Z |

**Rozwiązanie**:

    SELECT
        Make,
        Time
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(minute, 1)) <> Make

**Wyjaśnienie**: Użyj **LAG** toopeek do hello wejściowy strumienia wstecz jedno zdarzenie i pobrać hello **upewnij** wartość. Porównaj je po toohello **upewnij** wartość na powitania bieżącego zdarzenia i dane wyjściowe hello zdarzeń, gdy są one różne.

## <a name="query-example-find-hello-first-event-in-a-window"></a>Przykład zapytania: Znajdź hello pierwszego zdarzenia w oknie
**Opis elementu**: Znajdź hello pierwszego samochodu w co 10 minut.

**Dane wejściowe**:

| LicensePlate | Wprowadź | Time |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Dane wyjściowe**:

| LicensePlate | Wprowadź | Time |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |

**Rozwiązanie**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) = 1

Teraz upewnijmy zmiany hello problemu i Znajdź hello pierwszego samochodu konkretnej co 10 minut.

| LicensePlate | Wprowadź | Time |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Rozwiązanie**:

    SELECT 
        LicensePlate,
        Make,
        Time
    FROM 
        Input TIMESTAMP BY Time
    WHERE 
        IsFirst(minute, 10) OVER (PARTITION BY Make) = 1

## <a name="query-example-find-hello-last-event-in-a-window"></a>Przykład zapytania: hello Znajdź ostatnie zdarzenie w oknie
**Opis elementu**: Znajdź hello ostatniego samochodu w co 10 minut.

**Dane wejściowe**:

| LicensePlate | Wprowadź | Time |
| --- | --- | --- |
| DXE 5291 |Honda |2015-07-27T00:00:05.0000000Z |
| YZK 5704 |Ford |2015-07-27T00:02:17.0000000Z |
| RMV 8282 |Honda |2015-07-27T00:05:01.0000000Z |
| YHN 6970 |Toyota |2015-07-27T00:06:00.0000000Z |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| QYF 9358 |Honda |2015-07-27T00:12:02.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Dane wyjściowe**:

| LicensePlate | Wprowadź | Time |
| --- | --- | --- |
| VFE 1616 |Toyota |2015-07-27T00:09:31.0000000Z |
| MDR 6128 |BMW |2015-07-27T00:13:45.0000000Z |

**Rozwiązanie**:

    WITH LastInWindow AS
    (
        SELECT 
            MAX(Time) AS LastEventTime
        FROM 
            Input TIMESTAMP BY Time
        GROUP BY 
            TumblingWindow(minute, 10)
    )
    SELECT 
        Input.LicensePlate,
        Input.Make,
        Input.Time
    FROM
        Input TIMESTAMP BY Time 
        INNER JOIN LastInWindow
        ON DATEDIFF(minute, Input, LastInWindow) BETWEEN 0 AND 10
        AND Input.Time = LastInWindow.LastEventTime

**Wyjaśnienie**: istnieją dwa kroki w zapytaniu hello. Hello pierwszy znalezione przez jeden hello najnowsze sygnatury czasowej w systemie windows 10 minut. Witaj drugi krok sprzężenia hello wyniki hello pierwszego zapytania z hello oryginalnego strumienia toofind hello zdarzeń pasujących hello ostatniego sygnatury czasowe w każdym okna. 

## <a name="query-example-detect-hello-absence-of-events"></a>Przykład zapytania: wykrywanie hello braku zdarzeń
**Opis elementu**: Sprawdź, czy strumień nie ma wartości odpowiadający niektórych kryterium.
Na przykład 2 kolejnych samochodów z hello przez sam wprowadzony hello przez drogowej w hello ostatnich 90 sekund?

**Dane wejściowe**:

| Wprowadź | LicensePlate | Time |
| --- | --- | --- |
| Honda |ABC 123 |2015-01-01T00:00:01.0000000Z |
| Honda |AAA 999 |2015-01-01T00:00:02.0000000Z |
| Toyota |DEF 987 |2015-01-01T00:00:03.0000000Z |
| Honda |GHI 345 |2015-01-01T00:00:04.0000000Z |

**Dane wyjściowe**:

| Wprowadź | Time | CurrentCarLicensePlate | FirstCarLicensePlate | FirstCarTime |
| --- | --- | --- | --- | --- |
| Honda |2015-01-01T00:00:02.0000000Z |AAA 999 |ABC 123 |2015-01-01T00:00:01.0000000Z |

**Rozwiązanie**:

    SELECT
        Make,
        Time,
        LicensePlate AS CurrentCarLicensePlate,
        LAG(LicensePlate, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarLicensePlate,
        LAG(Time, 1) OVER (LIMIT DURATION(second, 90)) AS FirstCarTime
    FROM
        Input TIMESTAMP BY Time
    WHERE
        LAG(Make, 1) OVER (LIMIT DURATION(second, 90)) = Make

**Wyjaśnienie**: Użyj **LAG** toopeek do hello wejściowy strumienia wstecz jedno zdarzenie i pobrać hello **upewnij** wartość. Porównaj je toohello **upewnij** wartości hello bieżącego zdarzenia i dane wyjściowe hello zdarzeń, jeśli są one hello takie same. Można również użyć **LAG** tooget danych dotyczących samochodów poprzedniej hello.

## <a name="query-example-detect-hello-duration-between-events"></a>Przykład zapytania: wykrywanie hello czas między zdarzeniami
**Opis elementu**: Znajdź hello czasu trwania jednego z określonych zdarzeń. Podana clickstream sieci web, na przykład określić czas hello funkcji.

**Dane wejściowe**:  

| Użytkownik | Funkcja | Wydarzenie | Time |
| --- | --- | --- | --- |
| user@location.com |RightMenu |Uruchamianie |2015-01-01T00:00:01.0000000Z |
| user@location.com |RightMenu |Koniec |2015-01-01T00:00:08.0000000Z |

**Dane wyjściowe**:  

| Użytkownik | Funkcja | Czas trwania |
| --- | --- | --- |
| user@location.com |RightMenu |7 |

**Rozwiązanie**:

````
    SELECT
        [user], feature, DATEDIFF(second, LAST(Time) OVER (PARTITION BY [user], feature LIMIT DURATION(hour, 1) WHEN Event = 'start'), Time) as duration
    FROM input TIMESTAMP BY Time
    WHERE
        Event = 'end'
````

**Wyjaśnienie**: Użyj hello **ostatniego** ostatniego działać tooretrieve hello **czasu** wartość, gdy typ zdarzenia hello **Start**. Witaj **ostatniego** używa **PARTITION BY [użytkownik]** tooindicate, który hello wyniku jest obliczany na unikatowy użytkownika. Zapytanie Hello ma maksymalną 1 godzina próg hello odstęp czasu między **Start** i **zatrzymać** zdarzenia, ale można skonfigurować zgodnie z potrzebami **(LIMIT DURATION(hour, 1)**.

## <a name="query-example-detect-hello-duration-of-a-condition"></a>Przykład zapytania: wykrywanie czas trwania hello warunku
**Opis elementu**: Sprawdzanie, jak długo wystąpił warunek.
Na przykład załóżmy, że usterki spowodowała wszystkich samochodów niepoprawne ciężar (ponad 20 000 jednostkach funt). Chcemy czas trwania hello toocompute hello usterek.

**Dane wejściowe**:

| Wprowadź | Time | Waga |
| --- | --- | --- |
| Honda |2015-01-01T00:00:01.0000000Z |2000 |
| Toyota |2015-01-01T00:00:02.0000000Z |25000 |
| Honda |2015-01-01T00:00:03.0000000Z |26000 |
| Toyota |2015-01-01T00:00:04.0000000Z |25000 |
| Honda |2015-01-01T00:00:05.0000000Z |26000 |
| Toyota |2015-01-01T00:00:06.0000000Z |25000 |
| Honda |2015-01-01T00:00:07.0000000Z |26000 |
| Toyota |2015-01-01T00:00:08.0000000Z |2000 |

**Dane wyjściowe**:

| StartFault | EndFault |
| --- | --- |
| 2015-01-01T00:00:02.000Z |2015-01-01T00:00:07.000Z |

**Rozwiązanie**:

````
    WITH SelectPreviousEvent AS
    (
    SELECT
    *,
        LAG([time]) OVER (LIMIT DURATION(hour, 24)) as previousTime,
        LAG([weight]) OVER (LIMIT DURATION(hour, 24)) as previousWeight
    FROM input TIMESTAMP BY [time]
    )

    SELECT 
        LAG(time) OVER (LIMIT DURATION(hour, 24) WHEN previousWeight < 20000 ) [StartFault],
        previousTime [EndFault]
    FROM SelectPreviousEvent
    WHERE
        [weight] < 20000
        AND previousWeight > 20000
````

**Wyjaśnienie**: Użyj **LAG** strumień wejściowy hello tooview przez 24 godziny i wyszukać wystąpienia where **StartFault** i **StopFault** są objęte hello Waga < 20000.

## <a name="query-example-fill-missing-values"></a>Przykład zapytania: wypełnienie brakujących wartości
**Opis elementu**: hello strumienia zdarzeń, które nie mają wartości, można utworzyć w strumieniu zdarzeń o regularnych odstępach czasu.
Na przykład generują zdarzenie co 5 sekund, która raportuje hello ostatnio widoczne punktu danych.

**Dane wejściowe**:

| T | wartość |
| --- | --- |
| "2014-01-01T06:01:00" |1 |
| "2014-01-01T06:01:05" |2 |
| "2014-01-01T06:01:10" |3 |
| "2014-01-01T06:01:15" |4 |
| "2014-01-01T06:01:30" |5 |
| "2014-01-01T06:01:35" |6 |

**Dane wyjściowe (pierwszych 10 wierszy)**:

| windowend | lastevent.t | lastevent.Value |
| --- | --- | --- |
| 2014-01-01T14:01:00.000Z |2014-01-01T14:01:00.000Z |1 |
| 2014-01-01T14:01:05.000Z |2014-01-01T14:01:05.000Z |2 |
| 2014-01-01T14:01:10.000Z |2014-01-01T14:01:10.000Z |3 |
| 2014-01-01T14:01:15.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:20.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:25.000Z |2014-01-01T14:01:15.000Z |4 |
| 2014-01-01T14:01:30.000Z |2014-01-01T14:01:30.000Z |5 |
| 2014-01-01T14:01:35.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:40.000Z |2014-01-01T14:01:35.000Z |6 |
| 2014-01-01T14:01:45.000Z |2014-01-01T14:01:35.000Z |6 |

**Rozwiązanie**:

    SELECT
        System.Timestamp AS windowEnd,
        TopOne() OVER (ORDER BY t DESC) AS lastEvent
    FROM
        input TIMESTAMP BY t
    GROUP BY HOPPINGWINDOW(second, 300, 5)


**Wyjaśnienie**: to zapytanie generuje zdarzenia co 5 sekund i dane wyjściowe hello ostatnie zdarzenie odebrany wcześniej. Witaj [okna Hopping](https://msdn.microsoft.com/library/dn835041.aspx "Hopping okno usługi Azure Stream Analytics") czas trwania określa, jak daleko wstecz hello zapytanie wygląda toofind hello najnowsze zdarzenie (300 sekund w tym przykładzie).

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

