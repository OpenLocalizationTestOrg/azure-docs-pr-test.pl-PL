---
title: "aaaAdding a niezależnych za pomocą narzędzi elastycznej bazy danych | Dokumentacja firmy Microsoft"
description: "Jak ustawić toouse niezależnych tooa odłamków nowe tooadd interfejsy API elastycznego skalowania."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="be103-103">Dodawanie niezależnych, za pomocą narzędzi elastycznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="be103-103">Adding a shard using Elastic Database tools</span></span>
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="be103-104">tooadd niezależnych dla nowego zakresu lub klucza</span><span class="sxs-lookup"><span data-stu-id="be103-104">tooadd a shard for a new range or key</span></span>
<span data-ttu-id="be103-105">Aplikacje często wymagają toosimply dodać nowe dane toohandle odłamków oczekuje się od nowych kluczy lub kluczy zakresów, mapy niezależnego fragmentu, która już istnieje.</span><span class="sxs-lookup"><span data-stu-id="be103-105">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="be103-106">Na przykład aplikację podzielonej na podstawie Identyfikatora dzierżawcy może być konieczne tooprovision nowy identyfikator niezależnego fragmentu dla nowej dzierżawy lub co miesiąc podzielonej danych może być konieczne nowy identyfikator niezależnego fragmentu udostępnione przed rozpoczęciem powitalne każdego nowego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="be103-106">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="be103-107">Jeśli nowy zakres hello wartości kluczy nie jest już częścią istniejące mapowanie, jest bardzo proste tooadd hello nowe niezależnego fragmentu i skojarz hello nowy klucz lub zakres toothat niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="be103-107">If hello new range of key values is not already part of an existing mapping, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a><span data-ttu-id="be103-108">Przykład: Dodawanie niezależnego fragmentu i jego istniejącej mapy niezależnego fragmentu zakresu tooan</span><span class="sxs-lookup"><span data-stu-id="be103-108">Example:  adding a shard and its range tooan existing shard map</span></span>
<span data-ttu-id="be103-109">W przykładzie użyto hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) metod i tworzy wystąpienie hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) klasy.</span><span class="sxs-lookup"><span data-stu-id="be103-109">This sample uses hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="be103-110">W przykładowym hello poniżej bazy danych o nazwie **sample_shard_2** i wszystkie obiekty niezbędne schematu wewnątrz niej utworzono zakres toohold [300, 400).</span><span class="sxs-lookup"><span data-stu-id="be103-110">In hello sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created toohold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="be103-111">Alternatywnie można użyć programu Powershell toocreate nowego Menedżera mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="be103-111">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="be103-112">Przykład jest dostępny [tutaj](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="be103-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="be103-113">tooadd niezależnych pustą część istniejącego zakresu</span><span class="sxs-lookup"><span data-stu-id="be103-113">tooadd a shard for an empty part of an existing range</span></span>
<span data-ttu-id="be103-114">W niektórych sytuacjach może masz już zamapowana niezależnych tooa zakresu i częściowo wypełnione z danymi, ale teraz ma niezależnego fragmentu różnych ukierunkowanej tooa toobe nadchodzących danych.</span><span class="sxs-lookup"><span data-stu-id="be103-114">In some circumstances, you may have already mapped a range tooa shard and partially filled it with data, but you now want upcoming data toobe directed tooa different shard.</span></span> <span data-ttu-id="be103-115">Na przykład możesz niezależnego fragmentu wg dnia zakres i zostały już przydzielone niezależnych tooa 50 dni, ale dnia 24 ma tooland przyszłych danych w różnych niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="be103-115">For example, you shard by day range and have already allocated 50 days tooa shard, but on day 24, you want future data tooland in a different shard.</span></span> <span data-ttu-id="be103-116">Witaj elastycznej bazy danych [narzędzia do scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md) mogą wykonać tę operację, ale jeśli przenoszenia danych nie jest konieczne (na przykład dane dla zakresu hello dni [25, 50), tj., dzień 25 włącznie too50 wyłączności, jeszcze nie istnieje) można wykonać to całkowicie przy użyciu hello bezpośrednio interfejsy API Management mapy niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="be103-116">hello elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for hello range of days [25, 50), i.e., day 25 inclusive too50 exclusive, does not yet exist) you can perform this entirely using hello Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a><span data-ttu-id="be103-117">Przykład: podział zakresu i przypisywanie hello pustych niezależnych nowo dodanych tooa części</span><span class="sxs-lookup"><span data-stu-id="be103-117">Example: splitting a range and assigning hello empty portion tooa newly-added shard</span></span>
<span data-ttu-id="be103-118">Utworzono bazę danych o nazwie "sample_shard_2" oraz wszystkie obiekty niezbędne schematu wewnątrz niej.</span><span class="sxs-lookup"><span data-stu-id="be103-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="be103-119">**Ważne**: Użyj tej techniki tylko w przypadku niektórych, które hello zakres mapowania hello aktualizacji jest pusta.</span><span class="sxs-lookup"><span data-stu-id="be103-119">**Important**:  Use this technique only if you are certain that hello range for hello updated mapping is empty.</span></span>  <span data-ttu-id="be103-120">metody Hello powyżej sprawdza dane dla zakresu hello przenoszony, dlatego najlepiej jest tooinclude sprawdza w kodzie.</span><span class="sxs-lookup"><span data-stu-id="be103-120">hello methods above do not check data for hello range being moved, so it is best tooinclude checks in your code.</span></span>  <span data-ttu-id="be103-121">Jeśli istnieją wiersze w zakresie hello przenoszony, hello rzeczywiste dane dystrybucji nie będzie odpowiadała hello niezależnych zaktualizowane mapy.</span><span class="sxs-lookup"><span data-stu-id="be103-121">If rows exist in hello range being moved, hello actual data distribution will not match hello updated shard map.</span></span> <span data-ttu-id="be103-122">Użyj hello [narzędzia do scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operacji zamiast tego w tych przypadkach.</span><span class="sxs-lookup"><span data-stu-id="be103-122">Use hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

