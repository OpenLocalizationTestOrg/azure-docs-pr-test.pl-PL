---
title: dane historyczne aaaManage w tabelach danych czasowych z zasadami przechowywania | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse przechowywania danych tymczasowych zasad tookeep danych historycznych pod kontrolą."
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
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a><span data-ttu-id="91339-103">Zarządzanie danych historycznych w tabelach danych czasowych z zasady przechowywania</span><span class="sxs-lookup"><span data-stu-id="91339-103">Manage historical data in Temporal Tables with retention policy</span></span>
<span data-ttu-id="91339-104">Tabele danych czasowych może zwiększyć baz danych o rozmiarze ponad zwykłych tabelach, zwłaszcza jeśli przechowywanie danych historycznych przez dłuższy okres.</span><span class="sxs-lookup"><span data-stu-id="91339-104">Temporal Tables may increase database size more than regular tables, especially if you retain historical data for a longer period of time.</span></span> <span data-ttu-id="91339-105">W związku z tym zasady przechowywania danych historycznych jest istotnym elementem planowania i zarządzanie cyklem życia hello każdej tabeli danych czasowych.</span><span class="sxs-lookup"><span data-stu-id="91339-105">Hence, retention policy for historical data is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="91339-106">Tabele danych czasowych w bazie danych SQL Azure pochodzą z mechanizmem przechowywania łatwy w użyciu, który ułatwia wykonywanie tego zadania.</span><span class="sxs-lookup"><span data-stu-id="91339-106">Temporal Tables in Azure SQL Database come with easy-to-use retention mechanism that helps you accomplish this task.</span></span>

<span data-ttu-id="91339-107">Przechowywania historii danych czasowych można skonfigurować na poziomie pojedynczej tabeli hello, dzięki czemu użytkownicy, który toocreate przedawnienia elastyczne zasady.</span><span class="sxs-lookup"><span data-stu-id="91339-107">Temporal history retention can be configured at hello individual table level, which allows users toocreate flexible aging polices.</span></span> <span data-ttu-id="91339-108">Stosowanie przechowywania danych czasowych jest prosty: wymaga tylko jednego toobe parametru ustawiona podczas zmiany schematu lub tworzenia tabeli.</span><span class="sxs-lookup"><span data-stu-id="91339-108">Applying temporal retention is simple: it requires only one parameter toobe set during table creation or schema change.</span></span>

<span data-ttu-id="91339-109">Po zdefiniowaniu zasad przechowywania bazy danych SQL Azure rozpoczyna regularnie sprawdzanie, czy istnieją historyczne wierszy, które kwalifikują się do czyszczenia danych.</span><span class="sxs-lookup"><span data-stu-id="91339-109">After you define retention policy, Azure SQL Database starts checking regularly if there are historical rows that are eligible for automatic data cleanup.</span></span> <span data-ttu-id="91339-110">Identyfikacja zgodnych wierszy i ich usunięcia z tabeli historii hello występować w sposób niewidoczny dla użytkownika, w zadania w tle hello zaplanowane i uruchamiane przez hello system.</span><span class="sxs-lookup"><span data-stu-id="91339-110">Identification of matching rows and their removal from hello history table occur transparently, in hello background task that is scheduled and run by hello system.</span></span> <span data-ttu-id="91339-111">Warunek wieku wiersze tabeli historii hello jest sprawdzany zależności w kolumnie hello reprezentujący koniec okresu SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="91339-111">Age condition for hello history table rows is checked based on hello column representing end of SYSTEM_TIME period.</span></span> <span data-ttu-id="91339-112">Jeśli okres przechowywania, na przykład ustawiono toosix miesiące, kwalifikuje się do oczyszczania wiersze tabeli spełniają hello następującego warunku:</span><span class="sxs-lookup"><span data-stu-id="91339-112">If retention period, for example, is set toosix months, table rows eligible for cleanup satisfy hello following condition:</span></span>

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

<span data-ttu-id="91339-113">W hello poprzedzających przykład, możemy przyjąć, że **ValidTo** kolumna odpowiada toohello koniec okresu SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="91339-113">In hello preceding example, we assumed that **ValidTo** column corresponds toohello end of SYSTEM_TIME period.</span></span>

