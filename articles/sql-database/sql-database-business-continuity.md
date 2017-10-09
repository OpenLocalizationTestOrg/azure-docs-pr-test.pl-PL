---
title: "aaaCloud ciągłość działania — odzyskiwanie bazy danych — baza danych SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, w jaki sposób usługa Azure SQL Database obsługuje ciągłość działalności biznesowej w chmurze i odzyskiwanie bazy danych oraz pomaga zapewnić działanie aplikacji o kluczowym znaczeniu w chmurze."
keywords: business continuity,cloud business continuity,database disaster recovery,database recovery
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 18e5d3f1-bfe5-4089-b6fd-76988ab29822
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/15/2017
ms.author: sashan
ms.openlocfilehash: c9a6ff86fbbc04ce839a4fca79594b573b71644c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-business-continuity-with-azure-sql-database"></a>Omówienie zagadnień dotyczących ciągłości działalności biznesowej zapewnianej przez usługę Azure SQL Database

Ten przegląd zawiera opis możliwości hello, które bazy danych SQL Azure zapewnia ciągłość prowadzenia działalności biznesowej i odzyskiwania po awarii. Więcej informacji na temat opcji, zalecenia i samouczki dotyczące odzyskiwania z destrukcyjne zdarzenia, które mogą spowodować utratę danych lub spowodować Twojej bazy danych i aplikacji toobecome niedostępny. Dowiedz się jakie toodo błąd użytkownika albo aplikacji wpływa na integralność danych, region platformy Azure ma awarii lub aplikacja wymaga konserwacji.

## <a name="sql-database-features-that-you-can-use-tooprovide-business-continuity"></a>Funkcje bazy danych SQL można tooprovide ciągłość działania

Usługa SQL Database udostępnia kilka funkcji zapewniających ciągłość działalności biznesowej, w tym zautomatyzowane kopie zapasowe oraz opcjonalną replikację bazy danych. Każda z tych funkcji ma różne charakterystyki dotyczące szacowanego czasu odzyskiwania (ERT, estimated recovery time) i potencjalnej utraty danych dotyczących ostatnich transakcji. Po zapoznaniu się z tymi opcjami można dokonać między nimi wyboru, a także — w większości przypadków — użyć ich razem w ramach różnych scenariuszy. Podczas opracowywania planu zapewnienia ciągłości działalności należy toounderstand hello maksymalny dopuszczalny czas oczekiwania aplikacji hello pełni odzyskuje po zdarzeniu destrukcyjne hello — jest to celu czasu odzyskiwania (RTO). Należy również toounderstand hello maksymalną ilość ostatnie aplikacji hello aktualizacji (interwał czasu) danych może tolerować utraty podczas odzyskiwania po zdarzeniu destrukcyjne hello — jest to cel punktu odzyskiwania (RPO).

powitania po porównuje tabeli hello Wstaw i cel punktu odzyskiwania dla hello trzech najbardziej typowych scenariuszy.

| Możliwości | Warstwa Podstawowa | Warstwa standardowa | Warstwa Premium |
| --- | --- | --- | --- |
| Przywracanie do punktu w czasie z kopii zapasowej |Dowolny punkt przywracania w ciągu ostatnich 7 dni |Dowolny punkt przywracania w ciągu ostatnich 35 dni |Dowolny punkt przywracania w ciągu ostatnich 35 dni |
| Geograficznie — Przywracanie z kopii zapasowych z replikacją geograficzną |ERT < 12 godz., RPO < 1 godz. |ERT < 12 godz., RPO < 1 godz. |ERT < 12 godz., RPO < 1 godz. |
| Przywracanie z magazynu usługi Azure Backup |ERT < 12 godz., RPO < 1 tydz. |ERT < 12 godz., RPO < 1 tydz. |ERT < 12 godz., RPO < 1 tydz. |
| Aktywna replikacja geograficzna |ERT < 30 s, RPO < 5 s |ERT < 30 s, RPO < 5 s |ERT < 30 s, RPO < 5 s |

