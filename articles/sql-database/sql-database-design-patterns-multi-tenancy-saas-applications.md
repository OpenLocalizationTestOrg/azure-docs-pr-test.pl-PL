---
title: "wzorce aaaDesign dla wielodostępnych aplikacji SaaS i usługi Azure SQL Database | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono wymagania hello i muszą tooconsider typowe wzorce Architektura danych aplikacji bazy danych z wieloma dzierżawcami, które działają w środowisku chmury, a hello różnych wpływ na skojarzone z tych wzorców. Wyjaśniono również, jak bazy danych SQL Azure z elastycznych pul i elastycznych narzędzia pomóc spełnić te wymagania w sposób nie naruszenia."
keywords: 
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 1dd20c6b-ddbb-40ef-ad34-609d398d008a
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-design
ms.date: 02/01/2017
ms.author: srinia
ms.openlocfilehash: a4b58935b08cb78792e65a675d680de708b709fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multi-tenant-saas-applications-and-azure-sql-database"></a>Projektowanie wzorce dla wielodostępnych aplikacji SaaS i bazy danych SQL Azure
W tym artykule można zapoznać się hello wymagania i typowe wzorce Architektura danych z wieloma dzierżawcami oprogramowania jako usługa (SaaS) aplikacje baz danych, które są uruchamiane w środowisku chmury. Objaśniono także czynniki hello należy tooconsider i hello kompromisy wzorce projektowania. Pule elastyczne i narzędzi elastycznej bazy danych SQL Azure może pomóc własnych wymagań bez naruszania innych celów.

Deweloperzy czasami podejmować decyzje, które działają przed ich zainteresowaniami najlepsze długoterminowej podczas projektowania modeli dzierżawy dla warstwy danych hello aplikacje wielodostępne. Co najmniej początkowo deweloperzy mogą postrzegać łatwość programowania i obniżyć koszty dostawcy usług chmury jako ważniejsze od dzierżawcy izolacji lub hello skalowalność aplikacji. Ten wybór może prowadzić toocustomer zadowolenia problemy i kosztowne korekty kursu później.

Aplikacja wielodostępne jest aplikacji hostowanej w środowisku chmury i zapewnia hello sam zestaw usług toohundreds lub tysięcy dzierżawców, którzy nie udostępniać lub jego dane są widoczne. Przykładem jest aplikacja SaaS, która zapewnia usługi tootenants w środowisku hostowanych w chmurze.

## <a name="multi-tenant-applications"></a>Aplikacje wielodostępne
W aplikacjach wielodostępne danych i obciążenia mogą być łatwo partycjonowane. Można podzielić danych oraz obciążeniu, na przykład na bloki dzierżawy, ponieważ większość żądań są wykonywane w obrębie hello dzierżawcy. Ta właściwość jest związane z danych hello i obciążenia hello, a jego objawach wzorce aplikacji hello omówione w tym artykule.

Deweloperzy Użyj tego typu aplikacji na powitania w pełnym zakresie aplikacje oparte na chmurze, w tym:

* Partnera bazy danych aplikacji, które są toohello wykonano przejście co aplikacje SaaS w chmurze
* Skompilowany dla chmury hello hello tła aplikacji SaaS
* Bezpośrednie, uwzględniającym klienta aplikacji
* Pracownik aplikacjach enterprise

Aplikacje SaaS, które zostały zaprojektowane dla chmury hello i tych, których certyfikaty główne, aplikacje baz danych partnera są zwykle aplikacje wielodostępne. Te aplikacje SaaS dostarczanie specjalistycznych aplikacji jako dzierżaw tootheir usługi. Dzierżawcy można uzyskać dostępu do usługi aplikacji hello i mają pełne prawa własności skojarzone dane przechowywane w ramach aplikacji hello. Jednak zaletą tootake hello zalet SaaS, dzierżaw musi przekazanie pewną kontrolę nad ich danymi. Ufają tookeep dostawcy usługi SaaS hello swoje dane, bezpieczne i odizolowane od danych innych dzierżawców. Przykładem tego rodzaju wielodostępnych aplikacji SaaS są MYOB, SnelStart i Salesforce.com. Każda z tych aplikacji mogą być partycjonowane wzdłuż granic dzierżawy i wzorce projektowe aplikacji hello pomocy technicznej, które omówiono w tym artykule.