## <a name="how-tooconfigure-retention-policy"></a><span data-ttu-id="91339-114">Jak tooconfigure zasady przechowywania?</span><span class="sxs-lookup"><span data-stu-id="91339-114">How tooconfigure retention policy?</span></span>
<span data-ttu-id="91339-115">Przed skonfigurowaniem zasad przechowywania dla tabeli danych czasowych należy sprawdzić w pierwszej kolejności czy włączone jest przechowywanie historycznych danych czasowych *na poziomie bazy danych hello*.</span><span class="sxs-lookup"><span data-stu-id="91339-115">Before you configure retention policy for a temporal table, check first whether temporal historical retention is enabled *at hello database level*.</span></span>

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

<span data-ttu-id="91339-116">Baza danych flagi **is_temporal_history_retention_enabled** jest zestaw tooON domyślnie, ale użytkownicy można go zmienić za pomocą instrukcji ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="91339-116">Database flag **is_temporal_history_retention_enabled** is set tooON by default, but users can change it with ALTER DATABASE statement.</span></span> <span data-ttu-id="91339-117">Jest również automatycznie tooOFF zestaw po [punktu w czasie przywracania](sql-database-recovery-using-backups.md) operacji.</span><span class="sxs-lookup"><span data-stu-id="91339-117">It is also automatically set tooOFF after [point in time restore](sql-database-recovery-using-backups.md) operation.</span></span> <span data-ttu-id="91339-118">Oczyszczanie przechowywania historii danych czasowych tooenable dla bazy danych, wykonaj hello następującej instrukcji:</span><span class="sxs-lookup"><span data-stu-id="91339-118">tooenable temporal history retention cleanup for your database, execute hello following statement:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> <span data-ttu-id="91339-119">Możesz skonfigurować czas przechowywania w przypadku tabel czasowych, nawet jeśli **is_temporal_history_retention_enabled** jest wyłączona, ale automatycznego oczyszczania przestarzałych wierszy jest nie są uruchamiane w takiej sytuacji.</span><span class="sxs-lookup"><span data-stu-id="91339-119">You can configure retention for temporal tables even if **is_temporal_history_retention_enabled** is OFF, but automatic cleanup for aged rows is not triggered in that case.</span></span>
> 
> 

<span data-ttu-id="91339-120">Zasady przechowywania jest skonfigurowane podczas tworzenia tabeli, określając wartość parametru HISTORY_RETENTION_PERIOD hello:</span><span class="sxs-lookup"><span data-stu-id="91339-120">Retention policy is configured during table creation by specifying value for hello HISTORY_RETENTION_PERIOD parameter:</span></span>

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

<span data-ttu-id="91339-121">Bazy danych SQL Azure umożliwia przechowywanie toospecify przy użyciu różne jednostki: dni, tygodnie, MIESIĄCE i lata.</span><span class="sxs-lookup"><span data-stu-id="91339-121">Azure SQL Database allows you toospecify retention period by using different time units: DAYS, WEEKS, MONTHS, and YEARS.</span></span> <span data-ttu-id="91339-122">W przypadku pominięcia HISTORY_RETENTION_PERIOD przyjęto NIESKOŃCZONE przechowywania.</span><span class="sxs-lookup"><span data-stu-id="91339-122">If HISTORY_RETENTION_PERIOD is omitted, INFINITE retention is assumed.</span></span> <span data-ttu-id="91339-123">Umożliwia także NIESKOŃCZONE — słowo kluczowe jawnie.</span><span class="sxs-lookup"><span data-stu-id="91339-123">You can also use INFINITE keyword explicitly.</span></span>

