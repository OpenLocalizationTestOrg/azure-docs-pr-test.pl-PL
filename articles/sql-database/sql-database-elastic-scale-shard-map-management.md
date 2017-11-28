---
title: aaaScale limit bazy danych Azure SQL | Dokumentacja firmy Microsoft
description: Jak toouse hello ShardMapManager, biblioteki klienta elastycznej bazy danych
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a><span data-ttu-id="b5a0b-103">Skalowanie w poziomie baz danych, menedżera map niezależnego fragmentu hello</span><span class="sxs-lookup"><span data-stu-id="b5a0b-103">Scale out databases with hello shard map manager</span></span>
<span data-ttu-id="b5a0b-104">tooeasily skalowania bazy danych SQL Azure, użyj Menedżera map niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-104">tooeasily scale out databases on SQL Azure, use a shard map manager.</span></span> <span data-ttu-id="b5a0b-105">Menedżera map niezależnego fragmentu Hello jest specjalne bazy danych, która przechowuje Mapowanie globalne informacje o wszystkich odłamków (bazy danych) w zestawie niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-105">hello shard map manager is a special database that maintains global mapping information about all shards (databases) in a shard set.</span></span> <span data-ttu-id="b5a0b-106">Witaj metadanych umożliwia aplikacji tooconnect toohello prawidłową bazę danych na podstawie wartości hello z hello **klucza dzielenia na fragmenty**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-106">hello metadata allows an application tooconnect toohello correct database based upon hello value of hello **sharding key**.</span></span> <span data-ttu-id="b5a0b-107">Ponadto każdy identyfikator niezależnego fragmentu w zestawie hello zawiera map, które śledzą dane dotyczące niezależnych lokalne powitania (nazywane **shardlets**).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-107">In addition, every shard in hello set contains maps that track hello local shard data (known as **shardlets**).</span></span> 

![Identyfikator niezależnego fragmentu mapy zarządzania](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

<span data-ttu-id="b5a0b-109">Zrozumienie, jak te mapowania są zbudowane jest istotne tooshard mapy zarządzania.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-109">Understanding how these maps are constructed is essential tooshard map management.</span></span> <span data-ttu-id="b5a0b-110">Odbywa się przy użyciu hello [klasy ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), liczba znalezionych w hello [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md) toomanage niezależnego fragmentu mapowania.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-110">This is done using hello [ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx), found in hello [Elastic Database client library](sql-database-elastic-database-client-library.md) toomanage shard maps.</span></span>  

## <a name="shard-maps-and-shard-mappings"></a><span data-ttu-id="b5a0b-111">Mapy niezależnego fragmentu i niezależnego fragmentu mapowania</span><span class="sxs-lookup"><span data-stu-id="b5a0b-111">Shard maps and shard mappings</span></span>
<span data-ttu-id="b5a0b-112">Dla każdego niezależnych musisz wybrać typ hello toocreate mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-112">For each shard, you must select hello type of shard map toocreate.</span></span> <span data-ttu-id="b5a0b-113">Wybór Hello zależy od hello Architektura bazy danych:</span><span class="sxs-lookup"><span data-stu-id="b5a0b-113">hello choice depends on hello database architecture:</span></span> 

1. <span data-ttu-id="b5a0b-114">Pojedynczej dzierżawy na bazę danych</span><span class="sxs-lookup"><span data-stu-id="b5a0b-114">Single tenant per database</span></span>  
2. <span data-ttu-id="b5a0b-115">Wiele dzierżaw dla jednej bazy danych (dwa typy):</span><span class="sxs-lookup"><span data-stu-id="b5a0b-115">Multiple tenants per database (two types):</span></span>
   1. <span data-ttu-id="b5a0b-116">Mapowanie list</span><span class="sxs-lookup"><span data-stu-id="b5a0b-116">List mapping</span></span>
   2. <span data-ttu-id="b5a0b-117">Mapowanie zakresu</span><span class="sxs-lookup"><span data-stu-id="b5a0b-117">Range mapping</span></span>

<span data-ttu-id="b5a0b-118">Model pojedynczego dzierżawcy można utworzyć **mapowania listy** mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-118">For a single-tenant model, create a **list mapping** shard map.</span></span> <span data-ttu-id="b5a0b-119">model pojedynczej dzierżawy Hello przypisuje jednej bazy danych dla każdego dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-119">hello single-tenant model assigns one database per tenant.</span></span> <span data-ttu-id="b5a0b-120">Jest to efektywne modelu dla deweloperów SaaS, ponieważ takie rozwiązanie upraszcza zarządzanie.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-120">This is an effective model for SaaS developers as it simplifies management.</span></span>

![Mapowanie list][1]

<span data-ttu-id="b5a0b-122">modelu wielodostępnym Hello przypisuje kilka dzierżaw tooa pojedynczej bazy danych (i grup dzierżawcy mogą rozpowszechniają wielu baz danych).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-122">hello multi-tenant model assigns several tenants tooa single database (and you can distribute groups of tenants across multiple databases).</span></span> <span data-ttu-id="b5a0b-123">Użyj tego modelu, gdy oczekuje się, że każdy dzierżawca toohave niewielkie zbiory danych musi.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-123">Use this model when you expect each tenant toohave small data needs.</span></span> <span data-ttu-id="b5a0b-124">W tym modelu możemy Przypisz zakres przy użyciu bazy danych tooa dzierżawców **mapowanie zakresu**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-124">In this model, we assign a range of tenants tooa database using **range mapping**.</span></span> 

![Mapowanie zakresu][2]

<span data-ttu-id="b5a0b-126">Lub możesz wdrożyć model bazy danych wielu dzierżawców przy użyciu *mapowania listy* tooassign wiele dzierżaw tooa pojedynczej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-126">Or you can implement a multi-tenant database model using a *list mapping* tooassign multiple tenants tooa single database.</span></span> <span data-ttu-id="b5a0b-127">Na przykład DB1 jest używane toostore informacji na temat identyfikatora dzierżawy 1 do 5 i bazy danych DB2 przechowuje dane dla dzierżawy 7 i dzierżawcy 10.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-127">For example, DB1 is used toostore information about tenant id 1 and 5, and DB2 stores data for tenant 7 and tenant 10.</span></span> 

![Wielu dzierżawców dla jednej bazy danych][3] 

### <a name="supported-net-types-for-sharding-keys"></a><span data-ttu-id="b5a0b-129">Obsługiwane typy .net dla kluczy dzielenia na fragmenty</span><span class="sxs-lookup"><span data-stu-id="b5a0b-129">Supported .Net types for sharding keys</span></span>
<span data-ttu-id="b5a0b-130">Elastyczne hello obsługi skalowania po .net Framework typy jako klucze dzielenia na fragmenty:</span><span class="sxs-lookup"><span data-stu-id="b5a0b-130">Elastic Scale support hello following .Net Framework types as sharding keys:</span></span>

* <span data-ttu-id="b5a0b-131">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="b5a0b-131">integer</span></span>
* <span data-ttu-id="b5a0b-132">długa</span><span class="sxs-lookup"><span data-stu-id="b5a0b-132">long</span></span>
* <span data-ttu-id="b5a0b-133">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="b5a0b-133">guid</span></span>
* <span data-ttu-id="b5a0b-134">Byte]</span><span class="sxs-lookup"><span data-stu-id="b5a0b-134">byte[]</span></span>  
* <span data-ttu-id="b5a0b-135">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="b5a0b-135">datetime</span></span>
* <span data-ttu-id="b5a0b-136">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="b5a0b-136">timespan</span></span>
* <span data-ttu-id="b5a0b-137">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="b5a0b-137">datetimeoffset</span></span>

