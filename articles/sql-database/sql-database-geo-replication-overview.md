---
title: "aaaFailover grup i aktywna replikacja geograficzna — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Grupy pracy awaryjnej automatycznie z aktywna replikacja geograficzna umożliwia toosetup 4 replik bazy danych w żadnym hello centrach danych platformy Azure i pracy awaryjnej autoomatically w zdarzeniu hello awarii."
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2a29f657-82fb-4283-9a83-e14a144bfd93
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 07/10/2017
ms.author: sashan
ms.openlocfilehash: 7a39af8505624c0f19c5abccff051af836b1f9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-failover-groups-and-active-geo-replication"></a>Omówienie: Grup trybu Failover i aktywna replikacja geograficzna
Aktywna replikacja geograficzna umożliwia tooconfigure zapasowe toofour czytelny pomocniczych baz danych w hello centrum danych tych samych lub różnych lokalizacji (regiony). Dodatkowej bazy danych są dostępne na potrzeby zapytań i pracy awaryjnej w przypadku hello data center awarii lub hello brakiem tooconnect toohello głównej bazy danych. Witaj pracy awaryjnej musi być inicjowana ręcznie przez aplikację hello hello użytkownika. Po przejściu w tryb failover hello nową podstawową ma końcowego innego połączenia. 

> [!NOTE]
> Aktywna replikacja geograficzna jest dostępna dla wszystkich baz danych w warstwach usług z wszystkich we wszystkich regionach.
>  

Grupy pracy awaryjnej automatycznie w usłudze Azure bazy danych SQL (w — wersja zapoznawcza) jest tooautomatically funkcja zaprojektowana bazy danych SQL Zarządzanie relacji — replikacja geograficzna, łączności i pracy awaryjnej na dużą skalę. Hello klientów korzyści hello możliwości tooautomatically odzyskać wielu powiązanych baz danych w regionie pomocniczym powitania po poważnej awarii regionalnych lub inne nieplanowanego zdarzenia, które powoduje utratę pełnej lub częściowej hello usługi baza danych SQL dostępność w regionie podstawowym hello. Ponadto użyciem hello do odczytu bazy danych w dodatkowej toooffload tylko do odczytu obciążeń.  Ponieważ grupy pracy awaryjnej automatycznie wymagają wielu baz danych, które muszą zostać skonfigurowane na serwerze podstawowym hello. Podstawowe i dodatkowe serwery muszą być w hello tej samej subskrypcji. Grupy pracy awaryjnej automatycznie obsługują replikacji wszystkich baz danych w hello grupy tooonly jednego serwera pomocniczego w innym regionie. Aktywna replikacja geograficzna, bez trybu failover automatycznie grup, umożliwia się too4 pomocnicze bazy danych w dowolnym regionie.

Jeśli używasz aktywna replikacja geograficzna i przyczyny głównej bazy danych nie powiedzie się, lub po prostu toobe potrzeb przełączony w tryb offline, można zainicjować tooany trybu failover z dodatkowej bazy danych. Podczas pracy awaryjnej jest aktywowane tooone hello pomocniczych baz danych, wszystkie inne pomocnicze bazy danych są automatycznie dołączane toohello nową podstawową. Jeśli używasz trybu failover automatyczne odzyskiwanie bazy danych (w podglądzie) toomanage i wszelkie awarii, który ma wpływ na jednego lub kilku baz danych hello w hello grupy powoduje automatyczną pracę awaryjną grup. Zasady trybu failover automatycznie hello, która najlepiej odpowiada Twoim potrzebom aplikacji można skonfigurować, lub można zrezygnować i korzystać z aktywacji ręczne. Ponadto pracy awaryjnej automatycznie grupy (w podglądzie) podaj odczytu i zapisu, a punkty końcowe odbiornika tylko do odczytu, które pozostają bez zmian podczas pracy w trybie Failover. Czy używać aktywacji ręczne lub automatyczne trybu failover, pracy awaryjnej zmienia wszystkie pomocnicze bazy danych w hello tooprimary grupy. Po zakończeniu pracy awaryjnej bazy danych hello rekord DNS hello jest aktualizowane automatycznie tooredirect hello punkty końcowe toohello nowy region.

Możesz zarządzać replikacji i trybu failover poszczególne bazy danych lub zestaw baz danych na serwerze lub w puli elastycznej za pomocą aktywna replikacja geograficzna. Możesz zrobić tego za pomocą hello [portalu Azure](sql-database-geo-replication-portal.md), [PowerShell](sql-database-geo-replication-powershell.md), [języka Transact-SQL](sql-database-geo-replication-transact-sql.md), lub hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163685.aspx). Po przejściu w tryb failover upewnij się, że hello wymagania dotyczące uwierzytelniania dla serwera i bazy danych są skonfigurowane na powitania nową podstawową. Aby uzyskać więcej informacji, zobacz [zabezpieczeń bazy danych SQL po awarii](sql-database-geo-replication-security-config.md). Dotyczy to zarówno tooactive — replikacja geograficzna i pracy awaryjnej automatycznie grupy (w — wersja zapoznawcza).