Aplikacje dostarczające usługi bezpośredniego toocustomers lub tooemployees w organizacji (użytkownicy często określonego tooas, zamiast dzierżawcy) są inną kategorię na powitania spektrum wielodostępnych aplikacji. Klienci subskrypcji usługi toohello i nie ma danych hello hello usługodawcy zbiera i przechowuje. Dostawcy usług ma mniej rygorystyczne tookeep wymagania odizolowane od siebie poza obowiązkowe dla instytucji rządowych zasad zachowania poufności danych swoich klientów. Przykładem tego rodzaju aplikacji wielodostępnych uwzględniającym klienta są nośnika dostawców zawartości, takich jak Netflix, serwis Spotify i Xbox LIVE. Inne przykłady aplikacji łatwo partitionable są skierowane do klienta, aplikacji w skali Internet lub aplikacji Internetu rzeczy (IoT), w którym każdy klienta lub urządzenia można służyć jako partycji. Granice partycji można oddzielić użytkowników i urządzeń.

Nie wszystkie aplikacje partycji łatwo wzdłuż jednej właściwości, takie jak dzierżawy, odbiorcy, użytkownika lub urządzenia. Zasób przedsiębiorstwa złożonych planowania aplikacji (ERP), na przykład ma produktów, zamówień i klientów. Zwykle ma on złożonych schematu z tysiącami wysokiej połączonych tabel.

Żadna strategia jednej partycji można zastosować tooall tabel i działa między obciążenia aplikacji. Ten artykuł skupia się na aplikacje wielodostępne, które łatwo partitionable danych i obciążeń.

## <a name="multi-tenant-application-design-trade-offs"></a>Kompromis projektowania aplikacji z wieloma dzierżawcami
wzorzec projektowy Hello wybierający zwykle Deweloper aplikacji wielodostępnej opiera się pod uwagę następujące czynniki hello:

* **Odizolowania dzierżawców**. Twórca Hello musi tooensure, że żaden z dzierżawców ma dzierżaw tooother niechcianego dostępu do danych. Witaj izolacji wymaganie rozszerza tooother właściwości, takie jak zapewnienie ochrony z sąsiadów zakłócenia, jest możliwe toorestore danych dzierżawcy i wdrażanie dostosowań specyficznego dla dzierżawy.
* **Koszt zasobów w chmurze**. Aplikacja SaaS musi toobe konkurencyjnych kosztów. Deweloper aplikacji wielodostępnych może wybierz toooptimize obniżenia kosztów hello użycie zasobów w chmurze, takie jak magazyn i obliczeniowe kosztów.
* **Łatwość DevOps**. Deweloper aplikacji wielodostępnych potrzebuje ochrony izolacji tooincorporate, obsługa, monitorowanie kondycji hello ich aplikacji i schemat bazy danych i rozwiązywania problemów dzierżawy. Złożoność w opracowywaniu aplikacji oraz operacji bezpośrednio przekłada tooincreased kosztów i będzie wymagał z zadowolenia dzierżawy.
* **Skalowalność**. Witaj możliwości tooincrementally dodać więcej dzierżaw i pojemności dla dzierżawców, którzy wymagają jest konieczne tooa powodzenie operacji SaaS.

Każdy z nich ma tooanother możliwości w porównaniu. Chmura najniższy koszt Hello oferty nie może oferować hello najodpowiedniejszym środowisko programistyczne. Ważne jest, aby dewelopera toomake bieżąco opcje te opcje i możliwości ich podczas procesu projektowania aplikacji hello.

