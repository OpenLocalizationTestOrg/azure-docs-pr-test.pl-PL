---
title: aaaSQL testowanie odzyskiwania po awarii bazy danych | Dokumentacja firmy Microsoft
description: "Uczyć się wskazówki i najlepsze rozwiązania dotyczące korzystania z bazy danych SQL Azure tooperform awaryjnego odzyskiwania ćwiczenia toohelp Zachowaj toofailures odporność aplikacji krytycznym znaczeniu dla firmy misji i awarie."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a>Wykonywanie wyszczególniania odzyskiwania po awarii
Zalecane jest okresowo wykonywać weryfikacji aplikacja jest gotowa do przepływu pracy odzyskiwania. Weryfikowanie, czy zachowanie aplikacji hello i zagadnień dotyczących danych utraty i/lub hello przerw w działaniu obejmuje czy tryb failover jest dobrym rozwiązaniem engineering. Również jest wymagane przez większość standardy branżowe w ramach certyfikacji ciągłości biznesowej.

Obejmuje wykonywania wyszczególniania odzyskiwania po awarii:

* Symulowanie symulacje awarii warstwy danych
* Odzyskiwanie
* Sprawdź poprawność odzyskiwania post integralności aplikacji

W zależności od tego, jak możesz [przeznaczony dla ciągłość prowadzenia działalności biznesowej aplikacji](sql-database-business-continuity.md), hello przepływu pracy tooexecute hello Przechodzenie do szczegółów mogą się różnić. Poniżej opisano najważniejsze wskazówki hello przeprowadzenie wyszczególniania odzyskiwania po awarii, w kontekście hello bazy danych SQL Azure.

## <a name="geo-restore"></a>Przywracanie geograficzne
tooprevent hello utracie danych podczas przeprowadzania wyszczególniania odzyskiwania po awarii, zaleca się przeprowadzania hello Przechodzenie do szczegółów, tworząc kopię hello środowiska produkcyjnego i używa go przy użyciu środowiska testowego aplikacji hello tooverify przepływu pracy awaryjnej.

#### <a name="outage-simulation"></a>Symulacji awarii
toosimulate hello awarii, można usunąć ani zmienić nazwy hello źródłowej bazy danych. Powoduje to błędów łączności aplikacji.

#### <a name="recovery"></a>Odzyskiwanie
* Wykonać przywracaniem geograficznym hello hello bazy danych na innym serwerze, zgodnie z opisem [tutaj](sql-database-disaster-recovery.md).
* Zmień hello aplikacji konfiguracji tooconnect toohello odzyskanej bazy danych i wykonaj hello [skonfigurować bazę danych po odzyskaniu](sql-database-disaster-recovery.md) przewodnik toocomplete hello odzyskiwania.

#### <a name="validation"></a>Walidacja
* Zakończenie hello Przechodzenie do szczegółów weryfikując aplikacji hello integralności post odzyskiwania (w tym parametry połączenia, logowania, podstawowych funkcji testowania lub innych operacji sprawdzania poprawności część procedur signoffs standardowej aplikacji).

## <a name="geo-replication"></a>Replikacja geograficzna
Dla bazy danych, która jest chroniony za pomocą Przechodzenie do szczegółów — replikacja geograficzna hello wykonywania obejmuje planowany tryb failover toohello dodatkowej bazy danych. Hello planowany tryb failover zapewnia, że hello głównej i pomocniczej bazy danych hello pozostają zsynchronizowane podczas przełączania ról hello. W odróżnieniu od hello nieplanowanego trybu failover, ta operacja nie powoduje utraty danych, więc hello Przechodzenie do szczegółów mogą być wykonywane w środowisku produkcyjnym hello.

#### <a name="outage-simulation"></a>Symulacji awarii
toosimulate hello awarii, można wyłączyć aplikacji sieci web hello lub maszyny wirtualnej podłączone toohello w bazie danych. W efekcie hello połączeniami dla klientów sieci web hello.

#### <a name="recovery"></a>Odzyskiwanie
* Upewnij się, że konfiguracja aplikacji hello w hello DR region punktów toohello była dodatkowej która staje się hello pełni dostępny nową podstawową.
* Wykonaj [planowanego trybu failover](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) toomake hello pomocniczej bazy danych nowego podstawowego
* Wykonaj hello [skonfigurować bazę danych po odzyskaniu](sql-database-disaster-recovery.md) przewodnik toocomplete hello odzyskiwania.

#### <a name="validation"></a>Walidacja
* Zakończenie hello Przechodzenie do szczegółów weryfikując aplikacji hello integralności post odzyskiwania (w tym parametry połączenia, logowania, podstawowych funkcji testowania lub innych operacji sprawdzania poprawności część procedur signoffs standardowej aplikacji).

## <a name="next-steps"></a>Następne kroki
* toolearn o scenariuszach ciągłości biznesowej, zobacz [ciągłości scenariuszy](sql-database-business-continuity.md)
* toolearn o bazy danych SQL Azure automatycznego tworzenia kopii zapasowych, zobacz [bazy danych SQL automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md)
* toolearn o za pomocą kopie zapasowe automatycznego odzyskiwania, zobacz [przywrócić bazę danych z kopii zapasowych hello inicjowane przez usługę](sql-database-recovery-using-backups.md)
* toolearn o szybsze opcje odzyskiwania, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md)  
