---
title: "Odwołanie wyszukiwania aaaAzure Log Analytics | Dokumentacja firmy Microsoft"
description: "Odwołanie wyszukiwania analizy dzienników Hello opisuje hello wyszukiwania języka i zawiera opcje składni zapytania ogólne hello, używanych podczas wyszukiwania danych i filtrowania toohelp wyrażenia zawęzić kryteria wyszukiwania."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 402615a2-bed0-4831-ba69-53be49059718
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7478a1139b88a1ce76ebb7b76027a6ccd66f4f27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-search-reference"></a>Odwołanie wyszukiwania analizy dzienników

>[!NOTE]
> W tym artykule opisano dziennik wyszukiwania przy użyciu hello bieżący język zapytań w analizy dzienników.  Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie należy zapoznać się zbyt[hello dokumentacja języka dla nowego języka hello](https://go.microsoft.com/fwlink/?linkid=856079).

Witaj następującą sekcję informacyjną dotyczące języków wyszukiwania opisano hello kwerendy ogólne składni opcje używanych podczas wyszukiwania danych i filtrowania toohelp wyrażenia zawęzić kryteria wyszukiwania. Omówiono także poleceń na pobrane dane hello można tootake akcji.

Informacje o pola hello zwracane w wynikach wyszukiwania i hello aspektów, które ułatwiają Dowiedz się więcej o kategoriach podobne danych w hello [pola wyszukiwania i aspekt odwoływać sekcji](#search-field-and-facet-reference).

## <a name="general-query-syntax"></a>Składnia zapytania ogólne
Witaj zapytań ogólne ma następującą składnię:

```
filterExpression | command1 | command2 …
```

Witaj wyrażenie filtru (`filterExpression`) definiuje hello warunku "where" dla hello zapytania. polecenia Hello stosowane toohello wyników zwróconych przez zapytanie hello. Wiele poleceń muszą być oddzielone hello znaku kreski pionowej (|).

### <a name="general-syntax-examples"></a>Przykłady składni ogólnej
Przykłady:

```
system
```

Ta kwerenda zwraca wyniki zawierające słowo hello *systemu* w każde pole, które zostały zindeksowane dla pełnotekstowego lub warunki wyszukiwania.

> [!NOTE]
> Nie wszystkie pola są indeksowane w ten sposób, ale są najczęściej tekstowej pola (na przykład nazwy i opisy) zwykle hello.
>
>

```
system error
```

Ta kwerenda zwraca wyniki zawierające słowa hello *systemu* i *błąd*.

```
system error | sort ManagementGroupName, TimeGenerated desc | top 10
```

Ta kwerenda zwraca wyniki zawierające słowa hello *systemu* i *błąd*. Następnie sortuje hello wyniki według hello *ManagementGroupName* pola (rosnąco), a następnie według hello *TimeGenerated* (w kolejności malejącej). Trwa hello tylko 10 pierwszych wyników.

> [!IMPORTANT]
> Witaj wszystkie nazwy pól i wartości hello pól ciągów i tekst hello jest uwzględniana wielkość liter.
>
>

## <a name="filter-expressions"></a>Wyrażenia filtru
następujące podpunkty Hello opisano hello wyrażenia filtru.

### <a name="string-literals"></a>Literały ciągu
Literał ciągu jest dowolny ciąg, który nie jest rozpoznawany przez hello parser jako słowo kluczowe lub typu danych wstępnie zdefiniowane (na przykład, liczby lub daty).

Przykłady:

```
These all are string literals
```

To zapytanie szuka wyniki zawierające wystąpienia wszystkich pięciu wyrazów. tooperform złożonych ciąg wyszukiwania, należy ująć w znaki cudzysłowu literału ciągu znaków hello. Na przykład:

```
"Windows Server"
```

To polecenie zwróci tylko wyniki z dokładne dopasowania dla *systemu Windows Server*.

### <a name="numbers"></a>Numery
Hello parser obsługuje hello dziesiętną liczbą całkowitą i składni liczb zmiennoprzecinkowych dla pól wartości liczbowych.

Przykłady:

```
Type:Perf 0.5
```

```
HTTP 500
```

### <a name="dates-and-times"></a>Daty i godziny
Każdy element danych w systemie hello ma *TimeGenerated* właściwość, która reprezentuje hello pierwotna data i godzina hello rekordu. Niektóre typy danych mogą mieć dodatkowe Data i godzina (na przykład *LastModified*).

Witaj osi czasu **wykresu/godzina** selektora w Analiza dzienników Azure zawiera dystrybucji wyników wraz z upływem czasu (zgodnie z toohello bieżącego zapytania uruchamiane). To jest oparta na powitania *TimeGenerated* pola. Data i godzina pola mają określony ciąg formatu, który może być używana w zapytania toorestrict hello zapytania tooa określonym przedziale czasu. Umożliwia także przedziały czasu toorelative toorefer składni (na przykład "między 3 dni temu i 2 godz. temu").

Witaj poniżej przedstawiono prawidłowe formularze składni dat i godzin:

```
yyyy-mm-ddThh:mm:ss.dddZ
```

```
yyyy-mm-ddThh:mm:ss.ddd
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm:ss
```

```
yyyy-mm-ddThh:mm
```

```
yyyy-mm-dd
```


Na przykład:

```
TimeGenerated:2013-10-01T12:20
```

Witaj poprzednie polecenie zwraca tylko rekordy z *TimeGenerated* wartości dokładnie 12:20 na 1 października 2013.

Hello parser obsługuje również hello skrótu wartości daty/godziny, teraz. (Jest mało prawdopodobne, że da żadnych wyników, ponieważ nie była danych za pośrednictwem systemu hello to szybkie.)

Te przykłady są blokami konstrukcyjnymi toouse dat względnych i bezwzględnych. W hello trzech kolejnych podsekcjach, zobaczysz, jak toouse je w bardziej zaawansowane filtry, wraz z przykładami, korzystających z zakresów względnej daty.

### <a name="datetime-math"></a>Data/Godzina matematyczne
Użyj toooffset operatory matematyczne daty/godziny hello lub zaokrąglona hello wartości daty/godziny, przy użyciu prostych obliczeń daty/godziny.

Składnia:

```
datetime/unit
```

```
datetime[+|-]count unit
```

| Operator | Opis |
| --- | --- |
| / |Zaokrągla liczbę toohello daty/godziny określone jednostki. Na przykład teraz / dzień zaokrągla hello bieżącego toomidnight daty/godziny hello bieżącego dnia. |
| + lub - |Przesunięcia daty/godziny przez hello określić liczbę jednostek. Na przykład teraz + 1 godzina przesunięciami hello bieżącej daty/godziny, o godzinę wyprzedzeniem. 2013-10-01T12:00-10 dni przesunięcia wartości typu Date hello przez 10 dni. |

Operatory matematyczne daty/godziny hello można powiązane ze sobą. Na przykład:

```
NOW+1HOUR-10MONTHS/MINUTE
```

Witaj poniższej tabeli wymieniono obsługiwane hello jednostek daty/godziny.

| Jednostka daty/godziny | Opis |
| --- | --- |
| YEAR, YEARS |Zaokrąglenie toocurrent rok ani przesunięcia przez hello określono kilka lat temu. |
| MIESIĄC, MIESIĘCY |Zaokrąglenie toocurrent miesiąc lub przesunięcia przez hello określona liczba miesięcy. |
| DZIEŃ, DNI, DATA |Zaokrąglenie toocurrent dzień miesiąca hello lub przesunięcia przez hello określonej liczby dni. |
| GODZINA, GODZINY |Zaokrąglenie toocurrent godzinę lub przesunięcia przez hello określić liczbę godzin. |
| MINUTA, MINUT |Zaokrąglenie toocurrent minutę lub przesunięcia przez hello określić liczbę minut. |
| SECOND, SECONDS, |Zaokrągla toocurrent drugi lub przesunięcia przez hello określona liczba sekund. |
| MILISEKUNDY MILISEKUND, MILLI, MILLIS |Zaokrągla liczbę milisekund toocurrent lub przesunięcia przez hello określony liczbę milisekund. |

### <a name="field-facets"></a>Aspekty pola
Za pomocą pola aspektów, można określić warunku wyszukiwania hello określonych pól i ich dokładne wartości. To różni się od Pisanie zapytań "wolne tekst" dla różnych warunków w całym indeksie hello. Ta technika w poprzednich przykładach kilka ma już widoczne. Witaj poniżej przedstawiono przykłady bardziej złożonych.

**Składnia**

```
field:value
```

```
field=value
```

**Opis**

Wyszukiwanie hello pola hello określonej wartości. wartość Hello może być literał ciągu, numer, lub Data i godzina.

Na przykład:

```
TimeGenerated:NOW
```

```
ObjectDisplayName:"server01.contoso.com"
```

```
SampleValue:0.3
```

**Składnia**

*pole > wartość*

*pole < wartość*

*pole > = wartość*

*pole < = wartość*

*pole! = wartość*

**Opis**

Udostępnia porównania.

Na przykład:

```
TimeGenerated>NOW+2HOURS
```

**Składnia**

```
field:[from..to]
```

**Opis**

Umożliwia tworzenie aspektów zakresu.

Na przykład:

```
TimeGenerated:[NOW..NOW+1DAY]
```

```
SampleValue:[0..2]
```

### <a name="in"></a>W
Witaj **IN** — słowo kluczowe umożliwia tooselect z listy wartości. W zależności od składni hello używasz może to być to prosta lista wartości, który podasz lub listę wartości z agregacji.

Składnia 1:

```
field IN {value1,value2,value3,...}
```

Tej składni pozwala tooinclude wszystkie wartości na liście proste.



Przykłady:

```
EventID IN {1201,1204,1210}
```

```
Computer IN {"srv01.contoso.com","srv02.contoso.com"}
```

Składnia 2:

```
(Outer query) (Field toouse with inner query results) IN {Inner query | measure count() by (Field toosend tooouter query)} (rest  of outer query)  
```

Tej składni pozwala toocreate agregacji. Może następnie dostarczyć hello listę wartości z tej agregacji w innym zewnętrzne wyszukiwania (podstawowe), sprawdzający zdarzenia z tych wartości. W tym celu otaczającej hello wewnętrzny wyszukiwania w nawiasach klamrowych i skierowanie wyniki jako możliwe wartości dla pola w hello zewnętrzne wyszukiwania za pomocą operatora IN hello.

Przykład wewnętrzny zapytania: *komputerów obecnie brakujących aktualizacji zabezpieczeń* z następującego zapytania agregacji hello:

```
Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer
```    

Hello końcowego kwerendę, która wyszukuje *wszystkie zdarzenia systemu Windows dla komputerów, w obecnie brakujących aktualizacji zabezpieczeń* podobne hello następującego:

```
Type=Event Computer IN {Type:Update Classification="Security Updates"  UpdateState=needed TimeGenerated>NOW-25HOURS | measure count() by Computer}
```

### <a name="contains"></a>Contains
Witaj **zawiera** — słowo kluczowe umożliwia toofilter rekordów z polem, który zawiera określony ciąg. To jest rozróżniana wielkość liter, działa tylko w przypadku pól ciągów i nie może zawierać żadnych znaków ucieczki.

Składnia:

```
field:contains("string")
```

Przykład:

```
Type:contains("Event")
```

To polecenie zwróci rekordy z typem, który zawiera ciąg hello "Event". Przykłady obejmują **zdarzeń**, **SecurityEvent**, i **ServiceFabricOperationEvent**.



### <a name="regular-expressions"></a>Wyrażenia regularne
Można określić warunku wyszukiwania dla pola z wyrażeniem regularnym, za pomocą hello **Regex** — słowo kluczowe. Pełny opis składni hello można używać w wyrażeniach regularnych, zobacz [za pomocą wyrażeń regularnych toofilter dziennik wyszukiwania w analizy dzienników](log-analytics-log-searches-regex.md).

Składnia:

```
field:Regex("Regular Expression")
```

Przykład:

```
Computer:Regex("^C.*")
```

### <a name="logical-operators"></a>Operatory logiczne
języki obsługiwane przez operatorów logicznych hello zapytania Hello (*i*, *lub*, i *nie*) i ich aliasy w stylu języka C (*&&*,  *||* , i *!*odpowiednio). Można użyć tych operatorów toogroup nawiasów.

Przykłady:

```
system OR error

```

```
Type:Alert AND NOT(Severity:1 OR ObjectId:"8066bbc0-9ec8-ca83-1edc-6f30d4779bcb8066bbc0-9ec8-ca83-1edc-6f30d4779bcb")
```

Można pominąć hello operatora logicznego hello argumentów filtru najwyższego poziomu. W takim przypadku hello AND operator zakłada, że.

| Wyrażenie filtru | Odpowiednik zbyt|
| --- | --- |
| Błąd systemu: |System i błędów |
| System "Windows Server" lub ważność: 1 |System i ("Windows Server" lub ważność: 1) |

### <a name="wildcarding"></a>Symbole wieloznaczne
język zapytań Hello obsługuje przy użyciu hello ( \* ) znaków zbyt reprezentuje jeden lub więcej znaków wartości w zapytaniu.

Przykład:

 Znajdź wszystkie komputery z "SQL" w nazwie hello, takie jak "Redmond SQL".

```
Type=Event Computer=*SQL*
```

> [!NOTE]
> W tej chwili nie można używać symboli wieloznacznych w cudzysłowach. Na przykład wiadomości powitania `"*This text*"` uwzględnia hello (\*) używane jako literału (\*) znaków.


## <a name="commands"></a>Polecenia


polecenia Hello stosowane toohello wyniki zwrócone przez zapytanie hello. Użyj hello potoku znaków (|) tooapply toohello polecenia pobrać wyników. Wiele poleceń muszą być oddzielone hello znaku kreski pionowej.

> [!NOTE]
> Nazwy poleceń można pisać w wielkie lub małe litery, w odróżnieniu od nazw pól hello i hello danych.
>
>

### <a name="sort"></a>Sortuj
Składnia:

    sort field1 asc|desc, field2 asc|desc, …

Sortuje hello wyniki według określonego pola. Witaj sufiks asc/desc toosort hello wyniki w kolejności rosnącej lub malejącej jest opcjonalna. Jeśli zostanie pominięty, hello *asc* zakłada, że kolejność sortowania. Dla hello **TimeGenerated** pola *desc* zakłada się porządek sortowania, więc najpierw zwraca wyniki ostatniej hello domyślnie.

### <a name="toplimit"></a>TOP/Limit
Składnia:

    top number


    limit number
Limity hello odpowiedzi toohello top N wyników.

Przykład:

    Type:Alert errors detected | top 10

Zwraca hello 10 pierwszych zgodnych wyników.

### <a name="skip"></a>Pomiń
Składnia:

    skip number

Pomija hello liczba wyników na liście.

Przykład:

    Type:Alert errors detected | top 10 | skip 200

Zwraca górny 10 pasujących wyników zaczynając od wyniku 200.

### <a name="select"></a>Wybierz pozycję
Składnia:

    select field1, field2, ...

Ogranicza wyniki toohello pola, które można wybrać.

Przykład:

    Type:Alert errors detected | select Name, Severity

Limity hello pól wyników zwróconych zbyt*nazwa* i *ważność*.

### <a name="measure"></a>Miary
Witaj *miary* polecenia jest używane tooapply funkcji statystycznych toohello pierwotnych wyników. Jest to bardzo przydatne tooget *Grupuj według* widoków danych hello. Po użyciu polecenia miary hello, analizy dzienników zostanie wyświetlona tabela z wyników zagregowany.

**Składnia:**

    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]] by groupField1 [, groupField2 [, groupField3]]  [interval interval]


    measure aggregateFunction1([aggregatedField]) [as fieldAlias1] [, aggregateFunction2([aggregatedField2]) [as fieldAlias2] [, ...]]  interval interval



