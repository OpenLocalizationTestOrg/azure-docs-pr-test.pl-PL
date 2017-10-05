---
title: "Zarządzanie danych historycznych w tabelach danych czasowych z zasadami przechowywania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać zasad przechowywania danych tymczasowych do przechowywania danych historycznych pod kontrolą."
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: 8975d7a7d39114b2758d64a4df9f992cba6bf561
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="2b35b-103">Zarządzanie danych historycznych w tabelach danych czasowych z zasady przechowywania</span><span class="sxs-lookup"><span data-stu-id="2b35b-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="2b35b-104">Tabele danych czasowych może zwiększyć baz danych o rozmiarze ponad zwykłych tabelach, zwłaszcza jeśli przechowywanie danych historycznych przez dłuższy okres.</span><span class="sxs-lookup"><span data-stu-id="2b35b-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="2b35b-105">W związku z tym zasady przechowywania danych historycznych jest istotnym elementem planowania i zarządzanie cyklem życia każda tabela danych czasowych.</span><span class="sxs-lookup"><span data-stu-id="2b35b-105">Hence, retention policy for historical data is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="2b35b-106">Tabele danych czasowych w bazie danych SQL Azure pochodzą z mechanizmem przechowywania łatwy w użyciu, który ułatwia wykonywanie tego zadania.</span><span class="sxs-lookup"><span data-stu-id="2b35b-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="2b35b-107">Przechowywania historii danych czasowych może być skonfigurowana na poziomie pojedynczej tabeli, która umożliwia użytkownikom tworzenie elastycznych przedawnienia zasady.</span><span class="sxs-lookup"><span data-stu-id="2b35b-107">Temporal history retention can be configured at the individual table level, which allows users to create flexible aging polices.</span></span> <span data-ttu-id="2b35b-108">Stosowanie przechowywania danych czasowych jest prosty: wymaga tylko jeden parametr należy ustawić podczas zmiany schematu lub tworzenia tabeli.</span><span class="sxs-lookup"><span data-stu-id="2b35b-108">Applying temporal retention is simple: it requires only one parameter to be set during table creation or schema change.</span></span>

<span data-ttu-id="2b35b-109">Po zdefiniowaniu zasad przechowywania bazy danych SQL Azure rozpoczyna regularnie sprawdzanie, czy istnieją historyczne wierszy, które kwalifikują się do czyszczenia danych.</span><span class="sxs-lookup"><span data-stu-id="2b35b-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="2b35b-110">Identyfikacja pasujących wierszy i ich usunięcia z tabeli historii występować w sposób niewidoczny dla użytkownika, w zadania w tle, który jest zaplanowane i uruchamiane przez system.</span><span class="sxs-lookup"><span data-stu-id="2b35b-110">Identification of matching rows and their removal from the history table occur transparently, in the background task that is scheduled and run by the system.</span></span> <span data-ttu-id="2b35b-111">Warunek wieku wiersze tabeli historii zaznaczono oparte na kolumnie reprezentujący koniec okresu SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="2b35b-111">Age condition for the history table rows is checked based on the column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="2b35b-112">Jeśli okres przechowywania, na przykład ustawiono sześciu miesięcy, kwalifikuje się do oczyszczania wiersze tabeli spełniają następujący warunek:</span><span class="sxs-lookup"><span data-stu-id="2b35b-112">If retention period, for example, is set to six months, table rows eligible for cleanup satisfy the following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="2b35b-113">W powyższym przykładzie mamy przyjąć, że **ValidTo** kolumn odnosi się do końca okresu SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="2b35b-113">In the preceding example, we assumed that **ValidTo** column corresponds to the end of SYSTEM_TIME period.</span></span>

