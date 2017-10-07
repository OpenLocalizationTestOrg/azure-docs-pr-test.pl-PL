---
title: "Słownik Narzędzia bazy danych aaaElastic | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="5a068-103">Elastyczne słownik Narzędzia bazy danych</span><span class="sxs-lookup"><span data-stu-id="5a068-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="5a068-104">Witaj poniższe terminy są definiowane dla hello [narzędzi elastycznej bazy danych](sql-database-elastic-scale-introduction.md), funkcja bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5a068-104">hello following terms are defined for hello [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="5a068-105">Hello narzędzia są używane toomanage [mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md)i zawierają hello [biblioteki klienta](sql-database-elastic-database-client-library.md), hello [narzędzia do scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md), [pule elastyczne](sql-database-elastic-pool.md), i [zapytania](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a068-105">hello tools are used toomanage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include hello [client library](sql-database-elastic-database-client-library.md), hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="5a068-106">Te terminy są używane w [Dodawanie niezależnych, za pomocą narzędzi elastycznej bazy danych](sql-database-elastic-scale-add-a-shard.md) i [przy użyciu hello RecoveryManager klasy toofix niezależnego fragmentu mapy problemów](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5a068-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using hello RecoveryManager class toofix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Elastyczne warunki skali][1]

<span data-ttu-id="5a068-108">**Baza danych**: baza danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5a068-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="5a068-109">**Routing zależnych danych**: hello funkcje umożliwiające aplikacji niezależnego fragmentu tooa tooconnect danego klucza określonego dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="5a068-109">**Data dependent routing**: hello functionality that enables an application tooconnect tooa shard given a specific sharding key.</span></span> <span data-ttu-id="5a068-110">Zobacz [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="5a068-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="5a068-111">Porównywanie za**[zapytania wielu niezależnych](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="5a068-111">Compare too**[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="5a068-112">**Globalny identyfikator niezależnego fragmentu mapy**: mapy hello między dzielenia na fragmenty kluczy i ich odpowiednich fragmentów w **zestaw niezależnych**.</span><span class="sxs-lookup"><span data-stu-id="5a068-112">**Global shard map**: hello map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="5a068-113">mapy globalne niezależnych Hello są przechowywane w hello **menedżera map niezależnego fragmentu**.</span><span class="sxs-lookup"><span data-stu-id="5a068-113">hello global shard map is stored in hello **shard map manager**.</span></span> <span data-ttu-id="5a068-114">Porównywanie za**mapy lokalnego niezależnych**.</span><span class="sxs-lookup"><span data-stu-id="5a068-114">Compare too**local shard map**.</span></span>

<span data-ttu-id="5a068-115">**Lista niezależnych mapy**: mapy niezależnego fragmentu, w których dzielenia na fragmenty klucze są mapowane pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="5a068-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="5a068-116">Porównywanie za**mapy niezależnego fragmentu zakresu**.</span><span class="sxs-lookup"><span data-stu-id="5a068-116">Compare too**Range Shard Map**.</span></span>   

<span data-ttu-id="5a068-117">**Mapa lokalnych niezależnych**: przechowywane na niezależnego fragmentu, mapy niezależnych lokalne powitania zawiera mapowania dla shardlets hello, znajdującej się na powitania niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="5a068-117">**Local shard map**: Stored on a shard, hello local shard map contains mappings for hello shardlets that reside on hello shard.</span></span>

<span data-ttu-id="5a068-118">**Wiele niezależnych zapytania**: hello tooissue możliwości zapytanie wielu odłamków; zestawy wyników są zwracane, używając semantyki UNION ALL (znanej także jako "rozdysponowywania zapytania").</span><span class="sxs-lookup"><span data-stu-id="5a068-118">**Multi-shard query**: hello ability tooissue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="5a068-119">Porównywanie za**danych zależnych routingu**.</span><span class="sxs-lookup"><span data-stu-id="5a068-119">Compare too**data dependent routing**.</span></span>

<span data-ttu-id="5a068-120">**Wielodostępne** i **pojedynczej dzierżawy**: Pokazuje dzierżawy pojedynczej bazy danych i bazy danych wielu dzierżawców:</span><span class="sxs-lookup"><span data-stu-id="5a068-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Bazy danych jednym i wieloma dzierżawcami](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="5a068-122">Oto reprezentację **podzielonej** jednym i wieloma dzierżawcami baz danych.</span><span class="sxs-lookup"><span data-stu-id="5a068-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Bazy danych jednym i wieloma dzierżawcami](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="5a068-124">**Zakres niezależnych mapy**: mapy niezależnego fragmentu, w których hello strategii dystrybucji niezależnego fragmentu opiera się na różnych zakresów wartości ciągłe.</span><span class="sxs-lookup"><span data-stu-id="5a068-124">**Range shard map**: A shard map in which hello shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="5a068-125">**Tabele odwołań dla**: tabel, które nie są podzielonej, ale są replikowane między fragmentów.</span><span class="sxs-lookup"><span data-stu-id="5a068-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="5a068-126">Na przykład kodów pocztowych mogą być przechowywane w tabeli odniesienia.</span><span class="sxs-lookup"><span data-stu-id="5a068-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="5a068-127">**Identyfikator niezależnego fragmentu**: bazy danych SQL Azure, która przechowuje dane z zestawu danych podzielonej.</span><span class="sxs-lookup"><span data-stu-id="5a068-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="5a068-128">**Elastyczność niezależnego fragmentu**: hello możliwości tooperform zarówno **skalowanie w poziomie** i **skalowanie w pionie**.</span><span class="sxs-lookup"><span data-stu-id="5a068-128">**Shard elasticity**: hello ability tooperform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="5a068-129">**Tabele podzielonej**: tabele, które są podzielonej, tj., których danych jest rozłożona odłamków na podstawie ich wartości klucza dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="5a068-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="5a068-130">**Klucz dzielenia na fragmenty**: wartość kolumny, która określa, jak dane są przesyłane między fragmentów.</span><span class="sxs-lookup"><span data-stu-id="5a068-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="5a068-131">Witaj typ wartości może być jedną z następujących hello: **int**, **bigint**, **varbinary**, lub **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="5a068-131">hello value type can be one of hello following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="5a068-132">**Zestaw niezależnych**: hello kolekcji fragmentów, które są oparte na atrybutach toohello tej samej mapy niezależnego fragmentu w Menedżerze mapy niezależnego fragmentu hello.</span><span class="sxs-lookup"><span data-stu-id="5a068-132">**Shard set**: hello collection of shards that are attributed toohello same shard map in hello shard map manager.</span></span>  

<span data-ttu-id="5a068-133">**Shardlet**: wszystkie dane hello skojarzone z pojedynczą wartość klucz w niezależnych dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="5a068-133">**Shardlet**: All of hello data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="5a068-134">Shardlet jest hello najmniejsza możliwa przenoszenie danych do rozpowszechniania podzielonej tabel.</span><span class="sxs-lookup"><span data-stu-id="5a068-134">A shardlet is hello smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="5a068-135">**Mapa niezależnego fragmentu**: hello zestaw mapowań między dzielenia na fragmenty kluczy i ich odpowiednich fragmentów.</span><span class="sxs-lookup"><span data-stu-id="5a068-135">**Shard map**: hello set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="5a068-136">**Menedżer mapy niezależnego fragmentu**: Zarządzanie obiektu i danych sklepu, która zawiera poprzedzających hello niezależnego fragmentu map, niezależnych lokalizacji i mapowania dla jednego lub więcej zestawów niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="5a068-136">**Shard map manager**: A management object and data store that contains hello shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Mapowania][2]

