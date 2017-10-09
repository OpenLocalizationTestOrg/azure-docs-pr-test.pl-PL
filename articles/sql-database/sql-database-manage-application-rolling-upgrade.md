---
title: "Uaktualnianie aplikacji aaaRolling — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse replikacja geograficzna bazy danych SQL Azure toosupport online uaktualnień aplikacji w chmurze."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 58f42859-1e37-463c-a3d8-a3ca2e867148
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/16/2016
ms.author: sashan
ms.openlocfilehash: 18c56300916d129bff141624cc5c416b500408d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-rolling-upgrades-of-cloud-applications-using-sql-database-active-geo-replication"></a>Zarządzanie stopniowe aplikacji w chmurze przy użyciu aktywna replikacja geograficzna bazy danych SQL
> [!NOTE]
> [Aktywna replikacja geograficzna](sql-database-geo-replication-overview.md) jest teraz dostępna dla wszystkich baz danych w warstwach wszystkie.
> 

Dowiedz się, jak toouse [— replikacja geograficzna](sql-database-geo-replication-overview.md) w tooenable bazy danych SQL wprowadzanie uaktualnień aplikacji w chmurze. Ponieważ uaktualnienie jest dużo operacji, należy go części projektowania i planowania ciągłości biznesowej. W tym artykule, który opisano dwie różne metody organizowanie hello proces uaktualniania, a omówimy korzyści hello i kompromisy każdej z nich. Dla celów hello w tym artykule używamy prostą aplikację, która składa się z witryny sieci web połączonych tooa pojedynczej bazy danych jako jego warstwy danych. Naszym celem jest tooupgrade wersja 1 tooversion aplikacji hello 2 bez znacznego wpływu na środowisko pracy użytkownika końcowego hello. 

Podczas obliczania hello opcje uaktualniania należy rozważyć hello następujące czynniki:

* Wpływ na dostępność aplikacji podczas uaktualniania. Jak długo funkcja aplikacji hello może być ograniczony lub nieprawidłowego działania.
* Możliwość tooroll wstecz na wypadek niepowodzenia uaktualnienia.
* Luki w zabezpieczeniach aplikacji hello po wystąpieniu błędu krytycznego niepowiązanych podczas uaktualniania hello.
* Dolar całkowity koszt.  Obejmuje to dodatkowa Redundancja i przyrostowe kosztów składników tymczasowego hello używanych przez proces uaktualniania hello. 

## <a name="upgrading-applications-that-rely-on-database-backups-for-disaster-recovery"></a>Uaktualnianie aplikacji, które opierają się na kopie zapasowe bazy danych dla odzyskiwania po awarii
Jeśli aplikacji opiera się na automatyczne bazy danych kopii zapasowych i używa geograficzne do odzyskiwania po awarii, jest zazwyczaj wdrożonej tooa pojedynczy region platformy Azure. W takim przypadku proces uaktualniania hello obejmuje utworzenie kopii zapasowej wdrożenia wszystkich składników aplikacji objętego hello uaktualnienia. Menedżer ruchu Azure (WATM) będzie korzystać z profilem trybu failover hello zakłóceń użytkownika końcowego hello toominimize.  powitania po diagram ilustruje proces uaktualniania hello środowisko operacyjne wcześniejsze toohello. Witaj punktu końcowego <i>contoso 1.azurewebsites.net</i> reprezentuje gnieździe produkcyjnym aplikacji hello, która potrzebuje toobe uaktualniony. ponownie tooroll możliwości hello tooenable hello uaktualnienia, należy Utwórz miejsce etap kopię pełni zsynchronizowanych aplikacji hello. Hello poniższe kroki są wymagane tooprepare hello aplikacji hello uaktualnienia:

1. Utwórz miejsce etap hello uaktualnienia. toodo tworzenie pomocniczej bazy danych (1), a następnie wdrożona identyczne witryny hello tego samego regionu systemu Azure. Monitorowanie toosee dodatkowej hello Jeśli hello wstępne wypełnianie procesu zostało ukończone.
2. Utwórz profil trybu failover w WATM z <i>contoso 1.azurewebsites.net</i> jako punkt końcowy w trybie online i <i>contoso 2.azurewebsites.net</i> w trybie offline. 

> [!NOTE]
> Czynności przygotowujące hello Uwaga nie ma wpływu aplikacji hello w gnieździe produkcyjnym hello i może działać w trybie pełnego dostępu.
>  

