---
title: "Azure warstwy usług i wydajności bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Porównanie warstw usługi SQL Database i poziomy wydajności dla pojedynczej bazy danych i powodować puli elastycznej SQL"
keywords: "opcje bazy danych, wydajność bazy danych"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: f5c5c596-cd1e-451f-92a7-b70d4916e974
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: b27b78788614d32e6c0c4267fe0ce504ebd2f444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Jakie opcje wydajności są dostępne dla bazy danych SQL Azure

[Baza danych SQL Azure](sql-database-technical-overview.md) oferuje cztery warstwy usługi dla obu jednym i [puli](sql-database-elastic-pool.md) baz danych. Te warstwy usług są: **podstawowe**, **standardowe**, **Premium**, i **Premium RS**. W poszczególnych warstwach usług są wiele poziomów wydajności ([Dtu](sql-database-what-is-a-dtu.md)) i magazynu opcje toohandle różne rozmiary obciążeń i danych. Dodatkowe zasoby obliczeniowe zapewnienia wyższej wydajności i zasoby magazynu toodeliver coraz wyższą przepływność i pojemności. Można zmienić warstwy usług, poziomów wydajności i magazynu dynamicznie bez przestojów. 
- **Podstawowe**, **standardowe** i **Premium** wszystkie warstwy usług ma przestojów SLA 99.99%, elastyczne opcje ciągłości działania, funkcje zabezpieczeń i rozliczenia godzinowe. 
- Witaj **Premium RS** warstwy zapewnia hello te same poziomy wydajności podczas hello warstwy Premium z obniżonych umowy SLA, ponieważ będzie ona uruchamiana z mniejszą liczbę nadmiarowe kopie niż baza danych w hello innej warstwy usługi. Dlatego w przypadku hello awarii usługi, może być konieczne toorecover bazy danych z kopii zapasowej z zapasowej tooa 5-minutowy opóźnienie.

> [!IMPORTANT]
> Baza danych Azure SQL pobiera zagwarantowany zestaw zasobów i hello oczekiwane charakterystyki wydajności bazy danych nie dotyczy innych bazy danych w obrębie platformy Azure. 

## <a name="choosing-a-service-tier"></a>Wybieranie warstwy usług
Witaj Poniższa tabela zawiera przykłady warstw hello najlepiej nadaje się do różnych obciążeń aplikacji.

| Warstwa usług | Docelowe obciążenia |
| :--- | --- |
| **Podstawowa** | Najodpowiedniejsza dla małych baz danych. Standardowo zapewnia obsługę jednej aktywnej operacji w danym momencie. Przykłady zastosowania to bazy danych używane do tworzenia i testowania oprogramowania lub niewielkie, rzadko używane aplikacje. |
| **Standardowa** |Witaj Przejdź toooption dla aplikacji w chmurze z niskim toomedium we/wy wymagania dotyczące wydajności, obsługa wielu równoczesnych zapytań. Przykładowe zastosowania to aplikacje grupy roboczej lub sieci Web. |
| **Premium** | Przeznaczona dla dużych ilości transakcji z wysokimi wymaganiami dotyczącymi wydajności operacji we/wy przy obsłudze wielu równoczesnych użytkowników. Przykładem zastosowania mogą być bazy danych dla aplikacji o znaczeniu krytycznym. |
| **R — wersja Premium** | Przeznaczona dla obciążeń intensywnie wykonujących operacje We/Wy, które nie wymagają hello najwyższą dostępność gwarancji. Przykłady obejmują testowanie obciążeń wysokiej wydajności lub obciążenia analitycznych, gdzie hello bazy danych nie jest systemem hello rekordu. |
|||

Możesz utworzyć pojedynczych baz danych z dedykowanym zasobów w ramach warstwy usług na określonym [poziom wydajności](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) lub baz danych można również utworzyć [puli elastycznej SQL](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus). W puli elastycznej SQL zasoby obliczeniowe i magazynujące hello są współdzielone przez wiele baz danych w ramach pojedynczego serwera logicznego. 

Zasoby dostępne dla pojedynczej bazy danych są wyrażone w jednostki transakcji bazy danych (Dtu) i zasobów dla pul elastycznych SQL są wyrażane w postaci liczby jednostek transakcji elastycznej bazy danych (Edtu). Aby uzyskać więcej informacji na temat jednostek Dtu a Edtu, zobacz [co to są Dtu a Edtu?](sql-database-what-is-a-dtu.md).

toodecide na warstwy usług, uruchom przez określenie hello funkcji minimalna bazy danych, które należy:

