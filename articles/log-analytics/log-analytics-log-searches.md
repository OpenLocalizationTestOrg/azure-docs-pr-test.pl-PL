---
title: aaaFind danych z dziennika wyszukiwania Azure Log Analytics | Dokumentacja firmy Microsoft
description: "Dziennik wyszukiwania pozwalają toocombine i skorelowania danych dowolnego komputera z wielu źródeł w danym środowisku."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: 0d7b6712-1722-423b-a60f-05389cde3625
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 1161857a0027f05726492417362cb24a8fe21ef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-data-using-log-searches-in-log-analytics"></a>Wyszukiwanie danych przy użyciu dziennika wyszukiwania w analizy dzienników

>[!NOTE]
> W tym artykule opisano dziennik wyszukiwania przy użyciu hello bieżący język zapytań w analizy dzienników.  Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie należy zapoznać się zbyt[opis dziennika przeszukuje analizy dzienników (nowy)](log-analytics-log-search-new.md).


Na powitania najważniejsza część analizy dzienników jest funkcja wyszukiwania dziennika hello, dzięki czemu można toocombine i skorelowania danych dowolnego komputera z wielu źródeł w danym środowisku. Rozwiązania są również obsługiwane przez dziennik wyszukiwania toobring metryki można przestawiać wokół obszaru określonego problemu.

Na stronie wyszukiwania hello można utworzyć kwerendę, a następnie podczas wyszukiwania, możesz filtrować wyniki hello za pomocą formantów zestawu reguł. Można też utworzyć tootransform zaawansowanych zapytań, filtrować i raportu na wyniki.

Typowe zapytania wyszukiwania dziennika znajdują się na większości stronach rozwiązania. W konsoli OMS hello możesz kliknąć Kafelki lub przejść do szczegółów w elementach tooother tooview szczegóły elementu hello za pomocą wyszukiwania dziennika.

W tym samouczku zostanie omówiony toocover przykłady wszystkie podstawy hello podczas wyszukiwania dziennika.

Firma Microsoft będzie rozpoczynać się od prostego, praktyczne przykłady i następnie ich tak, aby uzyskać opis praktycznych zastosowań o toouse hello składni tooextract hello insights sposób hello danych.

Po znasz zapoznać się z techniki wyszukiwania, można przejrzeć hello [analizy dzienników dziennika odwołanie wyszukiwania](log-analytics-search-reference.md).

## <a name="use-basic-filters"></a>Używanie filtrów podstawowych
Witaj po pierwsze tooknow jest pierwszym hello część zapytania wyszukiwania, przed każdą "|" znak kreski pionowej, jest zawsze *filtru*. Należy go traktować jako klauzuli WHERE TSQL — Określa *co* podzbiór toopull danych z magazynu danych hello OMS. Wyszukiwanie w magazynie danych hello dotyczy przede wszystkim określenie właściwości hello hello dane tooextract, dlatego jest naturalna, czy zapytanie może rozpoczynać się hello klauzuli WHERE.

Hello najbardziej podstawową można użyć są następujące filtry *słowa kluczowe*, na przykład "error" lub 'timeout' lub nazwę komputera. Tego rodzaju prostego zapytania na ogół wraca kształtów różnych danych w ramach hello sam wyników. Analiza dzienników ma inną *typy* danych w systemie hello.

### <a name="tooconduct-a-simple-search"></a>tooconduct proste wyszukiwanie
1. W portalu OMS hello, kliknij przycisk **wyszukiwania dziennika**.  
    ![Kafelek wyszukiwania](./media/log-analytics-log-searches/oms-overview-log-search.png)
2. W polu zapytania hello wpisz `error` , a następnie kliknij przycisk **wyszukiwania**.  
    ![Błąd wyszukiwania](./media/log-analytics-log-searches/oms-search-error.png)  
    Na przykład hello zapytanie dla `error` w hello poniższy obraz zwrócone 100 000 **zdarzeń** rekordy (zbierane przez zarządzanie dziennikiem) 18 **ConfigurationAlert** rekordów (wygenerowanych przez konfigurację Ocena) i 12 **Zmianakonfiguracji** rekordy (przechwycone przez hello śledzenia zmian).   
    ![wyniki wyszukiwania](./media/log-analytics-log-searches/oms-search-results01.png)  

Te filtry nie są naprawdę klas typów obiektów. *Typ* jest tylko tag lub właściwość lub ciąg/Nazwa/kategorii, który jest dołączony tooa część danych. Niektóre dokumenty w systemie hello są oznaczone jako **typu: ConfigurationAlert** i niektóre są oznaczone jako **typu: wydajności**, lub **typu: zdarzenia**i tak dalej. Każdy wynik wyszukiwania, dokument, rekordu lub wpis zawiera wszystkie właściwości pierwotnych hello i ich wartości dla każdego z tych fragmentów danych i użyciem tych toospecify nazwy pól w filtrze hello tylko rekordy hello tooretrieve gdzie hello pole ma, czy wartość.

*Typ* jest naprawdę tylko pola, które mają wszystkie rekordy, nie jest inny niż inne pole. Ustanowiono to oparta na wartości hello hello typ pola. Ten rekord ma inny formularz lub kształtu. Okazjonalnie **typu = wydajności**, lub **typu = zdarzeń** jest również hello składni konieczne toolearn tooquery danych wydajności lub zdarzeń.

Po nazwie pola hello i przed wartością hello można użyć dwukropka (:) lub znakiem równości (=). **Typ: zdarzenie** i **typu = zdarzeń** są równoważne w rozumieniu, możesz wybrać hello styl preferowane.

Tak, jeśli hello wpisz = wydajności rekordów pole o nazwie "CounterName", a następnie można pisać zapytania podobne `Type=Perf CounterName="% Processor Time"`.

Zapewni to tylko dane dotyczące wydajności hello gdy nazwa licznika wydajności hello jest "% czasu procesora".

