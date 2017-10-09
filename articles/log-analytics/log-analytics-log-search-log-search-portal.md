---
title: aaaUsing hello wyszukiwania dziennika portal Azure Log Analytics | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera samouczek, który opisuje sposób toocreate dziennika wyszukiwania i analizowanie danych przechowywanych w obszarze roboczym analizy dzienników przy użyciu hello dziennik wyszukiwania portalu.  Samouczek Hello obejmuje uruchamiania niektórych zapytań proste tooreturn różnych typów danych oraz analizowanie wyników."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a>Tworzenie wyszukiwań dziennika w przy użyciu hello dziennik wyszukiwania portalu usługi Analiza dzienników Azure

> [!NOTE]
> W tym artykule opisano hello portal wyszukiwania dziennika przy użyciu hello nowego języka zapytań usługi Analiza dzienników Azure.  Możesz dowiedzieć się więcej o nowy język hello i uzyskać hello procedury tooupgrade obszaru roboczego na [uaktualnienia wyszukiwania dziennika toonew roboczym usługi Analiza dzienników Azure](log-analytics-log-search-upgrade.md).  
>
> Jeśli obszar roboczy nie został uaktualniony toohello nowy język zapytań, należy zapoznać się zbyt[wyszukiwanie danych przy użyciu dziennika wyszukiwania w analizy dzienników](log-analytics-log-searches.md) Aby uzyskać informacje o bieżącej wersji hello hello dziennik wyszukiwania portalu.

