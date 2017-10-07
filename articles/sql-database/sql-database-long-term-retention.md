---
title: kopie zapasowe bazy danych SQL Azure aaaStore dla zapasowej lat too10 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak baza danych SQL Azure obsługuje przechowywania kopii zapasowych na potrzeby się too10 lata."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a>Przechowywanie kopii zapasowych bazy danych SQL Azure dla się too10 lat.
Wiele aplikacji ma przepisów prawnych, zgodności lub innych firm celów, które wymagają kopii zapasowych bazy danych tooretain poza hello 7 35 dni udostępniane przez usługi Azure SQL Database [automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md). Dzięki funkcji hello długoterminowego przechowywania kopii zapasowych, można przechowywać kopie zapasowe bazy danych SQL w magazynie usług odzyskiwania Azure dla zapasowej lat too10. Można przechowywać się too1, 000 baz danych na magazynie. Następnie można wybrać jakiejkolwiek kopii zapasowej w toorestore magazynu hello go jako nową bazę danych.

> [!IMPORTANT]
> Długoterminowego przechowywania kopii zapasowych jest obecnie w wersji zapoznawczej i jest dostępna w następujących regionach hello: Australia Wschodnia, Australia Południowo-Wschodnia, Brazylia Południowa, środkowe stany USA, Azja Wschodnia, wschodnie stany USA, wschodnie stany USA 2, Indie środkowe, Indie Południowe, Japonia Wschodnia, Japonia Zachodnia, północno-środkowe stany, Północna Europa, Południowej środkowe stany USA, Azja południowo-wschodnia, Europa Zachodnia i zachodnie stany USA
>

> [!NOTE]
> Można włączyć zapasową baz danych too200 na magazynu w okresie 24-godzinnym. Zalecane jest użycie oddzielnych magazynu dla każdego serwera toominimize hello skutków ten limit. 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a>Jak działa długoterminowego przechowywania kopii zapasowych bazy danych SQL

Z długoterminowego przechowywania kopii zapasowych można skojarzyć serwer bazy danych SQL z magazynu usług odzyskiwania Azure. 

* Należy utworzyć magazyn hello w hello tej samej subskrypcji platformy Azure, utworzony hello programu SQL server i w hello sam geograficzne regionu i grupie zasobów. 
* Następnie skonfiguruj zasady przechowywania dla dowolnej bazy danych. Hello zasad powoduje, że hello co tydzień pełną bazy danych kopii zapasowych toobe skopiowane toohello magazyn usług odzyskiwania i przechowywane przez okres przechowywania określony hello (up too10 lat). 
* Następnie można przywrócić hello bazy danych z dowolnego z tych kopii zapasowych tooa nową bazę danych w dowolnego serwera w hello subskrypcji. Magazyn Azure tworzy kopię z istniejących kopii zapasowych i hello kopiowania nie ma wpływu wydajności na powitania istniejącej bazy danych.

> [!TIP]
> Aby tooguide instrukcje, zobacz [Konfigurowanie i przywrócenie z długoterminowego przechowywania kopii zapasowych bazy danych SQL Azure](sql-database-long-term-backup-retention-configure.md).

## <a name="enable-long-term-backup-retention"></a>Włącz długoterminowego przechowywania kopii zapasowych

tooconfigure długoterminowego przechowywania kopii zapasowych bazy danych:

1. Tworzenie magazynu usług odzyskiwania Azure w hello tego samego regionu, subskrypcji i zasobu grupy jako serwer bazy danych SQL. 
2. Zarejestruj powitania serwera toohello magazynu.
3. Tworzenie zasad ochrony usług odzyskiwania Azure.
4. Zastosuj hello ochrony zasad toohello baz danych, które wymagają długoterminowego przechowywania kopii zapasowych.

tooconfigure, zarządzać i Przywróć bazę danych z długoterminowego przechowywania kopii zapasowych automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure, wykonaj jedną z następujących hello:

* Przy użyciu hello portalu Azure: kliknij **długoterminowego przechowywania kopii zapasowych**, wybierz bazę danych, a następnie kliknij przycisk **Konfiguruj**. 

   ![Wybierz bazę danych do długoterminowego przechowywania kopii zapasowych](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* Przy użyciu programu PowerShell: Przejdź zbyt[Konfigurowanie i przywrócenie z długoterminowego przechowywania kopii zapasowych bazy danych SQL Azure](sql-database-long-term-backup-retention-configure.md).

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a>Przywracanie bazy danych przechowywanym hello długoterminowego przechowywania kopii zapasowych funkcji

toorecover z kopii zapasowej długoterminowego przechowywania kopii zapasowych:

1. Magazyn hello listy przechowywania hello kopii zapasowej.
2. Kontener hello listy jest mapowanych tooyour serwera logicznego.
3. Listy hello źródła danych w ramach hello magazynu, który jest mapowanych tooyour bazy danych.
4. Punkty odzyskiwania hello listy, które są dostępne toorestore.
5. Przywracanie bazy danych hello z serwera docelowego toohello punktu odzyskiwania hello w ramach subskrypcji.

tooconfigure, zarządzać i Przywróć bazę danych z długoterminowego przechowywania kopii zapasowych automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure, wykonaj jedną z następujących hello:

* Przy użyciu hello portalu Azure: Przejdź zbyt[Zarządzaj długoterminowego przechowywania kopii zapasowych użyciu hello portalu Azure](sql-database-long-term-backup-retention-configure.md). 

* Przy użyciu programu PowerShell: Przejdź zbyt[Zarządzanie długoterminowego przechowywania kopii zapasowych przy użyciu programu PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="get-pricing-for-long-term-backup-retention"></a>Pobierz ceny dla długoterminowego przechowywania kopii zapasowych

Długoterminowego przechowywania kopii zapasowych bazy danych SQL jest rozliczana zgodnie z toohello [usługi kopii zapasowej Azure cennik stawki](https://azure.microsoft.com/pricing/details/backup/).

Serwer bazy danych SQL powitania po zarejestrowanych toohello magazynu są naliczane opłaty za hello całkowita ilość miejsca, który jest używany przez cotygodniowe kopie zapasowe hello przechowywane w magazynie hello.

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a>Wyświetl dostępne kopie zapasowe, które są przechowywane w długoterminowego przechowywania kopii zapasowych

tooconfigure, zarządzać i Przywróć bazę danych z długoterminowego przechowywania kopii zapasowych automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure przy użyciu hello portalu Azure, wykonaj jedną z następujących hello:

* Przy użyciu hello portalu Azure: Przejdź zbyt[Zarządzaj długoterminowego przechowywania kopii zapasowych użyciu hello portalu Azure](sql-database-long-term-backup-retention-configure.md). 

* Przy użyciu programu PowerShell: Przejdź zbyt[Zarządzanie długoterminowego przechowywania kopii zapasowych przy użyciu programu PowerShell](sql-database-long-term-backup-retention-configure.md).

## <a name="disable-long-term-retention"></a>Wyłącz długoterminowego przechowywania

usługi odzyskiwania Hello automatycznie obsługuje oczyszczania hello oparte na powitania podane zasady przechowywania kopii zapasowych. 

toostop wysyłania hello kopii zapasowych dla określonej bazy danych magazynu toohello, Usuń hello zasad przechowywania dla tej bazy danych.
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> nie dotyczy to Hello kopii zapasowych, które są już w magazynie hello. Są one automatycznie usuwane przez hello usługi odzyskiwania po wygaśnięciu okresu przechowywania.

## <a name="long-term-backup-retention-faq"></a>Długoterminowego przechowywania kopii zapasowych — często zadawane pytania

**Można ręcznie usunąć z określonych kopii zapasowych w magazynie hello?**

Nie można obecnie. Magazyn Hello automatycznie oczyszcza kopii zapasowych, po zakończeniu okresu przechowywania hello.

**Można zarejestrować Mój serwer toostore kopii zapasowych toomore niż jeden Magazyn?**

Nie, obecnie można przechowywać kopie zapasowe tooonly jeden magazyn naraz.

**W ramach różnych subskrypcji może mieć magazyn i serwera?**

Nie, obecnie hello magazynu i serwer muszą być w hello tej samej subskrypcji i grupie zasobów.

**Można użyć magazynu, który został utworzony w regionie, który jest inny niż region Mój serwer?**

Nie, hello magazynu i serwer muszą być w hello tego samego regionu toominimize skopiuj czasu i zapobiec zmianom ruchu.

**Jak wiele baz danych można przechowywać w jednym magazynie?**

Obecnie firma Microsoft obsługuje konto too1, 000 baz danych na magazynie. 

**Jak wiele magazynów można utworzyć na subskrypcję?**

Możesz utworzyć zapasową magazynów too25 na subskrypcję.

**Jak wiele baz danych można skonfigurować na dzień na magazyn?**

Można skonfigurować 200 bazy danych dziennie na magazynie.

**Długoterminowego przechowywania kopii zapasowych działa z pul elastycznych?**

Tak. Wszystkie bazy danych w puli hello można skonfigurować za pomocą zasad przechowywania hello.

**Można wybrać hello czas, o której została utworzona kopia zapasowa hello?**

Nie, baza danych SQL steruje hello harmonogram tworzenia kopii zapasowych toominimize hello wpływ na wydajność w bazach danych.

**Masz przezroczystego szyfrowania danych włączone dla bazy danych. Można jej używać z magazynem hello?** 

Tak, przezroczystego szyfrowania danych jest obsługiwane. Można przywrócić hello bazy danych z magazynu hello, nawet jeśli hello oryginalnej bazy danych już nie istnieje.

**Co się stanie w przypadku kopii zapasowej hello w magazynie hello Jeśli Moja subskrypcja jest zawieszona?** 

Jeśli subskrypcja jest zawieszona, firma Microsoft przechowywała hello istniejących baz danych i tworzenie kopii zapasowych. Nowe kopie zapasowe nie są toohello skopiowanych magazynu. Po aktywowaniu hello subskrypcji usługi hello wznawia kopiowanie magazynu toohello kopii zapasowych. Magazyn staje się dostępny toohello operacje przywracania przy użyciu kopii zapasowych hello, które zostały skopiowane przed hello subskrypcja została zawieszona. 

**Można uzyskać dostępu do plików kopii zapasowej bazy danych SQL toohello, można pobrać lub je przywrócić toohello programu SQL server?**

Nie, nie jest obecnie.

**Jest to możliwe toohave wielu harmonogramów (codziennie, co tydzień, co miesiąc, co rok) w ramach zasad przechowywania SQL.**

Nie, wielu harmonogramów są obecnie dostępne tylko dla kopii zapasowych maszyn wirtualnych.

**Co zrobić, jeśli skonfigurowanie długoterminowego przechowywania kopii zapasowych w bazie danych, która jest aktywna replikacja geograficzna dodatkowej bazy danych dla?**

Ponieważ firma Microsoft nie wykonuj kopie zapasowe replik, nie ma opcja długoterminowego przechowywania kopii zapasowych z dodatkowej bazy danych. Jednak ważne jest dla użytkowników tooset się długoterminowego przechowywania kopii zapasowej w pomocniczej bazie danych aktywna replikacja geograficzna tych powodów:
* Po przejściu w tryb failover wykonywany i bazy danych hello staje się podstawowej bazy danych, traktujemy pełnej kopii zapasowej, który jest toovault przekazane.
* Nie istnieje bez dodatkowych kosztów toohello odbiorcy do definiowania długoterminowego przechowywania kopii zapasowej w pomocniczej bazie danych.

## <a name="next-steps"></a>Następne kroki
Ponieważ kopie zapasowe bazy danych ochronę danych przed przypadkowym uszkodzenia lub usunięcia, są one integralną część wszelkie ciągłość prowadzenia działalności biznesowej i strategii odzyskiwania po awarii. toolearn około hello innych rozwiązań ciągłość prowadzenia działalności biznesowej bazy danych SQL, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md).