## <a name="how-to-configure-retention-policy"></a><span data-ttu-id="2b35b-114">Jak skonfigurować zasady przechowywania?</span><span class="sxs-lookup"><span data-stu-id="2b35b-114">How to configure retention policy?</span></span>
<span data-ttu-id="2b35b-115">Przed skonfigurowaniem zasad przechowywania dla tabeli danych czasowych należy sprawdzić w pierwszej kolejności czy włączone jest przechowywanie historycznych danych czasowych *na poziomie bazy danych*.</span><span class="sxs-lookup"><span data-stu-id="2b35b-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at the database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="2b35b-116">Baza danych flagi **is_temporal_history_retention_enabled** jest ustawiona na wartość Domyślnie, ale użytkownicy można go zmienić za pomocą instrukcji ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="2b35b-116">Database flag **is_temporal_history_retention_enabled** is set to ON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="2b35b-117">Automatycznie ma wartość OFF po [punktu w czasie przywracania](sql-database-recovery-using-backups.md) operacji.</span><span class="sxs-lookup"><span data-stu-id="2b35b-117">It is also automatically set to OFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="2b35b-118">Aby włączyć oczyszczanie przechowywania historii danych czasowych dla bazy danych, należy wykonać następującą instrukcję:</span><span class="sxs-lookup"><span data-stu-id="2b35b-118">To enable temporal history retention cleanup for your database, execute the following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="2b35b-119">Możesz skonfigurować czas przechowywania w przypadku tabel czasowych, nawet jeśli **is_temporal_history_retention_enabled** jest wyłączona, ale automatycznego oczyszczania przestarzałych wierszy jest nie są uruchamiane w takiej sytuacji.</span><span class="sxs-lookup"><span data-stu-id="2b35b-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="2b35b-120">Zasady przechowywania jest skonfigurowane podczas tworzenia tabeli, określając wartość parametru HISTORY_RETENTION_PERIOD:</span><span class="sxs-lookup"><span data-stu-id="2b35b-120">Retention policy is configured during table creation by specifying value for the HISTORY_RETENTION_PERIOD parameter:</span></span>

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

<span data-ttu-id="2b35b-121">Baza danych SQL Azure pozwala określić przy użyciu różne jednostki okresu przechowywania: dni, tygodnie, MIESIĄCE i lata.</span><span class="sxs-lookup"><span data-stu-id="2b35b-121">Azure SQL Database allows you to specify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="2b35b-122">W przypadku pominięcia HISTORY_RETENTION_PERIOD przyjęto NIESKOŃCZONE przechowywania.</span><span class="sxs-lookup"><span data-stu-id="2b35b-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="2b35b-123">Umożliwia także NIESKOŃCZONE — słowo kluczowe jawnie.</span><span class="sxs-lookup"><span data-stu-id="2b35b-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="2b35b-124">W niektórych scenariuszach warto skonfigurować przechowywania po utworzeniu tabeli lub zmienić wcześniej skonfigurowane wartości.</span><span class="sxs-lookup"><span data-stu-id="2b35b-124">In some scenarios, you may want to configure retention after table creation, or to change previously configured value.</span></span> <span data-ttu-id="2b35b-125">W takim przypadku należy użyć instrukcji ALTER TABLE:</span><span class="sxs-lookup"><span data-stu-id="2b35b-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="2b35b-126">Ustawienie opcji SYSTEM_VERSIONING na OFF *nie zachowa* wartość okresu przechowywania.</span><span class="sxs-lookup"><span data-stu-id="2b35b-126">Setting SYSTEM_VERSIONING to OFF *does not preserve* retention period value.</span></span> <span data-ttu-id="2b35b-127">Ustawienie opcji SYSTEM_VERSIONING na ON, bez HISTORY_RETENTION_PERIOD jawnie określone wyniki w NIEOGRANICZONY okres przechowywania.</span><span class="sxs-lookup"><span data-stu-id="2b35b-127">Setting SYSTEM_VERSIONING to ON without HISTORY_RETENTION_PERIOD specified explicitly results in the INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="2b35b-128">Aby wyświetlić bieżący stan zasady przechowywania, użyj następującego zapytania, której jest przyłączany Flaga włączenia przechowywania danych czasowych na poziomie bazy danych z okresów przechowywania dla poszczególnych tabel:</span><span class="sxs-lookup"><span data-stu-id="2b35b-128">To review current state of the retention policy, use the following query that joins temporal retention enablement flag at the database level with retention periods for individual tables:</span></span>

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="2b35b-129">Jak baza danych SQL usuwa przestarzałe wierszy?</span><span class="sxs-lookup"><span data-stu-id="2b35b-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="2b35b-130">Układ indeksu tabeli historii zależy od procesu czyszczenia.</span><span class="sxs-lookup"><span data-stu-id="2b35b-130">The cleanup process depends on the index layout of the history table.</span></span> <span data-ttu-id="2b35b-131">Należy zauważyć, że *tylko do tabel historii z indeksem klastrowanym, (B-drzewa lub magazynu kolumn) może mieć skonfigurowanych zasad przechowywania skończoną*.</span><span class="sxs-lookup"><span data-stu-id="2b35b-131">It is important to notice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="2b35b-132">Zadanie w tle jest utworzone w celu wykonania oczyszczania przestarzałych danych dla wszystkich tabel danych czasowych z okresu przechowywania ograniczone.</span><span class="sxs-lookup"><span data-stu-id="2b35b-132">A background task is created to perform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="2b35b-133">Logika oczyszczania dla klastrowanego indeksu magazynu wierszy (B-drzewa) usuwa przestarzałe wiersza w mniejsze fragmenty (do 10 kilobajtów) minimalizując nacisk na dziennika bazy danych i podsystem We/Wy.</span><span class="sxs-lookup"><span data-stu-id="2b35b-133">Cleanup logic for the rowstore (B-tree) clustered index deletes aged row in smaller chunks (up to 10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="2b35b-134">Mimo że logiki oczyszczania wykorzystuje wymagane indeksu B-drzewa, kolejność usuwania starsze niż okres przechowywania nie może zagwarantować mocno wierszy.</span><span class="sxs-lookup"><span data-stu-id="2b35b-134">Although cleanup logic utilizes required B-tree index, order of deletions for the rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="2b35b-135">W związku z tym *nie przyjmują wszelkie zależności w kolejności Oczyszczanie aplikacji*.</span><span class="sxs-lookup"><span data-stu-id="2b35b-135">Hence, *do not take any dependency on the cleanup order in your applications*.</span></span>

