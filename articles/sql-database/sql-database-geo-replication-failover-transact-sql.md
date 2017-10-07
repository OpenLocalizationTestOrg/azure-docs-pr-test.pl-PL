---
title: Baza danych SQL Azure w trybie failover TSQL:initiate | Dokumentacja firmy Microsoft
description: "Zainicjuj tryb failover planowane lub nieplanowane bazy danych SQL Azure przy użyciu języka Transact-SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>Zainicjuj tryb failover planowane lub nieplanowane bazy danych SQL Azure z Transact-SQL

W tym artykule opisano sposób tooa pracy awaryjnej tooinitiate pomocniczej bazy danych SQL przy użyciu języka Transact-SQL. tooconfigure replikacja geograficzna, zobacz [skonfigurować — replikacja geograficzna bazy danych SQL Azure](sql-database-geo-replication-transact-sql.md).

tooinitiate trybu failover, potrzebne są następujące hello:

* Nazwy logowania, która jest dbmanager: na powitania podstawowego
* Ma db_ownership lokalnej bazy danych hello że będzie replikacja geograficzna
* Można na powitania partnera serwery toowhich dbmanager: Skonfiguruj — replikacja geograficzna
* Najnowsza wersja programu SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Zalecane jest, aby zawsze używała hello najnowszej wersji programu Management Studio tooremain synchronizowane z tooMicrosoft aktualizacje, Azure i bazy danych SQL. [Zaktualizuj program SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a>Zainicjuj planowany tryb failover podwyższania poziomu nowego podstawowego hello toobecome dodatkowej bazy danych
Można użyć hello **ALTER DATABASE** toopromote instrukcji nowego podstawowego hello toobecome dodatkowej bazy danych bazy danych w sposób planowane obniżenie hello istniejącej głównej toobecome pomocniczego. Ta instrukcja jest wykonywana na powitania głównej bazy danych na serwerze logicznym usługi Azure SQL Database hello hello, które znajdują się replikowane geograficznie pomocnicze bazy danych, która jest której poziom jest podwyższany. Ta funkcja jest przeznaczona dla planowanego trybu failover, takie jak podczas ćwiczeń hello odzyskiwania po awarii i wymaga podstawowej bazy danych tej hello być niedostępne.

polecenie Hello wykonuje hello następującego przepływu pracy:

1. Tymczasowo tryb toosynchronous replikacji przełączników powoduje wszystkie transakcje oczekujące toobe opróżnionych pomocniczy toohello i blokuje wszystkie nowe transakcje;
2. Przełączniki hello ról hello dwóch baz danych w partnerstwie — replikacja geograficzna hello.  

Ta sekwencja gwarantuje, że Witaj dwie bazy danych są synchronizowane, przed Przełącz role hello i w związku z tym nie dane zostaną utracone. Istnieje krótki okres, podczas którego obie bazy danych są niedostępne (w kolejności hello 0 sekund too25) podczas przełączania hello ról. Jeśli hello podstawowej bazy danych ma wiele baz danych w dodatkowej, polecenie hello zostanie automatycznie ponownej konfiguracji hello innych pomocniczych tooconnect toohello nową podstawową.  cała operacja Hello powinno zająć mniej niż minutę toocomplete w normalnych okolicznościach. Aby uzyskać więcej informacji, zobacz [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) i [warstwy usług](sql-database-service-tiers.md).

Użyj hello następujące kroki tooinitiate planowany tryb failover.

1. W Management Studio Połącz z bazy danych SQL Azure serwera logicznego toohello, w której znajduje się pomocniczej bazy danych replikacją geograficzną.
2. Otwórz folder baz danych hello, rozwiń węzeł hello **systemowych baz danych** folderu, kliknij prawym przyciskiem myszy **wzorca**, a następnie kliknij przycisk **nowe zapytanie**.
3. Użyj następujących hello **ALTER DATABASE** instrukcji tooswitch hello dodatkowej bazy danych toohello podstawową rolą.
   
        ALTER DATABASE <MyDB> FAILOVER;
4. Kliknij przycisk **Execute** toorun hello zapytania.

> [!NOTE]
> W rzadkich przypadkach jest możliwe, że operacja hello nie może ukończyć i mogą być zablokowane. W takim przypadku użytkownik hello można wykonać polecenie hello wymuszenia pracy awaryjnej i zaakceptować utraty danych.
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a>Zainicjuj nieplanowanego trybu failover z dodatkowej bazy danych hello podstawowej bazy danych toohello
Można użyć hello **ALTER DATABASE** toopromote instrukcji nowego podstawowego hello toobecome dodatkowej bazy danych bazy danych w sposób nieplanowane wymuszania obniżania hello hello istniejącej głównej toobecome pomocniczego w czasie gdy hello Podstawowa baza danych nie jest już dostępny. Ta instrukcja jest wykonywana na powitania głównej bazy danych na serwerze logicznym usługi Azure SQL Database hello hello, które znajdują się replikowane geograficznie pomocnicze bazy danych, która jest której poziom jest podwyższany.

Ta funkcja jest przeznaczona dla odzyskiwania po awarii podczas przywracania dostępność bazy danych hello jest szczególnie ważne i utratę danych jest akceptowany. Po wywołaniu wymuszenia pracy awaryjnej hello określone dodatkowej bazy danych natychmiast staje się hello podstawowej bazy danych i rozpoczyna się akceptowanie transakcjach zapisu. Jak hello oryginalnego podstawowej bazy danych jest możliwe tooreconnect z tej nowej podstawowej bazy danych, podjęto na powitania oryginalnego podstawowej bazy danych przyrostowej kopii zapasowej i hello starego podstawowej bazy danych odbywa się do pomocniczej bazy danych dla hello nowe podstawowej bazy danych; następnie jest jedynie Synchronizowanie replik hello nową podstawową.

Jednak ponieważ punktu w przywrócić czasu nie jest obsługiwany na powitania pomocniczej bazy danych, jeśli użytkownik hello żąda danych toorecover zatwierdzone toohello starego głównej bazy danych, która nie została replikowane toohello nowe podstawowej bazy danych przed wystąpieniem hello wymuszone trybu failover, Witaj użytkownik będzie musiał toorecover Obsługa tooengage to utraty danych.

Jeśli hello podstawowej bazy danych ma wiele baz danych w dodatkowej, polecenie hello zostanie automatycznie ponownej konfiguracji hello innych pomocniczych tooconnect toohello nową podstawową.

Użyj hello następujące kroki tooinitiate nieplanowany tryb failover.

1. W Management Studio Połącz z bazy danych SQL Azure serwera logicznego toohello, w której znajduje się pomocniczej bazy danych replikacją geograficzną.
2. Otwórz folder baz danych hello, rozwiń węzeł hello **systemowych baz danych** folderu, kliknij prawym przyciskiem myszy **wzorca**, a następnie kliknij przycisk **nowe zapytanie**.
3. Użyj następujących hello **ALTER DATABASE** instrukcji tooswitch hello dodatkowej bazy danych toohello podstawową rolą.
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. Kliknij przycisk **Execute** toorun hello zapytania.

> [!NOTE]
> Gdy zarówno podstawowy, jak i pomocniczy są w trybie online wydano polecenie hello hello stary serwer podstawowy staną się hello nowym serwerem pomocniczym natychmiast bez synchronizacji danych. Jeśli podstawowy hello jest przekazywanie transakcji po wydaniu polecenia hello utratę danych mogą wystąpić.
> 
> 

## <a name="next-steps"></a>Następne kroki
* Po przejściu w tryb failover upewnij się, że hello wymagania dotyczące uwierzytelniania dla serwera i bazy danych są skonfigurowane na powitania nową podstawową. Aby uzyskać więcej informacji, zobacz [zabezpieczeń bazy danych SQL po awarii](sql-database-geo-replication-security-config.md).
* Zobacz toolearn odzyskiwanie po awarii przy użyciu aktywna replikacja geograficzna, w tym kroki odzyskiwania przed i po odzyskaniu i przejściem do szczegółów odzyskiwania po awarii [odzyskiwania po awarii](sql-database-disaster-recovery.md)
* W blogu Sasha Nosov temat aktywnej replikacji geograficznej w temacie [uwagi na nowe możliwości replikacja geograficzna](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)
* Informacje o projektowaniu chmury aplikacji toouse aktywna replikacja geograficzna, zobacz [projektowanie aplikacji w chmurze dla ciągłości przy użyciu — replikacja geograficzna](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* Aby uzyskać informacji o korzystaniu z pul elastycznych aktywna replikacja geograficzna, zobacz [strategii odzyskiwania danych w puli elastycznej](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
* Omówienie ciągłości działalności biznesowej, zobacz [omówienie ciągłości działalności biznesowej](sql-database-business-continuity.md)