Agreguje wyniki hello według *groupField*i oblicza hello agregowane wartości miary za pomocą *aggregatedField*.

| Funkcja statystyczne miary | Opis |
| --- | --- |
| *Funkcja aggregateFunction* |Nazwa Hello hello funkcji agregującej (bez uwzględniania wielkości liter). obsługiwane są następujące funkcje agregujące Hello: COUNT, MAX, MIN, SUM, AVG, STDDEV, COUNTDISTINCT, percentyl ## lub PCT ## (## jest liczbą zakresu od 1 do 99). |
| *aggregatedField* |pole Hello jest agregowanie. To pole jest opcjonalne dla hello liczba funkcji agregującej, ale ma toobe istniejącego pola liczbowego SUM, MAX, MIN, AVG, STDDEV, percentyl ## lub PCT ## (## jest liczbą zakresu od 1 do 99). Witaj aggregatedField również może być hello **Rozszerz** obsługiwanych funkcji. |
| *fieldAlias* |(opcjonalnie) alias hello Hello obliczana wartość zagregowana. Jeśli nie zostanie określony, nazwa pola hello jest **AggregatedValue**. |
| *groupField* |Nazwa Hello hello pola, które zestaw wyników hello są grupowane według. |
| *Interwał* |Interwał czasowy Hello, w formacie hello:**nnnNAME**. **nnn**jest hello dodatnią liczbą całkowitą. **Nazwa** jest nazwą interwał hello. Nazwy obsługiwany interwał jest uwzględniana wielkość liter i obejmują: MILISEKUNDY [S] sekundy [S] MINUTĘ [S] z godziny [S] dnia [S] [S] miesiąca i roku [S]. |