<span data-ttu-id="2b35b-136">Zadanie oczyszczania dla klastrowanego magazynu kolumn spowoduje usunięcie całego [wiersz grup](https://msdn.microsoft.com/library/gg492088.aspx) jednocześnie (zwykle zawierają 1 milion wierszy każdego), który jest bardzo wydajny, szczególnie w przypadku, gdy dane historyczne zostanie wygenerowany w szybkim tempie.</span><span class="sxs-lookup"><span data-stu-id="2b35b-136">The cleanup task for the clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Przechowywania klastrowanego magazynu kolumn](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="2b35b-138">Kompresji danych doskonała i wydajne przechowywania oczyszczania sprawia, że klastrowany indeks magazynu kolumn doskonałym rozwiązaniem dla scenariuszy jeśli obciążenie generuje szybko dużej ilości danych historycznych.</span><span class="sxs-lookup"><span data-stu-id="2b35b-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="2b35b-139">Ten wzorzec jest typowa dla intensywnego [obciążenia przetwarzania transakcyjnego, które tabele danych czasowych](https://msdn.microsoft.com/library/mt631669.aspx) śledzenie zmian i inspekcji, analiza trendu lub wprowadzanie danych IoT.</span><span class="sxs-lookup"><span data-stu-id="2b35b-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="2b35b-140">Zagadnienia dotyczące indeksu</span><span class="sxs-lookup"><span data-stu-id="2b35b-140">Index considerations</span></span>
<span data-ttu-id="2b35b-141">Zadanie oczyszczania tabel klastrowanego indeksu magazynu wierszy wymaga indeksu do uruchomienia z kolumny odpowiadającego koniec okresu SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="2b35b-141">The cleanup task for tables with rowstore clustered index requires index to start with the column corresponding the end of SYSTEM_TIME period.</span></span> <span data-ttu-id="2b35b-142">Jeśli takie indeks nie istnieje, nie można skonfigurować okres przechowywania ograniczone:</span><span class="sxs-lookup"><span data-stu-id="2b35b-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="2b35b-143">*Msg 13765, poziom 16, stan 1 <br> </br> ustawienie okresu przechowywania ograniczone nie można w tabeli danych czasowych z systemową kontrolą wersji "temporalstagetestdb.dbo.WebsiteUserInfo", ponieważ tabela historii " temporalstagetestdb.dbo.WebsiteUserInfoHistory "nie zawiera wymaganego indeksu klastrowanego. Należy rozważyć utworzenie klastrowanego magazynu kolumn lub indeksu B-drzewa, począwszy od kolumny, która odpowiada koniec SYSTEM_TIME period w tabeli historii.*</span><span class="sxs-lookup"><span data-stu-id="2b35b-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because the history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with the column that matches end of SYSTEM_TIME period, on the history table.*</span></span>

<span data-ttu-id="2b35b-144">Należy zauważyć, że tabeli historii domyślny utworzony przez bazę danych SQL Azure już ma indeks, który jest zgodny z zasad przechowywania w klastrze.</span><span class="sxs-lookup"><span data-stu-id="2b35b-144">It is important to notice that the default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="2b35b-145">Jeśli próbujesz usunąć tego indeksu dla tabeli z okresu przechowywania ograniczone, operacja kończy się niepowodzeniem z powodu następującego błędu:</span><span class="sxs-lookup"><span data-stu-id="2b35b-145">If you try to remove that index on a table with finite retention period, operation fails with the following error:</span></span>

<span data-ttu-id="2b35b-146">*Msg 13766, poziom 16, stan 1 <br> </br> nie można porzucić indeksu klastrowanego "WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory", ponieważ jest on używany do automatycznego usuwania przestarzałych danych. Rozważ ustawienie HISTORY_RETENTION_PERIOD infinite na odpowiedniej systemową kontrolą wersji tabeli danych czasowych, jeśli musisz porzucić ten indeks.*</span><span class="sxs-lookup"><span data-stu-id="2b35b-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop the clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD to INFINITE on the corresponding system-versioned temporal table if you need to drop this index.*</span></span>

<span data-ttu-id="2b35b-147">Oczyszczanie klastrowany indeks magazynu kolumn działa optymalnie, jeśli umieszczanych historycznych wierszy w kolejności rosnącej (uporządkowane do końca okresu kolumny), co jest zawsze sytuacją, gdy w tabeli historii jest wypełniana wyłącznie przy użyciu mechanizmu SYSTEM_VERSIONIOING.</span><span class="sxs-lookup"><span data-stu-id="2b35b-147">Cleanup on the clustered columnstore index works optimally if historical rows are inserted in the ascending order (ordered by the end of period column), which is always the case when the history table is populated exclusively by the SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="2b35b-148">Wiersze w tabeli historii nie są uporządkowane według koniec kolumnie okresu (która może się po migracji istniejących danych historycznych), należy ponownie utworzyć klastrowanego indeksu magazynu kolumn na górze indeksu magazynu wierszy B-drzewa, który jest prawidłowo uporządkowanych, aby osiągnąć optymalną wydajność.</span><span class="sxs-lookup"><span data-stu-id="2b35b-148">If rows in the history table are not ordered by end of period column (which may be the case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, to achieve optimal performance.</span></span>

<span data-ttu-id="2b35b-149">Należy unikać odbudowywania klastrowany indeks magazynu kolumn w tabeli historii od okresu przechowywania ograniczone, ponieważ mogą ulec zmianie, kolejność w grupy wierszy naturalnie narzucone przez operację wersjonowania systemu.</span><span class="sxs-lookup"><span data-stu-id="2b35b-149">Avoid rebuilding clustered columnstore index on the history table with the finite retention period, because it may change ordering in the row groups naturally imposed by the system-versioning operation.</span></span> <span data-ttu-id="2b35b-150">Jeśli musisz odbudować indeksu klastrowanego magazynu kolumn w tabeli historii, to zrobić przez ponowne utworzenie u góry zgodne indeksu B-drzewa, zachowując kolejnością rowgroups niezbędne oczyszczania regularnych danych.</span><span class="sxs-lookup"><span data-stu-id="2b35b-150">If you need to rebuild clustered columnstore index on the history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in the rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="2b35b-151">Te same podejście należy podjąć w przypadku utworzenia tabeli danych czasowych z istniejącą tabelę historii, która ma klastrowany indeks kolumny bez kolejność gwarantowane danych:</span><span class="sxs-lookup"><span data-stu-id="2b35b-151">The same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by the end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="2b35b-152">Po skonfigurowaniu ograniczone przechowywanie tabeli historii z klastrowanego indeksu magazynu kolumn nie można utworzyć dodatkowe nieklastrowanych indeksów B-drzewa w tej tabeli:</span><span class="sxs-lookup"><span data-stu-id="2b35b-152">When finite retention period is configured for the history table with the clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="2b35b-153">Próba wykonania powyżej instrukcji nie powiodło się z powodu następującego błędu:</span><span class="sxs-lookup"><span data-stu-id="2b35b-153">An attempt to execute above statement fails with the following error:</span></span>

<span data-ttu-id="2b35b-154">*Msg 13772, poziom 16, stan 1 <br> </br> nie można utworzyć indeksu nieklastrowanego dla tabeli historii danych czasowych "WebsiteUserInfoHistory" ponieważ ma ona okres przechowywania skończona i klastrowany indeks magazynu kolumn zdefiniowane.*</span><span class="sxs-lookup"><span data-stu-id="2b35b-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="2b35b-155">Tworzenie zapytań o tabele z zasady przechowywania</span><span class="sxs-lookup"><span data-stu-id="2b35b-155">Querying tables with retention policy</span></span>
<span data-ttu-id="2b35b-156">Wszystkie zapytania w tabeli danych czasowych automatycznie odfiltrowywania historycznych wierszy pasujących zasad przechowywania ograniczone, aby uniknąć nieprzewidywalne i niespójne wyniki, ponieważ przestarzałych wierszy może zostać usunięta przez zadanie oczyszczania *w dowolnym momencie w czasie i dowolnego kolejność*.</span><span class="sxs-lookup"><span data-stu-id="2b35b-156">All queries on the temporal table automatically filter out historical rows matching finite retention policy, to avoid unpredictable and inconsistent results, since aged rows can be deleted by the cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="2b35b-157">Na poniższej ilustracji przedstawiono planu zapytania dla prostego zapytania:</span><span class="sxs-lookup"><span data-stu-id="2b35b-157">The following picture shows the query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="2b35b-158">Plan zapytania zawiera dodatkowy filtr stosowane do końca okresu kolumny (ValidTo) w operatorze skanowania indeksu klastrowanego w tabeli historii (wyróżniony).</span><span class="sxs-lookup"><span data-stu-id="2b35b-158">The query plan includes additional filter applied to end of period column (ValidTo) in the Clustered Index Scan operator on the history table (highlighted).</span></span> <span data-ttu-id="2b35b-159">W tym przykładzie przyjęto założenie, w tabeli WebsiteUserInfo ustawiono tego okresu przechowywania jeden miesiąc.</span><span class="sxs-lookup"><span data-stu-id="2b35b-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Filtr kwerendy przechowywania](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="2b35b-161">Jednak w tabeli historii są zapytania bezpośrednio, może wystąpić wierszy, które są starsze niż przechowywania określony okres, ale bez żadnych gwarancji dla powtarzalne wyniki.</span><span class="sxs-lookup"><span data-stu-id="2b35b-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="2b35b-162">Na poniższej ilustracji przedstawiono planu wykonania zapytania dla zapytania w tabeli historii bez dodatkowych filtrów:</span><span class="sxs-lookup"><span data-stu-id="2b35b-162">The following picture shows query execution plan for the query on the history table without additional filters applied:</span></span>

![Trwa badanie historii bez filtru przechowywania](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="2b35b-164">Nie należy polegać logiki biznesowej na odczytywania tabeli historii poza okresem przechowywania, jak możesz uzyskać niespójne lub nieoczekiwane wyniki.</span><span class="sxs-lookup"><span data-stu-id="2b35b-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="2b35b-165">Zalecane jest użycie czasowych zapytań z klauzulą FOR SYSTEM_TIME do analizowania danych w tabelach danych czasowych.</span><span class="sxs-lookup"><span data-stu-id="2b35b-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="2b35b-166">Punktu w czasie przywracania uwagi</span><span class="sxs-lookup"><span data-stu-id="2b35b-166">Point in time restore considerations</span></span>
<span data-ttu-id="2b35b-167">Podczas tworzenia nowej bazy danych przez [Przywracanie istniejącą bazę danych do określonego punktu w czasie](sql-database-recovery-using-backups.md), ma przechowywania danych czasowych wyłączona na poziomie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2b35b-167">When you create new database by [restoring existing database to a specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at the database level.</span></span> <span data-ttu-id="2b35b-168">(**is_temporal_history_retention_enabled** ustawiona flaga off).</span><span class="sxs-lookup"><span data-stu-id="2b35b-168">(**is_temporal_history_retention_enabled** flag set to OFF).</span></span> <span data-ttu-id="2b35b-169">Ta funkcja pozwala sprawdzić wszystkie wiersze historycznych podczas przywracania, nie martwiąc się, że przestarzałych wiersze zostaną usunięte przed uzyskanie do nich kwerendy.</span><span class="sxs-lookup"><span data-stu-id="2b35b-169">This functionality allows you to examine all historical rows upon restore, without worrying that aged rows are removed before you get to query them.</span></span> <span data-ttu-id="2b35b-170">Możesz użyć jej do *sprawdzić historycznych danych poza okresem przechowywania skonfigurowanych*.</span><span class="sxs-lookup"><span data-stu-id="2b35b-170">You can use it to *inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="2b35b-171">Załóżmy, że tabela danych czasowych ma podanego okresu przechowywania jeden miesiąc.</span><span class="sxs-lookup"><span data-stu-id="2b35b-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="2b35b-172">Jeśli baza danych została utworzona w warstwie Premium usługi, czy można utworzyć kopię bazy danych o stanie bazy danych się do 35 dni w przeszłości.</span><span class="sxs-lookup"><span data-stu-id="2b35b-172">If your database was created in Premium Service tier, you would be able to create database copy with the database state up to 35 days back in the past.</span></span> <span data-ttu-id="2b35b-173">Które skutecznie umożliwi analizowanie historycznych wierszy, które są do 65 dni przez bezpośrednie wysyłanie zapytań w tabeli historii.</span><span class="sxs-lookup"><span data-stu-id="2b35b-173">That effectively would allow you to analyze historical rows that are up to 65 days old by querying the history table directly.</span></span>

<span data-ttu-id="2b35b-174">Jeśli chcesz aktywować oczyszczania przechowywania danych tymczasowych, uruchom następującą instrukcję Transact-SQL po punkcie w czasie przywracania:</span><span class="sxs-lookup"><span data-stu-id="2b35b-174">If you want to activate temporal retention cleanup, run the following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="2b35b-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2b35b-175">Next steps</span></span>
<span data-ttu-id="2b35b-176">Aby dowiedzieć się, jak używać tabel danych czasowych w aplikacji, zapoznaj się [wprowadzenie do tabel danych czasowych w bazie danych SQL Azure](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="2b35b-176">To learn how to use Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="2b35b-177">Odwiedź Channel 9, aby usłyszeć [klienta rzeczywistych danych czasowych implementacji Powodzenie wątku](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) i obejrzyj [live pokaz danych czasowych](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="2b35b-177">Visit Channel 9 to hear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="2b35b-178">Aby uzyskać szczegółowe informacje o tabelach danych czasowych, przejrzyj [dokumentacji MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="2b35b-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

