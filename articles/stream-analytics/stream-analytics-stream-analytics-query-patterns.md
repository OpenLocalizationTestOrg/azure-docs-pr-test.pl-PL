---
title: "Zapytanie przykłady typowych wzorców użycia w Stream Analytics | Dokumentacja firmy Microsoft"
description: "Typowych wzorców zapytań usługi Azure Stream Analytics"
keywords: "Przykłady zapytań"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jenniehubbard
editor: cgronlun
ms.assetid: 6b9a7d00-fbcc-42f6-9cbb-8bbf0bbd3d0e
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/08/2017
ms.author: samacha
ms.openlocfilehash: a27bae1828bd469d4439e0ce43098edd73f54243
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="query-examples-for-common-stream-analytics-usage-patterns"></a>Zapytanie przykłady typowych wzorców użycia usługi analiza strumienia
## <a name="introduction"></a>Wprowadzenie
Zapytania w usłudze Azure Stream Analytics są wyrażone według języka przypominającego SQL zapytań. Te zapytania są udokumentowane w artykule [materiały referencyjne dotyczące języka zapytań usługi Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) przewodnik. W tym artykule przedstawiono rozwiązania kilka typowych wzorców zapytań, na podstawie w rzeczywistych scenariuszach. Jest pracy w toku i jest aktualizowany o nowe wzorce w sposób ciągły.

## <a name="query-example-convert-data-types"></a>Przykład zapytania: konwersji typów danych
**Opis elementu**: Definiowanie typów właściwości ze strumienia wejściowego.
Na przykład wagi samochodu pochodzi ze strumienia wejściowego jako ciągi i musi zostać skonwertowany do **INT** przeprowadzić **suma** go.

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

