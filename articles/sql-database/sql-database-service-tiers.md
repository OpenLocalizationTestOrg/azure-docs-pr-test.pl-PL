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
ms.openlocfilehash: b25ff5331f119efd44c61808f7d1d5decb226bd6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="what-performance-options-are-available-for-an-azure-sql-database"></a>Jakie opcje wydajności są dostępne dla bazy danych SQL Azure

[Baza danych SQL Azure](sql-database-technical-overview.md) oferuje cztery warstwy usługi dla obu jednym i [puli](sql-database-elastic-pool.md) baz danych. Te warstwy usług są: **podstawowe**, **standardowe**, **Premium**, i **Premium RS**. W poszczególnych warstwach usług są wiele poziomów wydajności ([Dtu](sql-database-what-is-a-dtu.md)) i opcje magazynu do obsługi różnych rozmiarach obciążeń i danych. Wyższe poziomy wydajności zapewnienia jej dodatkowych zasobów obliczeniowych i przestrzeni dyskowej na celu zapewnienie coraz większej przepustowości i pojemności. Można zmienić warstwy usług, poziomów wydajności i magazynu dynamicznie bez przestojów. 
- **Podstawowe**, **standardowe** i **Premium** wszystkie warstwy usług ma przestojów SLA 99.99%, elastyczne opcje ciągłości działania, funkcje zabezpieczeń i rozliczenia godzinowe. 
- **Premium RS** warstwy zapewnia te same poziomy wydajności warstwy Premium z obniżonych umowy SLA, ponieważ będzie ona uruchamiana z mniejszą liczbę nadmiarowe kopie niż bazy danych w innej warstwy usługi. Tak w przypadku awarii usługi, należy odzyskać bazę danych z kopii zapasowej z maksymalnie opóźnienie 5 minut.

> [!IMPORTANT]
> Baza danych Azure SQL pobiera zagwarantowany zestaw zasobów i ich oczekiwane charakterystyki bazy danych nie dotyczy innych bazy danych w obrębie platformy Azure. 

## <a name="choosing-a-service-tier"></a>Wybieranie warstwy usług
Tabela poniżej zawiera przykłady warstw najlepiej dopasowane do różnych obciążeń aplikacji.

| Warstwa usług | Docelowe obciążenia |
| :--- | --- |
| **Podstawowa** | Najodpowiedniejsza dla małych baz danych. Standardowo zapewnia obsługę jednej aktywnej operacji w danym momencie. Przykłady zastosowania to bazy danych używane do tworzenia i testowania oprogramowania lub niewielkie, rzadko używane aplikacje. |
| **Standardowa** |Najczęściej wybierana opcja dla aplikacji w chmurze z niewielkimi lub średnimi wymaganiami dotyczącymi wydajności operacji we/wy i obsługą wielu równoczesnych zapytań. Przykładowe zastosowania to aplikacje grupy roboczej lub sieci Web. |
| **Premium** | Przeznaczona dla dużych ilości transakcji z wysokimi wymaganiami dotyczącymi wydajności operacji we/wy przy obsłudze wielu równoczesnych użytkowników. Przykładem zastosowania mogą być bazy danych dla aplikacji o znaczeniu krytycznym. |
| **R — wersja Premium** | Przeznaczona dla obciążeń intensywnie wykonujących operacje We/Wy, które nie wymagają gwarancje najwyższą dostępność. Przykłady obejmują testowanie obciążeń wysokiej wydajności lub obciążenia analitycznych, gdzie bazy danych nie jest systemem rekordu. |
|||