Ten artykuł zawiera samouczek, który opisuje sposób toocreate dziennika wyszukiwania i analizowanie danych przechowywanych w obszarze roboczym analizy dzienników przy użyciu hello dziennik wyszukiwania portalu.  Samouczek Hello obejmuje uruchamiania niektórych zapytań proste tooreturn różnych typów danych oraz analizowanie wyników.  Głównie funkcji w portalu wyszukiwania dziennika hello modyfikowanie hello zapytanie, zamiast bezpośrednie modyfikowanie.  Szczegółowe informacje dotyczące bezpośredniego edytowania hello zapytania, zobacz hello [Query Language reference](https://go.microsoft.com/fwlink/?linkid=856079).

Wyszukiwanie toocreate w portalu analityka zaawansowane hello zamiast hello dziennik wyszukiwania portalu, zobacz [wprowadzenie hello Portal analityka](https://go.microsoft.com/fwlink/?linkid=856587).  Obu portalach Użyj hello tego samego zapytania języka tooaccess hello tych samych danych, w obszarze roboczym analizy dzienników hello.

## <a name="prerequisites"></a>Wymagania wstępne
W tym samouczku założono, że już obszar roboczy analizy dzienników z co najmniej jeden połączone źródła, które generuje dane dotyczące hello tooanalyze zapytania.  

- Jeśli nie masz obszaru roboczego, możesz utworzyć wolnego przy użyciu procedury hello na [Rozpoczynanie pracy z obszaru roboczego analizy dzienników](log-analytics-get-started.md).
- Co najmniej jednego połączenia [agenta Windows](log-analytics-windows-agents.md) lub [agenta systemu Linux](log-analytics-linux-agents.md) toohello obszaru roboczego.  

## <a name="open-hello-log-search-portal"></a>Otwórz hello dziennik wyszukiwania portalu
Rozpocznij od otwierania hello dziennik wyszukiwania portalu.  Można do niego dostęp w portalu OMS hello albo hello portalu Azure.

1. Otwórz hello portalu Azure.
2. Przejdź tooLog Analytics i wybierz obszar roboczy.
3. Wybierz opcję **wyszukiwania dziennika** toostay w portalu lub uruchamiania hello OMS portalu Azure, wybierając hello **portalu OMS** , a następnie klikając przycisk wyszukiwania dziennika hello.

![Przycisk wyszukiwania dziennika](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a>Tworzenie prostego wyszukiwania
Witaj najszybszy sposób tooretrieve toowork niektóre dane z jest proste zapytanie zwracające wszystkie rekordy w tabeli.  Jeśli masz obszar roboczy dowolnego systemu Windows lub Linux klientów połączonych tooyour, będziesz mieć danych albo hello zdarzenia (system Windows) lub tabeli dziennika systemowego (Linux).

Wpisz jeden hello następującego zapytania w polu wyszukiwania hello i kliknij przycisk Wyszukaj hello.  

```
Event
```
```
Syslog
```

Dane są zwracane w hello domyślny widok listy, a widać, ile całkowita liczba rekordów zostały zwrócone.

![Prostego zapytania](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

Tylko hello pierwszy kilka właściwości każdego rekordu są wyświetlane.  Kliknij przycisk **Pokaż więcej** toodisplay wszystkie właściwości dla określonego rekordu.

![Szczegóły rekordu](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a>Ustaw zakres czasu hello
Każdy rekord zebrane przez analizy dzienników ma **TimeGenerated** właściwość, która zawiera hello Data i godzina utworzenia tego rekordu hello.  Zapytania w portalu wyszukiwania dziennika hello zwraca tylko rekordy z **TimeGenerated** w zakresie czasu hello, który jest wyświetlany na powitania po lewej stronie ekranu hello.  

Filtr czasu hello można zmienić, wybierając z listy rozwijanej hello lub modyfikując hello suwaka.  Witaj suwak Wyświetla wykres słupkowy przedstawiający hello względną liczbę rekordów dla każdego segmentu czasu w zakresie hello.  Ten segment będą się różnić w zależności od zakresu hello.

zakres czasu domyślny Hello jest **1 dzień**.  Zmień tę wartość za**7 dni**, i zwiększyć hello całkowita liczba rekordów.

![Zakres czasu daty](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a>Filtrowanie wyników zapytania hello
Na powitania lewej części ekranu hello jest okienko filtru hello, dzięki czemu można tooadd filtrowania toohello zapytań bez modyfikowania jej bezpośrednio.  Kilka właściwości zwracanych rekordów hello są wyświetlane z najwyższym dziesięć wartościami z ich liczba rekordów.

Jeśli pracujesz z **zdarzeń**, wybierz hello pole wyboru obok zbyt**błąd** w obszarze **EVENTLEVELNAME**.   Jeśli pracujesz z **Syslog**, wybierz hello pole wyboru obok zbyt**błąd** w obszarze **poziom ważności**.  Spowoduje to zmianę zapytań hello tooone powitania po toolimit hello powoduje tooerror zdarzenia.

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtr](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

Okienko filtru toohello Dodaj właściwości, wybierając **dodać toofilters** z menu właściwości hello na jednym hello rekordów.

![Dodawanie toofilter menu](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

Można ustawić hello samego filtru, wybierając **filtru** menu właściwości hello rekord z wartością hello ma toofilter.  

Masz tylko hello **filtru** opcji dla właściwości o nazwie ich w kolorze niebieskim.  Są to *wyszukiwanie* pola, które są indeksowane dla warunki wyszukiwania.  Pola w kolorze szarym są *wolne tekst można wyszukiwać* pola o tylko hello **Pokaż odwołania** opcji.  Ta opcja zwraca rekordy, które mają tę wartość w dowolnej właściwości.

![Menu filtrowania](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

Można grupować hello wyników dla jednej właściwości, wybierając hello **Grupuj według** opcję w menu rekord hello.  Spowoduje to dodanie [Podsumuj](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) operator tooyour kwerendę, która wyświetla wyniki hello na wykresie.  Można grupować w więcej niż jedną właściwość, ale będzie potrzebny tooedit hello zapytania bezpośredniego.  Wybierz hello rekordów menu dalej Witaj Witaj **komputera** właściwości i wybierz **Grupuj według "Komputer"**.  

![Grupuj według komputera](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a>Praca z wynikami
portal wyszukiwania dziennika Hello ma wiele funkcji do pracy z hello wyników zapytania.  Można sortować, filtr i grupa powoduje tooanalyze hello danych bez modyfikowania zapytania rzeczywiste hello.  Domyślnie nie są sortowane wyniki zapytania.

tooview hello danych w formie tabeli, która zapewnia dodatkowe opcje filtrowania i sortowania, kliknij przycisk **tabeli**.  

![Widok tabeli](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

Kliknij strzałkę hello przez szczegóły hello tooview rekordów dla tego rekordu.

![Sortowanie wyników](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

Sortuj według dowolnego pola, klikając jej nagłówek kolumny.

![Sortowanie wyników](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

Filtrowanie wyników hello na określoną wartość w kolumnie hello, klikając przycisk Filtr hello i podając warunek filtru.

![Filtrowanie wyników](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

Grupy dla kolumny przez przeciągnięcie nagłówka kolumny toohello górnym hello wyników.  Można grupować według wielu pól przeciągając wiele kolumn toohello top.

![Wyniki grupy](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a>Praca z danych wydajności
Dane wydajności dla agentów systemów Windows i Linux są przechowywane w obszarze roboczym analizy dzienników hello w hello **wydajności** tabeli.  Rejestruje wydajności wyglądać podobnie jak dowolny inny rekord i firma Microsoft może zapisywać prostego zapytania, która zwraca wszystkie rekordy wydajności, podobnie jak ze zdarzeniami.

```
Perf
```

![Dane dotyczące wydajności](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

Mimo że zwracanie miliony rekordów wszystkie obiekty i liczniki wydajności nie jest bardzo przydatne.  Można użyć hello tych samych metod używanych powyżej toofilter hello danych lub po prostu wpisz hello następujące zapytanie bezpośrednio do pola wyszukiwania hello dziennika.  To polecenie zwróci tylko procesor rekordów użycia dla komputerów z systemami Windows i Linux.

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![Użycie procesora](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

To ogranicza hello danych tooa określonego licznika, ale jego nadal nie umieszcza je w postaci jest szczególnie przydatne.  Wyświetlanie danych hello w wykres liniowy, ale najpierw należy toogroup go przez komputer i TimeGenerated.  toogroup według wielu pól, należy toomodify hello zapytania bezpośrednio, więc modyfikować hello zapytania toohello poniżej.  Używa hello [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) funkcja na powitania **równowartości** właściwości toocalculate hello średnią wartość ciągu każdej godziny.

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Wykres danych wydajności](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

Teraz, gdy dane hello odpowiednio są grupowane, można je wyświetlić na wykresie visual przez dodanie hello [renderowania](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) operatora.  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Wykres liniowy](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o język zapytań usługi Analiza dzienników hello na [wprowadzenie hello Portal analityka](https://go.microsoft.com/fwlink/?linkid=856079).
- Zapoznaj się z artykułem samouczek przy użyciu hello [portal analityka zaawansowane](https://go.microsoft.com/fwlink/?linkid=856587) co pozwala toorun hello tego samego zapytania i dostęp do tych samych danych co hello dziennik wyszukiwania portalu hello.