![Konfiguracja replikacji Przejdź bazy danych SQL. Odzyskiwanie awaryjne chmury.](media/sql-database-manage-application-rolling-upgrade/Option1-1.png)

Po wykonaniu czynności przygotowujące hello aplikacji hello jest gotowy do uaktualnienia rzeczywiste hello. powitania po diagram ilustruje hello etapy hello procesu uaktualniania. 

1. Ustaw hello podstawowej bazy danych w hello produkcji miejsca tylko tooread tryb [3]. Gwarantuje to, że hello produkcji wystąpienie aplikacji hello (wersja 1) pozostanie tylko do odczytu podczas uaktualniania hello zindeksowanie hello danych rozbieżności między hello V1 i V2 wystąpień bazy danych.  
2. Odłącz dodatkowej bazy danych hello w trybie hello planowane zakończenie (4). Utworzy on pełni zsynchronizowanej kopii niezależne hello podstawowej bazy danych. Ta baza danych zostanie uaktualniona.
3. Włącz tryb zapisu tooread podstawowej bazy danych hello, a następnie uruchom skrypt uaktualnienia hello w gnieździe etap hello [5].     

![Konfiguracja — replikacja geograficzna bazy danych SQL. Odzyskiwanie awaryjne chmury.](media/sql-database-manage-application-rolling-upgrade/Option1-2.png)

Jeśli aktualizacja hello zakończyła się pomyślnie wszystko jest teraz gotowy tooswitch hello użytkownicy końcowi toohello przemieszczane kopiowania hello aplikacji. Teraz będzie gotowa do miejsca produkcji hello aplikacji hello.  Ten proces obejmuje kilka kroków więcej zgodnie z opisami na powitania po diagramu.

1. Przełącz hello online punktu końcowego w profilu WATM hello zbyt<i>contoso 2.azurewebsites.net</i>, wersji toohello V2 punktów hello witryny sieci web (6). Staje się teraz gniazda produkcyjnego hello z hello aplikacji V2 i ruch przez użytkownika końcowego hello jest tooit bezpośrednie.  
2. Jeśli nie są już potrzebne składniki aplikacji hello V1, możesz bezpiecznie usunąć je (7).   

![Konfiguracja — replikacja geograficzna bazy danych SQL. Odzyskiwanie awaryjne chmury.](media/sql-database-manage-application-rolling-upgrade/Option1-3.png)

Jeśli proces uaktualniania hello zakończy się niepowodzeniem, na przykład ze względu na błąd tooan skryptów uaktualniania hello, hello etap miejsca należy traktować jako naruszenia zabezpieczeń. tooroll kopii hello toohello przed uaktualnieniem stanu aplikacji po prostu przywrócić aplikacji hello w hello produkcji miejsca toofull dostępu. etapy Hello są wyświetlane na diagramie dalej hello.    

1. Ustaw hello trybu tooread zapisu kopii bazy danych (8). Spowoduje to przywrócenie hello pełne V1 funkcjonalnie w gnieździe produkcyjnym hello.
2. Analiza Przyczyna hello głównego i usunąć składniki hello naruszone w gnieździe etap hello (9). 

W tym momencie aplikacji hello jest w pełni funkcjonalny i kroki uaktualniania hello można powtarzać.

> [!NOTE]
> Witaj wycofywania nie wymaga zmian w profilu WATM jako już wskazuje zbyt<i>contoso 1.azurewebsites.net</i> jako hello aktywny punkt końcowy.
> 
> 

![Konfiguracja — replikacja geograficzna bazy danych SQL. Odzyskiwanie awaryjne chmury.](media/sql-database-manage-application-rolling-upgrade/Option1-4.png)

klucz Hello **korzyści** tej opcji jest uaktualnienie aplikacji w pojedynczym regionie przy użyciu zestawu prostych krokach. Koszt dolara Hello uaktualnienia hello jest stosunkowo niska. Witaj głównego **zależnościami** jest, że jeśli wystąpi błąd krytyczny podczas stan sprzed uaktualnienia toohello hello hello uaktualnienia odzyskiwania będzie obejmować ponownego wdrażania aplikacji hello w innym regionie i przywracania hello bazy danych z Tworzenie kopii zapasowej korzystającej z przywracaniem geograficznym. Ten proces spowoduje znaczne przestoju.   

