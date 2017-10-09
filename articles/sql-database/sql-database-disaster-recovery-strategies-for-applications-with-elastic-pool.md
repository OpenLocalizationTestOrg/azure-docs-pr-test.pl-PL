---
title: "rozwiązania w zakresie odzyskiwania po awarii aaaDesign — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodesign rozwiązania chmury odzyskiwania po awarii, wybierając hello wzorzec prawo trybu failover."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 2db99057-0c79-4fb0-a7f1-d1c057ec787f
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: sashan;carlrab
ms.openlocfilehash: 9d9eca7570c7a01c992d0b33d449721709b471c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-strategies-for-applications-using-sql-database-elastic-pools"></a>Strategie odzyskiwania po awarii dla aplikacji wykorzystujących pule elastyczne bazy danych SQL
Latach hello ma dowiedzieliśmy się, że usługi w chmurze nie są niezawodne i stanie krytycznego zdarzenia. Baza danych SQL udostępnia kilka możliwości tooprovide dla hello ciągłości działalności biznesowej aplikacji, gdy zdarzenia te występują. [Pule elastyczne](sql-database-elastic-pool.md) i pojedynczych baz danych obsługują hello tego samego rodzaju możliwości odzyskiwania po awarii. W tym artykule opisano kilka strategii odzyskiwania po awarii dla pul elastyczna korzystać z tych funkcjach ciągłości biznesowej bazy danych SQL.

W tym artykule wykorzystano powitania po canonical wzorzec aplikacji SaaS niezależnego dostawcy oprogramowania:

<i>Aplikacja sieci web opartej na chmurze nowoczesnych inicjuje jednej bazy danych SQL dla każdego użytkownika końcowego. Witaj niezależnego dostawcy oprogramowania ma wielu klientów i w związku z tym używa wielu baz danych, nazywane dzierżawy baz danych. Ponieważ hello dzierżawcy z bazy danych mają zwykle działania nieprzewidywalnych wzorców, hello niezależnego dostawcy oprogramowania puli elastycznej toomake hello bazy danych koszt używany bardzo przewidywalną przez dłuższy czas. puli elastycznej Hello także upraszcza zarządzanie wydajności hello, gdy wzrósł hello aktywności użytkownika. Ponadto aplikacji hello baz danych dzierżawy toohello używa wielu baz danych profilów użytkowników toomanage, zabezpieczeń, zbieranie wzorców użycia itd. Dostępność hello poszczególnych dzierżawców nie wpływa na dostępność aplikacji hello jako całość. Jednak hello dostępność i wydajność bazy danych zarządzania ma kluczowe znaczenie dla funkcji aplikacji hello i jeśli bazy danych zarządzania hello są w trybie offline hello całej aplikacji jest w trybie offline.</i>  

W tym artykule omówiono strategii odzyskiwania po awarii, obejmujących szereg scenariuszy z koszt poufnych uruchamiania aplikacji tooones wymagania rygorystyczne dostępności.

## <a name="scenario-1-cost-sensitive-startup"></a>Scenariusz 1. Koszt poufnych uruchamiania
<i>I am firm uruchamiania i bardzo jestem koszt poufnych.  Chcę toosimplify wdrażania i zarządzania aplikacji hello i I ma ograniczone umowy SLA dla poszczególnych odbiorców. Ale chcę aplikacji hello tooensure jako całość nigdy nie jest w trybie offline.</i>

wymaganie prostota hello toosatisfy, wdrażanie wszystkich dzierżawy baz danych w jednej puli elastycznej w hello region platformy Azure w wybranym i wdrażanie baz danych zarządzania jako replikacją geograficzną pojedynczych baz danych. W przypadku odzyskiwania po awarii hello dzierżawców Użyj przywracaniem geograficznym, które pojawia się bez ponoszenia dodatkowych kosztów. dostępność hello tooensure hello zarządzania bazami danych, replikacja geograficzna, ich region tooanother za pomocą trybu failover automatycznie grupy (w — wersja zapoznawcza) (krok 1). Koszt trwającą Hello hello konfiguracji odzyskiwania po awarii w tym scenariuszu jest równy toohello całkowity koszt hello pomocniczej bazy danych. Ta konfiguracja została przedstawiona na diagramie dalej hello.