### <a name="list-and-range-shard-maps"></a><span data-ttu-id="b5a0b-138">Mapuje niezależnych listy i zakresu</span><span class="sxs-lookup"><span data-stu-id="b5a0b-138">List and range shard maps</span></span>
<span data-ttu-id="b5a0b-139">Mapy niezależnych można skonstruować przy użyciu **list dzielenia na fragmenty poszczególne wartości klucza**, lub może być skonstruowany, za pomocą **wartości klucza zakresy dzielenia na fragmenty**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-139">Shard maps can be constructed using **lists of individual sharding key values**, or they can be constructed using **ranges of sharding key values**.</span></span> 

### <a name="list-shard-maps"></a><span data-ttu-id="b5a0b-140">Lista niezależnych mapy</span><span class="sxs-lookup"><span data-stu-id="b5a0b-140">List shard maps</span></span>
<span data-ttu-id="b5a0b-141">**Odłamków** zawierają **shardlets** i mapowanie shardlets tooshards hello jest obsługiwana przez mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-141">**Shards** contain **shardlets** and hello mapping of shardlets tooshards is maintained by a shard map.</span></span> <span data-ttu-id="b5a0b-142">A **mapy niezależnego fragmentu listy** jest skojarzenie między hello poszczególnych wartości klucza identyfikujące hello shardlets i baz danych hello, które służą jako niezależne.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-142">A **list shard map** is an association between hello individual key values that identify hello shardlets and hello databases that serve as shards.</span></span>  <span data-ttu-id="b5a0b-143">**Lista mapowań** są jawne i różnych wartości klucza może być zmapowane toohello tej samej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-143">**List mappings** are explicit and different key values can be mapped toohello same database.</span></span> <span data-ttu-id="b5a0b-144">Na przykład klucz 1 mapuje tooDatabase A i wartości kluczy, 3 i 6 odwołania B. bazy danych</span><span class="sxs-lookup"><span data-stu-id="b5a0b-144">For example, key 1 maps tooDatabase A, and key values 3 and 6 both reference Database B.</span></span>

| <span data-ttu-id="b5a0b-145">Klucz</span><span class="sxs-lookup"><span data-stu-id="b5a0b-145">Key</span></span> | <span data-ttu-id="b5a0b-146">Identyfikator niezależnego fragmentu lokalizacji</span><span class="sxs-lookup"><span data-stu-id="b5a0b-146">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="b5a0b-147">1</span><span class="sxs-lookup"><span data-stu-id="b5a0b-147">1</span></span> |<span data-ttu-id="b5a0b-148">Database_A</span><span class="sxs-lookup"><span data-stu-id="b5a0b-148">Database_A</span></span> |
| <span data-ttu-id="b5a0b-149">3</span><span class="sxs-lookup"><span data-stu-id="b5a0b-149">3</span></span> |<span data-ttu-id="b5a0b-150">Database_B</span><span class="sxs-lookup"><span data-stu-id="b5a0b-150">Database_B</span></span> |
| <span data-ttu-id="b5a0b-151">4</span><span class="sxs-lookup"><span data-stu-id="b5a0b-151">4</span></span> |<span data-ttu-id="b5a0b-152">Database_C</span><span class="sxs-lookup"><span data-stu-id="b5a0b-152">Database_C</span></span> |
| <span data-ttu-id="b5a0b-153">6</span><span class="sxs-lookup"><span data-stu-id="b5a0b-153">6</span></span> |<span data-ttu-id="b5a0b-154">Database_B</span><span class="sxs-lookup"><span data-stu-id="b5a0b-154">Database_B</span></span> |
| <span data-ttu-id="b5a0b-155">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="b5a0b-155">...</span></span> |<span data-ttu-id="b5a0b-156">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="b5a0b-156">...</span></span> |

