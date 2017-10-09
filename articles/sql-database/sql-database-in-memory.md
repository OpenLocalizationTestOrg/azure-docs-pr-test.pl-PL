---
title: "technologie SQL bazy danych w pamięci aaaAzure | Dokumentacja firmy Microsoft"
description: "Technologie usługi Azure SQL bazy danych w pamięci znacząco poprawić wydajność hello transakcyjne i obciążeń analizy. Dowiedz się, jak tootake korzystać z tych technologii."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="f1931-104">Optymalizacja wydajności za pomocą technologii w pamięci w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="f1931-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="f1931-105">Dzięki użyciu technologii w pamięci w bazie danych SQL Azure, można osiągnąć ulepszenia wydajności z różnych obciążeń: transakcyjna (transakcyjnego przetwarzania online (OLTP)), analytics (online analytical processing (OLAP)) i mieszanego (hybrydowe przetwarzanie analityczne/transakcji (HTAP)).</span><span class="sxs-lookup"><span data-stu-id="f1931-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="f1931-106">Z powodu hello większą wydajność zapytań i przetwarzania transakcji, technologie w pamięci też pomóc Ci tooreduce kosztów.</span><span class="sxs-lookup"><span data-stu-id="f1931-106">Because of hello more efficient query and transaction processing, In-Memory technologies also help you tooreduce cost.</span></span> <span data-ttu-id="f1931-107">Zwykle nie trzeba hello tooupgrade cenowym wzrost wydajności tooachieve hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-107">You typically don't need tooupgrade hello pricing tier of hello database tooachieve performance gains.</span></span> <span data-ttu-id="f1931-108">W niektórych przypadkach, nawet można zmniejszyć hello cenowym podczas nadal występuje ulepszenia wydajności z technologiami w pamięci.</span><span class="sxs-lookup"><span data-stu-id="f1931-108">In some cases, you might even be able reduce hello pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="f1931-109">Poniżej przedstawiono dwa przykłady sposobu OLTP w pamięci pomogła toosignificantly poprawić wydajność:</span><span class="sxs-lookup"><span data-stu-id="f1931-109">Here are two examples of how In-Memory OLTP helped toosignificantly improve performance:</span></span>

