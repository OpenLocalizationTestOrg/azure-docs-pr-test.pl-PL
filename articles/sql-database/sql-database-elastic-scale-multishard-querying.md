---
title: Zapytanie bazy danych Azure SQL podzielonej | Dokumentacja firmy Microsoft
description: "Uruchamianie zapytań między odłamków za pomocą biblioteki klienta elastycznej bazy danych."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: torsteng
ms.openlocfilehash: 33128357bd5b2bd744c5c1c3032f658ebe865d49
ms.sourcegitcommit: 5a6e943718a8d2bc5babea3cd624c0557ab67bd5
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/01/2017
---
# <a name="multi-shard-querying"></a>Wiele niezależnych zapytań
## <a name="overview"></a>Omówienie
Z [narzędzi elastycznej bazy danych](sql-database-elastic-scale-introduction.md), można utworzyć bazy danych podzielonej rozwiązania. **Wiele niezależnych badania** służy do zadań, takich jak kolekcja/raportowania danych wymagających uruchomienia zapytania, który rozciąga się na kilka fragmentów. (Natomiast aby [routingu zależne od danych](sql-database-elastic-scale-data-dependent-routing.md), które wykonuje całą pracę na jednego niezależnego fragmentu.) 

1. Pobierz **RangeShardMap** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn807318.aspx)) lub **ListShardMap** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._list_shard_map), [.NET ](https://msdn.microsoft.com/library/azure/dn807370.aspx)) przy użyciu **TryGetRangeShardMap** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.trygetrangeshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx)), **TryGetListShardMap** ([ Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.trygetlistshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx)), lub **GetShardMap** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.getshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx)) metody. Zobacz  **[konstruowania ShardMapManager](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager)**  i  **[uzyskać RangeShardMap lub ListShardMap](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap)**.
2. Utwórz **MultiShardConnection** ([Java](/java/api/com.microsoft.azure.elasticdb.query.multishard._multi_shard_connection), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)) obiektu.
3. Utwórz **MultiShardStatement lub MultiShardCommand** ([Java](/java/api/com.microsoft.azure.elasticdb.query.multishard._multi_shard_statement), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)). 
4. Ustaw **Właściwość CommandText** ([Java](/java/api/com.microsoft.azure.elasticdb.query.multishard._multi_shard_statement), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)) do polecenia T-SQL.
5. Wykonaj polecenie wywołując **ExecuteQueryAsync lub ExecuteReader** ([Java](), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)) metody.
6. Wyświetl wyniki za pomocą **MultiShardResultSet lub MultiShardDataReader** ([Java](/java/api/com.microsoft.azure.elasticdb.query.multishard._multi_shard_result_set), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)) klasy. 

## <a name="example"></a>Przykład
Poniższy kod przedstawia użycie wielu niezależnych zapytań za pomocą danego **ShardMap** o nazwie *myShardMap*. 

```csharp
using (MultiShardConnection conn = new MultiShardConnection(myShardMap.GetShards(), myShardConnectionString)) 
{ 
    using (MultiShardCommand cmd = conn.CreateCommand())
    { 
        cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
        cmd.CommandType = CommandType.Text; 
        cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
        cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

        using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
        { 
            while (sdr.Read())
            { 
                var c1Field = sdr.GetString(0); 
                var c2Field = sdr.GetFieldValue<int>(1); 
                var c3Field = sdr.GetFieldValue<Int64>(2);
            } 
        } 
    } 
} 
```

Najważniejsza różnica polega na konstrukcji niezależnych wielu połączeń. Gdzie **SqlConnection** działa na pojedynczej bazy danych **MultiShardConnection** przyjmuje ***kolekcji odłamków*** jako dane wejściowe. Wypełnianie kolekcji odłamków z mapy niezależnego fragmentu. Następnie wykonać zapytania w kolekcji przy użyciu fragmentów **UNION ALL** semantyki można złożyć jeden wynik ogólny. Opcjonalnie można dodać nazwę niezależnego fragmentu, z której pochodzi wiersz do danych wyjściowych przy użyciu **ExecutionOptions** właściwość polecenia. 

Należy pamiętać, wywołanie **myShardMap.GetShards()**. Ta metoda pobiera wszystkie odłamków z mapy niezależnego fragmentu i zapewnia prosty sposób do uruchamiania kwerendy dla wszystkich odpowiednich baz danych. Kolekcji odłamków dla wielu niezależnych zapytanie może być precyzyjnych dalsze przez wykonanie zapytania LINQ w kolekcji zwróconej z wywołania do **myShardMap.GetShards()**. W połączeniu z zasadami wyniki częściowe bieżących możliwości wielu niezależnych badania został zaprojektowany do pracy oraz dziesiątki maksymalnie setki fragmentów.

To ograniczenie z wielu niezależnych zapytań jest obecnie braku weryfikacji odłamków i shardlets, które będą pytani. Podczas routingu zależne od danych sprawdza, czy dany identyfikator niezależnego fragmentu mapy niezależnego fragmentu w czasie wykonywania zapytania, zapytania wielu niezależnego fragmentu nie wykonuj tego wyboru. Może to prowadzić do zapytań wielu niezależnych wykonywanych w bazach danych, które zostały usunięte z mapy niezależnego fragmentu.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Wiele niezależnych zapytań i operacji scalania podziału
Wiele niezależnych zapytania nie weryfikują czy shardlets w bazie danych, którego dotyczy kwerenda uczestniczą w trwających operacji scalania podziału. (Zobacz [odbierającej za pomocą narzędzia do scalania podziału elastycznej bazy danych](sql-database-elastic-scale-overview-split-and-merge.md).) Może to prowadzić do niespójności gdzie wierszy z tej samej shardlet Pokaż dla wielu baz danych w jednym zapytaniu wielu niezależnego fragmentu. Należy pamiętać o tych ograniczeniach i podczas wykonywania zapytania wielu niezależnych należy wziąć pod uwagę opróżniania trwających operacji scalania podziału i zmiany do mapy niezależnego fragmentu.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]


