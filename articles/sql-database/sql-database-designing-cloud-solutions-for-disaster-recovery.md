---
title: "Projektowanie usługi wysokiej dostępności przy użyciu usługi Azure SQL Database | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 40fe0ae04eb94322356ed19773512e3bc383639c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="designing-highly-available-services-using-azure-sql-database"></a>Projektowanie usługi wysokiej dostępności przy użyciu bazy danych SQL Azure

Podczas tworzenia i wdrażania usług wysokiej dostępności w bazie danych SQL Azure, użyj [trybu failover grupy i aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) do zapewnienia odporności na awarie regionalnych i poważnej awarii i Włącz szybkie odzyskiwanie pomocniczej bazy danych. Ten artykuł skupia się na typowe wzorce aplikacji i omówiono zalety i możliwości poszczególnych opcji, w zależności od wymagań wdrażania aplikacji, Umowa dotycząca poziomu usług przeznaczonych, opóźnienia ruchu i koszty. Informacje aktywna replikacja geograficzna z pule elastyczne, zobacz [strategii odzyskiwania danych w puli elastycznej](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).

## <a name="design-pattern-1-active-passive-deployment-for-cloud-disaster-recovery-with-a-co-located-database"></a>Wzorzec projektowy 1: aktywny / pasywny wdrożenia do chmury odzyskiwania po awarii z tej samej lokalizacji bazy danych
Ta opcja jest najbardziej odpowiednie dla aplikacji o następującej charakterystyce:

* Wystąpienia aktywne w pojedynczym regionie Azure
* Silne zależność od odczytu i zapisu (RW) dostęp do danych
* Łączność między region aplikacji sieci web i bazy danych nie jest akceptowany z powodu opóźnienia i ruchu koszt    

W takim przypadku topologii wdrożenia aplikacji jest zoptymalizowany do obsługi regionalnej awarii, gdy wszystkie składniki aplikacji ma wpływ i do trybu failover jako jednostka. W celu zapewnienia nadmiarowości geograficznej logiki aplikacji i bazy danych są replikowane do innego regionu, ale nie są używane dla obciążenia aplikacji w normalnych warunkach. Aplikacja w regionie pomocniczym powinien skonfigurowana do używania ciągu połączenia SQL do pomocniczej bazy danych. Menedżer ruchu jest skonfigurowany do użycia [metody routingu dla trybu failover](../traffic-manager/traffic-manager-configure-failover-routing-method.md).  

> [!NOTE]
> [Menedżer ruchu Azure](../traffic-manager/traffic-manager-overview.md) jest używany w tym artykule wyłącznie dla celów ilustracyjnych. Można użyć dowolnego równoważenia obciążenia rozwiązania, które obsługuje metody routingu dla trybu failover.    
>

Na poniższym diagramie przedstawiono tę konfigurację przed awarią.

![Konfiguracja — replikacja geograficzna bazy danych SQL. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-1.png)

Po awarii w regionie podstawowym usługi SQL Database wykrywa, że podstawowa baza danych nie jest dostępny i wyzwolić tryb failover w pomocniczej bazie danych na podstawie parametrów zasady automatycznej pracy awaryjnej. W zależności od Twojego umowy SLA dla aplikacji można zdecydować skonfigurować okres karencji między wykrywania awarii i pracy awaryjnej, sama. Konfigurowanie okresu prolongaty zmniejsza ryzyko utraty danych do przypadków, w którym jest poważnej awarii i dostępności w regionie nie można szybko przywrócić. Jeśli punkt końcowy trybu failover jest inicjowane przez Menedżera ruchu przed grupy pracy awaryjnej wyzwala trybu failover bazy danych, aplikacji sieci web nie będzie mógł ponownie połączyć się z bazą danych. Próba aplikacji automatycznie ponownie połączenie kończy się powodzeniem, natychmiast po zakończeniu trybu failover bazy danych. 

