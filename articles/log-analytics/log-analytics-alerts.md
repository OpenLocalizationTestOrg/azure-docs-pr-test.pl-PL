---
title: alerty aaaUnderstanding w Azure Log Analytics | Dokumentacja firmy Microsoft
description: "Alerty w analizy dzienników zidentyfikować ważne informacje zawarte w repozytorium OMS i aktywne powiadamia użytkownika o problemy lub wywołanie akcji tooattempt toocorrect je.  W tym artykule opisano hello różnych typów reguł alertów i jak są zdefiniowane."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: bfa0a5aaeca81674e79a6d647f36d937efeeb439
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-alerts-in-log-analytics"></a>Opis alertów w analizy dzienników

Alerty w analizy dzienników zidentyfikować ważne informacje zawarte w repozytorium analizy dzienników.  Ten artykuł przedstawia szczegóły alertu jak reguł w pracach analizy dzienników oraz hello różnice między różnych typów reguł alertów.

Hello procesu tworzenia reguł alertów Zobacz hello następujące artykuły:

- Tworzyć reguły alertów za pomocą [portalu Azure](log-analytics-alerts-creating.md)
- Tworzyć reguły alertów za pomocą [szablonu usługi Resource Manager](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md)
- Tworzyć reguły alertów za pomocą [interfejsu API REST](log-analytics-api-alerts.md)


## <a name="alert-rules"></a>Reguły alertów

Alerty są tworzone przez reguły alertów, które automatycznie uruchamiać dziennik wyszukiwania w regularnych odstępach czasu.  Jeśli wyniki wyszukiwania dziennika hello hello spełniających kryteria określonego tworzony jest rekord alertu.  Reguła Hello można następnie automatycznie uruchom jedno lub więcej tooproactively akcje powiadamiał hello alertu lub wywołać inny proces.  Różnych typów reguł alertów używać różnych logiki tooperform tej analizy.

![Alerty usługi Log Analytics](media/log-analytics-alerts/overview.png)

Reguły alertów są definiowane przez hello poniższe informacje:

- **Dziennik wyszukiwania**.  Witaj zapytania, które jest uruchamiane przy każdym generowane hello reguły alertów.  Hello rekordów zwróconych przez to zapytanie jest używane toodetermine, czy alert jest tworzony.
- **Przedział czasu**.  Określa zakres czasu hello hello zapytania.  Witaj zapytanie zwraca tylko te rekordy, które zostały utworzone w tym zakresie hello bieżącego czasu.  Może to być dowolna wartość od 5 minut do 24 godzin. Na przykład jeśli hello razem, gdy okno jest ustawione too60 minut, a zapytanie hello jest uruchamiane na 13:15:00, zwracany jest tylko rekordy między 12:15:00 a 13:15:00.
- **Częstotliwość**.  Określa, jak często hello zapytania powinny być uruchamiane. Może być dowolną wartość z zakresu od 5 minut do 24 godzin. Powinien być równy tooor poniżej hello przedział czasu.  Jeśli wartość hello jest większa niż przedział czasu hello, istnieje ryzyko rekordów jest pominięte.<br>Rozważmy na przykład okno czasu 30 minut i częstotliwość 60 minut.  Jeśli zapytanie hello jest uruchamiana 1:00, zwraca rekordów między 12:30 i 1:00 PM.  Witaj następnym będzie uruchamiane zapytanie hello jest 2:00, jeśli zwróci rekordów między 1:30 i 2:00.  Nigdy nie będzie można obliczyć wszystkie rekordy między 1:00 i 1:30.
- **Próg**.  Hello wyniki wyszukiwania dziennika hello są obliczane toodetermine, czy alert powinien zostać utworzony.  Próg Hello jest różne dla różnych typów hello reguł alertów.

Każdej reguły alertu w analizy dzienników jest jednym z dwóch typów.  Każdy z tych typów jest szczegółowo opisane w kolejnych sekcjach hello.