![Rysunek 1.](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-1.png)

W przypadku wystąpienia awarii w regionie podstawowym hello, toobring kroki odzyskiwania hello aplikacji w trybie online są zilustrowane hello dalej diagramu.

* grupy pracy awaryjnej Hello inicjuje automatycznej pracy awaryjnej hello zarządzania bazy danych toohello DR regionu. Aplikacja Hello jest automatycznie ponownie połączony toohello nowych kont głównych i wszystkich nowych i baz danych dzierżawy są tworzone w regionie DR hello. Witaj istniejących klientów, zobacz swoje dane, które są tymczasowo niedostępne.
* Tworzenie puli elastycznej hello przy użyciu hello samej konfiguracji jak hello oryginalnego puli (2).
* Użyj geograficzne toocreate kopii baz danych, hello dzierżawy (3). Można wziąć pod uwagę wyzwalania przywraca poszczególnych hello przez połączenia przez użytkownika końcowego hello lub użyć innego systemu priorytet specyficzne dla aplikacji.


W tym momencie w regionie DR hello aplikacji jest znowu w trybie online, ale niektórzy klienci opóźnienie podczas uzyskiwania dostępu do swoich danych.

![Rysunek 2](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-2.png)

Jeśli awaria hello tymczasowe, istnieje możliwość tego regionu podstawowego hello zostaną odzyskane przy Azure, zanim wszystkie przywracania bazy danych hello są kompletne w regionie hello odzyskiwania po awarii. W takim przypadku organizowania przenoszenie hello aplikacji wstecz toohello regionu podstawowego. proces Hello trwa hello czynności przedstawione na diagramie dalej hello.

* Anulowanie wszystkich żądań oczekujących przywracaniem geograficznym.   
* Tryb failover hello zarządzania bazami danych toohello regionu podstawowego (5). Po odzyskaniu hello region starego kolory podstawowe hello automatycznie stały się pomocnicze bazy danych. Teraz one ponownie przełączyć się ról. 
* Zmienianie aplikacji hello połączenia ciąg toopoint wstecz toohello głównej regionu. Teraz wszystkich nowych kont i baz danych dzierżawy są tworzone w regionie podstawowym hello. Niektóre istniejących klientów, zobacz swoje dane, które są tymczasowo niedostępne.   
* Ustaw wszystkie bazy danych w hello DR puli tylko tooread tooensure nie można modyfikować w regionie DR hello (6). 
* Dla każdej bazy danych w hello DR puli, która została zmieniona od czasu odzyskiwania hello Zmień lub usuń hello odpowiednie baz danych w puli głównej hello (7). 
* Kopia hello zaktualizować bazy danych z hello DR toohello głównej puli (8). 
* Usuwanie puli DR hello (9)

W tym momencie aplikacji jest w trybie online w regionie podstawowym hello z wszystkich dzierżawy baz danych dostępnych w puli głównej hello.

![Rysunek 3](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-3.png)

klucz Hello **korzystać** ta strategia jest niski koszt trwającą nadmiarowości warstwy danych. Kopie zapasowe są pobierane automatycznie przez hello usługi baza danych SQL z nie aplikacji ponownego zapisywania i bez ponoszenia dodatkowych kosztów.  Koszt Hello poniesienia tylko wtedy, gdy zostaną przywrócone hello elastycznych baz danych. Witaj **zależność** jest, że hello ukończenia odzyskiwania wszystkich baz danych dzierżawy ma długiego czasu. Witaj czas zależy od hello całkowitej liczby operacji przywracania inicjowania w hello DR regionu i całkowitego rozmiaru hello dzierżawy baz danych. Nawet w przypadku przywracania niektórzy dzierżawcy jest priorytety przez innych użytkowników, rywalizuje o hello wszystkich innych operacji przywracania, które są inicjowane w hello tego samego regionu jako usługa hello rozstrzyga o kolejności przetwarzania i ogranicza toominimize hello ogólnego wpływu na powitania klientów istniejących baz danych. Ponadto hello odzyskiwania baz danych dzierżawy hello nie można uruchomić, dopóki nie zostanie utworzona nowa pula elastyczna hello w regionie DR hello.