### <a name="use-database-backups-toorecover-a-database"></a>Użyj bazy danych toorecover kopie zapasowe bazy danych

Baza danych SQL automatycznie wykonuje kombinacji pełnej bazy danych kopii zapasowych co tydzień, co godzinę kopii zapasowych różnicowej bazy danych i transakcji kopii zapasowych dziennika co pięć — dziesięć minut tooprotect firmy przed utratą danych. Te kopie zapasowe są przechowywane w magazynu geograficznie nadmiarowego 35 dni w przypadku baz danych w warstwach usług standardowa i Premium hello i 7 dni w przypadku baz danych w warstwach usług podstawowa hello. Aby uzyskać więcej informacji, zobacz [warstw usług](sql-database-service-tiers.md). Jeśli okres przechowywania hello warstwę usługi nie spełnia wymagań biznesowych, może zwiększyć okresu przechowywania hello [zmianę warstwy usługi hello](sql-database-service-tiers.md). Hello bazy danych pełne i różnicowe kopie zapasowe są również replikowanych tooa [centrum danych sparowanego](../best-practices-availability-paired-regions.md) ochrony przed awarii centrum danych. Aby uzyskać więcej informacji, zobacz [kopie zapasowe bazy danych automatyczne](sql-database-automated-backups.md).

Jeśli okres przechowywania wbudowanych hello jest niewystarczająca dla aplikacji, można go rozszerzyć, konfigurując zasady przechowywania długoterminowego bazy danych. Aby uzyskać więcej informacji, zobacz [przechowywania długoterminowego](sql-database-long-term-retention.md).

Możesz użyć tych automatyczne bazy danych toorecover kopie zapasowe bazy danych z różnych zdarzeń destrukcyjne, zarówno w centrum danych, a tooanother centrum danych. Za pomocą kopii zapasowej bazy danych automatyczne, hello szacowany czasu odzyskiwania zależy od wielu czynników, w tym łączną liczbę baz danych odzyskiwania w hello sam hello region na powitania sam czasie hello rozmiar bazy danych, rozmiaru dziennika transakcji hello i przepustowość sieci. czas odzyskiwania Hello jest zazwyczaj mniej niż 12 godzin. Podczas odzyskiwania tooanother obszaru danych, hello ryzyko utraty danych jest godzinę too1 ograniczone przez hello magazynu geograficznie nadmiarowego co godzinę bazy danych różnicowych kopii zapasowych.

> [!IMPORTANT]
> toorecover przy użyciu automatycznego tworzenia kopii zapasowych, musisz być członkiem roli współautora serwera SQL hello lub właściciela subskrypcji hello — zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md). Można odzyskać za pomocą hello portalu Azure, programu PowerShell lub hello interfejsu API REST. Nie można używać języka Transact-SQL.
>

Zautomatyzowanych kopii zapasowych jako mechanizmu odzyskiwania i zapewniania ciągłości działalności biznesowej należy używać, jeśli aplikacja:

* Nie jest traktowana jako aplikacja o kluczowym znaczeniu.
* Nie ma powiązania umowy SLA - przestoju 24 godziny lub już nie powoduje odpowiedzialności finansowych.
* Niski częstotliwości zmian danych (niski transakcji na godzinę) i utraty się tooan godzina zmiany jest utrata danych.
* Jej koszt ma znaczenie.

Szybsze odzyskiwania, należy użyć [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) (omówione dalej). Jeśli potrzebujesz toobe stanie toorecover dane z okresu sprzed 35 dni, użyj [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md). 

### <a name="use-active-geo-replication-and-auto-failover-groups-in-preview-tooreduce-recovery-time-and-limit-data-loss-associated-with-a-recovery"></a>Użyj active — replikacja geograficzna i pracy awaryjnej automatycznie grupy (w podglądzie) tooreduce odzyskiwania czasu i limit utraty danych odzyskiwania