### <a name="toosearch-for-processor-time-performance-data"></a>toosearch danych wydajności czas procesora
* W polu zapytania wyszukiwania hello wpisz`Type=Perf CounterName="% Processor Time"`

Można również być bardziej szczegółowe i używać **InstanceName = _ "Ogółem"** w zapytaniu hello, która jest licznika wydajności systemu Windows. Możesz też wybrać zestaw reguł, a drugi **pola: wartość**. Filtr Hello jest automatycznie dodawany filtru tooyour hello pasku zapytania. Widać to w powitania po obrazu. Przedstawia on gdzie tooclick tooadd **InstanceName: "_łącznie"** toohello zapytań bez wprowadzania żadnych czynności.

![aspekt wyszukiwania](./media/log-analytics-log-searches/oms-search-facet.png)

Zapytanie staje się teraz`Type=Perf CounterName="% Processor Time" InstanceName="_Total"`

W tym przykładzie, nie masz toospecify **typu = wydajności** tooget toothis wynik. Ponieważ pola hello CounterName i InstanceName tylko istnieje dla rekordów typu = wydajności, zapytania hello jest wystarczająco konkretny tooreturn hello takie same wyniki hello dłużej, poprzednie jedną:

```
CounterName="% Processor Time" InstanceName="_Total"
```

Jest to spowodowane wszystkie filtry hello w zapytaniu hello są oceniane jako *i* ze sobą. Ostatecznie hello Dodaj kryteria toohello więcej pól, możesz uzyskać mniejszy, więcej określonych i precyzyjnych wyników.

Na przykład hello zapytania `Type=Event EventLog="Windows PowerShell"` jest identyczny zbyt`Type=Event AND EventLog="Windows PowerShell"`. Zwraca wszystkie zdarzenia, które zostały zarejestrowane w i zbierane z dziennika zdarzeń hello środowiska Windows PowerShell. Jeśli dodasz filtr wielokrotnie wielokrotnie, wybierając hello jest tego samego zestawu reguł, następnie hello problem czysto bardzo drobny — może zajmowały hello pasek wyszukiwania, ale nadal zwraca hello takie same wyniki ponieważ niejawny operator AND hello są zawsze dostępne.

Niejawny operator AND hello można łatwo cofnąć za pomocą operatora NOT jawnie. Na przykład:

`Type:Event NOT(EventLog:"Windows PowerShell")`lub jego odpowiednik `Type=Event EventLog!="Windows PowerShell"` zwrócić wszystkie zdarzenia ze wszystkich dzienników, które nie są hello dziennika programu Windows PowerShell.

Można użyć innych operator logiczny takich jak "Lub". Witaj następujące zapytanie zwraca rekordy, dla których hello EventLog znajduje albo aplikacji lub systemu.

```
EventLog=Application OR EventLog=System
```

Przy użyciu hello powyżej zapytania, otrzymasz wpisy dla obu dzienników w hello sam wyników.

Jednak jeśli usuniesz hello lub pozostawić hello niejawne i w miejscu, następnie hello następujące zapytanie nie utworzy żadnych wyników, ponieważ nie istnieje wpis dziennika zdarzeń, który należy tooBOTH dzienniki. Każdy wpis dziennika zdarzeń został napisany tooonly jedną z dwóch dzienniki hello.

```
EventLog=Application EventLog=System
```


## <a name="use-additional-filters"></a>Używanie filtrów dodatkowe
Witaj następujące zapytanie zwraca wpisy 2 dzienników zdarzeń dla wszystkich komputerów hello, które zostały wysłane dane.

```
EventLog=Application OR EventLog=System
```

![Wyniki wyszukiwania](./media/log-analytics-log-searches/oms-search-results03.png)

Wybranie jednego z pól hello lub filtry zostaną zawęzić hello zapytania tooa określonego komputera, z wyłączeniem innych protokołów. Wynikowe zapytanie Hello czy przypominać następujące hello.

```
EventLog=Application OR EventLog=System Computer=SERVER1.contoso.com
```

Czyli następujące toohello równoważne z powodu hello niejawne koniunkcji binarnej.

```
EventLog=Application OR EventLog=System AND Computer=SERVER1.contoso.com
```

Każde zapytanie jest oceniane w powitania po jawnym kolejności. Uwaga hello nawiasu.

```
(EventLog=Application OR EventLog=System) AND Computer=SERVER1.contoso.com
```

Podobnie jak hello pola dziennika zdarzeń, można pobrać dane tylko w przypadku zestaw komputerów określonych przez dodanie lub. Na przykład:

```
(EventLog=Application OR EventLog=System) AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com OR Computer=SERVER3.contoso.com)
```

Podobnie, ten powitania po return zapytania **% czasu procesora CPU** dla hello wybranych tylko dwa komputery.

```
CounterName="% Processor Time"  AND InstanceName="_Total" AND (Computer=SERVER1.contoso.com OR Computer=SERVER2.contoso.com)
```

### <a name="field-types"></a>Typy pól
Podczas tworzenia filtrów, należy poznać różnice hello w pracy z różnymi typami pól zwrócony przez dziennik wyszukiwania.

**Pola z możliwością przeszukiwania** Pokaż na niebiesko w wynikach wyszukiwania.  Pola, w których można użyć w polu toohello określone warunki wyszukiwania takie jak następujące hello:

```
Type: Event EventLevelName: "Error"
Type: SecurityEvent Computer:Contains("contoso.com")
Type: Event EventLevelName IN {"Error","Warning"}
```

**Zwolnij pól z możliwością wyszukiwania tekstu** są wyświetlane w kolorze szarym w wynikach wyszukiwania.  Nie można ich używać z polem toohello określone warunki wyszukiwania jak pól z możliwością wyszukiwania.  Są one tylko przeszukiwane, gdy wszystkie pola, takie jak następujące hello wykonywanie zapytania.