### <a name="range-shard-maps"></a><span data-ttu-id="b5a0b-157">Mapuje niezależnych zakresu</span><span class="sxs-lookup"><span data-stu-id="b5a0b-157">Range shard maps</span></span>
<span data-ttu-id="b5a0b-158">W **mapy niezależnego fragmentu zakresu**, zakresem kluczy hello jest opisany przez parę **[wartość niska, wysoka wartość)** gdzie hello *niska wartość* jest hello klucz minimum zakresu hello i hello *Wysokiej wartości* jest hello pierwszej wartości wyższej niż hello zakres.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-158">In a **range shard map**, hello key range is described by a pair **[Low Value, High Value)** where hello *Low Value* is hello minimum key in hello range, and hello *High Value* is hello first value higher than hello range.</span></span> 

<span data-ttu-id="b5a0b-159">Na przykład **[0, 100)** obejmuje wszystkie liczby całkowite większe niż lub równa 0 i mniejsza niż 100.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-159">For example, **[0, 100)** includes all integers greater than or equal 0 and less than 100.</span></span> <span data-ttu-id="b5a0b-160">Należy pamiętać, że wiele zakresów może punktu toohello sama baza danych i rozłączne zakresy są obsługiwane (np. [100,200) i [400,600) zarówno tooDatabase punktu C w poniższym przykładzie hello.)</span><span class="sxs-lookup"><span data-stu-id="b5a0b-160">Note that multiple ranges can point toohello same database, and disjoint ranges are supported (e.g., [100,200) and [400,600) both point tooDatabase C in hello example below.)</span></span>

| <span data-ttu-id="b5a0b-161">Klucz</span><span class="sxs-lookup"><span data-stu-id="b5a0b-161">Key</span></span> | <span data-ttu-id="b5a0b-162">Identyfikator niezależnego fragmentu lokalizacji</span><span class="sxs-lookup"><span data-stu-id="b5a0b-162">Shard Location</span></span> |
| --- | --- |
| <span data-ttu-id="b5a0b-163">[1,50)</span><span class="sxs-lookup"><span data-stu-id="b5a0b-163">[1,50)</span></span> |<span data-ttu-id="b5a0b-164">Database_A</span><span class="sxs-lookup"><span data-stu-id="b5a0b-164">Database_A</span></span> |
| <span data-ttu-id="b5a0b-165">[50,100)</span><span class="sxs-lookup"><span data-stu-id="b5a0b-165">[50,100)</span></span> |<span data-ttu-id="b5a0b-166">Database_B</span><span class="sxs-lookup"><span data-stu-id="b5a0b-166">Database_B</span></span> |
| <span data-ttu-id="b5a0b-167">[100,200)</span><span class="sxs-lookup"><span data-stu-id="b5a0b-167">[100,200)</span></span> |<span data-ttu-id="b5a0b-168">Database_C</span><span class="sxs-lookup"><span data-stu-id="b5a0b-168">Database_C</span></span> |
| <span data-ttu-id="b5a0b-169">[400,600)</span><span class="sxs-lookup"><span data-stu-id="b5a0b-169">[400,600)</span></span> |<span data-ttu-id="b5a0b-170">Database_C</span><span class="sxs-lookup"><span data-stu-id="b5a0b-170">Database_C</span></span> |
| <span data-ttu-id="b5a0b-171">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="b5a0b-171">...</span></span> |<span data-ttu-id="b5a0b-172">Przyciski ...</span><span class="sxs-lookup"><span data-stu-id="b5a0b-172">...</span></span> |

<span data-ttu-id="b5a0b-173">Każdej z tabel hello pokazanym powyżej to przykład koncepcyjnej **ShardMap** obiektu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-173">Each of hello tables shown above is a conceptual example of a **ShardMap** object.</span></span> <span data-ttu-id="b5a0b-174">Każdy wiersz jest uproszczony przykład osoba **PointMapping** (dla mapy niezależnego fragmentu listy hello) lub **RangeMapping** (dla mapy niezależnego fragmentu zakresu hello) obiektu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-174">Each row is a simplified example of an individual **PointMapping** (for hello list shard map) or **RangeMapping** (for hello range shard map) object.</span></span>

## <a name="shard-map-manager"></a><span data-ttu-id="b5a0b-175">Menedżer mapy niezależnego fragmentu</span><span class="sxs-lookup"><span data-stu-id="b5a0b-175">Shard map manager</span></span>
<span data-ttu-id="b5a0b-176">W bibliotece klienta hello hello niezależnego fragmentu mapy Menedżer jest kolekcja map niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-176">In hello client library, hello shard map  manager is a collection of shard maps.</span></span> <span data-ttu-id="b5a0b-177">Witaj danych zarządzanych przez **ShardMapManager** wystąpienia jest przechowywany w trzech miejscach:</span><span class="sxs-lookup"><span data-stu-id="b5a0b-177">hello data managed by a **ShardMapManager** instance is kept in three places:</span></span> 