**Wyjaśnienie**: Użyj **RZUTOWANIA** instrukcji w **wagi** pola, aby określić typ jej danych. Zobacz listę obsługiwanych typów danych w [typy danych (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835065.aspx).

## <a name="query-example-use-likenot-like-to-do-pattern-matching"></a>Przykład zapytania: Użyj notacji nie zostać dopasowanie wzorca
**Opis elementu**: Sprawdź, czy wartość pola o zdarzeniu zgodna niektórych wzorca.
Na przykład sprawdzić, czy wynik zwraca płyt licencji, które A zaczynać się i kończyć 9.

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

**Wyjaśnienie**: Użyj **jak** instrukcji, aby sprawdzić **LicensePlate** wartość w polu. Powinna zaczynać A, a następnie mieć dowolny ciąg zawierający zero lub więcej znaków i następnie kończyć 9. 

## <a name="query-example-specify-logic-for-different-casesvalues-case-statements"></a>Przykład zapytania: Określ logikę różnych przypadków/wartości (instrukcji CASE)
**Opis elementu**: Podaj innej obliczania pola, na podstawie określonego kryterium.
Na przykład Podaj opis ciągu upewnij ile samochodów tego samego przekazany z szczególnych przypadkach 1.

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

**Wyjaśnienie**: **przypadku** klauzuli pozwala na udostępnianie różnych obliczeń, na podstawie kryteriów, niektóre (w tym przypadku liczba samochodów w oknie agregacji).

## <a name="query-example-send-data-to-multiple-outputs"></a>Przykład zapytania: wysyłanie danych do wielu wyjść
**Opis elementu**: wysyłania danych do wielu elementów docelowych w danych wyjściowych z jednym zadaniu.
Na przykład analizować dane oparte na wartościach progowych alertu oraz archiwum wszystkie zdarzenia do magazynu obiektów blob.

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

**Wyjaśnienie**: **INTO** klauzuli informuje Stream Analytics której dane wyjściowe można zapisać danych do tej instrukcji.
Pierwszego zapytania jest przekazywanie danych Otrzymaliśmy do wyjścia nasze konto nazywa się **ArchiveOutput**.
Drugiego zapytania jest niektórych prostych agregacji i filtrowanie i wysyła wyniki do podrzędne system alertów.

Należy pamiętać, że możesz również użyć wyniki wspólnych wyrażeniach tabel (wyrażeń CTE) (takich jak **WITH** instrukcje) w wielu deklaracjach danych wyjściowych. Ta opcja ma dodatkowa korzyść otwarcia mniej czytników do źródła danych wejściowych.
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
**Opis elementu**: liczbę unikatowych wartości pól wyświetlanych w strumieniu w przedziale czasu.
Na przykład ile unikatowy sprawia, że przekazywane przez kabinę w oknie 2 sekundy samochodów?

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
**COUNT (różne upewnij)** zwraca liczbę unikatowych wartości w **upewnij** kolumny w przedziale czasu.

## <a name="query-example-determine-if-a-value-has-changed"></a>Przykład zapytania: ustalić, jeśli wartość została zmieniona
**Opis elementu**: przyjrzeć się poprzedniej wartości, aby ustalić, czy jest inna niż bieżąca wartość.
Na przykład jest poprzedniej samochodu na drodze przez tego samego upewnij jako bieżący samochód?

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

**Wyjaśnienie**: Użyj **LAG** wgląd do strumienia wejściowego jednego zdarzenia Wstecz w celu uzyskania **upewnij** wartość. Następnie porównania jej **upewnij** wartość dla bieżącego zdarzenia i dane wyjściowe zdarzenia, jeśli są one różne.

## <a name="query-example-find-the-first-event-in-a-window"></a>Przykład zapytania: Znajdź pierwsze zdarzenie w oknie
**Opis elementu**: Znajdź pierwszego samochodu co 10 minut.

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

Teraz załóżmy zmienić problemu i Znajdź pierwszego samochodu marki określonego w co 10 minut.

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

## <a name="query-example-find-the-last-event-in-a-window"></a>Przykład zapytania: Znajdź ostatnie zdarzenie w oknie
**Opis elementu**: Znajdź ostatni samochodu co 10 minut.

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

**Wyjaśnienie**: istnieją dwa kroki w zapytaniu. Pierwsza z nich znajduje najnowsze sygnatury czasowej w systemie windows 10 minut. Drugim krokiem łączy wyniki pierwszego zapytania z oryginalnego strumienia do znalezienia zdarzeń, zgodne ostatniego sygnatury czasowe w każdym okna. 

## <a name="query-example-detect-the-absence-of-events"></a>Przykład zapytania: wykrycia braku zdarzeń
**Opis elementu**: Sprawdź, czy strumień nie ma wartości odpowiadający niektórych kryterium.
Na przykład 2 samochodów następujących po sobie z tym samym upewnij wprowadzony drogowej przez w ciągu ostatnich 90 sekund?

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

**Wyjaśnienie**: Użyj **LAG** wgląd do strumienia wejściowego jednego zdarzenia Wstecz w celu uzyskania **upewnij** wartość. Aby porównać **upewnij** wartość w bieżącym zdarzeń, a następnie dane wyjściowe zdarzenia, jeśli są one takie same. Można również użyć **LAG** można pobrać danych dotyczących samochodów poprzedniej.

## <a name="query-example-detect-the-duration-between-events"></a>Przykład zapytania: wykrywanie czas między zdarzeniami
**Opis elementu**: Znajdź czasu trwania jednego z określonych zdarzeń. Biorąc pod uwagę clickstream sieci web, na przykład określić czas spędzony na funkcji.

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

**Wyjaśnienie**: Użyj **ostatniego** funkcji, aby pobrać ostatniego **czasu** wartość, gdy typ zdarzenia **Start**. **Ostatniego** używa **PARTITION BY [użytkownik]** wskazująca, czy wynik jest obliczana na unikatowy użytkownika. Zapytanie ma 1 godzina próg maksymalnego różnica czasu między **Start** i **zatrzymać** zdarzenia, ale można skonfigurować zgodnie z potrzebami **(LIMIT DURATION(hour, 1)**.

## <a name="query-example-detect-the-duration-of-a-condition"></a>Przykład zapytania: wykrywanie w czasie trwania warunek
**Opis elementu**: Sprawdzanie, jak długo wystąpił warunek.
Na przykład załóżmy, że usterki spowodowała wszystkich samochodów niepoprawne ciężar (ponad 20 000 jednostkach funt). Chcemy obliczeniowe czas trwania usterki.

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

**Wyjaśnienie**: Użyj **LAG** do wyświetlania strumień wejściowy przez 24 godziny i poszukaj wystąpień where **StartFault** i **StopFault** są objęte wagi < 20000.

## <a name="query-example-fill-missing-values"></a>Przykład zapytania: wypełnienie brakujących wartości
**Opis elementu**: dla tego strumienia zdarzeń, które nie mają wartości tworzy strumień zdarzeń o regularnych odstępach czasu.
Na przykład generują zdarzenie co 5 sekund, która raportuje najbardziej ostatnio widziany punktu danych.

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


**Wyjaśnienie**: to zapytanie generuje zdarzenia co 5 sekund i wyprowadza ostatnie zdarzenie odebrany wcześniej. [Okna Hopping](https://msdn.microsoft.com/library/dn835041.aspx "Hopping okno usługi Azure Stream Analytics") czas trwania określa, jak daleko wstecz zapytanie odwołuje się do Znajdź najnowsze zdarzenie (300 sekund w tym przykładzie).

## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie do usługi Azure Stream Analytics](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