## <a name="scenario-2-mature-application-with-tiered-service"></a>Scenariusz 2. Dojrzała aplikacji z usługą warstwowych
<i>Jestem dojrzałe aplikacji SaaS oferty usługi warstwowych i innej umowy SLA dla klientów z wersji próbnej i płatności klientów. W przypadku wersji próbnej klientów hello masz hello tooreduce koszt możliwie. Klienci wersji próbnej może zająć Przestój, ale chcę tooreduce jego prawdopodobieństwo. W przypadku płatności klientom Witaj przestój jest ryzyko transmitowane. Tak, chcę toomake się, że klienci płatniczych są zawsze tooaccess stanie ich danych.</i> 

toosupport, w tym scenariuszu oddzielne hello próbne z płatnej dzierżawcy przez umieszczenie ich w osobnych pulach elastycznej. Klienci wersji próbnej Hello mają niższe eDTU na dzierżawy i dolnym SLA dłuższego czasu odzyskiwania. płatniczych klientom Witaj znajdują się w puli z wyższej eDTU na dzierżawę i wyższe umowy SLA. tooguarantee hello najniższy czas odzyskiwania, baz danych dzierżawy hello płatniczych klientów są replikacją geograficzną. Ta konfiguracja została przedstawiona na diagramie dalej hello. 

![Rysunek 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-4.png)

Jak hello pierwszego scenariusza baz danych zarządzania hello jest dość aktywnych, aby używać jednego replikacją geograficzną bazy danych dla niego (1). Dzięki temu hello przewidywalną wydajność nowe subskrypcje klienta, aktualizacji profilu i innych operacji zarządzania. Witaj regionu, w którym znajdują się kolory podstawowe hello baz danych zarządzania hello jest hello regionu podstawowego i hello regionu, w którym znajdują się hello pomocniczych baz danych zarządzania hello jest region hello odzyskiwania po awarii.

Witaj płacących odbiorców dzierżawcy z bazy danych ma active baz danych w puli udostępniane w regionie podstawowym hello "płatnej" hello. Udostępnić dodatkowej puli z hello takie same nazwy w regionie hello odzyskiwania po awarii. Poszczególni dzierżawcy jest puli dodatkowej toohello replikacją geograficzną (2). Umożliwia to szybkie odzyskiwanie wszystkie dzierżawy bazy danych przy użyciu trybu failover. 

W przypadku wystąpienia awarii w regionie podstawowym hello, toobring kroki odzyskiwania hello aplikacji w trybie online są przedstawione na diagramie dalej hello:

![Rysunek 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-5.png)

* Bezpośrednio w trybie Failover hello zarządzania bazami danych toohello DR region (3).
* Zmień aplikacji hello połączenia ciąg toopoint toohello DR regionu. Teraz wszystkich nowych kont i baz danych dzierżawy są tworzone w regionie DR hello. Hello istniejących klientów wersji próbnej, zobacz swoje dane, które są tymczasowo niedostępne.
* Tryb failover hello płatnej puli toohello baz danych dzierżawcy w hello DR region tooimmediately przywrócić ich dostępności (4). Ponieważ trybu failover hello jest szybkie metadanych zmiany poziomu, należy wziąć pod uwagę optymalizacji, gdzie poszczególne praca awaryjna hello są wyzwalane na żądanie przez hello połączenia przez użytkownika końcowego. 
* Jeśli rozmiar eDTU puli dodatkowej został niższa niż hello podstawowego, ponieważ tylko wymagane hello tooprocess hello Zmiana wydajności rejestruje podczas ich zostały pomocnicze bazy danych, bazy danych dodatkowej hello natychmiast zwiększyć pojemność puli hello teraz tooaccommodate hello pełnej Obciążenie wszystkich dzierżaw (5). 
* Utwórz nową pulę elastyczną hello z hello takie same nazwy i hello sam konfiguracji w regionie hello odzyskiwania po awarii dla klientów wersji próbnej hello baz danych (6). 
* Po utworzeniu puli hello wersji próbnej klientów za pomocą geograficzne toorestore hello poszczególne dzierżawy w wersji próbnej z bazy danych do nowej puli hello (7). Należy wziąć pod uwagę wyzwalania przywraca poszczególnych hello przez połączenia przez użytkownika końcowego hello, lub użyj innego systemu priorytet specyficzne dla aplikacji.