1. <span data-ttu-id="b5a0b-178">**Globalne mapy niezależnego fragmentu (GSM)**: Określ tooserve bazy danych jako repozytorium powitania dla wszystkich map niezależnego fragmentu i mapowania.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-178">**Global Shard Map (GSM)**: You specify a database tooserve as hello repository for all of its shard maps and mappings.</span></span> <span data-ttu-id="b5a0b-179">Specjalne tabele i procedury składowane są tworzone automatycznie toomanage hello informacji.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-179">Special tables and stored procedures are automatically created toomanage hello information.</span></span> <span data-ttu-id="b5a0b-180">Zazwyczaj jest mała baza danych, a lekkim dostępne i nie powinna być używana na potrzeby innych aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-180">This is typically a small database and lightly accessed, and it should not be used for other needs of hello application.</span></span> <span data-ttu-id="b5a0b-181">Witaj tabele są w schemacie specjalne o nazwie **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-181">hello tables are in a special schema named **__ShardManagement**.</span></span> 
2. <span data-ttu-id="b5a0b-182">**Lokalny identyfikator niezależnego fragmentu mapy (LSM) tak**: każdej bazy danych, który określisz toobe niezależnego fragmentu jest zmodyfikowany toocontain kilka tabel małe i specjalnych procedur składowanych, zawierające i zarządzanie niezależnych toothat określonych informacji mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-182">**Local Shard Map (LSM)**: Every database that you specify toobe a shard is modified toocontain several small tables and special stored procedures that contain and manage shard map information specific toothat shard.</span></span> <span data-ttu-id="b5a0b-183">Te informacje są nadmiarowe informacje hello w hello GSM, i udostępnia informacje o mapy niezależnego fragmentu toovalidate w pamięci podręcznej aplikacji hello bez wprowadzania żadnych obciążenia na powitania GSM; Aplikacja Hello używa hello LSM toodetermine mapowanie pamięci podręcznej jest nadal ważny.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-183">This information is redundant with hello information in hello GSM, and it allows hello application toovalidate cached shard map information without placing any load on hello GSM; hello application uses hello LSM toodetermine if a cached mapping is still valid.</span></span> <span data-ttu-id="b5a0b-184">Hello tabele odpowiedniego toohello LSM na każdym niezależnego fragmentu są również w schemacie hello **__ShardManagement**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-184">hello tables corresponding toohello LSM on each shard are also in hello schema **__ShardManagement**.</span></span>
3. <span data-ttu-id="b5a0b-185">**Pamięci podręcznej aplikacji**: każda aplikacja wystąpienia dostęp do **ShardMapManager** obiekt zachowuje lokalnej pamięci podręcznej w pamięci z jego mapowanie.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-185">**Application cache**: Each application instance accessing a **ShardMapManager** object maintains a local in-memory cache of its mappings.</span></span> <span data-ttu-id="b5a0b-186">Przechowuje informacje routingu, która została ostatnio pobrana.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-186">It stores routing information that has recently been retrieved.</span></span> 

## <a name="constructing-a-shardmapmanager"></a><span data-ttu-id="b5a0b-187">Konstruowanie ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="b5a0b-187">Constructing a ShardMapManager</span></span>
<span data-ttu-id="b5a0b-188">A **ShardMapManager** obiekt jest tworzony przy użyciu [fabryki](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) wzorca.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-188">A **ShardMapManager** object is constructed using a [factory](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) pattern.</span></span> <span data-ttu-id="b5a0b-189">Witaj  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  metoda przyjmuje poświadczenia (w tym hello nazwy serwera i bazy danych zawierający hello GSM) w formie hello  **ConnectionString** i zwraca wystąpienie klasy **ShardMapManager**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-189">hello **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** method takes credentials (including hello server name and database name holding hello GSM) in hello form of a **ConnectionString** and returns an instance of a **ShardMapManager**.</span></span>  

<span data-ttu-id="b5a0b-190">**Uwaga:** hello **ShardMapManager** były tworzone tylko raz dla domeny aplikacji w ramach hello kodu inicjowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-190">**Please Note:** hello **ShardMapManager** should be instantiated only once per app domain, within hello initialization code for an application.</span></span> <span data-ttu-id="b5a0b-191">Tworzenie wystąpień dodatkowe ShardMapManager w hello tego samego elementu appdomain, wynikiem będzie znacznie większą ilość pamięci i procesora aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-191">Creation of additional instances of ShardMapManager in hello same appdomain, will result in increased memory and CPU utilization of hello application.</span></span> <span data-ttu-id="b5a0b-192">A **ShardMapManager** może zawierać dowolną liczbę niezależnych mapy.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-192">A **ShardMapManager** can contain any number of shard maps.</span></span> <span data-ttu-id="b5a0b-193">Mapa jednego niezależnego fragmentu może być wystarczające dla wielu aplikacji, istnieją momenty, gdy różne zestawy baz danych są używane do innego schematu lub do celów unikatowe; w takich przypadkach może być preferowana wielu map niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-193">While a single shard map may be sufficient for many applications, there are times when different sets of databases are used for different schema or for unique purposes; in those cases multiple shard maps may be preferable.</span></span> 