Możesz utworzyć pojedynczych baz danych z dedykowanym zasobów w ramach warstwy usług na określonym [poziom wydajności](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) lub baz danych można również utworzyć [puli elastycznej SQL](sql-database-service-tiers.md#elastic-pool-service-tiers-and-performance-in-edtus). W puli elastycznej SQL zasobów obliczeniowych i przestrzeni dyskowej są współdzielone przez wiele baz danych w ramach pojedynczego serwera logicznego. 

Zasoby dostępne dla pojedynczej bazy danych są wyrażone w jednostki transakcji bazy danych (Dtu) i zasobów dla pul elastycznych SQL są wyrażane w postaci liczby jednostek transakcji elastycznej bazy danych (Edtu). Aby uzyskać więcej informacji na temat jednostek Dtu a Edtu, zobacz [co to są Dtu a Edtu?](sql-database-what-is-a-dtu.md).

Wybierając warstwę usług, rozpocznij od ustalenia minimalnego potrzebnego zakresu funkcji bazy danych:

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
> Magazyn do 4 TB jest obecnie dostępna w następujących regionach: East2 nam, zachodnie stany USA, Virginia nam wersji dla instytucji rządowych, Europa Zachodnia, Niemcy centralnej, Południowej, Azja Wschodnia, Japonia Wschodnia, Australia Wschodnia, Kanada centralnej i Kanada Wschodnia. Zobacz [ograniczenia bieżącego 4 TB](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize)
>

Po określeniu warstwy odpowiednią usługę, można przystąpić do określenia poziomu wydajności (liczba jednostek Dtu) i wielkość pamięci masowej dla bazy danych. 

- Poziomy wydajności S2 i S3 w **standardowe** warstwy są często dobry punkt wyjścia. 
- W przypadku baz danych wysokiego procesora CPU lub we/wy, wydajność poziomy w **Premium** warstwy są prawo punkt początkowy. 
- **Premium** warstwy oferuje więcej procesora CPU i rozpoczyna się od 10 x więcej operacji We/Wy w porównaniu do najwyższej wydajności w **standardowe** warstwy.
- **PremiumRS** warstwa oferuje wydajność **Premium** warstwy koszt będzie niższy koszt, ale z ograniczonymi umowy SLA.

> [!IMPORTANT]
> Przegląd [puli elastycznej SQL](sql-database-elastic-pool.md) tematu, aby uzyskać szczegółowe informacje o grupowanie baz danych w pule elastyczne SQL do udostępniania zasobów obliczeniowych i przestrzeni dyskowej. W pozostałej części w tym temacie skupiono się na warstwy usług i poziomy wydajności dla pojedynczej bazy danych.
>

## <a name="single-database-service-tiers-and-performance-levels"></a>Warstwy usług i poziomy wydajności pojedynczej bazy danych
Dla pojedynczej bazy danych istnieje wiele poziomów wydajności i ilości pamięci masowej w poszczególnych warstwach usług. 

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

## <a name="scaling-up-or-scaling-down-a-single-database"></a>Skalowanie pojedynczej bazy danych w górę lub w dół

Po początkowym wybraniu warstwy usług i poziomu wydajności możesz dynamicznie skalować pojedynczą bazę danych w górę lub w dół na podstawie rzeczywistego użycia.  

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-dynamically-scale-up-or-scale-down/player]
>

Zmienienie warstwy usług i/lub poziomu wydajności bazy danych powoduje utworzenie repliki oryginalnej bazy danych na nowym poziomie wydajności, a następnie przełączenie połączeń do repliki. Podczas tego procesu nie zostaną utracone żadne dane, ale podczas przełączania do repliki połączenia do bazy danych są chwilowo wyłączane, dlatego niektóre bieżące transakcje mogą zostać wycofane. Czas dla przełącznika za pośrednictwem zmienia się, ale zazwyczaj w sekcji 4 sekundy jest mniej niż 30 sekund 99% czasu. W przypadku dużej liczby transakcji transmitowane w chwili połączenia są wyłączone, czas za pośrednictwem przełącznika może trwać dłużej.  

Czas trwania całego procesu skalowania w górę zależy zarówno od rozmiaru, jak i warstwy usług bazy danych przed zmianą oraz po niej. Na przykład zmienienie bazy danych o rozmiarze 250 GB z warstwy Standardowa, na warstwę Standardowa lub w obrębie warstwy Standardowa powinno zająć maksymalnie 6 godzin. Zmiana poziomów wydajności bazy danych o tym samym rozmiarze w obrębie warstwy Premium powinno zająć maksymalnie 3 godziny.

> [!TIP]
> Aby sprawdzić stan operacji skalowania trwającą bazy danych SQL, można użyć następującej kwerendy: ```select * from sys.dm_operation_status```.
>

* Jeśli uaktualniasz do wyższego poziomu wydajności ani warstwy usługi, maksymalny rozmiar bazy danych nie zwiększa chyba że jawnie określ większy rozmiar maksymalny.
* Na starszą wersję bazy danych, bazy danych musi być mniejszy niż maksymalny dozwolony rozmiar warstwy usługi docelowej. 
* Podczas uaktualniania bazy danych o [— replikacja geograficzna](sql-database-geo-replication-portal.md) włączone, Uaktualnij swoje pomocniczej bazy danych do warstwy żądaną wydajność przed uaktualnieniem podstawowej bazy danych (ogólne wskazówki). Podczas uaktualniania do ugrading innej wersji, konieczne jest najpierw dodatkowej bazy danych. 
* Podczas zmiany na starszą wersję bazy danych o [— replikacja geograficzna](sql-database-geo-replication-portal.md) włączone, obniżyć jego głównej bazy danych do warstwy żądaną wydajność przed przejściem dodatkowej bazy danych (ogólne wskazówki). Podczas zmiany na starszą wersję do innej wersji zmiana wersji na starszą podstawowej bazy danych jest wymagana. 