> [!NOTE]
> Aby osiągnąć całkowicie koordynowanym pracy awaryjnej aplikacji i baz danych, należy opracować metodę monitorowania i użyć ręcznego przełączania trybu failover punktów końcowych aplikacji sieci web i baz danych.
>

Po zakończeniu pracy awaryjnej zarówno punkty końcowe aplikacji, jak i bazy danych, aplikacja zostanie rozpoczęte przetwarzanie żądania użytkownika w regionie B i pozostanie wspólnie z bazą danych, ponieważ podstawowej bazy danych jest teraz w regionie B. W tym scenariuszu przedstawiono na poniższym diagramie. W wszystkie diagramy aktywnych połączeń wskazuje linia ciągła, linie przerywana wskazują wstrzymaną połączeń i znaki stop wskazać wyzwalaczy akcji.

![Replikacja geograficzna: Tryb Failover dodatkowej bazy danych. Kopia zapasowa danych aplikacji.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-2.png)

Jeśli wystąpi awaria w regionie pomocniczym, łącze replikacji między serwerem podstawowym i pomocniczym bazy danych jest wstrzymana, ale przejście w tryb failover nie jest wyzwalany, ponieważ nie ma wpływu na podstawowej bazy danych. Dostępność aplikacji nie ulega zmianie w takim przypadku, ale aplikacja działa narażonych i w związku z tym bardziej narażony w przypadku obu regionów awarii w przedziale czasu.