```
"Error"
Type: Event "Exception"
```


### <a name="boolean-operators"></a>Operatory logiczne
Datetime i pól liczbowych, możesz wyszukać wartości przy użyciu *większe*, *mniejszym niż*, i *mniejsza lub równa*. Można używać operatorów prosty przykład >, <>, =, < =,! = w pasku wyszukiwania hello zapytania.

Umożliwia wysyłanie zapytań określonego dziennika zdarzeń w określonym okresie czasu. Na przykład hello ostatnich 24 godzinach jest wyrażona z powitania po wyrażeniu skrótu.

```
EventLog=System TimeGenerated>NOW-24HOURS
```


#### <a name="toosearch-using-a-boolean-operator"></a>toosearch przy użyciu operatora logicznego
* W polu zapytania wyszukiwania hello wpisz`EventLog=System TimeGenerated>NOW-24HOURS`  
    ![Wyszukiwanie z wartość logiczna](./media/log-analytics-log-searches/oms-search-boolean.png)

Mimo że można kontrolować graficznie hello interwał czasu, a większość czasu może być toodo, czy tooincluding zalety filtr czasu bezpośrednio do hello zapytania. Na przykład, to rozwiązanie idealne za pomocą pulpitów nawigacyjnych, w którym można zastąpić hello czasu dla każdego kafelka, niezależnie od hello *globalne* selektor czas na powitania strony pulpitu nawigacyjnego. Aby uzyskać więcej informacji, zobacz [sprawach czas na pulpicie nawigacyjnym](http://cloudadministrator.wordpress.com/2014/10/19/system-center-advisor-restarted-time-matters-in-dashboard-part-6/).

Filtrowanie według czasu, pamiętać uzyskać wyniki dla hello *przecięcia* z hello dwóch okresów: hello określona w portalu OMS hello (S1) i hello określona w zapytaniu hello (S2).

![część wspólną](./media/log-analytics-log-searches/oms-search-intersection.png)

Oznacza to, że jeśli hello okresów nie intersect, na przykład w portalu OMS hello, którym można wybrać **ten tydzień** w hello kwerendy, gdzie został zdefiniowany **ostatniego tygodnia**, to nie ma żadnych przecięcia i użytkownik nie będzie otrzymywać żadnych wyników.

Operatory porównania pola TimeGenerated hello są przydatne także w innych sytuacjach. Na przykład w przypadku pól liczbowych.

Podane na przykład, że alerty oceny konfiguracji hello następujące wartości ważności:

* 0 = informacji
* 1 = Ostrzeżenie
* 2 = krytyczne

Można wyszukać zarówno ostrzegawcze i krytyczne alerty i wykluczyć informacyjną sieci z hello następujące zapytanie:

```
Type=ConfigurationAlert  Severity>=1
```


Umożliwia także zakresu zapytania. Oznacza to, zapewniają hello początku i na końcu zakresu wartości w sekwencji. Na przykład jeśli zdarzenia z dziennika zdarzeń programu Operations Manager hello gdzie hello identyfikator zdarzenia jest większy lub równy too2100, ale nie jest większa niż 2199, następnie hello następujące kwerendy zwróci je.

```
Type=Event EventLog="Operations Manager" EventID:[2100..2199]
```


> [!NOTE]
> należy użyć składni zakresu Hello jest hello dwukropka (:) pola: wartość separatora i *nie* hello znak równości (=). Ujmij hello dolna i górna końca zakresu hello w nawiasach kwadratowych i oddziel dwie kropki (.).
>
>

## <a name="manipulate-search-results"></a>Opracowanie wyników wyszukiwania
Jeśli szukasz danych zostanie mają toorefine zapytania wyszukiwania oraz mają dobrej poziom kontroli nad hello wyników. Pobierane są wyniki, można zastosować tootransform polecenia je.

Polecenia w wyszukiwaniach analizy dzienników *musi* należy wykonać po hello znaku kreski pionowej (|). Filtr musi być zawsze hello pierwsza część ciągu zapytania. Definiuje zestaw danych hello, w którym pracujesz z, a następnie "powoduje przekazanie w potoku" uzyskanych w poleceniu. Następnie można użyć potoku hello tooadd dodatkowych poleceń. To jest luźno podobne potoku środowiska Windows PowerShell toohello.

Ogólnie rzecz biorąc, hello język wyszukiwania analizy dzienników próbuje toomake styl i wskazówki dotyczące programu PowerShell toofollow it podobne toohello IT zalet i tooease hello naukę.

Polecenia mają nazwy zleceń, dzięki czemu można łatwo sprawdzić, co zrobić.  

### <a name="sort"></a>Sortuj
polecenie sortowania Hello pozwala hello toodefine sortowanie według wielu pól. Nawet jeśli nie używasz go, domyślna, czas, w kolejności malejącej jest wymuszana. Najnowsze wyniki Hello są zawsze u góry hello wyników wyszukiwania. Oznacza to, że po uruchomieniu wyszukiwania z `Type=Event EventID=1234` co naprawdę wykonaniu dla Ciebie jest:

```
Type=Event EventID=1234 **| Sort TimeGenerated desc**
```

To, ponieważ jest typem hello doświadczenia, które znasz w dziennikach. Na przykład w Podglądzie zdarzeń systemu Windows hello.

Możesz użyć sortowania toochange hello sposób są zwracane. Witaj poniższych przykładach pokazano, jak to działa.

```
Type=Event EventID=1234 | Sort TimeGenerated asc
```

```
Type=Event EventID=1234 | Sort Computer asc
```

```
Type=Event EventID=1234 | Sort Computer asc,TimeGenerated desc
```


Hello proste powyższych przykładach można działanie polecenia — zmienia kształt hello hello wyników, które hello filtr zwrócił.

### <a name="limit-and-top"></a>Limit i od góry
Inne mniej znanych polecenie jest ograniczona. Limit wynosi zlecenie przypominającej programu PowerShell. Limit jest funkcjonalnie identyczne toohello polecenie TOP. Witaj następujące kwerendy zwracają hello takie same wyniki.

```
Type=Event EventID=600 | Limit 1
```

```
Type=Event EventID=600 | Top 1
```


#### <a name="toosearch-using-top"></a>za pomocą górnej toosearch
* W polu zapytania wyszukiwania hello wpisz`Type=Event EventID=600 | Top 1`   
    ![top wyszukiwania](./media/log-analytics-log-searches/oms-search-top.png)

W powyższy obraz powitania, istnieją tysiące 358 rekordy z EventID = 600. Witaj pól, aspekty i filtry na powitania left zawsze Pokaż informacje o wynikach hello *przez część filtru hello* hello zapytania, który jest częścią hello przed znakiem potoku. Witaj **wyniki** okienko tylko zwraca wynik hello najnowszych 1, ponieważ hello przykładowe polecenie w kształcie i przekształcić hello wyników.

### <a name="select"></a>Wybierz pozycję
Wybierz polecenie Hello zachowuje się jak Select-Object w programie PowerShell. Zwraca przefiltrowane wyniki, które nie ma wszystkich swoich oryginalnych właściwości. Wybiera hello tylko te właściwości, które określisz.

#### <a name="toorun-a-search-using-hello-select-command"></a>toorun wyszukiwany przy użyciu polecenia select hello
1. W polu Wyszukaj wpisz `Type=Event` , a następnie kliknij przycisk **wyszukiwania**.
2. Kliknij przycisk **+ Pokaż więcej** w jednym z tooview wyniki hello ma wszystkie właściwości hello, które hello wyników.
3. Wybierz tych jawnie i hello zmiany zapytań za`Type=Event | Select Computer,EventID,RenderedDescription`.  
    ![Wybierz wyszukiwanie](./media/log-analytics-log-searches/oms-search-select.png)

To polecenie jest szczególnie przydatne, gdy mają toocontrol wyszukiwania wyjściowy i wybierz tylko hello części danych, który znaczenia naprawdę podróży często nie jest pełną dokumentację hello. Umożliwia to również mieć rekordów o różnych typach *niektórych* wspólnych właściwości, ale nie *wszystkie* ich właściwości są wspólne. Generowanie danych wyjściowych, który wygląda tabeli w naturalnie więcej lub działa dobrze w przypadku, gdy eksportowany plik CSV tooa, a następnie sprasowany w programie Excel.

## <a name="use-hello-measure-command"></a>Użyj polecenia miary hello
MIARA jest jednym z najbardziej wszechstronny polecenia hello w wyszukiwaniach analizy dzienników. Umożliwia on tooapply statystyczne *funkcje* tooyour danych i wyników agregacji pogrupowane według danego pola. Istnieje wiele funkcji statystycznych, które obsługuje miary.

### <a name="measure-count"></a>Miara count()
Witaj pierwszy toowork funkcji statystycznych z, a jedną toounderstand najprostszym hello jest hello *count()* funkcji.

Wynikiem każde zapytanie operacji wyszukiwania, takie jak `Type=Event`, pokazuje filtrów, nazywane również aspekty na powitania po lewej stronie wyników wyszukiwania. filtry Hello pokazują rozkład wartości przy użyciu danego pola hello wyników w hello wyszukiwania.

![liczba miar wyszukiwania](./media/log-analytics-log-searches/oms-search-measure-count01.png)

Na przykład w hello obrazu powyżej, które będzie widoczny hello **komputera** pola i informuje, że w zdarzeniach prawie 739 tysięcy hello w wynikach hello, umożliwiają 68 unikatowe i różne wartości hello **komputera** pole w tych rekordów. Kafelek Hello przedstawia tylko hello 5 pierwszych, które są hello najbardziej typowych 5 wartości, które są zapisywane w hello **komputera** pól), są posortowane według hello liczby dokumentów, które zawierają tej określonej wartości w tym polu. W obrazie hello widać, — czy wśród tych zdarzeń prawie 369 tysięcy — tysięcy 90 pochodzi z komputera OpsInsights04.contoso.com hello, tysięcy 83 z hello DB03.contoso.com komputera i tak dalej.