* Oferowane usługi przywracania różnią się w zależności do warstwy usług. Jeśli są powrót do subskrypcji **podstawowe** warstwy, konieczne będzie krótszym okresie przechowywania kopii zapasowych — Zobacz [kopie zapasowe bazy danych SQL Azure](sql-database-automated-backups.md).
* Nowe właściwości bazy danych są stosowane dopiero po zakończeniu wprowadzania zmian.


## <a name="current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize"></a>Bieżące ograniczenia P11 i P15 z replikacją baz danych, maxsize 4 TB

Maksymalny rozmiar 4 TB P11 i P15 z replikacją bazy danych jest obsługiwana w pewnych regionach (wspomnianej wcześniej). Następujące zagadnienia i ograniczenia dotyczą P11 i P15 z replikacją baz danych, maxsize 4 TB:

- Jeśli zostanie wybrana opcja maxsize 4 TB, podczas tworzenia bazy danych (przy użyciu wartość 4 TB lub 4096 GB), polecenia create kończy się niepowodzeniem z powodu błędu Jeśli bazy danych jest obsługiwana w nieobsługiwany region.
- Dla istniejących P11 P15 z replikacją baz danych i znajduje się w jednym z obsługiwanych regionów możesz zwiększyć magazynu maxsize 4 TB. Można to sprawdzić za pomocą [wybierz DATABASEPROPERTYEX](https://msdn.microsoft.com/library/ms186823.aspx) lub sprawdzając rozmiar bazy danych w portalu Azure. Uaktualnianie istniejącego P11 lub P15 z replikacją bazy danych można wykonać tylko przez głównego identyfikatora logowania poziomu serwera lub członków dbmanager: roli bazy danych. 
- Jeśli operacja uaktualnienia jest wykonywane w obsługiwanym regionie natychmiast zaktualizować konfigurację. Podczas procesu uaktualniania bazy danych pozostaje w trybie online. Nie można jednak wykorzystywać pełne 4 TB pamięci masowej aż pliki bazy danych rzeczywistych zostały uaktualnione do nowej maxsize. Wymagany czas zależy od rozmiaru bazy danych trwa uaktualnianie.  
- Podczas tworzenia lub aktualizowania P11 lub P15 z replikacją bazy danych, można wybrać tylko między 1 TB i 4 TB maxsize. Pośredni magazyn o rozmiarze nie są obecnie obsługiwane. Podczas tworzenia P11/P15, wstępnie wybrane jest domyślną opcją 1 TB pamięci masowej. W przypadku baz danych znajdujących się w jednym z obsługiwanych regionów może zwiększyć maksymalną magazynu do 4TB dla nowego lub istniejącego pojedynczej bazy danych. Dla wszystkich innych regionów nie można zwiększyć maksymalny rozmiar w ponad 1 TB. Cena nie zmienia się po wybraniu 4 TB pamięci masowej uwzględnione.
- Nie można zmienić 4 TB maxsize bazy danych do 1 TB, nawet jeśli jest używane przechowywania poniżej 1 TB. W związku z tym użytkownik nie może obniżyć poziom P11 - 4 TB/P15 - 4 TB P11 - 1 TB/P15 - 1 TB lub dolnej warstwy wydajności na przykład P1 P6) do momentu zapewniamy opcje dodatkowe miejsce do magazynowania w pozostałej części warstwy wydajności. To ograniczenie ma zastosowanie również do przywracania i kopiowania scenariusze, w tym punkcie w czasie, przywracanie geograficznie, długo-długoterminowego — kopia zapasowa przechowywania i kopii bazy danych. Po skonfigurowaniu bazy danych z opcją 4 TB wszystkie operacje przywracania bazy danych musi być uruchamiane w P11/P15 z maxsize 4 TB.
- Podczas tworzenia lub uaktualniania bazy danych programu P11/P15 nieobsługiwany region, tworzenie lub aktualizacja kończy się niepowodzeniem z powodu następującego błędu: **P11 i P15 z replikacją bazy danych z maksymalnie 4 TB pamięci masowej są dostępne w Virginia nam wersji dla instytucji rządowych nam East2, zachodnie stany USA, zachód Europa, Niemcy środkowe południowo Azja Wschodnia, Japonia Wschodnia, Australia Wschodnia, Kanada Środkowa i Kanada Wschodnia.**
- Aktywna replikacja geograficzna scenariuszach:
   - Definiowanie relacji — replikacja geograficzna: Jeśli podstawowa baza danych jest P11 lub P15 z replikacją, secondary(ies) musi być także P11 lub P15; niższe poziomy wydajności są odrzucane jako pomocnicze bazy danych, ponieważ nie może obsłużyć 4 TB.
   - Uaktualnianie podstawowej bazy danych w relacji replikacji geograficznej: Zmiana parametru maxsize do 4 TB w głównej bazie danych wyzwala te same zmiany w pomocniczej bazie danych. Obu uaktualnień musi zakończyć się powodzeniem zmiany na serwerze podstawowym zaczęły obowiązywać. Region dla opcji 4TB ograniczeniom (zobacz powyżej). Pomocniczy znajduje się w regionie, który nie obsługuje 4 TB, podstawowy nie jest uaktualniany.