W tym momencie aplikacja jest znowu w trybie online w regionie DR hello. Wszystkie płatniczych klienci mają dostęp do danych tootheir podczas wersji próbnej klientom Witaj opóźnienie podczas uzyskiwania dostępu do swoich danych.

Gdy regionu podstawowego hello zostaną odzyskane przy Azure *po* została przywrócona aplikacji hello w regionie hello odzyskiwania po awarii można kontynuować używanie aplikacji hello w tym regionie lub można określić regionu podstawowego toofail toohello Wstecz. Jeśli jest odzyskiwana regionu podstawowego hello *przed* hello trybu failover proces jest zakończony, należy wziąć pod uwagę w przypadku braku wstecz od razu. Powrót po awarii Hello przyjmuje hello czynności przedstawione na diagramie dalej hello: 

![Rysunek 6.](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-6.png)

* Anulowanie wszystkich żądań oczekujących przywracaniem geograficznym.   
* Tryb failover hello zarządzania z bazy danych (8). Po odzyskaniu hello region hello stary serwer podstawowy automatycznie stanie się hello dodatkowej. Teraz, staje się on Witaj ponownie podstawowego.  
* Tryb failover hello płatnej dzierżawy baz danych (9). Podobnie po odzyskaniu hello region starego kolory podstawowe hello automatycznie stanie się hello pomocnicze bazy danych. Teraz stają się one kolory podstawowe hello ponownie. 
* Zestaw hello przywrócona wersji próbnej baz danych, które zostały zmienione w regionie DR hello tylko tooread (10).
* Dla każdej bazy danych w puli odzyskiwania po awarii klientom wersji próbnej hello, która zmienione od czasu odzyskiwania hello Zmień lub usuń hello odpowiednią bazę danych w puli głównej hello klientów wersji próbnej (11). 
* Kopiuj hello zaktualizować baz danych z hello DR toohello głównej puli (12). 
* Usuwanie puli DR hello [13] 

> [!NOTE]
> Operacja trybu failover Hello jest asynchroniczne. czas odzyskiwania hello toominimize, jest ważne, wykonaj polecenie pracy awaryjnej hello dzierżawy baz danych w partiach co najmniej 20 baz danych. 
> 
> 

klucz Hello **korzystać** tej strategii jest hello najwyższy umowy SLA dla hello płatności klientów. Gwarantuje również to hello nowe wersje próbne są odblokowane, natychmiast po utworzeniu hello wersji próbnej DR puli. Witaj **zależność** otrzymuje że taka konfiguracja zwiększa hello całkowity koszt hello dzierżawcy z bazy danych przez koszt hello hello dodatkowej puli odzyskiwania po awarii dla klientów. Dodatkowo Jeśli pula dodatkowej hello ma inny rozmiar, płatniczych klientom Witaj wydajność niższe po pracy awaryjnej zakończenia hello uaktualnienia puli w regionie hello odzyskiwania po awarii. 

## <a name="scenario-3-geographically-distributed-application-with-tiered-service"></a>Scenariusz 3. Geograficznie rozproszonych aplikacji przy użyciu usługi warstwowej
<i>Masz dojrzałe aplikacji SaaS z ofertami warstwowych usługi. Chcę toooffer bardzo agresywnie toomy SLA płatnej klientów, zminimalizować ryzyko hello znaczenie w przypadku wystąpienia awarii, ponieważ nawet krótki przerwania może spowodować niezadowolenie klienta. Jest krytyczne w tym hello płatności klienci zawsze mogą mieć dostęp do swoich danych. próby Hello są bezpłatne i umowa SLA nie jest oferowany podczas okresu próbnego hello.</i> 

toosupport tego scenariusza, użyj trzech oddzielnych elastyczne pule. Dwie pule taki sam rozmiar świadczenia z wysoką jednostek Edtu na bazę danych w dwóch różnych regionach toocontain hello płatnej klientów dzierżawcy z bazy danych. Pula trzeci Hello zawierająca próbne hello może być niższe jednostek Edtu na bazę danych i udostępniane w jednym z dwóch regionach hello.