<span data-ttu-id="b5a0b-194">W tym kodzie aplikacja próbuje tooopen istniejące **ShardMapManager** z hello [metody TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-194">In this code, an application tries tooopen an existing **ShardMapManager** with hello [TryGetSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).</span></span>  <span data-ttu-id="b5a0b-195">Jeśli obiekty reprezentujące Global **ShardMapManager** (GSM) nie zostały jeszcze istnieje wewnątrz hello bazy danych, powitania klienta biblioteki tworzy je tam przy użyciu hello [metody CreateSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-195">If objects representing a Global **ShardMapManager** (GSM) do not yet exist inside hello database, hello client library creates them there using hello [CreateSqlShardMapManager method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).</span></span>

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
    // If it doesn't already exist, then create it. 
    ShardMapManager shardMapManager; 
    bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

    if (shardMapManagerExists) 
     { 
        Console.WriteLine("Shard Map Manager already exists");
    } 
    else
    {
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

<span data-ttu-id="b5a0b-196">Alternatywnie można użyć programu Powershell toocreate nowego Menedżera mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-196">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="b5a0b-197">Przykład jest dostępny [tutaj](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-197">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="get-a-rangeshardmap-or-listshardmap"></a><span data-ttu-id="b5a0b-198">Pobierz RangeShardMap lub ListShardMap</span><span class="sxs-lookup"><span data-stu-id="b5a0b-198">Get a RangeShardMap or ListShardMap</span></span>
<span data-ttu-id="b5a0b-199">Po utworzeniu niezależnych menedżera map, możesz uzyskać hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) lub [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) przy użyciu hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), lub hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) metody.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-199">After creating a shard map manager, you can get hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) using hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method.</span></span>

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a><span data-ttu-id="b5a0b-200">Poświadczenia administrowania niezależnego fragmentu mapy</span><span class="sxs-lookup"><span data-stu-id="b5a0b-200">Shard map administration credentials</span></span>
<span data-ttu-id="b5a0b-201">Aplikacje, które administrowania i manipulowania mapy niezależnego fragmentu różnią się od tych, które korzystają z połączeń tooroute mapy niezależnego fragmentu hello.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-201">Applications that administer and manipulate shard maps are different from those that use hello shard maps tooroute connections.</span></span> 

<span data-ttu-id="b5a0b-202">mapuje tooadminister niezależnego fragmentu (Dodawanie lub zmienianie odłamków, mapy niezależnego fragmentu, niezależnego fragmentu mapowania, itp.) musi utworzyć wystąpienia hello **ShardMapManager** przy użyciu **poświadczenia, które mają uprawnienia w bazie danych zarówno hello GSM i na każdym odczytu/zapisu bazy danych, która służy jako identyfikator niezależnego fragmentu**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-202">tooadminister shard maps (add or change shards, shard maps, shard mappings, etc.) you must instantiate hello **ShardMapManager** using **credentials that have read/write privileges on both hello GSM database and on each database that serves as a shard**.</span></span> <span data-ttu-id="b5a0b-203">poświadczenia Hello muszą zezwalać na dla operacji zapisu dla tabel hello w obu hello GSM i LSM niezależnego fragmentu mapy informacji jest wprowadzona lub zmienić również podobnie jak w przypadku tworzenia tabel LSM na nowych fragmentów.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-203">hello credentials must allow for writes against hello tables in both hello GSM and LSM as shard map information is entered or changed, as well as for creating LSM tables on new shards.</span></span>  

