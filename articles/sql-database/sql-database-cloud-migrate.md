---
title: aaaSQL serwera bazy danych migracji tooAzure bazy danych SQL | Dokumentacja firmy Microsoft
description: "Więcej informacji o migracji tooAzure bazy danych SQL Database w chmurze hello programu SQL Server. Użyć bazy danych migracji narzędzia tootest zgodności wcześniejsze toodatabase migracji."
keywords: "migracja bazy danych,migracja bazy danych programu sql server,narzędzia migracji bazy danych,migracja bazy danych,migracja bazy danych sql"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 9cf09000-87fc-4589-8543-a89175151bc2
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-migrate
ms.date: 02/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a5e879404dd2da1dd5254a6134e3ee1517648db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-database-migration-toosql-database-in-hello-cloud"></a>TooSQL migracji bazy danych programu SQL Server bazy danych w chmurze hello
W tym artykule opisano Witaj dwie podstawowe metody migracji programu SQL Server 2005 lub nowszego tooAzure bazy danych SQL Database. Witaj pierwsza metoda jest prostsza, ale wymaga niektóre, prawdopodobnie znacznie zmniejsza czas przestoju w trakcie migracji hello. Druga metoda Hello jest bardziej złożony, ale zasadniczo eliminuje przestoju podczas migracji hello.