- Za pomocą usługi Import/Eksport ładowania P11 - 4TB/P15 - 4TB bazy danych nie jest obsługiwane. Użyj SqlPackage.exe do [zaimportować](sql-database-import.md) i [wyeksportować](sql-database-export.md) danych.

## <a name="manage-single-database-service-tiers-and-performance-levels-using-the-azure-portal"></a>Zarządzanie pojedynczej bazy danych warstwy usług i poziomy wydajności przy użyciu portalu Azure

Aby ustawić lub zmienić warstwę usługi, poziom wydajności lub wielkość magazynu do nowego lub istniejącego Azure bazy danych SQL przy użyciu portalu Azure, otwórz **skonfigurować wydajności** okna bazy danych, klikając **(warstwy cenowej Skalowanie Dtu)** — jak pokazano na poniższym zrzucie ekranu. 

- Ustawianie lub zmienianie warstwy usług, wybierając warstwy usługi dla obciążenia. 
- Ustaw lub zmień poziom wydajności (**Dtu**) w warstwie usługi za pomocą **jednostek dtu w warstwie** suwaka.
- Ustaw lub zmień wielkość pamięci masowej dla poziomu wydajności za pomocą **magazynu** suwaka. 

  ![Konfigurowanie usługi warstwę i poziom wydajności](./media/sql-database-service-tiers/service-tier-performance-level.png)

> [!IMPORTANT]
> Przegląd [bieżące ograniczenia P11 i P15 z replikacją baz danych z 4 TB maxsize](sql-database-service-tiers.md#current-limitations-of-p11-and-p15-databases-with-4-tb-maxsize) podczas wybierania P11 lub P15 warstwy usług.
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-powershell"></a>Zarządzanie pojedynczej bazy danych warstwy usług i poziomy wydajności przy użyciu programu PowerShell

Ustawianie lub zmienianie bazy danych Azure SQL warstwy usług, poziomów wydajności i wielkość magazynu przy użyciu programu PowerShell, użyj następujących poleceń cmdlet programu PowerShell. Jeśli musisz zainstalować lub uaktualnić programu PowerShell, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps). 

| Polecenie cmdlet | Opis |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Tworzy bazę danych |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Pobiera jeden lub więcej baz danych|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Ustawia właściwości dla bazy danych lub przenosi istniejącą bazę danych do puli elastycznej|


> [!TIP]
> Aby uzyskać przykładowy skrypt programu PowerShell, który monitoruje metryki wydajności bazy danych, skaluje go na wyższy poziom wydajności i tworzy regułę alertu w jednym z metryki wydajności, zobacz [monitora i skali pojedynczego SQL bazy danych przy użyciu programu PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).

## <a name="manage-single-database-service-tiers-and-performance-levels-using-the-azure-cli"></a>Zarządzanie pojedynczej bazy danych warstwy usług i poziomy wydajności przy użyciu wiersza polecenia platformy Azure

