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
# <a name="adding-a-shard-using-elastic-database-tools"></a>Dodawanie niezależnych, za pomocą narzędzi elastycznej bazy danych
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a>tooadd niezależnych dla nowego zakresu lub klucza
Aplikacje często wymagają toosimply dodać nowe dane toohandle odłamków oczekuje się od nowych kluczy lub kluczy zakresów, mapy niezależnego fragmentu, która już istnieje. Na przykład aplikację podzielonej na podstawie Identyfikatora dzierżawcy może być konieczne tooprovision nowy identyfikator niezależnego fragmentu dla nowej dzierżawy lub co miesiąc podzielonej danych może być konieczne nowy identyfikator niezależnego fragmentu udostępnione przed rozpoczęciem powitalne każdego nowego miesiąca. 

Jeśli nowy zakres hello wartości kluczy nie jest już częścią istniejące mapowanie, jest bardzo proste tooadd hello nowe niezależnego fragmentu i skojarz hello nowy klucz lub zakres toothat niezależnego fragmentu. 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a>Przykład: Dodawanie niezależnego fragmentu i jego istniejącej mapy niezależnego fragmentu zakresu tooan
W przykładzie użyto hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) metod i tworzy wystąpienie hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) klasy. W przykładowym hello poniżej bazy danych o nazwie **sample_shard_2** i wszystkie obiekty niezbędne schematu wewnątrz niej utworzono zakres toohold [300, 400).  

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


Alternatywnie można użyć programu Powershell toocreate nowego Menedżera mapy niezależnego fragmentu. Przykład jest dostępny [tutaj](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a>tooadd niezależnych pustą część istniejącego zakresu
W niektórych sytuacjach może masz już zamapowana niezależnych tooa zakresu i częściowo wypełnione z danymi, ale teraz ma niezależnego fragmentu różnych ukierunkowanej tooa toobe nadchodzących danych. Na przykład możesz niezależnego fragmentu wg dnia zakres i zostały już przydzielone niezależnych tooa 50 dni, ale dnia 24 ma tooland przyszłych danych w różnych niezależnego fragmentu. Witaj elastycznej bazy danych [narzędzia do scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md) mogą wykonać tę operację, ale jeśli przenoszenia danych nie jest konieczne (na przykład dane dla zakresu hello dni [25, 50), tj., dzień 25 włącznie too50 wyłączności, jeszcze nie istnieje) można wykonać to całkowicie przy użyciu hello bezpośrednio interfejsy API Management mapy niezależnego fragmentu.

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a>Przykład: podział zakresu i przypisywanie hello pustych niezależnych nowo dodanych tooa części
Utworzono bazę danych o nazwie "sample_shard_2" oraz wszystkie obiekty niezbędne schematu wewnątrz niej.  

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

**Ważne**: Użyj tej techniki tylko w przypadku niektórych, które hello zakres mapowania hello aktualizacji jest pusta.  metody Hello powyżej sprawdza dane dla zakresu hello przenoszony, dlatego najlepiej jest tooinclude sprawdza w kodzie.  Jeśli istnieją wiersze w zakresie hello przenoszony, hello rzeczywiste dane dystrybucji nie będzie odpowiadała hello niezależnych zaktualizowane mapy. Użyj hello [narzędzia do scalania podziału](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operacji zamiast tego w tych przypadkach.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

