---
title: "aaaReport dla baz danych chmury skalowalnych w poziomie (poziomy podziału) | Dokumentacja firmy Microsoft"
description: "jak toouse cross zapytań bazy danych dla bazy danych"
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
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a><span data-ttu-id="c3c2f-103">Raport w chmurze skalowalnych w poziomie bazy danych (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="c3c2f-103">Report across scaled-out cloud databases (preview)</span></span>
<span data-ttu-id="c3c2f-104">Możesz utworzyć raporty z wielu baz danych Azure SQL z punktu pojedynczego połączenia przy użyciu [elastycznej zapytania](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3c2f-104">You can create reports from multiple Azure SQL databases from a single connection point using an [elastic query](sql-database-elastic-query-overview.md).</span></span> <span data-ttu-id="c3c2f-105">Hello bazy danych musi być podzielony w poziomie, (określane również jako "podzielonej").</span><span class="sxs-lookup"><span data-stu-id="c3c2f-105">hello databases must be horizontally partitioned (also known as "sharded").</span></span>

<span data-ttu-id="c3c2f-106">Jeśli masz istniejącą bazę danych, zobacz [Migrowanie istniejącej bazy danych bazy danych poza tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).</span><span class="sxs-lookup"><span data-stu-id="c3c2f-106">If you have an existing database, see [Migrating existing databases tooscaled-out databases](sql-database-elastic-convert-to-use-elastic-tools.md).</span></span>

<span data-ttu-id="c3c2f-107">obiekty SQL hello toounderstand potrzebne tooquery, zobacz [zapytanie na poziomie partycjonowanej baz danych](sql-database-elastic-query-horizontal-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="c3c2f-107">toounderstand hello SQL objects needed tooquery, see [Query across horizontally partitioned databases](sql-database-elastic-query-horizontal-partitioning.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3c2f-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c3c2f-108">Prerequisites</span></span>
<span data-ttu-id="c3c2f-109">Pobierz i uruchom hello [wprowadzenie próbki narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3c2f-109">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="c3c2f-110">Tworzenie mapy niezależnego fragmentu manager za pomocą hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="c3c2f-110">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="c3c2f-111">W tym miejscu spowoduje utworzenie mapy niezależnego fragmentu manager oraz kilka fragmentów, następuje wstawiania danych do odłamków hello.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-111">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="c3c2f-112">W przypadku tooalready skonfigurowano fragmentów danych podzielonej w nich, można pominąć hello następujące kroki i przenieść toohello następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-112">If you happen tooalready have shards setup with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="c3c2f-113">Tworzenie i uruchamianie hello **wprowadzenie do korzystania z narzędzi elastycznej bazy danych** przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-113">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="c3c2f-114">Wykonaj kroki hello aż do kroku 7 w sekcji hello [pobieranie i uruchamianie aplikacji przykładowej hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="c3c2f-114">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="c3c2f-115">Na końcu hello kroku 7 zostanie wyświetlony hello następującego wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="c3c2f-115">At hello end of Step 7, you will see hello following command prompt:</span></span>

    ![Wiersz polecenia][1]
2. <span data-ttu-id="c3c2f-117">W oknie polecenia hello, wpisz "1", a następnie naciśnij klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-117">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="c3c2f-118">Tworzy menedżera map niezależnego fragmentu hello i dodaje dwa niezależne toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-118">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="c3c2f-119">Następnie wpisz "3" i naciśnij klawisz **Enter**; powtórzenie akcji hello cztery razy.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-119">Then type "3" and press **Enter**; repeat hello action four times.</span></span> <span data-ttu-id="c3c2f-120">Wstawia Przykładowe wiersze danych z fragmentów.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-120">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="c3c2f-121">Witaj [portalu Azure](https://portal.azure.com) powinny być widoczne trzech nowych baz danych na serwerze:</span><span class="sxs-lookup"><span data-stu-id="c3c2f-121">hello [Azure portal](https://portal.azure.com) should show three new databases in your server:</span></span>

   ![Visual Studio potwierdzenia][2]

   <span data-ttu-id="c3c2f-123">W tym momencie między bazami danych zapytania są obsługiwane za pomocą biblioteki klienta elastycznej bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-123">At this point, cross-database queries are supported through hello Elastic Database client libraries.</span></span> <span data-ttu-id="c3c2f-124">Na przykład opcja 4 w oknie polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-124">For example, use option 4 in hello command window.</span></span> <span data-ttu-id="c3c2f-125">wyniki zapytania wielu niezależnych Hello są zawsze **UNION ALL** hello wyniki wszystkich fragmentów.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-125">hello results from a multi-shard query are always a **UNION ALL** of hello results from all shards.</span></span>

   <span data-ttu-id="c3c2f-126">W następnej sekcji hello możemy utworzyć obsługującego bardziej zaawansowane funkcje zapytań hello danych między odłamków punkt końcowy bazy danych przykładowych.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-126">In hello next section, we create a sample database endpoint that supports richer querying of hello data across shards.</span></span>

## <a name="create-an-elastic-query-database"></a><span data-ttu-id="c3c2f-127">Tworzenie elastycznej kwerendy bazy danych</span><span class="sxs-lookup"><span data-stu-id="c3c2f-127">Create an elastic query database</span></span>
1. <span data-ttu-id="c3c2f-128">Otwórz hello [portalu Azure](https://portal.azure.com) i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-128">Open hello [Azure portal](https://portal.azure.com) and log in.</span></span>
2. <span data-ttu-id="c3c2f-129">Utwórz nową bazę danych Azure SQL w hello tym samym serwerze co konfigurację niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-129">Create a new Azure SQL database in hello same server as your shard setup.</span></span> <span data-ttu-id="c3c2f-130">Nazwa bazy danych hello "ElasticDBQuery."</span><span class="sxs-lookup"><span data-stu-id="c3c2f-130">Name hello database "ElasticDBQuery."</span></span>

    ![Portalu Azure i warstwę cenową][3]

    > [!NOTE]
    > <span data-ttu-id="c3c2f-132">można użyć istniejącej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-132">you can use an existing database.</span></span> <span data-ttu-id="c3c2f-133">Jeśli możesz to zrobić, nie może być jeden z fragmentów hello chcieliby tooexecute zapytań na.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-133">If you can do so, it must not be one of hello shards that you would like tooexecute your queries on.</span></span> <span data-ttu-id="c3c2f-134">Ta baza danych będzie służyć do tworzenia hello obiektów metadanych dla zapytania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-134">This database will be used for creating hello metadata objects for an elastic database query.</span></span>
    >

## <a name="create-database-objects"></a><span data-ttu-id="c3c2f-135">Tworzenie obiektów bazy danych</span><span class="sxs-lookup"><span data-stu-id="c3c2f-135">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="c3c2f-136">Klucz główny o zakresie bazy danych i poświadczeń</span><span class="sxs-lookup"><span data-stu-id="c3c2f-136">Database-scoped master key and credentials</span></span>
<span data-ttu-id="c3c2f-137">Są używane tooconnect toohello niezależnego fragmentu mapy manager i odłamków hello:</span><span class="sxs-lookup"><span data-stu-id="c3c2f-137">These are used tooconnect toohello shard map manager and hello shards:</span></span>

1. <span data-ttu-id="c3c2f-138">Otwórz program SQL Server Management Studio lub SQL Server Data Tools w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-138">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="c3c2f-139">Połącz tooElasticDBQuery bazy danych i wykonaj następujące polecenia T-SQL hello:</span><span class="sxs-lookup"><span data-stu-id="c3c2f-139">Connect tooElasticDBQuery database and execute hello following T-SQL commands:</span></span>

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    <span data-ttu-id="c3c2f-140">"username" i "password" powinien być hello sam jako informacje logowania używane w kroku 6 [pobieranie i uruchamianie aplikacji przykładowej hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) w [wprowadzenie do korzystania z narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3c2f-140">"username" and "password" should be hello same as login information used in step 6 of [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Getting started with elastic database tools](sql-database-elastic-scale-get-started.md).</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="c3c2f-141">Zewnętrzne źródła danych</span><span class="sxs-lookup"><span data-stu-id="c3c2f-141">External data sources</span></span>
<span data-ttu-id="c3c2f-142">toocreate zewnętrznego źródła danych, wykonaj następujące polecenia w bazie danych ElasticDBQuery hello hello:</span><span class="sxs-lookup"><span data-stu-id="c3c2f-142">toocreate an external data source, execute hello following command on hello ElasticDBQuery database:</span></span>

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 <span data-ttu-id="c3c2f-143">"CustomerIDShardMap" jest nazwa hello hello niezależnego fragmentu mapy, jeśli utworzono hello niezależnego fragmentu mapy, a następnie mapować niezależnego fragmentu Menedżera przy użyciu hello — przykład narzędzi elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-143">"CustomerIDShardMap" is hello name of hello shard map, if you created hello shard map and shard map manager using hello elastic database tools sample.</span></span> <span data-ttu-id="c3c2f-144">Jednak jeśli używasz niestandardowych ustawień dla tego przykładu, następnie należy hello niezależnego fragmentu mapy wybrana nazwa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-144">However, if you used your custom setup for this sample, then it should be hello shard map name you chose in your application.</span></span>

### <a name="external-tables"></a><span data-ttu-id="c3c2f-145">Tabele zewnętrzne</span><span class="sxs-lookup"><span data-stu-id="c3c2f-145">External tables</span></span>
<span data-ttu-id="c3c2f-146">Tworzenie tabeli zewnętrznej zgodny hello tabeli klientów na powitania odłamków, wykonując następujące polecenia w bazie danych ElasticDBQuery hello:</span><span class="sxs-lookup"><span data-stu-id="c3c2f-146">Create an external table that matches hello Customers table on hello shards by executing hello following command on ElasticDBQuery database:</span></span>

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="c3c2f-147">Wykonywanie przykładowego zapytania T-SQL elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="c3c2f-147">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="c3c2f-148">Po zdefiniowaniu zewnętrznym źródle danych i tabele zewnętrzne mogą teraz używać pełnej T-SQL w tabelach zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-148">Once you have defined your external data source and your external tables you can now use full T-SQL over your external tables.</span></span>

<span data-ttu-id="c3c2f-149">Wykonaj tę kwerendę w bazie danych ElasticDBQuery hello:</span><span class="sxs-lookup"><span data-stu-id="c3c2f-149">Execute this query on hello ElasticDBQuery database:</span></span>

    select count(CustomerId) from [dbo].[Customers]

<span data-ttu-id="c3c2f-150">Można zauważyć zapytania hello agreguje wyniki wszystkich odłamków hello i zapewnia hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c3c2f-150">You will notice that hello query aggregates results from all hello shards and gives hello following output:</span></span>

![Szczegóły danych wyjściowych][4]

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="c3c2f-152">Importuj tooExcel wyników zapytania elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="c3c2f-152">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="c3c2f-153">Możesz zaimportować hello wyników z pliku programu Excel tooan zapytania.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-153">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="c3c2f-154">Uruchom program Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-154">Launch Excel 2013.</span></span>
2. <span data-ttu-id="c3c2f-155">Przejdź toohello **danych** wstążki.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-155">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="c3c2f-156">Kliknij przycisk **z innych źródeł** i kliknij przycisk **z programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-156">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importowania z programu Excel z innych źródeł][5]
4. <span data-ttu-id="c3c2f-158">W hello **Kreator połączenia danych** wpisz powitania serwera nazwę i poświadczenia logowania.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-158">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="c3c2f-159">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="c3c2f-159">Then click **Next**.</span></span>
5. <span data-ttu-id="c3c2f-160">W oknie dialogowym hello **hello wybierz bazy danych, która zawiera dane hello**, wybierz pozycję hello **ElasticDBQuery** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-160">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="c3c2f-161">Wybierz hello **klientów** tabeli w widoku listy hello, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-161">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="c3c2f-162">Następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-162">Then click **Finish**.</span></span>
7. <span data-ttu-id="c3c2f-163">W hello **i zaimportuj dane** formularza, w obszarze **wybierz sposób tooview tych danych w skoroszycie**, wybierz pozycję **tabeli** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-163">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="c3c2f-164">Witaj wszystkie wiersze z **klientów** tabeli, przechowywane w różnych odłamków wypełnić hello arkuszu programu Excel.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-164">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

<span data-ttu-id="c3c2f-165">Możesz teraz użyć funkcji wizualizacji zaawansowanych danych programu Excel.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-165">You can now use Excel’s powerful data visualization functions.</span></span> <span data-ttu-id="c3c2f-166">Można użyć ciągu połączenia hello nazwę serwera, nazwa bazy danych i poświadczeń tooconnect BI i dane integracji narzędzia toohello zapytania elastycznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-166">You can use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="c3c2f-167">Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-167">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="c3c2f-168">Może się odwoływać toohello elastycznej zapytanie do bazy danych i tabel zewnętrznych, podobnie jak wszystkie inne bazy danych programu SQL Server i czy można połączyć toowith własnych narzędzi tabel programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-168">You can refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="c3c2f-169">Koszty</span><span class="sxs-lookup"><span data-stu-id="c3c2f-169">Cost</span></span>
<span data-ttu-id="c3c2f-170">Brak bez dodatkowych opłat dla funkcji hello elastycznej kwerendy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-170">There is no additional charge for using hello Elastic Database Query feature.</span></span>

<span data-ttu-id="c3c2f-171">Aby uzyskać informacje o cenach zobacz [szczegóły cennika bazy danych SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="c3c2f-171">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3c2f-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3c2f-172">Next steps</span></span>

* <span data-ttu-id="c3c2f-173">Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3c2f-173">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="c3c2f-174">Samouczek partycjonowania pionowego, zobacz [wprowadzenie do korzystania z bazy danych między kwerendy (partycjonowanie pionowe)](sql-database-elastic-query-getting-started-vertical.md).</span><span class="sxs-lookup"><span data-stu-id="c3c2f-174">For a vertical partitioning tutorial, see [Getting started with cross-database query (vertical partitioning)](sql-database-elastic-query-getting-started-vertical.md).</span></span>
* <span data-ttu-id="c3c2f-175">Dla zapytań dotyczących danych pionowo podzielonym na partycje i składnię i przykład, zobacz [zapytań w pionie na partycje danych)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c3c2f-175">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="c3c2f-176">Dla zapytań dotyczących danych poziomie podzielonym na partycje i składnię i przykład, zobacz [zapytań w poziomie na partycje danych)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="c3c2f-176">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="c3c2f-177">Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.</span><span class="sxs-lookup"><span data-stu-id="c3c2f-177">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