- <span data-ttu-id="f1931-110">Za pomocą OLTP w pamięci [rozwiązań biznesowych kworum został toodouble stanie ich obciążenie poprawienie Dtu 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="f1931-110">By using In-Memory OLTP, [Quorum Business Solutions was able toodouble their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="f1931-111">Oznacza jednostek dtu w warstwie *jednostki przepływności bazy danych*, a także mesurement zużycia zasobów.</span><span class="sxs-lookup"><span data-stu-id="f1931-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="f1931-112">Witaj poniżej film wideo przedstawia znaczne ulepszenia w zużycie zasobów z przykładowe obciążenie: [OLTP w pamięci wideo bazy danych SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="f1931-112">hello following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="f1931-113">Aby uzyskać więcej informacji, zobacz hello wpisie w blogu: [OLTP w pamięci w blogu blogu bazy danych SQL Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="f1931-113">For more details, see hello blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="f1931-114">Technologie w pamięci są dostępne wszystkie bazy danych w warstwie Premium hello, w tym baz danych w puli elastycznej Premium.</span><span class="sxs-lookup"><span data-stu-id="f1931-114">In-Memory technologies are available in all databases in hello Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="f1931-115">Witaj poniższego klipu wideo wyjaśniono, potencjalne zwiększenie wydajności w przypadku technologii w pamięci w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f1931-115">hello following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="f1931-116">Należy pamiętać, że hello są bardziej wydajne zawsze wyświetlany zależy od wielu czynników, takich jak rodzaj hello hello obciążenia i dane, wzorca dostępu hello bazy danych i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="f1931-116">Remember that hello performance gain that you see always depends on many factors, including hello nature of hello workload and data, access pattern of hello database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="f1931-117">Baza danych SQL Azure ma hello następujące technologie w pamięci:</span><span class="sxs-lookup"><span data-stu-id="f1931-117">Azure SQL Database has hello following In-Memory technologies:</span></span>

- <span data-ttu-id="f1931-118">*OLTP w pamięci* zwiększa przepustowość i zmniejsza opóźnienia przetwarzania transakcji.</span><span class="sxs-lookup"><span data-stu-id="f1931-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="f1931-119">Scenariusze, w których warto skorzystać z OLTP w pamięci są: przetwarzanie takich jak handlowych i gier, wprowadzanie danych z urządzeń IoT, buforowanie ładowania danych i tabeli tymczasowej i scenariusze zmiennej tabeli lub zdarzenia transakcji wysokiej przepustowości.</span><span class="sxs-lookup"><span data-stu-id="f1931-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="f1931-120">*Klastrowane indeksy magazynu kolumn* ograniczyć wpływ sieci magazynowania (w górę too10 razy) i zwiększyć wydajność dla raportowania i zapytań analiz.</span><span class="sxs-lookup"><span data-stu-id="f1931-120">*Clustered columnstore indexes* reduce your storage footprint (up too10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="f1931-121">Można używać go z tabel faktów w Twojej toofit składnice danych większej ilości danych w bazie danych i zwiększyć wydajność.</span><span class="sxs-lookup"><span data-stu-id="f1931-121">You can use it with fact tables in your data marts toofit more data in your database and improve performance.</span></span> <span data-ttu-id="f1931-122">Ponadto można jej używać z danych historycznych w Twojej tooarchive operacyjnej bazy danych i być tooquery stanie się too10 razy więcej danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-122">Also, you can use it with historical data in your operational database tooarchive and be able tooquery up too10 times more data.</span></span>
- <span data-ttu-id="f1931-123">*Klastrowanych indeksów magazynu kolumn* HTAP pomocy można toogain wgląd w czasie rzeczywistym w firmie za pomocą zapytań hello operacyjnej bazy danych bezpośrednio, bez toorun potrzeby hello kosztowne wyodrębniania, transformacji i proces ładowania (ETL) i poczekaj dla hello wypełnione toobe magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-123">*Nonclustered columnstore indexes* for HTAP help you toogain real-time insights into your business through querying hello operational database directly, without hello need toorun an expensive extract, transform, and load (ETL) process and wait for hello data warehouse toobe populated.</span></span> <span data-ttu-id="f1931-124">Klastrowanych indeksów magazynu kolumn Zezwalaj bardzo szybkie wykonywanie zapytania analityczne na powitania bazy danych OLTP, przy jednoczesnym zmniejszeniu hello wpływ na obciążenie operacyjne hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on hello OLTP database, while reducing hello impact on hello operational workload.</span></span>
- <span data-ttu-id="f1931-125">Może także zawierać kombinację hello tabeli zoptymalizowanej pod kątem pamięci z indeksem magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="f1931-125">You can also have hello combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="f1931-126">To połączenie umożliwia tooperform transakcji bardzo szybkie przetwarzanie i zbyt*jednocześnie* wykonywania analizy zapytanie bardzo szybko na powitania takie same dane.</span><span class="sxs-lookup"><span data-stu-id="f1931-126">This combination enables you tooperform very fast transaction processing, and too*concurrently* run analytics queries very quickly on hello same data.</span></span>

<span data-ttu-id="f1931-127">Zarówno indeksy magazynu kolumn i OLTP w pamięci zostały część produktu SQL Server powitania od 2012 i 2014 r. odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="f1931-127">Both columnstore indexes and In-Memory OLTP have been part of hello SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="f1931-128">Azure SQL Database i programu SQL Server hello udostępnianie tego samego implementacją technologii w pamięci.</span><span class="sxs-lookup"><span data-stu-id="f1931-128">Azure SQL Database and SQL Server share hello same implementation of In-Memory technologies.</span></span> <span data-ttu-id="f1931-129">Idąc dalej, nowych funkcji do tych technologii są wydawane w bazie danych SQL Azure, przed wprowadzeniem w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f1931-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="f1931-130">W tym temacie opisano aspekty indeksy OLTP w pamięci i magazynu kolumn, które są określone tooAzure bazy danych SQL i przykłady zawiera również:</span><span class="sxs-lookup"><span data-stu-id="f1931-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific tooAzure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="f1931-131">Zostanie wyświetlony hello wpływ tych technologii limity rozmiaru magazynu i danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-131">You'll see hello impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="f1931-132">Zobaczysz, jak toomanage hello przenoszenia baz danych używających tych technologii między hello różnym warstwom cenowym.</span><span class="sxs-lookup"><span data-stu-id="f1931-132">You'll see how toomanage hello movement of databases that use these technologies between hello different pricing tiers.</span></span>
- <span data-ttu-id="f1931-133">Zostanie wyświetlone dwa — przykłady ilustrujące stosowania hello OLTP w pamięci, a także indeksy magazynu kolumn w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f1931-133">You'll see two samples that illustrate hello use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="f1931-134">Zobacz hello następujące zasoby, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f1931-134">See hello following resources for more information.</span></span>

<span data-ttu-id="f1931-135">Szczegółowe informacje na temat technologii hello:</span><span class="sxs-lookup"><span data-stu-id="f1931-135">In-depth information about hello technologies:</span></span>

- <span data-ttu-id="f1931-136">[Omówienie OLTP w pamięci i scenariusze użycia](https://msdn.microsoft.com/library/mt774593.aspx) (obejmuje odwołania toocustomer wdrożeń i tooget informacji uruchomiona)</span><span class="sxs-lookup"><span data-stu-id="f1931-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references toocustomer case studies and information tooget started)</span></span>
- [<span data-ttu-id="f1931-137">Dokumentacja OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="f1931-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="f1931-138">Przewodnik indeksy magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="f1931-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="f1931-139">Hybrydowe transakcyjnej/przetwarzanie analityczne (HTAP), nazywany także [operacyjne analiz w czasie rzeczywistym](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="f1931-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="f1931-140">Szybkie Elementarz na OLTP w pamięci: [Szybki Start 1: technologii OLTP w pamięci szybciej T-SQL wydajności](http://msdn.microsoft.com/library/mt694156.aspx) (inny toohelp artykułu Rozpoczynanie pracy)</span><span class="sxs-lookup"><span data-stu-id="f1931-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article toohelp you get started)</span></span>

<span data-ttu-id="f1931-141">Szczegółowe wideo na temat technologii hello:</span><span class="sxs-lookup"><span data-stu-id="f1931-141">In-depth videos about hello technologies:</span></span>

- <span data-ttu-id="f1931-142">[OLTP w pamięci w usłudze Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (zawierającą pokaz wydajności przynosi korzyści i kroki tooreproduce te wyniki samodzielnie)</span><span class="sxs-lookup"><span data-stu-id="f1931-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps tooreproduce these results yourself)</span></span>
- [<span data-ttu-id="f1931-143">Wideo OLTP w pamięci: Co to jest i kiedy/jak toouse go</span><span class="sxs-lookup"><span data-stu-id="f1931-143">In-Memory OLTP Videos: What it is and When/How toouse it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="f1931-144">Indeks magazynu kolumn: Analiza w pamięci wideo z konferencji Ignite 2016</span><span class="sxs-lookup"><span data-stu-id="f1931-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="f1931-145">Rozmiar magazynu i danych</span><span class="sxs-lookup"><span data-stu-id="f1931-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="f1931-146">Limit rozmiaru i magazynu danych dla OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="f1931-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="f1931-147">OLTP w pamięci zawiera tabele zoptymalizowane pod kątem pamięci, które są używane do przechowywania danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f1931-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="f1931-148">Następujące tabele są wymagane toofit w pamięci.</span><span class="sxs-lookup"><span data-stu-id="f1931-148">These tables are required toofit in memory.</span></span> <span data-ttu-id="f1931-149">Ponieważ zarządzanie pamięci bezpośrednio w hello usługi baza danych SQL, mamy koncepcji hello przydziału dla danych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f1931-149">Because you manage memory directly in hello SQL Database service, we have hello  concept of a quota for user data.</span></span> <span data-ttu-id="f1931-150">Tę koncepcję jest określony tooas *magazynu OLTP w pamięci*.</span><span class="sxs-lookup"><span data-stu-id="f1931-150">This idea is referred tooas *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="f1931-151">Każda baza danych z obsługiwanych autonomiczny warstwa cenowa i każda pula elastyczna warstwa cenowa zawiera pewne magazynu OLTP w pamięci.</span><span class="sxs-lookup"><span data-stu-id="f1931-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="f1931-152">W czasie hello zapisu otrzymasz gigabajta przestrzeni dyskowej dla każdego 125 jednostki transakcji bazy danych (Dtu) lub elastycznej bazy danych jednostek transakcji (Edtu).</span><span class="sxs-lookup"><span data-stu-id="f1931-152">At hello time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="f1931-153">Witaj [warstw usługi SQL Database](sql-database-service-tiers.md) artykuł ma listę oficjalnego hello hello magazynu OLTP w pamięci, która jest dostępna dla poszczególnych obsługiwanych autonomiczna baza danych i warstwy cenowej puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="f1931-153">hello [SQL Database service tiers](sql-database-service-tiers.md) article has hello official list of hello In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="f1931-154">Witaj następującej liczby elementów kierunku z magazynu OLTP w pamięci, centralnych zasad dostępu:</span><span class="sxs-lookup"><span data-stu-id="f1931-154">hello following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="f1931-155">Wiersze danych aktywnego użytkownika w tabelach zoptymalizowanych pod kątem pamięci i zmiennych tabel.</span><span class="sxs-lookup"><span data-stu-id="f1931-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="f1931-156">Należy pamiętać, że stare wersje wiersza nie są wliczane do zakończenia hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-156">Note that old row versions don't count toward hello cap.</span></span>
- <span data-ttu-id="f1931-157">Indeksów tabel zoptymalizowanych pod kątem pamięci.</span><span class="sxs-lookup"><span data-stu-id="f1931-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="f1931-158">Nakłady operacyjne operacji ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="f1931-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="f1931-159">Jeśli naciśniesz zakończenia hello komunikat o błędzie "limit przydziału" i nie jesteś już stanie tooinsert lub aktualizacji danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-159">If you hit hello cap, you receive an out-of-quota error, and you are no longer able tooinsert or update data.</span></span> <span data-ttu-id="f1931-160">toomitigate tego błędu, Usuń dane, lub zwiększ hello cenowym hello bazy danych lub puli.</span><span class="sxs-lookup"><span data-stu-id="f1931-160">toomitigate this error, delete data or increase hello pricing tier of hello database or pool.</span></span>

<span data-ttu-id="f1931-161">Aby uzyskać więcej informacji dotyczących monitorowania użycia magazynu OLTP w pamięci i konfigurowania alertów, gdy prawie osiągnęła limit hello, zobacz [Monitor w pamięci magazynu](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="f1931-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit hello cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="f1931-162">Temat pul elastycznych</span><span class="sxs-lookup"><span data-stu-id="f1931-162">About elastic pools</span></span>

<span data-ttu-id="f1931-163">Używając puli elastycznej hello magazynu OLTP w pamięci jest współużytkowana przez wszystkie bazy danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-163">With elastic pools, hello In-Memory OLTP storage is shared across all databases in hello pool.</span></span> <span data-ttu-id="f1931-164">W związku z tym użycia hello w jednej bazie danych może wpłynąć na innych baz danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-164">Therefore, hello usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="f1931-165">Są dwa środki zaradcze dla tego:</span><span class="sxs-lookup"><span data-stu-id="f1931-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="f1931-166">Skonfiguruj Max-liczbę jednostek eDTU dla baz danych jest niższa niż liczba jednostek eDTU hello hello pulę jako całość.</span><span class="sxs-lookup"><span data-stu-id="f1931-166">Configure a Max-eDTU for databases that is lower than hello eDTU count for hello pool as a whole.</span></span> <span data-ttu-id="f1931-167">Maksymalna caps hello wykorzystanie magazynu OLTP w pamięci, w dowolnej bazy danych w puli hello, rozmiar toohello, który odpowiada toohello liczby jednostek eDTU.</span><span class="sxs-lookup"><span data-stu-id="f1931-167">This maximum caps hello In-Memory OLTP storage utilization, in any database in hello pool, toohello size that corresponds toohello eDTU count.</span></span>
- <span data-ttu-id="f1931-168">Skonfiguruj Min-eDTU, która jest większa niż 0.</span><span class="sxs-lookup"><span data-stu-id="f1931-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="f1931-169">Tego minimalna gwarancji, że każda baza danych w puli hello ma hello ilość dostępnego magazynu OLTP w pamięci, która odpowiada toohello skonfigurowany Min eDTU.</span><span class="sxs-lookup"><span data-stu-id="f1931-169">This minimum guarantees that each database in hello pool has hello amount of available In-Memory OLTP storage that corresponds toohello configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="f1931-170">Rozmiar danych i magazynu dla indeksów magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="f1931-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="f1931-171">Indeksy magazynu kolumn nie są wymagane toofit w pamięci.</span><span class="sxs-lookup"><span data-stu-id="f1931-171">Columnstore indexes aren't required toofit in memory.</span></span> <span data-ttu-id="f1931-172">W związku z tym hello tylko limit na rozmiar hello indeksów hello jest hello maksymalny ogólny rozmiar bazy danych, które opisano w hello [warstw usługi SQL Database](sql-database-service-tiers.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="f1931-172">Therefore, hello only cap on hello size of hello indexes is hello maximum overall database size, which is documented in hello [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="f1931-173">Gdy używasz klastrowane indeksy magazynu kolumn, kolumnowy kompresji jest używane do przechowywania tabeli podstawowej hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-173">When you use clustered columnstore indexes, columnar compression is used for hello base table storage.</span></span> <span data-ttu-id="f1931-174">Kompresja ta może znacznie zmniejszyć rozmiaru magazynu hello dane użytkowników, co oznacza, że można umieścić więcej danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-174">This compression can significantly reduce hello storage footprint of your user data, which means that you can fit more data in hello database.</span></span> <span data-ttu-id="f1931-175">I kompresji hello można go zwiększyć z [kolumnowy kompresji archiwizacji](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="f1931-175">And hello compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="f1931-176">Hello kompresji, które pozwalają osiągnąć zależy od charakteru hello hello danych, ale 10 razy hello kompresji nie jest nietypowa sytuacja.</span><span class="sxs-lookup"><span data-stu-id="f1931-176">hello amount of compression that you can achieve depends on hello nature of hello data, but 10 times hello compression is not uncommon.</span></span>

<span data-ttu-id="f1931-177">Na przykład jeśli baza danych o maksymalnym rozmiarze 1 terabajtów (TB) i osiągnąć kompresji hello 10 razy przy użyciu indeksów magazynu kolumn, można umieścić łącznie 10 TB danych użytkownika w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times hello compression by using columnstore indexes, you can fit a total of 10 TB of user data in hello database.</span></span>

<span data-ttu-id="f1931-178">Gdy używasz klastrowanych indeksów magazynu kolumn tabeli podstawowej hello jest nadal przechowywane w formacie tradycyjnego magazynu wierszy hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-178">When you use nonclustered columnstore indexes, hello base table is still stored in hello traditional rowstore format.</span></span> <span data-ttu-id="f1931-179">W związku z tym hello oszczędności pojemności magazynu nie są big z klastrowane indeksy magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="f1931-179">Therefore, hello storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="f1931-180">Jednak jeśli liczba indeksów nieklastrowanych tradycyjnych z indeksem magazynu kolumn w jednym, również widzieć ogólną oszczędności rozmiaru magazynu hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="f1931-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in hello storage footprint for hello table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="f1931-181">Przenoszenie baz danych korzystających z technologii w pamięci między warstw cenowych</span><span class="sxs-lookup"><span data-stu-id="f1931-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="f1931-182">Brak Nigdy nie wszelkie niezgodności lub innych problemów po uaktualnieniu tooa wyższe cenowym, takich jak z tooPremium standardowa.</span><span class="sxs-lookup"><span data-stu-id="f1931-182">There are never any incompatibilities or other problems when you upgrade tooa higher pricing tier, such as from Standard tooPremium.</span></span> <span data-ttu-id="f1931-183">Funkcje dostępne Hello i zasoby tylko zwiększyć.</span><span class="sxs-lookup"><span data-stu-id="f1931-183">hello available functionality and resources only increase.</span></span>

<span data-ttu-id="f1931-184">Ale starszą wersję hello warstwy cenowej może niekorzystnie wpłynąć na bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-184">But downgrading hello pricing tier can negatively impact your database.</span></span> <span data-ttu-id="f1931-185">wpływ Hello jest szczególnie widoczne, gdy obniżyć z Premium tooStandard lub podstawowa, gdy baza danych zawiera obiekty OLTP w pamięci.</span><span class="sxs-lookup"><span data-stu-id="f1931-185">hello impact is especially apparent when you downgrade from Premium tooStandard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="f1931-186">Tabele zoptymalizowane pod kątem pamięci i indeksy magazynu kolumn są niedostępne po obniżenia poziomu hello (nawet jeśli są one widoczne).</span><span class="sxs-lookup"><span data-stu-id="f1931-186">Memory-optimized tables, and columnstore indexes, are unavailable after hello downgrade (even if they remain visible).</span></span> <span data-ttu-id="f1931-187">powitalne te same kwestie należy w przypadku obniżenia hello cenowym puli elastycznej lub przenoszenia bazy danych z technologiami w pamięci w standardowej lub podstawowa puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="f1931-187">hello same considerations apply when you're lowering hello pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="f1931-188">Przetwarzanie OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="f1931-188">In-Memory OLTP</span></span>

<span data-ttu-id="f1931-189">*Zmiana wersji na starszą tooBasic/Standard*: OLTP w pamięci nie jest obsługiwane w bazach danych w hello warstwy standardowa lub Basic.</span><span class="sxs-lookup"><span data-stu-id="f1931-189">*Downgrading tooBasic/Standard*: In-Memory OLTP isn't supported in databases in hello Standard or Basic tier.</span></span> <span data-ttu-id="f1931-190">Ponadto nie jest możliwe toomove bazy danych zawierającej wszystkie OLTP w pamięci obiektów toohello warstwy standardowa lub Basic.</span><span class="sxs-lookup"><span data-stu-id="f1931-190">In addition, it isn't possible toomove a database that has any In-Memory OLTP objects toohello Standard or Basic tier.</span></span>

<span data-ttu-id="f1931-191">Przed obniżyć hello bazy danych tooStandard/Basic, Usuń wszystkie tabele zoptymalizowane pod kątem pamięci i typy tabel, a także wszystkich modułów skompilowanych w sposób macierzysty T-SQL.</span><span class="sxs-lookup"><span data-stu-id="f1931-191">Before you downgrade hello database tooStandard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="f1931-192">Brak toounderstand sposób programowy czy danego bazy danych obsługuje OLTP w pamięci.</span><span class="sxs-lookup"><span data-stu-id="f1931-192">There is a programmatic way toounderstand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="f1931-193">Możesz wykonać hello następującego zapytania języka Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="f1931-193">You can execute hello following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="f1931-194">Jeśli hello zapytanie zwraca **1**, OLTP w pamięci jest obsługiwana w tej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-194">If hello query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="f1931-195">*Zmiana wersji na starszą dolnej warstwy Premium tooa*: dane w tabelach zoptymalizowanych pod kątem pamięci musi mieścić się w hello magazynu OLTP w pamięci, który jest skojarzony z hello cenowym hello bazy danych lub w puli elastycznej hello jest dostępny.</span><span class="sxs-lookup"><span data-stu-id="f1931-195">*Downgrading tooa lower Premium tier*: Data in memory-optimized tables must fit within hello In-Memory OLTP storage that is associated with hello pricing tier of hello database or is available in hello elastic pool.</span></span> <span data-ttu-id="f1931-196">Spróbuj hello toolower warstwy cenowej lub przenieść bazę danych hello w puli, który nie ma za mało dostępnej pamięci OLTP w pamięci, operacja hello kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="f1931-196">If you try toolower hello pricing tier or move hello database into a pool that doesn't have enough available In-Memory OLTP storage, hello operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="f1931-197">Indeksy magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="f1931-197">Columnstore indexes</span></span>

<span data-ttu-id="f1931-198">*Zmiana wersji na starszą tooBasic lub Standard*: warstwy standardowa lub Basic hello indeksy są obsługiwane tylko dla warstwy cenowej Premium hello, a nie w systemie magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="f1931-198">*Downgrading tooBasic or Standard*: Columnstore indexes are supported only on hello Premium pricing tier, and not on hello Standard or Basic tiers.</span></span> <span data-ttu-id="f1931-199">Można obniżyć z tooStandard bazy danych lub Basic, indeksu magazynu kolumn staje się niedostępna.</span><span class="sxs-lookup"><span data-stu-id="f1931-199">When you downgrade your database tooStandard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="f1931-200">Hello system obsługuje indeksu magazynu kolumn, ale nigdy nie wykorzystuje hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="f1931-200">hello system maintains your columnstore index, but it never leverages hello index.</span></span> <span data-ttu-id="f1931-201">Uaktualnienie później wstecz tooPremium indeksu magazynu kolumn jest od razu gotowy toobe ponownie wykorzystać.</span><span class="sxs-lookup"><span data-stu-id="f1931-201">If you later upgrade back tooPremium, your columnstore index is immediately ready toobe leveraged again.</span></span>

<span data-ttu-id="f1931-202">Jeśli masz **klastrowanych** indeksu magazynu kolumn po obniżania poziomu niedostępny hello całej tabeli.</span><span class="sxs-lookup"><span data-stu-id="f1931-202">If you have a **clustered** columnstore index, hello whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="f1931-203">Dlatego zaleca się usunąć wszystkich *klastrowanych* indeksy magazynu kolumn przed obniżyć poniżej warstwy Premium hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below hello Premium tier.</span></span>

<span data-ttu-id="f1931-204">*Zmiana wersji na starszą dolnej warstwy Premium tooa*: ten obniżenia poziomu zakończy się pomyślnie, jeśli hello całej bazy danych mieści się w hello maksymalny rozmiar bazy danych dla obiektu docelowego hello warstwy cenowej lub do dostępnego magazynu hello w puli elastycznej hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-204">*Downgrading tooa lower Premium tier*: This downgrade succeeds if hello whole database fits within hello maximum database size for hello target pricing tier, or within hello available storage in hello elastic pool.</span></span> <span data-ttu-id="f1931-205">Nie ma żadnego określonego wpływu z hello indeksy magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="f1931-205">There is no specific impact from hello columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a><span data-ttu-id="f1931-206">1. Zainstaluj hello próbki OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="f1931-206">1. Install hello In-Memory OLTP sample</span></span>

<span data-ttu-id="f1931-207">Witaj AdventureWorksLT przykładowej bazy danych można utworzyć za pomocą kilku kliknięć w hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f1931-207">You can create hello AdventureWorksLT sample database with a few clicks in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="f1931-208">Następnie hello w tej sekcji opisano sposób można wzbogacić bazy danych AdventureWorksLT z obiektami OLTP w pamięci i Wykaż zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="f1931-208">Then, hello steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="f1931-209">Aby uzyskać więcej simplistic, ale atrakcyjność wizualną demonstrację wydajności OLTP w pamięci Zobacz:</span><span class="sxs-lookup"><span data-stu-id="f1931-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="f1931-210">Wersja: [w pamięci — oltp pokaz-wersja 1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="f1931-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="f1931-211">Kod źródłowy: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="f1931-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="f1931-212">Kroki instalacji</span><span class="sxs-lookup"><span data-stu-id="f1931-212">Installation steps</span></span>

1. <span data-ttu-id="f1931-213">W hello [portalu Azure](https://portal.azure.com/), utworzyć bazy danych Premium na serwerze.</span><span class="sxs-lookup"><span data-stu-id="f1931-213">In hello [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="f1931-214">Zestaw hello **źródła** toohello AdventureWorksLT przykładowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-214">Set hello **Source** toohello AdventureWorksLT sample database.</span></span> <span data-ttu-id="f1931-215">Aby uzyskać szczegółowe instrukcje, zobacz [utworzyć pierwszą bazę danych Azure SQL](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f1931-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="f1931-216">Uzyskuj toohello bazy danych programu SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1931-216">Connect toohello database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="f1931-217">Kopiuj hello [skryptu OLTP w pamięci języka Transact-SQL](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Schowka.</span><span class="sxs-lookup"><span data-stu-id="f1931-217">Copy hello [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour clipboard.</span></span> <span data-ttu-id="f1931-218">Witaj skryptu T-SQL tworzy hello obiekty niezbędne w pamięci w hello AdventureWorksLT przykładową bazę danych utworzoną w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="f1931-218">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="f1931-219">Wklej hello skryptu T-SQL w programie SSMS, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-219">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="f1931-220">Witaj `MEMORY_OPTIMIZED = ON` instrukcji CREATE TABLE klauzuli są niezwykle istotne.</span><span class="sxs-lookup"><span data-stu-id="f1931-220">hello `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="f1931-221">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f1931-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="f1931-222">Błąd 40536</span><span class="sxs-lookup"><span data-stu-id="f1931-222">Error 40536</span></span>


<span data-ttu-id="f1931-223">Jeśli zostanie wyświetlony błąd 40536 po uruchomieniu skryptu hello T-SQL, uruchom powitania po tooverify skryptu T-SQL, czy w pamięci obsługuje hello bazy danych:</span><span class="sxs-lookup"><span data-stu-id="f1931-223">If you get error 40536 when you run hello T-SQL script, run hello following T-SQL script tooverify whether hello database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="f1931-224">W wyniku **0** oznacza, że w pamięci nie jest obsługiwany, i **1** oznacza, że jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="f1931-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="f1931-225">toodiagnose hello problem, upewnij się, że hello baza danych jest w warstwie usług Premium hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-225">toodiagnose hello problem, ensure that hello database is at hello Premium service tier.</span></span>


#### <a name="about-hello-created-memory-optimized-items"></a><span data-ttu-id="f1931-226">O hello utworzone elementy zoptymalizowanych pod kątem pamięci</span><span class="sxs-lookup"><span data-stu-id="f1931-226">About hello created memory-optimized items</span></span>

<span data-ttu-id="f1931-227">**Tabele**: hello przykład zawiera następujące tabele zoptymalizowane pod kątem pamięci hello:</span><span class="sxs-lookup"><span data-stu-id="f1931-227">**Tables**: hello sample contains hello following memory-optimized tables:</span></span>

- <span data-ttu-id="f1931-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="f1931-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="f1931-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="f1931-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="f1931-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="f1931-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="f1931-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="f1931-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="f1931-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="f1931-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="f1931-233">Możesz sprawdzić tabel zoptymalizowanych pod kątem pamięci przy użyciu hello **Eksplorator obiektów** w programie SSMS.</span><span class="sxs-lookup"><span data-stu-id="f1931-233">You can inspect memory-optimized tables through hello **Object Explorer** in SSMS.</span></span> <span data-ttu-id="f1931-234">Kliknij prawym przyciskiem myszy **tabel** > **filtru** > **ustawienia filtrowania** > **jest zoptymalizowana pod kątem pamięci**.</span><span class="sxs-lookup"><span data-stu-id="f1931-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="f1931-235">Witaj, wartość jest równa 1.</span><span class="sxs-lookup"><span data-stu-id="f1931-235">hello value equals 1.</span></span>


<span data-ttu-id="f1931-236">Lub możesz zbadać hello widokach katalogów, takich jak:</span><span class="sxs-lookup"><span data-stu-id="f1931-236">Or you can query hello catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="f1931-237">**Procedura składowana skompilowanych w sposób macierzysty**: SalesLT.usp_InsertSalesOrder_inmem można sprawdzić za pomocą widoku wykazu kwerendy:</span><span class="sxs-lookup"><span data-stu-id="f1931-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a><span data-ttu-id="f1931-238">Uruchom hello przykładowe obciążenie OLTP</span><span class="sxs-lookup"><span data-stu-id="f1931-238">Run hello sample OLTP workload</span></span>

<span data-ttu-id="f1931-239">Witaj jedyna różnica między hello następujące dwa *procedur składowanych* hello Pierwsza procedura używa wersji hello tabel zoptymalizowanych pod kątem pamięci, podczas hello Druga procedura używa hello zwykłych tabelach na dysku:</span><span class="sxs-lookup"><span data-stu-id="f1931-239">hello only difference between hello following two *stored procedures* is that hello first procedure uses memory-optimized versions of hello tables, while hello second procedure uses hello regular on-disk tables:</span></span>

- <span data-ttu-id="f1931-240">SalesLT**.** usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="f1931-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="f1931-241">SalesLT**.** usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="f1931-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="f1931-242">W tej sekcji, zobaczysz, jak toouse hello przydatną **ostress.exe** tooexecute narzędzie Witaj dwie procedury przechowywanej na poziomach stressful.</span><span class="sxs-lookup"><span data-stu-id="f1931-242">In this section, you see how toouse hello handy **ostress.exe** utility tooexecute hello two stored procedures at stressful levels.</span></span> <span data-ttu-id="f1931-243">Możesz porównać, jak długo toofinish uruchamia akcent hello dwa.</span><span class="sxs-lookup"><span data-stu-id="f1931-243">You can compare how long it takes for hello two stress runs toofinish.</span></span>


<span data-ttu-id="f1931-244">Po uruchomieniu ostress.exe zaleca się, że przekazujesz przeznaczony dla obu hello następujące wartości parametrów:</span><span class="sxs-lookup"><span data-stu-id="f1931-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of hello following:</span></span>

- <span data-ttu-id="f1931-245">Uruchamianie dużej liczby równoczesnych połączeń przy użyciu - n100.</span><span class="sxs-lookup"><span data-stu-id="f1931-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="f1931-246">Ma przy każdej pętli połączenia setki razy, za pomocą parametru-r500.</span><span class="sxs-lookup"><span data-stu-id="f1931-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="f1931-247">Jednak może być toostart wartościami znacznie mniejszy, takich jak - n10 i - r50 tooensure, czy wszystko działa.</span><span class="sxs-lookup"><span data-stu-id="f1931-247">However, you might want toostart with much smaller values like -n10 and -r50 tooensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="f1931-248">Skrypt dla ostress.exe</span><span class="sxs-lookup"><span data-stu-id="f1931-248">Script for ostress.exe</span></span>


<span data-ttu-id="f1931-249">Ta sekcja wyświetla hello skryptu T-SQL, osadzonego w naszym ostress.exe wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f1931-249">This section displays hello T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="f1931-250">skrypt Hello używa elementów, które zostały utworzone przez hello skryptu T-SQL, który został wcześniej zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="f1931-250">hello script uses items that were created by hello T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="f1931-251">Hello poniższy skrypt wstawia przykładowe zamówienia sprzedaży z pięciu pozycji do następujących hello zoptymalizowanych pod kątem pamięci *tabel*:</span><span class="sxs-lookup"><span data-stu-id="f1931-251">hello following script inserts a sample sales order with five line items into hello following memory-optimized *tables*:</span></span>

- <span data-ttu-id="f1931-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="f1931-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="f1931-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="f1931-253">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="f1931-254">Witaj toomake *_ondisk* wersji hello ostress.exe poprzedniego skryptu T-SQL, należy zastąpić zarówno wystąpień hello *_inmem* podciąg z *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="f1931-254">toomake hello *_ondisk* version of hello preceding T-SQL script for ostress.exe, you would replace both occurrences of hello *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="f1931-255">Te elementy zastępcze wpływa na powitania nazwy tabel i procedur składowanych.</span><span class="sxs-lookup"><span data-stu-id="f1931-255">These replacements affect hello names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="f1931-256">Zainstaluj narzędzia RML i ostress</span><span class="sxs-lookup"><span data-stu-id="f1931-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="f1931-257">W idealnym przypadku będzie zaplanować toorun ostress.exe na maszynie wirtualnej platformy Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="f1931-257">Ideally, you would plan toorun ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="f1931-258">Należy utworzyć [maszyny Wirtualnej Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) w hello tego samego Azure region geograficzny, w którym znajduje się baza danych AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="f1931-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="f1931-259">Ale może uruchamiać ostress.exe na laptopie zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="f1931-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="f1931-260">Hello maszyny Wirtualnej lub niezależnie od hosta, możesz wybrać, zainstaluj narzędzia powtarzania Markup Language (RML) hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-260">On hello VM, or on whatever host you choose, install hello Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="f1931-261">programy narzędziowe Hello ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="f1931-261">hello utilities include ostress.exe.</span></span>

<span data-ttu-id="f1931-262">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="f1931-262">For more information, see:</span></span>
- <span data-ttu-id="f1931-263">Witaj dyskusji ostress.exe [przykładowej bazy danych OLTP w pamięci](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1931-263">hello ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="f1931-264">[Przykładowe bazy danych do OLTP w pamięci](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1931-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="f1931-265">Witaj [blogu instalowania ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1931-265">hello [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a><span data-ttu-id="f1931-266">Uruchom hello *_inmem* najpierw podkreślają obciążenia</span><span class="sxs-lookup"><span data-stu-id="f1931-266">Run hello *_inmem* stress workload first</span></span>


<span data-ttu-id="f1931-267">Można użyć *RML Cmd monitu* toorun okno wiersza polecenia naszych ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="f1931-267">You can use an *RML Cmd Prompt* window toorun our ostress.exe command line.</span></span> <span data-ttu-id="f1931-268">Parametry wiersza polecenia Hello bezpośrednie ostress do:</span><span class="sxs-lookup"><span data-stu-id="f1931-268">hello command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="f1931-269">Równoczesne uruchamianie połączenia o szybkości 100 (-n100).</span><span class="sxs-lookup"><span data-stu-id="f1931-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="f1931-270">Każdy połączenia uruchomienia skryptu T-SQL hello 50 razy (-r50).</span><span class="sxs-lookup"><span data-stu-id="f1931-270">Have each connection run hello T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="f1931-271">Witaj toorun poprzedzających ostress.exe wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="f1931-271">toorun hello preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="f1931-272">Resetuj zawartości danych bazy danych hello, uruchamiając następujące polecenie w programie SSMS, toodelete hello wszystkie dane hello został wstawiony przez wszystkie poprzednie działa:</span><span class="sxs-lookup"><span data-stu-id="f1931-272">Reset hello database data content by running hello following command in SSMS, toodelete all hello data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="f1931-273">Skopiuj tekst hello hello poprzedzających ostress.exe wiersza polecenia tooyour Schowka.</span><span class="sxs-lookup"><span data-stu-id="f1931-273">Copy hello text of hello preceding ostress.exe command line tooyour clipboard.</span></span>

3. <span data-ttu-id="f1931-274">Zastąp hello `<placeholders>` hello parametrów -S - U -P - d z hello Popraw wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="f1931-274">Replace hello `<placeholders>` for hello parameters -S -U -P -d with hello correct real values.</span></span>

4. <span data-ttu-id="f1931-275">Edytowany linii polecenia są uruchamiane w oknie RML Cmd.</span><span class="sxs-lookup"><span data-stu-id="f1931-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="f1931-276">Wynik jest czas trwania</span><span class="sxs-lookup"><span data-stu-id="f1931-276">Result is a duration</span></span>


<span data-ttu-id="f1931-277">Po zakończeniu pracy ostress.exe zapisuje hello czas trwania jako jego końcowego wiersza danych wyjściowych w oknie RML Cmd hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-277">When ostress.exe finishes, it writes hello run duration as its final line of output in hello RML Cmd window.</span></span> <span data-ttu-id="f1931-278">Na przykład krótszą uruchomienia testu trwała około 1,5 minuty:</span><span class="sxs-lookup"><span data-stu-id="f1931-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="f1931-279">Resetuj, edytowanie *_ondisk*, uruchom ponownie</span><span class="sxs-lookup"><span data-stu-id="f1931-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="f1931-280">Po uzyskaniu wyniku hello hello *_inmem* uruchomić, wykonaj następujące kroki dla hello hello *_ondisk* Uruchom:</span><span class="sxs-lookup"><span data-stu-id="f1931-280">After you have hello result from hello *_inmem* run, perform hello following steps for hello *_ondisk* run:</span></span>


1. <span data-ttu-id="f1931-281">Resetowanie hello bazy danych, uruchamiając następujące polecenie w programie SSMS toodelete hello wszystkie dane hello wstawione przez hello poprzedniego uruchomienia:</span><span class="sxs-lookup"><span data-stu-id="f1931-281">Reset hello database by running hello following command in SSMS toodelete all hello data that was inserted by hello previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="f1931-282">Edytuj hello ostress.exe wiersza polecenia tooreplace wszystkie *_inmem* z *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="f1931-282">Edit hello ostress.exe command line tooreplace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="f1931-283">Uruchom ponownie ostress.exe na powitania po raz drugi i przechwytywania hello czas trwania wynik.</span><span class="sxs-lookup"><span data-stu-id="f1931-283">Rerun ostress.exe for hello second time, and capture hello duration result.</span></span>

4. <span data-ttu-id="f1931-284">Ponownie resetowania hello bazy danych (w przypadku usuwania odpowiedzialne, które mogą być duże ilości danych testowych).</span><span class="sxs-lookup"><span data-stu-id="f1931-284">Again, reset hello database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="f1931-285">Porównanie oczekiwanego wyników</span><span class="sxs-lookup"><span data-stu-id="f1931-285">Expected comparison results</span></span>

<span data-ttu-id="f1931-286">Nasze testy w pamięci wykazały, że wydajność poprawia **dziewięciokrotnie** dla tego simplistic obciążenia z ostress uruchomione na maszynie Wirtualnej platformy Azure w hello sam region platformy Azure jako hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f1931-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in hello same Azure region as hello database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a><span data-ttu-id="f1931-287">2. Zainstaluj hello próbki analityka w pamięci</span><span class="sxs-lookup"><span data-stu-id="f1931-287">2. Install hello In-Memory Analytics sample</span></span>


<span data-ttu-id="f1931-288">W tej sekcji można porównywać hello We/Wy i wyniki statystyk podczas korzystania z indeksu magazynu kolumn lub indeksu b drzewa tradycyjnych.</span><span class="sxs-lookup"><span data-stu-id="f1931-288">In this section, you compare hello IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="f1931-289">Analiz w czasie rzeczywistym na obciążenia OLTP jest często najlepszym toouse nieklastrowany indeks magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="f1931-289">For real-time analytics on an OLTP workload, it's often best toouse a nonclustered columnstore index.</span></span> <span data-ttu-id="f1931-290">Aby uzyskać więcej informacji, zobacz [opisane indeksy magazynu kolumn](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1931-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-hello-columnstore-analytics-test"></a><span data-ttu-id="f1931-291">Przygotowanie hello magazynu kolumn analytics testu</span><span class="sxs-lookup"><span data-stu-id="f1931-291">Prepare hello columnstore analytics test</span></span>


1. <span data-ttu-id="f1931-292">Użyj hello Azure toocreate portalu nową bazę danych AdventureWorksLT z hello próbki.</span><span class="sxs-lookup"><span data-stu-id="f1931-292">Use hello Azure portal toocreate a fresh AdventureWorksLT database from hello sample.</span></span>
 - <span data-ttu-id="f1931-293">Użyj takiej samej nazwie.</span><span class="sxs-lookup"><span data-stu-id="f1931-293">Use that exact name.</span></span>
 - <span data-ttu-id="f1931-294">Wybierz wszystkie warstwy usług Premium.</span><span class="sxs-lookup"><span data-stu-id="f1931-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="f1931-295">Kopiuj hello [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Schowka.</span><span class="sxs-lookup"><span data-stu-id="f1931-295">Copy hello [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour clipboard.</span></span>
 - <span data-ttu-id="f1931-296">Witaj skryptu T-SQL tworzy hello obiekty niezbędne w pamięci w hello AdventureWorksLT przykładową bazę danych utworzoną w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="f1931-296">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="f1931-297">Witaj skrypt tworzy hello tabeli wymiarów i tabel faktów.</span><span class="sxs-lookup"><span data-stu-id="f1931-297">hello script creates hello Dimension table and two fact tables.</span></span> <span data-ttu-id="f1931-298">tabele faktów Hello są wypełniane przy użyciu 3.5 milion wierszy.</span><span class="sxs-lookup"><span data-stu-id="f1931-298">hello fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="f1931-299">skrypt Hello może potrwać toocomplete 15 minut.</span><span class="sxs-lookup"><span data-stu-id="f1931-299">hello script might take 15 minutes toocomplete.</span></span>

3. <span data-ttu-id="f1931-300">Wklej hello skryptu T-SQL w programie SSMS, a następnie uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="f1931-300">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="f1931-301">Witaj **magazynu kolumn** — słowo kluczowe w hello **CREATE INDEX** instrukcja jest niezwykle ważny, jak w programie:</span><span class="sxs-lookup"><span data-stu-id="f1931-301">hello **COLUMNSTORE** keyword in hello **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="f1931-302">Ustaw poziom toocompatibility AdventureWorksLT 130:</span><span class="sxs-lookup"><span data-stu-id="f1931-302">Set AdventureWorksLT toocompatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="f1931-303">Poziom 130 nie jest z nią bezpośrednio powiązane pamięci tooIn funkcji.</span><span class="sxs-lookup"><span data-stu-id="f1931-303">Level 130 is not directly related tooIn-Memory features.</span></span> <span data-ttu-id="f1931-304">Jednak poziom 130 zwykle zapewnia lepszą wydajność zapytań, niż 120.</span><span class="sxs-lookup"><span data-stu-id="f1931-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="f1931-305">Tabele klucza i indeksy magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="f1931-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="f1931-306">dbo. Tabela mająca klastrowany indeks magazynu kolumn, który udostępnia zaawansowane kompresji w hello jest FactResellerSalesXL_CCI *danych* poziom.</span><span class="sxs-lookup"><span data-stu-id="f1931-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at hello *data* level.</span></span>

- <span data-ttu-id="f1931-307">dbo. Tabela mająca równoważne regularne indeks klastrowany, które są kompresowane tylko w hello jest FactResellerSalesXL_PageCompressed *strony* poziom.</span><span class="sxs-lookup"><span data-stu-id="f1931-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at hello *page* level.</span></span>


#### <a name="key-queries-toocompare-hello-columnstore-index"></a><span data-ttu-id="f1931-308">Indeks magazynu kolumn hello toocompare klucza zapytania</span><span class="sxs-lookup"><span data-stu-id="f1931-308">Key queries toocompare hello columnstore index</span></span>


<span data-ttu-id="f1931-309">Brak [kilka typów zapytania T-SQL, które można uruchomić](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee ulepszenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="f1931-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performance improvements.</span></span> <span data-ttu-id="f1931-310">W kroku 2 hello skryptu T-SQL należy zwrócić uwagę toothis pary zapytań.</span><span class="sxs-lookup"><span data-stu-id="f1931-310">In step 2 in hello T-SQL script, pay attention toothis pair of queries.</span></span> <span data-ttu-id="f1931-311">Różnią się tylko w jednym wierszu:</span><span class="sxs-lookup"><span data-stu-id="f1931-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="f1931-312">Klastrowany indeks magazynu kolumn jest hello FactResellerSalesXL\_WIK tabeli.</span><span class="sxs-lookup"><span data-stu-id="f1931-312">A clustered columnstore index is in hello FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="f1931-313">Hello poniższy fragment skryptu T-SQL wyświetla statystyki dla We/Wy i godziny dla zapytania hello każdej tabeli.</span><span class="sxs-lookup"><span data-stu-id="f1931-313">hello following T-SQL script excerpt prints statistics for IO and TIME for hello query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="f1931-314">W bazie danych z warstwy cenowej P2 hello może spodziewać się bardziej wydajne hello około dziewięciokrotnie dla tego zapytania przy użyciu hello klastrowany indeks magazynu kolumn w porównaniu z hello tradycyjnych indeksu.</span><span class="sxs-lookup"><span data-stu-id="f1931-314">In a database with hello P2 pricing tier, you can expect about nine times hello performance gain for this query by using hello clustered columnstore index compared with hello traditional index.</span></span> <span data-ttu-id="f1931-315">Z P15 z replikacją może spodziewać się bardziej wydajne hello około 57 razy przy użyciu hello indeksu magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="f1931-315">With P15, you can expect about 57 times hello performance gain by using hello columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="f1931-316">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f1931-316">Next steps</span></span>

- [<span data-ttu-id="f1931-317">Szybki Start 1: Technologii OLTP w pamięci, aby zwiększyć wydajność T-SQL</span><span class="sxs-lookup"><span data-stu-id="f1931-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="f1931-318">Użyj OLTP w pamięci w istniejącej aplikacji usługi Azure SQL</span><span class="sxs-lookup"><span data-stu-id="f1931-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="f1931-319">[Monitor OLTP w pamięci magazynu](sql-database-in-memory-oltp-monitoring.md) dla OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="f1931-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f1931-320">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="f1931-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="f1931-321">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="f1931-321">Deeper information</span></span>

- [<span data-ttu-id="f1931-322">Dowiedz się, jak kworum podwaja obciążenia klucza bazy danych podczas opuszczania jednostek dtu w warstwie 70% z OLTP w pamięci w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="f1931-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="f1931-323">OLTP w pamięci w bazie danych Azure SQL wpis w blogu</span><span class="sxs-lookup"><span data-stu-id="f1931-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="f1931-324">Dowiedz się więcej o OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="f1931-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="f1931-325">Dowiedz się więcej o indeksy magazynu kolumn</span><span class="sxs-lookup"><span data-stu-id="f1931-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="f1931-326">Dowiedz się więcej o operacyjne analiz w czasie rzeczywistym</span><span class="sxs-lookup"><span data-stu-id="f1931-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="f1931-327">Zobacz [typowe wzorce obciążeń i zagadnienia dotyczące migracji](http://msdn.microsoft.com/library/dn673538.aspx) (w którym opisano wzorców obciążenia, gdzie OLTP w pamięci zapewnia często znaczący wzrost wydajności)</span><span class="sxs-lookup"><span data-stu-id="f1931-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="f1931-328">Aplikacja — projekt</span><span class="sxs-lookup"><span data-stu-id="f1931-328">Application design</span></span>

- [<span data-ttu-id="f1931-329">(Optymalizacja w pamięci) OLTP w pamięci</span><span class="sxs-lookup"><span data-stu-id="f1931-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="f1931-330">Użyj OLTP w pamięci w istniejącej aplikacji usługi Azure SQL</span><span class="sxs-lookup"><span data-stu-id="f1931-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="f1931-331">Narzędzia</span><span class="sxs-lookup"><span data-stu-id="f1931-331">Tools</span></span>

- [<span data-ttu-id="f1931-332">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f1931-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="f1931-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="f1931-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="f1931-334">SQL Server Data Tools (SSDT)</span><span class="sxs-lookup"><span data-stu-id="f1931-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