Co zrobić, jeśli chcesz toosee wszystkie wartości, ponieważ Kafelek hello przedstawia tylko hello tylko 5 pierwszych?

To miara bazowa hello polecenia można wykonać za pomocą funkcji count() hello. Ta funkcja nie używa żadnych parametrów. Wystarczy określić pole hello za pomocą którego chcesz toogroup — Witaj **komputera** pola w tym przypadku:

`Type=Event | Measure count() by Computer`

![liczba miar wyszukiwania](./media/log-analytics-log-searches/oms-search-measure-count-computer.png)

Jednak **komputera** jest to pole używane *w* każdego z nich dane — obejmuje nie relacyjnych baz danych i nie istnieje żadne oddzielne **komputera** obiektów w dowolnym miejscu. Po prostu hello wartości *w* hello danych można opisać jakiej encji wygenerowany je oraz wiele innych właściwości aspekty hello danych — dlatego hello termin *aspektu*. Jednak równie dobrze można grupować według innych pól. Ponieważ oryginalne wyniki hello prawie 739 tysięcy zdarzeń, które są przekazywane w potoku do polecenia miary hello również ma pole o nazwie **EventID**, można zastosować hello tego samego toogroup technika według tego pola i Pobierz liczbę zdarzeń przez identyfikator zdarzenia:

```
Type=Event | Measure count() by EventID
```

Jeśli użytkownik nie chce hello rzeczywistego rekordu liczba, która zawiera konkretną wartość, ale zamiast tego, jeśli chcesz tylko listę hello wartości samodzielnie, możesz dodać *wybierz* polecenia na końcu hello go i po prostu wybierz hello pierwszej kolumny:

