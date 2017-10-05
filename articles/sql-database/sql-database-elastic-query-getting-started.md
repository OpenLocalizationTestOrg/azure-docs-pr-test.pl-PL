---
title: "Raport dla baz danych chmury skalowalnych w poziomie (poziomy podziału) | Dokumentacja firmy Microsoft"
description: "jak używać wielu zapytań bazy danych dla bazy danych"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: 8eb56d44c3a261f6325d4fc91f169d09bf108160
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="13f6a-103">Raport w chmurze skalowalnych w poziomie bazy danych (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="13f6a-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="13f6a-104">Możesz utworzyć raporty z wielu baz danych Azure SQL z punktu pojedynczego połączenia przy użyciu [elastycznej zapytania](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13f6a-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="13f6a-105">Bazy danych musi być podzielony w poziomie, (określane również jako "podzielonej").</span><span class="sxs-lookup"><span data-stu-id="13f6a-105">The databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="13f6a-106">Jeśli masz istniejącą bazę danych, zobacz [Migrowanie istniejących baz danych do baz danych skalowalnych w poziomie](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="13f6a-106">If you have an existing database, see [Migrating existing databases to scaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="13f6a-107">Aby poznać obiektów SQL potrzebne do zapytania, zobacz [zapytanie na poziomie partycjonowanej baz danych](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="13f6a-107">To understand the SQL objects needed to query, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13f6a-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="13f6a-108">Prerequisites</span></span>
<span data-ttu-id="13f6a-109">Pobierz i uruchom [wprowadzenie próbki narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="13f6a-109">Download and run the [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-the-sample-app"></a><span data-ttu-id="13f6a-110">Utwórz identyfikator niezależnego fragmentu mapy manager za pomocą przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="13f6a-110">Create a shard map manager using the sample app</span></span>
<span data-ttu-id="13f6a-111">W tym polu spowoduje utworzenie mapy niezależnego fragmentu manager oraz kilka fragmentów, następuje wstawiania danych do fragmentów.</span><span class="sxs-lookup"><span data-stu-id="13f6a-111">Here you will create a shard map manager along with several shards, followed by insertion of data into the shards.</span></span> <span data-ttu-id="13f6a-112">Jeśli możesz już mają ustawienia fragmentów danych podzielonej w nich, możesz pominąć następujące kroki i przejść do następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="13f6a-112">If you happen to already have shards setup with sharded data in them, you can skip the following steps and move to the next section.</span></span>

1. <span data-ttu-id="13f6a-113">Tworzenie i uruchamianie **wprowadzenie do korzystania z narzędzi elastycznej bazy danych** przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="13f6a-113">Build and run the **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="13f6a-114">Postępuj zgodnie z instrukcjami aż do kroku 7 w sekcji [pobieranie i uruchamianie aplikacji przykładowej](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="13f6a-114">Follow the steps until step 7 in the section [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="13f6a-115">Po zakończeniu kroku 7 zostanie wyświetlony następujący wiersz polecenia:</span><span class="sxs-lookup"><span data-stu-id="13f6a-115">At the end of Step 7, you will see the following command prompt:</span></span>

    ![Wiersz polecenia][1]
2. <span data-ttu-id="13f6a-117">W oknie wiersza polecenia wpisz "1" i naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="13f6a-117">In the command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="13f6a-118">Tworzy identyfikator niezależnego fragmentu menedżera map i dodaje dwa niezależne do serwera.</span><span class="sxs-lookup"><span data-stu-id="13f6a-118">This creates the shard map manager, and adds two shards to the server.</span></span> <span data-ttu-id="13f6a-119">Następnie wpisz "3" i naciśnij klawisz **Enter**; powtórzenie akcji cztery razy.</span><span class="sxs-lookup"><span data-stu-id="13f6a-119">Then type "3" and press **Enter**; repeat the action four times.</span></span> <span data-ttu-id="13f6a-120">Wstawia Przykładowe wiersze danych z fragmentów.</span><span class="sxs-lookup"><span data-stu-id="13f6a-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="13f6a-121">[Portalu Azure](https://portal.azure.com) powinny być widoczne trzech nowych baz danych na serwerze:</span><span class="sxs-lookup"><span data-stu-id="13f6a-121">The [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Visual Studio potwierdzenia][2]

   <span data-ttu-id="13f6a-123">W tym momencie między bazami danych zapytania są obsługiwane za pomocą biblioteki klienta elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="13f6a-123">At this point, cross-database queries are supported through the Elastic Database client libraries.</span></span> <span data-ttu-id="13f6a-124">Na przykład opcja 4 w oknie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="13f6a-124">For example, use option 4 in the command window.</span></span> <span data-ttu-id="13f6a-125">Wyniki zapytania wielu niezależnych są zawsze **UNION ALL** wyników z wszystkich fragmentów.</span><span class="sxs-lookup"><span data-stu-id="13f6a-125">The results from a multi-shard query are always a **UNION ALL** of the results from all shards.</span></span>

   <span data-ttu-id="13f6a-126">W następnej sekcji utworzymy punktu końcowego bazy danych przykładowych obsługującego bardziej zaawansowane funkcje zapytań danych w liczbie fragmentów.</span><span class="sxs-lookup"><span data-stu-id="13f6a-126">In the next section, we create a sample database endpoint that supports richer querying of the data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="13f6a-127">Tworzenie elastycznej kwerendy bazy danych</span><span class="sxs-lookup"><span data-stu-id="13f6a-127">Create an elastic query database</span></span>
1. <span data-ttu-id="13f6a-128">Otwórz [portalu Azure](https://portal.azure.com) i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="13f6a-128">Open the [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="13f6a-129">Utwórz nową bazę danych Azure SQL, w tym samym serwerze co konfigurację niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="13f6a-129">Create a new Azure SQL database in the same server as your shard setup.</span></span> <span data-ttu-id="13f6a-130">Nazwa bazy danych "ElasticDBQuery."</span><span class="sxs-lookup"><span data-stu-id="13f6a-130">Name the database "ElasticDBQuery."</span></span>

    ![Portalu Azure i warstwę cenową][3]

    > [!NOTE]
    > <span data-ttu-id="13f6a-132">można użyć istniejącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="13f6a-132">you can use an existing database.</span></span> <span data-ttu-id="13f6a-133">Jeśli to zrobisz, nie może być jednym z fragmentów, które chcesz wykonać zapytania na.</span><span class="sxs-lookup"><span data-stu-id="13f6a-133">If you can do so, it must not be one of the shards that you would like to execute your queries on.</span></span> <span data-ttu-id="13f6a-134">Ta baza danych będzie służyć do tworzenia obiektów metadanych dla zapytania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="13f6a-134">This database will be used for creating the metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="13f6a-135">Tworzenie obiektów bazy danych</span><span class="sxs-lookup"><span data-stu-id="13f6a-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="13f6a-136">Klucz główny o zakresie bazy danych i poświadczeń</span><span class="sxs-lookup"><span data-stu-id="13f6a-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="13f6a-137">Są one używane do nawiązania połączenia Menedżera mapy niezależnego fragmentu i odłamków:</span><span class="sxs-lookup"><span data-stu-id="13f6a-137">These are used to connect to the shard map manager and the shards:</span></span>

1. <span data-ttu-id="13f6a-138">Otwórz program SQL Server Management Studio lub SQL Server Data Tools w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="13f6a-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="13f6a-139">Łączenia z bazą danych ElasticDBQuery i wykonaj następujące polecenia T-SQL:</span><span class="sxs-lookup"><span data-stu-id="13f6a-139">Connect to ElasticDBQuery database and execute the following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="13f6a-140">"username" i "password" powinny być takie same jak informacje logowania używany w kroku 6 [pobieranie i uruchamianie aplikacji przykładowej](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) w [wprowadzenie do korzystania z narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="13f6a-140">"username" and "password" should be the same as login information used in step 6 of [Download and run the sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="13f6a-141">Zewnętrzne źródła danych</span><span class="sxs-lookup"><span data-stu-id="13f6a-141">External data sources</span></span>
<span data-ttu-id="13f6a-142">Aby utworzyć zewnętrznego źródła danych, uruchom następujące polecenie w bazie danych ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="13f6a-142">To create an external data source, execute the following command on the ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="13f6a-143">"CustomerIDShardMap" jest nazwą mapy niezależnego fragmentu, jeśli utworzono mapy niezależnego fragmentu i Menedżera mapy niezależnego fragmentu przy użyciu przykładowych narzędzi elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="13f6a-143">"CustomerIDShardMap" is the name of the shard map, if you created the shard map and shard map manager using the elastic database tools sample.</span></span> <span data-ttu-id="13f6a-144">Jednak jeśli używasz niestandardowych ustawień dla tego przykładu, następnie należy wybrana w aplikacji Nazwa mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="13f6a-144">However, if you used your custom setup for this sample, then it should be the shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="13f6a-145">Tabele zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="13f6a-145">External tables</span></span>
<span data-ttu-id="13f6a-146">Tworzenie tabeli zewnętrznej zgodny tabeli Klienci na odłamków, wykonując następujące polecenie na ElasticDBQuery bazy danych:</span><span class="sxs-lookup"><span data-stu-id="13f6a-146">Create an external table that matches the Customers table on the shards by executing the following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="13f6a-147">Wykonywanie przykładowego zapytania T-SQL elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="13f6a-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="13f6a-148">Po zdefiniowaniu zewnętrznym źródle danych i tabele zewnętrzne mogą teraz używać pełnej T-SQL w tabelach zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="13f6a-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="13f6a-149">Wykonaj tę kwerendę w bazie danych ElasticDBQuery:</span><span class="sxs-lookup"><span data-stu-id="13f6a-149">Execute this query on the ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="13f6a-150">Można zauważyć, że zapytanie agreguje wyniki wszystkich odłamków i zapewnia następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="13f6a-150">You will notice that the query aggregates results from all the shards and gives the following output:</span></span>

![Szczegóły danych wyjściowych][4]

## <a name="import-elastic-database-query-results-to-excel"></a><span data-ttu-id="13f6a-152">Importuj wyniki zapytania elastycznej bazy danych do programu Excel</span><span class="sxs-lookup"><span data-stu-id="13f6a-152">Import elastic database query results to Excel</span></span>
 <span data-ttu-id="13f6a-153">Możesz zaimportować wyników zapytania do pliku programu Excel.</span><span class="sxs-lookup"><span data-stu-id="13f6a-153">You can import the results from of a query to an Excel file.</span></span>

1. <span data-ttu-id="13f6a-154">Uruchom program Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="13f6a-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="13f6a-155">Przejdź do **danych** wstążki.</span><span class="sxs-lookup"><span data-stu-id="13f6a-155">Navigate to the **Data** ribbon.</span></span>
3. <span data-ttu-id="13f6a-156">Kliknij przycisk **z innych źródeł** i kliknij przycisk **z programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="13f6a-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importowania z programu Excel z innych źródeł][5]
4. <span data-ttu-id="13f6a-158">W **Kreator połączenia danych** wpisz poświadczenia, a nazwa logowania serwera.</span><span class="sxs-lookup"><span data-stu-id="13f6a-158">In the **Data Connection Wizard** type the server name and login credentials.</span></span> <span data-ttu-id="13f6a-159">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="13f6a-159">Then click **Next**.</span></span>
5. <span data-ttu-id="13f6a-160">W oknie dialogowym **wybierz bazę danych, która zawiera dane, które mają**, wybierz pozycję **ElasticDBQuery** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="13f6a-160">In the dialog box **Select the database that contains the data you want**, select the **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="13f6a-161">Wybierz **klientów** tabeli w widoku listy, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="13f6a-161">Select the **Customers** table in the list view and click **Next**.</span></span> <span data-ttu-id="13f6a-162">Następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="13f6a-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="13f6a-163">W **i zaimportuj dane** formularza, w obszarze **wybierz sposób wyświetlania tych danych w skoroszycie**, wybierz pozycję **tabeli** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="13f6a-163">In the **Import Data** form, under **Select how you want to view this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="13f6a-164">Wszystkie wiersze z **klientów** tabeli, przechowywane w różnych odłamków wypełnić arkuszu programu Excel.</span><span class="sxs-lookup"><span data-stu-id="13f6a-164">All the rows from **Customers** table, stored in different shards populate the Excel sheet.</span></span>

<span data-ttu-id="13f6a-165">Możesz teraz użyć funkcji wizualizacji zaawansowanych danych programu Excel.</span><span class="sxs-lookup"><span data-stu-id="13f6a-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="13f6a-166">Parametry połączenia z nazwą serwera, nazwa bazy danych i poświadczeń służy do nawiązania narzędzi integracji danych i analizy Biznesowej kwerendy elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="13f6a-166">You can use the connection string with your server name, database name and credentials to connect your BI and data integration tools to the elastic query database.</span></span> <span data-ttu-id="13f6a-167">Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="13f6a-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="13f6a-168">Może się odwoływać do kwerendy elastycznej bazy danych i tabele zewnętrzne, podobnie jak wszystkie inne bazy danych programu SQL Server i tabel programu SQL Server, które można połączyć się z narzędziem.</span><span class="sxs-lookup"><span data-stu-id="13f6a-168">You can refer to the elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect to with your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="13f6a-169">Koszty</span><span class="sxs-lookup"><span data-stu-id="13f6a-169">Cost</span></span>
<span data-ttu-id="13f6a-170">Brak bez dodatkowych opłat dla funkcji elastycznej kwerendy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="13f6a-170">There is no additional charge for using the Elastic Database Query feature.</span></span>

<span data-ttu-id="13f6a-171">Aby uzyskać informacje o cenach zobacz [szczegóły cennika bazy danych SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="13f6a-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="13f6a-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="13f6a-172">Next steps</span></span>

* <span data-ttu-id="13f6a-173">Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13f6a-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="13f6a-174">Samouczek partycjonowania pionowego, zobacz [wprowadzenie do korzystania z bazy danych między kwerendy (partycjonowanie pionowe)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="13f6a-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="13f6a-175">Dla zapytań dotyczących danych pionowo podzielonym na partycje i składnię i przykład, zobacz [zapytań w pionie na partycje danych)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="13f6a-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="13f6a-176">Dla zapytań dotyczących danych poziomie podzielonym na partycje i składnię i przykład, zobacz [zapytań w poziomie na partycje danych)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="13f6a-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="13f6a-177">Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="13f6a-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