| **Funkcji warstwy usługi** | **Podstawowa** | **Standardowa** | **Premium** | **R — wersja Premium**|
| :-- | --: | --: | --: | --: |
| Rozmiar maksymalny pojedynczej bazy danych | 2 GB | 250 GB | 4 TB *  | 500 GB  |
| Rozmiar maksymalny puli elastycznej | 156 GB | 2,9 TB | 4 TB * | 750 GB |
| Maksymalny rozmiar bazy danych w puli elastycznej | 2 GB | 250 GB | 500 GB | 500 GB |
| Maksymalna liczba baz danych dla każdej puli | 500  | 500 | 100 | 100 |
| Maksymalna pojedynczej bazy danych Dtu | 5 | 100 | 4000 | 1000 |
| Maksymalna Dtu na bazę danych w puli elastycznej | 5 | 3000 | 4000 | 1000 |
| Okres przechowywania kopii zapasowych bazy danych | 7 dni | 35 dni | 35 dni | 35 dni |
||||||

> [!IMPORTANT]
> Magazyn zapasowej too4 TB jest obecnie dostępna w następujących regionach hello: East2 nam, zachodnie stany USA, Virginia nam wersji dla instytucji rządowych, Europa Zachodnia, Niemcy centralnej, Południowej, Azja Wschodnia, Japonia Wschodnia, Australia Wschodnia, Kanada centralnej i Kanada Wschodnia. Zobacz [ograniczenia bieżącego 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)
>

Po określeniu warstwy odpowiednią usługę hello są poziom wydajności hello gotowe toodetermine (hello liczba jednostek Dtu) i wielkość magazynu hello hello bazy danych. 

- Witaj S2 i S3 poziomy wydajności w hello **standardowe** warstwy są często dobry punkt wyjścia. 
- W przypadku baz danych wysokiego procesora CPU lub we/wy, hello poziomy wydajności w hello **Premium** warstwy są hello prawo punkt początkowy. 
- Witaj **Premium** warstwa oferuje więcej czasu Procesora i rozpoczyna się od 10 x więcej operacji We/Wy w porównaniu toohello najwyższy poziom wydajności w hello **standardowe** warstwy.
- Witaj **PremiumRS** warstwa oferuje wydajność hello hello **Premium** warstwy koszt będzie niższy koszt, ale z ograniczonymi umowy SLA.

> [!IMPORTANT]
> Przejrzyj hello [puli elastycznej SQL](sql-database-elastic-pool.md) tematu hello szczegółowe informacje na temat grupowanie baz danych w SQL elastyczne pule tooshare zasoby obliczeniowe i magazynujące. Witaj pozostałej części w tym temacie skupiono się na warstwy usług i poziomy wydajności dla pojedynczej bazy danych.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>Warstwy usług i poziomy wydajności pojedynczej bazy danych
Dla pojedynczej bazy danych istnieje wiele poziomów wydajności i ilości pamięci masowej w poszczególnych warstwach usług. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>Skalowanie pojedynczej bazy danych w górę lub w dół

Po początkowym wybraniu warstwy usług i poziomu wydajności możesz dynamicznie skalować pojedynczą bazę danych w górę lub w dół na podstawie rzeczywistego użycia.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

Zmiana hello poziomu warstwy i/lub wydajności usługi bazy danych tworzy replikę hello oryginalnej bazy danych na nowy poziom wydajności hello, a następnie przełącza połączeń toohello repliki. W trakcie tego procesu nie zostały utracone żadne dane, ale podczas hello krótki chwilę po przełączyć możemy toohello repliki bazy danych toohello połączeń są wyłączone, więc niektóre transakcje w locie może zostać przywrócona. Hello długość czasu dla przełącznika hello za pośrednictwem zmienia się, ale jest zazwyczaj mniej niż 30 sekund 99% czasu hello jest w sekcji 4 sekundy. W przypadku dużej liczby transakcji w locie na powitania obecnie połączeń są wyłączone, hello czas przełącznika hello za pośrednictwem może trwać dłużej.  

czas trwania Hello hello cały proces skalowania w górę zależy od rozmiaru zarówno hello i warstwy usługi dla hello bazy danych przed i po zmianie hello. Na przykład zmienienie bazy danych o rozmiarze 250 GB z warstwy Standardowa, na warstwę Standardowa lub w obrębie warstwy Standardowa powinno zająć maksymalnie 6 godzin. Bazy danych o hello samej wielkości, który jest zmiana poziomów wydajności w ramach warstwy usług Premium hello, należy zakończyć w ciągu 3 godziny.

