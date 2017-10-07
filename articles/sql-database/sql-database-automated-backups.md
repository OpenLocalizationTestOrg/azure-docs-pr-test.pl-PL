---
title: aaaAzure bazy danych SQL automatyczne, geograficznie nadmiarowego kopie zapasowe | Dokumentacja firmy Microsoft
description: "Baza danych SQL automatycznie tworzy kopię zapasową lokalnej bazy danych co kilka minut i korzysta z magazynu geograficznie nadmiarowego Azure dostęp do odczytu dla nadmiarowość geograficzna."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 3ee3d49d-16fa-47cf-a3ab-7b22aa491a8d
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 8aff5356e8142707dd7cd2533a4aa5ea8fec866d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-automatic-sql-database-backups"></a>Więcej informacji na temat automatycznego tworzenia kopii zapasowej bazy danych SQL

Baza danych SQL automatycznie tworzy kopie zapasowe bazy danych i korzysta z magazynu geograficznie nadmiarowego Azure dostęp do odczytu (RA-GRS) tooprovide z nadmiarowość geograficzna. Te kopie zapasowe są tworzone automatycznie i bez dodatkowych opłat. Nie trzeba toodo cokolwiek toomake ich się tak stać. Kopie zapasowe bazy danych są integralną część każdej strategii odzyskiwania biznesowych, jak ciągłości i odzyskiwaniem po awarii, ponieważ ich ochronę danych przed przypadkowym uszkodzenia lub usunięcia. Jeśli kopie zapasowe tookeep własne kontenera magazynu można skonfigurować zasadę długoterminowego przechowywania kopii zapasowych. Aby uzyskać więcej informacji, zobacz [Długoterminowe przechowywanie](sql-database-long-term-retention.md).

## <a name="what-is-a-sql-database-backup"></a>Co to jest kopia zapasowa bazy danych SQL?