```
Type=Event | Measure count() by EventID | Select EventID
```

Następnie można uzyskać w bardziej skomplikowanych i wstępnie sortowanie wyników hello w zapytaniu hello lub wystarczy kliknąć hello kolumn w siatce hello zbyt.

```
Type=Event | Measure count() by EventID | Select EventID | Sort EventID asc
```

#### <a name="toosearch-using-measure-count"></a>toosearch za pomocą liczby miary
* W polu zapytania wyszukiwania hello wpisz`Type=Event | Measure count() by EventID`
* Dołącz `| Select EventID` toohello koniec hello zapytania.
* Na koniec Dołącz `| Sort EventID asc` toohello koniec hello zapytania.

Istnieje kilka ważnych kwestii toonotice i wyróżnienie:

Po pierwsze hello wyniki będą nie są oryginalne nieprzetworzone wyniki hello już. Zamiast tego są one wyników zagregowany — zasadniczo grup wyników. Nie jest to problem, ale należy pamiętać, że w przypadku interakcji z kształtem bardzo różnych danych, która różni się od hello oryginalnego raw kształtu, który jest tworzony na bieżąco hello wyniku funkcji agregacji/statystyczne hello.

Drugi, **pomiaru liczby** obecnie zwraca tylko hello top 100 wyników distinct. To ograniczenie nie dotyczy toohello innych funkcji statystycznych. Tak zazwyczaj należy toouse dokładniejsze toosearch pierwszy filtr dla określonych elementów przed zastosowaniem funkcji count() miary.

## <a name="use-hello-max-and-min-functions-with-hello-measure-command"></a>Użyj funkcji max i min hello za pomocą polecenia miary hello
Istnieją różne scenariusze gdzie **Max() miary** i **Min() miary** są przydatne. Jednak ponieważ każdej funkcji jest przeciwny od siebie, możemy ilustrują Max() i możesz eksperymentować z Min() samodzielnie.

Po wykonaniu zapytania do zdarzenia zabezpieczeń mają **poziom** właściwość, która może się różnić. Na przykład:

```
Type=SecurityEvent
```

![start liczba miar wyszukiwania](./media/log-analytics-log-searches/oms-search-measure-max01.png)

Jeśli chcesz tooview hello najwyższej wartości dla wszystkich zabezpieczeń hello zdarzenia danego komputera z programem, hello Grupuj według pola, możesz użyć

```
Type=ConfigurationAlert | Measure Max(Level) by Computer
```

![Wyszukiwanie miary maksymalnej komputera](./media/log-analytics-log-searches/oms-search-measure-max02.png)

Który będzie wyświetlany dla hello komputerów, które ma **poziom** rekordów, większość z nich ma co najmniej poziom 8, ma wiele poziom 16.

```
Type=ConfigurationAlert | Measure Max(Severity) by Computer
```

![Maksymalny czas miar wyszukiwania wygenerowany komputera](./media/log-analytics-log-searches/oms-search-measure-max03.png)

Ta funkcja działa prawidłowo w przypadku liczb, ale współdziała również z pól daty i godziny. Ostatnio jest przydatne toocheck dla hello lub sygnatura czasowa ostatniej dowolne dane indeksowanym dla każdego komputera. Na przykład: gdy został hello najnowszych zabezpieczeń zgłoszone zdarzenie dla każdej maszyny?

```
Type=ConfigurationChange | Measure Max(TimeGenerated) by Computer
```

## <a name="use-hello-avg-function-with-hello-measure-command"></a>Funkcja avg hello za pomocą polecenia miary hello
Hello Avg() funkcji statystycznych używane z miarą umożliwia toocalculate hello średnią wartość niektóre pola, a grupy wyniki za hello w tym samym lub innym polu. Jest to użyteczne w wielu przypadkach, takich jak dane dotyczące wydajności.

Zaczniemy dane dotyczące wydajności. Należy pamiętać, że OMS aktualnie zbiera dane liczników wydajności dla systemu Windows i Linux maszyny.

toosearch dla *wszystkie* dane dotyczące wydajności, zapytanie najprostsze hello jest:

```
Type=Perf
```

![wyszukiwanie start Śr.](./media/log-analytics-log-searches/oms-search-avg01.png)

Witaj pierwszą rzeczą, którą można zauważyć jest czy analizy dzienników przedstawiono trzy perspektyw: lista, na której przedstawiono przedstawiającego rekordy rzeczywiste hello za hello na wykresach. Tabela, która przedstawia widok tabelaryczny danych licznika wydajności. i metryki, który wskazuje wykresów dla hello liczników wydajności.

Powyższy obraz powitania istnieją dwa zestawy pola oznaczone wskazujące hello poniżej:

* pierwszy zestaw Hello identyfikuje nazwę licznika wydajności systemu Windows, nazwa obiektu i nazwę wystąpienia w hello zapytania filtru. Są to hello pola prawdopodobnie będą najczęściej używane jako aspekty/filtrów
* **Równowartości** jest wartość rzeczywista hello hello licznika. W tym przykładzie wartość hello jest *75*.
* **TimeGenerated** jest 12:51 w formacie 24-godzinnym.

Oto widoku metryki hello na wykresie.

![wyszukiwanie start Śr.](./media/log-analytics-log-searches/oms-search-avg02.png)

Po informacji o hello wydajności rekordu kształtu, a o przeczytaj informacje o innych technik wyszukiwania można użyć miary Avg() tooaggregate ten typ danych liczbowych.

