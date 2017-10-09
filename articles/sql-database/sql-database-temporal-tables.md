---
title: "aaaGetting rozpoczęte w tabelach danych czasowych w bazie danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooget pracę z przy użyciu tabel danych czasowych w bazie danych SQL Azure."
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="d4b7b-103">Wprowadzenie do tabel danych czasowych w bazie danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="d4b7b-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="d4b7b-104">Tabele danych czasowych są nową funkcją programowalności bazy danych SQL Azure, która pozwala tootrack i analizować hello pełną historię zmian danych, bez potrzeby hello programowania.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you tootrack and analyze hello full history of changes in your data, without hello need for custom coding.</span></span> <span data-ttu-id="d4b7b-105">Tabele danych czasowych zachować kontekstu tootime ściśle powiązanych danych, aby przechowywane dane mogą być interpretowane jako prawidłowy tylko w określonym okresie hello.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-105">Temporal Tables keep data closely related tootime context so that stored facts can be interpreted as valid only within hello specific period.</span></span> <span data-ttu-id="d4b7b-106">Ta właściwość tabel danych czasowych umożliwia wydajne analizy na podstawie czasu i pobierania wgląd w dane dotyczące zmiany danych.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="d4b7b-107">Scenariusz danych czasowych</span><span class="sxs-lookup"><span data-stu-id="d4b7b-107">Temporal Scenario</span></span>
<span data-ttu-id="d4b7b-108">W tym artykule przedstawiono hello kroki tooutilize tabel danych czasowych w scenariuszu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-108">This article illustrates hello steps tooutilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="d4b7b-109">Załóżmy, że chcesz tootrack aktywność użytkownika na nowej witryny sieci Web, który jest obecnie opracowywane od początku lub na istniejącej witryny sieci Web, które mają tooextend z analizowanie aktywności użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-109">Suppose that you want tootrack user activity on a new website that is being developed from scratch or on an existing website that you want tooextend with user activity analytics.</span></span> <span data-ttu-id="d4b7b-110">W tym przykładzie uproszczony przyjęto założenie, że hello liczbę odwiedzonych stron sieci web w okresie czasu jest wskaźnik musi toobe przechwycony i monitorowane w bazie danych witryny sieci Web hello, który znajduje się w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-110">In this simplified example, we assume that hello number of visited web pages during a period of time is an indicator that needs toobe captured and monitored in hello website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="d4b7b-111">Celem Hello hello historycznej analizy aktywności użytkownika tooget dane wejściowe tooredesign witryny sieci Web i zapewnia lepsze środowisko dla użytkowników zewnętrznych hello.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-111">hello goal of hello historical analysis of user activity is tooget inputs tooredesign website and provide better experience for hello visitors.</span></span>

<span data-ttu-id="d4b7b-112">Witaj modelu bazy danych dla tego scenariusza jest bardzo prosty — pomiar aktywności użytkownika odpowiada za pomocą pola jeden **PageVisited**i są przechwytywane oraz podstawowe informacje na temat hello profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-112">hello database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on hello user profile.</span></span> <span data-ttu-id="d4b7b-113">Ponadto do analizy na podstawie czasu można zachowa serii wierszy dla każdego użytkownika, której każdy wiersz reprezentuje hello liczbę stron, dany użytkownik odwiedzi w określonym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents hello number of pages a particular user visited within a specific period of time.</span></span>

