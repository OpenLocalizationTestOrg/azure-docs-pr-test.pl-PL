---
title: bazy danych Azure SQL podzielonej aaaQuery | Dokumentacja firmy Microsoft
description: "Uruchamianie zapytań między odłamków za pomocą biblioteki klienta elastycznej bazy danych hello."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: a1f0763935a6807b74aa9dec477714e8d117417d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-shard-querying"></a>Wiele niezależnych zapytań
## <a name="overview"></a>Omówienie
Z hello [narzędzi elastycznej bazy danych](sql-database-elastic-scale-introduction.md), można utworzyć bazy danych podzielonej rozwiązania. **Wiele niezależnych badania** służy do zadań, takich jak kolekcja/raportowania danych wymagających uruchomienia zapytania, który rozciąga się na kilka fragmentów. (Natomiast to zbyt[routingu zależne od danych](sql-database-elastic-scale-data-dependent-routing.md), które wykonuje całą pracę na jednego niezależnego fragmentu.) 

1. Pobierz [ **RangeShardMap** ](https://msdn.microsoft.com/library/azure/dn807318.aspx) lub [ **ListShardMap** ](https://msdn.microsoft.com/library/azure/dn807370.aspx) przy użyciu hello [ **TryGetRangeShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ **TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), lub hello [ **GetShardMap** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) metody. Zobacz [ **konstruowania ShardMapManager** ](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) i [ **uzyskać RangeShardMap lub ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Utwórz  **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)**  obiektu.
3. Utwórz  **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Zestaw hello  **[Właściwość CommandText](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)**  tooa polecenia T-SQL.
5. Wykonanie polecenia hello przez wywołanie hello  **[metodę ExecuteReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. Wyświetl wyniki hello za pomocą hello  **[klasy MultiShardDataReader](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Przykład
Witaj poniższy kod ilustruje hello użycie wielu niezależnych zapytań za pomocą danego **ShardMap** o nazwie *myShardMap*. 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
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


Najważniejsza różnica polega na konstrukcji hello niezależnych wielu połączeń. Gdzie **SqlConnection** działa na pojedynczej bazy danych hello **MultiShardConnection** przyjmuje ***kolekcji odłamków*** jako dane wejściowe. Wypełnia kolekcję hello odłamków z mapy niezależnego fragmentu. następnie jest przeprowadzana kwerenda Hello na powitania zbiór odłamków przy użyciu **UNION ALL** tooassemble semantykę pojedynczego wyniku ogólnej. Opcjonalnie można dodać nazwę hello hello niezależnego fragmentu wiersza hello, z której pochodzi toohello wyjściowe hello **ExecutionOptions** właściwość polecenia. 

Należy zwrócić uwagę hello wywołanie za**myShardMap.GetShards()**. Ta metoda pobiera wszystkie odłamków z mapy niezależnego fragmentu hello i zapewnia prosty sposób toorun zapytania dla wszystkich odpowiednich baz danych. Hello kolekcji odłamków dla wielu niezależnych zapytanie może być precyzyjnych dalsze, wykonując LINQ zapytanie dotyczące kolekcji hello zwracany z wywołania hello zbyt**myShardMap.GetShards()**. W połączeniu z zasadami wyniki częściowe hello hello bieżących możliwości wielu niezależnych badania została toowork zaprojektowane dla dziesiątki się toohundreds fragmentów.

To ograniczenie z wielu niezależnych zapytań jest obecnie Brak hello zatwierdzania liczbie fragmentów i shardlets, które będą pytani. Podczas routingu zależne od danych sprawdza, czy dany identyfikator niezależnego fragmentu mapy niezależnego fragmentu hello w czasie hello kwerendy, zapytania wielu niezależnego fragmentu nie wykonuj tego wyboru. Może to spowodować zapytań niezależnego fragmentu toomulti wykonywanych w bazach danych, które zostały usunięte z hello niezależnego fragmentu mapy.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Wiele niezależnych zapytań i operacji scalania podziału
Wiele niezależnych zapytania nie weryfikują czy shardlets w bazie danych, którego dotyczy kwerenda hello uczestniczą w trwających operacji scalania podziału. (Zobacz [skalowania, za pomocą narzędzia hello scalanie podziału elastycznej bazy danych](sql-database-elastic-scale-overview-split-and-merge.md).) Może to spowodować tooinconsistencies której wiersze z hello tego samego Pokaż shardlet dla wielu baz danych w hello tego samego zapytania wielu niezależnego fragmentu. Należy pamiętać o tych ograniczeniach oraz należy wziąć pod uwagę opróżnianie trwającą scalania podziału operacje i zmiany toohello niezależnego fragmentu mapy podczas wykonywania zapytania wielu niezależnych.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>Zobacz też
**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)**  klasy i metody.

Zarządzanie za pomocą hello odłamków [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md). Zawiera obszar nazw o nazwie [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) zapewnia tooquery możliwości hello wielu odłamków przy użyciu pojedynczego zapytania i wyników. Zapewnia on podczas badania abstrakcji przez kolekcję fragmentów. Umożliwia także zasad alternatywnych wykonywania, w szczególności częściowe wyniki, toodeal z błędami podczas wykonywania zapytania w wielu fragmentów.  