Opcja zakresu Hello jest możliwe tylko w polach grupy daty/godziny (takich jak *TimeGenerated* i *TimeCreated*). Obecnie to nie jest wymuszana przez usługę hello, ale pole bez daty i godziny przekazywane zaplecza toohello powoduje błąd w czasie wykonywania. Po zaimplementowaniu sprawdzanie poprawności schematu hello interfejsu API usługi hello odrzuca zapytań, które pola bez daty/godziny na użytek interwał agregacji. Bieżący Hello *miary* implementacja obsługuje grupowania interwał funkcji agregacji.

W przypadku pominięcia klauzuli BY hello, ale podano interwału (jako drugi składni), hello *TimeGenerated* pola przyjęto, że domyślnie.

Przykłady:

**Przykład 1**

    Type:Alert | measure count() as Count by ObjectId

Grupy hello alertów według *ObjectID*i oblicza hello liczbę alertów dla każdej grupy. Witaj zagregowane wartości jest zwracana jako hello *liczba* pola (alias).

**Przykład 2**

    Type:Alert | measure count() interval 1HOUR

Grupy hello alerty przez 1 godzinę przy użyciu hello *TimeGenerated* pola i zwraca hello liczbę alertów w każdym interwale.

**Przykład 3**

    Type:Alert | measure count() as AlertsPerHour interval 1HOUR

Jako hello w poprzednim przykładzie, ale z aliasem pola zagregowane (*AlertsPerHour*).

**Przykład 4**

    * | Miara count() przez 5DAYS interwał TimeCreated

Grupuje wyniki hello przez 5 dni przy użyciu hello *TimeCreated* pola i zwraca hello liczbę wyników w każdym interwale.

**Przykład 5**

    Type:Alert | measure max(Severity) by WorkflowName

Grupy hello alerty według nazwy obciążenia i zwraca hello ważność alertu maksymalną wartość dla każdego przepływu pracy.

**Przykład 6**

    Type:Alert | measure min(Severity) by WorkflowName

Jako hello w poprzednim przykładzie, ale z hello *min* zagregowane funkcji.

**Przykład 7**

    Type:Perf | measure avg(CounterValue) by Computer

Grupuje wydajności przez komputer, a następnie oblicza średnią hello (średni).

**Przykład 8**

    Type:Perf | measure sum(CounterValue) by Computer

Sam, jak poprzedni przykład Witaj, ale używa *suma*.

**Przykład 9**

    Type:Perf | measure stddev(CounterValue) by Computer

Sam, jak poprzedni przykład Witaj, ale używa *stddev*.

**Przykład 10**

    Type:Perf | measure percentile70(CounterValue) by Computer

Sam, jak poprzedni przykład Witaj, ale używa *percentile70*.

**Przykład 11**

    Type:Perf | measure pct70(CounterValue) by Computer

Sam, jak poprzedni przykład Witaj, ale używa *pct70*. Należy pamiętać, że *PCT ##* jest tylko aliasu dla *percentyl ##* funkcji.

**Przykład 12**

    Type:Perf | measure avg(CounterValue) by Computer, CounterName

Grupuje wydajności najpierw przez komputer, a następnie CounterName i oblicza średnią hello (średni).

**Przykład 13**

    Type:Alert | measure count() as Count by WorkflowName | sort Count desc | top 5

Pobiera hello top pięć przepływy pracy z hello maksymalną liczbę alertów.

**Przykład 14**

    * | Miara countdistinct(Computer) według typu

Zlicza hello unikatowych komputerów raportowania dla każdego typu.

**Przykład 15**

    * | Miara countdistinct(Computer) interwał 1 godzina

Zlicza hello unikatowych komputerów raportowania co godzinę.

**Przykład 16**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total” | measure avg(CounterValue) by Computer Interval 1HOUR
```

Grupuje % czasu procesora przez komputer i zwraca hello średnia dla każdej godziny.

**Przykład 17**

    Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES

Grupuje W3CIISLog przez metodę i zwraca maksymalny hello co 5 minut.

**Przykład 18**

```
Type:Perf CounterName=”% Processor Time” InstanceName=”_Total”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer Interval 1HOUR
```

Grupy % czasu procesora komputera i zwraca hello minimum, średnia 75 percentyl i maksymalną wartość dla co godzinę.

**Przykład 19**

```
Type:Perf CounterName=”% Processor Time”  | measure min(CounterValue) as MIN, avg(CounterValue) as AVG, percentile75(CounterValue) as PCT75, max(CounterValue) as MAX by Computer, InstanceName Interval 1HOUR
```

Grup % czasu procesora najpierw według komputera, a następnie wystąpienia nazwy i zwraca hello minimum, Średni, 75. percentyl, a maksymalną wartość dla co godzinę.

**Przykład 20**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | measure max(product(CounterValue,60)) as MaxDWPerMin by InstanceName Interval 1HOUR
```

Oblicza maksymalną hello na minutę dla każdego dysku operacji zapisu na dysku na tym komputerze.