<span data-ttu-id="b5a0b-204">Zobacz [poświadczenia używane biblioteki klienta elastycznej bazy danych hello tooaccess](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-204">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

### <a name="only-metadata-affected"></a><span data-ttu-id="b5a0b-205">Tylko metadane, których to dotyczy</span><span class="sxs-lookup"><span data-stu-id="b5a0b-205">Only metadata affected</span></span>
<span data-ttu-id="b5a0b-206">Metody używane do zapełniania lub zmiany hello **ShardMapManager** danych nie należy zmieniać hello dane użytkownika przechowywane w odłamków hello, samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-206">Methods used for populating or changing hello **ShardMapManager** data do not alter hello user data stored in hello shards themselves.</span></span> <span data-ttu-id="b5a0b-207">Na przykład metod, takich jak **CreateShard**, **DeleteShard**, **UpdateMapping**, itd. wpływa na powitania niezależnego fragmentu mapy zawierają tylko metadane.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-207">For example, methods such as **CreateShard**, **DeleteShard**, **UpdateMapping**, etc. affect hello shard map metadata only.</span></span> <span data-ttu-id="b5a0b-208">Nie należy usuwać, Dodaj lub alter użytkownika dane zawarte w odłamków hello.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-208">They do not remove, add, or alter user data contained in hello shards.</span></span> <span data-ttu-id="b5a0b-209">Jednak te metody są zaprojektowane toobe używane w połączeniu z oddzielnych Przeprowadź toocreate lub usunąć rzeczywiste bazy danych lub ten ruch wiersze z tabeli toorebalance tooanother jednego niezależnego fragmentu podzielonej środowiska.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-209">Instead, these methods are designed toobe used in conjunction with separate operations you perform toocreate or remove actual databases, or that move rows from one shard tooanother toorebalance a sharded environment.</span></span>  <span data-ttu-id="b5a0b-210">(hello **scalania podziału** narzędzia dołączonego do narzędzi elastycznej bazy danych korzysta z poniższych interfejsów API oraz organizowanie rzeczywiste przeniesienie danych między odłamków.) Zobacz [skalowania, za pomocą narzędzia hello scalanie podziału elastycznej bazy danych](sql-database-elastic-scale-overview-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-210">(hello **split-merge** tool included with elastic database tools makes use of these APIs along with orchestrating actual data movement between shards.) See [Scaling using hello Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).</span></span>

## <a name="populating-a-shard-map-example"></a><span data-ttu-id="b5a0b-211">Wypełnianie przykład mapy niezależnego fragmentu</span><span class="sxs-lookup"><span data-stu-id="b5a0b-211">Populating a shard map example</span></span>
<span data-ttu-id="b5a0b-212">Poniżej przedstawiono przykład sekwencji operacji toopopulate mapy określonych niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-212">An example sequence of operations toopopulate a specific shard map is shown below.</span></span> <span data-ttu-id="b5a0b-213">Kod Hello wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b5a0b-213">hello code performs these steps:</span></span> 

1. <span data-ttu-id="b5a0b-214">Nowej mapy niezależnego fragmentu jest tworzony w ramach menedżera map niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-214">A new shard map is created within a shard map manager.</span></span> 
2. <span data-ttu-id="b5a0b-215">Witaj metadanych dla dwóch różnych odłamków jest dodawany toohello niezależnego fragmentu mapy.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-215">hello metadata for two different shards is added toohello shard map.</span></span> 
3. <span data-ttu-id="b5a0b-216">Różnych mapowań klucza zakresu zostaną dodane, a hello ogólną mapy niezależnego fragmentu hello jest wyświetlana zawartość.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-216">A variety of key range mappings are added, and hello overall contents of hello shard map are displayed.</span></span> 

<span data-ttu-id="b5a0b-217">Kod Hello jest zapisywany tak, aby metody hello można uruchomić ponownie, jeśli wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-217">hello code is written so that hello method can be rerun if an error occurs.</span></span> <span data-ttu-id="b5a0b-218">Każde żądanie sprawdza, czy identyfikator niezależnego fragmentu lub mapowanie już istnieje, przed podjęciem próby wykonania toocreate go.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-218">Each request tests whether a shard or mapping already exists, before attempting toocreate it.</span></span> <span data-ttu-id="b5a0b-219">Witaj kodu zakłada, że bazy danych o nazwie **sample_shard_0**, **sample_shard_1** i **sample_shard_2** zostały już utworzone na serwerze hello odwołuje się ciąg **shardServer**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-219">hello code assumes that databases named **sample_shard_0**, **sample_shard_1** and **sample_shard_2** have already been created in hello server referenced by string **shardServer**.</span></span> 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

<span data-ttu-id="b5a0b-220">Jak można użyć programu PowerShell zamiast skryptów tooachieve hello spowodować takie same.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-220">As an alternative you can use PowerShell scripts tooachieve hello same result.</span></span> <span data-ttu-id="b5a0b-221">Dostępne są niektóre przykłady z programu PowerShell próbki hello [tutaj](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-221">Some of hello sample PowerShell examples are available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>     

<span data-ttu-id="b5a0b-222">Po mapy niezależnego fragmentu są wypełnione, aplikacje dostępu do danych można utworzyć lub dostosowywane toowork przy użyciu map hello.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-222">Once shard maps have been populated, data access applications can be created or adapted toowork with hello maps.</span></span> <span data-ttu-id="b5a0b-223">Wypełnianie lub manipulowanie mapy hello muszą wystąpić ponownie dopiero **mapę układu** musi toochange.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-223">Populating or manipulating hello maps need not occur again until **map layout** needs toochange.</span></span>  

## <a name="data-dependent-routing"></a><span data-ttu-id="b5a0b-224">Routing zależny od danych</span><span class="sxs-lookup"><span data-stu-id="b5a0b-224">Data dependent routing</span></span>
<span data-ttu-id="b5a0b-225">Hello niezależnego fragmentu Mapa Menedżera będzie najbardziej używany w aplikacji, które wymagają bazy danych połączenia tooperform hello dane specyficzne dla aplikacji operacji.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-225">hello shard map manager will be most used in applications that require database connections tooperform hello app-specific data operations.</span></span> <span data-ttu-id="b5a0b-226">Te połączenia musi być skojarzony z hello poprawną bazą danych.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-226">Those connections must be associated with hello correct database.</span></span> <span data-ttu-id="b5a0b-227">Jest to nazywane **danych zależnych routingu**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-227">This is known as **Data Dependent Routing**.</span></span> <span data-ttu-id="b5a0b-228">W przypadku tych aplikacji wystąpienia obiekt menedżera niezależnego fragmentu mapy z fabryki hello przy użyciu poświadczeń, które mają dostęp tylko do odczytu w bazie danych GSM hello.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-228">For these applications, instantiate a shard map manager object from hello factory using credentials that have read-only access on hello GSM database.</span></span> <span data-ttu-id="b5a0b-229">Poszczególnych żądań w połączeniach nowszej Podaj poświadczenia niezbędne do łączenia toohello odpowiedni identyfikator niezależnego fragmentu w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-229">Individual requests for later connections supply credentials necessary for connecting toohello appropriate shard database.</span></span>

<span data-ttu-id="b5a0b-230">Należy pamiętać, że te aplikacje (przy użyciu **ShardMapManager** otwarty przy użyciu poświadczeń tylko do odczytu) nie można wprowadzić zmiany mapy toohello lub mapowania.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-230">Note that these applications (using **ShardMapManager** opened with read-only credentials) cannot make changes toohello maps or mappings.</span></span> <span data-ttu-id="b5a0b-231">W przypadku tych potrzeb utworzyć administracyjne dotyczące aplikacji i skryptów programu PowerShell, zapewniających poświadczenia z niskimi uprawnieniami, zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-231">For those needs, create administrative-specific applications or PowerShell scripts that supply higher-privileged credentials as discussed earlier.</span></span> <span data-ttu-id="b5a0b-232">Zobacz [poświadczenia używane biblioteki klienta elastycznej bazy danych hello tooaccess](sql-database-elastic-scale-manage-credentials.md).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-232">See [Credentials used tooaccess hello Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span>

<span data-ttu-id="b5a0b-233">Aby uzyskać więcej informacji, zobacz [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-233">For more details, see [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> 

## <a name="modifying-a-shard-map"></a><span data-ttu-id="b5a0b-234">Modyfikowanie mapy niezależnego fragmentu</span><span class="sxs-lookup"><span data-stu-id="b5a0b-234">Modifying a shard map</span></span>
<span data-ttu-id="b5a0b-235">Mapa niezależnych można zmienić na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-235">A shard map can be changed in different ways.</span></span> <span data-ttu-id="b5a0b-236">Modyfikowanie wszystkich hello następujące metody hello metadane opisujące odłamków hello i ich mapowania, ale ich nie należy fizycznie modyfikować danych w ramach odłamków hello ani ich tworzyć ani nie usuwaj hello rzeczywiste baz danych.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-236">All of hello following methods modify hello metadata describing hello shards and their mappings, but they do not physically modify data within hello shards, nor do they create or delete hello actual databases.</span></span>  <span data-ttu-id="b5a0b-237">Niektóre operacje hello na mapie niezależnego fragmentu hello opisanych poniżej może być konieczne toobe skoordynować z działania administracyjne, które fizycznie przenieść dane lub dodać i usunąć bazy danych służy jako niezależne.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-237">Some of hello operations on hello shard map described below may need toobe coordinated with administrative actions that physically move data or that add and remove databases serving as shards.</span></span>

<span data-ttu-id="b5a0b-238">Te metody współpracują ze sobą jako bloków konstrukcyjnych hello dostępne modyfikowania hello ogólną rozkład danych w środowisku podzielonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-238">These methods work together as hello building blocks available for modifying hello overall distribution of data in your sharded database environment.</span></span>  

* <span data-ttu-id="b5a0b-239">tooadd lub usuń odłamków: Użyj  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  i  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  z hello [Shardmap klasy](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-239">tooadd or remove shards: use **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)** and **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)** of hello [Shardmap class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx).</span></span> 
  
    <span data-ttu-id="b5a0b-240">Witaj serwera i reprezentujący hello docelowy identyfikator niezależnego fragmentu bazy danych musi już istnieć dla tooexecute te operacje.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-240">hello server and database representing hello target shard must already exist for these operations tooexecute.</span></span> <span data-ttu-id="b5a0b-241">Te metody nie mają wpływu na powitania baz danych, tylko na metadanych w mapie niezależnego fragmentu hello.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-241">These methods do not have any impact on hello databases themselves, only on metadata in hello shard map.</span></span>
* <span data-ttu-id="b5a0b-242">toocreate lub usuwanie punktów lub zakresy, które są mapowane odłamków toohello: Użyj  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  z hello [Klasy RangeShardMapping](https://msdn.microsoft.com/library/azure/dn807318.aspx), i  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  z hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span><span class="sxs-lookup"><span data-stu-id="b5a0b-242">toocreate or remove points or ranges that are mapped toohello shards: use **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**, **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)** of hello [RangeShardMapping class](https://msdn.microsoft.com/library/azure/dn807318.aspx), and **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)** of hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)</span></span>
  
    <span data-ttu-id="b5a0b-243">Wiele różnych punktach lub zakresy mogą być mapowane toohello sam identyfikator niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-243">Many different points or ranges can be mapped toohello same shard.</span></span> <span data-ttu-id="b5a0b-244">Te metody mają wpływ tylko na metadanych — nie wpływają na dane, które mogą już być obecne w fragmentów.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-244">These methods only affect metadata - they do not affect any data that may already be present in shards.</span></span> <span data-ttu-id="b5a0b-245">Jeśli dane wymagają toobe usunięte z bazy danych hello w kolejności toobe zgodne z **DeleteMapping** operacje, konieczne będzie tooperform te operacje oddzielnie, ale w połączeniu z przy użyciu tych metod.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-245">If data needs toobe removed from hello database in order toobe consistent with **DeleteMapping** operations, you will need tooperform those operations separately but in conjunction with using these methods.</span></span>  
* <span data-ttu-id="b5a0b-246">toosplit istniejących zakresów do dwóch lub scalania sąsiadujących zakresów w jednym: Użyj  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  i  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-246">toosplit existing ranges into two, or merge adjacent ranges into one: use **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)** and **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.</span></span>  
  
    <span data-ttu-id="b5a0b-247">Należy pamiętać, że dzielenie i scalanie operacji **nie należy zmieniać klucza toowhich niezależnego fragmentu hello wartości są mapowane**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-247">Note that split and merge operations **do not change hello shard toowhich key values are mapped**.</span></span> <span data-ttu-id="b5a0b-248">Podział dzieli istniejący zakres na dwie części, ale pozostawia zarówno jako toohello mapowane sam identyfikator niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-248">A split breaks an existing range into two parts, but leaves both as mapped toohello same shard.</span></span> <span data-ttu-id="b5a0b-249">Scalanie działa na dwóch sąsiadujących zakresów, które są już mapowane toohello sam identyfikator niezależnego fragmentu, łączenie ich do jednego zakresu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-249">A merge operates on two adjacent ranges that are already mapped toohello same shard, coalescing them into a single range.</span></span>  <span data-ttu-id="b5a0b-250">Witaj przepływu punkty lub zakresy się między odłamków musi toobe koordynowane przy użyciu **UpdateMapping** w połączeniu z rzeczywiste przeniesienie danych.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-250">hello movement of points or ranges themselves between shards needs toobe coordinated by using **UpdateMapping** in conjunction with actual data movement.</span></span>  <span data-ttu-id="b5a0b-251">Można użyć hello **podziału/Merge** usługi, która jest częścią elastycznej bazy danych narzędzi toocoordinate niezależnego fragmentu mapy zmian z przepływu danych, gdy potrzebny jest przepływu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-251">You can use hello **Split/Merge** service that is part of elastic database tools toocoordinate shard map changes with data movement, when movement is needed.</span></span> 
* <span data-ttu-id="b5a0b-252">Mapa toore (lub Przenieś) poszczególnych punktów lub zakresy toodifferent odłamków: Użyj  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-252">toore-map (or move) individual points or ranges toodifferent shards: use **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.</span></span>  
  
    <span data-ttu-id="b5a0b-253">Ponieważ danych może być konieczne toobe przeniesione z jednego niezależnego fragmentu tooanother w kolejności toobe zgodne z **UpdateMapping** operacji, konieczne będzie tooperform tego przepływu oddzielnie, ale w połączeniu z przy użyciu tych metod.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-253">Since data may need toobe moved from one shard tooanother in order toobe consistent with **UpdateMapping** operations, you will need tooperform that movement separately but in conjunction with using these methods.</span></span>
* <span data-ttu-id="b5a0b-254">mapowania tootake online i offline: Użyj  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  i  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello stan online mapowania.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-254">tootake mappings online and offline: use **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)** and **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)** toocontrol hello online state of a mapping.</span></span> 
  
    <span data-ttu-id="b5a0b-255">Niektóre operacje na niezależnego fragmentu mapowania są dozwolone tylko podczas mapowania jest w stanie "offline", w tym **UpdateMapping** i **DeleteMapping**.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-255">Certain operations on shard mappings are only allowed when a mapping is in an “offline” state, including **UpdateMapping** and **DeleteMapping**.</span></span> <span data-ttu-id="b5a0b-256">Podczas mapowania jest w trybie offline, żądanie zależne od danych oparte na kluczu zawarte w tym mapowania spowoduje zwrócenie błędu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-256">When a mapping is offline, a data-dependent request based on a key included in that mapping will return an error.</span></span> <span data-ttu-id="b5a0b-257">Ponadto gdy zakres jest najpierw przełączona w tryb offline, wszystkie niezależnych toohello dotyczy połączeń są automatycznie skasowane w kolejności wyniki niespójne lub niekompletne tooprevent zapytań skierowanej zakresy zmieniane.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-257">In addition, when a range is first taken offline, all connections toohello affected shard are automatically killed in order tooprevent inconsistent or incomplete results for queries directed against ranges being changed.</span></span> 

<span data-ttu-id="b5a0b-258">Mapowania są niezmienne obiekty w środowisku .net.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-258">Mappings are immutable objects in .Net.</span></span>  <span data-ttu-id="b5a0b-259">Wszystkie metody hello powyżej, które spowodują zmianę mapowania również unieważnienie toothem żadnych odwołań w kodzie.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-259">All of hello methods above that change mappings also invalidate any references toothem in your code.</span></span> <span data-ttu-id="b5a0b-260">toomake it łatwiejsze tooperform sekwencji działań, które spowodują zmianę stanu mapowania, wszystkie metody hello, które spowodują zmianę mapowania zwrócić nowe mapowanie odwołania, co operacje można powiązać.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-260">toomake it easier tooperform sequences of operations that change a mapping’s state, all of hello methods that change a mapping return a new mapping reference, so operations can be chained.</span></span> <span data-ttu-id="b5a0b-261">Na przykład toodelete istniejące mapowanie w sm shardmap, który zawiera klucz hello 25, można wykonywać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="b5a0b-261">For example, toodelete an existing mapping in shardmap sm that contains hello key 25, you can execute hello following:</span></span> 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a><span data-ttu-id="b5a0b-262">Dodawanie niezależnego fragmentu</span><span class="sxs-lookup"><span data-stu-id="b5a0b-262">Adding a shard</span></span>
<span data-ttu-id="b5a0b-263">Aplikacje często wymagają toosimply dodać nowe dane toohandle odłamków oczekuje się od nowych kluczy lub kluczy zakresów, mapy niezależnego fragmentu, która już istnieje.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-263">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="b5a0b-264">Na przykład aplikację podzielonej na podstawie Identyfikatora dzierżawcy może być konieczne tooprovision nowy identyfikator niezależnego fragmentu dla nowej dzierżawy lub co miesiąc podzielonej danych może być konieczne nowy identyfikator niezależnego fragmentu udostępnione przed rozpoczęciem powitalne każdego nowego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-264">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="b5a0b-265">Jeśli hello nowy zakres wartości kluczy nie jest już częścią istniejące mapowanie i nie przenoszenia danych jest to konieczne, jest bardzo prosty tooadd hello nowy identyfikator niezależnego fragmentu i Skojarz nowy klucz hello lub fragmentacji toothat zakresu.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-265">If hello new range of key values is not already part of an existing mapping and no data movement is necessary, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> <span data-ttu-id="b5a0b-266">Aby uzyskać więcej informacji na temat dodawania nowych fragmentów, zobacz [Dodawanie nowych niezależnego fragmentu](sql-database-elastic-scale-add-a-shard.md).</span><span class="sxs-lookup"><span data-stu-id="b5a0b-266">For details on adding new shards, see [Adding a new shard](sql-database-elastic-scale-add-a-shard.md).</span></span>

<span data-ttu-id="b5a0b-267">W scenariuszach, wymagających przenoszenia danych jednak narzędzie scalania podziału hello jest wymagane tooorchestrate przenoszenia danych hello między odłamków w połączeniu z hello niezbędne niezależnych mapy aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="b5a0b-267">For scenarios that require data movement, however, hello split-merge tool is needed tooorchestrate hello data movement between shards in combination with hello necessary shard map updates.</span></span> <span data-ttu-id="b5a0b-268">Aby uzyskać szczegółowe informacje o wykorzystaniu hello yool scalania podziału, zobacz [omówienie scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="b5a0b-268">For details on using hello split-merge yool, see [Overview of split-merge](sql-database-elastic-scale-overview-split-and-merge.md)</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