Poniżej przedstawiono prosty przykład:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" | Measure Avg(CounterValue) by Computer
```

![Wyszukaj samplevalue Śr.](./media/log-analytics-log-searches/oms-search-avg03.png)

W tym przykładzie wybierz licznik wydajności hello łączny czas procesora CPU i średnia przez komputer. Chcesz toonarrow dół hello tooonly Twojego wyniki ostatniego 6 godzin, można formant filtru czasu hello lub określ kwerendy w następujący sposób:

```
Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer
```

### <a name="toosearch-using-hello-avg-function-with-hello-measure-command"></a>za pomocą funkcji AVG. hello za pomocą polecenia miary hello toosearch
* W polu zapytania wyszukiwania hello wpisz `Type=Perf  ObjectName:Processor  InstanceName:_Total  CounterName:"% Processor Time" TimeGenerated>NOW-6HOURS | Measure Avg(CounterValue) by Computer`.

Można zagregować i skorelować danych *między* komputerów. Na przykład, załóżmy, że masz zestawu hostów w jakieś farmy, gdzie każdy węzeł jest taki sam tooany, drugi i one tylko do tego samego typu pracy i obciążenia powinien uwzględniać około powitalne wszystkie. Można pobrać ich liczniki, które go w jednym z hello następujących zapytań i uzyskać średnie hello całej farmy. Można uruchomić, wybierając hello komputerów z hello poniższy przykład:

```
Type=Perf AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Teraz, gdy masz hello komputery mają również tylko tooselect dwa kluczowe wskaźniki wydajności (KPI): % użycia procesora CPU i % wolnego miejsca na dysku. Tak staje się części zapytania hello:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS
```

Teraz można dodać komputery i liczniki z hello poniższy przykład:

```
Type=Perf InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03")
```

Masz bardzo określonego zaznaczenia, dlatego hello **miar Avg()** polecenia przywrócić średnia hello nie na komputerze, ale w farmie hello, grupując przez CounterName. Na przykład:

```
Type=Perf  InstanceName:_Total  ((ObjectName:Processor AND CounterName:"% Processor Time") OR (ObjectName="LogicalDisk" AND CounterName="% Free Space")) AND TimeGenerated>NOW-4HOURS AND (Computer="AzureMktg01" OR Computer="AzureMktg02" OR Computer="AzureMktg03") | Measure Avg(CounterValue) by CounterName
```

Zapewnia widok compact przydatne kilka kluczowych wskaźników wydajności w danym środowisku.

![Grupowanie avg wyszukiwania](./media/log-analytics-log-searches/oms-search-avg04.png)

Łatwo za pomocą zapytania wyszukiwania hello w pulpicie nawigacyjnym. Na przykład można zapisać kwerendę wyszukiwania hello i utworzyć pulpit nawigacyjny z niego o nazwie *kluczowych wskaźników wydajności sieci Web farmy*. toolearn więcej informacji na temat korzystania z pulpitów nawigacyjnych, zobacz [utworzyć niestandardowy pulpit nawigacyjny w analizy dzienników](log-analytics-dashboards.md).

![pulpit nawigacyjny avg wyszukiwania](./media/log-analytics-log-searches/oms-search-avg05.png)

### <a name="use-hello-sum-function-with-hello-measure-command"></a>Funkcja sum hello za pomocą polecenia miary hello
Funkcja sum Hello jest podobne funkcje tooother hello miary polecenia. Można zobaczyć przykład o jak toouse hello funkcja sum [Wyszukaj dzienniki IIS W3C w Microsoft Azure Operational Insights](http://blogs.msdn.com/b/dmuscett/archive/2014/09/20/w3c-iis-logs-search-in-system-center-advisor-limited-preview.aspx).

Można użyć Max() i Min() z liczb, daty i godziny oraz ciągów tekstowych. Ciągi tekstowe są posortowane alfabetycznie i uzyskać pierwszy i ostatni.

Jednak nie można używać Sum() z wyjątkiem pól wartości liczbowych. Dotyczy to również tooAvg().

### <a name="use-hello-percentile-function-with-hello-measure-command"></a>Użyj funkcji percentylu hello za pomocą polecenia miary hello
funkcja PERCENTYL Hello jest podobne tooAvg() i Sum() można używać tylko jego pól wartości liczbowych. Można użyć dowolnego percentyl między 1 too99 na pola liczbowego. Możesz także używać ich obu **percentyl** i **pct** poleceń. Oto kilka przykładów:  

```
Type:Perf CounterName:"DiskTransers/sec" |measure percentile95(CurrentValue) by Computer
```
```
Type:Perf ObjectName=LogicalDisk CounterName="Current Disk Queue Length" Computer="MyComputerName" | measure pct65(CurrentValue) by InstanceName
```

## <a name="use-hello-where-command"></a>Używaj hello, gdzie jest to polecenie
Witaj, gdy polecenie działa jak filtr, ale mogą być stosowane w filtrze toofurther potoku hello agregowana wyniki oferowanych przez polecenie miary — jako min. tooraw wyniki, które zostały przefiltrowane na początku hello zapytania.

Na przykład:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer
```

Można dodać inny potoku "|" znaków i hello, gdzie tooonly polecenia uzyskać komputerów, których średnie wykorzystanie Procesora jest powyżej 80% z hello następujący przykład:

```
Type=Perf  CounterName="% Processor Time"  InstanceName="_Total" | Measure Avg(CounterValue) as AVGCPU by Computer | Where AVGCPU>80
```

Jeśli znasz program Microsoft System Center — Operations Manager można traktować hello w przypadku, gdy polecenia w zakresie pakietu zarządzania. Przykład Witaj, gdyby regułę, pierwsza część zapytania hello hello będzie hello źródła danych i hello gdzie polecenie będzie hello wykrywanie warunku.

