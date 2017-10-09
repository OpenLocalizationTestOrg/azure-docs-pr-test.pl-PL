---
title: aaaRestore bazy danych Azure SQL z kopii zapasowej | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat punktu w czasie przywracania, umożliwiający tooroll kopii bazy danych SQL Azure tooa poprzedniego punktu w czasie (w górę too35 dni)."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: monicar
ms.assetid: fd1d334d-a035-4a55-9446-d1cf750d9cf7
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.openlocfilehash: 84ecc306a2072445c10dbf1e9d7cf3d1b43860cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="recover-an-azure-sql-database-using-automated-database-backups"></a>Odzyskiwanie bazy danych Azure SQL przy użyciu kopii zapasowych bazy danych automatycznych
Baza danych SQL oferuje następujące opcje bazy danych odzyskiwania przy użyciu [automatyczne kopie zapasowe bazy danych](sql-database-automated-backups.md) i [kopie zapasowe w przechowywania długoterminowego](sql-database-long-term-retention.md). Można przywrócić z kopii zapasowej bazy danych, aby:

* Nową bazę danych na powitania odzyskana na tym samym serwerze logicznym tooa określonego punktu w czasie w okresie przechowywania hello. 
* A bazy danych na powitania sam serwer logiczny odzyskać usuniętej bazy danych podczas usuwania toohello.
* Nową bazę danych na dowolnym serwerze logicznym w dowolnym regionie odzyskać punktu toohello hello najnowszych codziennych kopii zapasowych w magazynie obiektów blob z replikacją geograficzną (RA-GRS).

> [!IMPORTANT]
> Nie można zastąpić istniejącą bazę danych podczas przywracania.
>

Można również użyć [automatyczne kopie zapasowe bazy danych](sql-database-automated-backups.md) toocreate [kopiowanie bazy danych](sql-database-copy.md) na dowolnym serwerze logicznym w dowolnym regionie. 

## <a name="recovery-time"></a>Czas odzyskiwania
Witaj toorestore czas odzyskiwania, które bazy danych przy użyciu kopii zapasowych automatycznych bazy danych jest w pełni funkcjonalne przez kilka czynników: 

* rozmiar Hello hello bazy danych
* poziom wydajności Hello hello bazy danych
* Liczba Hello zaangażowany dzienników transakcji
* punkt przywracania toohello toorecover odtwarzany Hello ilość działania, które należy toobe
* przepustowość sieci Hello przywracania hello jest tooa inny region 
* Liczba Hello przywracania równoczesnych żądań przetwarzanych w region docelowy hello. 
  
  Dla bardzo dużych i/lub aktywnej bazy danych Przywróć hello może potrwać kilka godzin. Jeśli istnieje długimi awaria w regionie, jest to możliwe, że ma dużą liczbę żądań geograficzne przetwarzanych przez innych regionów. Gdy istnieje wiele żądań, czasu odzyskiwania hello może zwiększyć dla baz danych w tym regionie. Pełne przywracanie większości baz danych w ciągu 12 godzin.
  
Nie ma wbudowanej funkcji toodo zbiorczego przywracanie. Witaj [bazy danych SQL Azure: pełne odzyskiwanie serwera](https://gallery.technet.microsoft.com/Azure-SQL-Database-Full-82941666) skrypt jest przykładem jedną z metod wykonasz to zadanie.

> [!IMPORTANT]
> toorecover przy użyciu automatycznego tworzenia kopii zapasowych, należy być członkiem roli współautora serwera SQL hello w subskrypcji hello lub być właścicielem subskrypcji hello. Można odzyskać za pomocą hello portalu Azure, programu PowerShell lub hello interfejsu API REST. Nie można używać języka Transact-SQL. 
> 

## <a name="point-in-time-restore"></a>W momencie przywracania

Można przywrócić istniejącej bazy danych tooan wcześniej punktu w czasie jako nową bazę danych na powitania sam przy użyciu serwera logicznego hello portalu Azure, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), lub hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Aby uzyskać przykładowy skrypt programu PowerShell przedstawiający tooperform w momencie przywracania bazy danych, zobacz temat [Przywróć bazę danych SQL przy użyciu programu PowerShell](scripts/sql-database-restore-database-powershell.md).
>

Hello bazy danych może być przywrócona tooany warstwy usług lub wydajności i jako pojedynczej bazy danych lub w puli elastycznej. Upewnij się, ma wystarczające zasoby na serwerze logicznym hello lub w toowhich puli elastycznej hello są przywracane hello bazy danych. Po wykonaniu tych czynności hello przywrócona baza danych jest bazą danych normalne, pełni dostępny online. Witaj przywrócić bazy danych jest pobierana stawkami normalnym na podstawie poziomu wydajności i warstwę usług. Nie wiąże się z opłatami do czasu ukończenia hello Przywracanie bazy danych.