Wzorzec popularnych programowanie jest toopack wielu dzierżawców do jednej lub kilku baz danych. Witaj zalety tego podejścia są niższe koszty, ponieważ płacisz za kilka baz danych i prostota względną hello pracy z ograniczoną liczbę baz danych. Jednak wraz z upływem czasu dewelopera wielodostępnych aplikacji SaaS będzie Pamiętaj, że ten wybór ma istotne downsides izolacji dzierżawców i skalowalność. W przypadku izolacji dzierżawców ważne, dodatkowego nakładu pracy jest wymagane tooprotect dzierżawy danych w magazynie udostępnionym przed nieautoryzowanym dostępem lub zakłócenia sąsiadów. Tego dodatkowego nakładu pracy może znacznie zwiększyć programistycznych i kosztów obsługi izolacji. Podobnie jeśli wymagana jest dodanie dzierżawcy, tym wzorcu projektowym wymaga zwykle od danych dzierżawy tooredistribute doświadczenia z całej bazy danych tooproperly skali hello danych warstwie aplikacji.  

Często izolacji dzierżawy jest podstawowe wymagania w aplikacjach wielodostępne SaaS, które automatycznie dostosowują się toobusinesses i organizacji. Deweloper może skłonny przez postrzegana zalet prostotę i koszt w porównaniu z izolacji dzierżawców i skalowalność. Takie rozwiązanie może okazać się złożone i kosztowne miarę rozwoju hello usługi i wymagania dotyczące izolacji dzierżawy staną się bardziej ważne i zarządzanych w warstwie aplikacji hello. Jednak w wielodostępnych aplikacji, które mają toocustomers usługi bezpośredniego, dla użytkownika, izolacji dzierżawców może być niższy priorytet niż optymalizacji dla koszt zasobów chmury.

## <a name="multi-tenant-data-models"></a>Modeli danych z wieloma dzierżawcami
Typowe rozwiązania projekt umieszczenia danych dzierżawy należy wykonać trzy różne modele, pokazany na rysunku 1.

![modeli danych aplikacji z wieloma dzierżawcami](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-multi-tenant-data-models.png)

Rysunek 1: Typowe projektowania rozwiązania modeli danych z wieloma dzierżawcami

* **Bazy danych dla dzierżawy**. Każdy dzierżawca ma własną bazę danych. Wszystkie dane specyficzne dla dzierżawy jest dzierżawy zamkniętej toohello bazy danych i odizolowane od pozostałych dzierżawców i ich danych.
* **Udostępnione bazy danych podzielonej**. Wiele dzierżaw współużytkować jeden z wielu baz danych. Odrębnego zestawu dzierżawcy jest przypisany tooeach bazy danych przy użyciu strategii partycjonowania, takich jak wyznaczania wartości skrótu, zakres lub listy partycjonowania. Ta strategia dystrybucji danych jest często tooas określonego dzielenia na fragmenty.
* **Udostępnione pojedynczej bazy danych**. Pojedynczy, czasami duży bazy danych zawiera dane dla wszystkich dzierżawców, które są rozróżniane w kolumnie Identyfikator dzierżawy.

> [!NOTE]
> Deweloper aplikacji może wybrać tooplace różnych dzierżaw w schematach innej bazy danych, a następnie użyj hello schematu nazwa toodisambiguate hello różnym dzierżawcom. Nie zaleca się tą metodą, ponieważ zwykle wymaga hello korzystanie z dynamicznego SQL i nie może być aktywne buforowanie planu. W hello dalszej części tego artykułu możemy skupić się na udostępnionych hello tabeli podejście do tej kategorii wielodostępnych aplikacji.
> 
> 

