---
title: "Elastyczne bazy danych narzędzia słownik | Dokumentacja firmy Microsoft"
description: "Wyjaśnienie pojęcia dotyczące narzędzi elastycznej bazy danych"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 0fda4bb948bbed1c14d468519ba67cce9bc4e6c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="caa0c-103">Elastyczne słownik Narzędzia bazy danych</span><span class="sxs-lookup"><span data-stu-id="caa0c-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="caa0c-104">Poniższe terminy są definiowane dla [narzędzi elastycznej bazy danych](sql-database-elastic-scale-introduction.md), funkcja bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="caa0c-104">The following terms are defined for the [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="caa0c-105">Narzędzia są używane do zarządzania [mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md)i obejmują [biblioteki klienta](sql-database-elastic-database-client-library.md), [narzędzia do scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md), [pule elastyczne](sql-database-elastic-pool.md)i [zapytania](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="caa0c-105">The tools are used to manage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include the [client library](sql-database-elastic-database-client-library.md), the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="caa0c-106">Te terminy są używane w [Dodawanie niezależnych, za pomocą narzędzi elastycznej bazy danych](sql-database-elastic-scale-add-a-shard.md) i [za pomocą klasy RecoveryManager rozwiązywania problemów mapy niezależnego fragmentu](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="caa0c-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Elastyczne warunki skali][1]

<span data-ttu-id="caa0c-108">**Baza danych**: baza danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="caa0c-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="caa0c-109">**Routing zależnych danych**: włącza aplikację do nawiązania połączenia niezależnych danego klucza dzielenia na fragmenty określonych funkcji.</span><span class="sxs-lookup"><span data-stu-id="caa0c-109">**Data dependent routing**: The functionality that enables an application to connect to a shard given a specific sharding key.</span></span> <span data-ttu-id="caa0c-110">Zobacz [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="caa0c-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="caa0c-111">Porównaj z  **[zapytania wielu niezależnych](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="caa0c-111">Compare to **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="caa0c-112">**Globalny identyfikator niezależnego fragmentu mapy**: mapy między dzielenia na fragmenty kluczy i ich odpowiednich fragmentów w **zestaw niezależnych**.</span><span class="sxs-lookup"><span data-stu-id="caa0c-112">**Global shard map**: The map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="caa0c-113">Mapy niezależnych globalne są przechowywane w **menedżera map niezależnego fragmentu**.</span><span class="sxs-lookup"><span data-stu-id="caa0c-113">The global shard map is stored in the **shard map manager**.</span></span> <span data-ttu-id="caa0c-114">Porównaj z **mapy lokalnego niezależnych**.</span><span class="sxs-lookup"><span data-stu-id="caa0c-114">Compare to **local shard map**.</span></span>

<span data-ttu-id="caa0c-115">**Lista niezależnych mapy**: mapy niezależnego fragmentu, w których dzielenia na fragmenty klucze są mapowane pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="caa0c-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="caa0c-116">Porównaj z **niezależnego fragmentu Map zakres**.</span><span class="sxs-lookup"><span data-stu-id="caa0c-116">Compare to **Range Shard Map**.</span></span>   

<span data-ttu-id="caa0c-117">**Mapa lokalnych niezależnych**: przechowywane na niezależnego fragmentu, mapa lokalnych niezależnego fragmentu zawiera mapowania dla shardlets, który znajduje się na niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="caa0c-117">**Local shard map**: Stored on a shard, the local shard map contains mappings for the shardlets that reside on the shard.</span></span>

<span data-ttu-id="caa0c-118">**Wiele niezależnych zapytania**: mógł wystawiać zapytanie wielu odłamków; zestawy wyników są zwracane, używając semantyki UNION ALL (znanej także jako "rozdysponowywania zapytania").</span><span class="sxs-lookup"><span data-stu-id="caa0c-118">**Multi-shard query**: The ability to issue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="caa0c-119">Porównaj z **danych zależnych routingu**.</span><span class="sxs-lookup"><span data-stu-id="caa0c-119">Compare to **data dependent routing**.</span></span>

<span data-ttu-id="caa0c-120">**Wielodostępne** i **pojedynczej dzierżawy**: Pokazuje dzierżawy pojedynczej bazy danych i bazy danych wielu dzierżawców:</span><span class="sxs-lookup"><span data-stu-id="caa0c-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Bazy danych jednym i wieloma dzierżawcami](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="caa0c-122">Oto reprezentację **podzielonej** jednym i wieloma dzierżawcami baz danych.</span><span class="sxs-lookup"><span data-stu-id="caa0c-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Bazy danych jednym i wieloma dzierżawcami](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="caa0c-124">**Zakres niezależnych mapy**: mapy niezależnego fragmentu, w którym strategii dystrybucji niezależnego fragmentu opiera się na różnych zakresów wartości ciągłe.</span><span class="sxs-lookup"><span data-stu-id="caa0c-124">**Range shard map**: A shard map in which the shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="caa0c-125">**Tabele odwołań dla**: tabel, które nie są podzielonej, ale są replikowane między fragmentów.</span><span class="sxs-lookup"><span data-stu-id="caa0c-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="caa0c-126">Na przykład kodów pocztowych mogą być przechowywane w tabeli odniesienia.</span><span class="sxs-lookup"><span data-stu-id="caa0c-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="caa0c-127">**Identyfikator niezależnego fragmentu**: bazy danych SQL Azure, która przechowuje dane z zestawu danych podzielonej.</span><span class="sxs-lookup"><span data-stu-id="caa0c-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="caa0c-128">**Elastyczność niezależnego fragmentu**: możliwość wykonywania zarówno **skalowanie w poziomie** i **skalowanie w pionie**.</span><span class="sxs-lookup"><span data-stu-id="caa0c-128">**Shard elasticity**: The ability to perform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="caa0c-129">**Tabele podzielonej**: tabele, które są podzielonej, tj., których danych jest rozłożona odłamków na podstawie ich wartości klucza dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="caa0c-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="caa0c-130">**Klucz dzielenia na fragmenty**: wartość kolumny, która określa, jak dane są przesyłane między fragmentów.</span><span class="sxs-lookup"><span data-stu-id="caa0c-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="caa0c-131">Typ wartości może być jedną z następujących: **int**, **bigint**, **varbinary**, lub **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="caa0c-131">The value type can be one of the following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="caa0c-132">**Zestaw niezależnych**: zbiór fragmentów, które są przypisane do tego samego mapy niezależnego fragmentu w Menedżerze mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="caa0c-132">**Shard set**: The collection of shards that are attributed to the same shard map in the shard map manager.</span></span>  

<span data-ttu-id="caa0c-133">**Shardlet**: wszystkie dane skojarzone z pojedynczą wartość klucz w niezależnych dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="caa0c-133">**Shardlet**: All of the data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="caa0c-134">Shardlet jest najmniejsza możliwa przenoszenie danych do rozpowszechniania podzielonej tabel.</span><span class="sxs-lookup"><span data-stu-id="caa0c-134">A shardlet is the smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="caa0c-135">**Mapa niezależnego fragmentu**: zestaw mapowań między dzielenia na fragmenty kluczy i ich odpowiednich fragmentów.</span><span class="sxs-lookup"><span data-stu-id="caa0c-135">**Shard map**: The set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="caa0c-136">**Menedżer mapy niezależnego fragmentu**: Zarządzanie obiektu i magazynu danych zawierającą poprzedzających niezależnego fragmentu map, lokalizacje niezależnego fragmentu i mapowania dla jednego lub więcej zestawów niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="caa0c-136">**Shard map manager**: A management object and data store that contains the shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Mapowania][2]

