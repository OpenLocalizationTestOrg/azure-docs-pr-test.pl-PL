---
title: "liczniki aaaPerformance niezależnego fragmentu mapowania Menedżer"
description: "ShardMapManager klas i danych zależnych routingu liczniki wydajności"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a>Liczniki wydajności dla menedżera map fragmentów
Można przechwycić wydajność hello [menedżera map niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md), zwłaszcza w przypadku korzystania [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md). Liczniki są tworzone z metodami hello Microsoft.Azure.SqlDatabase.ElasticScale.Client klasy.  

Liczniki są używane tootrack wydajność hello [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md) operacji. Te liczniki są dostępne w hello monitora wydajności w kategorii "Zarządzanie bazą danych niezależnego fragmentu: elastycznej" hello.

**Do najnowszej wersji hello:** Przejdź zbyt[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Zobacz też [uaktualniania aplikacji toouse hello najnowsze elastycznej bazy danych biblioteki klienta](sql-database-elastic-scale-upgrade-client-library.md).

## <a name="prerequisites"></a>Wymagania wstępne
* Witaj kategorii wydajności hello toocreate i liczników, użytkownik musi być częścią lokalne powitania **Administratorzy** grupy na komputerze hello hosting aplikacji hello.  
* toocreate wydajności wystąpienia licznika i zaktualizować liczniki hello, hello użytkownik musi być członkiem albo hello **Administratorzy** lub **Użytkownicy monitora wydajności** grupy. 

## <a name="create-performance-category-and-counters"></a>Tworzenie kategorii wydajności i liczniki
liczniki hello toocreate wywołać metodę CreatePeformanceCategoryAndCounters hello hello [ShardMapManagmentFactory klasy](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx). Tylko administrator może wykonać hello metody: 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

Można również użyć [to](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) metoda hello tooexecute skryptu programu PowerShell. Metoda Hello tworzy hello następujące liczniki wydajności:  

* **Buforowane mapowania**: liczba mapowania mapę niezależnego fragmentu hello w pamięci podręcznej.
* **Operacje DDR na sekundę**: szybkości danych zależnych operacji routingu hello niezależnego fragmentu mapy. Ten licznik jest aktualizowany po wywołaniu zbyt[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) wynikiem pomyślnym połączeniu toohello docelowy identyfikator niezależnego fragmentu. 
* **Mapowanie trafienia pamięci podręcznej wyszukiwania na sekundę**: szybkość przeprowadzania operacji wyszukiwania pomyślne pamięci podręcznej dla mapowań hello niezależnego fragmentu mapy. 
* **Chybienia pamięci podręcznej wyszukiwania na sekundę mapowania**: liczba operacji wyszukiwania w pamięci podręcznej nie powiodło się dla mapowań hello niezależnego fragmentu mapy.
* **Mapowania dodane lub zaktualizowane w pamięci podręcznej na sekundę**: szybkości mapowania, które są dodawane lub zaktualizowane w pamięci podręcznej hello niezależnego fragmentu mapy. 
* **Mapowania usuwane z pamięci podręcznej na sekundę**: współczynnik jaką mapowania są usuwane z pamięci podręcznej hello niezależnego fragmentu mapy. 

Liczniki wydajności są tworzone dla każdej mapy niezależnych pamięci podręcznej na proces.  

## <a name="notes"></a>Uwagi
Witaj następujące zdarzenia wyzwolić tworzenie hello hello liczników wydajności:  

* Inicjowanie hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) z [wczesny ładowania](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx), jeśli hello ShardMapManager zawiera wszystkie mapy niezależnego fragmentu. Obejmują one hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) i hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) metody.
* Pomyślne wyszukiwania mapy niezależnego fragmentu (przy użyciu [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) lub [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)). 
* Pomyślnym utworzeniu przy użyciu CreateShardMap() mapy niezależnego fragmentu.

liczniki wydajności Hello będą aktualizowane przez wszystkich operacji pamięci podręcznej na powitania niezależnego fragmentu mapy i mapowania. Pomyślne usunięcie mapy niezależnego fragmentu hello usunięcie wystąpienia liczników wydajności hello przy użyciu DeleteShardMap reults ().  

## <a name="best-practices"></a>Najlepsze praktyki
* Tworzenie hello kategorii wydajności i liczniki powinny być wykonywane tylko raz, przed utworzeniem hello ShardMapManager obiektu. Co wykonanie polecenia hello CreatePerformanceCategoryAndCounters() Czyści hello liczniki poprzedniego (utraty danych przekazywanych przez wszystkie wystąpienia) i tworzy nowe.  
* Wystąpienia licznika wydajności są tworzone na proces. Awarii aplikacji ani usuwania mapy niezależnego fragmentu z pamięci podręcznej hello spowoduje usunięcie wystąpienia liczników wydajności hello.  

### <a name="see-also"></a>Zobacz też
[Przegląd funkcji usługi elastycznej bazy danych](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