## <a name="popular-multi-tenant-data-models"></a>Modele popularnych danych z wieloma dzierżawcami
Jest ważne tooevaluate hello różnych typów modeli danych wielodostępne pod względem hello aplikacji projektowania kompromis, który już określiliśmy. Czynniki te pomagają scharakteryzowania hello trzech opisanych wcześniej najbardziej typowych modeli danych z wieloma dzierżawcami i ich użycia bazy danych, jak pokazano na rysunku 2.

* **Izolacja**. Witaj stopień izolacji między dzierżawcami może być środek izolacji dzierżawców, ile osiąga modelu danych.
* **Koszt zasobów w chmurze**. Witaj ilość udostępniania zasobów między dzierżawcami zoptymalizować koszt zasobów chmury. Zasób można zdefiniować jako hello obliczeniowej i pamięci masowej kosztów.
* **Koszt DevOps**. Witaj łatwość tworzenia aplikacji, wdrażania i zarządzania zmniejsza całkowity koszt operacji SaaS.  

Na rysunku 2 osi hello Y pokazuje hello poziom izolacji dzierżawców. oś Hello X pokazuje hello poziom udostępniania zasobów. Szary Hello ukośnej strzałki w środku hello wskazuje kierunek hello kosztów DevOps, zmierzające tooincrease lub zmniejszenie.

![Wzorce projektowe popularnych aplikacji wieloma dzierżawcami](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-popular-application-patterns.png)

Rysunek 2: Modele popularnych danych wielodostępne

Hello wiązania kwadrantu prawym dolnym na rysunku 2 przedstawiono wzorzec aplikacji, który używa potencjalnie dużą, udostępnionych pojedynczej bazy danych i hello udostępnione tabeli (lub osobnych schematu) podejście. To ułatwia udostępnianie, ponieważ wszystkie dzierżawcy używają hello sama baza danych zasobów (Procesora, pamięci, wejście/wyjście) w jednej bazie danych zasobów. Ale izolacji dzierżawców, jest ograniczona. Może być konieczne tootake dzierżaw tooprotect dodatkowe kroki od siebie w warstwie aplikacji hello. Te dodatkowe kroki mogą znacznie zwiększyć hello DevOps koszt tworzenia i zarządzania aplikacji hello. Skala hello hello sprzętu, który obsługuje bazę danych hello jest ograniczona skalowalność.

wiązania kwadrantu lewym dolnym Hello na rysunku 2 przedstawiono wielu dzierżawców podzielonej między wieloma bazami danych (zwykle innego sprzętu jednostek skalowania). Każda baza danych obsługuje podzbiór dzierżawcy, jakich adresów dotyczą skalowalność hello z innymi wzorami. Jeśli większej pojemności jest wymagana w przypadku dzierżaw więcej, można umieścić na nowych baz danych przydzielone jednostki skalowania sprzętu toonew łatwo hello dzierżaw. Jednak ilość hello udostępniania zasobów zostanie zmniejszona. Tylko do dzierżawców dotyczącymi hello takie same jednostki skalowania udostępniać zasoby. Metoda ta umożliwia małego poprawy tootenant izolacji, ponieważ wiele dzierżaw nadal są zawsze umieszczane bez automatycznie chronione od siebie nawzajem akcje. Złożoność aplikacji pozostaje wysoki.

wiązania kwadrantu lewej górnej Hello na rysunku 2 jest hello trzeci rozwiązanie. Dane każdego dzierżawcy umieszcza w własną bazę danych. Takie podejście ma właściwości dobrej izolacji dzierżawców, ale ogranicza udostępniania zasobów, gdy każda baza danych ma własną zasobów dedykowanych. Ta metoda jest zalecana, jeśli wszystkie dzierżawy mają przewidywalna obciążeń. Jeśli obciążenia dzierżaw są mniej przewidywalne, nie można zoptymalizować dostawcy hello udostępniania zasobów. Nieprzewidywalność jest typowe dla aplikacji SaaS. dostawcy Hello albo należy udostępnić nadmierne wymagania toomeet lub niższy zasobów. Każda z tych operacji powoduje wyższe koszty lub niższy zadowolenia dzierżawy. Wyższy stopień zasobów, udostępnianie dzierżaw staje się bardziej ekonomiczne rozwiązanie hello toomake pożądane. Coraz hello bazy danych również zwiększa toodeploy koszt DevOps i obsługa aplikacji hello. Pomimo tych problemów ta metoda zapewnia izolację najlepszym i najłatwiejszy hello dzierżaw.