## <a name="upgrading-applications-that-rely-on-database-geo-replication-for-disaster-recovery"></a>Uaktualnianie aplikacji, które zależą od bazy danych — replikacja geograficzna odzyskiwania po awarii
Jeśli aplikacja korzysta z georeplikacji ciągłość prowadzenia działalności biznesowej, jest tooat wdrożony co najmniej dwóch różnych regionach z aktywnym wdrożeniu w regionie podstawowym i rezerwy wdrożenia w regionie kopii zapasowej. Ponadto czynniki toohello wspomniano wcześniej, hello procesu uaktualniania należy zagwarantować, że:

* Aplikacja Hello pozostaje chroniona przed poważnej awarii przez cały czas podczas procesu uaktualniania hello
* Witaj geograficznie nadmiarowego składniki aplikacji hello są uaktualniane równolegle ze składnikami active hello

tooachieve profilu tych celów, przy użyciu trybu failover hello Azure ruchu Manager (WATM) będzie korzystać z jedna aktualizacja aktywna i trzy punkty końcowe kopii zapasowej.  powitania po diagram ilustruje proces uaktualniania hello środowisko operacyjne wcześniejsze toohello. Witaj witryn sieci web <i>contoso 1.azurewebsites.net</i> i <i>contoso dr.azurewebsites.net</i> reprezentują gnieździe produkcyjnym aplikacji hello z nadmiarowością pełnej geograficznych. ponownie tooroll możliwości hello tooenable hello uaktualnienia, należy Utwórz miejsce etap kopię pełni zsynchronizowanych aplikacji hello. Ponieważ potrzebna tooensure aplikacji hello Szybkie odzyskiwanie w przypadku, gdy wystąpi błąd krytyczny podczas procesu uaktualniania hello hello etap miejsca musi toobe geograficznie nadmiarowego również. Hello poniższe kroki są wymagane tooprepare hello aplikacji hello uaktualnienia:

1. Utwórz miejsce etap hello uaktualnienia. toodo tworzenie pomocniczej bazy danych (1), a następnie wdrożona identyczne kopię hello witryny sieci web w hello tego samego regionu systemu Azure. Monitorowanie toosee dodatkowej hello Jeśli hello wstępne wypełnianie procesu zostało ukończone.
2. Utwórz geograficznie nadmiarowego pomocniczej bazy danych w miejscu etap hello poprzez replikację geograficzną hello dodatkowej bazy danych toohello kopii zapasowej region (jest to nazywane "łańcuchowej — replikacja geograficzna"). Monitorowanie kopii zapasowej toosee dodatkowej hello Jeśli hello wstępne wypełnianie procesu jest wypełniony (3).
3. Utwórz kopię rezerwy hello witryny sieci web w regionie kopii zapasowej hello, a następnie połącz go toohello pomocniczy geograficznie nadmiarowego (4).  
4. Dodaj dodatkowe punkty końcowe hello <i>contoso 2.azurewebsites.net</i> i <i>contoso 3.azurewebsites.net</i> toohello profilu trybu failover w WATM jako punktów końcowych w trybie offline (5). 

> [!NOTE]
> Czynności przygotowujące hello Uwaga nie ma wpływu aplikacji hello w gnieździe produkcyjnym hello i może działać w trybie pełnego dostępu.
> 
> 

![Konfiguracja — replikacja geograficzna bazy danych SQL. Odzyskiwanie awaryjne chmury.](media/sql-database-manage-application-rolling-upgrade/Option2-1.png)

Po wykonaniu czynności przygotowujące hello miejsca etap hello jest gotowy do uaktualnienia hello. powitania po diagram przedstawia kroki uaktualniania hello.

1. Ustaw hello podstawowej bazy danych w hello produkcji miejsca tylko tooread tryb (6). Gwarantuje to, że hello produkcji wystąpienie aplikacji hello (wersja 1) pozostanie tylko do odczytu podczas uaktualniania hello zindeksowanie hello danych rozbieżności między hello V1 i V2 wystąpień bazy danych.  
2. Odłącz hello dodatkowej bazy danych przy użyciu tego samego regionu w hello hello tryb planowane zakończenie (7). Utworzy on pełni zsynchronizowanej kopii niezależne hello podstawowej bazy danych, które automatycznie stanie się podstawowym po zakończeniu hello. Ta baza danych zostanie uaktualniona.
3. Włącz hello podstawowej bazy danych w trybie zapisu tooread miejsca etap hello, a następnie uruchom skrypt uaktualnienia hello (8).    

![Konfiguracja — replikacja geograficzna bazy danych SQL. Odzyskiwanie awaryjne chmury.](media/sql-database-manage-application-rolling-upgrade/Option2-2.png)