Można użyć zapytania hello jako Kafelek **Mój pulpit nawigacyjny**, jako monitor sortuje, toosee, gdy komputer procesorów jest nadmiernie używany. toolearn więcej informacji na temat pulpitów nawigacyjnych, zobacz [utworzyć niestandardowy pulpit nawigacyjny w analizy dzienników](log-analytics-dashboards.md). Można również tworzyć i korzystać z pulpitów nawigacyjnych przy użyciu aplikacji mobilnej hello. Aby uzyskać więcej informacji, zobacz [aplikacji mobilnej OMS ](http://www.windowsphone.com/en-us/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865). Kafelkach dolnej dwa hello powitania po obrazu, zawiera hello monitor wyświetlane listy, a liczba. Zasadniczo należy zawsze ma numer toobe hello zero i hello toobe lista jest pusta. W przeciwnym razie oznacza warunek alertu. W razie potrzeby można użyć tootake spojrzeć na komputery, które są wykorzystanie.

![mobilnego pulpitu nawigacyjnego](./media/log-analytics-log-searches/oms-search-mobile.png)

## <a name="use-hello-in-operator"></a>Użyj hello w operatorze
Witaj *IN* operatora, wraz z *NOT IN* pozwala subsearches toouse, które są wyszukiwania, które zawierają inne wyszukiwania jako argument. Znajdują się w nawiasy {}, w innym *głównej* lub *zewnętrzne* wyszukiwania. wynik Hello subsearch, często listę różne wyniki, następnie jest używany jako argument w jego wyszukiwania podstawowego.

Możesz użyć subsearches toomatch podzestawy danych nie opisywane bezpośrednio w wyrażeniu wyszukiwania, ale mogą być generowane z wyszukiwania. Na przykład, jeśli interesuje Cię przy użyciu jednego toofind Wyszukaj wszystkie zdarzenia z *komputerów brakujących aktualizacji zabezpieczeń*, wówczas należy toodesign subsearch, która najpierw określi, że *komputerów brakujących aktualizacji zabezpieczeń*  przed znajdzie zdarzenia należące toothose hostów.

Tak, można express *komputerów aktualnie brakuje wymaganych aktualizacji zabezpieczeń* z hello następujące zapytania:

```
Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer
```    

![W przykładzie wyszukiwania](./media/log-analytics-log-searches/oms-search-in01-revised.png)

Po utworzeniu listy hello hello wyszukiwania można używać jako wewnętrzne wyszukiwania toofeed hello listę komputerów w zewnętrznym wyszukiwania (podstawowe), który będzie szukać zdarzenia dla tych komputerów. W tym celu otaczającej hello wewnętrzny wyszukiwania w nawiasach klamrowych i podawania wyniki jako możliwych wartości filtru/pola wyszukiwania zewnętrzne hello przy użyciu operatora IN hello. Zapytanie Hello będzie wyglądać:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer}
```
![W przykładzie wyszukiwania](./media/log-analytics-log-searches/oms-search-in02-revised.png)

Również powiadomienie hello czasu używany w hello wewnętrzny wyszukiwania, ponieważ filtr hello oceny aktualizacji systemu wykonuje migawkę wszystkich komputerów, co 24 godziny. Możesz wprowadzić hello wewnętrzny zapytania więcej lekkie i precyzyjne przez wyszukiwanie tylko jeden dzień. zewnętrzne wyszukiwania Hello użyje hello czasu wyboru w interfejsie użytkownika hello, pobierania zdarzeń z hello ostatnich 7 dni. Zobacz [operatorów logicznych](#boolean-operators) uzyskać więcej informacji o czasie operatorów.

Ponieważ użytkownik naprawdę tylko wyniki wyszukiwania wewnętrzny hello jako wartość filtru dla hello Użyj hello jednego zewnętrznego, można nadal stosować poleceń w hello zewnętrzne wyszukiwania. Na przykład można nadal hello grupy powyżej zdarzenia za pomocą innego polecenia miary:

```
Type=Event Computer IN {Type:Update UpdateState=Needed Optional=false Classification="Security Updates" TimeGenerated>NOW-24HOURS | measure count() by Computer} | measure count() by Source
```

![W przykładzie wyszukiwania](./media/log-analytics-log-searches/oms-search-in03-revised.png)

Ogólnie rzecz biorąc ma tooexecute Twojego zapytania wewnętrzny szybko ponieważ analizy dzienników ma przekroczeń limitu czasu po stronie serwera dla go, a także tooreturn niewielką ilość wyników. Jeśli hello wewnętrzny zapytanie zwraca więcej wyników, listy wyników hello obcinana, który może powodować tooreturn zewnętrzne wyszukiwania hello niepoprawnych wyników.

Inna reguła jest tego Wyszukaj wewnętrzny hello musi obecnie tooprovide *zagregowane* wyników. Innymi słowy, musi ona zawierać *miary* polecenia; nie można obecnie źródła danych pierwotnych wyników w zewnętrznym wyszukiwania.

Ponadto może istnieć tylko jeden operator IN oraz musi być hello filtr w zapytaniu hello. Nie może mieć wielu operatorów w lub czy to zasadniczo uniemożliwia uruchomiony wielu subsearches: hello punkt jest tego tylko jeden wyszukiwania sub/wewnętrzny ważne jest możliwe każdego zewnętrzne wyszukiwania.

Nawet w przypadku tych granic w umożliwia wielu rodzajów skorelowane wyszukiwania i umożliwia toodefine coś podobnego toogroups, takich jak komputery, użytkowników lub pliki — niezależnie od hello danych zawierają. Poniżej przedstawiono więcej przykładów:

**Wszystkie aktualizacje Brak z komputerów z wyłączonym ustawienie automatycznej aktualizacji**

```
Type=Update UpdateState=Needed Optional=false Computer IN {Type=UpdateSummary WindowsUpdateSetting=Manual | measure count() by Computer} | measure count() by KBID
```

**Wszystkie zdarzenia błędów z komputerów z uruchomionym programem SQL Server (=, którym dysponuje oceny SQL)**

```
Type=Event EventLevelName=error Computer IN {Type=SQLAssessmentRecommendation | measure count() by Computer}
```

**Wszystkie zdarzenia zabezpieczeń z komputerów, które są kontrolerami domeny (=, którym dysponuje oceny AD)**

```
Type=SecurityEvent Computer IN { Type=ADAssessmentRecommendation | measure count() by Computer }
```

**Które inne konta zalogowanych toohello samych komputerach, na którym konto BACONLAND\jochan zalogował się na?**

```
Type=SecurityEvent EventID=4624   Account!="BACONLAND\\jochan" Computer IN { Type=SecurityEvent EventID=4624   Account="BACONLAND\\jochan" | measure count() by Computer } | measure count() by Account
```

## <a name="use-hello-distinct-command"></a>Użyj polecenia różne hello
Jak nazwa hello sugeruje, to polecenie zawiera listę różnych wartości dla pola. Jest zaskakująco proste, ale bardzo przydatne. Witaj, które same może zostać osiągnięty przy polecenia count() miary również, jak pokazano poniżej.

```
Type=Event | Measure count() by Computer
```

![Przykład polecenia różne wyszukiwania](./media/log-analytics-log-searches/oms-search-distinct01-revised.png)

Jednak w przypadku wszystkich interesuje Cię tylko listę różne wartości i nie hello liczby dokumentów, których tej wartości, następnie DISTINCT zapewniają czyszczący i łatwiejsze tooread danych wyjściowych i krótszy składni, jak pokazano poniżej.

```
Type=Event | Distinct Computer
```
![Przykład polecenia różne wyszukiwania](./media/log-analytics-log-searches/oms-search-distinct02-revised.png)

## <a name="use-hello-countdistinct-function-with-hello-measure-command"></a>Funkcja countdistinct hello za pomocą polecenia miary hello
Funkcja countdistinct Hello zlicza hello unikatowe wartości w każdej grupie. Na przykład można użyć toocount hello liczba unikatowych komputerów raportowania dla każdego typu:

```
* | measure countdistinct(Computer) by Type
```

![OMS countdistinct](./media/log-analytics-log-searches/oms-countdistinct.png)

## <a name="use-hello-measure-interval-command"></a>Polecenie interwał hello miary
Z niemal zbierania danych wydajności w czasie rzeczywistym, można zbierać i wizualizować wszystkie licznika wydajności w analizy dzienników. Po prostu wprowadzanie zapytania hello **typu: wydajności** zwróci tysiące metryki wykresów na podstawie liczby hello liczników i serwerów w środowisku analizy dzienników. Z agregacją metryki na żądanie, można przyjrzeć się hello ogólną metryki w środowisku w wysokiego poziomu, a nowości w bardziej szczegółowe dane na potrzeby.

Załóżmy, że chcesz tooknow, co to jest hello średnie wykorzystanie Procesora na wszystkich komputerach. Spojrzenie na powitania średnie wykorzystanie Procesora dla każdego komputera, może nie być pomocne ponieważ może pobrać wygładzania wyników. toolook do bardziej szczegółowe informacje, można zagregować wyników czasu mniejsze fragmenty okna i wyglądu do szeregów czasowych w różnych wymiarach. Na przykład można wykonywać hello średniej godzinowej użycia procesora CPU na wszystkich komputerach w następujący sposób:

```
Type:Perf CounterName="% Processor Time" InstanceName="_Total" | measure avg(CounterValue) by Computer Interval 1HOUR
```

![Interwał średni miary](./media/log-analytics-log-searches/oms-measure-avg-interval.png)

Domyślnie te wyniki zostaną wyświetlone na wykresie wiersz interakcyjne wielu serii.  Ten wykres obsługuje serii przełączanie (z ponowne skalowanie osi y), powiększanie i kursora myszy.  opcję wyświetlania tabeli Hello jest wciąż dostępna na potrzeby przeglądania danych pierwotnych hello w razie potrzeby.

Można także grupować według innych pól. W tym przykładzie wyświetlane wszystkie liczniki % hello jednego określonego komputera, i chcesz się tooknow co to jest hello percentylu co godzinę 70 co licznika:

```
Type:Perf Computer=beefpatty4 CounterName=%* InstanceName=_Total | measure percentile70(CounterValue) by CounterName Interval 1HOUR
```
Jeden element toonote są te zapytania nie liczniki tooperformance ograniczone. Można je stosować tooany metryki. W tym przykładzie wyświetlane dzienniki programu IIS W3C. Chcę tooknow co to jest hello maksymalny czas, który przejmuje on 5 minut do przetwarzania każdego żądania:

```
Type:W3CIISLog | measure max(TimeTaken) by csMethod Interval 5MINUTES
```

### <a name="use-multiple-aggregates-in-one-query"></a>Użyj wielu wartości zagregowanych w jednym zapytaniu
Można określić wiele klauzul agregacji w poleceniu miary.  Każdy z nich można używać z aliasem niezależnie.  Jeśli nie zostanie podany, hello alias co nazwa pola będzie hello funkcji agregującej, która została użyta (tj. "avg(CounterValue)" jak avg(CounterValue)).

 ```
Type=WireData | measure avg(ReceivedBytes), avg(SentBytes) by Direction interval 1hour
```
![OMS multiaggregates1](./media/log-analytics-log-searches/oms-multiaggregates1.png)

Oto inny przykład:

 ```
* | measure countdistinct(Computer) as Computers, count() as TotalRecords by Type
```


## <a name="next-steps"></a>Następne kroki
Aby uzyskać dodatkowe informacje dziennika wyszukiwania zobacz:

* Użyj [pola niestandardowe w analizy dzienników](log-analytics-custom-fields.md) tooextend dziennik wyszukiwania.
* Przejrzyj hello [analizy dzienników dziennika odwołanie wyszukiwania](log-analytics-search-reference.md) tooview wszystkie hello wyszukiwania pól i aspektów, które są dostępne w analizy dzienników.