Zazwyczaj przywrócić tooan bazy danych punktu wcześniej na potrzeby odzyskiwania. Gdy w ten sposób można traktować hello przywróconej bazy danych jako zamiennik hello oryginalnej bazy danych lub użyj go tooretrieve danych z, a następnie zaktualizuj hello oryginalnej bazy danych. 

* ***Baza danych zamiany:*** Jeśli hello przywrócić bazy danych służy jako serwer zamienny dla hello oryginalnej bazy danych, należy sprawdzić poziom wydajności hello i/lub warstwy usług są odpowiednie i skalować hello bazy danych, jeśli to konieczne. Można zmienić nazwy hello oryginalnej bazy danych, a następnie nadaj hello przywrócić bazy danych hello oryginalna nazwa za pomocą polecenia ALTER DATABASE hello w T-SQL. 
* ***Odzyskiwanie danych:*** Jeśli planujesz tooretrieve danych z hello przywrócić bazy danych toorecover z błędu użytkownika lub aplikacji, należy toowrite i wykonać hello niezbędnych danych odzyskiwania skrypty tooextract danych z hello przywrócić toohello bazy danych oryginalnej bazy danych. Chociaż hello operacji przywracania może zająć toocomplete długi czas, nie jest widoczna hello listy baz danych w trakcie procesu przywracania hello hello Przywracanie bazy danych. Po usunięciu hello bazy danych podczas przywracania hello hello operacji przywracania została anulowana i nie są naliczane opłaty hello bazy danych, która nie została ukończona hello przywracania. 

### <a name="azure-portal"></a>Azure Portal

Witaj toorecover tooa punktu w czasie przy użyciu portalu Azure, otwórz hello stron dla bazy danych i kliknij przycisk **przywrócić** na powitania narzędzi.

![punkt w czasie przywracania](./media/sql-database-recovery-using-backups/point-in-time-recovery.png)