tooguarantee hello najniższy czas odzyskiwania podczas awarii, bazy danych dzierżawy hello płatniczych klientów są, replikacją geograficzną z 50% hello głównej bazy danych w hello dwóch regionach. Podobnie każdy region ma 50% hello pomocniczej bazy danych. Dzięki temu, jeśli region jest w trybie offline, tylko 50% hello płatnej baz danych klientów wpływ na i mieć toofail za pośrednictwem. Witaj pozostaną nienaruszone innych baz danych. Ta konfiguracja została przedstawiona w powitania po diagramu:

![Rysunek 4](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-7.png)

Jak w poprzednich scenariuszach hello są dość aktywnej bazy danych zarządzania hello tak skonfigurowane jako pojedyncze replikacją geograficzną bazy danych (1). Dzięki temu hello przewidywalną wydajność hello nowe subskrypcje klienta, aktualizacji profilu i innych operacji zarządzania. Region A jest hello regionu podstawowego dla baz danych zarządzania hello i hello region B służy do odzyskiwania bazy danych zarządzania hello.

bazy danych dzierżawy Hello płatniczych klientów są również replikacją geograficzną, ale z kolory podstawowe i pomocnicze podzielony między region A i region B (2). W ten sposób hello dzierżawy głównej bazy danych wpływ awarii hello może przełączyć się toohello innego regionu i stają się dostępne. Witaj, druga połowa hello dzierżawcy z bazy danych nie można wpływ na cały. 

Witaj dalej diagramie przedstawiono tootake kroki odzyskiwania hello, w przypadku wystąpienia awarii w regionie A.

![Rysunek 5](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-8.png)

* Bezpośrednio w trybie Failover hello zarządzania bazami danych tooregion B (3).
* Zmień aplikacji hello połączenia ciąg toopoint toohello zarządzania baz danych w regionie zmodyfikować B. hello zarządzania baz danych toomake się, że hello nowych kont i baz danych dzierżawy są tworzone w regionie B i brak znaleziono hello istniejących baz danych dzierżawy jako źródło. Hello istniejących klientów wersji próbnej, zobacz swoje dane, które są tymczasowo niedostępne.
* Tryb failover hello płatnej dzierżawcy baz danych toopool 2 w regionie B tooimmediately przywrócić ich dostępności (4). Ponieważ trybu failover hello jest szybkie metadanych zmiany poziomu, można rozważyć optymalizacji, gdzie poszczególne praca awaryjna hello są wyzwalane na żądanie przez hello połączenia przez użytkownika końcowego. 
* Od teraz puli 2 zawiera tylko głównej bazy danych, hello całkowita obciążenia wzrost puli hello i natychmiast może zwiększyć rozmiaru eDTU (5). 
* Utwórz nową pulę elastyczną hello z hello takie same nazwy i hello sam konfiguracji w regionie hello B dla klientów wersji próbnej hello baz danych (6). 
* Po hello tworzona jest pula Użyj geograficzne toorestore hello poszczególne dzierżawy w wersji próbnej bazy danych w puli hello (7). Można wziąć pod uwagę wyzwalania przywraca poszczególnych hello przez połączenia przez użytkownika końcowego hello lub użyć innego systemu priorytet specyficzne dla aplikacji.

> [!NOTE]
> Operacja trybu failover Hello jest asynchroniczne. czas odzyskiwania hello toominimize, ważne jest wykonanie polecenia pracy awaryjnej hello dzierżawy baz danych w partiach co najmniej 20 baz danych. 
> 

W tym momencie aplikacja jest znowu w trybie online w regionie B. Wszystkie płatniczych klienci mają dostęp do danych tootheir podczas wersji próbnej klientom Witaj opóźnienie podczas uzyskiwania dostępu do swoich danych.

Po odzyskaniu region, A musi toodecide, jeśli chcesz toouse region B dla klientów z wersji próbnej lub powrotu po awarii toousing hello wersji próbnej klientów puli w regionie A. Jedno kryterium można % hello baz danych dzierżawy w wersji próbnej zmodyfikowane hello odzyskiwania. Niezależnie od tej decyzji należy dzierżaw hello płatnej toore równowagi między dwoma zestawami. Witaj dalej diagram przedstawia proces hello, gdy hello dzierżawy w wersji próbnej z bazy danych nie powiedzie się wstecz tooregion A.  

![Rysunek 6.](./media/sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool/diagram-9.png)