Te czynniki wpływają również hello wzorzec projektowy, który klient wybierze:

* **Własność danych dzierżawy**. Aplikacja, w którym dzierżaw zachować własność własne dane objawach hello wzorzec pojedynczej bazy danych dla każdego dzierżawcy.
* **Skalowalność**. Aplikacja, która dotyczy setki tysięcy lub miliony dzierżaw objawach udostępniania podejścia, takie jak dzielenia na fragmenty bazy danych. Wymagania dotyczące izolacji nadal może stanowić wyzwanie.
* **Wartość i business modelu**. Jeśli aplikacja na dzierżawcy przychodu relacjami małych (mniej niż dolara), wymagania dotyczące izolacji stają się mniej istotny i udostępnionej bazy danych. W przypadku kilku kwoty lub więcej przychód na dzierżawy modelu bazy danych na dzierżawy jest coraz. Może pomóc, zmniejszyć koszty rozwoju.

Podana hello projektowania kompromisy pokazany na rysunku 2, idealne rozwiązanie w modelu wielodostępnym musi właściwości izolacji dzierżawy dobrej tooincorporate z zasobem optymalne udostępnianie między dzierżawcami. Ten model mieści się w kategorii hello opisanego w wiązania kwadrantu prawym górnym hello na rysunku 2.

## <a name="multi-tenancy-support-in-azure-sql-database"></a>Obsługa wielu dzierżawców w bazie danych SQL Azure
Baza danych SQL Azure obsługuje wszystkie wzorce wielodostępnych aplikacji wyróżnione na rysunku 2. Pule elastyczne obsługuje ona również wzorzec aplikacji, który łączy udostępniania zasobów dobrej i podejścia hello izolacji zalet hello bazy danych dla dzierżawy (zobacz wiązania kwadrantu prawym górnym hello na rysunku 3). Narzędzi elastycznej bazy danych i możliwości w bazie danych SQL pomóc zmniejszyć hello toodevelop kosztów i działanie aplikacji, która ma wiele baz danych (wyświetlane w obszarze hello cieniowania na rysunku 3). Te narzędzia ułatwiają tworzenie i zarządzanie aplikacjami, które korzystają z dowolnych hello wzorce obsługi wielu baz danych.

![Wzorce w bazie danych Azure SQL](./media/sql-database-design-patterns-multi-tenancy-saas-applications/sql-database-patterns-sqldb.png)

Rysunek 3: Wzorce wielodostępnych aplikacji w bazie danych SQL Azure

## <a name="database-per-tenant-model-with-elastic-pools-and-tools"></a>Model bazy danych dla dzierżawy o elastycznych pul i narzędzia
Pule elastyczne w bazie danych SQL łączyć izolacji dzierżawcy z zasobów między dzierżawy baz danych toobetter Obsługa hello bazy danych dla dzierżawy podejście do udostępniania. Baza danych SQL jest rozwiązanie SaaS dostawców, którzy tworzą aplikacje wielodostępne warstwy danych. obciążenia Hello zasobu udostępnianie między dzierżawcami przewiduje się z warstwy usług bazy danych toohello warstwy aplikacji hello. z zadania elastyczne, elastyczne zapytania transakcji elastycznej i biblioteki klienta elastycznej bazy danych hello upraszcza Hello złożoność zarządzania i wykonywanie zapytań na dużą skalę w bazach danych.

