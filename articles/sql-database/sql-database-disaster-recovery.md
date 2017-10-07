---
title: aaaSQL bazy danych odzyskiwania po awarii | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorecover bazę danych z datacenter regionalnej awarii lub niepowodzenia hello aktywna replikacja geograficzna bazy danych SQL Azure i możliwości przywracania geo."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 4800960e-3f9d-40ce-9e55-fb7f2784c067
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: sashan
ms.openlocfilehash: bae08485863067748107ec4808e52d8e88e2de0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-database-or-failover-tooa-secondary"></a>Przywracanie bazy danych SQL Azure lub pracy awaryjnej tooa dodatkowej
Baza danych SQL Azure oferuje następujące możliwości odzyskiwania po awarii hello:

* [Aktywna replikacja geograficzna](sql-database-geo-replication-overview.md)
* [Geograficzne](sql-database-recovery-using-backups.md#point-in-time-restore)

Zobacz toolearn o scenariuszach ciągłości biznesowej i funkcje hello obsługujące te scenariusze [ciągłość prowadzenia działalności biznesowej](sql-database-business-continuity.md).

### <a name="prepare-for-hello-event-of-an-outage"></a>Przygotowanie do zdarzeń hello awarii
Do poprawnego działania obszaru danych tooanother odzyskiwania przy użyciu aktywna replikacja geograficzna lub geograficznie nadmiarowego kopii zapasowych należy tooprepare serwera w innym data center awarii toobecome hello nowym serwerem podstawowym powinien hello musi wystąpić, jak również mają dobrze zdefiniowanego kroki udokumentowanych i przetestowany tooensure smooth odzyskiwania. Te kroki przygotowania obejmują:

* Zidentyfikuj serwer logiczny hello w innym regionie toobecome hello nowym serwerem podstawowym. Z aktywna replikacja geograficzna będzie to co najmniej jedną i prawdopodobnie każdego z serwerów pomocniczych hello. Do przywrócenia geograficznie, zazwyczaj będzie serwera w hello [sparowanego region](../best-practices-availability-paired-regions.md) hello regionu, w którym znajduje się baza danych.
* Identyfikowanie i opcjonalnie zdefiniować, reguły zapory poziomu serwera hello potrzebne na dla użytkowników tooaccess hello nowe podstawowej bazy danych.
* Określ, jak ma tooredirect użytkowników toohello nowym serwerem podstawowym, takich jak zmiana parametry połączenia lub zmieniając wpisy DNS.
* Zidentyfikować i opcjonalnie utworzyć, hello logowania, które musi znajdować się w bazie danych master hello na powitania nowym serwerem podstawowym i upewnij się, że te logowania ma odpowiednie uprawnienia w bazie danych master hello, jeśli istnieje. Aby uzyskać więcej informacji, zobacz [zabezpieczeń bazy danych SQL po awarii](sql-database-geo-replication-security-config.md)
* Określ reguły alertów, które będą potrzebne toobe zaktualizowane toomap toohello nowe podstawowej bazy danych.
* Konfiguracja inspekcji hello dokumentu na powitania bieżącej podstawowej bazy danych
* Wykonaj [wyszczególniania odzyskiwania po awarii](sql-database-disaster-recovery-drills.md). toosimulate o awarii do przywrócenia geograficznie, można usunąć ani zmienić nazwy awarii łączności aplikacji toocause hello źródłowej bazy danych. toosimulate awarii dla aktywnej georeplikacji, można wyłączyć maszyny wirtualnej podłączone toohello bazy danych lub pracy awaryjnej hello bazy danych toocause łączności błędy aplikacji lub aplikacji sieci web hello.

## <a name="when-tooinitiate-recovery"></a>Podczas odzyskiwania tooinitiate
Operacja odzyskiwania Hello ma wpływ na powitania aplikacji. Konieczna jest zmiana parametrów połączenia SQL hello lub przekierowania przy użyciu serwera DNS, a może spowodować utratę danych trwałych. W związku z tym należy to zrobić tylko w przypadku awarii hello prawdopodobnie toolast dłużej niż celu czasu odzyskiwania aplikacji. Gdy hello aplikacji jest wdrożony tooproduction należy wykonać regularnego monitorowania kondycji aplikacji hello i użyć hello następujące dane, które jest uzasadnione tooassert punktów, które hello odzyskiwania:

1. Niepowodzenie trwałe połączenie z danych toohello warstwy aplikacji hello.
2. Hello portalu Azure zawiera alert o incydentu w regionie hello szerokie wpływu.
3. Serwer bazy danych SQL Azure Hello jest oznaczony jako ograniczone.

W zależności od Twojej aplikacji tolerancji toodowntime i możliwości biznesowe odpowiedzialności należy wziąć pod uwagę następujące opcje odzyskiwania hello.

Użyj hello [pobrać możliwych do odzyskania bazy danych](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) tooget hello najnowszy punkt przywracania z replikacją geograficzną.

## <a name="wait-for-service-recovery"></a>Poczekaj, aż usługi odzyskiwania
Hello Azure zespoły działają dokładnie dostępności usługi toorestore jak szybko jak to możliwe, ale w zależności od przyczyny głównej hello może potrwać kilka godzin, a dni.  Jeśli aplikacja może tolerować znaczących przestoju możesz po prostu poczekać hello toocomplete odzyskiwania. W takim przypadku jest wymagana żadna akcja ze strony użytkownika. Możesz wyświetlać bieżący stan usługi hello na naszych [pulpit nawigacyjny kondycji usługi Azure](https://azure.microsoft.com/status/). Po odzyskaniu hello regionu hello dostępność aplikacji zostaną przywrócone.

## <a name="fail-over-toogeo-replicated-secondary-database"></a>Tryb failover replikowane toogeo dodatkowej bazy danych
Jeśli przestój aplikacji może spowodować odpowiedzialności firm należy używać baz danych z replikacją geograficzną w aplikacji. To umożliwi dostępności przywracania tooquickly aplikacji hello w innym regionie, w razie awarii. Dowiedz się, jak za[skonfigurować — replikacja geograficzna](sql-database-geo-replication-portal.md).

dostępność toorestore hello database(s) możesz muszą tooinitiate hello pomocniczy replikacją geograficzną toohello trybu failover przy użyciu jednej z metod hello obsługiwane.

Użyj jednej z powitania po przewodnikach toofail za pośrednictwem tooa replikowane geograficznie pomocnicze bazy danych:

* [Tryb failover tooa replikowane geograficznie pomocnicze przy użyciu portalu Azure](sql-database-geo-replication-portal.md)
* [Tryb failover tooa replikowane geograficznie pomocnicze przy użyciu programu PowerShell](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [Tryb failover tooa replikowane geograficznie pomocnicze za pomocą T-SQL](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a>Odzyskać, używając funkcji przywracania geo
Jeśli przestój aplikacji nie powoduje odpowiedzialności firm można użyć [geograficzne](sql-database-recovery-using-backups.md) jako toorecover — metoda baz danych z aplikacji. Tworzy kopię bazy danych hello z jego najnowszej kopii zapasowej geograficznie nadmiarowy.

## <a name="configure-your-database-after-recovery"></a>Konfigurowanie bazy danych po odzyskaniu
Jeśli używasz trybu failover — replikacja geograficzna lub toorecover geograficznie przywracania po awarii, należy się upewnić że hello łączności toohello nowych baz danych jest skonfigurowany prawidłowo, dzięki czemu można wznowić funkcja normalne aplikacji hello. To jest lista kontrolna tooget zadania gotowy produkcyjnego odzyskanej bazy danych.

### <a name="update-connection-strings"></a>Aktualizowanie parametrów połączenia
Ponieważ odzyskanej bazy danych będą znajdować się w innym serwerze, należy tooupdate aplikacji połączenia ciąg toopoint toothat serwera.

Aby uzyskać więcej informacji na temat zmiany parametrów połączenia, zobacz hello języka programowania odpowiednie dla Twojej [biblioteki połączeń](sql-database-libraries.md).

### <a name="configure-firewall-rules"></a>Konfigurowanie reguł zapory
Należy toomake się, że reguły zapory hello skonfigurowane na serwerze i dopasowania bazy danych hello te, które zostały skonfigurowane na serwerze podstawowym hello i podstawowej bazy danych. Aby uzyskać więcej informacji, zobacz [porady: Konfigurowanie ustawień zapory (baza danych SQL Azure)](sql-database-configure-firewall-settings.md).

### <a name="configure-logins-and-database-users"></a>Konfigurowanie logowania i bazy danych użytkowników
Należy toomake się, że wszystkie logowania hello używanych przez aplikację na powitania serwera, który jest hostem odzyskanej bazy danych. Aby uzyskać więcej informacji, zobacz [konfiguracji zabezpieczeń — replikacja geograficzna](sql-database-geo-replication-security-config.md).

> [!NOTE]
> Skonfigurowanie i testowanie reguł zapory serwera i logowań (i ich uprawnienia) podczas wyszczególniania odzyskiwania po awarii. Te obiekty z poziomu serwera i ich konfiguracji może nie być dostępne podczas awarii hello.
> 
> 

### <a name="setup-telemetry-alerts"></a>Ustaw alerty telemetrii
Należy toomake się, że istniejące ustawienia reguły alertów są zaktualizowane toomap toohello odzyskanej bazy danych i hello inny serwer.

Aby uzyskać więcej informacji o regułach alertów bazy danych, zobacz [odbieranie powiadomień Alert](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) i [kondycja usługi Śledź](../monitoring-and-diagnostics/insights-service-health.md).

### <a name="enable-auditing"></a>Włączanie inspekcji
Jeśli inspekcja jest wymagana tooaccess bazy danych, należy tooenable inspekcji po hello odzyskiwanie bazy danych. Aby uzyskać więcej informacji, zobacz [inspekcji bazy danych](sql-database-auditing.md).

## <a name="next-steps"></a>Następne kroki
* toolearn o bazy danych SQL Azure automatycznego tworzenia kopii zapasowych, zobacz [bazy danych SQL automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md)
* toolearn o ciągłości projektowania i odzyskiwania różnych scenariuszy biznesowych, zobacz [ciągłości scenariuszy](sql-database-business-continuity.md)
* toolearn o za pomocą kopie zapasowe automatycznego odzyskiwania, zobacz [przywrócić bazę danych z kopii zapasowych hello inicjowane przez usługę](sql-database-recovery-using-backups.md)