* Anulowanie wszystkich oczekujących przywracaniem geograficznym żądań tootrial DR puli.   
* Tryb failover baza danych zarządzania hello (8). Po odzyskaniu hello region hello stary serwer podstawowy automatycznie aktywowano hello dodatkowej. Teraz, staje się on Witaj ponownie podstawowego.  
* Wybierz, które płatną dzierżawy bazy danych niepowodzenie wstecz toopool 1 i zainicjuj tryb failover tootheir pomocnicze bazy danych (9). Po odzyskaniu hello regionu wszystkie bazy danych w puli 1 została automatycznie pomocnicze bazy danych. Teraz 50% ich stają się ponownie kolory podstawowe. 
* Zmniejszyć rozmiar hello eDTU oryginalnego puli 2 toohello (10).
* Ustaw wszystkie przywrócone wersji próbnej baz danych w regionie hello B tylko tooread (11).
* Dla każdej bazy danych w hello wersji próbnej DR puli, która została zmieniona od czasu odzyskiwania hello Zmień lub usuń hello odpowiednią bazę danych w wersji próbnej puli głównej hello (12). 
* Kopiuj hello zaktualizować bazy danych z hello DR toohello głównej puli [13]. 
* Usuwanie puli DR hello (14) 

klucz Hello **korzyści** tej strategii są:

* Obsługuje ona hello najbardziej agresywne umowy SLA dla hello płatności klientów, ponieważ zapewnia, że awarii nie może mieć wpływ na więcej niż 50% hello dzierżawcy z bazy danych. 
* Gwarantuje hello nowe wersje próbne są odblokowane, jak dziennik hello DR puli jest tworzona podczas odzyskiwania hello. 
* Umożliwia efektywniejsze wykorzystanie pojemności puli hello 50% dodatkowej bazy danych w puli 1 i 2 puli dotrą toobe mniej aktywne niż hello głównej bazy danych.

Witaj głównego **kompromisy** są:

* operacji CRUD Hello bazach danych zarządzania hello mieć mniejsze opóźnienia dla hello użytkownicy końcowi połączone tooregion A niż dla tooregion użytkownicy końcowi połączone hello B są wykonywane przed hello podstawowy hello zarządzania z bazy danych.
* Wymaga to bardziej złożonych projektu hello zarządzania z bazy danych. Na przykład każdy rekord dzierżawy ma tag lokalizacji wymagające toobe została zmieniona w trakcie pracy awaryjnej i powrotu po awarii.  
* Hello płatności klientów może zgłaszać obniżenia wydajności niż zwykle hello uaktualnienia puli w regionie B ukończenie. 

## <a name="summary"></a>Podsumowanie
Ten artykuł skupia się na strategii odzyskiwania po awarii hello hello warstwy bazy danych używana przez aplikację wielodostępne SaaS niezależnego dostawcy oprogramowania. Hello strategii wybierzesz opiera się na potrzeby hello aplikacji hello, takie jak hello modelu biznesowego, hello SLA mają toooffer tooyour klientów, budżetu ograniczenia itp. Każdy opisano strategii opisanych hello korzyści i zależność, można podjąć świadomej decyzji. Określonych aplikacji może także inne składniki platformy Azure. Aby przejrzeć ich wskazówki ciągłości biznesowej i organizowania odzyskiwania hello hello warstwy bazy danych z nimi. toolearn więcej informacji o zarządzaniu odzyskiwania bazy danych aplikacji na platformie Azure, zobacz zbyt[projektowania rozwiązań chmury odzyskiwania po awarii](sql-database-designing-cloud-solutions-for-disaster-recovery.md).  

## <a name="next-steps"></a>Następne kroki
* toolearn o bazy danych SQL Azure automatycznego tworzenia kopii zapasowych, zobacz [bazy danych SQL automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md).
* Omówienie ciągłości działalności biznesowej i scenariuszy, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).
* toolearn o za pomocą kopie zapasowe automatycznego odzyskiwania, zobacz [przywrócić bazę danych z kopii zapasowych hello inicjowane przez usługę](sql-database-recovery-using-backups.md).
* toolearn o szybsze opcje odzyskiwania, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md).
* toolearn o za pomocą automatycznych kopii zapasowej do archiwizacji, zobacz [kopiowanie bazy danych](sql-database-copy.md).