| Wymagania dotyczące aplikacji | Funkcje bazy danych SQL |
| --- | --- |
| Izolacji dzierżawców i udostępnianie zasobów |[Pule elastyczne](sql-database-elastic-pool.md): Przydziel pulę zasobów bazy danych SQL i współużytkują zasoby hello między różnymi bazami danych. Ponadto pojedynczych baz danych można narysować tyle samo zasobów z puli hello jako tooaccommodate wymagana pojemność żądanie nagłego termin toochanges w obciążeń dzierżawców. Hello puli elastycznej sam można skalować w górę lub w dół zgodnie z potrzebami. Pule elastyczne udostępniają łatwość zarządzania i monitorowania i rozwiązywania problemów na poziomie puli hello. |
| Łatwość DevOps dla baz danych |[Pule elastyczne](sql-database-elastic-pool.md): jak wspomniano wcześniej. |
| | [Zapytanie elastycznej](sql-database-elastic-query-horizontal-partitioning.md): zapytania dla baz danych na potrzeby raportowania lub cross dzierżawy analizy. |
| | [Zadania elastyczne](sql-database-elastic-jobs-overview.md): pakiet i niezawodne wdrażanie operacji konserwacji bazy danych lub schemat bazy danych zmiany toomultiple baz danych. |
| | [Transakcje elastycznej](sql-database-elastic-transactions-overview.md): proces powoduje zmianę tooseveral baz danych w sposób atomic i izolowanym. Elastyczne transakcje są wymagane, gdy aplikacje muszą "wszystkie lub żadne" gwarancje przez kilka operacji w bazie danych. |
| | [Biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md): Zarządzanie dystrybucje danych i mapy dzierżawy toodatabases. |

## <a name="shared-models"></a>Udostępnione modele
Jak opisano wcześniej, dostawców większości SaaS, podejście modelu udostępnionego może stanowić problemy z problemami dotyczącymi izolacji dzierżawy i złożoności przy opracowywaniu aplikacji oraz konserwacji. Jednak na aplikacje wielodostępne, które zapewniają usługi bezpośrednio dzierżawy tooconsumers, wymagania dotyczące izolacji nie może być wysoki priorytet jako minimalizowania kosztów. Mogą one toopack stanie dzierżaw w przynajmniej jednej bazy danych na koszty tooreduce o wysokiej gęstości. Modele udostępnione bazy danych przy użyciu pojedynczej bazy danych lub wielu baz danych podzielonej może spowodować dodatkowych korzyści w koszt udostępniania i ogólnej zasobu. Baza danych SQL Azure zapewnia izolację lepsze bezpieczeństwo i zarządzania na dużą skalę w warstwie danych hello kompilacji niektórych funkcji, które ułatwiają klientom.