<span data-ttu-id="91339-124">W niektórych scenariuszach może być tooconfigure przechowywania po utworzeniu tabeli lub toochange wcześniej skonfigurowane wartości.</span><span class="sxs-lookup"><span data-stu-id="91339-124">In some scenarios, you may want tooconfigure retention after table creation, or toochange previously configured value.</span></span> <span data-ttu-id="91339-125">W takim przypadku należy użyć instrukcji ALTER TABLE:</span><span class="sxs-lookup"><span data-stu-id="91339-125">In that case use ALTER TABLE statement:</span></span>

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> <span data-ttu-id="91339-126">Ustawienie SYSTEM_VERSIONING tooOFF *nie zachowa* wartość okresu przechowywania.</span><span class="sxs-lookup"><span data-stu-id="91339-126">Setting SYSTEM_VERSIONING tooOFF *does not preserve* retention period value.</span></span> <span data-ttu-id="91339-127">Ustawienie tooON SYSTEM_VERSIONING bez HISTORY_RETENTION_PERIOD określone jawnie wyniki w hello NIEOGRANICZONY okres przechowywania.</span><span class="sxs-lookup"><span data-stu-id="91339-127">Setting SYSTEM_VERSIONING tooON without HISTORY_RETENTION_PERIOD specified explicitly results in hello INFINITE retention period.</span></span>
> 
> 

<span data-ttu-id="91339-128">tooreview bieżący stan hello zasady przechowywania, użyj następujących hello kwerendy tę flagę aktywacji przechowywania danych czasowych sprzężenia na poziomie bazy danych hello z okresów przechowywania dla poszczególnych tabel:</span><span class="sxs-lookup"><span data-stu-id="91339-128">tooreview current state of hello retention policy, use hello following query that joins temporal retention enablement flag at hello database level with retention periods for individual tables:</span></span>

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


## <a name="how-sql-database-deletes-aged-rows"></a><span data-ttu-id="91339-129">Jak baza danych SQL usuwa przestarzałe wierszy?</span><span class="sxs-lookup"><span data-stu-id="91339-129">How SQL Database deletes aged rows?</span></span>
<span data-ttu-id="91339-130">procesu oczyszczania Hello zależy od hello układ indeksu tabeli historii hello.</span><span class="sxs-lookup"><span data-stu-id="91339-130">hello cleanup process depends on hello index layout of hello history table.</span></span> <span data-ttu-id="91339-131">Jest ważne toonotice który *tylko do tabel historii z indeksem klastrowanym, (B-drzewa lub magazynu kolumn) może mieć skonfigurowanych zasad przechowywania skończoną*.</span><span class="sxs-lookup"><span data-stu-id="91339-131">It is important toonotice that *only history tables with a clustered index (B-tree or columnstore) can have finite retention policy configured*.</span></span> <span data-ttu-id="91339-132">Zadanie w tle jest tworzony tooperform oczyszczania przestarzałych danych dla wszystkich tabel danych czasowych z okresu przechowywania ograniczone.</span><span class="sxs-lookup"><span data-stu-id="91339-132">A background task is created tooperform aged data cleanup for all temporal tables with finite retention period.</span></span>
<span data-ttu-id="91339-133">Oczyścić logikę klastrowanego indeksu magazynu wierszy (B-drzewa) hello usuwa wiersz przestarzałe w mniejsze fragmenty (up too10K) minimalizując nacisk na dziennika bazy danych i podsystem We/Wy.</span><span class="sxs-lookup"><span data-stu-id="91339-133">Cleanup logic for hello rowstore (B-tree) clustered index deletes aged row in smaller chunks (up too10K) minimizing pressure on database log and I/O subsystem.</span></span> <span data-ttu-id="91339-134">Mimo że używa logiki oczyszczania wymagane indeksu B-drzewa, kolejność usunięcia wierszy hello starsze niż okres przechowywania nie może zagwarantować mocno.</span><span class="sxs-lookup"><span data-stu-id="91339-134">Although cleanup logic utilizes required B-tree index, order of deletions for hello rows older than retention period cannot be firmly guaranteed.</span></span> <span data-ttu-id="91339-135">W związku z tym *nie przyjmują wszelkie zależności na powitania oczyszczania kolejności w aplikacjach*.</span><span class="sxs-lookup"><span data-stu-id="91339-135">Hence, *do not take any dependency on hello cleanup order in your applications*.</span></span>