## <a name="verbs"></a><span data-ttu-id="5a068-138">Zlecenia</span><span class="sxs-lookup"><span data-stu-id="5a068-138">Verbs</span></span>
<span data-ttu-id="5a068-139">**Skalowanie w poziomie**: hello polega na skalowanie w poziomie (lub w) kolekcja odłamków przez dodanie lub usunięcie fragmentów tooa niezależnego fragmentu mapy, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="5a068-139">**Horizontal scaling**: hello act of scaling out (or in) a collection of shards by adding or removing shards tooa shard map, as shown below.</span></span>

![Skalowanie w poziomie i w pionie][3]

<span data-ttu-id="5a068-141">**Scal**: hello act przenoszenie shardlets z dwóch odłamków tooone niezależnych i odpowiednio aktualizacji hello niezależnego fragmentu mapy.</span><span class="sxs-lookup"><span data-stu-id="5a068-141">**Merge**: hello act of moving shardlets from two shards tooone shard and updating hello shard map accordingly.</span></span>

<span data-ttu-id="5a068-142">**Przenieś Shardlet**: hello act przenoszenia niezależnych różnych tooa shardlet pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="5a068-142">**Shardlet move**: hello act of moving a single shardlet tooa different shard.</span></span> 

<span data-ttu-id="5a068-143">**Identyfikator niezależnego fragmentu**: hello polega na poziomie partycjonowania identycznie strukturalnych danych między wieloma bazami danych oparte na kluczu dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="5a068-143">**Shard**: hello act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="5a068-144">**Podziel**: hello act przenoszenia shardlets kilka z niezależnych (zazwyczaj jest to nowy) tooanother jednego niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="5a068-144">**Split**: hello act of moving several shardlets from one shard tooanother (typically new) shard.</span></span> <span data-ttu-id="5a068-145">Klucz dzielenia na fragmenty są dostarczane przez użytkownika hello, jak hello podzielić punktu.</span><span class="sxs-lookup"><span data-stu-id="5a068-145">A sharding key is provided by hello user as hello split point.</span></span>

<span data-ttu-id="5a068-146">**Skalowanie w pionie**: hello polega na skalowanie w górę (lub w dół) hello poziomu wydajności poszczególnych niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="5a068-146">**Vertical Scaling**: hello act of scaling up (or down) hello performance level of an individual shard.</span></span> <span data-ttu-id="5a068-147">Na przykład zmiana niezależnych od standardowego tooPremium, (co powoduje więcej zasobów obliczeniowych).</span><span class="sxs-lookup"><span data-stu-id="5a068-147">For example, changing a shard from Standard tooPremium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

