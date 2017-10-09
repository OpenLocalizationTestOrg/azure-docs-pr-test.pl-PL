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
# <a name="migrate-existing-databases-tooscale-out"></a>Migrowanie istniejących baz danych tooscale w poziomie
Łatwe zarządzanie istniejących skalowalnych w poziomie podzielonej baz danych za pomocą narzędzi bazy danych usługi Azure SQL Database (takich jak hello [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md)). Najpierw należy przekonwertować istniejącego zestawu baz danych toouse hello [menedżera map niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md). 

## <a name="overview"></a>Omówienie
toomigrate istniejącej bazy danych podzielonej: 

1. Przygotowanie hello [bazy danych Menedżera mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md).
2. Utwórz hello niezależnego fragmentu mapy.
3. Przygotuj hello poszczególnych fragmentów.  
4. Dodaj mapę niezależnego fragmentu toohello mapowania.

Te techniki można implementować przy użyciu albo hello [biblioteki klienta .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), lub skryptów programu PowerShell hello znaleźć pod adresem [Azuresql DB - skrypty narzędzi elastycznej bazy danych](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db). Przykłady Hello tutaj za pomocą skryptów środowiska PowerShell hello.

Aby uzyskać więcej informacji na temat hello ShardMapManager, zobacz [zarządzania mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md). Omówienie hello narzędzi elastycznej bazy danych, zobacz [Przegląd funkcji elastycznej bazy danych](sql-database-elastic-scale-introduction.md).

## <a name="prepare-hello-shard-map-manager-database"></a>Przygotowanie hello niezależnego fragmentu mapy manager w bazie danych
Menedżera map niezależnego fragmentu Hello jest specjalne bazy danych, która zawiera hello danych toomanage skalowalnych w poziomie w bazach danych. Użyj istniejącej bazy danych lub Utwórz nową bazę danych. Należy pamiętać, że baza danych działa jako menedżera map niezależnego fragmentu nie powinien być hello sam bazy danych jako niezależnego fragmentu. Należy również zauważyć, że skrypt programu PowerShell hello nie tworzy hello bazy danych dla Ciebie. 

## <a name="step-1-create-a-shard-map-manager"></a>Krok 1: tworzenie niezależnych menedżera map
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a>tooretrieve hello niezależnego fragmentu mapy manager
Po utworzeniu można pobrać hello niezależnego fragmentu mapy manager z tego polecenia cmdlet. Ten krok jest niezbędny, za każdym razem, gdy należy toouse hello ShardMapManager obiektu.

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a>Krok 2: Tworzenie mapy niezależnego fragmentu hello
Należy wybrać typ hello toocreate mapy niezależnego fragmentu. Wybór Hello zależy od hello Architektura bazy danych: 

1. Pojedynczej dzierżawy na bazę danych (terminów, zobacz hello [słownik](sql-database-elastic-scale-glossary.md).) 
2. Wiele dzierżaw dla jednej bazy danych (dwa typy):
   1. Mapowanie list
   2. Mapowanie zakresu

Model pojedynczego dzierżawcy można utworzyć **mapowania listy** mapy niezależnego fragmentu. model pojedynczej dzierżawy Hello przypisuje jednej bazy danych dla każdego dzierżawcy. Jest to efektywne modelu dla deweloperów SaaS, ponieważ takie rozwiązanie upraszcza zarządzanie.

![Mapowanie list][1]

modelu wielodostępnym Hello przypisuje kilka dzierżaw tooa pojedynczej bazy danych (i grup dzierżawcy mogą rozpowszechniają wielu baz danych). Użyj tego modelu, gdy oczekuje się, że każdy dzierżawca toohave niewielkie zbiory danych musi. W tym modelu możemy Przypisz zakres przy użyciu bazy danych tooa dzierżawców **mapowanie zakresu**. 

![Mapowanie zakresu][2]

Lub możesz wdrożyć model bazy danych wielu dzierżawców przy użyciu *mapowania listy* tooassign wiele dzierżaw tooa pojedynczej bazy danych. Na przykład DB1 jest używane toostore informacji na temat identyfikatora dzierżawy 1 do 5 i bazy danych DB2 przechowuje dane dla dzierżawy 7 i dzierżawcy 10. 

