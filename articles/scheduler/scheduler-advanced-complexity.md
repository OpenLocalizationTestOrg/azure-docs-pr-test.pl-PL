---
title: "tooBuild aaaHow harmonogramy złożone i zaawansowane cyklu z Harmonogram systemu Azure"
description: "Jak planuje złożone tooBuild i zaawansowane cyklu z Harmonogram systemu Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5c124986-9f29-4cbc-ad5a-c667b37fbe5a
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 02172791978b12be0ccb3078125d057b2efe8523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-complex-schedules-and-advanced-recurrence-with-azure-scheduler"></a>Jak planuje złożone tooBuild i zaawansowane cyklu z Harmonogram systemu Azure
## <a name="overview"></a>Omówienie
Centralnym hello Azure harmonogramu zadania jest hello *harmonogram*. Harmonogram Hello Określa, kiedy i jak hello harmonogramu wykonuje zadanie hello.

Harmonogram systemu Azure umożliwia toospecify różne jednorazowe i cyklicznego harmonogramy dla zadania. *Jednorazowe* harmonogramy wyzwalać raz o określonej godzinie — skutecznie znajdują się one *cyklicznego* harmonogramy, które są wykonywane tylko raz. Harmonogramów cyklicznych wyzwalać na wstępnie określoną częstotliwością.

Z tego rodzaju elastyczności Harmonogram systemu Azure umożliwia obsługuje wiele różnych scenariuszy biznesowych:

* Porządkowanie danych okresowe — np. codziennie, Usuń wszystkie tweetów starsze niż 3 miesiące
* Archiwalne — np. co miesiąc, usługi toobackup historii faktury wypychania
* Żądania dotyczące danych zewnętrznych — np. co 15 minut, pobierają nowe ski prognoza pogody z NOAA
* Przetwarzanie — np. każdy dzień tygodnia, poza godzinami szczytu obrazu, użyj chmury przetwarzania obrazów toocompress przekazać tego dnia