<span data-ttu-id="91339-136">Witaj zadanie oczyszczania dla hello klastrowanego magazynu kolumn spowoduje usunięcie całego [wiersz grup](https://msdn.microsoft.com/library/gg492088.aspx) jednocześnie (zwykle zawierają 1 milion wierszy każdego), który jest bardzo wydajny, szczególnie w przypadku, gdy dane historyczne zostanie wygenerowany w szybkim tempie.</span><span class="sxs-lookup"><span data-stu-id="91339-136">hello cleanup task for hello clustered columnstore removes entire [row groups](https://msdn.microsoft.com/library/gg492088.aspx) at once (typically contain 1 million of rows each), which is very efficient, especially when historical data is generated at a high pace.</span></span>

![Przechowywania klastrowanego magazynu kolumn](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

<span data-ttu-id="91339-138">Kompresji danych doskonała i wydajne przechowywania oczyszczania sprawia, że klastrowany indeks magazynu kolumn doskonałym rozwiązaniem dla scenariuszy jeśli obciążenie generuje szybko dużej ilości danych historycznych.</span><span class="sxs-lookup"><span data-stu-id="91339-138">Excellent data compression and efficient retention cleanup makes clustered columnstore index a perfect choice for scenarios when your workload rapidly generates high amount of historical data.</span></span> <span data-ttu-id="91339-139">Ten wzorzec jest typowa dla intensywnego [obciążenia przetwarzania transakcyjnego, które tabele danych czasowych](https://msdn.microsoft.com/library/mt631669.aspx) śledzenie zmian i inspekcji, analiza trendu lub wprowadzanie danych IoT.</span><span class="sxs-lookup"><span data-stu-id="91339-139">That pattern is typical for intensive [transactional processing workloads that use temporal tables](https://msdn.microsoft.com/library/mt631669.aspx) for change tracking and auditing, trend analysis, or IoT data ingestion.</span></span>

## <a name="index-considerations"></a><span data-ttu-id="91339-140">Zagadnienia dotyczące indeksu</span><span class="sxs-lookup"><span data-stu-id="91339-140">Index considerations</span></span>
<span data-ttu-id="91339-141">Zadanie oczyszczania Hello tabel klastrowanego indeksu magazynu wierszy wymaga toostart indeksu z hello kolumny odpowiedniego hello końca okresu SYSTEM_TIME.</span><span class="sxs-lookup"><span data-stu-id="91339-141">hello cleanup task for tables with rowstore clustered index requires index toostart with hello column corresponding hello end of SYSTEM_TIME period.</span></span> <span data-ttu-id="91339-142">Jeśli takie indeks nie istnieje, nie można skonfigurować okres przechowywania ograniczone:</span><span class="sxs-lookup"><span data-stu-id="91339-142">If such index doesn't exist, you cannot configure a finite retention period:</span></span>

<span data-ttu-id="91339-143">*Msg 13765, poziom 16, stan 1 <br> </br> ustawienie okresu przechowywania ograniczone nie można w tabeli danych czasowych z systemową kontrolą wersji "temporalstagetestdb.dbo.WebsiteUserInfo", ponieważ tabela historii hello " temporalstagetestdb.dbo.WebsiteUserInfoHistory "nie zawiera wymaganego indeksu klastrowanego. Należy rozważyć utworzenie klastrowanego magazynu kolumn lub indeksu B-drzewa, począwszy od hello kolumny, która odpowiada koniec SYSTEM_TIME period w tabeli historii hello.*</span><span class="sxs-lookup"><span data-stu-id="91339-143">*Msg 13765, Level 16, State 1 <br></br> Setting finite retention period failed on system-versioned temporal table 'temporalstagetestdb.dbo.WebsiteUserInfo' because hello history table 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' does not contain required clustered index. Consider creating a clustered columnstore or B-tree index starting with hello column that matches end of SYSTEM_TIME period, on hello history table.*</span></span>

<span data-ttu-id="91339-144">Jest ważne toonotice, który hello tabeli historii domyślny utworzony przez bazę danych SQL Azure już ma klastrowany indeks, który jest zgodny z zasady przechowywania.</span><span class="sxs-lookup"><span data-stu-id="91339-144">It is important toonotice that hello default history table created by Azure SQL Database already has clustered index, which is compliant for retention policy.</span></span> <span data-ttu-id="91339-145">Jeśli spróbujesz tooremove tego indeksu dla tabeli z okresu przechowywania ograniczone, operacja nie powiedzie się z hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="91339-145">If you try tooremove that index on a table with finite retention period, operation fails with hello following error:</span></span>

<span data-ttu-id="91339-146">*Msg 13766, poziom 16, stan 1 <br> </br> nie można porzucić indeksu klastrowanego hello "WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory", ponieważ jest on używany do automatycznego usuwania przestarzałych danych. Jeśli potrzebujesz toodrop tego indeksu, należy wziąć pod uwagę tooINFINITE HISTORY_RETENTION_PERIOD ustawienie na powitania odpowiedniej tabeli danych czasowych systemową kontrolą wersji.*</span><span class="sxs-lookup"><span data-stu-id="91339-146">*Msg 13766, Level 16, State 1 <br></br> Cannot drop hello clustered index 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' because it is being used for automatic cleanup of aged data. Consider setting HISTORY_RETENTION_PERIOD tooINFINITE on hello corresponding system-versioned temporal table if you need toodrop this index.*</span></span>

<span data-ttu-id="91339-147">Oczyszczanie na powitania klastrowany indeks magazynu kolumn działa optymalnie, jeśli umieszczanych historycznych wierszy w kolejności rosnącej (uporządkowane według hello koniec okresu kolumny), co jest zawsze hello sytuacją, gdy tabela historii hello jest wypełniana wyłącznie hello SYSTEM_ hello Mechanizm VERSIONIOING.</span><span class="sxs-lookup"><span data-stu-id="91339-147">Cleanup on hello clustered columnstore index works optimally if historical rows are inserted in hello ascending order (ordered by hello end of period column), which is always hello case when hello history table is populated exclusively by hello SYSTEM_VERSIONIOING mechanism.</span></span> <span data-ttu-id="91339-148">Wiersze w tabeli historii hello nie są uporządkowane według koniec kolumnie okresu (które mogą być przypadku powitania po migracji istniejących danych historycznych), należy ponownie utworzyć klastrowanego indeksu magazynu kolumn na górze indeksu magazynu wierszy B-drzewa, który jest poprawnie określona, tooachieve optymalną wydajność.</span><span class="sxs-lookup"><span data-stu-id="91339-148">If rows in hello history table are not ordered by end of period column (which may be hello case if you migrated existing historical data), you should re-create clustered columnstore index on top of B-tree rowstore index that is properly ordered, tooachieve optimal performance.</span></span>

<span data-ttu-id="91339-149">Należy unikać odbudowywania klastrowany indeks magazynu kolumn w tabeli historii hello hello okres przechowywania ograniczone, ponieważ mogą ulec zmianie, kolejność w naturalnie narzucone przez operację system-versioning hello grupy wierszy hello.</span><span class="sxs-lookup"><span data-stu-id="91339-149">Avoid rebuilding clustered columnstore index on hello history table with hello finite retention period, because it may change ordering in hello row groups naturally imposed by hello system-versioning operation.</span></span> <span data-ttu-id="91339-150">Jeśli potrzebujesz toorebuild klastrowany indeks magazynu kolumn w tabeli historii hello zrobić, ponowne utworzenie u góry zgodne indeksu B-drzewa, zachowując kolejnością rowgroups hello niezbędne oczyszczania regularnych danych.</span><span class="sxs-lookup"><span data-stu-id="91339-150">If you need toorebuild clustered columnstore index on hello history table, do that by re-creating it on top of compliant B-tree index, preserving ordering in hello rowgroups necessary for regular data cleanup.</span></span> <span data-ttu-id="91339-151">Witaj, które same podejście należy podjąć w przypadku utworzenia tabeli danych czasowych z istniejącą tabelę historii, która ma klastrowany indeks kolumny bez kolejność gwarantowane danych:</span><span class="sxs-lookup"><span data-stu-id="91339-151">hello same approach should be taken if you create temporal table with existing history table that has clustered column index without guaranteed data order:</span></span>

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

<span data-ttu-id="91339-152">Po skonfigurowaniu ograniczone przechowywanie hello tabeli historii z hello klastrowany indeks magazynu kolumn nie można utworzyć dodatkowe nieklastrowanych indeksów B-drzewa w tej tabeli:</span><span class="sxs-lookup"><span data-stu-id="91339-152">When finite retention period is configured for hello history table with hello clustered columnstore index, you cannot create additional non-clustered B-tree indexes on that table:</span></span>

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

<span data-ttu-id="91339-153">Próba tooexecute powyżej instrukcji kończy się niepowodzeniem z hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="91339-153">An attempt tooexecute above statement fails with hello following error:</span></span>

<span data-ttu-id="91339-154">*Msg 13772, poziom 16, stan 1 <br> </br> nie można utworzyć indeksu nieklastrowanego dla tabeli historii danych czasowych "WebsiteUserInfoHistory" ponieważ ma ona okres przechowywania skończona i klastrowany indeks magazynu kolumn zdefiniowane.*</span><span class="sxs-lookup"><span data-stu-id="91339-154">*Msg 13772, Level 16, State 1 <br></br> Cannot create non-clustered index on a temporal history table 'WebsiteUserInfoHistory' since it has finite retention period and clustered columnstore index defined.*</span></span>

## <a name="querying-tables-with-retention-policy"></a><span data-ttu-id="91339-155">Tworzenie zapytań o tabele z zasady przechowywania</span><span class="sxs-lookup"><span data-stu-id="91339-155">Querying tables with retention policy</span></span>
<span data-ttu-id="91339-156">Wszystkie zapytania w tabeli danych czasowych hello automatycznie odfiltrowywania historycznych wierszy pasujących zasad przechowywania ograniczone, tooavoid nieprzewidywalne i niespójne wyniki, ponieważ przestarzałych wierszy może zostać usunięta przez zadanie oczyszczania hello, *w dowolnym momencie w czasie, a w kolejność dowolnego*.</span><span class="sxs-lookup"><span data-stu-id="91339-156">All queries on hello temporal table automatically filter out historical rows matching finite retention policy, tooavoid unpredictable and inconsistent results, since aged rows can be deleted by hello cleanup task, *at any point in time and in arbitrary order*.</span></span>

<span data-ttu-id="91339-157">Witaj poniższej ilustracji przedstawiono hello planu zapytania dla prostego zapytania:</span><span class="sxs-lookup"><span data-stu-id="91339-157">hello following picture shows hello query plan for a simple query:</span></span>

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

<span data-ttu-id="91339-158">Zapytanie Hello plan zawiera dodatkowy filtr stosowane tooend (ValidTo) w kolumnie okresu w operatorze hello skanowania indeksu klastrowanego w tabeli historii hello (wyróżniony).</span><span class="sxs-lookup"><span data-stu-id="91339-158">hello query plan includes additional filter applied tooend of period column (ValidTo) in hello Clustered Index Scan operator on hello history table (highlighted).</span></span> <span data-ttu-id="91339-159">W tym przykładzie przyjęto założenie, w tabeli WebsiteUserInfo ustawiono tego okresu przechowywania jeden miesiąc.</span><span class="sxs-lookup"><span data-stu-id="91339-159">This example assumes that one MONTH retention period was set on WebsiteUserInfo table.</span></span>

![Filtr kwerendy przechowywania](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

<span data-ttu-id="91339-161">Jednak w tabeli historii są zapytania bezpośrednio, może wystąpić wierszy, które są starsze niż przechowywania określony okres, ale bez żadnych gwarancji dla powtarzalne wyniki.</span><span class="sxs-lookup"><span data-stu-id="91339-161">However, if you query history table directly, you may see rows that are older than specified retention period, but without any guarantee for repeatable query results.</span></span> <span data-ttu-id="91339-162">Witaj poniższej ilustracji przedstawiono planu wykonania zapytania dla zapytania hello w tabeli historii hello bez dodatkowych filtrów:</span><span class="sxs-lookup"><span data-stu-id="91339-162">hello following picture shows query execution plan for hello query on hello history table without additional filters applied:</span></span>

![Trwa badanie historii bez filtru przechowywania](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

<span data-ttu-id="91339-164">Nie należy polegać logiki biznesowej na odczytywania tabeli historii poza okresem przechowywania, jak możesz uzyskać niespójne lub nieoczekiwane wyniki.</span><span class="sxs-lookup"><span data-stu-id="91339-164">Do not rely your business logic on reading history table beyond retention period as you may get inconsistent or unexpected results.</span></span> <span data-ttu-id="91339-165">Zalecane jest użycie czasowych zapytań z klauzulą FOR SYSTEM_TIME do analizowania danych w tabelach danych czasowych.</span><span class="sxs-lookup"><span data-stu-id="91339-165">We recommend that you use temporal queries with FOR SYSTEM_TIME clause for analyzing data in temporal tables.</span></span>

## <a name="point-in-time-restore-considerations"></a><span data-ttu-id="91339-166">Punktu w czasie przywracania uwagi</span><span class="sxs-lookup"><span data-stu-id="91339-166">Point in time restore considerations</span></span>
<span data-ttu-id="91339-167">Podczas tworzenia nowej bazy danych przez [Przywracanie istniejącej bazy danych tooa określonego punktu w czasie](sql-database-recovery-using-backups.md), ma przechowywania danych czasowych wyłączona na poziomie bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="91339-167">When you create new database by [restoring existing database tooa specific point in time](sql-database-recovery-using-backups.md), it has temporal retention disabled at hello database level.</span></span> <span data-ttu-id="91339-168">(**is_temporal_history_retention_enabled** tooOFF ustawiona flaga).</span><span class="sxs-lookup"><span data-stu-id="91339-168">(**is_temporal_history_retention_enabled** flag set tooOFF).</span></span> <span data-ttu-id="91339-169">Ta funkcja umożliwia tooexamine zostaną usunięte wszystkie wiersze historycznych podczas przywracania, nie martwiąc, które przestarzałe wierszy, zanim będzie można pobrać tooquery je.</span><span class="sxs-lookup"><span data-stu-id="91339-169">This functionality allows you tooexamine all historical rows upon restore, without worrying that aged rows are removed before you get tooquery them.</span></span> <span data-ttu-id="91339-170">Służy on zbyt*sprawdzić historycznych danych poza okresem przechowywania skonfigurowanych*.</span><span class="sxs-lookup"><span data-stu-id="91339-170">You can use it too*inspect historical data beyond configured retention period*.</span></span>

<span data-ttu-id="91339-171">Załóżmy, że tabela danych czasowych ma podanego okresu przechowywania jeden miesiąc.</span><span class="sxs-lookup"><span data-stu-id="91339-171">Say that a temporal table has one MONTH retention period specified.</span></span> <span data-ttu-id="91339-172">Jeśli baza danych została utworzona w warstwie Premium usługi, będzie możliwe toocreate kopii bazy danych z hello stan bazy danych w górę too35 dni w przeszłości hello.</span><span class="sxs-lookup"><span data-stu-id="91339-172">If your database was created in Premium Service tier, you would be able toocreate database copy with hello database state up too35 days back in hello past.</span></span> <span data-ttu-id="91339-173">Które skutecznie pozwoli tooanalyze historycznych wierszy, które są uruchomione too65 dni przez bezpośrednie wysyłanie zapytań hello tabeli historii.</span><span class="sxs-lookup"><span data-stu-id="91339-173">That effectively would allow you tooanalyze historical rows that are up too65 days old by querying hello history table directly.</span></span>

<span data-ttu-id="91339-174">Oczyszczanie przechowywania danych tymczasowych tooactivate, uruchomić hello następującej instrukcji języka Transact-SQL po punkcie w czasie przywracania:</span><span class="sxs-lookup"><span data-stu-id="91339-174">If you want tooactivate temporal retention cleanup, run hello following Transact-SQL statement after point in time restore:</span></span>

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a><span data-ttu-id="91339-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91339-175">Next steps</span></span>
<span data-ttu-id="91339-176">jak toouse tabel danych czasowych w aplikacji, zapoznaj się z toolearn [wprowadzenie do tabel danych czasowych w bazie danych SQL Azure](sql-database-temporal-tables.md).</span><span class="sxs-lookup"><span data-stu-id="91339-176">toolearn how toouse Temporal Tables in your applications, check out [Getting Started with Temporal Tables in Azure SQL Database](sql-database-temporal-tables.md).</span></span>

<span data-ttu-id="91339-177">Toohear odwiedziny Channel 9 [klienta rzeczywistych danych czasowych implementacji Powodzenie wątku](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) i obejrzyj [live danych czasowych pokaz](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="91339-177">Visit Channel 9 toohear a [real customer temporal implementation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

<span data-ttu-id="91339-178">Aby uzyskać szczegółowe informacje o tabelach danych czasowych, przejrzyj [dokumentacji MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="91339-178">For detailed information about Temporal Tables, review [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>

