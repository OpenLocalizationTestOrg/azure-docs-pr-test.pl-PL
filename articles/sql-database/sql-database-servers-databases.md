---
title: "aaaCreate & Zarządzaj serwerami Azure SQL & baz danych | Dokumentacja firmy Microsoft"
description: "Informacje dotyczące serwera bazy danych SQL Azure i pojęcia dotyczące bazy danych oraz tworzenie i zarządzanie serwerami i bazami danych za pomocą hello portalu Azure, programu PowerShell hello Azure CLI, języka Transact-SQL i hello interfejsu API REST."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 0f526e388a5a620349f5a14e8d57a8355ac451ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-sql-database-servers-and-databases"></a>Utwórz i Zarządzaj serwerami bazy danych SQL Azure i baz danych

Baza danych Azure SQL jest zarządzany bazy danych w systemie Microsoft Azure, która jest tworzona w [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) ze zdefiniowanym zestawem [zasobów obliczeniowych i magazynu dla różnych obciążeń](sql-database-service-tiers.md). Baza danych Azure SQL jest skojarzony z serwera logicznego bazy danych SQL Azure, który jest tworzony w określonym regionie Azure. 

## <a name="an-azure-sql-database-can-be-a-single-pooled-or-partitioned-database"></a>Baza danych Azure SQL mogą być jednej puli i podzielonym na partycje bazy danych

Baza danych Azure SQL mogą być:

- pojedynczą bazą danych z [własnym zestawem zasobów](sql-database-what-is-a-dtu.md#what-are-database-transaction-units-dtus) (jednostki DTU).
- Część [puli elastycznej SQL](sql-database-elastic-pool.md) który [udostępnia zestaw zasobów](sql-database-what-is-a-dtu.md#what-are-elastic-database-transaction-units-edtus) (Edtu)
- częścią [skalowanego zestawu baz danych podzielonych na fragmenty](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling), które mogą być pojedynczymi bazami danych lub pulami baz danych.
- częścią zestawu baz danych uczestniczącego we [wzorcu projektowym wielodostępnych aplikacji SaaS](sql-database-design-patterns-multi-tenancy-saas-applications.md), którego bazy danych mogą być pojedynczymi bazami danych i/lub pulami baz danych. 

> [!TIP]
> Prawidłowe nazwy baz danych opisano w artykule [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identyfikatory baz danych). 
>
 
- Witaj domyślne sortowanie bazy danych używane przez usługę Microsoft Azure SQL Database jest **SQL_LATIN1_GENERAL_CP1_CI_AS**, gdzie **LATIN1_GENERAL** jest angielski (Stany Zjednoczone), **CP1** Strona kodowa 1252, jest **CI** nie uwzględnia wielkości liter, i **AS** jest akcentów. Aby uzyskać więcej informacji o sposobie tooset hello sortowania, zobacz [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx).
- Baza danych SQL Azure Microsoft obsługuje danych tabelarycznych (TDS) protokół klienta wersja strumienia 7.3 lub nowszej.
- Dozwolone są tylko połączenia protokołu TCP/IP.

## <a name="what-is-an-azure-sql-logical-server"></a>Co to jest serwer logiczny Azure SQL?

Serwer logiczny działa jako centralny punkt administracyjny dla wielu baz danych, w tym [puli elastycznej SQL](sql-database-elastic-pool.md) [logowania](sql-database-manage-logins.md), [reguły zapory](sql-database-firewall-configure.md), [inspekcji reguły](sql-database-auditing.md), [zasady wykrywania zagrożeń](sql-database-threat-detection.md), i [trybu failover grupy](sql-database-geo-replication-overview.md). W regionie innym niż jego grupa zasobów może być serwerem logicznym. Serwer logiczny Hello musi istnieć przed utworzeniem hello bazy danych Azure SQL. Wszystkie bazy danych na serwerze są tworzone w ramach hello sam region jako powitania serwera logicznego. 


> [!IMPORTANT]
> W bazie danych SQL serwer jest konstrukcją logiczną, która różni się od wystąpienia programu SQL Server, które można zapoznać się z Witaj świecie lokalnych. W szczególności hello usługi baza danych SQL sprawia, że nie gwarancji dotyczących lokalizacji hello baz danych w relacji serwerów logicznych tootheir i ujawnia nie dostęp na poziomie wystąpienia lub funkcji.
> 

Tworzenie serwera logicznego, należy podać serwer, konto logowania i hasło, które ma prawa administracyjne toohello głównej bazy danych na tym serwerze i wszystkich baz danych utworzonych na tym serwerze. To konto początkowej jest konto logowania SQL. Baza danych SQL Azure obsługuje uwierzytelnianie SQL i uwierzytelniania usługi Azure Active Directory do uwierzytelniania. Aby uzyskać informacje dotyczące logowania i uwierzytelniania, zobacz [Zarządzanie bazami danych i Logowaniami w bazie danych SQL Azure](sql-database-manage-logins.md). Uwierzytelnianie systemu Windows nie jest obsługiwane. 

> [!TIP]
> Aby uzyskać prawidłowy zasób grupy i nazw serwerów, zobacz [nazewnictwa reguły i ograniczenia](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).
>

Serwer logiczny bazy danych Azure:

- Zostało utworzone w ramach subskrypcji platformy Azure, ale mogą zostać przeniesione z jego subskrypcją tooanother zawartych w niej zasobów
- Jest zasobem nadrzędnej hello baz danych, pule elastyczne i magazyny danych
- Obejmuje przestrzeń nazw dla bazy danych, pule elastyczne i magazyny danych
- Jest kontenerem logicznym z semantyki silne okres istnienia - Usuń serwer i usuwa hello zawartych baz danych, pule elastyczne i magazyny danych
- Uczestniczy w [kontroli dostępu opartej na rolach na platformie Azure (RBAC)](/active-directory/role-based-access-control-what-is) — bazy danych, pule elastyczne i hurtowni danych w ramach serwera dziedziczyć praw dostępu powitania serwera
- Jest elementem znaczących tożsamości hello baz danych, pule elastyczne i magazynów danych dla zasobów platformy Azure do celów zarządzania (zobacz hello URL schematu dla baz danych i pul)
- Rozmieszcza zasoby w regionie
- Udostępnia punkt końcowy połączenia dla dostępu do baz danych (<serverName>.database.windows.net)
- Zapewnia dostęp toometadata dotyczące zawartych w niej zasobów przy użyciu widoków DMV przez połączenia bazy danych master tooa 
- Określa zakres powitania dla zasad zarządzania, które zastosować baz danych tooits — logowania, zapory, inspekcji, zagrożenia wykrywania itp. 
- Jest ograniczony przez przydział w ramach subskrypcji nadrzędnej hello (sześciu serwerów na subskrypcję domyślnie - [Zobacz subskrypcji w tym miejscu ogranicza](../azure-subscription-service-limits.md))
- Określa zakres hello limit przydziału bazy danych i limit przydziału jednostek DTU dla hello zasoby, które zawiera (na przykład DTU 45 000)
- Jest zakres przechowywania wersji hello możliwościami włączonymi zawartych w niej zasobów 
- Logowania główne na poziomie serwera mogą zarządzać wszystkimi bazami danych na serwerze
- Może zawierać nazwy logowania podobne toothose w wystąpieniach programu SQL Server lokalnie udzielono dostępu tooone lub więcej baz danych na powitania serwera, które mogą być ograniczone przyznanych uprawnień administracyjnych. Aby uzyskać więcej informacji, zobacz temat [Logowania](sql-database-manage-logins.md).

## <a name="azure-sql-databases-protected-by-sql-database-firewall"></a>Chronione przez zaporę bazy danych SQL Azure bazy danych SQL

toohelp chronić dane, [zapory bazy danych SQL](sql-database-firewall-configure.md) uniemożliwia wszystkich serwera bazy danych tooyour dostępu lub dowolny z jej baz danych z poza serwerem toohello połączenie bezpośrednio za pośrednictwem połączenia subskrypcji platformy Azure. tooenable dodatkowych problemów z łącznością, należy najpierw [utworzyć co najmniej jedną regułę zapory](sql-database-firewall-configure.md#creating-and-managing-firewall-rules). Do tworzenia i zarządzania pule elastyczne SQL, zobacz [pule elastyczne](sql-database-elastic-pool.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-portal"></a>Zarządzaj serwerami Azure SQL, baz danych i zapory przy użyciu hello portalu Azure

Można utworzyć grupy zasobów hello usługa Azure SQL database wcześniejsze lub podczas tworzenia hello sam serwer. Istnieje wiele metod uzyskania tooa nowy formularz serwera SQL, tworząc nowy serwer SQL lub podczas tworzenia nowej bazy danych. 

### <a name="create-a-blank-sql-server-logical-server"></a>Utwórz puste SQL server (serwer logiczny)

Witaj toocreate serwera (bez bazy danych) bazy danych SQL Azure przy użyciu [portalu Azure](https://portal.azure.com), przejdź tooa pustego programu SQL server (serwer logiczny) formularza. Witaj Poniższy zrzut ekranu przedstawia jedną metodę otwierania toocreate formularza pusty serwer logiczny SQL. 

   ![Tworzenie serwera logicznego ukończone formularza](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

Jeśli zostanie wyświetlony formularz toothis przy użyciu innej metody, hello informacje w formularzu hello jest identyczne.

### <a name="create-a-blank-or-sample-sql-database"></a>Utwórz puste lub przykładowa baza danych SQL

Witaj toocreate bazy danych Azure SQL przy użyciu [portalu Azure](https://portal.azure.com), przejdź tooa pusty formularz bazy danych SQL i podaj hello wymagane informacje. Można utworzyć grupy zasobów hello usługa Azure SQL database i serwer logiczny wcześniejsze lub podczas tworzenia hello bazy danych. Można utworzyć pustą bazę danych lub utworzyć oparty na Adventure Works LT. przykładowej bazy danych 

  ![tworzenie bazy danych 1](./media/sql-database-get-started-portal/create-database-1.png)

> [WAŻNE] Aby uzyskać informacje na temat wybierania hello warstwę cenową dla bazy danych, zobacz [warstw usług](sql-database-service-tiers.md).
>

### <a name="manage-an-existing-sql-server"></a>Zarządzanie istniejącego serwera SQL

toomanage istniejącego serwera, przejdź toohello serwera przy użyciu metod — przykład wyświetlanie określonej strony bazy danych SQL, hello **serwerów SQL** strony lub hello **wszystkie zasoby** strony. powitania po zrzut ekranu przedstawia sposób toobegin ustawienia zapory poziomu serwera z hello **omówienie** strony serwera. 

   ![Omówienie serwera logicznego](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

toomanage istniejącej bazy danych, przejdź toohello **baz danych SQL** i kliknij przycisk hello bazy danych chcesz toomanage. powitania po zrzut ekranu przedstawia sposób toobegin ustawienia zapory poziomu serwera bazy danych z hello **omówienie** stron dla bazy danych. 

   ![reguła zapory serwera](./media/sql-database-get-started-portal/server-firewall-rule.png) 

> [!IMPORTANT]
> właściwości wydajności tooconfigure dla bazy danych, zobacz [warstw usług](sql-database-service-tiers.md).
>

> [!TIP]
> Samouczek szybki start dla usługi Azure portalu, zobacz [tworzenie bazy danych Azure SQL w portalu Azure hello](sql-database-get-started-portal.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-powershell"></a>Zarządzaj serwerami oraz baz danych Azure SQL a zapory przy użyciu programu PowerShell

toocreate i zarządzania Azure, programu SQL server, baz danych i zapory przy użyciu programu Azure PowerShell, użyj następującego polecenia cmdlet programu PowerShell hello. Jeśli konieczne tooinstall lub uaktualnić programu PowerShell, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps). Do tworzenia i zarządzania pule elastyczne SQL, zobacz [pule elastyczne](sql-database-elastic-pool.md).

| Polecenie cmdlet | Opis |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Tworzy bazę danych |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Pobiera jeden lub więcej baz danych|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Ustawia właściwości dla bazy danych lub przenosi istniejącą bazę danych do puli elastycznej|
|[Remove-AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Usuwa z bazy danych|
|[Nowe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)|Tworzy grupę zasobów]
|[Nowe AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver)|Tworzy serwer|
|[Get-AzureRmSqlServer](/powershell/module/azurerm.sql/get-azurermsqlserver)|Zwraca informacje na temat serwerów|
|[Set-AzureRmSqlServer](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/set-azurermsqlserver)|Modyfikuje właściwości serwera|
|[Remove-AzureRmSqlServer](/powershell/module/azurerm.sql/remove-azurermsqlserver)|Usuwa serwer|
|[New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule)|Tworzy regułę zapory poziomu serwera |
|[Get-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/get-azurermsqlserverfirewallrule)|Pobiera reguły zapory serwera|
|[Set-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/set-azurermsqlserverfirewallrule)|Modyfikuje regułę zapory na serwerze|
|[Remove-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/remove-azurermsqlserverfirewallrule)|Usuwa regułę zapory z serwera.|

> [!TIP]
> Samouczek szybki start programu PowerShell, zobacz [tworzenia pojedynczej bazy danych Azure SQL przy użyciu programu PowerShell](sql-database-get-started-portal.md). Dla programu PowerShell przykładowe skrypty, zobacz [toocreate PowerShell użyj pojedynczego SQL Azure bazy danych, a następnie skonfigurować reguły zapory](scripts/sql-database-create-and-configure-database-powershell.md) i [monitora i skali pojedynczego SQL bazy danych przy użyciu programu PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-cli"></a>Zarządzaj serwerami Azure SQL, baz danych i zapory przy użyciu hello wiersza polecenia platformy Azure

toocreate serwerów Azure SQL, baz danych i zapór z hello oraz zarządzanie [interfejsu wiersza polecenia Azure](/cli/azure/overview), poniższych hello [bazy danych SQL interfejsu wiersza polecenia Azure](/cli/azure/sql/db) poleceń. Użyj hello [powłoki chmury](/azure/cloud-shell/overview) toorun hello interfejsu wiersza polecenia w przeglądarce lub [zainstalować](/cli/azure/install-azure-cli) go na system macOS, Linux lub Windows. Do tworzenia i zarządzania pule elastyczne SQL, zobacz [pule elastyczne](sql-database-elastic-pool.md).

| Polecenie cmdlet | Opis |
| --- | --- |
|[Tworzenie bazy danych sql az](/cli/azure/sql/db#create) |Tworzy bazę danych|
|[Lista bazy danych sql az](/cli/azure/sql/db#list)|Wyświetla listę wszystkich baz danych i magazynów danych na serwerze lub wszystkie bazy danych w puli elastycznej|
|[Lista wersje az bazy danych sql](/cli/azure/sql/db#list-editions)|Wyświetla dostępne usługi cele i limity magazynu|
|[bazy danych sql az listy użycia](/cli/azure/sql/db#list-usages)|Zwraca bazy danych użycia|
|[Pokaż bazy danych sql az](/cli/azure/sql/db#show)|Pobiera Magazyn bazy danych lub danych|
|[Aktualizacja bazy danych sql az](/cli/azure/sql/db#update)|Aktualizuje bazę danych|
|[Usuwanie bazy danych sql az](/cli/azure/sql/db#delete)|Usuwa z bazy danych|
|[Tworzenie grupy az](/cli/azure/group#create)|Tworzy grupę zasobów|
|[Utwórz az programu sql server](/cli/azure/sql/server#create)|Tworzy serwer|
|[Lista serwerów sql az](/cli/azure/sql/server#list)|Wyświetla serwery|
|[Serwer sql az listy użycia](/cli/azure/sql/server#list-usages)|Zwraca użycia serwera|
|[Pokaż serwera sql az](/cli/azure/sql/server#show)|Pobiera serwera|
|[Aktualizacja programu sql server az](/cli/azure/sql/server#update)|Serwer aktualizacji|
|[Usuń serwer sql az](/cli/azure/sql/server#delete)|Usuwa serwer|
|[Utwórz az programu sql server — reguły zapory](/cli/azure/sql/server/firewall-rule#create)|Powoduje utworzenie reguły zapory serwera|
|[Lista reguł zapory serwera sql az](/cli/azure/sql/server/firewall-rule#list)|Wyświetla listę reguł zapory hello na serwerze|
|[Pokaż reguły zapory serwera sql az](/cli/azure/sql/server/firewall-rule#show)|Wyświetla szczegóły hello reguły zapory|
|[Aktualizacja reguły zapory programu sql server az](/cli/azure/sql/server/firewall-rule#update)|Aktualizuje regułę zapory|
|[Usuwanie reguły zapory serwera sql az](/cli/azure/sql/server/firewall-rule#delete)|Usuwa regułę zapory|

> [!TIP]
> Samouczek szybki start wiersza polecenia platformy Azure, zobacz [tworzenia pojedynczej bazy danych Azure SQL przy użyciu interfejsu wiersza polecenia Azure hello](sql-database-get-started-cli.md). Dla interfejsu wiersza polecenia Azure przykładowe skrypty, zobacz [toocreate CLI użyj pojedynczego SQL Azure bazy danych, a następnie skonfigurować reguły zapory](scripts/sql-database-create-and-configure-database-cli.md) i [toomonitor Użyj interfejsu wiersza polecenia i skalowania pojedynczej bazy danych SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-transact-sql"></a>Zarządzaj serwerami oraz baz danych Azure SQL a zapory przy użyciu języka Transact-SQL

toocreate i zarządzania usługi Azure SQL server, baz danych i zapór z Transact-SQL, użyj następującego polecenia T-SQL hello. Możesz wykonywać te polecenia przy użyciu hello portalu Azure, [programu SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), lub inny program, który można połączyć z serwerem bazy danych SQL Azure tooan i przekazać języka Transact-SQL polecenia. Do zarządzania pule elastyczne SQL, zobacz [pule elastyczne](sql-database-elastic-pool.md).

> [!IMPORTANT]
> Nie można utworzyć ani usunąć z serwerem przy użyciu języka Transact-SQL.
>

| Polecenie | Opis |
| --- | --- |
|[Utwórz bazę danych (baza danych Azure SQL)](/sql/t-sql/statements/create-database-azure-sql-database)|Tworzy nową bazę danych. Musi być połączony toohello bazy danych master toocreate nową bazę danych.|
| [ALTER DATABASE (baza danych Azure SQL)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modyfikuje bazy danych Azure SQL. |
|[ALTER DATABASE (Azure SQL Data Warehouse)](/sql/t-sql/statements/alter-database-azure-sql-data-warehouse)|Modyfikuje magazyn danych Azure SQL.|
|[Usuwanie bazy danych (Transact-SQL)](/sql/t-sql/statements/drop-database-transact-sql)|Usuwa z bazy danych.|
|[sys.database_service_objectives (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Zwraca hello edition (warstwy usług), celem usługi (warstwa cenowa) i nazwę puli elastycznej dla bazy danych Azure SQL lub usługi Azure SQL Data Warehouse. Jeśli zalogowany toohello głównej bazy danych na serwerze bazy danych SQL Azure, zwraca informacje o wszystkich baz danych. Dla usługi Azure SQL Data Warehouse musi być połączony toohello bazy danych master.|
|[sys.dm_db_resource_stats (baza danych SQL Azure)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database)| Zwraca zużycie Procesora, operacji We/Wy i pamięci dla bazy danych z bazy danych SQL Azure. Dla co 15 s istnieje jeden wiersz, nawet jeśli nic się nie hello bazy danych.|
|[sys.resource_stats (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database)|Zwraca procesora CPU, użycia i magazynu danych dla bazy danych SQL Azure. Witaj, dane są zbierane i agregowane w ciągu 5 minut.|
|[sys.database_connection_stats (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-database-connection-stats-azure-sql-database)|Zawiera dane statystyczne dla zdarzenia łączności bazy danych SQL Database przedstawiające przegląd bazy danych połączenia sukcesy i niepowodzenia. |
|[sys.event_log (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-event-log-azure-sql-database)|Zwraca pomyślnego połączenia z bazą danych usługi Azure SQL Database, błędy połączeń i zakleszczenia. Można użyć tego tootrack informacji lub Rozwiązywanie problemów z działania bazy danych z bazy danych SQL.|
|[procedurę składowaną sp_set_firewall_rule (baza danych SQL Azure)](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)|Tworzy lub aktualizuje hello ustawienia zapory poziomu serwera dla serwera bazy danych SQL. Ta procedura składowana jest dostępna tylko w hello bazy danych master toohello poziomu serwera głównego identyfikatora logowania. Reguły zapory poziomu serwera można tworzyć tylko za pomocą języka Transact-SQL, po utworzeniu pierwszej reguły zapory poziomu serwera hello przez użytkownika z uprawnienia na poziomie Azure|
|[sys.firewall_rules (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database)|Zwraca informacje na temat ustawień zapory poziomu serwera hello skojarzonych z bazy danych SQL Microsoft Azure.|
|[sp_delete_firewall_rule (baza danych SQL Azure)](/sql/relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database)|Usuwa ustawienia zapory poziomu serwera z serwerem bazy danych SQL. Ta procedura składowana jest dostępna tylko w hello bazy danych master toohello poziomu serwera głównego identyfikatora logowania.|
|[sp_set_database_firewall_rule (baza danych SQL Azure)](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)|Tworzy lub aktualizuje hello reguły zapory poziomu bazy danych dla bazy danych SQL Azure lub usługi SQL Data Warehouse. Można skonfigurować reguł zapory bazy danych dla bazy danych master hello i baz danych użytkowników w bazie danych SQL. Reguły zapory bazy danych są przydatne, gdy przy użyciu zawarte bazy danych użytkowników. |
|[sys.database_firewall_rules (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database)|Zwraca informacje na temat ustawień zapory na poziomie bazy danych hello skojarzonych z bazy danych SQL Microsoft Azure. |
|[sp_delete_database_firewall_rule (baza danych SQL Azure)](/sql/relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database)|Ustawienia zapory na poziomie bazy danych usuwa z bazy danych SQL Azure lub SQL Data Warehouse. |


> [!TIP]
> Samouczek szybki start Microsoft Windows za pomocą programu SQL Server Management Studio, zobacz [bazy danych SQL Azure: Użyj programu SQL Server Management Studio tooconnect i zapytań danych](sql-database-connect-query-ssms.md). Samouczek szybki start za pomocą programu Visual Studio Code na powitania macOS, Linux lub Windows, temacie [bazy danych SQL Azure: Użyj Visual Studio Code tooconnect i zapytań danych](sql-database-connect-query-vscode.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-rest-api"></a>Zarządzaj serwerami Azure SQL, baz danych i zapory przy użyciu hello interfejsu API REST

toocreate i zarządzanie Azure SQL server, baz danych i zapory przy użyciu hello interfejsu API REST, zobacz [interfejsu API REST bazy danych SQL Azure](/rest/api/sql/).

## <a name="next-steps"></a>Następne kroki

- toolearn dotyczących pul baz danych przy użyciu puli elastycznej SQL, zobacz [pule elastyczne](sql-database-elastic-pool.md).
- Informacje o hello usługi baza danych SQL Azure, zobacz [co to jest SQL Database?](sql-database-technical-overview.md).
- toolearn dotyczące migrowania tooAzure bazy danych programu SQL Server, zobacz [migracji tooAzure bazy danych SQL](sql-database-cloud-migrate.md).
- Informacje dotyczące obsługiwanych funkcji można znaleźć w temacie [Funkcje](sql-database-features.md).