Aktualizacja hello zakończyła się pomyślnie są teraz gotowe tooswitch hello użytkownicy końcowi toohello V2 wersję aplikacji hello. powitania po diagram ilustruje hello etapy.

1. Przełącz hello aktywny punkt końcowy w profilu WATM hello zbyt<i>contoso 2.azurewebsites.net</i>, które teraz wskazuje wersję toohello V2 hello witryny sieci web (9). Staje się teraz gnieździe produkcyjnym z hello aplikacji V2 i ruch przez użytkownika końcowego jest bezpośrednie tooit. 
2. Jeśli nie są już potrzebne hello V1 aplikacji, możesz bezpiecznie usunąć go (10 i 11).  

![Konfiguracja — replikacja geograficzna bazy danych SQL. Odzyskiwanie awaryjne chmury.](media/sql-database-manage-application-rolling-upgrade/Option2-3.png)

Jeśli proces uaktualniania hello zakończy się niepowodzeniem, na przykład ze względu na błąd tooan skryptów uaktualniania hello, hello etap miejsca należy traktować jako naruszenia zabezpieczeń. tooroll kopii hello toohello przed uaktualnieniem stanu aplikacji po prostu przywrócić aplikacji hello toousing w gnieździe produkcyjnym hello z pełnym dostępem. etapy Hello są wyświetlane na diagramie dalej hello.    

1. Zestaw hello kopia podstawowej bazy danych w trybie zapisu tooread miejscem produkcyjnym hello (12). Spowoduje to przywrócenie hello pełne V1 funkcjonalnie w gnieździe produkcyjnym hello.
2. Analiza Przyczyna hello głównego i usunąć składniki hello naruszone w gnieździe etap hello (13 i 14). 

W tym momencie aplikacji hello jest w pełni funkcjonalny i kroki uaktualniania hello można powtarzać.

> [!NOTE]
> Witaj wycofywania nie wymaga zmian w profilu WATM jako już wskazuje zbyt <i>contoso 1.azurewebsites.net</i> jako hello aktywny punkt końcowy.
> 
> 

![Konfiguracja — replikacja geograficzna bazy danych SQL. Odzyskiwanie awaryjne chmury.](media/sql-database-manage-application-rolling-upgrade/Option2-4.png)

klucz Hello **korzyści** tej opcji jest można uaktualnić zarówno aplikacji hello, jak i jego geograficznie nadmiarowego kopiowania równolegle w bez naruszania ciągłość prowadzenia działalności biznesowej podczas uaktualniania hello. Witaj głównego **zależnościami** wymaga nadmiarowości dwa razy każdego składnika aplikacji i w związku z tym generuje wyższy koszt dolara ($). Obejmuje ona również bardziej skomplikowanych przepływów pracy. 

## <a name="summary"></a>Podsumowanie
Witaj dwie metody uaktualniania opisane w artykule hello różnią się złożoność i hello dolara kosztów, ale obie skupić się na minimalizując hello czasu, gdy użytkownik końcowy hello jest ograniczony tylko do tooread operacji. Tego czasu bezpośrednio jest zdefiniowana przez czas trwania hello hello skryptu uaktualnienia. Nie jest zależny od rozmiaru bazy danych hello, usługi hello warstwy, wybierz opcję, hello konfiguracji witryny sieci web i innych czynników, które nie można łatwo zarządzać. Jest to spowodowane wszystkie kroki przygotowania hello jest całkowicie niezależna od hello kroki uaktualniania i mogą być przeprowadzane bez wpływu na powitania aplikacji produkcyjnej. wydajność Hello skryptu uaktualnienia hello jest hello kluczowym czynnikiem, określająca hello środowisko użytkownika końcowego podczas uaktualniania. Dlatego najlepiej hello mogła ją udoskonalać jest koncentrujące się wysiłków na tworzenie skryptów uaktualniania hello jak najbardziej efektywne.  

## <a name="next-steps"></a>Następne kroki
* Omówienie ciągłości działalności biznesowej i scenariuszy, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).
* toolearn o bazy danych SQL Azure automatycznego tworzenia kopii zapasowych, zobacz [bazy danych SQL automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md).
* toolearn o za pomocą kopie zapasowe automatycznego odzyskiwania, zobacz [przywrócić bazę danych z automatycznych kopii zapasowych](sql-database-recovery-using-backups.md).
* toolearn o szybsze opcje odzyskiwania, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md).


