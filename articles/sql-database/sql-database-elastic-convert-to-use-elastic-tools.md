---
title: "aaaMigrate istniejących baz danych poza tooscale | Dokumentacja firmy Microsoft"
description: "Konwertuj narzędzi elastycznej bazy danych toouse bazy danych podzielonej przez utworzenie menedżera map niezależnego fragmentu"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a><span data-ttu-id="8417a-103">Migrowanie istniejących baz danych tooscale w poziomie</span><span class="sxs-lookup"><span data-stu-id="8417a-103">Migrate existing databases tooscale-out</span></span>
<span data-ttu-id="8417a-104">Łatwe zarządzanie istniejących skalowalnych w poziomie podzielonej baz danych za pomocą narzędzi bazy danych usługi Azure SQL Database (takich jak hello [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md)).</span><span class="sxs-lookup"><span data-stu-id="8417a-104">Easily manage your existing scaled-out sharded databases using Azure SQL Database database tools (such as hello [Elastic Database client library](sql-database-elastic-database-client-library.md)).</span></span> <span data-ttu-id="8417a-105">Najpierw należy przekonwertować istniejącego zestawu baz danych toouse hello [menedżera map niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="8417a-105">You must first convert an existing set of databases toouse hello [shard map manager](sql-database-elastic-scale-shard-map-management.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="8417a-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8417a-106">Overview</span></span>
<span data-ttu-id="8417a-107">toomigrate istniejącej bazy danych podzielonej:</span><span class="sxs-lookup"><span data-stu-id="8417a-107">toomigrate an existing sharded database:</span></span> 

1. <span data-ttu-id="8417a-108">Przygotowanie hello [bazy danych Menedżera mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="8417a-108">Prepare hello [shard map manager database](sql-database-elastic-scale-shard-map-management.md).</span></span>
2. <span data-ttu-id="8417a-109">Utwórz hello niezależnego fragmentu mapy.</span><span class="sxs-lookup"><span data-stu-id="8417a-109">Create hello shard map.</span></span>
3. <span data-ttu-id="8417a-110">Przygotuj hello poszczególnych fragmentów.</span><span class="sxs-lookup"><span data-stu-id="8417a-110">Prepare hello individual shards.</span></span>  
4. <span data-ttu-id="8417a-111">Dodaj mapę niezależnego fragmentu toohello mapowania.</span><span class="sxs-lookup"><span data-stu-id="8417a-111">Add mappings toohello shard map.</span></span>

<span data-ttu-id="8417a-112">Te techniki można implementować przy użyciu albo hello [biblioteki klienta .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), lub skryptów programu PowerShell hello znaleźć pod adresem [Azuresql DB - skrypty narzędzi elastycznej bazy danych](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="8417a-112">These techniques can be implemented using either hello [.NET Framework client library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), or hello PowerShell scripts found at [Azure SQL DB - Elastic Database tools scripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span> <span data-ttu-id="8417a-113">Przykłady Hello tutaj za pomocą skryptów środowiska PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="8417a-113">hello examples here use hello PowerShell scripts.</span></span>

<span data-ttu-id="8417a-114">Aby uzyskać więcej informacji na temat hello ShardMapManager, zobacz [zarządzania mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md).</span><span class="sxs-lookup"><span data-stu-id="8417a-114">For more information about hello ShardMapManager, see [Shard map management](sql-database-elastic-scale-shard-map-management.md).</span></span> <span data-ttu-id="8417a-115">Omówienie hello narzędzi elastycznej bazy danych, zobacz [Przegląd funkcji elastycznej bazy danych](sql-database-elastic-scale-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8417a-115">For an overview of hello elastic database tools, see [Elastic Database features overview](sql-database-elastic-scale-introduction.md).</span></span>

## <a name="prepare-hello-shard-map-manager-database"></a><span data-ttu-id="8417a-116">Przygotowanie hello niezależnego fragmentu mapy manager w bazie danych</span><span class="sxs-lookup"><span data-stu-id="8417a-116">Prepare hello shard map manager database</span></span>
<span data-ttu-id="8417a-117">Menedżera map niezależnego fragmentu Hello jest specjalne bazy danych, która zawiera hello danych toomanage skalowalnych w poziomie w bazach danych.</span><span class="sxs-lookup"><span data-stu-id="8417a-117">hello shard map manager is a special database that contains hello data toomanage scaled-out databases.</span></span> <span data-ttu-id="8417a-118">Użyj istniejącej bazy danych lub Utwórz nową bazę danych.</span><span class="sxs-lookup"><span data-stu-id="8417a-118">You can use an existing database, or create a new database.</span></span> <span data-ttu-id="8417a-119">Należy pamiętać, że baza danych działa jako menedżera map niezależnego fragmentu nie powinien być hello sam bazy danych jako niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="8417a-119">Note that a database acting as shard map manager should not be hello same database as a shard.</span></span> <span data-ttu-id="8417a-120">Należy również zauważyć, że skrypt programu PowerShell hello nie tworzy hello bazy danych dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="8417a-120">Also note that hello PowerShell script does not create hello database for you.</span></span> 

## <a name="step-1-create-a-shard-map-manager"></a><span data-ttu-id="8417a-121">Krok 1: tworzenie niezależnych menedżera map</span><span class="sxs-lookup"><span data-stu-id="8417a-121">Step 1: create a shard map manager</span></span>
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a><span data-ttu-id="8417a-122">tooretrieve hello niezależnego fragmentu mapy manager</span><span class="sxs-lookup"><span data-stu-id="8417a-122">tooretrieve hello shard map manager</span></span>
<span data-ttu-id="8417a-123">Po utworzeniu można pobrać hello niezależnego fragmentu mapy manager z tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8417a-123">After creation, you can retrieve hello shard map manager with this cmdlet.</span></span> <span data-ttu-id="8417a-124">Ten krok jest niezbędny, za każdym razem, gdy należy toouse hello ShardMapManager obiektu.</span><span class="sxs-lookup"><span data-stu-id="8417a-124">This step is needed every time you need toouse hello ShardMapManager object.</span></span>

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a><span data-ttu-id="8417a-125">Krok 2: Tworzenie mapy niezależnego fragmentu hello</span><span class="sxs-lookup"><span data-stu-id="8417a-125">Step 2: create hello shard map</span></span>
<span data-ttu-id="8417a-126">Należy wybrać typ hello toocreate mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="8417a-126">You must select hello type of shard map toocreate.</span></span> <span data-ttu-id="8417a-127">Wybór Hello zależy od hello Architektura bazy danych:</span><span class="sxs-lookup"><span data-stu-id="8417a-127">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="8417a-128">Pojedynczej dzierżawy na bazę danych (terminów, zobacz hello [słownik](sql-database-elastic-scale-glossary.md).)</span><span class="sxs-lookup"><span data-stu-id="8417a-128">Single tenant per database (For terms, see hello [glossary](sql-database-elastic-scale-glossary.md).)</span></span> 
2. <span data-ttu-id="8417a-129">Wiele dzierżaw dla jednej bazy danych (dwa typy):</span><span class="sxs-lookup"><span data-stu-id="8417a-129">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="8417a-130">Mapowanie list</span><span class="sxs-lookup"><span data-stu-id="8417a-130">List mapping</span></span>
   2. <span data-ttu-id="8417a-131">Mapowanie zakresu</span><span class="sxs-lookup"><span data-stu-id="8417a-131">Range mapping</span></span>

<span data-ttu-id="8417a-132">Model pojedynczego dzierżawcy można utworzyć **mapowania listy** mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="8417a-132">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="8417a-133">model pojedynczej dzierżawy Hello przypisuje jednej bazy danych dla każdego dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="8417a-133">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="8417a-134">Jest to efektywne modelu dla deweloperów SaaS, ponieważ takie rozwiązanie upraszcza zarządzanie.</span><span class="sxs-lookup"><span data-stu-id="8417a-134">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mapowanie list][1]

<span data-ttu-id="8417a-136">modelu wielodostępnym Hello przypisuje kilka dzierżaw tooa pojedynczej bazy danych (i grup dzierżawcy mogą rozpowszechniają wielu baz danych).</span><span class="sxs-lookup"><span data-stu-id="8417a-136">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="8417a-137">Użyj tego modelu, gdy oczekuje się, że każdy dzierżawca toohave niewielkie zbiory danych musi.</span><span class="sxs-lookup"><span data-stu-id="8417a-137">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="8417a-138">W tym modelu możemy Przypisz zakres przy użyciu bazy danych tooa dzierżawców **mapowanie zakresu**.</span><span class="sxs-lookup"><span data-stu-id="8417a-138">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Mapowanie zakresu][2]

<span data-ttu-id="8417a-140">Lub możesz wdrożyć model bazy danych wielu dzierżawców przy użyciu *mapowania listy* tooassign wiele dzierżaw tooa pojedynczej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8417a-140">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="8417a-141">Na przykład DB1 jest używane toostore informacji na temat identyfikatora dzierżawy 1 do 5 i bazy danych DB2 przechowuje dane dla dzierżawy 7 i dzierżawcy 10.</span><span class="sxs-lookup"><span data-stu-id="8417a-141">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Wielu dzierżawców dla jednej bazy danych][3] 

<span data-ttu-id="8417a-143">**W oparciu o wybór, wybierz jedną z następujących opcji:**</span><span class="sxs-lookup"><span data-stu-id="8417a-143">**Based on your choice, choose one of these options:**</span></span>

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a><span data-ttu-id="8417a-144">Opcja 1: Tworzenie mapy niezależnego fragmentu mapowania listy</span><span class="sxs-lookup"><span data-stu-id="8417a-144">Option 1: create a shard map for a list mapping</span></span>
<span data-ttu-id="8417a-145">Tworzenie przy użyciu obiektu ShardMapManager hello mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="8417a-145">Create a shard map using hello ShardMapManager object.</span></span> 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a><span data-ttu-id="8417a-146">Opcja 2: Tworzenie mapy niezależnego fragmentu mapowania zakresu</span><span class="sxs-lookup"><span data-stu-id="8417a-146">Option 2: create a shard map for a range mapping</span></span>
<span data-ttu-id="8417a-147">Należy pamiętać, że tooutilize tego wzorca mapowania, zakresy ciągłe toobe wymaga wartości identyfikatora dzierżawy i jest dopuszczalne toohave przerwa w zakresach hello po prostu pomijając hello zakres podczas jej tworzenia hello.</span><span class="sxs-lookup"><span data-stu-id="8417a-147">Note that tooutilize this mapping pattern, tenant id values needs toobe continuous ranges, and it is acceptable toohave gap in hello ranges by simply skipping hello range when creating hello databases.</span></span>

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a><span data-ttu-id="8417a-148">Opcja 3: Lista mapowania na pojedynczej bazy danych</span><span class="sxs-lookup"><span data-stu-id="8417a-148">Option 3: List mappings on a single database</span></span>
<span data-ttu-id="8417a-149">Konfigurowanie ten wzorzec wymaga również tworzenia mapy listy jak pokazano w kroku 2, opcja 1.</span><span class="sxs-lookup"><span data-stu-id="8417a-149">Setting up this pattern also requires creation of a list map as shown in step 2, option 1.</span></span>

## <a name="step-3-prepare-individual-shards"></a><span data-ttu-id="8417a-150">Krok 3: Przygotowanie poszczególnych odłamków</span><span class="sxs-lookup"><span data-stu-id="8417a-150">Step 3: Prepare individual shards</span></span>
<span data-ttu-id="8417a-151">Dodaj każdy identyfikator niezależnego fragmentu (baza danych) toohello niezależnego fragmentu mapy menedżera.</span><span class="sxs-lookup"><span data-stu-id="8417a-151">Add each shard (database) toohello shard map manager.</span></span> <span data-ttu-id="8417a-152">Do przechowywania informacji o mapowaniu to przygotowuje hello pojedynczych baz danych.</span><span class="sxs-lookup"><span data-stu-id="8417a-152">This prepares hello individual databases for storing mapping information.</span></span> <span data-ttu-id="8417a-153">Tej metody należy wykonać na każdym niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="8417a-153">Execute this method on each shard.</span></span>

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a><span data-ttu-id="8417a-154">Krok 4: Dodawanie mapowania</span><span class="sxs-lookup"><span data-stu-id="8417a-154">Step 4: Add mappings</span></span>
<span data-ttu-id="8417a-155">Dodawanie Hello mapowań zależy od rodzaju hello mapować niezależnego fragmentu utworzoną.</span><span class="sxs-lookup"><span data-stu-id="8417a-155">hello addition of mappings depends on hello kind of shard map you created.</span></span> <span data-ttu-id="8417a-156">Jeśli utworzono mapy listy, możesz dodać mapowania listy.</span><span class="sxs-lookup"><span data-stu-id="8417a-156">If you created a list map, you add list mappings.</span></span> <span data-ttu-id="8417a-157">Jeśli utworzono map zakres, należy dodać mapowania zakresu.</span><span class="sxs-lookup"><span data-stu-id="8417a-157">If you created a range map, you add range mappings.</span></span>

### <a name="option-1-map-hello-data-for-a-list-mapping"></a><span data-ttu-id="8417a-158">Opcja 1: mapowanie danych hello mapowania listy</span><span class="sxs-lookup"><span data-stu-id="8417a-158">Option 1: map hello data for a list mapping</span></span>
<span data-ttu-id="8417a-159">Mapowanie danych hello przez dodanie mapowania listy dla każdego dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="8417a-159">Map hello data by adding a list mapping for each tenant.</span></span>  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a><span data-ttu-id="8417a-160">Opcja 2: mapowanie danych hello mapowania zakresu</span><span class="sxs-lookup"><span data-stu-id="8417a-160">Option 2: map hello data for a range mapping</span></span>
<span data-ttu-id="8417a-161">Dodaj hello zakresu mapowania dla wszystkich hello dzierżawy zakres identyfikatora - skojarzenia bazy danych:</span><span class="sxs-lookup"><span data-stu-id="8417a-161">Add hello range mappings for all hello tenant id range - database associations:</span></span>

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a><span data-ttu-id="8417a-162">Krok 4 — opcja 3: hello dane mapy dla wielu dzierżawców w pojedynczej bazy danych</span><span class="sxs-lookup"><span data-stu-id="8417a-162">Step 4 option 3: map hello data for multiple tenants on a single database</span></span>
<span data-ttu-id="8417a-163">Dla każdego dzierżawcy, uruchom hello Dodaj ListMapping (opcja 1, powyżej).</span><span class="sxs-lookup"><span data-stu-id="8417a-163">For each tenant, run hello Add-ListMapping (option 1, above).</span></span> 

## <a name="checking-hello-mappings"></a><span data-ttu-id="8417a-164">Sprawdzanie, czy hello mapowania</span><span class="sxs-lookup"><span data-stu-id="8417a-164">Checking hello mappings</span></span>
<span data-ttu-id="8417a-165">Informacje o istniejących odłamków hello i mapowania hello skojarzonych z nimi mogą być przeszukiwane przy użyciu następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="8417a-165">Information about hello existing shards and hello mappings associated with them can be queried using following commands:</span></span>  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a><span data-ttu-id="8417a-166">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="8417a-166">Summary</span></span>
<span data-ttu-id="8417a-167">Po zakończeniu instalacji hello można rozpocząć biblioteki klienta elastycznej bazy danych hello toouse.</span><span class="sxs-lookup"><span data-stu-id="8417a-167">Once you have completed hello setup, you can begin toouse hello Elastic Database client library.</span></span> <span data-ttu-id="8417a-168">Można również użyć [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md) i [zapytania wielu niezależnych](sql-database-elastic-scale-multishard-querying.md).</span><span class="sxs-lookup"><span data-stu-id="8417a-168">You can also use [data dependent routing](sql-database-elastic-scale-data-dependent-routing.md) and [multi-shard query](sql-database-elastic-scale-multishard-querying.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8417a-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8417a-169">Next steps</span></span>
<span data-ttu-id="8417a-170">Pobierz skrypty programu PowerShell hello [bazy danych elastyczne bazy danych SQL Azure narzędzi sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="8417a-170">Get hello PowerShell scripts from [Azure SQL DB-Elastic Database tools sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

<span data-ttu-id="8417a-171">narzędzia Hello są również w witrynie GitHub: [Azure/elastyczna db-tools](https://github.com/Azure/elastic-db-tools).</span><span class="sxs-lookup"><span data-stu-id="8417a-171">hello tools are also on GitHub: [Azure/elastic-db-tools](https://github.com/Azure/elastic-db-tools).</span></span>

<span data-ttu-id="8417a-172">Użyj hello narzędzia do scalania podziału toomove danych tooor z modelu pojedynczej dzierżawy tooa modelu wielodostępnym.</span><span class="sxs-lookup"><span data-stu-id="8417a-172">Use hello split-merge tool toomove data tooor from a multi-tenant model tooa single tenant model.</span></span> <span data-ttu-id="8417a-173">Zobacz [narzędzia do scalania podziału](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8417a-173">See [Split merge tool](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8417a-174">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8417a-174">Additional resources</span></span>
<span data-ttu-id="8417a-175">Aby uzyskać informacje na temat typowych wzorców architektury danych w aplikacjach baz danych typu oprogramowanie jako usługa (SaaS), zobacz artykuł [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) (Wzorce projektowe dla wielodostępnych aplikacji SaaS korzystających z usługi Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="8417a-175">For information on common data architecture patterns of multi-tenant software-as-a-service (SaaS) database applications, see [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md).</span></span>

## <a name="questions-and-feature-requests"></a><span data-ttu-id="8417a-176">Pytania i żądania funkcji</span><span class="sxs-lookup"><span data-stu-id="8417a-176">Questions and Feature Requests</span></span>
<span data-ttu-id="8417a-177">Odpowiedzi na pytania, proszę dotrzeć toous na powitania [forum bazy danych SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) i funkcja żądań, dodaj je toohello [forum opinii bazy danych SQL](https://feedback.azure.com/forums/217321-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="8417a-177">For questions, please reach out toous on hello [SQL Database forum](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) and for feature requests, please add them toohello [SQL Database feedback forum](https://feedback.azure.com/forums/217321-sql-database/).</span></span>

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

