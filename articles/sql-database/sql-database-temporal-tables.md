---
title: Wprowadzenie do tabel danych czasowych w bazie danych Azure SQL | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak rozpocząć używanie tabel danych czasowych w bazie danych SQL Azure."
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
ms.openlocfilehash: d84db682089c65c2716d2d9bd92f7bc0ac47af27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="ddd11-103">Wprowadzenie do tabel danych czasowych w bazie danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="ddd11-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="ddd11-104">Tabele danych czasowych są nową funkcją programowalności bazy danych SQL Azure, umożliwiające śledzić i analizować pełną historię zmian danych, bez konieczności pisania kodu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="ddd11-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you to track and analyze the full history of changes in your data, without the need for custom coding.</span></span> <span data-ttu-id="ddd11-105">Tabele danych czasowych Zachowaj dane ściśle związane z kontekstu czasu, aby przechowywane dane mogą być interpretowane jako prawidłowy tylko w określonym okresie.</span><span class="sxs-lookup"><span data-stu-id="ddd11-105">Temporal Tables keep data closely related to time context so that stored facts can be interpreted as valid only within the specific period.</span></span> <span data-ttu-id="ddd11-106">Ta właściwość tabel danych czasowych umożliwia wydajne analizy na podstawie czasu i pobierania wgląd w dane dotyczące zmiany danych.</span><span class="sxs-lookup"><span data-stu-id="ddd11-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="ddd11-107">Scenariusz danych czasowych</span><span class="sxs-lookup"><span data-stu-id="ddd11-107">Temporal Scenario</span></span>
<span data-ttu-id="ddd11-108">W tym artykule przedstawiono kroki, aby korzystać z tabel danych czasowych w scenariuszu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ddd11-108">This article illustrates the steps to utilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="ddd11-109">Załóżmy, że chcesz śledzić aktywność użytkownika nowej witryny sieci Web, który jest obecnie opracowywane od początku lub w istniejącej witrynie internetowej, który ma zostać rozszerzony o analizowanie aktywności użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ddd11-109">Suppose that you want to track user activity on a new website that is being developed from scratch or on an existing website that you want to extend with user activity analytics.</span></span> <span data-ttu-id="ddd11-110">W tym przykładzie uproszczony przyjęto założenie, że liczba odwiedzane strony sieci web w okresie czasu jest wskaźnik musi zostać przechwycone i monitorowane w bazie danych witryny sieci Web, który znajduje się w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd11-110">In this simplified example, we assume that the number of visited web pages during a period of time is an indicator that needs to be captured and monitored in the website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="ddd11-111">Celem historycznej analizy aktywności użytkownika jest uzyskanie danych wejściowych do przeprojektowania witryny sieci Web i zapewnia lepsze środowisko dla gości.</span><span class="sxs-lookup"><span data-stu-id="ddd11-111">The goal of the historical analysis of user activity is to get inputs to redesign website and provide better experience for the visitors.</span></span>

<span data-ttu-id="ddd11-112">Model bazy danych dla tego scenariusza jest bardzo prosty — pomiar aktywności użytkownika odpowiada za pomocą pola jeden **PageVisited**i są przechwytywane oraz podstawowe informacje o profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ddd11-112">The database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on the user profile.</span></span> <span data-ttu-id="ddd11-113">Ponadto do analizy na podstawie czasu można zachowa serii wierszy dla każdego użytkownika, której każdy wiersz reprezentuje liczbę stron dany użytkownik odwiedzi w określonym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="ddd11-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents the number of pages a particular user visited within a specific period of time.</span></span>

