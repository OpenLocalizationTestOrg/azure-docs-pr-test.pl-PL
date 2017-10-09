---
title: "aaaDesign usługi wysokiej dostępności przy użyciu usługi Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat projektowania aplikacji dla usługi wysokiej dostępności przy użyciu bazy danych SQL Azure."
keywords: "w chmurze odzyskiwania po awarii, rozwiązania w zakresie odzyskiwania po awarii, kopia zapasowa danych aplikacji, replikacja geograficzna, planowanie ciągłości biznesowej"
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: e8a346ac-dd08-41e7-9685-46cebca04582
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 04/21/2017
ms.author: sashan
ms.openlocfilehash: 815f754ba7014cd8a1108a2d84c2a8f71d7030a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>Projektowanie usługi wysokiej dostępności przy użyciu bazy danych SQL Azure

Podczas tworzenia i wdrażania usług wysokiej dostępności w bazie danych SQL Azure, użyj [trybu failover grupy i aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) tooprovide odporności tooregional awarie i poważnej awarii i Włącz szybkie odzyskiwanie toohello pomocniczej bazy danych. Ten artykuł skupia się na typowe wzorce aplikacji i omówiono hello zalety i możliwości poszczególnych opcji, w zależności od wymagań wdrażania aplikacji hello, hello Umowa dotycząca poziomu usług przeznaczonych, opóźnienia ruchu i koszty. Informacje aktywna replikacja geograficzna z pule elastyczne, zobacz [strategii odzyskiwania danych w puli elastycznej](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>Wzorzec projektowy 1: aktywny / pasywny wdrożenia do chmury odzyskiwania po awarii z tej samej lokalizacji bazy danych
Ta opcja jest najbardziej odpowiednie dla aplikacji z hello następujące cechy:

* Wystąpienia aktywne w pojedynczym regionie Azure
* Silne zależność od toodata dostępu (RW) do odczytu / zapisu
* Łączność między region hello bazy danych i aplikacji sieci web hello nie jest akceptowane powodu kosztów toolatency i ruchu    

W takim przypadku topologii wdrożenia aplikacji hello jest zoptymalizowany do obsługi regionalnej awarii, gdy wpływ na wszystkie składniki aplikacji i toofailover jako jednostka. W celu zapewnienia nadmiarowości geograficznej logiki aplikacji hello i hello bazy danych są replikowane tooanother region, ale nie są używane dla obciążenia aplikacji hello w normalnych warunkach hello. Aplikacja Hello w regionie pomocniczym hello powinien być skonfigurowany toouse połączenia ciąg toohello pomocniczej bazy danych SQL. Menedżer ruchu skonfigurowano toouse [metody routingu dla trybu failover](../traffic-manager/traffic-manager-configure-failover-routing-method.md).  

> [!NOTE]
> [Menedżer ruchu Azure](../traffic-manager/traffic-manager-overview.md) jest używany w tym artykule wyłącznie dla celów ilustracyjnych. Można użyć dowolnego równoważenia obciążenia rozwiązania, które obsługuje metody routingu dla trybu failover.    
>

powitania po diagramie przedstawiono tę konfigurację przed awarią.

![Konfiguracja — replikacja geograficzna bazy danych SQL. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

Po awarii w regionie podstawowym hello usługi baza danych SQL hello wykrywa głównej bazy danych hello nie jest dostępny i wyzwolić tryb failover toohello pomocniczej bazy danych na podstawie parametrów hello hello zasad automatycznej pracy awaryjnej. W zależności od Twojego umowy SLA dla aplikacji można określić tooconfigure okres prolongaty między hello wykrywania awarii hello i pracy awaryjnej hello, sama. Konfigurowanie okresu prolongaty zmniejsza ryzyko hello przypadków gdzie jest poważnej awarii hello i dostępności w regionie hello nie można szybko przywrócić toohello utraty danych. Jeśli hello punktu końcowego w tryb failover jest inicjowane przez Menedżera ruchu hello przed hello trybu failover grupy wyzwalaczy hello trybu failover hello bazy danych, aplikacji sieci web hello nie jest możliwe tooreconnect toohello w bazie danych. aplikacji Hello tooreconnect próba powiedzie się automatycznie, zaraz po zakończeniu hello trybu failover z bazy danych. 

> [!NOTE]
> tooachieve całkowicie koordynowany pracy awaryjnej aplikacji hello i hello baz danych, należy opracować metodę monitorowania i użyć ręcznego przełączania trybu failover hello punktów końcowych z aplikacji sieci web i hello baz danych.
>

Po ukończeniu pracy awaryjnej hello aplikacji hello punktów końcowych i hello bazy danych aplikacji hello ponownie rozpocznie przetwarzanie żądania użytkownika hello w regionie hello B i pozostanie wspólnie z hello bazy danych, ponieważ hello podstawowa baza danych jest teraz w region B. W tym scenariuszu przedstawiono na powitania po diagramu. W wszystkie diagramy aktywnych połączeń wskazuje linia ciągła, linie przerywana wskazują wstrzymaną połączeń i znaki stop wskazać wyzwalaczy akcji.

![Replikacja geograficzna: Baza danych toosecondary trybu Failover. Kopia zapasowa danych aplikacji.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

W przypadku wystąpienia awarii w regionie pomocniczym hello, hello łącze replikacji między hello głównej i pomocniczej bazy danych hello jest wstrzymana, ale hello trybu failover nie jest uruchamiane, ponieważ nie ma wpływu na powitania podstawowej bazy danych. dostępność aplikacji Hello nie ulega zmianie w takim przypadku, ale aplikacji hello działa narażonych i w związku z tym bardziej narażony w przypadku obu regionów awarii w przedziale czasu.

> [!NOTE]
> Do odzyskiwania po awarii zalecamy hello konfiguracji z regionami tootwo ograniczone wdrożenia aplikacji. Jest to spowodowane większości hello Azure lokalizacji geograficznych mieć tylko dwóch regionach. Ta konfiguracja nie będzie chronić aplikacji z jednoczesnych poważnej awarii obu regionów.  W przypadku mało prawdopodobnego takiej awarii, można odzyskać bazy danych za pomocą trzeci region [operacji przywracania geograficznie](sql-database-disaster-recovery.md#recover-using-geo-restore).
>

Po awarii hello skuteczność została osłabiona hello dodatkowej bazy danych zostanie automatycznie ponownie wykonywać synchronizację z hello podstawowego. Podczas synchronizacji wydajności hello głównej może dotyczyć nieco w zależności od hello ilości danych wymaga toobe zsynchronizowane. Witaj poniższym diagramie przedstawiono awaria w regionie pomocniczym hello.

![Dodatkowej bazy danych są synchronizowane z podstawowym. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

klucz Hello **zalety** tego wzorca projektu są:

* Witaj tej samej aplikacji sieci web jest regionów wdrożonej tooboth bez żadnej konfiguracji określonego regionu i trybu failover toohello tooreact dodatkową logikę. 
* wydajność aplikacji Hello nie ma wpływu na pracy awaryjnej jako hello aplikacji sieci web i bazy danych hello są zawsze wspólnie.

Witaj głównego **zależnościami** jest to, że nadmiarowe aplikacji hello wystąpienie w regionie pomocniczym hello jest używany tylko do odzyskiwania po awarii.

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>Wzorzec projektowy 2: Wdrażanie aktywny aktywny w programie Równoważenie obciążenia aplikacji
Tej opcji odzyskiwania po awarii chmury jest najbardziej odpowiednie dla aplikacji z hello następujące cechy:

* Wysoki współczynnik bazy danych odczytuje toowrites
* Baza danych opóźnienie odczytu jest dla użytkownika końcowego hello ważniejsze niż opóźnienie zapisu na powitania 
* Logika tylko do odczytu mogą być oddzielone od logiki odczytu i zapisu przy użyciu innego połączenia ciągu
* Logika tylko do odczytu nie zależy od danych pełni synchronizowana z najnowszymi aktualizacjami hello  

Jeśli aplikacje mają te właściwości, równoważenie obciążenia hello połączeń użytkowników końcowych w wielu wystąpień aplikacji w różnych regionach znacząco poprawić hello środowisko pracy użytkownika końcowego. Dwóch regionach hello należy wybrać jako hello pary odzyskiwania po awarii i hello trybu failover grupa powinna zawierać hello baz danych w tych obszarach. tooimplement równoważenia obciążenia, każdy region powinien mieć aktywne wystąpienia aplikacji hello z hello odczytu i zapisu (RW) logiki połączone toohello odbiornika odczytu i zapisu punktem końcowym hello trybu failover grupy. Będzie ona zagwarantować, że czy tryb failover hello zostanie automatycznie rozpoczęte Jeśli podstawowa baza danych: hello jest wpływ awaria. Witaj tylko do odczytu logiki (RO) w aplikacji sieci web hello należy łączyć bezpośrednio toohello bazy danych, w tym regionie. Usługi Traffic manager można skonfigurować toouse [wydajności routingu](../traffic-manager/traffic-manager-configure-performance-routing-method.md) z [punkt końcowy monitorowania](../traffic-manager/traffic-manager-monitoring.md) włączony dla każdego wystąpienia aplikacji.

Jak wzorzec #1 należy rozważyć wdrożenie podobne monitorowania aplikacji. Ale w przeciwieństwie do wzorca #1 hello monitorowania aplikacji nie będzie odpowiedzialna za wyzwolenie pracy awaryjnej punktu końcowego hello.

> [!NOTE]
> Ten wzorzec korzysta z więcej niż jednej pomocniczej bazy danych, tylko hello dodatkowej w regionie B będzie używany na potrzeby trybu failover i powinna być częścią hello trybu failover grupy.
>

Menedżer ruchu należy skonfigurować dla lokalizacji geograficznej wydajności routingu toodirect hello użytkownika połączenia toohello wystąpienia najbliższego toohello użytkownika aplikacji. powitania po diagram przedstawia tej konfiguracji przed awarią.

![Nie przestoju: wydajności routingu toonearest aplikacji. Replikacja geograficzna.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

Wykrycie awarii bazy danych w regionie hello A hello trybu failover grupy będą automatycznie Inicjuj tryb failover hello głównej bazy danych w dodatkowej toohello region, A w regionie B. Zostanie również automatycznie zaktualizować hello odbiornika odczytu i zapisu punktu końcowego tooregion B, Odczyt i zapis połączenia w aplikacji sieci web hello nie wpłynie na. Menedżera ruchu Hello powoduje wyłączenie punktu końcowego w trybie offline hello z tabeli routingu hello, ale będzie nadal routingu hello użytkownika końcowego ruchu toohello pozostałych online wystąpień. Witaj parametry połączenia SQL tylko do odczytu nie jest ograniczona zgodnie z ich zawsze punktu toohello bazy danych w hello tego samego regionu. 

powitania po diagram przedstawia hello nowej konfiguracji po hello w tryb failover.

![Konfiguracja po pracy awaryjnej. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

W przypadku wystąpienia awarii w dodatkowej regionów hello hello Menedżera ruchu spowoduje automatyczne usunięcie punktu końcowego w trybie offline hello w tym regionie z hello tabeli routingu. zostanie zawieszony Hello replikacji kanału toohello dodatkowej bazy danych w tym regionie. Ponieważ regiony pozostałych hello dodatkowe ruchu danych w tym scenariuszu, wydajność aplikacji hello jest ograniczona w hello awarii. Po awarii hello skuteczność została osłabiona hello dodatkowej bazy danych w regionie wpływ na powitania zostaną natychmiast zsynchronizowane z hello podstawowego. Podczas hello wydajność synchronizacji hello głównej może dotyczyć nieco w zależności od hello ilości danych wymaga toobe zsynchronizowane. powitania po diagram ilustruje awaria w regionie B.

![Awaria w regionie pomocniczym. Odzyskiwanie awaryjne chmury — replikacja geograficzna.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

klucz Hello **korzyści** projektu tego wzorca jest skalowanie obciążenia aplikacji hello między wiele replik pomocniczych tooachieve hello optymalne wydajności. Witaj **wady i zalety** tej opcji są:

* Odczyt i zapis połączeń między wystąpieniami aplikacji hello i bazy danych ma różnych opóźnienia i kosztów
* Wydajność aplikacji jest ograniczona w hello awarii

> [!NOTE]
> Podejście podobne może służyć toooffload specjalizowany obciążeń, takich jak raportowanie zadania, narzędzia do analizy biznesowej lub tworzenie kopii zapasowych. Zazwyczaj te obciążenia użycie zasobów znaczących bazy danych w związku z tym zaleca się, że wskazanie jednego z hello pomocniczej bazy danych dla nich z hello wydajności poziomu toohello dopasowane przewidywane obciążenia.
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>Wzorzec projektowy 3: Wdrażanie aktywny / pasywny konserwacji danych
Ta opcja jest najbardziej odpowiednie dla aplikacji z hello następujące cechy:

* Utraty danych jest biznesowych wysokiego ryzyka. Hello trybu failover z bazy danych można tylko w ostateczności przypadku poważnej awarii hello.
* Aplikacja Hello obsługuje tylko do odczytu i zapisu i odczytu tryby operacji i może działać w trybie"tylko do odczytu" przez pewien czas.

W tym wzorcu aplikacji hello Przełącza tryb tylko do tooread po rozpoczęciu połączenia odczytu i zapisu hello występują błędy przekroczenia limitu czasu. Witaj aplikacji sieci Web jest wdrożone tooboth regionów i Dodaj punktu końcowego połączenia toohello odbiornika odczytu i zapisu oraz innego połączenia toohello odbiornika tylko do odczytu z punktu końcowego. Menedżer ruchu Hello powinny zostać skonfigurowane toouse [routingu trybu failover](../traffic-manager/traffic-manager-configure-failover-routing-method.md) z [punkt końcowy monitorowania](../traffic-manager/traffic-manager-monitoring.md) włączone dla punktu końcowego aplikacji hello w każdym regionie.

powitania po diagram przedstawia tej konfiguracji przed awarią.

![Aktywny / pasywny wdrożenia przed trybu failover. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

Menedżer ruchu hello wykrycie tooregion awarii łączności A automatycznie zmienia wystąpienia aplikacji toohello ruchu użytkowników w regionie B. Z tego wzorca ważne jest, aby ustawić okres prolongaty hello z utraty tooa wystarczająco wysoka wartość danych, np. 24 godziny. Zapewni on zapobiec utracie danych w przypadku awarii hello jest skorygowane w tym czasie. Po aktywowaniu aplikacji sieci Web w regionie hello B hello operacje odczytu i zapisu hello rozpocznie się niepowodzeniem. W tym momencie należy go przełącznika toohello trybie tylko do odczytu. W tym hello tryb żądania będą automatycznie routingiem toohello dodatkowej bazy danych. W przypadku hello hello poważnej awarii awarii nie zostaną skorygowane w okresie prolongaty hello i grupy pracy awaryjnej hello wyzwoli hello trybu failover. Po tym hello odbiornika odczytu i zapisu będą dostępne i tooit wywołania hello zatrzyma się niepowodzeniem. Jest to zilustrowane powitania po diagramu.

![Awaria: Aplikacja w trybie tylko do odczytu. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

Jeśli hello awaria w regionie podstawowym hello jest skorygowane w okresie prolongaty hello, Menedżera ruchu wykrywa hello przywrócenia łączności w regionie podstawowym hello i zmienia wystąpienia aplikacji użytkownika ruchu toohello Wstecz w regionie A. To wystąpienie aplikacji zostanie wznowione, a także działa w trybie odczytu i zapisu przy użyciu hello podstawowej bazy danych w regionie A.

W przypadku wystąpienia awarii w regionie hello B hello Menedżera ruchu wykrywa niepowodzenie hello punkt końcowy aplikacji hello w regionie B i hello trybu failover grupy przełączników hello odbiornika tylko do odczytu tooregion A. Ta awaria nie ma wpływu na środowisko pracy użytkownika końcowego hello, ale mają być widoczne hello podstawowej bazy danych podczas awarii hello. Jest to zilustrowane powitania po diagramu.

![Awaria: Dodatkowej bazy danych. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

Po awarii hello skuteczność została osłabiona hello dodatkowej bazy danych jest natychmiast synchronizowane z hello podstawowego i odbiornika hello tylko do odczytu jest wyłączone toohello wstecz dodatkowej bazy danych w regionie B. Podczas synchronizacji wydajności hello głównej może dotyczyć nieco w zależności od hello ilości danych wymaga toobe zsynchronizowane.

Ten wzorzec projektowy ma kilka **zalety**:

* Pozwala ona na uniknięcie utraty danych podczas hello tymczasowych przestojów.
* Czas przestoju tylko zależy szybkość Menedżera ruchu wykrywa hello awarii łączności, które można skonfigurować.

Witaj **zależnościami** jest:

* Aplikacja musi być możliwe toooperate w trybie tylko do odczytu.

> [!NOTE]
> W przypadku awarii usługi trwałe w regionie hello należy ręcznie uaktywnić trybu failover bazy danych i zaakceptować hello utraty danych. Aplikacja Hello będzie działać w regionie pomocniczym hello z toohello dostępu odczytu i zapisu do bazy danych.
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>Planowanie ciągłości biznesowej: Wybierz projekt aplikacji do chmury odzyskiwania po awarii
Strategię odzyskiwania po awarii określonej chmury można łączyć lub rozszerzyć te wzorce projektowe toobest hello spełnianie wymagań aplikacji.  Jak wspomniano wcześniej, strategii hello, która zostanie wybrana jest oparta na powitania SLA mają toooffer tooyour klientów i topologii wdrożenia aplikacji hello. toohelp przewodnik decyzji, hello w poniższej tabeli porównano opcje hello na podstawie hello szacowany danych utracie lub odzyskiwania cel punktu (RPO) i odzyskiwania szacowany czas (Wstaw).

| wzorzec | CEL PUNKTU ODZYSKIWANIA | WSTAW |
|:--- |:--- |:--- |
| Aktywny / pasywny wdrożenia dla odzyskiwania po awarii z dostępem do tej samej lokalizacji bazy danych |Dostęp do odczytu zapisu < 5 s |Czas wykrywania awarii + czas wygaśnięcia DNS |
| Aktywny aktywny wdrożenia aplikacji Równoważenie obciążenia sieciowego |Dostęp do odczytu zapisu < 5 s |Czas wykrywania awarii + czas wygaśnięcia DNS |
| Aktywny / pasywny wdrożenia do przechowywania danych |Dostęp tylko do odczytu < 5 s | Dostęp tylko do odczytu = 0 |
||Dostęp do odczytu zapisu = zero | Dostęp do odczytu zapisu = czas wykrycia błędu + okres prolongaty przy utracie danych |
|||

## <a name="next-steps"></a>Następne kroki
* toolearn o bazy danych SQL Azure automatycznego tworzenia kopii zapasowych, zobacz [bazy danych SQL automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md)
* Omówienie ciągłości działalności biznesowej i scenariuszy, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md)
* toolearn o za pomocą kopie zapasowe automatycznego odzyskiwania, zobacz [przywrócić bazę danych z kopii zapasowych hello inicjowane przez usługę](sql-database-recovery-using-backups.md)
* toolearn o szybsze opcje odzyskiwania, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md)  
* toolearn o za pomocą automatycznych kopii zapasowej do archiwizacji, zobacz [kopiowanie bazy danych](sql-database-copy.md)
* Informacje aktywna replikacja geograficzna z pule elastyczne, zobacz [strategii odzyskiwania danych w puli elastycznej](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