Toocreate technologii programu SQL Server korzysta z bazy danych SQL [pełne](https://msdn.microsoft.com/library/ms186289.aspx), [różnicowej](https://msdn.microsoft.com/library/ms175526.aspx), i [dziennika transakcji](https://msdn.microsoft.com/library/ms191429.aspx) kopii zapasowych. kopie zapasowe dziennika transakcji Hello nastąpić zazwyczaj co 5 – 10 minut z częstotliwością hello na podstawie poziomu wydajności hello i ilości aktywności bazy danych. Kopie zapasowe dziennika transakcji, o pełne i różnicowe kopie zapasowe, pozwalają toorestore bazy danych tooa określonego punktu w czasie toohello tym samym serwerze, który obsługuje bazę danych hello. Po przywróceniu bazy danych hello rysunki usługi limit które pełne, różnicowej i kopie zapasowe dziennika transakcji należy przywrócić toobe.


Te kopie zapasowe, można użyć:

* Przywracanie bazy danych tooa w momencie w okresie przechowywania hello. Ta operacja spowoduje utworzenie nowej bazy danych w hello tym samym serwerze co hello oryginalnej bazy danych.
* Przywróć razem toohello usuniętej bazy danych, gdy zostało ono usunięte lub dowolnym momencie w okresie przechowywania hello. Witaj usunięte bazy danych można przywrócić tylko w hello tym samym serwerze, na którym utworzono hello oryginalnej bazy danych.
* Przywróć region geograficzny tooanother bazy danych. Dzięki temu można toorecover z geograficzne po awarii, jeśli nie masz dostępu do serwera i bazy danych. Tworzy nową bazę danych w dowolnym istniejącego serwera, w dowolnym miejscu hello world. 
* Przywróć bazę danych z kopii zapasowej określonych przechowywane w magazynie usług odzyskiwania Azure. Dzięki temu można toorestore stara wersja hello bazy danych toosatisfy żądanie zgodności lub toorun starą wersję aplikacji hello. Zobacz [przechowywania długoterminowego](sql-database-long-term-retention.md).
* tooperform przywracania, zobacz [przywrócić bazę danych z kopii zapasowych](sql-database-recovery-using-backups.md).

> [!NOTE]
> W magazynie Azure określenie hello *replikacji* odnosi się toocopying plików z jednej lokalizacji tooanother. SQL do *replikacji bazy danych* odwołuje się tookeeping toomultiple pomocniczej bazy danych synchronizowane z podstawowej bazy danych. 
> 

## <a name="how-much-backup-storage-is-included-at-no-cost"></a>Ile miejsca do magazynowania kopii zapasowej wchodzi bezpłatnie?
Baza danych SQL umożliwia % too200 maksymalną elastycznie bazy danych magazynu za pomocą magazynu kopii zapasowej bez ponoszenia dodatkowych kosztów. Na przykład jeśli wystąpienie standardowe bazy danych o rozmiarze DB elastycznie 250 GB, masz 500 GB miejsca do magazynowania kopii zapasowej bez dodatkowych opłat. Jeśli bazy danych przekroczy hello podane magazynu kopii zapasowej, można wybrać okres przechowywania hello tooreduce, kontaktując się z pomocą techniczną platformy Azure. Innym rozwiązaniem jest toopay magazynu bardzo kopii zapasowej, która jest rozliczany według hello standardowe stawki dostęp do odczytu geograficznie magazynu geograficznie nadmiarowego (RA-GRS). 

## <a name="how-often-do-backups-happen"></a>Jak często stanie kopie zapasowe?
Kopie zapasowe pełnej bazy danych są wykonywane co tydzień, kopie zapasowe różnicowej bazy danych są zazwyczaj wykonywane co kilka godzin, a dziennik transakcji, których kopie zapasowe są zazwyczaj wykonywane co 5 – 10 minut. Pierwsza pełna kopia zapasowa Hello jest zaplanowane, natychmiast po utworzeniu bazy danych. Zazwyczaj wykonuje w ciągu 30 minut, ale może to trwać dłużej baza danych hello jest znaczne rozmiary. Na przykład hello początkowa kopia zapasowa może trwać dłużej w przywróconej bazy danych lub kopii bazy danych. Po hello pierwsza pełna kopia zapasowa wszystkie dodatkowe kopie zapasowe są automatycznie zaplanowane i zarządzane w trybie dyskretnym w tle hello. dokładny czas Hello wszystkie kopie zapasowe bazy danych jest określana przez hello usługi baza danych SQL jako jego hello ogólną obciążenia systemu. 

Replikacja geograficzna Hello magazynu kopii zapasowych występuje na podstawie harmonogramu replikacji usługi Azure Storage hello.

## <a name="how-long-do-you-keep-my-backups"></a>Jak długo zachować kopiach zapasowych?
Każdej kopii zapasowej bazy danych SQL ma okres przechowywania, która jest oparta na powitania [warstwy usług](sql-database-service-tiers.md) hello bazy danych. Witaj okres przechowywania bazy danych w:


* Warstwy usług podstawowa wynosi 7 dni.
* Standardowa usługa warstwa jest 35 dni.
* Warstwy usług Premium jest 35 dni.

Jeśli obniżyć bazy danych z hello Standard lub Premium usługi warstw tooBasic, hello kopie zapasowe są zapisywane na siedem dni. Wszystkie istniejące kopie zapasowe starsze niż 7 dni nie są już dostępne. 

W przypadku uaktualniania bazy danych z tooStandard warstwy podstawowej usługi hello lub Premium bazy danych SQL przechowuje istniejących kopii zapasowych aż do ich 35 dni temu. Zapewnia nowe kopie zapasowe w miarę ich występowania 35 dni.

W przypadku usunięcia bazy danych, bazy danych SQL przechowuje kopie zapasowe hello w hello sam sposób jak to by się dla bazy danych online. Na przykład załóżmy, że należy usunąć podstawowa baza danych ma okres przechowywania wynosi siedem dni. Kopię zapasową, która jest czterech dni są zapisywane dla trzech dni.

> [!IMPORTANT]
> Jeśli usuniesz hello Azure SQL server hostującym bazy danych SQL, wszystkich baz danych należących do serwera toohello również zostaną usunięte i nie można odzyskać. Nie można przywrócić usuniętego serwera.
> 

## <a name="how-tooextend-hello-backup-retention-period"></a>Jak tooextend hello kopii zapasowej okres przechowywania?
Jeśli aplikacja wymaga hello kopie zapasowe są dostępne do czasu można rozszerzyć okres przechowywania wbudowanych hello konfigurując hello długoterminowego przechowywania kopii zapasowych zasady dla pojedynczych baz danych (zasada od lewej do prawej). Dzięki temu okres przechowywania wbudowane it hello tooextend wieloletnim too10 tooup 35 dni. Aby uzyskać więcej informacji, zobacz [Długoterminowe przechowywanie](sql-database-long-term-retention.md).

Po dodaniu powitania od lewej do prawej zasad tooa bazy danych przy użyciu portalu Azure lub interfejsu API hello co tydzień pełne kopie zapasowe bazy danych będą automatycznie skopiowane tooyour właścicielem magazynu usługi Kopia zapasowa Azure. Jeśli baza danych jest szyfrowany przy tworzenia kopii zapasowych funkcji TDE hello są automatycznie szyfrowane, gdy.  Hello magazynu usług automatycznie usunie kopie zapasowe wygasłe na podstawie ich sygnatury czasowej oraz hello zasad od lewej do prawej.  Dlatego nie zostanie muszą harmonogram tworzenia kopii zapasowych hello toomanage lub martwić o oczyszczania hello hello starych plików. Hello przywracania interfejs API obsługuje magazyn kopii zapasowych przechowywanych w hello tak długo, jak magazyn hello jest hello tej samej subskrypcji co baza danych SQL. Możesz użyć hello portalu Azure lub programu PowerShell tooaccess te kopie zapasowe.

> [!TIP]
> Aby tooguide instrukcje, zobacz [Konfigurowanie i przywrócenie z długoterminowego przechowywania kopii zapasowych bazy danych SQL Azure](sql-database-long-term-backup-retention-configure.md)
>

## <a name="are-backups-encrypted"></a>Kopie zapasowe są szyfrowane?

Po włączeniu funkcji TDE dla bazy danych Azure SQL kopii zapasowych również są szyfrowane. Wszystkie nowe bazy danych Azure SQL korzystają z funkcji TDE domyślnie włączone. Aby uzyskać więcej informacji o funkcji TDE, zobacz [przezroczystego szyfrowania danych z bazy danych SQL Azure](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database).

## <a name="next-steps"></a>Następne kroki

- Kopie zapasowe bazy danych są integralną część każdej strategii odzyskiwania biznesowych, jak ciągłości i odzyskiwaniem po awarii, ponieważ ich ochronę danych przed przypadkowym uszkodzenia lub usunięcia. toolearn około hello innych rozwiązań ciągłości biznesowej bazy danych SQL Azure, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).
- toorestore tooa punktu w czasie przy użyciu hello portalu Azure, zobacz [bazy danych tooa punktu przywracania w czasie przy użyciu portalu Azure hello](sql-database-recovery-using-backups.md).
- toorestore tooa punktu w czasie przy użyciu programu PowerShell, zobacz [bazy danych tooa punktu przywracania w czasie przy użyciu programu PowerShell](scripts/sql-database-restore-database-powershell.md).
- tooconfigure, zarządzania i przywrócenie z długoterminowego przechowywania automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure przy użyciu hello Azure portalu, zobacz [Zarządzaj długoterminowego przechowywania kopii zapasowych użyciu hello portalu Azure](sql-database-long-term-backup-retention-configure.md).
- tooconfigure, zarządzać i Przywróć z długoterminowego przechowywania automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure przy użyciu programu PowerShell, zobacz [Zarządzanie długoterminowego przechowywania kopii zapasowych przy użyciu programu PowerShell](sql-database-long-term-backup-retention-configure.md).