Aktywna replikacja geograficzna wykorzystanie hello [zawsze na](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) technologii tooasynchronously programu SQL Server to zreplikowanie zatwierdzonych transakcji w hello podstawowej bazy danych tooa pomocniczej bazie danych przy użyciu izolacji migawce zatwierdzonego odczytu (RCSI). Grupy pracy awaryjnej automatycznie stanowią semantyki grupy hello na górze aktywna replikacja geograficzna, ale hello sam mechanizm replikacji asynchronicznej jest używana. Gdy na dowolnym etapie, hello dodatkowej bazy danych może być nieco za hello podstawowej bazy danych, danych pomocniczych hello jest gwarantowana toonever ma częściowe transakcji. Nadmiarowość między region umożliwia odzyskiwanie tooquickly aplikacji z trwałą utratę całe centrum danych lub części spowodowane klęski żywiołowej, krytycznego błędów ludzkich lub złośliwych działań Centrum danych. Hello danych specyficznych dla celu punktu odzyskiwania można znaleźć w folderze [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).

Witaj poniższej ilustracji przedstawiono przykład aktywna replikacja geograficzna skonfigurowany z użyciem hello północno-środkowe stany regionu podstawowego i pomocniczego w hello południowo-środkowe stany regionu.

![Replikacja geograficzna relacji](./media/sql-database-active-geo-replication/geo-replication-relationship.png)

Ponieważ hello pomocniczej bazy danych można odczytać, mogą być używane toooffload obciążeń tylko do odczytu, takich jak zadania raportowania. Jeśli używasz aktywna replikacja geograficzna jest możliwe toocreate hello dodatkowej bazy danych w hello tego samego regionu podstawowego hello, ale nie zwiększa aplikacji hello odporności toocatastrophic błędów. Jeśli używasz trybu failover automatycznie grupy (w podglądzie) z dodatkowej bazy danych zawsze jest tworzony w innym regionie.

Ponadto toodisaster odzyskiwania aktywna replikacja geograficzna, mogą być używane w hello następujące scenariusze:

* **Baza danych migracji**: toomigrate aktywna replikacja geograficzna bazę danych z jednego serwera tooanother w trybie online można używać z minimalną przestoju.
* **Uaktualnianie aplikacji**: można utworzyć dodatkowe pomocniczy jako kopia tyłu podczas uaktualniania aplikacji.