### <a name="where"></a>gdzie
Składnia:

```
**where** AggregatedValue>20
```

Można używać tylko po *miary* hello filtru toofurther polecenia zagregowane wyniki tego hello *miary* opracowała funkcji agregacji.

Przykłady:

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) as MAXCPU by Computer

    Type:Perf CounterName:"% Total Run Time" | Measure max(CounterValue) by Computer | where (AggregatedValue>50 and AggregatedValue<90)



### <a name="dedup"></a>Funkcja deduplikacji
Składnia:

    Dedup FieldName

Zwraca pierwszy dokument hello znaleziono dla każdej unikatowej wartości hello podane pole.

Przykład:

    Type=Event | Dedup EventID | sort TimeGenerated DESC

W tym przykładzie zwraca jedno zdarzenie (hello najnowsze zdarzenie) na identyfikator zdarzenia.

### <a name="join"></a>Join
Sprzężenia hello wyniki tooform dwa zapytania pojedynczy wyników.  Obsługuje wiele typów sprzężeń opisanego w hello postępuj zgodnie z tabeli.

| Typ sprzężenia | Opis |
|:--|:--|
| wewnętrzny | Zwraca tylko rekordów o pasującej wartości w obu zapytania. |
| zewnętrzne | Zwraca wszystkie rekordy z obu zapytań.  |
| Po lewej  | Zwraca wszystkie rekordy z lewym zapytań i pasujące rekordy z prawej zapytania. |


- Sprzężenia nie obsługują aktualnie zapytania, które zawierają hello **w** — słowo kluczowe, hello **miary** polecenia lub hello **Rozszerz** polecenia, jeśli elementem docelowym pola z hello prawo kwerendy.
- Obecnie można uwzględnić tylko jedno pole sprzężenia.
- Pojedynczy wyszukiwania nie może zawierać więcej niż jedno połączenie.

**Składnia**

```
<left-query> | JOIN <join-type> <left-query-field-name> (<right-query>) <right-query-field-name>
```

**Przykłady**

tooillustrate hello sprzężenia różnych typów, należy rozważyć dołączenie typu danych zbieranych z dziennik niestandardowy o nazwie MyBackup_CL z hello pulsu dla każdego komputera.  Te typy danych mają powitania po danych.

`Type = MyBackup_CL`

| TimeGenerated | Computer (Komputer) | LastBackupStatus |
|:---|:---|:---|
| 2017-4/20 01:26:32.137 AM | SRV01.contoso.com | Powodzenie |
| 2017-4/20 02:13:12.381 AM | SRV02.contoso.com | Powodzenie |
| 2017-4/20 02:13:12.381 AM | srv03.contoso.com | Niepowodzenie |

`Type = Hearbeat`(Tylko podzestaw pokazane pola)

| TimeGenerated | Computer (Komputer) | ComputerIP |
|:---|:---|:---|
| 2017-4/21 12:01:34.482 PM. | SRV01.contoso.com | 10.10.100.1 |
| 2017-4/21 12:02:21.916 PM. | SRV02.contoso.com | 10.10.100.2 |
| 2017-4/21 12:01:47.373 PM. | srv04.contoso.com | 10.10.100.4 |

#### <a name="inner-join"></a>sprzężenie wewnętrzne

`Type=MyBackup_CL | join inner Computer (Type=Heartbeat) Computer`

Zwraca hello następujące rekordy, jeśli pole komputera hello odpowiada dla obu typów danych.

| Computer (Komputer)| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| SRV01.contoso.com | 2017-4/20 01:26:32.137 AM | Powodzenie | 2017-4/21 12:01:34.482 PM. | 10.10.100.1 | Pulsu |
| SRV02.contoso.com | 2017-4/20 02:13:12.381 AM | Powodzenie | 2017-4/21 12:02:21.916 PM. | 10.10.100.2 | Pulsu |


#### <a name="outer-join"></a>sprzężenie zewnętrzne

`Type=MyBackup_CL | join outer Computer (Type=Heartbeat) Computer`

Zwraca hello następujące rekordy dla obu typów danych.

| Computer (Komputer)| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| SRV01.contoso.com | 2017-4/20 01:26:32.137 AM | Powodzenie  | 2017-4/21 12:01:34.482 PM. | 10.10.100.1 | Pulsu |
| SRV02.contoso.com | 2017-4/20 02:14:12.381 AM | Powodzenie  | 2017-4/21 12:02:21.916 PM. | 10.10.100.2 | Pulsu |
| srv03.contoso.com | 2017-4/20 01:33:35.974 AM | Niepowodzenie  | 2017-4/21 12:01:47.373 PM. | | |
| srv04.contoso.com |                           |          | 2017-4/21 12:01:47.373 PM. | 10.10.100.2 | Pulsu |



#### <a name="left-join"></a>Lewe sprzężenie

`Type=MyBackup_CL | join left Computer (Type=Heartbeat) Computer`

Zwraca hello następujące rekordy z MyBackup_CL z żadnych pól zgodnych z pulsu.

| Computer (Komputer)| TimeGenerated | LastBackupStatus | TimeGenerated_joined | ComputerIP_joined | Type_joined |
|:---|:---|:---|:---|:---|:---|
| SRV01.contoso.com | 2017-4/20 01:26:32.137 AM | Powodzenie | 2017-4/21 12:01:34.482 PM. | 10.10.100.1 | Pulsu |
| SRV02.contoso.com | 2017-4/20 02:13:12.381 AM | Powodzenie | 2017-4/21 12:02:21.916 PM. | 10.10.100.2 | Pulsu |
| srv03.contoso.com | 2017-4/20 02:13:12.381 AM | Niepowodzenie | | | |


### <a name="extend"></a>Rozszerzanie
Umożliwia toocreate pola czasu wykonywania zapytania. Należy pamiętać, że nie można używać pól czasu wykonywania z hello miary polecenia tooperform agregacji.

**Przykład 1**

    Type=SQLAssessmentRecommendation | Extend product(RecommendationScore, RecommendationWeight) AS RecommendationWeightedScore
Pokazuje ważone wynik zalecenie zalecenia SQL do oceny.

**Przykład 2**

    Type=Perf CounterName="Private Bytes" | EXTEND div(CounterValue,1024) AS KBs | Select CounterValue,Computer,KBs
Zawiera wartość licznika w KB/s, zamiast bajtów.

**Przykład 3**

    Type=WireData | EXTEND scale(TotalBytes,0,100) AS ScaledTotalBytes | Select ScaledTotalBytes,TotalBytes | SORT TotalBytes DESC
Skaluje hello wartość WireData TotalBytes w taki sposób, że wszystkie wyniki należą do zakresu od 0 do 100.

**Przykład 4**

```
Type=Perf CounterName="% Processor Time" | EXTEND if(map(CounterValue,0,50,0,1),"HIGH","LOW") as UTILIZATION
```
Znaczniki wartości liczników wydajności mniej niż 50 procent jako niski, a inne jako wysoki.

**Przykład 5**

```
Type= Perf CounterName="Disk Writes/sec" Computer="BaconDC01.BaconLand.com" | Extend product(CounterValue,60) as DWPerMin| measure max(DWPerMin) by InstanceName Interval 1HOUR
```
Oblicza maksymalną hello na minutę dla każdego dysku operacji zapisu na dysku na tym komputerze.

**Obsługiwane funkcje**