> [!TIP]
> toocheck stanu hello skalowanie operacji trwającą bazy danych SQL, można użyć hello następujące zapytania: ```select * from sys.dm_operation_status```.
>

* Jeśli uaktualniasz tooa wyższej warstwy lub wydajności poziomu usług hello maksymalny rozmiar bazy danych nie zwiększa chyba że jawnie określ większy rozmiar maksymalny.
* toodowngrade bazy danych, hello bazy danych musi być mniejszy niż maksymalny dozwolony rozmiar hello warstwy usługi docelowej hello. 
* Podczas uaktualniania bazy danych o [— replikacja geograficzna](sql-database-geo-replication-portal.md) włączone, Uaktualnij tą warstwą żądaną wydajność toohello pomocniczej bazy danych przed uaktualnieniem hello podstawowej bazy danych (ogólne wskazówki). Podczas uaktualniania różnych tooa dodatkowej bazy danych wersji ugrading hello najpierw jest wymagana. 
* Podczas zmiany na starszą wersję bazy danych o [— replikacja geograficzna](sql-database-geo-replication-portal.md) włączone, obniżyć jej warstwy żądaną wydajność toohello głównej bazy danych przed przejściem hello dodatkowej bazy danych (ogólne wskazówki). Podczas zmiany na starszą wersję tooa różnych, konieczne jest najpierw edition starszą wersję hello podstawowej bazy danych. 

* Witaj przywracania oferty usług są różne dla hello różnych warstwach usług. Jeśli są obniżenie toohello **podstawowe** warstwy, konieczne będzie krótszym okresie przechowywania kopii zapasowych — Zobacz [kopie zapasowe bazy danych SQL Azure](sql-database-automated-backups.md).
* nowe właściwości Hello hello bazy danych nie są stosowane dopiero po zakończeniu zmiany hello.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>Bieżące ograniczenia P11 i P15 z replikacją baz danych, maxsize 4 TB

Maksymalny rozmiar 4 TB P11 i P15 z replikacją bazy danych jest obsługiwana w pewnych regionach (wspomnianej wcześniej). Witaj następujące zagadnienia i ograniczenia tooP11 i stosowane P15 z replikacją baz danych, maxsize 4 TB:

- Wybranie opcji maxsize 4 TB hello podczas tworzenia bazy danych (przy użyciu wartość 4 TB lub 4096 GB) hello Utwórz polecenie kończy się niepowodzeniem z powodu błędu, jeśli baza danych hello jest obsługiwana w nieobsługiwany region.
- Dla istniejących P11 P15 z replikacją baz danych i znajduje się w jednym z hello obsługiwane regiony można zwiększyć hello maxsize magazynu too4 TB. Można to sprawdzić za pomocą hello [wybierz DATABASEPROPERTYEX](https://msdn.microsoft.com/library/ms186823.aspx) lub sprawdzając hello rozmiar bazy danych w hello portalu Azure. Uaktualnianie istniejącego P11 lub P15 z replikacją bazy danych można wykonać tylko członkowie roli bazy danych dbmanager: hello lub głównego identyfikatora logowania poziomu serwera. 
- Jeśli operacja uaktualnienia jest wykonywane w natychmiast zaktualizować konfiguracji hello obsługiwanym regionie. podczas procesu uaktualniania hello Hello bazy danych pozostaje w trybie online. Jednak nie można korzystać z pełnej hello 4 TB pamięci masowej, dopóki hello rzeczywistej bazy danych pliki zostały uaktualnione toohello nowe maxsize. Długość Hello wymagany zależy od rozmiaru hello hello bazy danych trwa uaktualnianie.  
- Podczas tworzenia lub aktualizowania P11 lub P15 z replikacją bazy danych, można wybrać tylko między 1 TB i 4 TB maxsize. Pośredni magazyn o rozmiarze nie są obecnie obsługiwane. Podczas tworzenia P11/P15, hello domyślna opcja magazynowania 1 TB jest wstępnie wybrane. W przypadku baz danych znajdujących się w jednym z hello obsługiwane regiony można zwiększyć hello too4TB maksymalną magazynu do nowego lub istniejącego pojedynczej bazy danych. Dla wszystkich innych regionów nie można zwiększyć maksymalny rozmiar w ponad 1 TB. Cena Hello nie zmienia się po wybraniu 4 TB pamięci masowej uwzględnione.
- Witaj 4 TB maxsize bazy danych nie może być zmienione too1 TB nawet jeśli hello przechowywania używane jest poniżej 1 TB. W związku z tym nie można obniżyć tooa P11 - 4 TB/P15 - 4 TB P11 - 1 TB/P15 - 1 TB lub dolnej warstwy wydajności na przykład P6 tooP1) do momentu zapewniamy opcje dodatkowe miejsce do magazynowania hello reszty hello warstwy wydajności. To ograniczenie obowiązuje również toohello przywracania i kopiowania scenariusze, w tym punkcie w czasie, przywracanie geograficznie, długo-długoterminowego — kopia zapasowa przechowywania i kopii bazy danych. Po skonfigurowaniu bazy danych z opcją 4 TB hello wszystkie operacje przywracania bazy danych musi być uruchamiane w P11/P15 z maxsize 4 TB.
- Podczas tworzenia lub uaktualniania bazy danych programu P11/P15 nieobsługiwany region hello Tworzenie lub operacji uaktualniania kończy się niepowodzeniem z hello następujący komunikat o błędzie: **P11 P15 z replikacją bazy danych i z zapasowej too4TB magazynu są dostępne w East2 nam, zachodnie stany USA, Virginia nam wersji dla instytucji rządowych Europa Zachodnia, Niemcy środkowe południowo Azja Wschodnia, Japonia Wschodnia, Australia Wschodnia, Kanada Środkowa i Kanada Wschodnia.**
- Aktywna replikacja geograficzna scenariuszach:
   - Definiowanie relacji — replikacja geograficzna: w przypadku P11 lub P15 hello podstawowej bazy danych hello secondary(ies) musi być także P11 lub P15; niższe poziomy wydajności są odrzucane jako pomocnicze bazy danych, ponieważ nie może obsłużyć 4 TB.
   - Uaktualnianie hello podstawowej bazy danych w relacji replikacji geograficznej: zmiana hello maxsize too4 TB w podstawowej bazy danych wyzwala hello same zmiany na powitania dodatkowej bazy danych. Obu uaktualnień musi zakończyć się powodzeniem, zmiana hello hello głównej tootake efekt. Region dla opcji 4TB hello ograniczeniom (zobacz powyżej). Hello dodatkowej znajduje się w regionie, który nie obsługuje 4 TB, hello podstawowy nie jest uaktualniany.
