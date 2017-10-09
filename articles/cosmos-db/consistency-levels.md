---
title: "poziomy aaaConsistency w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Azure DB rozwiązania Cosmos ma pięć spójności poziomy toohelp saldo ostatecznego spójności, dostępnością i opóźnieniem kompromis."
keywords: "spójność ostateczna azure rozwiązania cosmos db, azure, programu Microsoft azure"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: cgronlun
documentationcenter: 
ms.assetid: 3fe51cfa-a889-4a4a-b320-16bf871fe74c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac399c229d0856cd811bc81568536e519af3300f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tunable-data-consistency-levels-in-azure-cosmos-db"></a>Poziomy spójności danych dostosowywalne w usłudze Azure DB rozwiązania Cosmos
Azure DB rozwiązania Cosmos zaprojektowano z hello tła z globalnego dystrybucji pamiętać dla każdego modelu danych. Jest zaprojektowana toooffer przewidywalną małe opóźnienia gwarancji, umowa SLA dostępności 99,99% i wielu dobrze zdefiniowany rozluźnić modeli spójności. Obecnie bazy danych Azure rozwiązania Cosmos zawiera pięć poziomów spójności: silne, nieaktualność, sesji, prefiks spójne i "ostateczna". 

Oprócz **silne** i **spójność ostateczna** modeli często oferowane przez rozproszonych baz danych, bazy danych rozwiązania Cosmos Azure udostępnia trzy modele spójności starannie wersja i operationalized więcej i zweryfikowała ich przydatności przed rzeczywistych przypadków użycia. Są to hello **ograniczone nieaktualności**, **sesji**, i **spójne prefiks** poziomy spójności. Zbiorczo te poziomy spójności pięć Włącz toomake dobrze uzasadnione kompromis między spójności, dostępnością i opóźnieniem. 

## <a name="distributed-databases-and-consistency"></a>Rozproszone baz danych i spójności
Komercyjnie rozpowszechniane bazy danych można podzielić na dwie kategorie: bazy danych, które nie oferują żadnych dobrze zdefiniowanych, sprawdzalnych opcji spójności, i bazy danych, które oferują dwie skrajne opcje programowania (spójność silna lub ostateczna). 