## <a name="deleted-database-restore"></a>Przywracanie usuniętej bazy danych
Możesz przywrócić czas usuwania toohello usuniętej bazy danych usuniętej bazy danych na powitania przy użyciu tego samego serwera logicznego hello portalu Azure, [PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/restore-azurermsqldatabase), lub hello [REST (createMode = przywracanie)](https://msdn.microsoft.com/library/azure/mt163685.aspx). 

> [!TIP]
> Dla przykładu środowiska PowerShell skryptu przedstawiający toorestore usuniętej bazy danych, zobacz temat [Przywróć bazę danych SQL przy użyciu programu PowerShell](scripts/sql-database-restore-database-powershell.md).
>

> [!IMPORTANT]
> W przypadku usunięcia wystąpienia serwera bazy danych SQL Azure, jej baz danych, również zostaną usunięte i nie może zostać odzyskany. Obecnie nie jest obsługiwane dla przywracanie usuniętych serwera.
> 

### <a name="azure-portal"></a>Azure Portal

toorecover usuniętej bazy danych podczas jego [okres przechowywania](sql-database-service-tiers.md) przy użyciu hello portalu Azure, otwórz hello strony serwera i w obszarze operacji hello, kliknij przycisk **usunięte bazy danych**.

![usunięte bazy danych — Przywracanie-1](./media/sql-database-recovery-using-backups/deleted-database-restore-1.png)


![usunięte bazy danych — Przywracanie-2](./media/sql-database-recovery-using-backups/deleted-database-restore-2.png)

## <a name="geo-restore"></a>Przywracanie geograficzne
Można przywrócić bazy danych SQL na dowolnym serwerze w dowolnym regionie Azure z hello najnowszych replikacją geograficzną pełne i różnicowe kopie zapasowe. Geograficzne używa geograficznie nadmiarowej kopii zapasowej jako źródła i mogą być używane toorecover bazy danych nawet jeśli hello bazy danych lub centrum danych jest niedostępny z powodu awarii tooan. 

Geograficzne jest hello domyślna opcja odzyskiwania, gdy baza danych jest niedostępna z powodu zdarzenia w regionie hello, w którym hostowana jest baza danych hello. Jeśli na dużą skalę zdarzenia w wynikach regionu w niedostępności aplikacji bazy danych, można przywrócić bazę danych z serwera tooa kopii zapasowych z replikacją geograficzną hello w innym regionie. Nastąpi opóźnienie między po różnicowej kopii zapasowej jest zajęty i gdy jest replikacją geograficzną tooan Azure blob w innym regionie. To opóźnienie może wynosić zapasowej godzinę tooan tak, jeśli awarii, mogą być zapasowej utraty danych tooone godzinę. Witaj następującej ilustracji zawiera przywracania bazy danych hello z hello ostatniej dostępnej kopii zapasowej w innym regionie.

![geograficzne](./media/sql-database-geo-restore/geo-restore-2.png)

> [!TIP]
> Dla przykładu środowiska PowerShell skryptu przedstawiający tooperform przywracania geograficznie, zobacz temat [Przywróć bazę danych SQL przy użyciu programu PowerShell](scripts/sql-database-restore-database-powershell.md).
> 

W momencie przywracania na dodatkowej geograficzna nie jest obecnie obsługiwane. W momencie przywracania jest możliwe tylko dla podstawowej bazy danych. Aby uzyskać szczegółowe informacje o korzystaniu z przywracaniem geograficznym toorecover po awarii, zobacz [odzyskiwanie po awarii](sql-database-disaster-recovery.md).

> [!IMPORTANT]
> Odzyskiwanie z kopii zapasowych jest hello najbardziej podstawowa z powitania po awarii hello rozwiązań odzyskiwania dostępnych w bazie danych SQL z najdłuższym RPO i szacowania czasu odzyskiwania (Wstaw). Rozwiązania z wykorzystaniem podstawowych baz danych geograficzne jest często rozsądne rozwiązanie odzyskiwania po awarii z Wstaw 12 godzin. Dla rozwiązania z wykorzystaniem większych standardowa lub Premium baz danych, które wymagają krótsze czasy odzyskiwania, należy rozważyć użycie [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md). Aktywna replikacja geograficzna oferuje znacznie niższe RPO i Wstaw, ponieważ wymaga tylko możesz zainicjować dodatkowej tooa stale replikowane trybu failover. Aby uzyskać więcej informacji na opcji contiuity firm, zobacz [over ciągłość prowadzenia działalności biznesowej](sql-database-business-continuity.md).
> 

### <a name="azure-portal"></a>Azure Portal

toogeo przywracania, a bazy danych podczas jego [okres przechowywania](sql-database-service-tiers.md) przy użyciu hello portalu Azure, otwórz stronę baz danych SQL hello, a następnie kliknij przycisk **Dodaj**. W hello **wybierz źródło** pole tekstowe, wybierz **kopii zapasowej**. Określ hello kopii zapasowej, z których tooperform hello odzyskiwania w regionie hello i na serwerze hello wybranych przez użytkownika. 

## <a name="programmatically-performing-recovery-using-automated-backups"></a>Programowo odzyskiwanie przy użyciu automatycznego tworzenia kopii zapasowych
Jak już wspomniano oprócz toohello portalu Azure, odzyskiwanie bazy danych można wykonać programowo przy użyciu programu Azure PowerShell lub hello interfejsu API REST. następujące tabele Hello opisano hello zestaw poleceń, które są dostępne.

### <a name="powershell"></a>PowerShell
| Polecenie cmdlet | Opis |
| --- | --- |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase) |Pobiera jeden lub więcej baz danych. |
| [Get-AzureRMSqlDeletedDatabaseBackup](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | Pobiera usuniętej bazy danych, które można przywrócić. |
| [Get-AzureRmSqlDatabaseGeoBackup](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) |Pobiera geograficznie nadmiarowego kopii zapasowej bazy danych. |
| [Przywracanie AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) |Przywraca bazę danych SQL. |
|  | |

### <a name="rest-api"></a>Interfejs API REST
| Interfejs API | Opis |
| --- | --- |
| [REST (createMode = odzyskiwania)](https://msdn.microsoft.com/library/azure/mt163685.aspx) |Przywraca bazę danych |
| [GET, Utwórz lub zaktualizuj stan bazy danych](https://msdn.microsoft.com/library/azure/mt643934.aspx) |Zwraca stan hello podczas operacji przywracania |
|  | |

## <a name="summary"></a>Podsumowanie
Automatyczne kopie zapasowe chronić baz danych użytkownika i błędy aplikacji, usuwać przypadkowemu bazy danych i długimi przestojami. Ta funkcja wbudowana jest dostępna dla wszystkich warstw usług i poziomy wydajności. 

## <a name="next-steps"></a>Następne kroki
* Omówienie ciągłości działalności biznesowej i scenariuszy, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md)
* toolearn o bazy danych SQL Azure automatycznego tworzenia kopii zapasowych, zobacz [bazy danych SQL automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md)
* toolearn dotyczące długoterminowego przechowywania kopii zapasowych, zobacz [długoterminowego przechowywania kopii zapasowych](sql-database-long-term-retention.md)
* tooconfigure, zarządzania i przywrócenie z długoterminowego przechowywania automatycznych kopii zapasowych w magazynie usług odzyskiwania Azure przy użyciu hello Azure portalu, zobacz [Konfigurowanie i używanie długoterminowej kopii zapasowej przechowywania](sql-database-long-term-backup-retention-configure.md). 
* toolearn o szybsze opcje odzyskiwania, zobacz [aktywna replikacja geograficzna](sql-database-geo-replication-overview.md)  