W tym artykule firma Microsoft przeprowadzenie przykład zadań, które można utworzyć z Harmonogram systemu Azure. Udostępniamy hello dane JSON, który opisano każdy z harmonogramów. Jeśli używasz hello [interfejsu API REST harmonogramu](https://msdn.microsoft.com/library/mt629143.aspx), można użyć tego samego JSON dla [Tworzenie zadania harmonogramu Azure](https://msdn.microsoft.com/library/mt629145.aspx).

## <a name="supported-scenarios"></a>Obsługiwane scenariusze
Witaj wiele przykłady w tym temacie przedstawiają szerokość hello scenariuszy obsługiwanych przez usługę Azure harmonogramu. Ogólnie te przykłady przedstawiają sposób harmonogramy toocreate wielu wzorców zachowanie, w tym hello tych poniżej:

* Uruchom raz od określonej daty i godziny
* Uruchom i powtarzanie wiele razy jawne
* Natychmiastowe uruchomienie i powtarzanie
* Uruchom i powtarzanie co  *n*  minuty, godziny, dni, tygodnie lub miesiące, począwszy od określonego czasu
* Uruchom i powtarzanie częstotliwością co tydzień lub co miesiąc, ale tylko w określone dni, określone dni tygodnia lub określone dni miesiąca
* Uruchom i powtarzanie na wiele razy w okresie — np. ostatni piątek i poniedziałek każdego miesiąca lub 5:15:00 i 17:15:00 każdego dnia

## <a name="dates-and-datetimes"></a>Daty i dat i godzin
Daty w zadania harmonogramu Azure wykonaj hello [specyfikacji ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) i zawierają tylko hello Data.

Odwołania do daty i godziny w Azure harmonogramu zadań wykonaj hello [specyfikacji ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) i zawierać części zarówno datę i godzinę. Daty i godziny, która nie określa przesunięcie UTC zakłada, że toobe UTC.  

## <a name="how-to-use-json-and-rest-api-for-creating-schedules"></a>Korzystanie z formatu JSON i interfejsu API REST do tworzenia harmonogramów
Witaj toocreate przy użyciu prostego harmonogramu [interfejsu API REST harmonogramu Azure](https://msdn.microsoft.com/library/mt629143), pierwszy [zarejestrować subskrypcji u dostawcy zasobów](https://msdn.microsoft.com/library/azure/dn790548.aspx) (nazwa dostawcy hello harmonogramu jest  *Microsoft.Scheduler*), następnie [tworzenie kolekcji zadań](https://msdn.microsoft.com/library/mt629159.aspx), a na końcu [utworzyć zadanie](https://msdn.microsoft.com/library/mt629145.aspx). Podczas tworzenia zadania można określić planowania i cyklu przy użyciu formatu JSON, takich jak hello jedną fragmentem książki poniżej:

    {
        "startTime": "2012-08-04T00:00Z", // optional
         …
        "recurrence":                     // optional
        {
            "frequency": "week",     // can be "year" "month" "day" "week" "hour" "minute"
            "interval": 1,                // optional, how often toofire (default too1)
            "schedule":                   // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]                      
            },
            "count": 10,                  // optional (default toorecur infinitely)
            "endTime": "2012-11-04",      // optional (default toorecur infinitely)
        },
        …
    }

## <a name="overview-job-schema-basics"></a>Omówienie: Zadanie schematu podstawy
w poniższej tabeli Hello zawiera ogólne omówienie hello główne elementy pokrewne toorecurrence i Planowanie zadania:

| **Nazwy JSON** | **Opis** |
|:--- |:--- |
| ***czas rozpoczęcia*** |*wartość startTime* jest daty i godziny. Proste harmonogramów *startTime* jest pierwsze wystąpienie hello i złożone harmonogramów hello zadanie zostanie uruchomione nie wcześniej niż *startTime*. |
| ***cyklu*** |Witaj *cyklu* obiektu określa zasady cyklu dla zadania hello i hello cyklu hello zadanie będzie wykonywane za pomocą. Witaj cyklu obsługuje elementy hello *częstotliwości, interwał, endTime, count,* i *harmonogram*. Jeśli *cyklu* jest zdefiniowany, *częstotliwość* jest wymagana; hello innych elementów *cyklu* są opcjonalne. |
| ***częstotliwość*** |Witaj *częstotliwość* ciąg reprezentujący hello częstotliwość jednostki, które hello zadania powtarzania. Obsługiwane wartości to *"min", "Godzina", "day", "tydzień"* lub *"miesiąc".* |
| ***Interwał*** |Witaj *interwał* jest dodatnią liczbą całkowitą i określa interwał hello hello *częstotliwość* określający, jak często hello zadania. Na przykład jeśli *interwał* 3 i *częstotliwość* jest "tydzień" hello zadania wystąpi co 3 tygodni. Harmonogram systemu Azure obsługuje maksymalnie *interwał* 18 miesięcy do miesięcznej częstotliwości 78 tygodniach częstotliwości co tydzień lub 548 dni dzienną częstotliwość. Godziny i minuty częstotliwość hello obsługiwany zakres to 1 < = *interwał* < = 1000. |
| ***wartość endTime*** |Witaj *endTime* ciąg Określa hello daty i godziny poza które hello nie powinien wykonać zadanie. Nie jest prawidłową toohave *endTime* w przeszłości hello. Jeśli nie *endTime* lub jest określona liczba, zadanie hello nieograniczonej działa. Zarówno *endTime* i *liczby* nie może być uwzględniony w hello samo zadanie. |
| ***Liczba*** |<p>Witaj *liczba* jest dodatnią liczbą całkowitą (większe od zera) określająca hello liczbę razy, to zadanie powinno zostać uruchomione przed zakończeniem.</p><p>Witaj *liczba* reprezentuje hello liczba hello zadanie będzie uruchamiane przed określane jako ukończone. Na przykład dla zadania, która jest wykonywana codziennie o *liczba* 5 i rozpoczęcie poniedziałek, hello zadanie zostało ukończone po wykonaniu w piątek. Jeśli uruchomiony hello przypada w przeszłości hello, wykonanie pierwszej hello jest obliczana na podstawie czasu tworzenia hello.</p><p>Jeśli nie *endTime* lub *liczba* jest określona, zadanie hello nieograniczonej działa. Zarówno *endTime* i *liczby* nie może być uwzględniony w hello samo zadanie.</p> |
| ***Harmonogram*** |Zadanie o określonej częstotliwości zmienia jego cyklu na podstawie harmonogramu cyklu. A *harmonogram* zawiera zmiany na podstawie minuty, godziny, dni tygodnia, dni miesiąca i numer tygodnia. |

## <a name="overview-job-schema-defaults-limits-and-examples"></a>Omówienie: Zadania wartości domyślne schematu, ograniczenia i przykłady
Po tym omówieniu omówimy każdego z tych elementów szczegółowo opcji.

| **Nazwy JSON** | **Typ wartości** | **Wymagane?** | **Wartość domyślna** | **Prawidłowe wartości** | **Przykład** |
|:--- |:--- |:--- |:--- |:--- |:--- |
| ***czas rozpoczęcia*** |Ciąg |Nie |Brak |Daty i godziny ISO-8601 |<code>"startTime" : "2013-01-09T09:30:00-08:00"</code> |
| ***cyklu*** |Obiekt |Nie |Brak |Obiekt cyklu |<code>"recurrence" : { "frequency" : "monthly", "interval" : 1 }</code> |
| ***częstotliwość*** |Ciąg |Tak |Brak |"min", "Godzina", "day", "tydzień", "miesiąc" |<code>"frequency" : "hour"</code> |
| ***Interwał*** |Liczba |Nie |1 |1 too1000. |<code>"interval":10</code> |
| ***wartość endTime*** |Ciąg |Nie |Brak |Wartość daty i godziny reprezentującą godzinę w przyszłości hello |<code>"endTime" : "2013-02-09T09:30:00-08:00"</code> |
| ***Liczba*** |Liczba |Nie |Brak |>= 1 |<code>"count": 5</code> |
| ***Harmonogram*** |Obiekt |Nie |Brak |Obiekt harmonogramu |<code>"schedule" : { "minute" : [30], "hour" : [8,17] }</code> |

## <a name="deep-dive-starttime"></a>Szczegółowe informacje na temat: *startTime*
Hello poniższej tabeli przechwytywania jak *startTime* kontroluje sposób uruchamiania zadania.

| **wartość startTime** | **Brak cyklu** | **Cyklu. Nie harmonogramu** | **Cyklu z harmonogramem** |
|:--- |:--- |:--- |:--- |
| **Brak godziny rozpoczęcia** |Uruchom raz natychmiast |Uruchom raz natychmiast. Uruchom podczas kolejnych wykonań kodu oparte na obliczanie od czasu ostatniego wykonania |<p>Uruchom raz natychmiast</p><p>Kolejne wykonania opierają na harmonogramie cyklu</p> |
| **Godzina rozpoczęcia w przeszłości** |Uruchom raz natychmiast |<p>Oblicz pierwszy czas wykonania przyszłych po czasie rozpoczęcia, a następnie uruchom w tym czasie</p><p>Uruchom oncalculating podczas kolejnych wykonań kodu na podstawie od czasu ostatniego wykonania</p><p>Zobacz przykład pod tą tabelą, aby uzyskać więcej informacji</p> |<p>Zadania uruchamiania *nie sooner niż* hello określony czas rozpoczęcia. pierwsze wystąpienie Hello opiera się na harmonogram hello obliczana na podstawie czasu rozpoczęcia hello</p><p>Kolejne wykonania opierają na harmonogramie cyklu</p> |
| **Godzina rozpoczęcia w przyszłości lub obecnie** |Uruchom raz o określonym czasie rozpoczęcia |<p>Uruchom raz o określonym czasie rozpoczęcia</p><p>Uruchom podczas kolejnych wykonań kodu oparte na obliczanie od czasu ostatniego wykonania</p> |<p>Zadania uruchamiania *nie sooner niż* hello określony czas rozpoczęcia. pierwsze wystąpienie Hello opiera się na harmonogram hello obliczana na podstawie czasu rozpoczęcia hello</p><p>Kolejne wykonania opierają na harmonogramie cyklu</p> |

Zobacz przykład co się stanie, gdy *startTime* jest w przeszłości, hello z *cyklu* , lecz nie *harmonogram*.  Załóżmy, że hello obecna godzina to 2015-04-08 13:00, *startTime* jest 2015-04-07 14:00 i *cyklu* to 2 dni (zdefiniowane z *częstotliwość*: dzień i *interwał*: 2.) Należy pamiętać, że hello *startTime* jest w przeszłości hello i występuje przed hello bieżący czas

W tych warunkach hello *wykonanie pierwszej* będzie 2015-04-09 14:00\. Aparat harmonogramu Hello oblicza wykonywania wystąpienia od godziny rozpoczęcia hello.  Wszystkie wystąpienia w przeszłości hello są odrzucane. Aparat Hello używa hello następne wystąpienie, który występuje w przyszłości hello.  W tym przypadku *startTime* jest 2015-04-07 godzinie 2:00, więc hello następne wystąpienie jest 2 dni od tego czasu jest 2015-04-09 2:00 pm.

Należy pamiętać, że wykonanie pierwszej hello będzie hello nawet jeśli sam hello startTime 2015-04-05 14:00 lub 14:00\ 2015-04-01. Po wykonaniu pierwszej hello podczas kolejnych wykonań kodu są obliczane przy użyciu hello zaplanowane — tak byłyby w 2015-04-11 godzinie 2:00, następnie 2015-04-13 godzinie 2:00, następnie 2015-04-15 godzinie 2:00, itp.

Finally, gdy zadanie ma harmonogramu, jeśli godziny i/lub minut nie są ustawione w harmonogramie hello one domyślne toohello godziny i/lub minut hello wykonanie pierwszej, odpowiednio.

## <a name="deep-dive-schedule"></a>Szczegółowe informacje na temat: *harmonogramu*
Z jednej strony *harmonogram* można *limit* hello Liczba wykonań zadania.  Na przykład, jeśli zadanie o częstotliwości "miesiąc" ma *harmonogram* , na którym działają tylko dzień 31, zadanie hello działa tylko miesięcy, które mają 31<sup>st</sup> dnia.

Witaj w drugiej strony, *harmonogram* może również *rozwiń* hello Liczba wykonań zadania. Na przykład, jeśli zadanie o częstotliwości "miesiąc" ma *harmonogram* czy działa na dni miesiąca 1 i 2, hello zadanie jest uruchamiane na powitania 1<sup>st</sup> i 2<sup>nd</sup> dni miesiąca hello zamiast tylko raz miesiąc.

Jeśli określonych jest wiele elementów harmonogram, kolejność hello jest z największą toosmallest hello — numer tygodnia, miesiąc, dzień, dzień tygodnia, godziny i minuty.

Witaj poniższej tabeli opisano *harmonogram* elementy szczegółowo.

| **Nazwy JSON** | **Opis** | **Prawidłowe wartości** |
|:--- |:--- |:--- |
| **minut** |Minuty, godziny hello, w których hello zadania |<ul><li>Liczba całkowita, lub</li><li>Tablica liczb całkowitych</li></ul> |
| **godziny** |Godziny, dnia hello, w których hello zadania |<ul><li>Liczba całkowita, lub</li><li>Tablica liczb całkowitych</li></ul> |
| **dni tygodnia** |Dni hello tygodnia hello zadania będą uruchamiane. Można określić tylko z częstotliwością tygodniową. |<ul><li>"Poniedziałek", "Wtorek", "Środa", "Czwartek", "Piątek", "Sobota" i "Niedziela"</li><li>Tablica hello powyżej wartości (tablicy maksymalny rozmiar 7)</li></ul>*Nie* z uwzględnieniem wielkości liter |
| **monthlyOccurrences** |Określa dni hello miesiąca hello zadania będzie działać. Można określić tylko z częstotliwością miesięczną. |<ul><li>Tablica obiektów monthlyOccurrence:</li></ul> <pre>{ "day": *day*,<br />  "occurrence": *occurrence*<br />}</pre><p> *dzień* jest dzień hello hello tygodnia hello zadania zostanie uruchomiony, np. {niedziela} jest każdą niedzielę hello miesiąca. Wymagany.</p><p>Wystąpienie jest *wystąpienie* hello dzień w miesiącu hello, np. {niedziela, -1} jest hello Ostatnia niedziela hello miesiąca. Opcjonalny.</p> |
| **monthDays** |Dzień hello miesiąca hello zadanie zostanie uruchomione. Można określić tylko z częstotliwością miesięczną. |<ul><li>Dowolna wartość < = -1 i > =-31.</li><li>Dowolna wartość > = 1 i < = 31.</li><li>Tablica powyższych wartości</li></ul> |

## <a name="examples-recurrence-schedules"></a>Przykłady: Harmonogramy cyklu
Hello poniżej przedstawiono przykłady różnych harmonogramów cyklu — koncentrowanie się na powitania harmonogram obiekt i jego elementów podrzędnych.

Witaj harmonogramów poniżej wszystkich założono, że hello *interwał* ustawiono too1\. Ponadto jeden musi, że częstotliwość prawo hello w toowhat zgodnie to w hello *harmonogram* — np. nie może użyć częstotliwości "day" i mieć modyfikację "monthDays" hello harmonogramu. Takie ograniczenia opisanych powyżej.

| **Przykład** | **Opis** |
|:--- |:--- |
| <code>{"hours":[5]}</code> |Uruchom na 5: 00 każdego dnia. Harmonogram systemu Azure pasuje do każdej wartości w "godzin" z każdej wartości w "min", po jednym toocreate Uruchom listę cały czas hello, w których hello toobe jest zadanie. |
| <code>{"minutes":[15], "hours":[5]}</code> |Uruchom na 5:15:00 każdego dnia |
| <code>{"minutes":[15], "hours":[5,17]}</code> |Uruchom na 5:15:00 a 17:15 codziennie |
| <code>{"minutes":[15,45], "hours":[5,17]}</code> |Uruchom na 5:15:00, 5:45:00, 17:15:00, a 17:45 codziennie |
| <code>{"minutes":[0,15,30,45]}</code> |Uruchom co 15 minut |
| <code>{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}</code> |Uruchom co godzinę. To zadanie jest uruchamiane co godzinę. Minuta Hello jest kontrolowany przez hello *startTime*, jeśli jest określony, lub jeśli nie zostanie określona, przez czas utworzenia hello. Na przykład, jeśli godzina 12:25 hello czas rozpoczęcia lub czas utworzenia (którekolwiek ma zastosowanie), hello zadanie będzie uruchamiane w o 00:25, 01:25 02:25,..., 23:25. Witaj harmonogram jest równoważne toohaving zadanie o *częstotliwość* "Godzina" *interwał* 1 i nie *harmonogram*. Witaj różnicą jest to, że ten harmonogram może zostać wykorzystana z różnymi *częstotliwość* i *interwał* toocreate inne zadania zbyt. Na przykład, jeśli hello *częstotliwość* były "miesiąc" hello harmonogram może działać tylko raz w miesiącu zamiast codziennie Jeśli *częstotliwość* zostały "dzień" |
| <code>{minutes:[0]}</code> |Uruchom co godzinę na powitania godzinę. To zadanie jest uruchamiane co godzinę, ale na godzinę hello (np. 00: 00, 1: 00, 2 AM, itp.) To zadanie tooa równoważne z częstotliwością "Godzina", startTime zero minut i bez harmonogramu Jeśli częstotliwość hello zostały "day", ale w przypadku "week" lub "month" hello częstotliwości harmonogramu hello jest wykonywany tylko jeden dzień tygodnia lub jeden dzień w miesiącu odpowiednio. |
| <code>{"minutes":[15]}</code> |Uruchom po 15 minutach Ostatnia godzina co godzinę. Uruchamiany co godzinę, począwszy od 0:15, 1:15 i 2:15, aż do 22:15 i 23:15. |
| <code>{"hours":[17], "weekDays":["saturday"]}</code> |Jednocześnie 17: 00 w soboty co tydzień |
| <code>{hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Jednocześnie 17: 00 w poniedziałek, środę i piątek co tydzień |
| <code>{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Jednocześnie 17:15:00 a: 45 17 w poniedziałek, środę i piątek co tydzień |
| <code>{"hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Uruchom na 5: 00 a 17 w poniedziałek, środę i piątek co tydzień |
| <code>{"minutes":[15,45], "hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Uruchom na 5:15:00, 5:45:00, 17:15:00, a: 45 17 w poniedziałek, środę i piątek co tydzień |
| <code>{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Uruchamiany co 15 minut w dni robocze |
| <code>{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Uruchom co 15 minut w dni robocze miedzy 9 a 4:45 PM. |
| <code>{"weekDays":["sunday"]}</code> |Uruchom w niedziele podczas uruchamiania |
| <code>{"weekDays":["tuesday", "thursday"]}</code> |We wtorki i czwartki podczas uruchamiania |
| <code>{"minutes":[0], "hours":[6], "monthDays":[28]}</code> |Uruchom przy 6: 00 w hello 28 dzień z co miesiąc (przy założeniu częstotliwość miesiąc) |
| <code>{"minutes":[0], "hours":[6], "monthDays":[-1]}</code> |Wykonać na powitania ostatni dzień miesiąca hello 6: 00. Jeśli chcesz toorun zadania na powitania ostatni dzień miesiąca, zamiast dnia 28, 29, 30 i 31 -1. |
| <code>{"minutes":[0], "hours":[6], "monthDays":[1,-1]}</code> |Uruchom o 6: 00 na powitania pierwszy i ostatni dzień co miesiąc |
| <code>{monthDays":[1,-1]}</code> |Uruchamianych na powitania pierwszy i ostatni dzień co miesiąc, co godzina rozpoczęcia |
| <code>{monthDays":[1,14]}</code> |Uruchom na powitania pierwszy i czternasty dnia miesiąca co na czas rozpoczęcia |
| <code>{monthDays":[2]}</code> |Uruchom na powitania drugiego dnia hello miesiąca o godzinie czas rozpoczęcia |
| <code>{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |Uruchom w pierwszym piątek każdego miesiąca o godzinie 5: 00 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |: Uruchomienie na pierwszy piątek każdego miesiąca w momencie rozpoczęcia |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}</code> |Uruchom na trzeci piątek koniec miesiąca, co miesiąc, w momencie rozpoczęcia |
| <code>{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Uruchom na pierwszy i ostatni piątek miesiąca w 5:15:00 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Uruchomienie na pierwszy i ostatni piątek miesiąca w momencie rozpoczęcia |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}</code> |Uruchom w piątym piątek co miesiąc podczas uruchamiania. Jeśli w nie mają żadnych piątej piątek miesiąca nie działa, ponieważ jest toorun zaplanowane tylko piątej piątki. Można rozważyć użycie -1 zamiast 5 dla wystąpienia hello Jeśli zadanie hello toorun na powitania ostatniego wystąpienia piątek miesiąca hello. |
| <code>{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}</code> |Uruchom co 15 minut na ostatni piątek miesiąca hello |
| <code>{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}</code> |Uruchom na 5:15:00, 5:45:00, 17:15:00, a: 45 17 na hello 3 środa co miesiąc |

## <a name="see-also"></a>Zobacz też
 [Co to jest Scheduler?](scheduler-intro.md)

 [Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek](scheduler-concepts-terms.md)

 [Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure](scheduler-get-started-portal.md)

 [Plany i rozliczenia w usłudze Azure Scheduler](scheduler-plans-billing.md)

 [Dokumentacja interfejsu API REST usługi Azure Scheduler](https://msdn.microsoft.com/library/mt629143)

 [Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler](scheduler-powershell-reference.md)

 [Wysoka dostępność i niezawodność usługi Azure Scheduler](scheduler-high-availability-reliability.md)

 [Limity, wartości domyślne i kody błędów usługi Azure Scheduler](scheduler-limits-defaults-errors.md)

 [Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler](scheduler-outbound-authentication.md)