![Schemat](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="ddd11-115">Na szczęście nie trzeba umieścić wszelkich starań w aplikacji, aby zachować informacje o działaniach.</span><span class="sxs-lookup"><span data-stu-id="ddd11-115">Fortunately, you do not need to put any effort in your app to maintain this activity information.</span></span> <span data-ttu-id="ddd11-116">W tabelach danych czasowych ten proces jest automatyczne — umożliwiając pełną elastyczność podczas projektowania witryny sieci Web i więcej czasu skupić się na analizy danych, do samej siebie.</span><span class="sxs-lookup"><span data-stu-id="ddd11-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time to focus on the data analysis itself.</span></span> <span data-ttu-id="ddd11-117">Jedyną operacją, musisz wykonać jest zapewnienie, że **WebSiteInfo** tabeli jest skonfigurowany jako [danych czasowych systemową kontrolą wersji](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="ddd11-117">The only thing you have to do is to ensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="ddd11-118">Dokładne kroki mogą korzystać z tabel danych czasowych w tym scenariuszu opisano poniżej.</span><span class="sxs-lookup"><span data-stu-id="ddd11-118">The exact steps to utilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="ddd11-119">Krok 1: Konfigurowanie tabel jako danych czasowych</span><span class="sxs-lookup"><span data-stu-id="ddd11-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="ddd11-120">W zależności od tego, czy są uruchamianie nowych aplikacji lub uaktualnienia istniejącej aplikacji zostanie Tworzenie tabel danych czasowych lub modyfikować istniejące przez dodanie atrybutów danych czasowych.</span><span class="sxs-lookup"><span data-stu-id="ddd11-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="ddd11-121">Ogólnie rzecz biorąc przypadku danego scenariusza można kombinacja tych dwóch opcji.</span><span class="sxs-lookup"><span data-stu-id="ddd11-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="ddd11-122">Wykonaj te za pomocą akcji [programu SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) lub inne narzędzie do projektowania języka Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="ddd11-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddd11-123">Zalecane jest używanie najnowszej wersji programu Management Studio, aby zachować synchronizację z aktualizacjami platformy Microsoft Azure i usługi SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ddd11-123">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="ddd11-124">[Zaktualizuj program SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddd11-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="ddd11-125">Utwórz nową tabelę</span><span class="sxs-lookup"><span data-stu-id="ddd11-125">Create new table</span></span>
<span data-ttu-id="ddd11-126">Użyj elementu menu kontekstowego "Nową tabelę systemową kontrolą wersji" w Eksploratorze obiektów w programie SSMS, Otwórz Edytor zapytań przy użyciu skryptu szablonu tabeli danych czasowych, a następnie użyć "Określ wartości dla parametrów szablonu" (Ctrl + Shift + M) do wypełniania szablonu:</span><span class="sxs-lookup"><span data-stu-id="ddd11-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer to open the query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) to populate the template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="ddd11-128">Programu SSDT wybierz szablon "Tabela danych czasowych (systemową)", podczas dodawania nowych elementów do projektu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="ddd11-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items to the database project.</span></span> <span data-ttu-id="ddd11-129">Które Otwórz projektanta tabel i umożliwiają łatwe określenie układu tabeli:</span><span class="sxs-lookup"><span data-stu-id="ddd11-129">That will open table designer and enable you to easily specify the table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="ddd11-131">Można również tworzenie tabeli danych czasowych, określając instrukcji języka Transact-SQL bezpośrednio, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ddd11-131">You can also a create temporal table by specifying the Transact-SQL statements directly, as shown in the example below.</span></span> <span data-ttu-id="ddd11-132">Należy zauważyć, że elementy obowiązkowe każda tabela danych czasowych definicji okresu i klauzuli SYSTEM_VERSIONING z odwołaniem do innej tabeli użytkownika, który będzie przechowywać wersje wierszy historycznych:</span><span class="sxs-lookup"><span data-stu-id="ddd11-132">Note that the mandatory elements of every temporal table are the PERIOD definition and the SYSTEM_VERSIONING clause with a reference to another user table that will store historical row versions:</span></span>

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

<span data-ttu-id="ddd11-133">Towarzyszący tabeli historii z domyślnej konfiguracji jest tworzony automatycznie podczas tworzenia tabeli danych czasowych z systemową kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="ddd11-133">When you create system-versioned temporal table, the accompanying history table with the default configuration is automatically created.</span></span> <span data-ttu-id="ddd11-134">Tabela historii domyślny zawiera B-drzewa indeksu klastrowanego na kolumny okresu (koniec, start) z włączoną kompresją strony.</span><span class="sxs-lookup"><span data-stu-id="ddd11-134">The default history table contains a clustered B-tree index on the period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="ddd11-135">Ta konfiguracja jest optymalna dla większości scenariuszy, w których są używane tabele danych czasowych, szczególnie w przypadku [inspekcja danych](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="ddd11-135">This configuration is optimal for the majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="ddd11-136">W tym przypadku firma Microsoft Staraj się wykonywać analizy trendów na podstawie czasu za pośrednictwem dłużej historii danych i większych zestawów danych, dlatego wybór magazynu dla tabeli historii jest klastrowany indeks magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="ddd11-136">In this particular case, we aim to perform time-based trend analysis over a longer data history and with bigger data sets, so the storage choice for the history table is a clustered columnstore index.</span></span> <span data-ttu-id="ddd11-137">Klastrowanego magazynu kolumn zawiera bardzo dobre kompresji i wydajności dla zapytań analitycznych.</span><span class="sxs-lookup"><span data-stu-id="ddd11-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="ddd11-138">Tabele danych czasowych umożliwiają skonfigurowanie indeksów w tabelach bieżących i danych czasowych całkowicie niezależnie.</span><span class="sxs-lookup"><span data-stu-id="ddd11-138">Temporal Tables give you the flexibility to configure indexes on the current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="ddd11-139">Indeksy magazynu kolumn są dostępne tylko w warstwie usług premium.</span><span class="sxs-lookup"><span data-stu-id="ddd11-139">Columnstore indexes are only available in the premium service tier.</span></span>
>

<span data-ttu-id="ddd11-140">Poniższy skrypt pokazuje, jak można zmienić domyślny indeks w tabeli historii do klastrowanego magazynu kolumn:</span><span class="sxs-lookup"><span data-stu-id="ddd11-140">The following script shows how default index on history table can be changed to the clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="ddd11-141">Tabele danych czasowych są reprezentowane w Eksploratorze obiektów z określonym ikonę ułatwiają identyfikację podczas jego tabeli historii jest wyświetlany jako węzeł podrzędny.</span><span class="sxs-lookup"><span data-stu-id="ddd11-141">Temporal Tables are represented in the Object Explorer with the specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-to-temporal"></a><span data-ttu-id="ddd11-143">Instrukcja ALTER istniejącej tabeli danych czasowych</span><span class="sxs-lookup"><span data-stu-id="ddd11-143">Alter existing table to temporal</span></span>
<span data-ttu-id="ddd11-144">Teraz obejmuje alternatywnych scenariusz, w którym tabeli WebsiteUserInfo już istnieje, ale nie została zaprojektowana w celu przechowywania historii zmian.</span><span class="sxs-lookup"><span data-stu-id="ddd11-144">Let’s cover the alternative scenario in which the WebsiteUserInfo table already exists, but was not designed to keep a history of changes.</span></span> <span data-ttu-id="ddd11-145">W takim przypadku można po prostu rozszerzyć istniejącą tabelę jako tymczasowa, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="ddd11-145">In this case, you can simply extend the existing table to become temporal, as shown in the following example:</span></span>

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

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="ddd11-146">Krok 2: Regularnego uruchamiania obciążenia</span><span class="sxs-lookup"><span data-stu-id="ddd11-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="ddd11-147">Główną zaletą tabel danych czasowych jest, nie trzeba zmienić lub dostosować witryny sieci Web w dowolny sposób, aby przeprowadzić śledzenie zmian.</span><span class="sxs-lookup"><span data-stu-id="ddd11-147">The main advantage of Temporal Tables is that you do not need to change or adjust your website in any way to perform change tracking.</span></span> <span data-ttu-id="ddd11-148">Po utworzeniu tabel danych czasowych niewidocznie utrwalić poprzednie wersje wiersza za każdym razem, gdy wykonywania modyfikacji danych w.</span><span class="sxs-lookup"><span data-stu-id="ddd11-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="ddd11-149">Aby korzystać z automatycznego śledzenia zmian dla tego scenariusza, umożliwia tylko zaktualizować kolumny **PagesVisited** za każdym razem, gdy użytkownik kończy się jego sesji w witrynie sieci Web:</span><span class="sxs-lookup"><span data-stu-id="ddd11-149">In order to leverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on the website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="ddd11-150">Należy zauważyć zapytanie update nie trzeba znać dokładny czas podczas bieżącej operacji wystąpił ani w jaki sposób dane historyczne zostaną zachowane dla przyszłych analizy.</span><span class="sxs-lookup"><span data-stu-id="ddd11-150">It is important to notice that the update query doesn’t need to know the exact time when the actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="ddd11-151">Zarówno aspekty automatycznie są obsługiwane przez bazę danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ddd11-151">Both aspects are automatically handled by the Azure SQL Database.</span></span> <span data-ttu-id="ddd11-152">Na poniższym diagramie przedstawiono, jak dane historii jest generowany na każdej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="ddd11-152">The following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="ddd11-154">Krok 3: Wykonanie analizy danych historycznych</span><span class="sxs-lookup"><span data-stu-id="ddd11-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="ddd11-155">Teraz po włączeniu danych czasowych system-versioning analizy danych historycznych jest tylko jedno zapytanie od użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ddd11-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="ddd11-156">W tym artykule, firma Microsoft udostępni kilka przykładów, które rozwiązują typowe scenariusze analizy — Aby poznać wszystkie szczegóły, zapoznaj się z różnymi opcjami wprowadzone w systemie [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) klauzuli.</span><span class="sxs-lookup"><span data-stu-id="ddd11-156">In this article, we will provide a few examples that address common analysis scenarios - to learn all details, explore various options introduced with the [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="ddd11-157">Aby wyświetlić najaktywniejszych użytkowników 10 uporządkowanych według liczby odwiedzane strony sieci web na godzinę temu, uruchom to zapytanie:</span><span class="sxs-lookup"><span data-stu-id="ddd11-157">To see the top 10 users ordered by the number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="ddd11-158">To zapytanie do analizowania wizyt lokacji dzień temu miesiąc temu można łatwo zmodyfikować lub w dowolnym momencie w ciągu ostatnich ma.</span><span class="sxs-lookup"><span data-stu-id="ddd11-158">You can easily modify this query to analyze the site visits as of a day ago, a month ago or at any point in the past you wish.</span></span>

<span data-ttu-id="ddd11-159">Aby wykonać podstawowe analiz statystycznych z poprzedniego dnia, skorzystaj z następującego przykładu:</span><span class="sxs-lookup"><span data-stu-id="ddd11-159">To perform basic statistical analysis for the previous day, use the following example:</span></span>

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

<span data-ttu-id="ddd11-160">Aby wyszukać działania określonego użytkownika, w określonym przedziale czasu, użyj klauzuli zawarte w:</span><span class="sxs-lookup"><span data-stu-id="ddd11-160">To search for activities of a specific user, within a period of time, use the CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="ddd11-161">Graficzne wizualizacji jest szczególnie wygodne czasowych zapytań, jak można wyświetlić trendów i wzorców użytkowania w intuicyjny sposób bardzo łatwo:</span><span class="sxs-lookup"><span data-stu-id="ddd11-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="ddd11-163">Schemat tabeli zmieniające się</span><span class="sxs-lookup"><span data-stu-id="ddd11-163">Evolving table schema</span></span>
<span data-ttu-id="ddd11-164">Zazwyczaj należy zmienić schemat tabeli danych czasowych podczas operacji tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ddd11-164">Typically, you will need to change the temporal table schema while you are doing app development.</span></span> <span data-ttu-id="ddd11-165">W tym wystarczy uruchomić regularne instrukcji ALTER TABLE instrukcje i bazy danych SQL Azure odpowiednio rozpropaguje zmiany do tabeli historii.</span><span class="sxs-lookup"><span data-stu-id="ddd11-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes to the history table.</span></span> <span data-ttu-id="ddd11-166">Poniższy skrypt pokazuje, jak dodać dodatkowe atrybut śledzenia:</span><span class="sxs-lookup"><span data-stu-id="ddd11-166">The following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="ddd11-167">Podobnie można zmienić definicji kolumny, gdy obciążenie jest aktywna:</span><span class="sxs-lookup"><span data-stu-id="ddd11-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase the length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="ddd11-168">Na koniec można usunąć kolumny, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="ddd11-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="ddd11-169">Można również użyć najnowszej [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) zmiany schematu tabeli danych czasowych podczas połączenia z bazą danych (w trybie online) lub w ramach projektu bazy danych (w trybie offline).</span><span class="sxs-lookup"><span data-stu-id="ddd11-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) to change temporal table schema while you are connected to the database (online mode) or as part of the database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="ddd11-170">Kontrolowanie przechowywania danych historycznych</span><span class="sxs-lookup"><span data-stu-id="ddd11-170">Controlling retention of historical data</span></span>
<span data-ttu-id="ddd11-171">Tabela historii może zwiększyć tabelach danych czasowych z systemową kontrolą wersji baz danych o rozmiarze ponad zwykłych tabelach.</span><span class="sxs-lookup"><span data-stu-id="ddd11-171">With system-versioned temporal tables, the history table may increase the database size more than regular tables.</span></span> <span data-ttu-id="ddd11-172">Tabel historii duży i coraz dłuższej może stać się problemem zarówno z powodu kosztów czystego magazynu, a także nakładające wydajności podatek danych czasowych zapytań.</span><span class="sxs-lookup"><span data-stu-id="ddd11-172">A large and ever-growing history table can become an issue both due to pure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="ddd11-173">W związku z tym tworzenie zasad przechowywania danych zarządzania danymi w tabeli historii jest istotnym elementem planowania i zarządzanie cyklem życia każda tabela danych czasowych.</span><span class="sxs-lookup"><span data-stu-id="ddd11-173">Hence, developing a data retention policy for managing data in the history table is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="ddd11-174">Z bazy danych SQL Azure masz następujące podejścia do zarządzania danych historycznych w tabeli danych czasowych:</span><span class="sxs-lookup"><span data-stu-id="ddd11-174">With Azure SQL Database, you have the following approaches for managing historical data in the temporal table:</span></span>

* [<span data-ttu-id="ddd11-175">Partycjonowanie tabel</span><span class="sxs-lookup"><span data-stu-id="ddd11-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="ddd11-176">Skrypt czyszczący niestandardowych</span><span class="sxs-lookup"><span data-stu-id="ddd11-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="ddd11-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ddd11-177">Next steps</span></span>
<span data-ttu-id="ddd11-178">Aby uzyskać szczegółowe informacje w tabelach danych czasowych, zapoznaj się z [dokumentacji MSDN](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="ddd11-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="ddd11-179">Odwiedź Channel 9, aby usłyszeć [klienta rzeczywistych danych czasowych implementacji Powodzenie wątku](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) i obejrzyj [live pokaz danych czasowych](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="ddd11-179">Visit Channel 9 to hear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