Ponadto toousing kopie zapasowe bazy danych dla bazy danych odzyskiwania, w przypadku zakłóceń firm, można użyć [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) tooconfigure toohave bazy danych, zapasowe toofour czytelny pomocniczych baz danych w regionach hello z sieci Wybór. Te pomocniczej bazy danych są będą synchronizowane z podstawowej bazy danych hello przy użyciu mechanizmu replikacji asynchronicznej. Ta funkcja jest używane tooprotect przed firm przerwy w przypadku wystąpienia awarii centrum danych lub podczas uaktualniania aplikacji. Aktywna replikacja geograficzna może być również używane tooprovide lepszą wydajność zapytań dla użytkowników toogeographically rozproszone zapytania tylko do odczytu.

zautomatyzowane tooenable i przezroczysty tryb failover należy zorganizować replikacją geograficzną baz danych do grupy przy użyciu hello [grupy pracy awaryjnej automatycznie](sql-database-geo-replication-overview.md) funkcji bazy danych SQL (w — wersja zapoznawcza).

Jeśli podstawowa baza danych: hello przejdzie do trybu offline nieoczekiwanie lub konieczne tootake go w trybie offline dla działań konserwacji, można szybko podwyższyć poziom podstawowy hello dodatkowej toobecome (nazywanych również trybu failover) i skonfigurować aplikacje tooconnect toohello podwyższenia poziomu podstawowego. Jeśli aplikacja nawiązuje połączenie toohello baz danych przy użyciu odbiornika grupy hello trybu failover, nie potrzebujesz toochange konfiguracji ciągu połączenia SQL powitania po pracy awaryjnej. Planowane przejście w tryb failover nie spowoduje utraty żadnych danych. Z nieplanowanego trybu failover może być niektóre małe ilości utraconych danych transakcji bardzo ostatnie powodu charakter toohello asynchroniczną replikację. Przy użyciu grup pracy awaryjnej automatycznego (w — wersja zapoznawcza), można dostosować hello trybu failover zasad toominimize hello ryzyko utraty danych. Po przejściu w tryb failover można nowsze powrotu po awarii — zgodnie z planem tooa lub jeśli Centrum danych hello wraca do trybu online. We wszystkich przypadkach użytkownicy wystąpić niewielki Przestój i muszą tooreconnect.

> [!IMPORTANT]
> aktywna replikacja geograficzna toouse i pracy awaryjnej automatycznie grupy (w — wersja zapoznawcza), użytkownik musi być hello właściciela subskrypcji lub mieć uprawnienia administracyjne w programie SQL Server. Możesz skonfigurować i pracy awaryjnej przy użyciu hello portalu Azure, programu PowerShell lub hello interfejsu API REST, korzystając z uprawnień subskrypcji platformy Azure lub przy użyciu języka Transact-SQL z uprawnieniami serwera SQL.
> 

Użyj active grup — replikacja geograficzna i pracy awaryjnej automatycznego (w wersji zapoznawczej), jeśli aplikacja spełnia dowolną z tych kryteriów:

* Ma kluczowe znaczenie.
* Obejmuje ją umowa dotycząca poziomu usług (SLA), zgodnie z którą przestój nie może być dłuższy niż 24 godziny.
* Może spowodować przestój finansowych odpowiedzialności.
* Ma wysoki współczynnik zmian danych i utrata zmian z okresu jednej godziny jest niedopuszczalna.
* Hello dodatkowych kosztów aktywna replikacja geograficzna jest niższa niż hello potencjalnych odpowiedzialności finansowych i skojarzone utraty biznesowych.

>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-protecting-important-DBs-from-regional-disasters-is-easy/player]
>

## <a name="recover-a-database-after-a-user-or-application-error"></a>Odzyskiwanie bazy danych po błędzie użytkownika lub aplikacji
*Nikt nie jest doskonały! Użytkownik może przypadkowo usunąć pewne dane, nieodwracalnie usunąć ważną tabelę lub nawet usunąć całą bazę danych. Lub aplikacji mogą przypadkowo zastąpić danych złe dane powodu wada aplikacji tooan.

