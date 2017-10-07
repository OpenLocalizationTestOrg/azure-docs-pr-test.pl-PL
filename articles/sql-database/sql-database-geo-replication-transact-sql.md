---
title: Replikacja geograficzna aaaConfigure bazy danych SQL Azure z Transact-SQL | Dokumentacja firmy Microsoft
description: "Konfigurowanie bazy danych SQL Azure przy użyciu języka Transact-SQL — replikacja geograficzna"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Skonfiguruj aktywna replikacja geograficzna bazy danych SQL Azure z Transact-SQL

W tym artykule opisano sposób tooconfigure aktywna replikacja geograficzna bazy danych SQL Azure z Transact-SQL.

tooinitiate trybu failover przy użyciu języka Transact-SQL, zobacz [zainicjowanie planowanego lub nieplanowanego trybu failover dla bazy danych SQL Azure z Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> Jeśli aktywna replikacja geograficzna (elementów dodatkowych do odczytu) jest używany do odzyskiwania po awarii należy skonfigurować grupę trybu failover dla wszystkich baz danych w aplikacji tooenable automatyczne i przezroczystym trybem failover. Ta funkcja jest dostępna w wersji zapoznawczej. Aby uzyskać więcej informacji, zobacz [pracy awaryjnej automatycznie grup i replikacja geograficzna](sql-database-geo-replication-overview.md).
> 
> 

aktywna replikacja geograficzna tooconfigure przy użyciu języka Transact-SQL, należy hello poniżej:

* Subskrypcja platformy Azure
* Serwerem logicznym bazy danych SQL Azure <MyLocalServer> i bazy danych SQL <MyDB> -podstawowej bazy danych hello, które mają tooreplicate
* Jeden lub więcej logicznej bazy danych SQL Azure serwerów < MySecondaryServer(n) > — Witaj logicznej serwerów, które będą hello partnerach, w których zostanie tworzenie pomocniczej bazy danych
* Nazwy logowania, która jest dbmanager: na powitania podstawowego
* Ma db_ownership lokalnej bazy danych hello że będzie replikacja geograficzna
* Można na powitania partnera serwery toowhich dbmanager: Skonfiguruj — replikacja geograficzna
* Witaj najnowsza wersja programu SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Zalecane jest, aby zawsze używała hello najnowszej wersji programu Management Studio tooremain synchronizowane z tooMicrosoft aktualizacje, Azure i bazy danych SQL. [Zaktualizuj program SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>Dodaj dodatkowej bazy danych
Można użyć hello **ALTER DATABASE** toocreate instrukcji replikacją geograficzną pomocniczej bazy danych na serwer partnera. Tej instrukcji można wykonywać na powitania głównej bazy danych powitania serwera zawierający hello bazy danych toobe replikowane. Witaj replikacją geograficzną bazy danych (hello "podstawowej bazy danych") wymaga hello sama nazwa jak hello bazy danych są replikowane i zostanie domyślnie hello samym poziomie usług jako hello podstawowej bazy danych. Witaj dodatkowej bazy danych może być do odczytu lub bez możliwości odczytu i może być pojedynczą bazę danych lub w puli elastycznej. Aby uzyskać więcej informacji, zobacz [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) i [warstwy usług](sql-database-service-tiers.md).
Po utworzeniu i rozpoczęta hello dodatkowej bazy danych, danych rozpocznie replikowanie asynchronicznie z hello podstawowej bazy danych. Witaj kroki opisują sposób replikacja geograficzna tooconfigure przy użyciu Management Studio. Kroki toocreate bez możliwości odczytu i do odczytu replik pomocniczych, podano jako pojedynczej bazy danych lub w puli elastycznej.

> [!NOTE]
> Jeśli baza danych istnieje na serwerze określony partner hello hello sama nazwa jak polecenie hello podstawowej bazy danych hello zakończy się niepowodzeniem.
> 

### <a name="add-readable-secondary-single-database"></a>Dodaj do odczytu pomocniczy (pojedynczej bazy danych)
Użyj hello następujące kroki toocreate pomocniczego do odczytu jako pojedynczej bazy danych.

1. W Management Studio połącz serwera logicznego bazy danych SQL Azure tooyour.
2. Otwórz folder baz danych hello, rozwiń węzeł hello **systemowych baz danych** folderu, kliknij prawym przyciskiem myszy **wzorca**, a następnie kliknij przycisk **nowe zapytanie**.
3. Użyj następujących hello **ALTER DATABASE** toomake instrukcji lokalnej bazy danych w podstawowej replikacji geograficznej z odczytywalną pomocniczą bazą danych na serwerze pomocniczym.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Kliknij przycisk **Execute** toorun hello zapytania.

### <a name="add-readable-secondary-elastic-pool"></a>Dodaj do odczytu pomocniczy (puli elastycznej)
Użyj hello następujące kroki toocreate pomocniczego do odczytu w puli elastycznej.

1. W Management Studio połącz serwera logicznego bazy danych SQL Azure tooyour.
2. Otwórz folder baz danych hello, rozwiń węzeł hello **systemowych baz danych** folderu, kliknij prawym przyciskiem myszy **wzorca**, a następnie kliknij przycisk **nowe zapytanie**.
3. Użyj następujących hello **ALTER DATABASE** toomake instrukcji lokalnej bazy danych w podstawowej replikacji geograficznej z odczytywalną pomocniczą bazą danych na serwerze pomocniczym w puli elastycznej.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Kliknij przycisk **Execute** toorun hello zapytania.

## <a name="remove-secondary-database"></a>Usuń z dodatkowej bazy danych
Można użyć hello **ALTER DATABASE** toopermanently instrukcji Zakończ hello replikacji współpracy między pomocniczej bazy danych i jego podstawowym. Ta instrukcja jest wykonywana na na które hello podstawowa baza danych znajduje się baza danych master hello. Po zakończeniu relacji hello hello dodatkowej bazy danych staje się zwykłej odczytu i zapisu bazy danych. Hello łączności toosecondary w bazie danych jest uszkodzona hello polecenia zakończy się pomyślnie, ale hello dodatkowej staną odczytu i zapisu, po przywróceniu łączności. Aby uzyskać więcej informacji, zobacz [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) i [warstwy usług](sql-database-service-tiers.md).

Użyj hello poniższych kroków tooremove replikowane geograficznie pomocnicze z powiązanie — replikacja geograficzna.

1. W Management Studio połącz serwera logicznego bazy danych SQL Azure tooyour.
2. Otwórz folder baz danych hello, rozwiń węzeł hello **systemowych baz danych** folderu, kliknij prawym przyciskiem myszy **wzorca**, a następnie kliknij przycisk **nowe zapytanie**.
3. Użyj następujących hello **ALTER DATABASE** instrukcji tooremove replikowane geograficznie pomocnicze.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Kliknij przycisk **Execute** toorun hello zapytania.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Monitor konfiguracji aktywna replikacja geograficzna i kondycji

Zadania monitorowania obejmują monitorowanie hello — replikacja geograficzna konfiguracji i monitorowanie kondycji replikacji danych.  Można użyć hello **sys.dm_geo_replication_links** dynamiczny widok zarządzania hello bazy danych master tooreturn informacje o wszystkich istniejących łącza replikacji dla każdej bazy danych na serwerze logicznym hello bazy danych SQL Azure. Ten widok zawiera wiersz dla każdego łącza replikacji hello między bazami danych podstawowych i pomocniczych. Można użyć hello **sys.dm_replication_link_status** dynamicznego zarządzania wyświetlić tooreturn wiersz dla każdej bazy danych SQL Azure, która obecnie prowadzi replikacji łącza replikacji. Dotyczy to zarówno podstawowych i pomocniczych baz danych. Jeśli istnieje więcej niż jedno łącze replikacji ciągłej dla danego podstawowej bazy danych, ta tabela zawiera wiersz dla każdego hello relacji. Widok Hello jest tworzony w wszystkich baz danych, w tym hello logicznej wzorca. Jednak badania ten widok wzorca logicznej hello zwraca pusty zestaw. Można użyć hello **sys.dm_operation_status** dynamicznego zarządzania wyświetlić stan hello tooshow dla wszystkich bazy danych operacji w tym stan hello hello łącza replikacji. Aby uzyskać więcej informacji, zobacz [sys.geo_replication_links (Azure SQL Database)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (Azure SQL Database)](https://msdn.microsoft.com/library/mt575504.aspx), i [sys.dm_operation_status (Azure SQL Database)](https://msdn.microsoft.com/library/dn270022.aspx).

Użyj hello następujące kroki toomonitor aktywna replikacja geograficzna powiązania.

1. W Management Studio połącz serwera logicznego bazy danych SQL Azure tooyour.
2. Otwórz folder baz danych hello, rozwiń węzeł hello **systemowych baz danych** folderu, kliknij prawym przyciskiem myszy **wzorca**, a następnie kliknij przycisk **nowe zapytanie**.
3. Za pomocą powitania po instrukcji tooshow wszystkie bazy danych — replikacja geograficzna łącza.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Kliknij przycisk **Execute** toorun hello zapytania.
5. Otwórz folder baz danych hello, rozwiń węzeł hello **systemowych baz danych** folderu, kliknij prawym przyciskiem myszy **MyDB**, a następnie kliknij przycisk **nowe zapytanie**.
6. Hello Użyj następujących instrukcji tooshow hello replikacji przed elementem i ostatni czas pomocniczych baz danych z MyDB replikacji.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Kliknij przycisk **Execute** toorun hello zapytania.
8. Użyj następującej instrukcji tooshow hello najnowszych — replikacja geograficzna operacji skojarzonej z bazą danych MyDB hello.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Kliknij przycisk **Execute** toorun hello zapytania.

## <a name="next-steps"></a>Następne kroki
* toolearn więcej informacji na temat trybu failover grupy i aktywna replikacja geograficzna, zobacz - [grup trybu Failover](sql-database-geo-replication-overview.md)
* Omówienie ciągłości działalności biznesowej i scenariuszy, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md)