| Funkcja | Opis | Przykłady składni |
| --- | --- | --- |
| ABS |Zwraca wartość bezwzględną hello hello określonej wartości lub funkcji. |`abs(x)` <br> `abs(-5)` |
| ACOS |Zwraca arcus cosinus wartości lub funkcji. |`acos(x)` |
| i |Zwraca wartość true tylko wtedy, gdy wszystkie argumentów oceny tootrue. |`and(not(exists(popularity)),exists(price))` |
| ASIN |Zwraca arcus sinus wartości lub funkcji. |`asin(x)` |
| ATAN |Zwraca arcus tangens wartości lub funkcji. |`atan(x)` |
| ATAN2 |Zwraca kąt hello wyniku konwersji hello hello prostokątna współrzędne x, y toopolar współrzędnych. |`atan2(x,y)` |
| cbrt — |Główny moduł. |`cbrt(x)` |
| ceil |Zaokrągla liczbę w górę tooan liczby całkowitej. |`ceil(x)`  <br> `ceil(5.6)`Zwraca 6 |
| COS |Zwraca cosinus kąta. |`cos(x)` |
| COSH |Zwraca cosinus hiperboliczny kąta. |`cosh(x)` |
| DEF |Skrót dla domyślnego. Zwraca hello wartość pola "pola". Jeśli pole hello nie istnieje, zwraca hello domyślna wartość określona i zwraca pierwszą wartość hello gdzie: `exists()==true`. |`def(rating,5)`. Ta funkcja def() zwraca hello klasyfikacji lub jeśli klasyfikacji nie jest określona w dokumencie hello zwraca 5. <br> `def(myfield, 1.0)`odpowiada za`if(exists(myfield),myfield,1.0)`. |
| stopni |Konwertuje wartość w radianach toodegrees. |`deg(x)` |
| DIV |`div(x,y)`dzieli x przez y. |`div(1,y)` <br> `div(sum(x,100),max(y,1))` |
| dystr. |Zwraca hello odległość między dwoma wektorami, (punkty) w n wymiarowej miejsca. Przyjmuje hello zasilania, a także wystąpień ValueSource dwóch lub więcej i oblicza hello odległości między dwoma wektorami hello. Każdy ValueSource musi być liczbą. Musi być parzystą liczbą wystąpień ValueSource przekazano i hello — metoda przyjęto założenie, że hello pierwszej połowie reprezentują wektor pierwszy hello i drugiej połowie hello reprezentują wektor drugi hello. |`dist(2, x, y, 0, 0)`Oblicza odległość euklidesowa hello między (0,0) i (x, y) dla każdego dokumentu. <br> `dist(1, x, y, 0, 0)`Oblicza odległość Manhattan (taxicab) hello między (0,0) i (x, y) dla każdego dokumentu. <br> `dist(2,,x,y,z,0,0,0)`Euklidesowa odległość między (0,0,0) i (x, y, z) dla każdego dokumentu.<br>`dist(1,x,y,z,e,f,g)`Manhattan odległość między (x, y, z) i (e, f, g), gdzie każda litera jest nazwą pola. |
| istnieje |Zwraca wartość TRUE, jeśli element członkowski pola hello istnieje. |`exists(author)`Zwraca wartość TRUE dla każdego dokumentu, który ma wartość w polu "Autor" hello.<br>`exists(query(price:5.00))`Zwraca wartość TRUE, jeśli pasuje do "cena", "5.00". |
| EXP |Zwraca Eulera numer wywoływane toopower x. |`exp(x)` |
| FLOOR |Zaokrągla liczbę w dół do liczby całkowitej tooan. |`floor(x)`  <br> `floor(5.6)`Zwraca 5 |
| hypo |Zwraca sqrt(sum(pow(x,2),pow(y,2))) bez pośredniego przepełnienie lub niedomiar. |`hypo(x,y)`  <br> ` |
| Jeśli |Umożliwia funkcja warunkowy zapytania. W `if(test,value1,value2)`, test jest lub odwołuje się tooa wartość logiczna lub wyrażenie, które zwraca wartość logiczną (TRUE lub FALSE). `value1`jest przez funkcję hello hello wartość zwracana, jeśli test daje w wyniku wartość TRUE. `value2`jest przez funkcję hello hello wartość zwracana, jeśli test daje w wyniku wartość FALSE. Wyrażenie może być dowolnej funkcji, które generuje wartości logiczne. Można także funkcji zwracającej wartości liczbowe, w których wielkość wartość 0 jest interpretowana jako wartość false lub w których wielkość pustego ciągu zwracanie ciągów, jest interpretowany jako FAŁSZ. |`if(termfreq(cat,'electronics'),popularity,42)`Ta funkcja sprawdza toosee każdy dokument zawiera hello termin "electronics" hello cat pola. W przypadku następnie hello jest zwracana wartość hello popularne pola. W przeciwnym razie jest zwracana wartość 42 hello. |
| liniowy |Implementuje `m*x+c`, gdzie m i c są stałe i x jest dowolną funkcją. Jest to równoważne zbyt`sum(product(m,x),c)`, ale nieco bardziej wydajne zaimplementowanego jako jednej funkcji. |`linear(x,m,c) linear(x,2,4)`Zwraca`2*x+4` |
| ln |Zwraca logarytm naturalny hello z hello określonych funkcji. |`ln(x)` |
| Dziennik |Zwraca hello dziennika podstawie 10 hello określonych funkcji. |`log(x)   log(sum(x,100))` |
| mapy |Mapuje wartości wejściowe funkcji x, spełniających kryteria min i max, wraz z wartościami granicznymi toohello określonego obiektu docelowego. Witaj argumenty min i max muszą być stałymi. docelowy argumenty Hello i domyślne może być stałe lub funkcji. Jeśli hello wartość x nie należy do zakresu od min i max, zwracany albo hello wartość x lub wartości domyślnej jest zwracany, jeśli określona jako 5. argument. |`map(x,min,max,target) map(x,0,0,1)`Zmienia wartości 0 too1. Może to być przydatne podczas obsługi wartości domyślnej 0.<br> `map(x,min,max,target,default)    map(x,0,100,1,-1)`Zmienia wartości między 0 a 100 too1 i wszystkie inne wartości zbyt-1.<br>  `map(x,0,100,sum(x,599),docfreq(text,solr))`Zmienia żadnych wartości z zakresu od 0 do 100 toox + 599 i innych toofrequency wartości hello terminu "solr" w hello pola tekstowego. |
| Maksymalna |Zwraca hello maksymalną wartość liczbowa wielu zagnieżdżonych funkcji lub stałe, które są określane jako argumenty: `max(x,y,...)`. max — funkcja Hello również może być przydatna do "bottoming out" innej funkcji lub pola dla niektórych określone stała.  Użyj hello `field(myfield,max)` składni wybierania hello maksymalną wartość jednego pola wielowartościowe. |`max(myfield,myotherfield,0)` |
| min. |Zwraca hello minimalną wartość numeryczna wiele zagnieżdżonych funkcji stałych, które są określane jako argumenty: `min(x,y,...)`. funkcji min Hello może także służyć do prezentowania "górna granica" dla funkcji przy użyciu stałej. Użyj hello `field(myfield,min)` składni wybierania hello minimalną wartość jednego pola wielowartościowe. |`min(myfield,myotherfield,0)` |
| mod |Oblicza modulo hello hello funkcji x przez hello funkcja y. |`mod(1,x)` <br> `mod(sum(x,100), max(y,1))` |
| MS |Zwraca milisekund różnica między argumenty. Daty są względną toohello Unix lub POSIX epoki czasu, północy, 1 stycznia 1970 UTC. Argumenty może być nazwa hello indeksowanego TrieDateField lub matematyczne daty na podstawie daty stałej lub teraz. `ms()`odpowiada za`ms(NOW)`, liczba milisekund, ponieważ epoki hello. `ms(a)`Zwraca hello wyrażony w milisekundach czas od momentu epoki hello, reprezentujący hello argument. `ms(a,b)`Zwraca hello wyrażony w milisekundach czas, tym b występuje przed, która jest `a - b`. |`ms(NOW/DAY)`<br>`ms(2000-01-01T00:00:00Z)`<br>`ms(mydatefield)`<br>`ms(NOW,mydatefield)`<br>`ms(mydatefield,2000-01-01T00:00:00Z)`<br>`ms(datefield1,datefield2)` |
| nie |wartość Hello logicznie zanegowane hello opakowana funkcja. |`not(exists(author))`Wartość TRUE tylko wtedy, gdy `exists(author)` ma wartość false. |
| lub |Rozłączenie logiczne. |`or(value1,value2)`Wartość TRUE, jeśli wartość1 lub wartość2 ma wartość true. |
| Pow |Generuje hello określony podstawowy toohello określony zasilania. `pow(x,y)`zgłasza zasilania x toohello y. |`pow(x,y)`<br>`pow(x,log(y))`<br>`pow(x,0.5)`Witaj takie same jak sqrt. |
| Produktu |Zwraca hello produktu wielu wartości lub funkcji, które są określone w postaci listy rozdzielanej przecinkami. `mul(...)`może także służyć jako alias dla tej funkcji. |`product(x,y,...)`<br>`product(x,2)`<br>`product(x,y)`<br>`mul(x,y)` |
| recip |Wykonuje funkcję wzajemnego z `recip(x,m,a,b)` implementacja `a/(m*x+b)`, gdzie m,, b są stałe i x jest dowolną funkcję arbitralnie złożonych. Gdy i b są równe i x > = 0, ta funkcja posiada maksymalną wartość 1, wyeliminować x zwiększa. Zwiększenie wartości hello i b wyniki razem w przepływie tooa całą funkcję hello płaska część krzywej hello. Te właściwości ułatwia tę funkcję nadaje się doskonale dla zwiększania nowych dokumentów, jeśli x to `rord(datefield)`. |`recip(myfield,m,a,b)`<br>`recip(rord(creationDate),1,1000,1000)` |
| rad |Konwertuje tooradians stopni. |`rad(x)` |
| Drukowanie |Zaokrągla liczbę toohello najbliższej liczby całkowitej. |`rint(x)`  <br> `rint(5.6)`Zwraca 6 |
| SIN |Zwraca sinus kąta. |`sin(x)` |
| SINH |Zwraca sinus hiperboliczny kąta. |`sinh(x)` |
| Skali |Skalowanie wartości funkcji hello x taki sposób, że należą one między hello określony minTarget i maxTarget włącznie. Bieżąca implementacja Hello przechodzi przez wszystkie hello funkcja wartości tooobtain hello min i max, więc można wybrać hello odpowiedniej skali. Bieżąca implementacja Hello nie rozróżnia po usunięciu dokumenty lub dokumenty, niezawierające wartości. W tych przypadkach używa 0.0 wartości. Oznacza to, że jeśli wartości są zwykle wszystkie większa niż 0,0, co może nadal końcowa 0,0 jako hello toomap wartość minimalna z. W takich przypadkach odpowiednie `map()` funkcji można używać jako wartość tooa toochange 0,0 rozwiązania w zakresie rzeczywistych hello, jak pokazano poniżej:`scale(map(x,0,0,5),1,2)` |`scale(x,minTarget,maxTarget)`<br>`scale(x,1,2)`Skaluje hello wartości x, w taki sposób, że wszystkie wartości należą do zakresu od 1 i 2 włącznie. |
| SQRT |Zwraca pierwiastek kwadratowy hello hello określonej wartości lub funkcji. |`sqrt(x)`<br>`sqrt(100)`<br>`sqrt(sum(x,100))` |
| strdist |Oblicza odległość hello między dwa ciągi. Używa interfejsu moduł sprawdzania pisowni hello Lucene w StringDistance i obsługuje wszystkie implementacje hello dostępne w tym pakiecie. Umożliwia także tooplug aplikacji w ich własnych za pośrednictwem zasobów w Solr możliwości ładowania. przyjmuje strdist `(string1, string2, distance measure)`. Możliwe wartości dla miary odległości to:<ul><li>jw: Winklera Jaro</li><li>Edytuj: Levenstein lub edycji odległości</li><li>ngram: hello NGramDistance, jeśli jest określony, można opcjonalnie Przekaż rozmiar ngram hello zbyt. Domyślna to 2.</li><li>FQN: W pełni kwalifikowaną nazwę implementację interfejsu StringDistance hello klasy. Musi mieć konstruktora nie argumentu.</li></ul> |`strdist("SOLR",id,edit)` |
| Sub |Zwraca x i y, z `sub(x,y)`. |`sub(myfield,myfield2)`<br>`sub(100,sqrt(myfield))` |
| Suma |Zwraca hello sumę wiele wartości lub funkcji, które są określone w postaci listy rozdzielanej przecinkami. `add(...)`może być używany jako alias dla tej funkcji. |`sum(x,y,...)`<br>`sum(x,1)`<br>`sum(x,y)`<br>`sum(sqrt(x),log(y),z,0.5)`<br>`add(x,y)` |
| termfreq |Zwraca liczbę hello razy termin hello pojawia się w polu powitania dla tego dokumentu. |termfreq(text,'memory') |
| tan |Zwraca tangens kąta. |`tan(x)` |
| TANH |Zwraca tangens hiperboliczny kąta. |`tanh(x)` |

## <a name="search-field-and-facet-reference"></a>Odwołanie wyszukiwania pola i aspektu
Korzystając z wyszukiwania dziennika toofind danych, wyniki są wyświetlane różne pola i aspektami. Niektóre informacje hello mogą nie być wyświetlane bardzo opisowy. Użyj powitania po toohelp informacji zrozumieć hello wyników.

| Pole | Typ wyszukiwania | Opis |
| --- | --- | --- |
| Dla identyfikatora dzierżawcy |Wszystkie |Toopartition używanych danych. |
| TimeGenerated |Wszystkie |Używane toodrive hello na osi czasu timeselectors (wyszukiwania i w innych ekranów). Reprezentuje on hello element danych został wygenerowany (zwykle na powitania agenta). czas Hello jest wyrażona w formacie ISO i jest zawsze UTC. W przypadku hello typów, które są oparte na istniejących Instrumentacji (to znaczy zdarzenia w dzienniku) jest to zazwyczaj hello w czasie rzeczywistym tego hello wpisu/wiersz/Zapis dziennika. W przypadku niektórych hello innych typów, które są tworzone za pomocą pakietów administracyjnych lub w chmurze hello (na przykład zalecenia lub alerty) hello reprezentuje czas coś innego. Jest to godzinę hello tego nowego elementu danych migawka konfiguracji pewnego rodzaju zostały zebrane, lub zalecenie/alert został utworzony na jego podstawie. |
| Identyfikator zdarzenia |Wydarzenie |Identyfikator zdarzenia w dzienniku zdarzeń systemu Windows hello. |
| Dziennik zdarzeń |Wydarzenie |Dziennik zdarzeń, w którym hello zdarzenie zostało zarejestrowane przez system Windows. |
| EventLevelName |Wydarzenie |Krytyczne/ostrzeżenia/informacji/Powodzenie |
| eventLevel |Wydarzenie |Wartości liczbowej dla krytycznych/ostrzeżenia/informacji/Powodzenie (Użyj EventLevelName łatwiejsze/bardziej czytelny zapytań). |
| SourceSystem |Wszystkie |Skąd pochodzą dane hello (w postaci liczby dołączyć tryb toohello usługi). Przykłady programu Microsoft System Center Operations Manager i usługi Azure Storage. |
| Nazwa obiektu |PerfHourly |Nazwa obiektu wydajności systemu Windows. |
| InstanceName |PerfHourly |Nazwa wystąpienia liczników wydajności systemu Windows. |
| CounteName |PerfHourly |Nazwa licznika wydajności systemu Windows. |
| ObjectDisplayName |PerfHourly, ConfigurationObjectProperty ConfigurationAlert, ConfigurationObject, |Nazwa wyświetlana obiektu hello objęci zasadę zbierania danych wydajności w programie Operations Manager. Może to być również hello wyświetlaną nazwą obiektu hello wykrytych przez usługę Operational Insights lub względem których hello alert został wygenerowany. |
| RootObjectName |PerfHourly, ConfigurationObjectProperty ConfigurationAlert, ConfigurationObject, |Nazwa wyświetlana hello nadrzędny obiekt hello objęci zasadę zbierania danych wydajności w programie Operations Manager nadrzędny hello (w relacji hostingu podwójny). Może to być również hello wyświetlaną nazwą obiektu hello wykrytych przez usługę Operational Insights lub względem których hello alert został wygenerowany. |
| Computer (Komputer) |Większość typów |Nazwa komputera należącego do hello danych. |
| DeviceName |ProtectionStatus |Dane hello nazwy komputera należy (taki sam jak "Komputer"). |
| DetectionId |ProtectionStatus | |
| ThreatStatusRank |ProtectionStatus |Pozycja stan zagrożenie jest numeryczna reprezentacja hello stanu zagrożeń. Podobne tooHTTP kody odpowiedzi, klasyfikacji hello ma luki pomiędzy hello numery (dlatego zagrożenia nie wynosi 150 i nie 100 lub 0), pozostawiając miejsca tooadd nowe stany. Dla zbiorczego stanu zagrożeń i stanu ochrony zamiar hello jest tooshow hello najgorszy stan, który hello komputera miało w wybranym okresie hello. numery Hello rank powitania innych stanów, można wyszukać hello rekord z największą liczbą hello. |
| ThreatStatus |ProtectionStatus |Opis ThreatStatus, mapuje 1:1 z ThreatStatusRank. |
| TypeofProtection |ProtectionStatus |Produkt ochrony przed złośliwym kodem, który zostanie wykryty na komputerze hello: Brak, narzędzie do usuwania złośliwego oprogramowania firmy Microsoft, Forefront itd. |
| ScanDate |ProtectionStatus | |
| SourceHealthServiceId |ProtectionStatus, RequiredUpdate |Identyfikator usługi badania kondycji agenta na tym komputerze. |
| HealthServiceId |Większość typów |Identyfikator usługi badania kondycji agenta na tym komputerze. |
| ManagementGroupName |Większość typów |Nazwa grupy zarządzania agentami dołączone do programu Operations Manager. W przeciwnym razie wartość jest równa null/puste. |
| Typ obiektu |ConfigurationObject |Typ (jak klasa/typu pakiet administracyjny programu Operations Manager) dla tego obiektu, wykryte przez oceny konfiguracji analizy dzienników. |
| UpdateTitle |RequiredUpdate |Nazwa hello aktualizacji, które nie stwierdzono zainstalowane. |
| PublishDate |RequiredUpdate |Podczas aktualizacji hello został opublikowany w witrynie Microsoft Update. |
| Serwer |RequiredUpdate |Dane hello nazwy komputera należy (taki sam jak "Komputer"). |
| Product (Produkt) |RequiredUpdate |Produkt, który hello aktualizacja dotyczy. |
| UpdateClassification |RequiredUpdate |Typ aktualizacji (na przykład pakiet zbiorczy aktualizacji lub dodatek service pack). |
| KBID |RequiredUpdate |Identyfikator artykułu KB, który opisuje najlepsze praktyki lub aktualizacji. |
| WorkflowName |ConfigurationAlert |Nazwa hello zasady lub monitora, wytworzonego hello alertu. |
| Ważność |ConfigurationAlert |Ważność alertu hello. |
| Priorytet |ConfigurationAlert |Priorytet alertu hello. |
| IsMonitorAlert |ConfigurationAlert |Ten alert został wygenerowany przez monitor (true) czy zasadę (false)? |
| AlertParameters |ConfigurationAlert |Plik XML z parametrami hello hello analizy dzienników alertu. |
| Kontekst |ConfigurationAlert |Plik XML z kontekstem hello hello analizy dzienników alertu. |
| Obciążenie |ConfigurationAlert |Technologia lub obciążenia, które hello alert dotyczy. |
| AdvisorWorkload |Zalecenie |Technologia lub obciążenia, które hello zalecenie odnosi się do. |
| Opis |ConfigurationAlert |Opis alertu (short). |
| DaysSinceLastUpdate |UpdateAgent |Ile dni temu (względną tooTimeGenerated tego rekordu) tego agenta zainstalować aktualizację z usługi Windows Server Update Service (WSUS) lub Microsoft Update? |
| DaysSinceLastUpdateBucket |UpdateAgent |Oparte na DaysSinceLastUpdate, kategoryzacji w przedziałów czasu z jak dawno temu komputera ostatniej instalacji żadnych aktualizacji usług WSUS/usługi Microsoft Update. |
| AutomaticUpdateEnabled |UpdateAgent |Sprawdzanie aktualizacji automatycznych włączone lub wyłączone dla tego agenta? |
| AutomaticUpdateValue |UpdateAgent |Aktualizacje automatyczne sprawdzanie, czy zestaw tooautomatically pobrać i zainstalować, tylko pobierania lub tylko sprawdzanie? |
| WindowsUpdateAgentVersion |UpdateAgent |Numer wersji hello agenta usługi Microsoft Update. |
| WSUSServer |UpdateAgent |Serwer WSUS, który jest celem tej usługi Windows update agent |
| OSVersion |UpdateAgent |Wersja systemu operacyjnego hello tej usługi Windows update agent jest uruchomiony w. |
| Nazwa |Zalecenie, ConfigurationObjectProperty |Nazwa/tytuł zalecenie hello lub nazwa właściwości hello z analizy dzienników konfiguracji oceny. |
| Wartość |ConfigurationObjectProperty |Wartość właściwości z analizy dzienników konfiguracji oceny. |
| KBLink |Zalecenie |Adres URL toohello KB artykule na temat tej najlepszej praktyki lub aktualizacji. |
| RecommendationStatus |Zalecenie |Zalecenia są hello kilka typów rekordów pobrać zaktualizowany, nie właśnie dodanej toohello indeksu wyszukiwania. Ten stan zmieni się, czy zalecenie hello jest aktywny lub open lub analizy dzienników wykryje, że został rozwiązany. |
| RenderedDescription |Wydarzenie |Renderowane opis (ponownie tekst z parametrami wypełnione) zdarzeń systemu Windows. |
| ParameterXml |Wydarzenie |Plik XML z parametrami hello w sekcji danych hello zdarzenia systemu Windows (taki jak pokazano w Podglądzie zdarzeń). |
| EventData |Wydarzenie |Plik XML z sekcji danych całego hello zdarzenia systemu Windows (taki jak pokazano w Podglądzie zdarzeń). |
| Element źródłowy |Wydarzenie |Źródło dziennika zdarzeń, który wygenerował zdarzenie hello. |
| EventCategory |Wydarzenie |Kategoria zdarzenia hello bezpośrednio z dziennika zdarzeń systemu Windows hello. |
| Nazwa użytkownika |Wydarzenie |Nazwa użytkownika zdarzeń systemu Windows hello (zazwyczaj NT AUTHORITY\LOCALSYSTEM). |
| SampleValue |PerfHourly |Średnia wartość dla agregacji godzinowej hello licznika wydajności. |
| Min |PerfHourly |Minimalna wartość w polu Interwał co godzinę powitania agregacji godzinowej licznika wydajności. |
| Maks. |PerfHourly |Maksymalna wartość w polu Interwał co godzinę powitania agregacji godzinowej licznika wydajności. |
| Percentile95 |PerfHourly |Witaj 95 wartość percentylu hello godzinny interwał agregacji godzinowej licznika wydajności. |
| SampleCount |PerfHourly |Ile próbek licznika wydajność pierwotna zostały tooproduce używane tym godzinne agregacji rekordu. |
| Zagrożenia |ProtectionStatus |Nazwa wykrytego złośliwego oprogramowania. |
| Konto magazynu |W3CIISLog |Z odczytano dziennika hello konta magazynu Azure. |
| AzureDeploymentID |W3CIISLog |Identyfikator wdrożenia usługi Azure hello chmury usługi hello dziennika należy. |
| Rola |W3CIISLog |Przynależność roli hello Azure cloud service hello dziennika. |
| RoleInstance |W3CIISLog |Należy RoleInstance hello Azure roli hello dziennika. |
| sSiteName |W3CIISLog |Witryny sieci Web usług IIS, która hello dziennika należy too(metabase notation); Pole s-sitename Hello hello oryginalny dziennik. |
| sComputerName |W3CIISLog |Pole s-computername Hello hello oryginalny dziennik. |
| sIP |W3CIISLog |Żądanie HTTP hello adres IP serwera został skierowany do. Pole s-ip Hello hello oryginalny dziennik. |
| csMethod |W3CIISLog |Metoda HTTP (na przykład GET/POST) używanego przez klienta hello w żądaniu hello HTTP. Witaj cs-method w dzienniku oryginalnego hello. |
| cIP |W3CIISLog |Pochodzi żądanie HTTP hello adres IP klienta. pole c-ip Hello hello oryginalny dziennik. |
| csUserAgent |W3CIISLog |Agent użytkownika HTTP deklaruje powitania klienta (przeglądarki lub w inny sposób). Witaj cs-user-agent w dzienniku oryginalnego hello. |
| scStatus |W3CIISLog |Zwracane przez klienta toohello serwera hello kod stanu HTTP (na przykład 200/403/500). Witaj cs-status w dzienniku oryginalnego hello. |
| Właściwość timeTaken |W3CIISLog |Czas (w milisekundach) to Żądanie hello trwało toocomplete. pole właściwość timetaken Hello hello oryginalny dziennik. |
| csUriStem |W3CIISLog |Względny identyfikator URI (bez adres hosta, który jest, / wyszukaj) który odebrał żądanie. pola cs uristem Hello hello oryginalny dziennik. |
| csUriQuery |W3CIISLog |Zapytanie URI. Identyfikator URI zapytania są niezbędne tylko w przypadku stron dynamicznych, takich jak strony ASP, więc to pole zawiera zwykle łącznika dla strony statyczne. |
| sPort |W3CIISLog |Port serwera, który hello żądania HTTP został wysłany (i który program IIS nasłuchuje, ponieważ jej pobrania go). |
| csUserName |W3CIISLog |Uwierzytelnić nazwę użytkownika, jeśli Żądanie hello jest uwierzytelniane i anonimowe nie. |
| csVersion |W3CIISLog |Wersja protokołu HTTP użyty w żądaniu hello (na przykład HTTP/1.1). |
| csCookie |W3CIISLog |Informacje dotyczące pliku cookie. |
| csReferer |W3CIISLog |Witryna ostatnio odwiedzona użytkownika hello. Ta witryna udostępniła link toohello bieżącej lokacji. |
| csHost |W3CIISLog |Nagłówek hosta (na przykład www.mysite.com) żądanego. |
| scSubStatus |W3CIISLog |Kod błędu podstanu. |
| scWin32Status |W3CIISLog |Kod stanu systemu Windows. |
| csBytes |W3CIISLog |Liczba bajtów wysłanych w żądaniu hello z powitania klienta toohello serwera. |
| scBytes |W3CIISLog |W odpowiedzi hello powitania klienta programu server toohello zwróconych bajtów. |
| ConfigChangeType |Zmianakonfiguracji |Typ zmiany (na przykład WindowsServices/oprogramowania). |
| ChangeCategory |Zmianakonfiguracji |Kategoria zmiany hello (zmodyfikowane Added/usunięte). |
| SoftwareType |Zmianakonfiguracji |Typ oprogramowania (aplikacja/aktualizacji). |
| SoftwareName |Zmianakonfiguracji |Nazwa oprogramowania hello (tylko toosoftware odpowiednich zmian). |
| Wydawca |Zmianakonfiguracji |Dostawcy, który publikuje hello oprogramowania (tylko toosoftware odpowiednich zmian). |
| SvcChangeType |Zmianakonfiguracji |Typ zmiany, która została zastosowana na usługi systemu Windows (stan/StartupType/ścieżka/konto_usługi). Jest to tylko tooWindows odpowiednie zmiany usługi. |
| SvcDisplayName |Zmianakonfiguracji |Nazwa wyświetlana usługi hello, która została zmieniona. |
| SvcName |Zmianakonfiguracji |Nazwa usługi hello, która została zmieniona. |
| SvcState |Zmianakonfiguracji |Nowy stan (bieżącego) hello usługi. |
| SvcPreviousState |Zmianakonfiguracji |Poprzedni znane stanu usługi hello (dotyczy tylko po zmianie stanu usługi). |
| SvcStartupType |Zmianakonfiguracji |Typ uruchomienia usługi. |
| SvcPreviousStartupType |Zmianakonfiguracji |Poprzedni typ uruchamiania usługi (dotyczy tylko po zmianie typ uruchomienia usługi). |
| SvcAccount |Zmianakonfiguracji |Konto usługi. |
| SvcPreviousAccount |Zmianakonfiguracji |Poprzedniego konta usługi (dotyczy tylko po zmianie konta usługi). |
| SvcPath |Zmianakonfiguracji |Ścieżka pliku wykonywalnego toohello usługi Windows hello. |
| SvcPreviousPath |Zmianakonfiguracji |Poprzednia ścieżka pliku wykonywalnego dla hello (dotyczy tylko jego zmiana) usługi Windows hello. |
| SvcDescription |Zmianakonfiguracji |Opis usługi hello. |
| Poprzednie |Zmianakonfiguracji |Poprzedni stan tego oprogramowania (nie zainstalowano zainstalowana/poprzedniej wersji). |
| Bieżący |Zmianakonfiguracji |Najnowszy stan tego oprogramowania (nie zainstalowano zainstalowana/bieżącej wersji). |

## <a name="next-steps"></a>Następne kroki
Aby uzyskać dodatkowe informacje dziennika wyszukiwania:

* Zapoznaj się z [dziennika wyszukiwania](log-analytics-log-searches.md) tooview szczegółowe informacje zebrane przez rozwiązania.
* Użyj [pola niestandardowe w analizy dzienników](log-analytics-custom-fields.md) tooextend dziennik wyszukiwania.