## <a name="verbs"></a><span data-ttu-id="caa0c-138">Zlecenia</span><span class="sxs-lookup"><span data-stu-id="caa0c-138">Verbs</span></span>
<span data-ttu-id="caa0c-139">**Skalowanie w poziomie**: polega na skalowanie w poziomie (lub w) kolekcja odłamków przez dodanie lub usunięcie fragmentów do mapy niezależnego fragmentu, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="caa0c-139">**Horizontal scaling**: The act of scaling out (or in) a collection of shards by adding or removing shards to a shard map, as shown below.</span></span>

![Skalowanie w poziomie i w pionie][3]

<span data-ttu-id="caa0c-141">**Scal**: polega na przenoszeniu shardlets z odłamków dwa na jeden identyfikator niezależnego fragmentu i odpowiednio aktualizowanie mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="caa0c-141">**Merge**: The act of moving shardlets from two shards to one shard and updating the shard map accordingly.</span></span>

<span data-ttu-id="caa0c-142">**Przenieś Shardlet**: act przenoszenia pojedynczego shardlet różnych niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="caa0c-142">**Shardlet move**: The act of moving a single shardlet to a different shard.</span></span> 

<span data-ttu-id="caa0c-143">**Identyfikator niezależnego fragmentu**: polega na poziomie partycjonowania identycznie strukturalnych danych między wieloma bazami danych oparte na kluczu dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="caa0c-143">**Shard**: The act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="caa0c-144">**Podziel**: polega na przenoszeniu shardlets kilka z jednego niezależnego fragmentu na inny identyfikator niezależnego fragmentu (zazwyczaj jest to nowy).</span><span class="sxs-lookup"><span data-stu-id="caa0c-144">**Split**: The act of moving several shardlets from one shard to another (typically new) shard.</span></span> <span data-ttu-id="caa0c-145">Klucz dzielenia na fragmenty są udostępniane przez użytkownika jako punkt podziału.</span><span class="sxs-lookup"><span data-stu-id="caa0c-145">A sharding key is provided by the user as the split point.</span></span>

<span data-ttu-id="caa0c-146">**Skalowanie w pionie**: polega na skalowanie w górę (lub w dół) poziom wydajności poszczególnych niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="caa0c-146">**Vertical Scaling**: The act of scaling up (or down) the performance level of an individual shard.</span></span> <span data-ttu-id="caa0c-147">Na przykład zmiana niezależnych zgodne ze standardem Premium (co powoduje więcej zasobów obliczeniowych).</span><span class="sxs-lookup"><span data-stu-id="caa0c-147">For example, changing a shard from Standard to Premium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