tooachieve rzeczywistych ciągłość prowadzenia działalności biznesowej, dodawanie nadmiarowość bazy danych między centrami danych jest tylko część hello rozwiązania. Odzyskiwanie aplikacji (usługa) end-to-end po poważnej awarii wymaga odzyskiwania wszystkich składników, które stanowią hello usługi i usług zależnych. Przykładami tych składników oprogramowania klienckiego hello (na przykład przeglądarki z niestandardowych skryptów JavaScript), sieci Web, magazynu i DNS. Bardzo ważne, czy wszystkie składniki są odporne toohello tego samego błędów i staną się dostępne w celu czasu odzyskiwania hello (RTO) aplikacji jest. W związku z tym należy tooidentify wszystkich zależnych usług i zrozumienie hello gwarancje i możliwości, które zapewniają. Następnie należy przełączyć tooensure odpowiednie kroki, które funkcje usługi podczas hello trybu failover hello usług, od których zależy. Aby uzyskać więcej informacji na temat projektowania rozwiązań do odzyskiwania po awarii, zobacz [projektowania rozwiązań chmury za pomocą odzyskiwania po awarii aktywna replikacja geograficzna](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

## <a name="active-geo-replication-capabilities"></a>Aktywna replikacja geograficzna możliwości
Funkcja aktywna replikacja geograficzna Hello zapewnia hello następujące podstawowe możliwości:
* **Automatyczne asynchroniczną replikację**: pomocniczej bazy danych można utworzyć tylko przez dodanie tooan istniejącej bazy danych. Witaj dodatkowej mogą być tworzone w dowolnym serwerze bazy danych SQL Azure. Po utworzeniu hello dodatkowej bazy danych jest wypełniana hello dane skopiowane z hello podstawowej bazy danych. Ten proces jest nazywany wstępnego wypełniania. Po utworzeniu pomocniczej bazy danych i rozpoczęta, aktualizacje toohello podstawowej bazy danych są asynchroniczne automatycznie replikowane toohello dodatkowej bazy danych. Asynchroniczną replikację oznacza, że transakcje są zostało zatwierdzone na poziomie hello podstawowej bazy danych, przed ich replikowanych toohello dodatkowej bazy danych. 
* **Do odczytu bazy danych w dodatkowej**: aplikacja może uzyskać dostęp do pomocniczej bazy danych dla operacji tylko do odczytu za pomocą hello takie same lub podmiotów zabezpieczeń używane do uzyskiwania dostępu do hello podstawowej bazy danych. Witaj pomocniczej bazy danych działanie w ramach izolacji migawki tryb tooensure replikacji aktualizacje hello hello głównej (dziennika powtarzania) nie jest opóźnione przez zapytania są wykonywane na powitania dodatkowej.

   > [!NOTE]
   > powtarzania dziennika Hello jest opóźnione na powitania dodatkowej bazy danych, jeśli istnieją aktualizacje schematu odbiera z hello podstawowy wymagające blokady schematu na powitania dodatkowej bazy danych. 
   > 

* **Wiele elementów dodatkowych do odczytu**: dwa lub więcej pomocniczych baz danych zwiększenia nadmiarowości i poziom ochrony hello podstawowej bazy danych i aplikacji. Jeśli istnieje wiele pomocniczych baz danych, aplikacji hello pozostaje chroniony nawet w przypadku awarii jednego z dodatkowej bazy danych hello. Jeśli nie powiedzie się istnieje tylko jeden z dodatkowej bazy danych, aplikacji hello jest uwidaczniany toohigher ryzyka, dopóki nie zostanie utworzony nowy pomocniczej bazy danych.

   > [!NOTE]
   > Jeśli używasz aktywna replikacja geograficzna toobuild globalnie rozproszone aplikacji i wymagają tooprovide tylko do odczytu do toodata w regionach więcej niż 4, możesz utworzyć dodatkowej pomocniczej (proces znany jako łańcucha). W ten sposób można osiągnąć nieograniczoną skali replikacji bazy danych. Ponadto łańcucha zmniejsza obciążenie związane z hello replikacji z hello podstawowej bazy danych. rozwiązanie Hello jest opóźnienie replikacji zwiększona hello na powitania większość liścia dodatkowej w bazach danych. . 
   >

* **Obsługa elastycznej puli baz danych**: aktywna replikacja geograficzna można skonfigurować dla dowolnej bazy danych w każdej puli elastycznej. Witaj dodatkowej bazy danych może być w innej puli elastycznej. W przypadku regularnego baz danych hello dodatkowej można puli elastycznej i odwrotnie tak długo, jak są warstwy usług hello hello takie same. 
* **Poziom wydajności można skonfigurować z dodatkowej bazy danych hello**: pomocniczej bazy danych można tworzyć za pomocą niższego poziomu wydajności niż hello podstawowego. Podstawowe i pomocnicze bazy danych są wymagane toohave hello tej samej warstwie usługi. Ta opcja nie jest zalecana dla aplikacji z działania zapisu bazy danych wysokiej ponieważ opóźnienie replikacji zwiększona hello zwiększa hello ryzyko utraty danych znacznej po przejściu w tryb failover. Ponadto po pogarsza wydajność aplikacji hello trybu failover do hello nowego podstawowego jest uaktualniony tooa większą wydajność poziomu. Witaj dziennika we/wy wartość procentową wykresu w portalu Azure udostępnia tooestimate dobrze hello poziomu wydajności minimalnej hello dodatkowej, która jest wymagana toosustain hello replikacji obciążenia. Na przykład, jeśli P6 jest podstawową bazą danych (1000 DTU) i jego dziennikiem procent we/wy jest dodatkowej hello 50% wymaga co najmniej toobe P4 (500 DTU). Można również pobrać hello dziennika we/wy danych przy użyciu [sys.resource_stats](https://msdn.microsoft.com/library/dn269979.aspx) lub [sys.dm_db_resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) bazy danych widoków.  Aby uzyskać więcej informacji dotyczących poziomów wydajności baz danych SQL hello, zobacz [opcje bazy danych SQL i wydajność](sql-database-service-tiers.md). 
* **Kontrolowane przez użytkownika trybu failover i powrotu po awarii**: pomocniczej bazy danych w dowolnym momencie w aplikacji hello lub hello użytkownika może być jawnie wyłączone toohello podstawową rolą. Podczas hello rzeczywista awaria "nieplanowane" opcja powinna być używana, która wspiera natychmiast podstawowego hello toobe dodatkowej. Gdy podstawowego nie powiodło się hello odzyskuje i jest dostępny ponownie, hello system automatycznie hello znaczniki odzyskać głównej jako dodatkowej i przełączyć go instalując nową podstawową hello. Powodu toohello asynchroniczne rodzaj replikacji niewielką ilość danych mogą zostać utracone podczas niezaplanowanych operacji Failover Jeśli podstawowy ulegnie awarii, przed rozpoczęciem replikacji hello najnowszych zmian toohello dodatkowej. W przypadku awarii podstawowego przy użyciu wielu pomocnicze bazy danych za pośrednictwem systemu hello automatycznie skonfiguruje hello relacji replikacji i hello łącza nowo pozostałych toohello pomocniczych podwyższenia poziomu podstawowego bez interwencji użytkownika. Po awarii hello, który spowodował hello pracy awaryjnej jest niewielkie, może być regionu podstawowego toohello aplikacji hello tooreturn pożądane. toodo, że polecenie pracy awaryjnej hello powinna być wywoływana z hello "planowane" opcji. 
* **Synchronizacja poświadczeń i jego reguły zapory**: Firma Microsoft zaleca używanie [bazy danych reguły zapory](sql-database-firewall-configure.md) dla baz danych z replikacją geograficzną, reguły te mogą być replikowane z tooensure bazy danych hello wszystkie pomocnicze bazy danych ma Witaj tej samej reguły zapory jako głównej hello. Takie podejście eliminuje potrzebę hello klientów toomanually konfigurowania i konserwacji reguły zapory na serwerach hostujących zarówno hello podstawowych i pomocniczych baz danych. Podobnie za pomocą [zawarte bazy danych użytkowników](sql-database-manage-logins.md) danych dostęp zapewnia podstawowe i pomocnicze bazy danych zawsze hello poświadczenia tego samego użytkownika, dlatego podczas pracy w trybie failover nie przerwom termin toomismatches z nazwy logowania i hasła. O dodanie hello [usługi Azure Active Directory](../active-directory/active-directory-whatis.md)wyeliminowanie hello należy całkowicie zarządzania poświadczeniami w bazach danych i klientów można zarządzać użytkownika tooboth podstawowych i pomocniczych baz danych programu access.

## <a name="auto-failover-group-capabilities"></a>Funkcje grupy pracy awaryjnej automatycznie

Funkcja grup pracy awaryjnej automatycznie zapewnia zaawansowane Abstrakcja aktywna replikacja geograficzna dzięki obsłudze replikacji poziomu grupy i automatycznej pracy awaryjnej. Ponadto spowoduje usunięcie parametrów połączenia SQL hello hello konieczność toochange po pracy awaryjnej zapewniając punkty końcowe dodatkowe odbiornika hello. 

* **Praca awaryjna grupy**: można utworzyć jedną lub wiele grup trybu failover między dwoma serwerami w różnych regionach (podstawowych i pomocniczych serwerów). Każda grupa może zawierać co najmniej jednej bazy danych, które są odzyskiwane jako jednostki, w przypadku, gdy wszystkie lub niektóre bazy danych podstawowego stają się niedostępny z powodu awarii tooan w regionie podstawowym hello.  
* **Podstawowy serwer**: serwera obsługującego hello głównej bazy danych w hello trybu failover grupie.
* **Serwer pomocniczy**: serwera obsługującego hello dodatkowej bazy danych w grupie pracy awaryjnej hello. serwer pomocniczy Hello nie może być w hello tego samego regionu powitania serwera podstawowego.
* **Dodawanie grupy toofailover baz danych**: można umieścić szereg baz danych w ramach serwera lub w ramach elastyczna pula do hello same grupy pracy awaryjnej. Jeśli dodasz grupie toohello autonomicznej bazy danych, automatycznie tworzy pomocniczej bazy danych przy użyciu hello tej samej wersji i poziom wydajności. W przypadku hello podstawowej bazy danych w puli elastycznej, dodatkowej hello jest tworzony automatycznie w puli elastycznej hello z hello takie same nazwy. Po dodaniu bazy danych, która ma już pomocniczej bazy danych serwera pomocniczego hello, że replikacja geograficzna jest dziedziczona przez hello grupy.

   > [!NOTE]
   > Dodając bazy danych, która ma już pomocniczej bazy danych na serwerze, który nie jest częścią grupy pracy awaryjnej hello w nowym serwerem pomocniczym jest tworzony w powitania serwera pomocniczego. 
   >

* **Odbiornik odczytu i zapisu grupy pracy awaryjnej**: Rekord DNS CNAME jest sformatowany jako  **&lt;nazwę grupy pracy awaryjnej&gt;. database.windows.net** wskazującego toohello bieżący adres URL serwera podstawowego. Umożliwia aplikacji SQL odczytu i zapisu hello tootransparently ponownie toohello podstawowej bazy danych zmiany podstawowego powitania po pracy awaryjnej. 
* **Praca awaryjna grupy tylko do odczytu odbiornika**: Rekord DNS CNAME jest sformatowany jako  **&lt;nazwę grupy pracy awaryjnej&gt;. secondary.database.windows.net** wskazującego adres URL serwera pomocniczego toohello. Umożliwia aplikacji SQL tylko do odczytu, Połącz tootransparently hello pomocniczej bazy danych toohello przy użyciu hello określone reguły równoważenia obciążenia. Opcjonalnie można określić, jeśli chcesz hello tylko do odczytu toobe ruchu automatycznie przekierowane toohello podstawowego serwera podczas hello serwer pomocniczy jest niedostępny.
* **Zasady automatycznej pracy awaryjnej**: Domyślnie grupa pracy awaryjnej hello jest skonfigurowana przy użyciu zasad automatycznej pracy awaryjnej. Hello system wyzwala trybu failover, jak zostaje wykryta awaria hello. Jeśli chcesz, aby przepływ pracy trybu failover hello toocontrol z aplikacji hello, można wyłączyć automatycznej pracy awaryjnej. 
* **Ręcznego przełączania trybu failover**: Inicjuj tryb failover ręcznie w dowolnym momencie, niezależnie od hello konfiguracji automatycznej pracy awaryjnej. Jeśli zasady automatycznej pracy awaryjnej nie jest skonfigurowany ręcznego przełączania trybu failover jest baz danych wymagane toorecover hello trybu failover grupy. Możesz zainicjować wymuszonym lub przyjazną trybu failover (z pełnej synchronizacji danych). ostatnie Hello można regionu podstawowego toohello toorelocate używane hello aktywnego serwera. Po zakończeniu pracy awaryjnej hello rekordy DNS są automatycznie aktualizowane tooensure łączności toohello właściwym serwerem.
* **Okres prolongaty utraty danych**: ponieważ hello podstawowe i pomocnicze bazy danych są synchronizowane przy użyciu replikacji asynchronicznej hello w tryb failover może spowodować utratę danych. Można dostosować tooreflect zasady automatycznej pracy awaryjnej hello utraty toodata uszkodzenia aplikacji. Konfigurując **GracePeriodWithDataLossHours**, można kontrolować czas oczekiwania hello systemu przed rozpoczęciem pracy awaryjnej hello, który jest tooresult prawdopodobieństwo utraty danych. 

   > [!NOTE]
   > Jeśli system wykryje, że bazy danych hello w grupie hello są nadal w trybie online (na przykład awaria hello tylko wpływ na płaszczyźnie kontroli usługi hello), natychmiast aktywuje tryb failover hello z pełnej synchronizacji danych (przyjazna trybu failover) niezależnie od wartości hello ustawione przez **GracePeriodWithDataLossHours**. Takie zachowanie gwarantuje, że istnieje nie powoduje utraty danych podczas odzyskiwania hello. okres prolongaty Hello obowiązuje tylko wtedy, gdy jest to przyjazna trybu failover nie jest możliwe. Jeśli awaria hello jest skorygowane przed upływem okresu prolongaty hello, hello trybu failover nie został aktywowany.
   >

* **Wiele grup pracy awaryjnej**: można skonfigurować wiele grup pracy awaryjnej dla hello samej pary serwerów toocontrol hello skali przechodzenia w tryb failover. Każda grupa nie powiedzie się za pośrednictwem niezależnie. Jeśli aplikacja wielodostępne używa pule elastyczne, można użyć tej możliwości toomix podstawowych i pomocniczych baz danych w każdej puli. W ten sposób można zmniejszyć wpływ awarii tooonly hello połowy hello dzierżaw.

## <a name="best-practices-of-building-highly-available-service"></a>Najlepsze rozwiązania w zakresie tworzenia usługi wysokiej dostępności

toobuild wysokiej dostępności usługi, który używa klientom Witaj bazy danych Azure SQL należy przestrzegać następujących wytycznych:
- **Użyj grupy trybu failover**: można utworzyć jedną lub wiele grup trybu failover między dwoma serwerami w różnych regionach (podstawowych i pomocniczych serwerów). Każda grupa może zawierać co najmniej jednej bazy danych, które są odzyskiwane jako jednostki, w przypadku, gdy wszystkie lub niektóre bazy danych podstawowego stają się niedostępny z powodu awarii tooan w regionie podstawowym hello. grupy pracy awaryjnej Hello tworzy geograficznie pomocnicze bazy danych z hello sama usługa cel jako hello podstawowego. Podczas dodawania istniejącego — replikacja geograficzna relacji toohello trybu failover grupy upewnij się, że hello geograficznie / pomocniczych skonfigurowano hello sama usługa cel poziomu jako hello podstawowego.
- **Użyj odbiornika odczytu i zapisu dla obciążenia OLTP**: podczas wykonywania OLTP, użyj operacji  **&lt;nazwę grupy pracy awaryjnej&gt;. database.windows.net** jako adres URL serwera hello i hello połączenia będą automatycznie ukierunkowanej toohello podstawowej. Ten adres URL nie zmieni się po hello w tryb failover.  
Tryb failover hello Uwaga polega na aktualizowanie powitalne rekordu DNS tak powitania klienta połączenia będą przekierowane toohello nowego podstawowego tylko po powitania klienta DNS odświeżania pamięci podręcznej.
- **Użyj tylko do odczytu odbiornika dla obciążenia tylko do odczytu**: jeśli obciążenie logicznie odizolowane tylko do odczytu, które jest nieaktualności toocertain na uszkodzenia danych, można użyć hello dodatkowej bazy danych w aplikacji hello. Dla sesji tylko do odczytu  **&lt;nazwę grupy pracy awaryjnej&gt;. secondary.database.windows.net** jako adres URL serwera hello i hello połączenia będą automatycznie ukierunkowanej toohello dodatkowej. Zalecane jest również, wskazanej w parametrach połączenia do odczytu próba przy użyciu **ApplicationIntent = ReadOnly**. 
- **Przygotowanie do pogorszenia się wydajności**: decyzja pracy awaryjnej programu SQL jest niezależna od reszty hello aplikacji hello lub innych usług używanych. Aplikacja Hello może mieć wartość "mixed" z niektórymi składnikami w jeden region, a niektóre w innym. tooavoid hello degradacji, upewnij się, wdrożenie nadmiarowego aplikacji hello w regionie hello odzyskiwania po awarii i postępuj zgodnie z wytycznymi hello w tym artykule.  
Aplikacja hello Uwaga w regionie DR hello nie ma toouse ciąg innego połączenia.  
- **Przygotowanie do utraty danych**: wykrycie awarii SQL automatyczne wyzwolenie pracy awaryjnej odczytu i zapisu, jeśli najlepiej naszych wiedzy jest zerowy toohello utraty danych. W przeciwnym razie oczekuje na powitania okres określony przez **GracePeriodWithDataLossHours**. Jeśli określono **GracePeriodWithDataLossHours**, można przygotować do utraty danych. Ogólnie rzecz biorąc podczas awarii, Azure objawach dostępności. Jeśli niedopuszczalna utraty danych, upewnij się, że tooset **GracePeriodWithDataLossHours** wystarczająco dużą liczbę tooa, takich jak 24 godziny. 


## <a name="upgrading-or-downgrading-a-primary-database"></a>Uaktualnianie lub zmiany na starszą wersję podstawowej bazy danych
Możesz uaktualnić lub starszą wersję poziomu wydajności różnych tooa podstawowej bazy danych (w ramach hello sam warstwę usługi) bez odłączania wszystkie pomocnicze bazy danych. Podczas uaktualniania, zalecamy najpierw uaktualnić hello dodatkowej bazy danych, a następnie uaktualnić podstawowy hello. Podczas zmiany na starszą wersję, odwrócić kolejność hello: najpierw obniżyć hello podstawowej i starszą wersję hello pomocniczej. Po uaktualnieniu lub starszą wersję warstwy innej usługi tooa bazy danych hello jest wymuszana tego zalecenia. 

> [!NOTE]
> Jeśli zostały utworzone jako część konfiguracji grupy pracy awaryjnej hello dodatkowej bazy danych nie jest zalecane toodowngrade hello dodatkowej bazy danych. Jest to tooensure warstwę danych ma wystarczającą pojemność tooprocess Twojego zwykłe obciążenie po aktywowaniu trybu failover. 
>

## <a name="preventing-hello-loss-of-critical-data"></a>Zapobieganie hello utratę krytycznych danych
Powodu toohello duże opóźnienie sieci rozległej ciągła kopia używa mechanizmu replikacji asynchronicznej. Asynchroniczną replikację powoduje utratę danych nieuniknione Jeśli wystąpi błąd. Jednak niektóre aplikacje mogą wymagać bez utraty danych. tooprotect te aktualizacje krytyczne, Deweloper aplikacji może wywołać hello [operacja sp_wait_for_database_copy_sync](https://msdn.microsoft.com/library/dn467644.aspx) procedury systemu natychmiast po zatwierdzania transakcji hello. Wywoływanie **operacja sp_wait_for_database_copy_sync** hello bloki wywoływania wątku czasu ostatniej zatwierdzić transakcji hello przesyłane toohello dodatkowej bazy danych. Jednak nie oczekiwania dla hello przekazane transakcje toobe odtwarzany i zatwierdzona na powitania dodatkowej. **Operacja sp_wait_for_database_copy_sync** tooa zakresie określonych ciągła kopia łącza. Każdy użytkownik z hello połączenia prawa toohello podstawowej bazy danych można wywołać tej procedury.

> [!NOTE]
> **Operacja sp_wait_for_database_copy_sync** przed utratą danych po pracy awaryjnej, ale nie zagwarantuje pełną synchronizację, aby uzyskać dostęp do odczytu. Witaj opóźnienia spowodowane przez **operacja sp_wait_for_database_copy_sync** wywołania procedury może być znaczny i zależy od rozmiaru hello hello dziennika transakcji w czasie hello hello wywołania. 
> 

## <a name="programmatically-managing-failover-groups-and-active-geo-replication"></a>Programowe zarządzanie grupami trybu failover i aktywna replikacja geograficzna
Zgodnie z opisem wcześniej, pracy awaryjnej automatycznie grupy (w — wersja zapoznawcza) i aktywne — replikacja geograficzna może być także zarządzane programowo przy użyciu programu Azure PowerShell i hello interfejsu API REST. następujące tabele Hello opisano hello zestaw poleceń, które są dostępne.

**Interfejs API Menedżera zasobów Azure i zabezpieczenia oparte na rolach**: aktywna replikacja geograficzna zawiera zestaw interfejsów API usługi Azure Resource Manager do zarządzania tym hello [interfejsu API REST bazy danych SQL Azure](https://docs.microsoft.com/rest/api/sql/) i [Azure Polecenia cmdlet programu PowerShell](https://docs.microsoft.com/powershell/azure/overview). Te interfejsy API wymagają hello korzystania z grup zasobów i obsługują zabezpieczeń opartych na rolach (RBAC). Aby uzyskać więcej informacji dotyczących sposobu tooimplement dostęp do ról, zobacz [kontroli dostępu](../active-directory/role-based-access-control-what-is.md).

> [!NOTE]
> Wiele nowych funkcji aktywna replikacja geograficzna są obsługiwane tylko przy użyciu [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) na podstawie [interfejsu API REST SQL Azure](https://msdn.microsoft.com/library/azure/mt163571.aspx) i [poleceń cmdlet programu PowerShell bazy danych SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx). Witaj [(klasyczne) interfejsu API REST](https://msdn.microsoft.com/library/azure/dn505719.aspx) i [bazy danych SQL Azure (klasyczne) polecenia cmdlet](https://msdn.microsoft.com/library/azure/dn546723.aspx) są obsługiwane przy użyciu hello zaleca się API usługi Azure Resource Manager na podstawie zgodności z poprzednimi wersjami. 
> 

## <a name="manage-sql-database-failover-using-using-transact-sql"></a>Zarządzanie SQL bazy danych trybu failover przy użyciu języka Transact-SQL

| Polecenie | Opis |
| --- | --- |
| [ALTER DATABASE (baza danych Azure SQL)](https://msdn.microsoft.com/library/mt574871.aspx) |Użyj istniejącej bazy danych Dodaj serwer POMOCNICZY ON argument toocreate pomocniczej bazy danych i rozpoczyna się replikacja danych |
| [ALTER DATABASE (baza danych Azure SQL)](https://msdn.microsoft.com/library/mt574871.aspx) |Użyj trybu FAILOVER lub FORCE_FAILOVER_ALLOW_DATA_LOSS tooswitch awarię podstawowej tooinitiate toobe dodatkowej bazy danych |
| [ALTER DATABASE (baza danych Azure SQL)](https://msdn.microsoft.com/library/mt574871.aspx) |Użyj Usuń serwer POMOCNICZY ON tooterminate replikacji danych między bazą danych SQL i hello określony dodatkowej bazy danych. |
| [sys.geo_replication_links (baza danych SQL Azure)](https://msdn.microsoft.com/library/mt575501.aspx) |Zwraca informacje o wszystkich istniejących łączy replikacji dla każdej bazy danych na serwerze logicznym hello bazy danych SQL Azure. |
| [sys.dm_geo_replication_link_status (baza danych SQL Azure)](https://msdn.microsoft.com/library/mt575504.aspx) |Pobiera hello czas ostatniej replikacji, ostatni opóźnienie replikacji i inne informacje o łącza replikacji hello określonej bazy danych SQL. |
| [sys.dm_operation_status (baza danych SQL Azure)](https://msdn.microsoft.com/library/dn270022.aspx) |Wyświetla stan powitania dla wszystkich operacji bazy danych, takich jak stan hello hello łączy replikacji. |
| [Operacja sp_wait_for_database_copy_sync (baza danych SQL Azure)](https://msdn.microsoft.com/library/dn467644.aspx) |powoduje toowait aplikacji hello, dopóki wszystkie zatwierdzone transakcje są replikowane i potwierdzone przez hello aktywnej pomocniczej bazy danych. |
|  | |

## <a name="manage-sql-database-failover-using-using-powershell"></a>Zarządzanie SQL bazy danych trybu failover przy użyciu programu PowerShell

| Polecenie cmdlet | Opis |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Pobiera jeden lub więcej baz danych. |
| [Nowe AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary) |Tworzy pomocniczej bazy danych dla istniejącej bazy danych i rozpoczyna się replikacja danych. |
| [Zestaw AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary) |Zmienia awarię podstawowej tooinitiate toobe dodatkowej bazy danych. |
| [Usuń AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) |Kończy replikacji danych między bazą danych SQL i hello określonego dodatkowej bazy danych. |
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) |Pobiera hello — replikacja geograficzna łącza między bazą danych SQL Azure i grupy zasobów lub SQL Server. |
| [Nowe AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   To polecenie tworzy grupę trybu failover i rejestruje go na serwerach głównych i dodatkowych|
| [Usuń AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/remove-azurermsqldatabasefailovergroup) | Usuwa hello trybu failover grupy z serwera hello i wszystkie pomocnicze bazy danych uwzględnione hello grupy |
| [Get-AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/get-azurermsqldatabasefailovergroup) | Pobiera konfigurację grupy hello trybu failover |
| [Zestaw AzureRmSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/set-azurermsqldatabasefailovergroup) |   Modyfikuje konfigurację hello hello trybu failover grupy |
| [Przełącznika AzureRMSqlDatabaseFailoverGroup](/powershell/module/azurerm.sql/switch-azurermsqldatabasefailovergroup) | Wyzwalacze pracy w trybie failover serwer pomocniczy toohello hello trybu failover grupy |
|  | |

> [!IMPORTANT]
> Przykładowe skrypty dla [Konfigurowanie i pracy awaryjnej pojedynczej bazy danych przy użyciu aktywna replikacja geograficzna](scripts/sql-database-setup-geodr-and-failover-database-powershell.md), [Konfigurowanie i pracy awaryjnej puli bazy danych przy użyciu aktywna replikacja geograficzna](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md), i [Konfiguruj i pracy awaryjnej grupę trybu failover dla pojedynczej bazy danych (wersja zapoznawcza)] (skrypty/sql-database-setup-geodr-failover-database-failover-group-powershell.md.
>

## <a name="manage-sql-database-failover-using-hello-rest-api"></a>Zarządzanie za pomocą interfejsu API REST hello bazy danych SQL w tryb failover
| Interfejs API | Opis |
| --- | --- |
| [Tworzenie lub aktualizacja bazy danych (createMode = przywracanie)](/rest/api/sql/Databases/CreateOrUpdate) |Tworzy, aktualizuje lub przywraca podstawowej lub pomocniczej bazy danych. |
| [GET, Utwórz lub zaktualizuj stan bazy danych](/rest/api/sql/Databases/CreateOrUpdate) |Zwraca stan hello podczas operacji tworzenia. |
| [Ustaw dodatkowej bazy danych jako podstawowy (planowany tryb Failover)](https://docs.microsoft.com/rest/api/sql/replicationlinkss#ReplicationLinks_Failover) |Ustawia repliki bazy danych jest kluczem podstawowym przez awarii z hello bieżącej podstawowej repliki w bazie danych. |
| [Ustaw dodatkowej bazy danych jako podstawowy (nieplanowanego trybu Failover)](https://docs.microsoft.com/rest/api/sql/replicationlinks#ReplicationLinks_FailoverAllowDataLoss) |Ustawia repliki bazy danych jest kluczem podstawowym przez awarii z hello bieżącej podstawowej repliki w bazie danych. Ta operacja może spowodować utratę danych. |
| [Pobierz łącza replikacji](/rest/api/sql/replicationlinks/get) |Pobiera łącze replikacji określonych określonej bazy danych SQL w partnerstwie — replikacja geograficzna. Pobiera on hello informacji widocznych w widoku wykazu sys.geo_replication_links hello. |
| [Łącza replikacji — lista przez bazę danych](/rest/api/sql/replicationlinks/listbydatabase) | Pobiera wszystkie linki replikacji określonej bazy danych SQL w partnerstwie — replikacja geograficzna. Pobiera on hello informacji widocznych w widoku wykazu sys.geo_replication_links hello. |
| [Usuń łącza replikacji](/rest/api/sql/databases/delete) | Usuwa łącze replikacji bazy danych. Nie można wykonać w trybie failover. |
| [Tworzenie lub aktualizacja trybu Failover grupy] / rest/api/sql/failovergroups/createorupdate) | Tworzy lub aktualizuje grupę trybu failover |
| [Usuń grupę trybu Failover](/rest/api/sql/failovergroups/delete) | Usuwa grupę trybu failover hello z powitania serwera |
| [Tryb failover (zaplanowana)](/rest/api/sql/failovergroups/failover) | Awaryjnie z bieżącego serwera podstawowego serwera toothis hello. |
| [Zezwalaj na wymuszenie trybu Failover utrata danych](/rest/api/sql/failovergroups/forcefailoverallowdataloss) |ails za pośrednictwem z bieżącego serwera podstawowego serwera toothis hello. Ta operacja może spowodować utratę danych. |
| [Grupy pracy awaryjnej Get](/rest/api/sql/failovergroups/get) | Pobiera grupy pracy awaryjnej. |
| [Wyświetlanie listy grup trybu Failover przez serwer](/rest/api/sql/failovergroups/listbyserver) | Wyświetla listę grup pracy awaryjnej hello na serwerze. |
| [Aktualizacja trybu Failover grupy](/rest/api/sql/failovergroups/update) | Aktualizuje grupy pracy awaryjnej. |
|  | |

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać przykładowe skrypty Zobacz:
   - [Konfigurowanie i pracy awaryjnej pojedynczej bazy danych przy użyciu aktywna replikacja geograficzna](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
   - [Konfigurowanie i pracy awaryjnej puli bazy danych przy użyciu aktywna replikacja geograficzna](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)
   - [Konfigurowanie i trybu failover, a praca awaryjna grupy dla pojedynczej bazy danych (wersja zapoznawcza)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md)
* Omówienie ciągłości działalności biznesowej i scenariuszy, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md)
* toolearn o bazy danych SQL Azure automatycznego tworzenia kopii zapasowych, zobacz [bazy danych SQL automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md).
* toolearn o za pomocą kopie zapasowe automatycznego odzyskiwania, zobacz [przywrócić bazę danych z kopii zapasowych hello inicjowane przez usługę](sql-database-recovery-using-backups.md).
* toolearn o wymaganiach dotyczących uwierzytelniania nowym serwerem podstawowym i bazy danych, zobacz [zabezpieczeń bazy danych SQL po awarii](sql-database-geo-replication-security-config.md).