W obu przypadkach należy tooensure tej bazy danych źródłowego hello jest zgodny z bazy danych SQL Azure przy użyciu hello [Asystenta migracji danych (DMA)](https://www.microsoft.com/download/details.aspx?id=53595). Zbliża się do bazy danych SQL V12 [funkcji parzystości](sql-database-features.md) z programem SQL Server, niż problemów powiązanych operacji tooserver poziomu i między bazami danych. Baz danych i aplikacji, które opierają się na [częściowo obsługiwane i nieobsługiwane funkcje](sql-database-transact-sql-information.md) muszą niektóre [reorganizacji toofix tych niezgodności](sql-database-cloud-migrate.md#resolving-database-migration-compatibility-issues) przed hello programu SQL Server można poddać migracji bazy danych.

> [!NOTE]
> toomigrate bazy danych z systemem innym niż SQL Server, w tym programu Microsoft Access, Sybase, MySQL, Oracle i bazy danych DB2 tooAzure bazy danych SQL, zobacz [Asystenta migracji programu SQL Server](https://blogs.msdn.microsoft.com/datamigration/2016/12/22/released-sql-server-migration-assistant-ssma-v7-2/).
> 

## <a name="method-1-migration-with-downtime-during-hello-migration"></a>Metoda 1: Migracji przestojów podczas migracji hello

 Tej metody należy użyć, jeżeli przestój jest dopuszczalny lub wykonywana jest testowa migracja produkcyjnej bazy danych do celów późniejszej migracji. Samouczek, zobacz [Migrowanie bazy danych programu SQL Server](sql-database-migrate-your-sql-server-database.md).

Witaj Poniższa lista zawiera ogólny przepływ pracy hello migracji bazy danych programu SQL Server za pomocą tej metody.

  ![Diagram migracji VSSSDT](./media/sql-database-cloud-migrate/azure-sql-migration-sql-db.png)

1. Oceny zgodności przy użyciu hello najnowszej wersji bazy danych hello [Asystenta migracji danych (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).
2. Przygotowanie wszelkich niezbędnych poprawek jako skryptów języka Transact-SQL.
3. Wykonaj kopię spójna transakcyjnie hello źródłowej bazy danych migracji - i upewnij się, nie dalszych zmian toohello źródłowej bazy danych (lub możesz ręcznie zastosować takie zmiany po ukończeniu migracji hello). Istnieje wiele metod tooquiesce bazę danych, z wyłączeniem toocreating łączności klienta [migawki bazy danych](https://msdn.microsoft.com/library/ms175876.aspx).
4. Wdróż kopii bazy danych toohello hello języka Transact-SQL skrypty tooapply hello poprawki.
5. [Eksportuj](sql-database-export.md) hello tooa kopii bazy danych. Pliku BACPAC plik na dysku lokalnym.
6. [Importuj](sql-database-import.md) hello. Pliku BACPAC pliku jako nowej bazy danych Azure SQL za pomocą jednej z kilku pliku BACPAC zaimportuj narzędzia, za pomocą SQLPackage.exe trwa hello zalecane narzędzie w celu uzyskania najlepszej wydajności.

### <a name="optimizing-data-transfer-performance-during-migration"></a>Optymalizowanie wydajności transferu danych podczas migracji 

Witaj, następujące listy zawiera zalecenia w celu uzyskania najlepszej wydajności podczas procesu importowania hello.

* Wybierz hello najwyższego poziomu usług i wydajności warstwy budżet zezwala na wydajność transferu hello toomaximize. Po zakończeniu migracji hello pieniędzy toosave można skalować w dół. 
* Minimalizowanie hello odległość między użytkownika. Pliku BACPAC plików i hello docelowym centrum danych.
* Wyłącz automatyczne statystyki na czas migracji.
* Partycjonuj tabele i indeksy.
* Usuń poindeksowane widoki i utwórz je ponownie po zakończeniu.
* Usuń bazę danych tooanother rzadko danych historycznych, a następnie przeprowadzić migrację tego danych historycznych tooa oddzielne bazy danych Azure SQL. Następnie będzie można wykonywać zapytania o te dane historyczne za pomocą [zapytań elastycznych](sql-database-elastic-query-overview.md).

### <a name="optimize-performance-after-hello-migration-completes"></a>Optymalizacja wydajności, po zakończeniu migracji hello

[Aktualizuj statystyki](https://msdn.microsoft.com/library/ms187348.aspx) z pełnego skanowania po zakończeniu migracji hello.

## <a name="method-2-use-transactional-replication"></a>Metoda 2. Użycie replikacji transakcyjnej

Gdy niedopuszczalna tooremove bazy danych SQL Server w środowisku produkcyjnym, podczas gdy jest wykonywana migracja hello, można użyć Replikacja transakcyjna programu SQL Server jako rozwiązania migracji. toouse tej metody hello źródłowej bazy danych musi spełniają hello [wymagania dotyczące replikacji transakcyjnej](https://msdn.microsoft.com/library/mt589530.aspx) i być zgodny z bazy danych SQL Azure. Informacje o replikacji SQL z funkcją AlwaysOn, zobacz [skonfigurować replikację dla zawsze włączonych grup dostępności (SQL Server)](/sql/database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server).

toouse tego rozwiązania, można skonfigurować bazy danych SQL Azure jako wystąpienie programu SQL Server toohello subskrybenta, że chcesz toomigrate. Witaj dystrybutora replikacji transakcyjnej synchronizuje dane z hello bazy danych toobe zsynchronizowane (hello wydawca) nowych transakcji nadal występuje. 

W przypadku replikacji transakcyjnej wszystkie zmiany tooyour danych lub schemat widoczne w Twojej bazy danych SQL Azure. Po zakończeniu synchronizacji hello i są gotowe toomigrate, Zmień parametry połączenia toopoint Twojej aplikacji hello ich tooyour bazy danych SQL Azure. Po replikacji transakcyjnej wstrzymanie wszelkie zmiany w lewo na źródłowej bazy danych i wszystkie aplikacje punkt tooAzure bazy danych, należy odinstalować replikacji transakcyjnej. Usługa Azure SQL Database stanie się Twoim systemem produkcyjnym.

 ![Diagram SeedCloudTR](./media/sql-database-cloud-migrate/SeedCloudTR.png)

> [!TIP]
> Umożliwia także toomigrate replikacji transakcyjnej podzbiór źródłowej bazy danych. publikacji Hello, aby replikować tooAzure bazy danych SQL mogą być tooa ograniczony podzestaw hello tabele w bazie danych hello replikowana. Dla każdej tabeli jest replikowany można ograniczyć hello danych tooa podzbiór wierszy hello i/lub podzbiór hello kolumn.
>

### <a name="migration-toosql-database-using-transaction-replication-workflow"></a>TooSQL migracji bazy danych przy użyciu przepływu transakcji replikacji

> [!IMPORTANT]
> Użyj hello najnowszej wersji programu SQL Server Management Studio tooremain synchronizowane z tooMicrosoft aktualizacji platformy Azure i bazy danych SQL. Starsze wersje programu SQL Server Management Studio nie mogą skonfigurować usługi SQL Database jako subskrybenta. [Zaktualizuj program SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 

1. Konfigurowanie dystrybucji
   -  [Przy użyciu programu SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_1)
   -  [Przy użyciu języka Transact-SQL](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_2)
2. Tworzenie publikacji
   -  [Przy użyciu programu SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_1)
   -  [Przy użyciu języka Transact-SQL](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_2)
3. Tworzenie subskrypcji
   -  [Przy użyciu programu SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_0)
   -  [Przy użyciu języka Transact-SQL](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_1)

### <a name="some-tips-and-differences-for-migrating-toosql-database"></a>Niektóre porady i różnice dotyczące migracji tooSQL bazy danych

1. Użycie dystrybutora lokalnego: 
   - Powoduje to negatywny wpływ na wydajność na powitania serwera. 
   - W przypadku nadmiernego wpływu na wydajność hello, można użyć innego serwera, ale dodaje złożoność zarządzania i administrowania.
2. Po wybraniu folderu migawek, upewnij się, że hello folderu wybranego jest wystarczająco duży toohold BCP każdej tabeli, która ma tooreplicate. 
3. Blokady tworzenia migawki hello skojarzone tabele do czasu ukończenia, więc odpowiednio zaplanować migawki. 
4. Usługa Azure SQL Database obsługuje wyłącznie subskrypcje wypychane. Można dodawać tylko subskrybenci z hello źródłowej bazy danych.

## <a name="resolving-database-migration-compatibility-issues"></a>Rozwiązywanie problemów ze zgodnością migracji bazy danych
Brak szerokiej gamy problemów ze zgodnością, które można napotkać, zależy od tego, hello wersji programu SQL Server hello źródłowej bazy danych i hello złożonością hello bazy danych, którego jest przeprowadzana migracja. Starsze wersje programu SQL Server mają więcej problemów ze zgodnością. Użyj następujących zasobów hello, oprócz tooa docelowe wyszukiwania Internet, korzystając z wyszukiwarki opcji:

* [Funkcje bazy danych programu SQL Server nieobsługiwane przez usługę Azure SQL Database](sql-database-transact-sql-information.md)
* [Nieobsługiwane funkcje aparatu bazy danych w programie SQL Server 2016](https://msdn.microsoft.com/library/ms144262%28v=sql.130%29)
* [Nieobsługiwane funkcje aparatu bazy danych w programie SQL Server 2014](https://msdn.microsoft.com/library/ms144262%28v=sql.120%29)
* [Nieobsługiwane funkcje aparatu bazy danych w programie SQL Server 2012](https://msdn.microsoft.com/library/ms144262%28v=sql.110%29)
* [Nieobsługiwane funkcje aparatu bazy danych w programie SQL Server 2008 R2](https://msdn.microsoft.com/library/ms144262%28v=sql.105%29)
* [Nieobsługiwane funkcje aparatu bazy danych w programie SQL Server 2005](https://msdn.microsoft.com/library/ms144262%28v=sql.90%29)

Ponadto toosearching hello Internet i przy użyciu tych zasobów, użyj hello [forum użytkowników MSDN programu SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver) lub [StackOverflow](http://stackoverflow.com/).

## <a name="next-steps"></a>Następne kroki
* Użyj skryptu hello na blogu inżynierów EMEA SQL Azure hello zbyt[monitorowanie użycia bazy danych tempdb podczas migracji](https://blogs.msdn.microsoft.com/azuresqlemea/2016/12/28/lesson-learned-10-monitoring-tempdb-usage/).
* Użyj skryptu hello na blogu inżynierów EMEA SQL Azure hello zbyt[monitorować hello miejsca w dzienniku transakcji bazy danych, gdy jest wykonywana migracja](https://blogs.msdn.microsoft.com/azuresqlemea/2016/10/31/lesson-learned-7-monitoring-the-transaction-log-space-of-my-database/0).
* Dla programu SQL Server zespół doradczy klientów przy użyciu pliku BACPAC plików, zobacz blog na temat migracji [Migrowanie z programu SQL Server tooAzure bazy danych SQL przy użyciu pliku BACPAC plików](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Aby uzyskać informacji na temat pracy z czasem UTC po migracji, zobacz [hello modyfikowanie domyślną strefę czasową dla lokalnej strefie czasowej](https://blogs.msdn.microsoft.com/azuresqlemea/2016/07/27/lesson-learned-4-modifying-the-default-time-zone-for-your-local-time-zone/).
* Aby uzyskać informacje na temat zmiany hello domyślny język bazy danych po migracji, zobacz [jak toochange hello domyślny język bazy danych SQL Azure](https://blogs.msdn.microsoft.com/azuresqlemea/2017/01/13/lesson-learned-16-how-to-change-the-default-language-of-azure-sql-database/).