Aby ustawić lub zmienić bazy danych Azure SQL warstwy usług, poziomów wydajności i wielkość magazynu przy użyciu wiersza polecenia platformy Azure, należy użyć następującego [bazy danych SQL interfejsu wiersza polecenia Azure](/cli/azure/sql/db) poleceń. Używaj usługi [Cloud Shell](/azure/cloud-shell/overview), aby uruchamiać interfejs wiersza polecenia w przeglądarce, albo [zainstaluj](/cli/azure/install-azure-cli) go w systemie macOS, Linux lub Windows. Do tworzenia i zarządzania pule elastyczne SQL, zobacz [pule elastyczne](sql-database-elastic-pool.md).

| Polecenie cmdlet | Opis |
| --- | --- |
|[Tworzenie bazy danych sql az](/cli/azure/sql/db#create) |Tworzy bazę danych|
|[Lista bazy danych sql az](/cli/azure/sql/db#list)|Wyświetla listę wszystkich baz danych i magazynów danych na serwerze lub wszystkie bazy danych w puli elastycznej|
|[Lista wersje az bazy danych sql](/cli/azure/sql/db#list-editions)|Wyświetla dostępne usługi cele i limity magazynu|
|[bazy danych sql az listy użycia](/cli/azure/sql/db#list-usages)|Zwraca bazy danych użycia|
|[Pokaż bazy danych sql az](/cli/azure/sql/db#show)|Pobiera Magazyn bazy danych lub danych|
|[Aktualizacja bazy danych sql az](/cli/azure/sql/db#update)|Aktualizuje bazę danych|

> [!TIP]
> Aby uzyskać skrypt wiersza polecenia platformy Azure, która może obsłużyć pojedynczej bazy danych Azure SQL do poziomu wydajności różnych po podczas badania informacji rozmiar bazy danych, zobacz [Użyj interfejsu wiersza polecenia, aby monitorować i skalowania pojedynczej bazy danych SQL](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-single-database-service-tiers-and-performance-levels-using-transact-sql"></a>Zarządzanie pojedynczej bazy danych warstwy usług i poziomy wydajności przy użyciu języka Transact-SQL

Ustawianie lub zmienianie bazy danych Azure SQL warstwy usług, poziomów wydajności i ilości pamięci masowej do języka Transact-SQL, użyj następujących poleceń T-SQL. Te polecenia przy użyciu portalu Azure może wystawiać [programu SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), lub inny program, który może nawiązywać połączenia z serwerem bazy danych SQL Azure i przekazać języka Transact-SQL polecenia. 

| Polecenie | Opis |
| --- | --- |
|[Utwórz bazę danych (baza danych Azure SQL)](/sql/t-sql/statements/create-database-azure-sql-database)|Tworzy nową bazę danych. Musisz mieć połączenie z główną bazą danych, aby utworzyć nową bazę danych.|
| [ALTER DATABASE (baza danych Azure SQL)](/sql/t-sql/statements/alter-database-azure-sql-database) |Modyfikuje bazy danych Azure SQL. |
|[sys.database_service_objectives (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Zwraca edition (warstwy usług), celem usługi (warstwa cenowa) i nazwę puli elastycznej dla bazy danych Azure SQL lub usługi Azure SQL Data Warehouse. Jeśli zalogowany do głównej bazy danych na serwerze bazy danych SQL Azure, zwraca informacje o wszystkich baz danych. Dla usługi Azure SQL Data Warehouse musi być podłączony do bazy danych master.|
|[sys.database_usage (baza danych SQL Azure)](/sql/relational-databases/system-catalog-views/sys-database-usage-azure-sql-database)|Wyświetla liczbę, typ i czas trwania baz danych na serwerze bazy danych SQL Azure.|

W poniższym przykładzie przedstawiono parametr maxsize zmieniane przy użyciu polecenia ALTER DATABASE:

 ```sql
ALTER DATABASE <myDatabaseName> 
   MODIFY (MAXSIZE = 4096 GB);
```

## <a name="manage-single-databases-using-the-rest-api"></a>Zarządzanie pojedynczych baz danych przy użyciu interfejsu API REST

Aby ustawić lub zmienić warstwy usługi bazy danych Azure SQL, poziomów wydajności i wielkość magazynu przy użyciu interfejsu API REST, zobacz [interfejsu API REST bazy danych SQL Azure](/rest/api/sql/).

## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej o [Dtu](sql-database-what-is-a-dtu.md).
* Aby dowiedzieć się więcej na temat monitorowania użycia jednostek dtu w warstwie, zobacz [monitorowania i dostrajania wydajności](sql-database-troubleshoot-performance.md).