Witaj wcześniejsze obciążeń aplikacji deweloperom minutia protokołach replikacji i oczekuje wady i zalety trudne toomake między spójności, dostępności, opóźnienia i przepływności. ostatnie Hello umieszcza toochoose wykorzystania, jeden Witaj dwie wartości graniczne. Pomimo liczebności hello badań i propozycje więcej niż 50 modeli spójności hello społeczności rozproszoną bazę danych nie został toocommercialize możliwe poziomy spójności poza silne i ewentualnej spójności. Rozwiązania cosmos DB umożliwia deweloperom toochoose między pięć modeli dobrze zdefiniowany spójności wzdłuż spektrum spójności hello — siły, ograniczone nieaktualności, [sesji](http://dl.acm.org/citation.cfm?id=383631), prefiks spójne i "ostateczna". 

![Azure DB rozwiązania Cosmos oferuje wiele dobrze zdefiniowanych toochoose modeli (swobodna) spójności z](./media/consistency-levels/five-consistency-levels.png)

Witaj w poniższej tabeli przedstawiono hello gwarancje określonych przez każdy poziom spójności.
 
**Poziomy spójności i gwarancje**

| Poziom spójności | Gwarancje |
| --- | --- |
| Silna | Operacje atomowe |
| Powiązana nieaktualność | Spójny prefiks. Odczyty opóźnione w stosunku do zapisów o k prefiksów lub interwał równy t |
| Sesja   | Spójny prefiks. Monotoniczne odczyty, monotoniczne zapisy, odczytywanie swoich zapisów, zapisy następują po odczytach |
| Spójny prefiks | Aktualizacje, zwracane są niektóre prefiks wszystkie aktualizacje hello, z luki |
| Ostateczna  | Odczyty poza kolejnością |

Można skonfigurować hello domyślnego poziomu spójności na Twoim koncie DB rozwiązania Cosmos (i później zastąpić spójności hello na określone żądanie odczytu). Wewnętrznie hello domyślnego poziomu spójności stosuje toodata w hello partycji zestawy, które mogą obejmować regionów. Spójność sesji przy użyciu około 73% naszych dzierżawcy, a spójność powiązanej nieaktualności preferowane jest 20%. Firma Microsoft obserwować, że około 3% klientów wypróbować różne poziomy spójności początkowo przed rozpoczęciem na wybór spójności określonych aplikacji. Możemy również obserwować, czy tylko 2% naszych dzierżaw zastąpienie poziomy spójności na podstawie danego żądania. 

W DB rozwiązania Cosmos Odczyty podawane w sesji, prefiks spójne i spójność ostateczna dwukrotnie są jako tanie jako odczyty z nieaktualności silne lub ograniczonych. Rozwiązania cosmos bazy danych ma branży kompleksowe SLA 99,99%, w tym gwarancje spójności oraz dostępność, przepustowości i opóźnień. Zastosujemy [sprawdzania linearizability](http://dl.acm.org/citation.cfm?id=1806634), które działa nieprzerwanie przez naszych telemetrii usługi i jawnie raporty żadnych tooyou naruszeń spójności. Aby uzyskać ograniczone nieaktualności, możemy monitorowania i raportowania, które miały wszelkie naruszenia i granice t. Dla wszystkich pięciu poziomów spójności swobodna możemy również zgłosić hello [Metryka prawdopodobieństwa spójność powiązanej nieaktualności](http://dl.acm.org/citation.cfm?id=2212359) tooyou bezpośrednio.  

## <a name="scope-of-consistency"></a>Zakres spójności
poziom szczegółowości Hello spójności jest zakresie tooa żądanie jednego użytkownika. Żądanie zapisu może odpowiadać tooan insert, replace, upsert lub usunąć transakcji. Podobnie jak w przypadku operacji zapisu, transakcji odczytu/zapytania jest również tooa zakresie pojedynczego użytkownika żądania. Hello użytkownika może być wymagane toopaginate za pośrednictwem dużej zestaw wyników, obejmujących wiele partycji, ale każda odczytać transakcji jest tooa zakresie jednej strony i udostępniane przez w ramach jednej partycji.

## <a name="consistency-levels"></a>Poziomy spójności
Domyślny poziom spójności można skonfigurować na Twoim koncie bazy danych, stosowanym kolekcje tooall (i baz danych) na koncie DB rozwiązania Cosmos. Domyślnie wszystkie odczyty i zapytań wystawiony na podstawie hello zasobów zdefiniowane przez użytkownika, użyj poziomu spójności hello domyślne z określonego na powitania konta bazy danych. Może osłabić hello poziomu spójności odczytu/zapytania określonego żądania przy użyciu w każdym hello obsługiwane interfejsów API. Istnieje pięć typów poziomów spójności obsługiwane przez protokół replikacji bazy danych Azure rozwiązania Cosmos hello, które zapewniają wyczyść zależność między spójności określone gwarancje i wydajności, zgodnie z opisem w tej sekcji.

**Silne**: 

* Zapewnia wysoki poziom spójności [linearizability](https://aphyr.com/posts/313-strong-consistency-models) gwarancji z hello odczytuje gwarantowane tooreturn hello najnowszej wersji elementu. 
* Silna spójność gwarantuje, że zapis jest widoczny dopiero w po jest trwałym zatwierdzeniu przez hello kworum Większość replik. Zapis jest albo synchronicznie trwałym zatwierdzeniu przez zarówno hello podstawowego, jak i kworum hello liczbę pomocniczych baz danych lub jest zostało przerwane. Odczytu zawsze zostaje potwierdzony hello większością głosów kworum do odczytu, klient nigdy nie można wyświetlić niezatwierdzone lub jego część zapisu i zawsze jest gwarantowana tooread hello najnowszych potwierdzonego zapisu. 
* Azure konta rozwiązania Cosmos bazy danych, które są skonfigurowane toouse wysoki poziom spójności nie można skojarzyć więcej niż jeden region platformy Azure z użyciem konta bazy danych Azure rozwiązania Cosmos. 
* Witaj kosztów operacji odczytu (na podstawie [jednostek żądania](request-units.md) używane) z wysoki poziom spójności jest wyższy niż sesji i "ostateczna", ale same hello jako spójność powiązanej nieaktualności.

**Ograniczone nieaktualności**: 

* Spójność powiązanej nieaktualności gwarantuje, że odczyty hello może opóźniona zapisy, przez co najwyżej *K* wersji lub prefiksy elementu lub *t* interwał czasu. 
* W związku z tym podczas wybierania ograniczone nieaktualności, hello "nieaktualności" można skonfigurować na dwa sposoby: numer wersji *K* elementu hello za pomocą którego odczyty hello opóźniona zapisy hello i interwał czasu hello *t* 
* Ograniczone nieaktualności oferty globalne zamówienia z wyjątkiem w hello "nieaktualności okno". Witaj monotoniczna odczytu gwarancje istnieje w obrębie regionu wewnątrz lub na zewnątrz hello "nieaktualności okno". 
* Spójność powiązanej nieaktualności zapewnia gwarancję spójności silniejsze niż sesji lub spójność ostateczna. Dla aplikacji rozproszonych globalnie zaleca się, że używasz spójność powiązanej nieaktualności do sytuacji, gdy będzie toohave wysoki poziom spójności, takich jak, ale również mają dostępności 99,99% i małe opóźnienia. 
* Azure kont rozwiązania Cosmos bazy danych, które są skonfigurowane przy użyciu spójność powiązanej nieaktualności można skojarzyć dowolną liczbę regiony platformy Azure z użyciem konta bazy danych Azure rozwiązania Cosmos. 
* Witaj kosztów operacji odczytu (pod względem używane RUs) z spójność powiązanej nieaktualności jest wyższy niż sesji i spójność ostateczna, ale same hello jako wysoki poziom spójności.

**Sesja**: 

* W przeciwieństwie do modeli globalne spójności hello oferowane przez poziomy spójności nieaktualności silne i ograniczonego spójność sesji jest tooa zakresie sesji klienta. 
* Spójność sesji jest idealny dla wszystkich scenariuszy, w którym sesję użytkownika lub urządzenia uczestniczy, ponieważ gwarantuje monotoniczna odczyty, monotoniczna zapisu i odczytu gwarancje własne zapisów (RYW). 
* Spójność sesji zapewnia przewidywalną spójność sesji, a maksymalna odczytu przepływności, a jednocześnie najmniejsze opóźnienia zapisów hello i odczytuje. 
* Azure kont rozwiązania Cosmos bazy danych, które są skonfigurowane przy użyciu spójność sesji można skojarzyć dowolną liczbę regiony platformy Azure z użyciem konta bazy danych Azure rozwiązania Cosmos. 
* Witaj z sesji poziomu spójności jest mniejsza niż nieaktualności silne i ograniczonego, ale spójność ostateczna więcej niż koszt operacja odczytu (pod względem używane RUs)

<a id="consistent-prefix"></a>
**Prefiks spójne**: 

* Prefiks spójne gwarantuje, że w przypadku braku kolejnych zapisów hello repliki w grupie hello ostatecznie zbieżność. 
* Prefiks spójne gwarantuje, że odczyty nigdy nie zobaczyć zapisy poza kolejnością. Jeśli wykonano operacji zapisu w kolejności hello `A, B, C`, klient widzi albo `A`, `A,B`, lub `A,B,C`, ale nigdy nie poza kolejnością jak `A,C` lub `B,A,C`.
* Azure kont rozwiązania Cosmos bazy danych, które są skonfigurowane przy użyciu prefiksu spójne spójności można skojarzyć dowolną liczbę regiony platformy Azure z użyciem konta bazy danych Azure rozwiązania Cosmos. 

**Ewentualne**: 

* Spójność ostateczna gwarantuje, że w przypadku braku kolejnych zapisów hello repliki w grupie hello ostatecznie zbieżność. 
* Spójność ostateczna jest hello formularza najsłabszą spójność, których klient może pobrać hello wartości, które są starsze niż hello z nich ma zauważony.
* Spójność ostateczna zapewnia najsłabszą hello spójności odczytu, ale oferuje hello można uzyskać najmniejsze opóźnienia zarówno odczytów i zapisów.
* Azure kont rozwiązania Cosmos bazy danych, które są skonfigurowane przy użyciu spójność ostateczna można skojarzyć dowolną liczbę regiony platformy Azure z użyciem konta bazy danych Azure rozwiązania Cosmos. 
* Witaj kosztów operacji odczytu (pod względem używane RUs) z spójność ostateczna powitania poziom jest hello najniższy wszystkie poziomy spójności bazy danych Azure rozwiązania Cosmos hello.

## <a name="configuring-hello-default-consistency-level"></a>Konfigurowanie poziomu spójności domyślne hello
1. W hello [portalu Azure](https://portal.azure.com/), w hello przechodzenia kliknij pozycję **bazy danych Azure rozwiązania Cosmos**.
2. W hello **bazy danych Azure rozwiązania Cosmos** bloku, toomodify konta bazy danych wybierz hello.
3. W bloku konta usługi powitania kliknij **domyślna spójność**.
4. W hello **domyślna spójność** bloku, wybierz hello nowy poziom spójności i kliknij przycisk **zapisać**.
   
    ![Zrzut ekranu przedstawiający wyróżnianie hello ikonę ustawień i spójności domyślny wpis](./media/consistency-levels/database-consistency-level-1.png)

## <a name="consistency-levels-for-queries"></a>Poziomy spójności dla zapytań
Domyślnie zasoby zdefiniowane przez użytkownika poziomu spójności hello zapytania jest hello tego samego poziomu spójności hello Odczyt. Domyślnie indeks hello jest aktualizowany synchronicznie na każdym insert, Zamień lub usuń kontener elementu toohello DB rozwiązania Cosmos. Ta umożliwia zapytania hello toohonor hello tego samego poziomu spójności co punktu odczytów. Bazy danych Azure rozwiązania Cosmos jest zoptymalizowany zapisu i obsługuje stałej ilości zapisy, indeks synchroniczne konserwacji i obsługująca spójne zapytania, można skonfigurować pewne tooupdate kolekcje ich indeksu opóźnieniem. Dodatkowo indeksowanie z opóźnieniem zwiększa wydajność zapisu hello i jest idealne dla scenariuszy wprowadzanie zbiorczego obciążenia jest głównie ciężki odczytu.  

| Tryb indeksowania | Odczytuje | Zapytania |
| --- | --- | --- |
| Spójność (ustawienie domyślne) |Wybierz jedną z nieaktualności silne, ograniczone, sesji, spójne prefiksu lub ostatecznego |Wybierz jedną z nieaktualności silne, ograniczone, sesji lub ostatecznego |
| Powolne |Wybierz jedną z nieaktualności silne, ograniczone, sesji, spójne prefiksu lub ostatecznego |Ostateczna |
| Brak |Wybierz jedną z nieaktualności silne, ograniczone, sesji, spójne prefiksu lub ostatecznego |Nie dotyczy |

Jako z żądaniami odczytu, możesz obniżyć poziom spójności hello żądania określonej kwerendy w każdym interfejsu API.

## <a name="next-steps"></a>Następne kroki
Jeśli chcesz toodo więcej odczytywania o poziomy spójności i wady i zalety, zaleca się hello następujące zasoby:

* Jakub Dougowi. Wyjaśniono spójności replikowanych danych za pośrednictwem baseball (klip wideo).   
  [https://www.youtube.com/Watch?v=gluIh8zd26I](https://www.youtube.com/watch?v=gluIh8zd26I)
* Jakub Dougowi. Wyjaśniono spójności replikowanych danych za pośrednictwem baseball.   
  [http://Research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.PDF](http://research.microsoft.com/pubs/157411/ConsistencyAndBaseballReport.pdf)
* Jakub Dougowi. Gwarancje sesji słabo spójności replikowanych danych.   
  [http://DL.ACM.org/CITATION.cfm?ID=383631](http://dl.acm.org/citation.cfm?id=383631)
* Abadi Danielowi. Wady i zalety spójności w projekcie: nowoczesnych systemów bazy danych dystrybucji: zakończenie jest tylko część wątku hello ".   
  [http://Computer.org/CSDL/mags/co/2012/02/mco2012020037-ABS.HTML](http://computer.org/csdl/mags/co/2012/02/mco2012020037-abs.html)
* Peterowi Bailis, Shivaram Venkataraman, Michael J. tw, Joseph M. Hellerstein, Stoica zakres przechowywania. Prawdopodobieństwa ograniczone nieaktualności (PBS) praktyczne częściowe kworum.   
  [http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.PDF](http://vldb.org/pvldb/vol5/p776_peterbailis_vldb2012.pdf)
* Werner Vogels. Ostateczna spójne — uruchomić ponownie.    
  [http://allthingsdistributed.com/2008/12/eventually_consistent.HTML](http://allthingsdistributed.com/2008/12/eventually_consistent.html)
* Moni Naor, wełny Avishai hello obciążenia, pojemności i dostępności z kworum systemów, dziennika SIAM Computing, v.27 n.2, 447 p.423, kwietnia 1998.
  [http://epubs.siam.org/DOI/ABS/10.1137/S0097539795281232](http://epubs.siam.org/doi/abs/10.1137/S0097539795281232)
* Burckhardt Sebastianowi, Krzysztof Dern, Macanal Musuvathi, Tan Royowi, każdy: linearizability pełny i automatyczne sprawdzanie, postępowania hello 2010 ACM SIGPLAN konferencji programowania języka projekt i implementację, czerwca 05 10 2010 naszej, Ontario, Kanada [doi > 10.1145/1806596.1806634] [http://dl.acm.org/citation.cfm?id=1806634](http://dl.acm.org/citation.cfm?id=1806634)
* Peterowi Bailis, Shivaram Venkataraman, Michael J. tw, Joseph M. Hellerstein, Stoica zakres przechowywania Probabilistically ograniczone nieaktualności do praktycznych kworum częściowe postępowania hello wydzielony VLDB, v.5 n.8, 787 p.776, kwietnia 2012 [http:// DL.ACM.org/CITATION.cfm?ID=2212359](http://dl.acm.org/citation.cfm?id=2212359)