- Za pomocą usługi Import/Eksport hello ładowania P11 - 4TB/P15 - 4TB bazy danych nie jest obsługiwane. Za pomocą SqlPackage.exe[zaimportować](sql-database-import.md) i [wyeksportować](sql-database-export.md) danych.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-portal"></a>Zarządzanie pojedynczej bazy danych warstwy usług i poziomy wydajności przy użyciu hello portalu Azure

tooset lub zmień hello warstwy usług, poziom wydajności lub wielkość magazynu dla nowego lub istniejącego Azure bazy danych SQL przy użyciu hello portalu Azure, otwórz hello **skonfigurować wydajności** okna bazy danych, klikając  **Warstwa cenowa (skala Dtu)** — pokazane na powitania po zrzut ekranu. 

- Ustawianie lub zmienianie warstwy usług hello wybierając hello warstwy usługi dla obciążenia. 
- Ustaw lub zmień poziom wydajności hello (**Dtu**) w ramach warstwy usług przy użyciu hello **jednostek dtu w warstwie** suwaka.
- Ustawianie lub zmienianie hello wielkość magazynu na poziomie wydajności hello przy użyciu hello **magazynu** suwaka. 

  ![Konfigurowanie usługi warstwę i poziom wydajności](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> Przegląd [bieżące ograniczenia P11 i P15 z replikacją baz danych z 4 TB maxsize](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize) podczas wybierania P11 lub P15 warstwy usług.
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>Zarządzanie pojedynczej bazy danych warstwy usług i poziomy wydajności przy użyciu programu PowerShell

tooset lub zmień warstwach usług bazy danych Azure SQL, poziomów wydajności i wielkość magazynu przy użyciu programu PowerShell, użyj hello następującego polecenia cmdlet programu PowerShell. Jeśli konieczne tooinstall lub uaktualnić programu PowerShell, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps). 

| Polecenie cmdlet | Opis |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Tworzy bazę danych |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Pobiera jeden lub więcej baz danych|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Ustawia właściwości dla bazy danych lub przenosi istniejącą bazę danych do puli elastycznej|


> [!TIP]
> Aby uzyskać przykładowy skrypt programu PowerShell, który monitoruje hello metryki wydajności bazy danych, skaluje go tooa wyższy poziom wydajności i tworzy regułę alertu w jednym z hello metryki wydajności, zobacz [monitora i skali pojedynczego SQL bazy danych przy użyciu PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).