- **[Liczba wyników](#number-of-results-alert-rules)**. Pojedynczy alert utworzenia hello liczba rekordów zwróconych hello dziennik wyszukiwania przekracza podanej liczby.
- **[Metryki pomiaru](#metric-measurement-alert-rules)**.  Alert utworzony dla każdego obiektu w wynikach hello hello dziennik wyszukiwania z wartościami, które wykraczają poza określoną wartość progową.

dostępne są następujące Hello różnice między typami reguły alertów.

- **Liczba wyników** reguły alertu zawsze spowoduje utworzenie jednego alertu chwilę **metryki pomiaru** alertu zasada tworzy alert dla każdego obiektu, który przekracza próg hello.
- **Liczba wyników** reguły alertów tworzą alert po przekroczeniu progu hello jeden raz. **Metryki pomiaru** reguły alertów można utworzyć alertu, po przekroczeniu progu hello niektórych wiele razy w określonym interwale.

## <a name="number-of-results-alert-rules"></a>Liczba wyników reguły alertów
**Liczba wyników** reguły alertów Utwórz pojedynczy alert, gdy hello liczbę rekordów zwróconych przez zapytanie wyszukiwania hello przekracza określoną wartość progową hello.

### <a name="threshold"></a>Próg
Próg Hello **liczba wyników** reguły alertu jest po prostu większa lub mniejsza od określonej wartości.  Jeśli hello liczbę rekordów zwróconych przez wyszukiwania dziennika hello zgodne te kryteria, tworzona jest alert.

### <a name="scenarios"></a>Scenariusze

#### <a name="events"></a>Zdarzenia
Ten typ alertu jest idealne rozwiązanie w przypadku pracy z zdarzenia, takie jak dzienniki zdarzeń systemu Windows, Syslog, i niestandardowe dzienniki.  Podczas tworzenia pobiera zdarzeń określony błąd, lub wielu zdarzeń błędu są tworzone w ramach okna określonym czasie, może być toocreate alertu.

tooalert na pojedyncze zdarzenie, zestaw hello liczba wyników toogreater niż 0 i hello częstotliwość i czas okna too5 minut.  Co 5 minut i sprawdź, czy wystąpienie hello pojedyncze zdarzenie, który został utworzony, ponieważ hello ostatni czas hello zapytanie zostało uruchomione z systemem hello zapytania.  Częstotliwość dłużej może być opóźniona hello czas między hello zdarzeń jest zbierane i alert hello tworzona.

Niektóre aplikacje mogą rejestrować okazjonalne błąd, który nie należy koniecznie zgłosi alert.  Na przykład aplikacja hello może ponów hello procesu, który utworzył zdarzenie błędu hello i powiedzie się hello następnym razem.  W takim przypadku nie można toocreate hello alert chyba, że wiele zdarzeń są tworzone w ramach okna określonym czasie.  

W niektórych przypadkach może być toocreate alert w przypadku braku hello zdarzenia.  Na przykład procesu mogą rejestrować tooindicate regularnego zdarzenia, który działa prawidłowo.  Jeżeli nie rejestrować jedno z tych zdarzeń w oknie określonym czasie, powinien zostać utworzony alert.  W takim przypadku za należy ustawić próg hello**mniej niż 1**.

#### <a name="performance-alerts"></a>Alerty wydajności
[Dane dotyczące wydajności](log-analytics-data-sources-performance-counters.md) jest przechowywana jako rekordów w hello tooevents podobne repozytorium OMS.  Jeśli chcesz tooalert przekroczenia określonego progu licznika wydajności, progu powinny uwzględnione w zapytaniu hello.

Na przykład, jeśli chce tooalert podczas hello procesor uruchamia się za pośrednictwem 90%, należy użyć zapytania, takie jak hello zgodnie z progiem hello hello reguły alertu **większa niż 0**.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" CounterValue>90

Jeśli potrzebujesz tooalert, gdy procesor hello średnio ponad 90% okna określony czas, użyj zapytanie, używając hello [miar polecenia](log-analytics-search-reference.md#commands) hello następujących hello próg alertu hello, takich jak **większa niż 0 **.

    Type=Perf ObjectName=Processor CounterName="% Processor Time" | measure avg(CounterValue) by Computer | where AggregatedValue>90

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania zmieniłby toohello następujące:`Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" and CounterValue>90`
> `Perf | where ObjectName=="Processor" and CounterName=="% Processor Time" | summarize avg(CounterValue) by Computer | where CounterValue>90`


## <a name="metric-measurement-alert-rules"></a>Metryki pomiaru reguły alertów

>[!NOTE]
> Reguły alertów metryki pomiaru są obecnie w wersji zapoznawczej.

**Metryki pomiaru** reguły alertów tworzyć alert dla każdego obiektu w zapytaniu z wartością, która przekracza określoną wartość progową.  Mają one powitania po istotnymi różnicami z **liczba wyników** reguły alertów.

#### <a name="log-search"></a>Wyszukiwanie w dzienniku
Za pomocą dowolnego zapytania dla **liczba wyników** reguły alertu są określone wymagania hello zapytania dla metryki pomiaru reguły alertu.  Musi on zawierać [miar polecenia](log-analytics-search-reference.md#commands) toogroup hello wyniki według określonego pola. To polecenie musi zawierać następujące elementy hello.

- **Funkcję agregacji**.  Określa hello obliczeń, które jest wykonywane i potencjalnie tooaggregate pola numerycznego.  Na przykład **count()** zwróci hello liczby rekordów w zapytaniu hello **avg(CounterValue)** zwróci średnią hello pola równowartości hello przedziałach hello.
- **Pole grupy**.  Zostaje utworzony rekord z zagregowane wartości dla poszczególnych wystąpień tego pola, a alert jest generowany dla każdego.  Na przykład, jeśli chce toogenerate alert dla każdego komputera, czy używasz **przez komputer**.   
- **Interwał**.  Definiuje hello interwał czasu, przez który hello są agregowane.  Na przykład, jeśli określono **5minutes**, może zostać utworzony rekord dla każdego wystąpienia pole grupy hello przez hello przedział czasu określony dla alertu hello agregowana co 5 minut.

#### <a name="threshold"></a>Próg
Próg Hello metryki pomiaru reguły alertów jest definiowany przez wartości zagregowanej i liczbę naruszeń.  Dowolnego punktu danych w wyszukiwania dziennika hello przekracza tę wartość, jest uznawane za naruszenia.  Jeśli hello liczba naruszeń w dla dowolnego obiektu w wynikach hello przekracza hello określona wartość, a następnie alert jest tworzony dla tego obiektu.

#### <a name="example"></a>Przykład
Rozważmy scenariusz, w którym chce alert dowolnego komputera przekroczeniu użycie procesora przez 90% trzy razy ponad 30 minut.  Należy utworzyć regułę alertu z hello poniższe informacje.  

**Zapytanie:** typu = wydajności ObjectName = CounterName procesora = "% czasu procesora" | miar avg(CounterValue) interwał komputera 5 minut<br>
**Przedział czasu:** 30 minut<br>
**Alert częstotliwości:** 5 minut<br>
**Wartość agregacji:** dużą niż 90<br>
**Na podstawie wyzwalania alertu:** naruszeń łączna liczba jest większa niż 5<br>

Zapytanie Hello spowodowałoby średnią wartość dla każdego komputera co 5 minut.  To zapytanie zostanie uruchomione co 5 minut dla danych zbieranych za pośrednictwem hello poprzednich 30 minut.  Poniżej przedstawiono przykładowe dane na trzech komputerach.

![Przykładowe wyniki zapytania](media/log-analytics-alerts/metrics-measurement-sample-graph.png)

W tym przykładzie oddzielne alerty zostałyby utworzone dla srv02 i srv03, ponieważ ich naruszenia progu 90% hello 3 razy za pośrednictwem hello przedział czasu.  Jeśli hello **na podstawie wyzwalania alertu:** zmieniono zbyt**kolejno** , a następnie alert będzie można utworzyć tylko dla srv03, ponieważ jego naruszony hello próg 3 kolejne próbki.

## <a name="alert-records"></a>Rejestruje alertu
Rekordy alertu przez reguły alertów w analizy dzienników mają **typu** z **Alert** i **SourceSystem** z **OMS**.  Mają one właściwości hello w hello w poniższej tabeli.

| Właściwość | Opis |
|:--- |:--- |
| Typ |*Alert* |
| SourceSystem |*OMS* |
| *Obiekt*  | [Alerty metryki pomiaru](#metric-measurement-alert-rules) ma właściwość hello pola grupy.  Na przykład jeśli wyszukiwania dziennika hello grup na komputerze, hello rekord z ma pole komputera o nazwie hello hello komputera jako wartość hello alertu.
| AlertName |Nazwa alertu hello. |
| AlertSeverity |Poziom ważności alertu hello. |
| LinkToSearchResults |Łącze tooLog analizy dziennika wyszukiwania, które zwraca hello rekordów w kwerendzie hello utworzony hello alert. |
| Zapytanie |Tekst zapytania hello, która została uruchomiona. |
| QueryExecutionEndTime |Koniec hello zakres czasu dla hello zapytania. |
| QueryExecutionStartTime |Początek hello zakres czasu dla hello zapytania. |
| ThresholdOperator | Operator, który został użyty przez regułę alertu hello. |
| ThresholdValue | Wartość, która była używana przez regułę alertu hello. |
| TimeGenerated |Data i godzina hello alert został utworzony. |

Istnieją inne rodzaje rekordy alertu przez hello [rozwiązania do zarządzania Alert](log-analytics-solution-alert-management.md) oraz [eksportuje usługi Power BI](log-analytics-powerbi.md).  Te wszystkie mają **typu** z **alertu** , ale można rozróżnić za ich **SourceSystem**.


## <a name="next-steps"></a>Następne kroki
* Zainstaluj hello [rozwiązania zarządzania alertami](log-analytics-solution-alert-management.md) zbierane alerty tooanalyze utworzone w analizy dzienników oraz alertów programu System Center Operations Manager.
* Przeczytaj więcej na temat [dziennika wyszukiwania](log-analytics-log-searches.md) który generowania alertów.
* Zakończenie wskazówki dla [Konfigurowanie webook](log-analytics-alerts-webhooks.md) z reguły alertu.  
* Dowiedz się, jak toowrite [elementy runbook automatyzacji Azure](https://azure.microsoft.com/documentation/services/automation) problemów tooremediate identyfikowana na podstawie alertów.