![Schemat](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="d4b7b-115">Na szczęście, nie trzeba tooput wszelkich starań w Twojej aplikacji toomaintain informacje te działania.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-115">Fortunately, you do not need tooput any effort in your app toomaintain this activity information.</span></span> <span data-ttu-id="d4b7b-116">W tabelach danych czasowych ten proces jest automatyczne — umożliwiając pełną elastyczność podczas projektowania witryny sieci Web i więcej toofocus czas na powitania analizy danych, sama.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time toofocus on hello data analysis itself.</span></span> <span data-ttu-id="d4b7b-117">Witaj, co ma toodo jest tooensure tylko który **WebSiteInfo** tabeli jest skonfigurowany jako [danych czasowych systemową kontrolą wersji](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="d4b7b-117">hello only thing you have toodo is tooensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="d4b7b-118">Witaj kolejnych kroków tooutilize tabel danych czasowych w tym scenariuszu opisano poniżej.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-118">hello exact steps tooutilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="d4b7b-119">Krok 1: Konfigurowanie tabel jako danych czasowych</span><span class="sxs-lookup"><span data-stu-id="d4b7b-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="d4b7b-120">W zależności od tego, czy są uruchamianie nowych aplikacji lub uaktualnienia istniejącej aplikacji zostanie Tworzenie tabel danych czasowych lub modyfikować istniejące przez dodanie atrybutów danych czasowych.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="d4b7b-121">Ogólnie rzecz biorąc przypadku danego scenariusza można kombinacja tych dwóch opcji.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="d4b7b-122">Wykonaj te za pomocą akcji [programu SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) lub inne narzędzie do projektowania języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4b7b-123">Zalecane jest, aby zawsze używała hello najnowszej wersji programu Management Studio tooremain synchronizowane z tooMicrosoft aktualizacje, Azure i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-123">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="d4b7b-124">[Zaktualizuj program SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4b7b-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="d4b7b-125">Utwórz nową tabelę</span><span class="sxs-lookup"><span data-stu-id="d4b7b-125">Create new table</span></span>
<span data-ttu-id="d4b7b-126">W menu kontekstowym "Nową tabelę systemową kontrolą wersji" w edytorze zapytań hello tooopen Eksplorator obiektów programu SSMS za pomocą skryptu szablonu tabeli danych czasowych, a następnie użyć szablonu hello toopopulate "Określ wartości dla parametrów szablonu" (Ctrl + Shift + M):</span><span class="sxs-lookup"><span data-stu-id="d4b7b-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer tooopen hello query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) toopopulate hello template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="d4b7b-128">Programu SSDT wybierz szablon "(systemową) tabeli danych czasowych" podczas dodawania nowych elementów toohello bazy danych projektu.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items toohello database project.</span></span> <span data-ttu-id="d4b7b-129">Czy będzie designer Otwórz tabelę i Włącz tooeasily możesz określić hello układu tabeli:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-129">That will open table designer and enable you tooeasily specify hello table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="d4b7b-131">Można również tworzenie tabeli danych czasowych, określając instrukcji języka Transact-SQL hello bezpośrednio, jak pokazano w poniższym przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-131">You can also a create temporal table by specifying hello Transact-SQL statements directly, as shown in hello example below.</span></span> <span data-ttu-id="d4b7b-132">Należy zauważyć, że elementy obowiązkowe hello każda tabela danych czasowych klauzuli SYSTEM_VERSIONING hello z tabelą użytkownika tooanother odwołania, który będzie przechowywać wersje wierszy historycznych i definicji okresu hello:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-132">Note that hello mandatory elements of every temporal table are hello PERIOD definition and hello SYSTEM_VERSIONING clause with a reference tooanother user table that will store historical row versions:</span></span>

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

<span data-ttu-id="d4b7b-133">Hello towarzyszące tabeli historii z konfiguracji domyślnej hello jest tworzony automatycznie podczas tworzenia tabeli danych czasowych z systemową kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-133">When you create system-versioned temporal table, hello accompanying history table with hello default configuration is automatically created.</span></span> <span data-ttu-id="d4b7b-134">Tabela historii domyślne Hello zawiera B-drzewa indeksu klastrowanego na kolumny okresu hello (koniec, start) z włączoną kompresją strony.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-134">hello default history table contains a clustered B-tree index on hello period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="d4b7b-135">Ta konfiguracja jest optymalna dla hello większość scenariuszy, w których są używane tabele danych czasowych, szczególnie w przypadku [inspekcja danych](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="d4b7b-135">This configuration is optimal for hello majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="d4b7b-136">W tym przypadku firma Microsoft osiągnięcia analizy trendów na podstawie czasu tooperform za pośrednictwem dłużej historii danych i większych zestawów danych, więc hello wybór magazynu dla tabeli historii hello jest klastrowany indeks magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-136">In this particular case, we aim tooperform time-based trend analysis over a longer data history and with bigger data sets, so hello storage choice for hello history table is a clustered columnstore index.</span></span> <span data-ttu-id="d4b7b-137">Klastrowanego magazynu kolumn zawiera bardzo dobre kompresji i wydajności dla zapytań analitycznych.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="d4b7b-138">Całkowicie niezależnie hello elastyczność tooconfigure indeksów w tabelach bieżących i danych czasowych hello podać tabel danych czasowych.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-138">Temporal Tables give you hello flexibility tooconfigure indexes on hello current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="d4b7b-139">Indeksy magazynu kolumn są dostępne tylko w warstwie usług premium hello.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-139">Columnstore indexes are only available in hello premium service tier.</span></span>
>

<span data-ttu-id="d4b7b-140">Witaj następującego skryptu pokazuje, jak domyślny indeks w tabeli historii może być zmienione toohello klastrowanego magazynu kolumn:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-140">hello following script shows how default index on history table can be changed toohello clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="d4b7b-141">Tabele danych czasowych są reprezentowane w hello Eksplorator obiektów z określonych ikonę hello ułatwiają identyfikację podczas jego tabeli historii jest wyświetlany jako węzeł podrzędny.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-141">Temporal Tables are represented in hello Object Explorer with hello specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a><span data-ttu-id="d4b7b-143">Zmienia istniejące tootemporal tabeli</span><span class="sxs-lookup"><span data-stu-id="d4b7b-143">Alter existing table tootemporal</span></span>
<span data-ttu-id="d4b7b-144">Teraz obejmuje hello alternatywnych scenariusz, w których hello WebsiteUserInfo tabeli już istnieje, ale nie zostało zaprojektowane tookeep historię zmian.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-144">Let’s cover hello alternative scenario in which hello WebsiteUserInfo table already exists, but was not designed tookeep a history of changes.</span></span> <span data-ttu-id="d4b7b-145">W takim przypadku można po prostu rozszerzyć hello istniejącej tabeli toobecome danych czasowych, jak pokazano na powitania poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-145">In this case, you can simply extend hello existing table toobecome temporal, as shown in hello following example:</span></span>

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="d4b7b-146">Krok 2: Regularnego uruchamiania obciążenia</span><span class="sxs-lookup"><span data-stu-id="d4b7b-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="d4b7b-147">główną zaletą tabel danych czasowych w Hello jest możesz nie wymagają toochange lub Dostosuj witryny sieci Web w sposób zmiany tooperform śledzenia.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-147">hello main advantage of Temporal Tables is that you do not need toochange or adjust your website in any way tooperform change tracking.</span></span> <span data-ttu-id="d4b7b-148">Po utworzeniu tabel danych czasowych niewidocznie utrwalić poprzednie wersje wiersza za każdym razem, gdy wykonywania modyfikacji danych w.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="d4b7b-149">W kolejności tooleverage śledzenie zmian automatycznego dla tego scenariusza, umożliwia tylko zaktualizować kolumny **PagesVisited** za każdym razem, gdy użytkownik kończy się jego sesji w witrynie sieci Web hello:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-149">In order tooleverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on hello website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="d4b7b-150">Jest ważne toonotice, który hello zapytanie update nie musi tooknow hello dokładny czas, gdy podczas bieżącej operacji hello ani w jaki sposób dane historyczne zostaną zachowane dla przyszłych analizy.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-150">It is important toonotice that hello update query doesn’t need tooknow hello exact time when hello actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="d4b7b-151">Zarówno aspekty automatycznie są obsługiwane przez hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-151">Both aspects are automatically handled by hello Azure SQL Database.</span></span> <span data-ttu-id="d4b7b-152">Witaj poniższym diagramie przedstawiono sposób dane historii jest generowany na każdej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-152">hello following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="d4b7b-154">Krok 3: Wykonanie analizy danych historycznych</span><span class="sxs-lookup"><span data-stu-id="d4b7b-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="d4b7b-155">Teraz po włączeniu danych czasowych system-versioning analizy danych historycznych jest tylko jedno zapytanie od użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="d4b7b-156">W tym artykule, firma Microsoft będzie zawierają kilka przykładów, które rozwiązują typowe scenariusze analizy - toolearn wszystkie szczegółowe informacje, zapoznaj się różne opcje wprowadzone w systemie hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) klauzuli.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-156">In this article, we will provide a few examples that address common analysis scenarios - toolearn all details, explore various options introduced with hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="d4b7b-157">toosee hello 10 użytkownicy z największą uporządkowanych według liczby hello odwiedzane strony sieci web na godzinę temu, uruchom to zapytanie:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-157">toosee hello top 10 users ordered by hello number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="d4b7b-158">To zapytanie może dopasowywać tooanalyze hello wizyty dzień temu miesiąc temu lub w dowolnym momencie w przeszłości hello ma.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-158">You can easily modify this query tooanalyze hello site visits as of a day ago, a month ago or at any point in hello past you wish.</span></span>

<span data-ttu-id="d4b7b-159">dla hello podstawowych celów analizy statystycznej tooperform poprzedniego dnia, użyj hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-159">tooperform basic statistical analysis for hello previous day, use hello following example:</span></span>

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

<span data-ttu-id="d4b7b-160">toosearch działań określonego użytkownika, w określonym przedziale czasu, użyj hello ZAWARTEJ w klauzuli:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-160">toosearch for activities of a specific user, within a period of time, use hello CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="d4b7b-161">Graficzne wizualizacji jest szczególnie wygodne czasowych zapytań, jak można wyświetlić trendów i wzorców użytkowania w intuicyjny sposób bardzo łatwo:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="d4b7b-163">Schemat tabeli zmieniające się</span><span class="sxs-lookup"><span data-stu-id="d4b7b-163">Evolving table schema</span></span>
<span data-ttu-id="d4b7b-164">Zazwyczaj należy schemat tabeli danych czasowych hello toochange podczas operacji tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-164">Typically, you will need toochange hello temporal table schema while you are doing app development.</span></span> <span data-ttu-id="d4b7b-165">W tym wystarczy uruchomić regularne instrukcji ALTER TABLE i bazy danych SQL Azure odpowiednio rozpropaguje zmiany toohello historii tabeli.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes toohello history table.</span></span> <span data-ttu-id="d4b7b-166">Witaj poniższy skrypt pokazuje, jak dodać dodatkowe atrybut śledzenia:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-166">hello following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="d4b7b-167">Podobnie można zmienić definicji kolumny, gdy obciążenie jest aktywna:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="d4b7b-168">Na koniec można usunąć kolumny, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="d4b7b-169">Można również użyć najnowszej [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange danych czasowych tabeli schematu, gdy są połączone toohello bazy danych (w trybie online) lub jako część hello projekt bazy danych (w trybie offline).</span><span class="sxs-lookup"><span data-stu-id="d4b7b-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal table schema while you are connected toohello database (online mode) or as part of hello database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="d4b7b-170">Kontrolowanie przechowywania danych historycznych</span><span class="sxs-lookup"><span data-stu-id="d4b7b-170">Controlling retention of historical data</span></span>
<span data-ttu-id="d4b7b-171">Tabela historii hello może zwiększyć tabelach danych czasowych z systemową kontrolą wersji hello baz danych o rozmiarze ponad zwykłych tabelach.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-171">With system-versioned temporal tables, hello history table may increase hello database size more than regular tables.</span></span> <span data-ttu-id="d4b7b-172">Tabel historii duży i coraz dłuższej może stać się problemem w obu toopure kosztów magazynowania, a także nakładające wydajności podatek danych czasowych zapytań.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-172">A large and ever-growing history table can become an issue both due toopure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="d4b7b-173">W związku z tym tworzenie zasad przechowywania danych zarządzania danymi w tabeli historii hello jest istotnym elementem planowania i zarządzanie cyklem życia hello każdej tabeli danych czasowych.</span><span class="sxs-lookup"><span data-stu-id="d4b7b-173">Hence, developing a data retention policy for managing data in hello history table is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="d4b7b-174">Z bazy danych SQL Azure masz następujące podejścia do zarządzania danych historycznych w tabeli danych czasowych hello hello:</span><span class="sxs-lookup"><span data-stu-id="d4b7b-174">With Azure SQL Database, you have hello following approaches for managing historical data in hello temporal table:</span></span>

* [<span data-ttu-id="d4b7b-175">Partycjonowanie tabel</span><span class="sxs-lookup"><span data-stu-id="d4b7b-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="d4b7b-176">Skrypt czyszczący niestandardowych</span><span class="sxs-lookup"><span data-stu-id="d4b7b-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="d4b7b-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4b7b-177">Next steps</span></span>
<span data-ttu-id="d4b7b-178">Aby uzyskać szczegółowe informacje w tabelach danych czasowych, zapoznaj się z [dokumentacji MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4b7b-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="d4b7b-179">Toohear odwiedziny Channel 9 [klienta rzeczywistych danych czasowych implementacji Powodzenie wątku](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) i obejrzyj [live danych czasowych pokaz](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="d4b7b-179">Visit Channel 9 toohear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