## <a name="manage-single-database-service-tiers-and-performance-levels-using-hello-azure-cli"></a>Zarządzanie pojedynczej bazy danych warstwy usług i poziomy wydajności przy użyciu hello wiersza polecenia platformy Azure

tooset lub zmień warstwach usług bazy danych Azure SQL, poziomów wydajności i wielkość magazynu przy użyciu hello wiersza polecenia platformy Azure, użyj następujących hello [bazy danych SQL interfejsu wiersza polecenia Azure](/cli/azure/sql/db) poleceń. Użyj hello [powłoki chmury](/azure/cloud-shell/overview) toorun hello interfejsu wiersza polecenia w przeglądarce lub [zainstalować](/cli/azure/install-azure-cli) go na system macOS, Linux lub Windows. Do tworzenia i zarządzania pule elastyczne SQL, zobacz [pule elastyczne](sql-database-elastic-pool.md).

| Polecenie cmdlet | Opis |
| --- | --- |
|[Tworzenie bazy danych sql az](/cli/azure/sql/db#create) |Tworzy bazę danych|
|[Lista bazy danych sql az](/cli/azure/sql/db#list)|Wyświetla listę wszystkich baz danych i magazynów danych na serwerze lub wszystkie bazy danych w puli elastycznej|
|[Lista wersje az bazy danych sql](/cli/azure/sql/db#list-editions)|Wyświetla dostępne usługi cele i limity magazynu|
|[bazy danych sql az listy użycia](/cli/azure/sql/db#list-usages)|Zwraca bazy danych użycia|
|[Pokaż bazy danych sql az](/cli/azure/sql/db#show)|Pobiera Magazyn bazy danych lub danych|
|[Aktualizacja bazy danych sql az](/cli/azure/sql/db#update)|Aktualizuje bazę danych|

> [!TIP]
> Aby uzyskać skrypt wiersza polecenia platformy Azure, która może obsłużyć jeden poziom wydajności różnych tooa bazy danych Azure SQL po podczas badania informacji o rozmiarze hello hello bazy danych, zobacz [toomonitor Użyj interfejsu wiersza polecenia i skalowania pojedynczej bazy danych SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Zarządzanie pojedynczej bazy danych warstwy usług i poziomy wydajności przy użyciu języka Transact-SQL

tooset lub zmień warstwach usług bazy danych Azure SQL, poziomów wydajności i ilości pamięci masowej do języka Transact-SQL, użyj hello następujące polecenia T-SQL. Możesz wykonywać te polecenia przy użyciu hello portalu Azure, [programu SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), lub inny program, który można połączyć z serwerem bazy danych SQL Azure tooan i przekazać języka Transact-SQL polecenia. 

| Polecenie | Opis |
| --- | --- |
|[Utwórz bazę danych (baza danych Azure SQL)](/sql/t-sql/statements/create-database-azure-sql-database)|Tworzy nową bazę danych. Musi być połączony toohello bazy danych master toocreate nową bazę danych.|
| [ALTER DATABASE (baza danych Azure SQL)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modyfikuje bazy danych Azure SQL. |
|[sys.database_service_objectives (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Zwraca hello edition (warstwy usług), celem usługi (warstwa cenowa) i nazwę puli elastycznej dla bazy danych Azure SQL lub usługi Azure SQL Data Warehouse. Jeśli zalogowany toohello głównej bazy danych na serwerze bazy danych SQL Azure, zwraca informacje o wszystkich baz danych. Dla usługi Azure SQL Data Warehouse musi być połączony toohello bazy danych master.|
|[sys.database_usage (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Wyświetla liczbę hello, typ i czas trwania baz danych na serwerze bazy danych SQL Azure.|

Witaj poniższy przykład przedstawia hello maxsize zmieniane przy użyciu polecenia ALTER DATABASE hello:

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-hello-rest-api"></a>Zarządzanie za pomocą interfejsu API REST hello pojedynczych baz danych

tooset lub zmień warstwach usług bazy danych Azure SQL, poziomów wydajności i wielkość magazynu przy użyciu hello interfejsu API REST, zobacz [interfejsu API REST bazy danych SQL Azure](/rest/api/sql/).

## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o [Dtu](sql-database-what-is-a-dtu.md).
* toolearn o monitorowaniu użycie jednostek DTU zobacz [monitorowania i dostrajania wydajności](sql-database-troubleshoot-performance.md).