![Wielu dzierżawców dla jednej bazy danych][3] 

**W oparciu o wybór, wybierz jedną z następujących opcji:**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>Opcja 1: Tworzenie mapy niezależnego fragmentu mapowania listy
Tworzenie przy użyciu obiektu ShardMapManager hello mapy niezależnego fragmentu. 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>Opcja 2: Tworzenie mapy niezależnego fragmentu mapowania zakresu
Należy pamiętać, że tooutilize tego wzorca mapowania, zakresy ciągłe toobe wymaga wartości identyfikatora dzierżawy i jest dopuszczalne toohave przerwa w zakresach hello po prostu pomijając hello zakres podczas jej tworzenia hello.

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>Opcja 3: Lista mapowania na pojedynczej bazy danych
Konfigurowanie ten wzorzec wymaga również tworzenia mapy listy jak pokazano w kroku 2, opcja 1.

## <a name="step-3-prepare-individual-shards"></a>Krok 3: Przygotowanie poszczególnych odłamków
Dodaj każdy identyfikator niezależnego fragmentu (baza danych) toohello niezależnego fragmentu mapy menedżera. Do przechowywania informacji o mapowaniu to przygotowuje hello pojedynczych baz danych. Tej metody należy wykonać na każdym niezależnego fragmentu.

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a>Krok 4: Dodawanie mapowania
Dodawanie Hello mapowań zależy od rodzaju hello mapować niezależnego fragmentu utworzoną. Jeśli utworzono mapy listy, możesz dodać mapowania listy. Jeśli utworzono map zakres, należy dodać mapowania zakresu.

### <a name="option-1-map-hello-data-for-a-list-mapping"></a>Opcja 1: mapowanie danych hello mapowania listy
Mapowanie danych hello przez dodanie mapowania listy dla każdego dzierżawcy.  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a>Opcja 2: mapowanie danych hello mapowania zakresu
Dodaj hello zakresu mapowania dla wszystkich hello dzierżawy zakres identyfikatora - skojarzenia bazy danych:

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a>Krok 4 — opcja 3: hello dane mapy dla wielu dzierżawców w pojedynczej bazy danych
Dla każdego dzierżawcy, uruchom hello Dodaj ListMapping (opcja 1, powyżej). 

## <a name="checking-hello-mappings"></a>Sprawdzanie, czy hello mapowania
Informacje o istniejących odłamków hello i mapowania hello skojarzonych z nimi mogą być przeszukiwane przy użyciu następujących poleceń:  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>Podsumowanie
Po zakończeniu instalacji hello można rozpocząć biblioteki klienta elastycznej bazy danych hello toouse. Można również użyć [danych zależnych routingu](sql-database-elastic-scale-data-dependent-routing.md) i [zapytania wielu niezależnych](sql-database-elastic-scale-multishard-querying.md).

## <a name="next-steps"></a>Następne kroki
Pobierz skrypty programu PowerShell hello [bazy danych elastyczne bazy danych SQL Azure narzędzi sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

narzędzia Hello są również w witrynie GitHub: [Azure/elastyczna db-tools](https://github.com/Azure/elastic-db-tools).

Użyj hello narzędzia do scalania podziału toomove danych tooor z modelu pojedynczej dzierżawy tooa modelu wielodostępnym. Zobacz [narzędzia do scalania podziału](sql-database-elastic-scale-get-started.md).

## <a name="additional-resources"></a>Dodatkowe zasoby
Aby uzyskać informacje na temat typowych wzorców architektury danych w aplikacjach baz danych typu oprogramowanie jako usługa (SaaS), zobacz artykuł [Design Patterns for Multi-tenant SaaS Applications with Azure SQL Database](sql-database-design-patterns-multi-tenancy-saas-applications.md) (Wzorce projektowe dla wielodostępnych aplikacji SaaS korzystających z usługi Azure SQL Database).

## <a name="questions-and-feature-requests"></a>Pytania i żądania funkcji
Odpowiedzi na pytania, proszę dotrzeć toous na powitania [forum bazy danych SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) i funkcja żądań, dodaj je toohello [forum opinii bazy danych SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

