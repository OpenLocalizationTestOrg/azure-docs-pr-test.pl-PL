---
title: "aaaData zależnych routingu w usłudze Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Jak toouse hello klasy ShardMapManager w aplikacjach .NET dla danych zależne od routingu, funkcja podzielonej baz danych w bazie danych SQL Azure"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="4697a-103">Routing zależny od danych</span><span class="sxs-lookup"><span data-stu-id="4697a-103">Data dependent routing</span></span>
<span data-ttu-id="4697a-104">**Dane zależne routingu** jest hello możliwości toouse hello danych z zapytania tooroute hello żądania tooan odpowiednie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4697a-104">**Data dependent routing** is hello ability toouse hello data in a query tooroute hello request tooan appropriate database.</span></span> <span data-ttu-id="4697a-105">Podczas pracy z bazy danych podzielonej jest wzorzec podstawowych.</span><span class="sxs-lookup"><span data-stu-id="4697a-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="4697a-106">kontekst żądania Hello mogą być również używane tooroute hello żądania, zwłaszcza, jeśli klucz dzielenia na fragmenty hello nie jest częścią zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="4697a-106">hello request context may also be used tooroute hello request, especially if hello sharding key is not part of hello query.</span></span> <span data-ttu-id="4697a-107">Każdej określonej kwerendy lub transakcji w aplikacji przy użyciu routingu zależnych danych jest ograniczone tooaccessing pojedynczej bazy danych na żądanie.</span><span class="sxs-lookup"><span data-stu-id="4697a-107">Each specific query or transaction in an application using data dependent routing is restricted tooaccessing a single database per request.</span></span> <span data-ttu-id="4697a-108">Witaj narzędzi elastycznej bazy danych SQL Azure, marszruty jest realizowane za pomocą hello  **[klasy ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  w aplikacjach ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="4697a-108">For hello Azure SQL Database Elastic tools, this routing is accomplished with hello **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="4697a-109">Aplikacja Hello nie jest konieczne tootrack różne parametry połączenia lub skojarzone z inną wycinków danych w środowisku podzielonej hello lokalizacji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4697a-109">hello application does not need tootrack various connection strings or DB locations associated with different slices of data in hello sharded environment.</span></span> <span data-ttu-id="4697a-110">Zamiast tego hello [Menedżera Map niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md) otwiera połączeń toohello poprawne baz danych w razie potrzeby na podstawie hello danych mapy niezależnego fragmentu hello i wartość hello hello dzielenia na fragmenty klucza, który jest elementem docelowym hello żądania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="4697a-110">Instead, hello [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections toohello correct databases when needed, based on hello data in hello shard map and hello value of hello sharding key that is hello target of hello application’s request.</span></span> <span data-ttu-id="4697a-111">klucz Hello jest zwykle hello *customer_id*, *tenant_id*, *date_key*, lub niektóre określonym identyfikatorze, który jest parametrem podstawowym hello żądania bazy danych).</span><span class="sxs-lookup"><span data-stu-id="4697a-111">hello key is typically hello *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of hello database request).</span></span> 

<span data-ttu-id="4697a-112">Aby uzyskać więcej informacji, zobacz [skalowanie limit programu SQL Server z routingiem zależnych danych](https://technet.microsoft.com/library/cc966448.aspx).</span><span class="sxs-lookup"><span data-stu-id="4697a-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-hello-client-library"></a><span data-ttu-id="4697a-113">Pobierz powitania klienta biblioteki</span><span class="sxs-lookup"><span data-stu-id="4697a-113">Download hello client library</span></span>
<span data-ttu-id="4697a-114">Klasa hello tooget, hello instalacji [elastycznej bazy danych klienta biblioteki](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span><span class="sxs-lookup"><span data-stu-id="4697a-114">tooget hello class, install hello [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="4697a-115">Przy użyciu ShardMapManager w danych zależnych aplikacji routingu</span><span class="sxs-lookup"><span data-stu-id="4697a-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="4697a-116">Aplikacje powinny wystąpienia hello **ShardMapManager** podczas inicjowania przy użyciu wywołania fabryki hello  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="4697a-116">Applications should instantiate hello **ShardMapManager** during initialization, using hello factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="4697a-117">W tym przykładzie zarówno **ShardMapManager** i określony **ShardMap** zawierający są zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="4697a-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="4697a-118">W tym przykładzie przedstawiono hello GetSqlShardMapManager i [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="4697a-118">This example shows hello GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a><span data-ttu-id="4697a-119">Użyj najniższy poświadczeń uprawnień możliwe uzyskania hello niezależnego fragmentu mapy</span><span class="sxs-lookup"><span data-stu-id="4697a-119">Use lowest privilege credentials possible for getting hello shard map</span></span>
<span data-ttu-id="4697a-120">Jeśli aplikacja nie jest manipulowanie hello niezależnego fragmentu mapy, używany w metodzie fabryki hello poświadczenia hello powinni mieć uprawnienia tylko do odczytu na powitania **globalne mapy niezależnego fragmentu** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4697a-120">If an application is not manipulating hello shard map itself, hello credentials used in hello factory method should have just read-only permissions on hello **Global Shard Map** database.</span></span> <span data-ttu-id="4697a-121">Te poświadczenia zwykle różnią się od menedżera map niezależnego fragmentu toohello poświadczenia używane tooopen połączenia.</span><span class="sxs-lookup"><span data-stu-id="4697a-121">These credentials are typically different from credentials used tooopen connections toohello shard map manager.</span></span> <span data-ttu-id="4697a-122">Zobacz też [poświadczenia używane biblioteki klienta elastycznej bazy danych hello tooaccess](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="4697a-122">See also [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-hello-openconnectionforkey-method"></a><span data-ttu-id="4697a-123">Wywołaj metodę OpenConnectionForKey hello</span><span class="sxs-lookup"><span data-stu-id="4697a-123">Call hello OpenConnectionForKey method</span></span>
<span data-ttu-id="4697a-124">Witaj  **[metody ShardMap.OpenConnectionForKey](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  zwraca połączenia ADO.Net gotowe do wydania poleceń toohello odpowiednie bazy danych na podstawie wartości hello hello **klucza**parametru.</span><span class="sxs-lookup"><span data-stu-id="4697a-124">hello **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands toohello appropriate database based on hello value of hello **key** parameter.</span></span> <span data-ttu-id="4697a-125">Identyfikator niezależnego fragmentu informacje są buforowane w aplikacji hello przez hello **ShardMapManager**, więc te żądania nie obejmują zazwyczaj wyszukiwania w bazie danych przed hello **globalne mapy niezależnego fragmentu** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4697a-125">Shard information is cached in hello application by hello **ShardMapManager**, so these requests do not typically involve a database lookup against hello **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="4697a-126">Witaj **klucza** parametr jest używany jako klucz wyszukiwania do hello niezależnego fragmentu mapy toodetermine hello odpowiednie bazy danych dla żądania hello.</span><span class="sxs-lookup"><span data-stu-id="4697a-126">hello **key** parameter is used as a lookup key into hello shard map toodetermine hello appropriate database for hello request.</span></span> 
* <span data-ttu-id="4697a-127">Witaj **connectionString** jest toopass używanych tylko poświadczenia użytkownika hello hello żądanego połączenia.</span><span class="sxs-lookup"><span data-stu-id="4697a-127">hello **connectionString** is used toopass only hello user credentials for hello desired connection.</span></span> <span data-ttu-id="4697a-128">Nie nazwy bazy danych lub nazwa serwera znajdują się w tym *connectionString* ponieważ metoda hello określi hello bazy danych i serwera przy użyciu hello **ShardMap**.</span><span class="sxs-lookup"><span data-stu-id="4697a-128">No database name or server name are included in this *connectionString* since hello method will determine hello database and server using hello **ShardMap**.</span></span> 
* <span data-ttu-id="4697a-129">Witaj  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  powinna być ustawiona zbyt**ConnectionOptions.Validate** mogą ulec zmianie w środowisku, gdzie mapuje niezależnego fragmentu czy wierszy może przenoszenia baz danych tooother jako wynik operacji dzielenie i scalanie.</span><span class="sxs-lookup"><span data-stu-id="4697a-129">hello **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set too**ConnectionOptions.Validate** if an environment where shard maps may change and rows may move tooother databases as a result of split or merge operations.</span></span> <span data-ttu-id="4697a-130">Obejmuje to mapa lokalnych niezależnego fragmentu toohello zapytania krótkie hello docelowej bazy danych (nie toohello globalne niezależnych map) przed połączenia hello jest dostarczany toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4697a-130">This involves a brief query toohello local shard map on hello target database (not toohello global shard map) before hello connection is delivered toohello application.</span></span> 

<span data-ttu-id="4697a-131">W przypadku niepowodzenia weryfikacji hello względem mapy niezależnych lokalne powitania (co oznacza, że pamięć podręczna hello jest niepoprawny) hello Menedżera Map niezależnego fragmentu będzie hello globalne niezależnych mapy tooobtain hello nowe poprawne wartość zapytania do wyszukiwania hello aktualizacji pamięci podręcznej hello i uzyskać i zwracają hello połączenie z odpowiednią bazą danych.</span><span class="sxs-lookup"><span data-stu-id="4697a-131">If hello validation against hello local shard map fails (indicating that hello cache is incorrect), hello Shard Map Manager will query hello global shard map tooobtain hello new correct value for hello lookup, update hello cache, and obtain and return hello appropriate database connection.</span></span> 

<span data-ttu-id="4697a-132">Użyj **ConnectionOptions.None** tylko podczas zmiany mapowania niezależnego fragmentu nie powinny podczas, gdy aplikacja jest w trybie online.</span><span class="sxs-lookup"><span data-stu-id="4697a-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="4697a-133">W takim przypadku hello buforowane wartości można założyć tooalways są poprawne i bezpiecznie pominięte hello bardzo obustronne weryfikacji wywołania toohello docelowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4697a-133">In that case, hello cached values can be assumed tooalways be correct, and hello extra round-trip validation call toohello target database can be safely skipped.</span></span> <span data-ttu-id="4697a-134">Która zmniejsza ruch bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4697a-134">That reduces database traffic.</span></span> <span data-ttu-id="4697a-135">Witaj **connectionOptions** również mogą zostać ustawione za pomocą wartości w tooindicate pliku konfiguracji, czy zmiany dzielenia na fragmenty są oczekiwane lub nie w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="4697a-135">hello **connectionOptions** may also be set via a value in a configuration file tooindicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="4697a-136">W tym przykładzie użyto hello wartość klucza **CustomerID**za pomocą **ShardMap** obiektu o nazwie **customerShardMap**.</span><span class="sxs-lookup"><span data-stu-id="4697a-136">This example uses hello value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

<span data-ttu-id="4697a-137">Witaj **OpenConnectionForKey** metoda zwraca nową już otwarte połączenia toohello poprawną bazę danych.</span><span class="sxs-lookup"><span data-stu-id="4697a-137">hello **OpenConnectionForKey** method returns a new already-open connection toohello correct database.</span></span> <span data-ttu-id="4697a-138">Połączenia używane w ten sposób nadal w pełni korzystać z buforowania połączenia ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="4697a-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="4697a-139">Ile transakcji i żądań można spełnić przez jednego niezależnego fragmentu w czasie, powinno to być hello modyfikacji tylko niezbędne w aplikacji już za pomocą ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="4697a-139">As long as transactions and requests can be satisfied by one shard at a time, this should be hello only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="4697a-140">Witaj  **[metody OpenConnectionForKeyAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  jest również dostępna w przypadku aplikacji sprawia, że użycie programowanie asynchroniczne z ADO.Net.</span><span class="sxs-lookup"><span data-stu-id="4697a-140">hello **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="4697a-141">Jego zachowanie jest hello danych zależnych routingu odpowiednik ADO. W sieci  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  metody.</span><span class="sxs-lookup"><span data-stu-id="4697a-141">Its behavior is hello data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="4697a-142">Integrowanie z obsługi błędu przejściowego</span><span class="sxs-lookup"><span data-stu-id="4697a-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="4697a-143">Najlepszym rozwiązaniem w tworzeniu aplikacji dostęp do danych w chmurze hello jest tooensure błędów przejściowych są objęte aplikacji hello oraz operacje hello są zwalniane kilka razy przed generowaniem błędu.</span><span class="sxs-lookup"><span data-stu-id="4697a-143">A best practice in developing data access applications in hello cloud is tooensure that transient faults are caught by hello app, and that hello operations are retried several times before throwing an error.</span></span> <span data-ttu-id="4697a-144">Wystąpienia błędu przejściowego obsługi dla aplikacji w chmurze została szczegółowo opisana w [obsługi błędów przejściowych](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span><span class="sxs-lookup"><span data-stu-id="4697a-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="4697a-145">Obsługa błędu przejściowego mogą współistnieć naturalnie wzorem hello danych zależnych routingu.</span><span class="sxs-lookup"><span data-stu-id="4697a-145">Transient fault handling can coexist naturally with hello Data Dependent Routing pattern.</span></span> <span data-ttu-id="4697a-146">Hello decydujące znaczenie jest tooretry hello danych żądanie dostępu tym hello **przy użyciu** bloku uzyskiwanej hello zależne od danych routingu połączenia.</span><span class="sxs-lookup"><span data-stu-id="4697a-146">hello key requirement is tooretry hello entire data access request including hello **using** block that obtained hello data-dependent routing connection.</span></span> <span data-ttu-id="4697a-147">w powyższym przykładzie Hello można ulegną w następujący sposób (Uwaga: zmiana wyróżnione).</span><span class="sxs-lookup"><span data-stu-id="4697a-147">hello example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="4697a-148">Przykład — danych zależnych routingu z obsługą błędu przejściowego</span><span class="sxs-lookup"><span data-stu-id="4697a-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


<span data-ttu-id="4697a-149">Pakiety obsługi błędu przejściowego tooimplement niezbędne są pobierane automatycznie podczas budowania hello elastycznej bazy danych przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4697a-149">Packages necessary tooimplement transient fault handling are downloaded automatically when you build hello elastic database sample application.</span></span> <span data-ttu-id="4697a-150">Pakiety są także dostępne oddzielnie w [Enterprise Library – bloku aplikacji obsługi błędów przejściowych](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span><span class="sxs-lookup"><span data-stu-id="4697a-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="4697a-151">Użyj wersji 6.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4697a-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="4697a-152">Spójności transakcyjnej</span><span class="sxs-lookup"><span data-stu-id="4697a-152">Transactional consistency</span></span>
<span data-ttu-id="4697a-153">Wszystkie operacje lokalnego tooa niezależnych gwarancję właściwości transakcyjnych.</span><span class="sxs-lookup"><span data-stu-id="4697a-153">Transactional properties are guaranteed for all operations local tooa shard.</span></span> <span data-ttu-id="4697a-154">Na przykład transakcji przesłane za pośrednictwem routingu zależne od danych wykonywania w zakresie hello hello docelowy identyfikator niezależnego fragmentu hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="4697a-154">For example, transactions submitted through data-dependent routing execute within hello scope of hello target shard for hello connection.</span></span> <span data-ttu-id="4697a-155">W tej chwili jest nie możliwości przewidzianych rejestrowanie wiele połączeń w transakcji, a w związku z tym nie bez gwarancji transakcyjne dla operacji wykonywanych przez odłamków.</span><span class="sxs-lookup"><span data-stu-id="4697a-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4697a-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4697a-156">Next steps</span></span>
<span data-ttu-id="4697a-157">Zobacz toodetach niezależnych lub tooreattach niezależnych [przy użyciu hello RecoveryManager klasy toofix niezależnego fragmentu mapy problemów](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="4697a-157">toodetach a shard, or tooreattach a shard, see [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