| Wymagania dotyczące aplikacji | Funkcje bazy danych SQL |
| --- | --- |
| Funkcje zabezpieczeń izolacji |[Zabezpieczenia na poziomie wiersza](https://msdn.microsoft.com/library/dn765131.aspx) |
| [Schemat bazy danych](https://msdn.microsoft.com/library/dd207005.aspx) | |
| Łatwość DevOps dla baz danych |[Elastyczne zapytania](sql-database-elastic-query-horizontal-partitioning.md) |
| | [Zadania elastyczne](sql-database-elastic-jobs-overview.md) |
| | [Elastyczne transakcji](sql-database-elastic-transactions-overview.md) |
| | [Biblioteka kliencka Elastic Database](sql-database-elastic-database-client-library.md) |
| | [Podziel elastycznej bazy danych i scalania](sql-database-elastic-scale-overview-split-and-merge.md) |

## <a name="summary"></a>Podsumowanie
Wymagania dotyczące izolacji dzierżawy są ważne w przypadku większości aplikacji wielodostępnych SaaS. Witaj najlepszych opcji tooprovide izolacji silnie leans kierunku hello podejście bazy danych dla dzierżawy. Witaj innych dwa podejścia wymagają inwestycji w warstwach złożonych aplikacji, które wymagają programowanie wykwalifikowanych pracowników tooprovide izolacji, co znacznie zwiększa koszt i ryzyko. Jeśli wymagania dotyczące izolacji nie uwzględnia się na początku programowanie usługi hello, może być bardziej kosztowne w modelach dwóch pierwszych hello modernizacji je. wady głównego Hello skojarzone z modelem bazy danych dla dzierżawy hello są koszty zasobów chmury pokrewne tooincreased tooreduced udostępniania, obsługi i zarządzania wielu baz danych. Deweloperzy aplikacji SaaS napotykają po wysłaniu tych kompromisy.

Chociaż kompromisy może być istotne bariery z większość dostawców usług bazy danych w chmurze, bazę danych SQL Azure eliminuje bariery hello z puli elastycznej i możliwości elastycznej bazy danych. Deweloperzy SaaS można łączyć właściwości izolacji hello modelu bazy danych na dzierżawy i zoptymalizować zasobów usprawnienia zarządzania hello i udostępniania wielu baz danych za pomocą elastycznych pul i powiązane z nim narzędzia.

Dostawcy wielodostępnych aplikacji, które nie mają żadnych wymagań izolacji dzierżawy i który pakietu dzierżaw w bazie danych o wysokiej gęstości może się okazać, że udostępnionych danych modeli wynik w dodatkowych efektywna współużytkowanie zasobów i zmniejszyć całkowity koszt. Narzędzi elastycznej bazy danych w usłudze Azure SQL Database, bibliotek dzielenia na fragmenty i funkcje zabezpieczeń ułatwiają tworzenie i zarządzanie nimi aplikacje wielodostępne dostawców w modelu SaaS.

## <a name="next-steps"></a>Następne kroki
[Wprowadzenie do narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md) z przykładową aplikację prezentującą powitania klienta biblioteki.

Utwórz [puli elastycznej niestandardowy pulpit nawigacyjny rozwiązania saas](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools-custom-dashboard) z przykładowej aplikacji, który korzysta z puli elastycznej dla rozwiązania ekonomicznych, skalowalnych bazy danych.

Za pomocą narzędzi bazy danych SQL Azure hello[migracji istniejącej bazy danych tooscale limit](sql-database-elastic-convert-to-use-elastic-tools.md).

toocreate puli elastycznej za pomocą hello Azure portalu, zobacz [tworzenia puli elastycznej](sql-database-elastic-pool-manage-portal.md).  

Dowiedz się, jak za[monitorować i zarządzać nimi puli elastycznej](sql-database-elastic-pool-manage-portal.md).

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Wdrażanie i Eksploruj aplikacji wielodostępnych, która używa bazy danych SQL Azure - Wingtip SaaS](sql-database-saas-tutorial.md)
* [Co to jest puli elastycznej platformy Azure?](sql-database-elastic-pool.md)
* [Scaling out with Azure SQL Database (Skalowanie w poziomie za pomocą usługi Azure SQL Database)](sql-database-elastic-scale-introduction.md)
* [aplikacje wielodostępne z narzędzi elastycznej bazy danych i zabezpieczenia na poziomie wiersza](sql-database-elastic-tools-multi-tenant-row-level-security.md)
* [Uwierzytelnianie w aplikacjach wielu dzierżawców przy użyciu usługi Azure Active Directory i OpenID Connect](../guidance/guidance-multitenant-identity-authenticate.md)
* [Aplikacja Tailspin Surveys](../guidance/guidance-multitenant-identity-tailspin.md)


## <a name="questions-and-feature-requests"></a>Pytania i żądania funkcji

Odpowiedzi na pytania, Znajdź NAS w hello [forum bazy danych SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted). Dodaj żądanie funkcji w hello [forum opinii bazy danych SQL](https://feedback.azure.com/forums/217321-sql-database/).