> [!NOTE]
> Do odzyskiwania po awarii zalecamy konfiguracji z wdrożeniem aplikacji jest ograniczona do dwóch regionach. Jest to spowodowane większość Azure lokalizacji geograficznych mają tylko dwóch regionach. Ta konfiguracja nie będzie chronić aplikacji z jednoczesnych poważnej awarii obu regionów.  W przypadku mało prawdopodobnego takiej awarii, można odzyskać bazy danych za pomocą trzeci region [operacji przywracania geograficznie](sql-database-disaster-recovery.md#recover-using-geo-restore).
>

Po awarii jest niewielkie, dodatkowej bazy danych zostanie automatycznie ponownie wykonywać synchronizację z serwera podstawowego. Podczas synchronizacji wydajności serwera podstawowego może dotyczyć nieco w zależności od ilości danych, które muszą być zsynchronizowane. Na poniższym diagramie przedstawiono awaria w regionie pomocniczym.

![Dodatkowej bazy danych są synchronizowane z podstawowym. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern1-3.png)

Klucz **zalety** tego wzorca projektu są:

* Ta sama aplikacja sieci web jest wdrażana na obu regionów, bez żadnej konfiguracji określonego regionu i nie dodatkowe logiki reagowanie na przejście w tryb failover. 
* Wydajność aplikacji nie ma wpływu na pracy awaryjnej jako aplikacji sieci web i bazy danych są zawsze wspólnie.

Głównym **zależnościami** jest nadmiarowy aplikację w regionie pomocniczym jest używana tylko do odzyskiwania po awarii.

## <a name="design-pattern-2-active-active-deployment-for-application-load-balancing"></a>Wzorzec projektowy 2: Wdrażanie aktywny aktywny w programie Równoważenie obciążenia aplikacji
Ta opcja odzyskiwania po awarii chmury jest najbardziej odpowiednie dla aplikacji o następującej charakterystyce:

* Wysoki współczynnik odczytów bazy danych do zapisu
* Baza danych opóźnienie odczytu jest dla użytkownika końcowego ważniejsze niż opóźnienie zapisu 
* Logika tylko do odczytu mogą być oddzielone od logiki odczytu i zapisu przy użyciu innego połączenia ciągu
* Logika tylko do odczytu nie zależy od danych pełni synchronizowana z najnowszymi aktualizacjami  

Jeśli aplikacje te właściwości, równoważenie obciążenia połączeń użytkowników końcowych w wielu wystąpień aplikacji w różnych regionach znacznie może zwiększyć ogólną środowisko użytkownika końcowego. Dwa regionów należy wybrać jako para odzyskiwania po awarii i trybu failover powinny znajdować się w grupie baz danych w tych obszarach. Aby zaimplementować równoważenia obciążenia, każdego regionu ma active wystąpienie aplikacji logiki (RW) odczytu i zapisu, połączony z punktem końcowym odczytu i zapisu odbiornika grupy pracy awaryjnej. Zostanie gwarantuje, że trybu failover zostanie automatycznie zainicjowany Jeśli podstawowa baza danych jest wpływ awaria. Tylko do odczytu logiki (RO) w aplikacji sieci web należy łączyć bezpośrednio z bazą danych w tym regionie. Usługi Traffic manager można skonfigurować do używania [wydajności routingu](../traffic-manager/traffic-manager-configure-performance-routing-method.md) z [punkt końcowy monitorowania](../traffic-manager/traffic-manager-monitoring.md) włączony dla każdego wystąpienia aplikacji.

Jak wzorzec #1 należy rozważyć wdrożenie podobne monitorowania aplikacji. Jednak w przeciwieństwie do wzorca #1 monitorowania aplikacji nie będzie odpowiedzialna za wyzwolenie pracy awaryjnej punktu końcowego.

> [!NOTE]
> Ten wzorzec korzysta z więcej niż jednej pomocniczej bazy danych, pomocniczej w regionie B będzie używany na potrzeby trybu failover i powinna być częścią grupy pracy awaryjnej.
>

Menedżer ruchu należy skonfigurować dla wydajności routingu do kierowania połączeń użytkowników do wystąpienia aplikacji najbliżej użytkownika lokalizacji geograficznej. Na poniższym diagramie przedstawiono tę konfigurację przed awarią.

![Nie przestoju: wydajności routingu do najbliższej aplikacji. Replikacja geograficzna.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-1.png)

Wykrycie awarii bazy danych w regionie, A grupy pracy awaryjnej zainicjuje automatycznie pracy awaryjnej z podstawowej bazy danych w regionie A na serwerze pomocniczym w regionie B. On również automatycznie zaktualizuje punktu końcowego odbiornika odczytu i zapisu do regionu B tak połączenia odczytu i zapisu w aplikacji sieci web nie jest ograniczona. Menedżer ruchu powoduje wyłączenie punktu końcowego w trybie offline z tabeli routingu, ale będzie kontynuowane, routingu ruchu przez użytkownika końcowego do pozostałych wystąpień online. Nie wpłynie parametry połączenia SQL tylko do odczytu, ponieważ zawsze punktu, w bazie danych w tym samym regionie. 

Na poniższym diagramie przedstawiono nowej konfiguracji po przejściu w tryb failover.

![Konfiguracja po pracy awaryjnej. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-2.png)

W przypadku wystąpienia awarii w jednej dodatkowej regionów usługi traffic manager spowoduje automatyczne usunięcie punktu końcowego w trybie offline w tym regionie z tabeli routingu. Kanał replikację do dodatkowej bazy danych w tym regionie zostanie zawieszona. Ponieważ pozostałe regiony dodatkowe ruchu danych w tym scenariuszu, wydajność aplikacji jest ograniczona w awarii. Po awarii jest niewielkie, dodatkowej bazy danych w regionie wpływ na będą natychmiast synchronizowane z serwerem podstawowym. Podczas synchronizacji wydajności serwera podstawowego może dotyczyć nieco w zależności od ilości danych, które muszą być zsynchronizowane. Na poniższym diagramie przedstawiono awaria w regionie B.

![Awaria w regionie pomocniczym. Odzyskiwanie awaryjne chmury — replikacja geograficzna.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern2-3.png)

Klucz **korzyści** projektu tego wzorca jest skalowanie obciążenia aplikacji na wiele pomocniczych baz danych, aby uzyskać optymalne wydajność. **Wady i zalety** tej opcji są:

* Odczyt i zapis połączenia między wystąpieniami aplikacji a bazy danych mają różnych opóźnienia i kosztów
* Wydajność aplikacji jest ograniczona w awarii

> [!NOTE]
> Podejście podobne umożliwia offload obciążeń specjalnych, takich jak raportowanie zadania, narzędzia do analizy biznesowej lub tworzenie kopii zapasowych. Zazwyczaj te obciążenia użycie zasobów znaczących bazy danych z tego powodu zaleca się wyznaczyć jednej pomocniczej bazy danych dla nich z poziomu wydajności do poziomu pasuje do oczekiwanego obciążenia.
>

## <a name="design-pattern-3-active-passive-deployment-for-data-preservation"></a>Wzorzec projektowy 3: Wdrażanie aktywny / pasywny konserwacji danych
Ta opcja jest najbardziej odpowiednie dla aplikacji o następującej charakterystyce:

* Utraty danych jest biznesowych wysokiego ryzyka. Tryb failover bazy danych można tylko w ostateczności przypadku poważnej awarii.
* Aplikacja obsługuje tylko do odczytu i zapisu i odczytu tryby operacji i może działać w trybie"tylko do odczytu" przez pewien czas.

W tym wzorcu aplikacji przełącza na tryb tylko do odczytu po rozpoczęciu połączenia odczytu i zapisu występują błędy przekroczenia limitu czasu. Aplikacja sieci Web jest wdrażana na obu regionów i obejmują połączenia z punktem końcowym odbiornika odczytu i zapisu oraz innego połączenia z punktem końcowym odbiornika tylko do odczytu. Traffic manager można skonfigurować do używania [routingu trybu failover](../traffic-manager/traffic-manager-configure-failover-routing-method.md) z [punkt końcowy monitorowania](../traffic-manager/traffic-manager-monitoring.md) włączone dla punktu końcowego aplikacji w każdym regionie.

Na poniższym diagramie przedstawiono tę konfigurację przed awarią.

![Aktywny / pasywny wdrożenia przed trybu failover. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-1.png)

Menedżer ruchu wykrycie awarii łączności do regionu A automatycznie przełączenie ruchu użytkowników do wystąpienia aplikacji w regionie B. Ten wzorzec ważne jest ustawienie okresu prolongaty utraty danych wystarczająco dużą wartość, np. 24 godziny. Zapewni on zapobiec utracie danych w przypadku awarii skuteczność została osłabiona w tym czasie. Po aktywowaniu aplikacji sieci Web w regionie B operacje odczytu i zapisu rozpocznie się niepowodzeniem. W tym momencie należy przełączyć do trybu tylko do odczytu. W tym trybie żądania zostanie automatycznie kierowane do dodatkowej bazy danych. W przypadku poważnej awarii awarii nie zostaną skorygowane w trakcie okresu prolongaty i grupy pracy awaryjnej jest wyzwalane w tryb failover. Po odbiornika odczytu i zapisu staną się dostępne i wywołania do niego zakończy się niepowodzeniem. Jest to zilustrowane w poniższym diagramie.

![Awaria: Aplikacja w trybie tylko do odczytu. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-2.png)

Jeśli w trakcie okresu prolongaty skuteczność została osłabiona awaria w regionie podstawowym, Menedżera ruchu wykrywa przywrócenia łączności w regionie podstawowym i zmienia ruchu użytkowników do wystąpienia aplikacji w regionie A. To wystąpienie aplikacji zostanie wznowione, a także działa w trybie odczytu i zapisu przy użyciu podstawowej bazy danych w regionie A.

W przypadku wystąpienia awarii w regionie B Menedżera ruchu wykrywa błąd punktu końcowego aplikacji w regionie B i odbiornika trybu failover grupy przełączników tylko do odczytu do regionu A. Ta awaria nie ma wpływu na środowisko pracy użytkownika końcowego, ale mają być widoczne podstawowej bazy danych podczas awarii. Jest to zilustrowane w poniższym diagramie.

![Awaria: Dodatkowej bazy danych. Odzyskiwanie awaryjne chmury.](./media/sql-database-designing-cloud-solutions-for-disaster-recovery/pattern3-3.png)

Po awarii jest niewielkie, dodatkowej bazy danych jest natychmiast synchronizowane z serwera podstawowego i przełączeniu odbiornika tylko do odczytu w pomocniczej bazie danych w regionie B. Podczas synchronizacji wydajności serwera podstawowego może dotyczyć nieco w zależności od ilości danych, które muszą być zsynchronizowane.

Ten wzorzec projektowy ma kilka **zalety**:

* Pozwala ona na uniknięcie utraty danych podczas tymczasowych przestojów.
* Czas przestoju tylko zależy szybkość Menedżera ruchu wykrywa awarii łączności, które można skonfigurować.

**Zależnościami** jest:

* Aplikacja musi mieć możliwość pracy w trybie tylko do odczytu.

> [!NOTE]
> W przypadku awarii usługi trwałe w regionie należy ręcznie uaktywnić trybu failover bazy danych i zaakceptować utraty danych. Aplikacja będzie działała w regionie pomocniczym z dostępem do odczytu i zapisu do bazy danych.
>

## <a name="business-continuity-planning-choose-an-application-design-for-cloud-disaster-recovery"></a>Planowanie ciągłości biznesowej: Wybierz projekt aplikacji do chmury odzyskiwania po awarii
Strategię odzyskiwania po awarii określonej chmury można łączyć lub rozszerzyć te wzorce projektowe, aby najlepiej odpowiadać potrzebom aplikacji.  Jak wspomniano wcześniej, strategii wybrane opiera się na umowie SLA chcesz zaoferować klientom i topologii wdrożenia aplikacji. W celu ułatwienia decyzji w poniższej tabeli porównano opcje, w zależności od utraty danych szacowany lub odzyskiwania (RPO) cel punktu i szacowany czas odzyskiwania (Wstaw).

| wzorzec | CEL PUNKTU ODZYSKIWANIA | WSTAW |
|:--- |:--- |:--- |
| Aktywny / pasywny wdrożenia dla odzyskiwania po awarii z dostępem do tej samej lokalizacji bazy danych |Dostęp do odczytu zapisu < 5 s |Czas wykrywania awarii + czas wygaśnięcia DNS |
| Aktywny aktywny wdrożenia aplikacji Równoważenie obciążenia sieciowego |Dostęp do odczytu zapisu < 5 s |Czas wykrywania awarii + czas wygaśnięcia DNS |
| Aktywny / pasywny wdrożenia do przechowywania danych |Dostęp tylko do odczytu < 5 s | Dostęp tylko do odczytu = 0 |
||Dostęp do odczytu zapisu = zero | Dostęp do odczytu zapisu = czas wykrycia błędu + okres prolongaty przy utracie danych |
|||

## <a name="next-steps"></a>Następne kroki
* Aby dowiedzieć się więcej na temat usługi Azure SQL bazy danych automatycznego tworzenia kopii zapasowych, zobacz [bazy danych SQL automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md)
* Omówienie ciągłości działalności biznesowej i scenariuszy, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md)
* Aby dowiedzieć się więcej o używaniu kopie zapasowe automatycznego odzyskiwania, zobacz [przywrócić bazę danych z kopii zapasowych inicjowane przez usługę](sql-database-recovery-using-backups.md)
* Informacje na temat opcji odzyskiwania szybsze, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md)  
* Aby dowiedzieć się, za pomocą automatycznych kopii zapasowej do archiwizacji, zobacz [kopiowanie bazy danych](sql-database-copy.md)
* Informacje aktywna replikacja geograficzna z pule elastyczne, zobacz [strategii odzyskiwania danych w puli elastycznej](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