W tym scenariuszu opcje odzyskiwania są następujące.

### <a name="perform-a-point-in-time-restore"></a>Wykonanie przywracania do punktu w czasie
Można użyć hello automatycznego tworzenia kopii zapasowych toorecover kopię tooa Twojej bazy danych, znane dobry punkt w czasie, pod warunkiem, że przypada w ciągu okresu przechowywania hello bazy danych. Po przywróceniu bazy danych hello można zastąpić oryginalnej bazy danych hello hello przywrócić bazy danych lub skopiuj hello potrzebne dane z danych hello przywrócone do hello oryginalnej bazy danych. Baza danych hello używa aktywna replikacja geograficzna, zaleca się kopiowanie danych hello wymagane z kopii hello przywrócić do oryginalnej bazy danych hello. Jeśli zastąpić oryginalnej bazy danych hello hello przywrócić bazy danych, należy tooreconfigure go i ponownie zsynchronizować aktywna replikacja geograficzna (co może potrwać jakiś czas, w przypadku dużych bazy danych).

Aby uzyskać więcej informacji i szczegółowy opis kroków w celu przywrócenia bazy danych tooa punktu w czasie przy użyciu portalu Azure hello lub przy użyciu programu PowerShell, zobacz [w momencie przywracania](sql-database-recovery-using-backups.md#point-in-time-restore). Nie można przeprowadzić odzyskiwania za pomocą języka Transact-SQL.

### <a name="restore-a-deleted-database"></a>Przywracanie usuniętej bazy danych
Jeśli hello bazy danych zostanie usunięty, ale nie został usunięty serwer logiczny hello, można przywrócić punktu toohello hello usunięte bazy danych z jaką został usunięty. Spowoduje to przywrócenie toohello kopii zapasowej bazy danych tego samego serwera logicznego SQL z którego został usunięty. Można przywrócić za pomocą hello oryginalną nazwę lub podaj nową nazwę lub hello przywrócić bazy danych.

Aby uzyskać więcej informacji oraz szczegółowe informacje na temat Przywracanie usuniętej bazy danych przy użyciu hello portalu Azure lub przy użyciu programu PowerShell, zobacz [przywrócić usuniętą bazę](sql-database-recovery-using-backups.md#deleted-database-restore). Nie można przeprowadzić przywracania za pomocą języka Transact-SQL.

> [!IMPORTANT]
> Jeśli serwer logiczny hello zostanie usunięty, nie można odzyskać usuniętej bazy danych.
>
>

### <a name="restore-from-azure-backup-vault"></a>Przywracanie z magazynu usługi Azure Backup
Jeśli baza danych jest skonfigurowany w celu przechowywania długoterminowego wystąpiła utrata danych hello poza hello bieżącego okresu przechowywania automatycznych kopii zapasowych, można przywrócić z kopii zapasowej co tydzień w magazynie kopii zapasowych Azure tooa Nowa baza danych. W tym momencie można zastąpić oryginalnej bazy danych hello hello przywrócić bazy danych lub skopiuj hello potrzebne dane z bazy danych hello przywrócone do hello oryginalnej bazy danych. Tooretrieve starą wersję uaktualnienia bazy danych poprzednich tooa najważniejszych aplikacji, należy wykonać żądanie z audytorów lub prawnym, można utworzyć bazy danych przy użyciu pełnej kopii zapasowej zapisane w hello Azure magazynu kopii zapasowych.  Aby uzyskać więcej informacji, zobacz [Długoterminowe przechowywanie](sql-database-long-term-retention.md).

## <a name="recover-a-database-tooanother-region-from-an-azure-regional-data-center-outage"></a>Odzyskiwanie po awarii centrum danych Azure regionalnych region tooanother bazy danych
<!-- Explain this scenario -->

Sporadycznie centrum danych platformy Azure może mieć awarię. Taka awaria powoduje zakłócenia działania firmy, które mogą trwać tylko kilka minut, ale mogą też trwać wiele godzin.

* Jedną z opcji jest toowait dla z powrotem do trybu online bazy danych toocome po awarii centrum danych hello. Działa to w przypadku aplikacji, które można pozwolić sobie bazy toohave hello danych w trybie offline. Na przykład opracowywanego projektu lub bezpłatnej wersji próbnej nie trzeba toowork na stale. Centrum danych po awarii nie wiesz, jak długo może ostatniej awarii hello, więc ta opcja działa tylko, jeśli nie potrzebujesz bazy danych przez pewien czas.
* Innym rozwiązaniem jest niepowodzenie tooeither za pośrednictwem obszaru danych tooanother Jeśli używasz aktywna replikacja geograficzna lub hello odzyskać bazę danych za pomocą kopii zapasowej bazy danych z magazynu geograficznie nadmiarowego (geograficznie przywracania). Tryb failover trwa tylko kilka sekund podczas odzyskiwania bazy danych z kopii zapasowych zajmuje godzin.

Po wykonaniu akcji, jak długo trwa możesz toorecover i ile utraty danych, które ponosisz zależy od sposobu podjęcia decyzji toouse tych funkcjach ciągłości biznesowej w aplikacji. W rzeczywistości może wybrać toouse połączenie kopie zapasowe bazy danych i aktywna replikacja geograficzna w zależności od wymagań aplikacji. Dyskusję na temat zagadnień dotyczących projektowania aplikacji na potrzeby autonomicznych baz danych i pul elastycznych za pomocą tych funkcji zapewniania ciągłości działalności biznesowej zawierają tematy [Design an application for cloud disaster recovery](sql-database-designing-cloud-solutions-for-disaster-recovery.md) (Projektowanie aplikacji pod kątem odzyskiwania po awarii w chmurze) i [Elastic Pool disaster recovery strategies](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md) (Strategie odzyskiwania po awarii dotyczące pul elastycznych).

Witaj poniższe sekcje zawierają omówienie hello toorecover czynności przy użyciu kopii zapasowych bazy danych lub aktywna replikacja geograficzna. Aby uzyskać szczegółowe instrukcje w tym planowanie wymagań, post kroki odzyskiwania i informacji na temat sposobu toosimulate tooperform awarii odzyskiwania po awarii przejść do szczegółów, zobacz [odzyskanie bazy danych SQL awarii](sql-database-disaster-recovery.md).

### <a name="prepare-for-an-outage"></a>Przygotowanie do awarii
Niezależnie od funkcji ciągłości biznesowej hello, używanego należy:

* Identyfikowanie i przygotować serwer docelowy hello, w tym reguły zapory poziomu serwera, nazwy logowania i uprawnień na poziomie bazy danych master.
* Określić sposób tooredirect klientów i nowy serwer toohello aplikacji klienta
* Udokumentować inne zależności, takie jak ustawienia inspekcji i alerty

Jeżeli nie poprawnie, Przywracanie aplikacji online po przejściu w tryb failover i odzyskiwanie bazy danych zajmuje dodatkowy czas i może również wymagać rozwiązywania problemów w czasie akcent — Nieprawidłowa kombinacja.

### <a name="fail-over-tooa-geo-replicated-secondary-database"></a>Tryb failover tooa replikowane geograficznie pomocnicze bazy danych
Jeśli używasz aktywna replikacja geograficzna i pracy awaryjnej automatycznie grupy (w podglądzie) jako mechanizm Twojej odzyskiwania można skonfigurować zasady automatycznej pracy awaryjnej lub użyć [ręcznego przełączania trybu failover](sql-database-disaster-recovery.md#fail-over-to-geo-replicated-secondary-database). Po zainicjowaniu hello trybu failover przyczyny hello dodatkowej toobecome hello nowych transakcji nowe toorecord podstawowego i gotowe i Odpowiedz tooqueries — minimalna utrata danych hello danych nie zostały przekazane. Informacje dotyczące projektowania hello procesu trybu failover, zobacz [projektowania aplikacji do chmury odzyskiwania po awarii](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

> [!NOTE]
> Gdy centrum danych hello wraca do trybu online starego kolory podstawowe hello automatycznie ponownie toohello nową podstawową i stają się pomocniczej bazy danych. Region oryginalny podstawowy toohello wstecz hello toorelocate należy planowanego trybu failover można inicjować ręcznie (powrót po awarii). 
> 

### <a name="perform-a-geo-restore"></a>Wykonaj operację przywracania geo
Jeśli używasz automatyczne kopie zapasowe z magazynu geograficznie nadmiarowego replikacji z mechanizmu odzyskiwania [zainicjować odzyskiwanie bazy danych, używając funkcji przywracania geograficznie](sql-database-disaster-recovery.md#recover-using-geo-restore). Odzyskiwanie zwykle odbywa się w ciągu 12 godzin — utraty danych zapasowej godzinę tooone zależą od podczas hello ostatni co godzinę różnicowej kopii zapasowej z podjęte i replikowane. Dopiero po zakończeniu odzyskiwania hello, hello bazy danych jest toorecord wszystkich transakcji lub odpowiada tooany zapytania. Spowoduje to przywrócenie bazy danych toohello ostatni dostępny punkt w czasie, przywracanie hello tooany dodatkowej geograficzna punktu w czasie nie jest obecnie obsługiwane.

> [!NOTE]
> Jeśli centrum danych hello wraca do trybu online przed przejściem aplikacji za pośrednictwem toohello odzyskanej bazy danych, możesz anulować hello odzyskiwania.  
>
>

### <a name="perform-post-failover--recovery-tasks"></a>Wykonywanie zadań po przejściu do trybu failover lub po odzyskiwaniu
Po odzyskaniu z dowolnego z tych mechanizmów odzyskiwania należy wykonać hello następujące dodatkowe zadania przed użytkownikami i aplikacje są kopii zapasowej i uruchamiania:

* Przekierowanie klientów i nowy serwer toohello aplikacji klienta i przywróconej bazy danych
* Upewnij się, reguły zapory poziomu serwera odpowiednie w przypadku tooconnect użytkowników (lub użyj [zapory poziomu bazy danych](sql-database-firewall-configure.md#creating-and-managing-firewall-rules))
* Zapewnij użycie odpowiednich danych logowania i uprawnień na poziomie głównej bazy danych (lub użyj [użytkowników, którzy się w niej znajdują](https://msdn.microsoft.com/library/ff929188.aspx))
* W razie potrzeby skonfiguruj inspekcję
* W razie potrzeby skonfiguruj alerty

## <a name="upgrade-an-application-with-minimal-downtime"></a>Uaktualnianie aplikacji przy minimalnych przestojach
Czasami aplikacji należy podjąć w trybie offline z powodu zaplanowanej konserwacji, takich jak uaktualnienie aplikacji. [Zarządzanie uaktualnieniami aplikacji](sql-database-manage-application-rolling-upgrade.md) w tym artykule opisano, jak uaktualnia tooenable aktywna replikacja geograficzna toouse Twojej chmury aplikacji toominimize przestoju podczas uaktualnienia równoległe i podaj ścieżkę odzyskiwania, jeśli jakaś nieprawidłowość. 

## <a name="next-steps"></a>Następne kroki
Dyskusję na temat zagadnień dotyczących projektowania aplikacji na potrzeby autonomicznych baz danych i pul elastycznych zawierają tematy [Design an application for cloud disaster recovery](sql-database-designing-cloud-solutions-for-disaster-recovery.md) (Projektowanie aplikacji pod kątem odzyskiwania po awarii w chmurze) i [Elastic Pool disaster recovery strategies](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md) (Strategie odzyskiwania po awarii dotyczące pul elastycznych).
