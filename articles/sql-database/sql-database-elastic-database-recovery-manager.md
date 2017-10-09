---
title: "aaaUsing toofix Menedżera odzyskiwania niezależnego fragmentu mapowania problemów | Dokumentacja firmy Microsoft"
description: "Użyj hello RecoveryManager klasy toosolve problemów przy użyciu map niezależnego fragmentu"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 45520ca3-6903-4b39-88ba-1d41b22da9fe
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: ddove
ms.openlocfilehash: 2218fb15122f1df466e65483480461e366317f2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-recoverymanager-class-toofix-shard-map-problems"></a>Przy użyciu hello RecoveryManager klasy toofix niezależnego fragmentu mapy problemów
Witaj [RecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.aspx) klasa udostępnia ADO.Net aplikacji hello możliwości tooeasily wykrywać i poprawiać niespójności między hello mapy globalne niezależnego fragmentu (GSM), a następnie mapować lokalnego niezależnych hello (LSM) tak, w środowisku bazy danych podzielonej. 

Witaj GSM i LSM Śledź hello mapowania poszczególnych baz danych w środowisku podzielonej. Czasami występuje podział między hello GSM i hello LSM. W takim przypadku użyj hello RecoveryManager klasy toodetect i napraw hello podziału.

Klasa RecoveryManager Hello jest częścią hello [biblioteki klienta elastycznej bazy danych](sql-database-elastic-database-client-library.md). 

![Identyfikator niezależnego fragmentu mapy][1]

Aby uzyskać definicje terminów, zobacz [słownik narzędzi elastycznej bazy danych](sql-database-elastic-scale-glossary.md). jak hello toounderstand **ShardMapManager** toomanage używane dane w podzielonym rozwiązania, zobacz [zarządzania mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md).

## <a name="why-use-hello-recovery-manager"></a>Dlaczego warto używać Menedżera odzyskiwania hello?
W środowisku podzielonej bazy danych ma jednej dzierżawy na bazę danych i wielu baz danych na serwerze. Może istnieć wiele serwerów w środowisku hello. Każda baza danych jest mapowany w mapie niezależnego fragmentu hello, dlatego wywołania mogą być kierowany toohello właściwym serwerem i bazy danych. Bazy danych są śledzone według tooa **klucza dzielenia na fragmenty**, i ma przypisany każdego niezależnych **zakres wartości klucza**. Na przykład klucz dzielenia na fragmenty może reprezentować powitania klienta nazwy z "D" za "F." Witaj, mapowanie wszystkich odłamków (alias bazy danych), ich zakresy mapowania są zawarte w hello **mapy globalne niezależnego fragmentu (GSM)**. Każda baza danych zawiera także mapy zakresów hello zawartych w niezależnych hello, znany jako hello **mapy lokalnego niezależnego fragmentu (LSM) tak,**. Gdy aplikacja łączy niezależnych tooa, mapowanie hello jest buforowany aplikacji hello szybkiego pobierania. Witaj LSM jest toovalidate używanych w pamięci podręcznej danych. 

Witaj GSM i LSM może stać się zsynchronizowany na powitania z następujących powodów:

1. Usuwanie Hello niezależnych, której zakres za toono dłużej być w użyciu lub zmiana nazwy niezależnego fragmentu. Powoduje usunięcie niezależnych **oddzielona mapowanie niezależnych**. Podobnie zmieniono nazwę bazy danych może spowodować oddzielone niezależnego fragmentu mapowania. W zależności od celem hello hello zmiany niezależnych hello może być konieczne toobe usunięte lub hello niezależnego fragmentu lokalizacji wymaga toobe aktualizacji. toorecover usuniętej bazy danych, zobacz [przywrócić usuniętą bazę](sql-database-recovery-using-backups.md).
2. Występuje zdarzenie geograficznie pracy w trybie failover. toocontinue, co należy zaktualizować hello nazwę serwera i nazwę bazy danych Menedżera mapy niezależnego fragmentu w aplikacji hello, a następnie szczegóły mapowania niezależnego fragmentu hello aktualizacji wszystkich odłamków na mapie niezależnego fragmentu. W przypadku geograficznie trybu failover, takie logiki odzyskiwania powinno zostać zautomatyzowane w przepływie pracy trybu failover hello. Automatyzowanie akcje odzyskiwania umożliwia frictionless możliwości zarządzania włączone geograficznie baz danych i pozwala uniknąć człowieka działań ręcznych. toolearn o toorecover opcje bazy danych w przypadku awarii centrum danych, zobacz [ciągłość prowadzenia działalności biznesowej](sql-database-business-continuity.md) i [odzyskiwania po awarii](sql-database-disaster-recovery.md).
3. Niezależnego fragmentu albo hello ShardMapManager bazy danych jest tooan przywróconej wcześniej punktu w czasie. toolearn dotyczące punktu w czasie odzyskiwania przy użyciu kopii zapasowych, zobacz [odzyskiwania za pomocą kopii zapasowej](sql-database-recovery-using-backups.md).

Aby uzyskać więcej informacji na temat narzędzi elastycznej bazy danych Azure SQL bazy danych — replikacja geograficzna i przywracania zobacz następujące hello: 

* [Omówienie: Chmury firm odzyskiwania po awarii ciągłości i bazy danych z bazy danych SQL](sql-database-business-continuity.md) 
* [Wprowadzenie do narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md)  
* [Zarządzanie ShardMap](sql-database-elastic-scale-shard-map-management.md)

## <a name="retrieving-recoverymanager-from-a-shardmapmanager"></a>Pobieranie RecoveryManager z ShardMapManager
pierwszym krokiem Hello jest toocreate wystąpienia RecoveryManager. Witaj [metody GetRecoveryManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getrecoverymanager.aspx) zwraca hello Menedżera odzyskiwania dla bieżącego hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) wystąpienia. Mapowanie niespójności w niezależnych hello tooaddress, należy najpierw pobrać hello RecoveryManager hello określonego niezależnych mapy. 

   ```
    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString,  
             ShardMapManagerLoadPolicy.Lazy);
             RecoveryManager rm = smm.GetRecoveryManager(); 
   ```

W tym przykładzie hello RecoveryManager jest inicjowana z hello ShardMapManager. Witaj ShardMapManager zawierający ShardMap jest również już zainicjowany. 

Ponieważ ten kod aplikacji manipuluje hello niezależnego fragmentu mapy, poświadczenia używane w metodzie fabryki hello hello (w hello poprzedzających przykład smmConnectionString) powinna być poświadczenia, które mają uprawnienia odczytu i zapisu w bazie danych GSM hello odwołuje się hello Parametry połączenia. Te poświadczenia zwykle różnią się od połączenia tooopen poświadczenia używane do routingu zależne od danych. Aby uzyskać więcej informacji, zobacz [powitania klienta elastycznej bazy danych przy użyciu poświadczeń](sql-database-elastic-scale-manage-credentials.md).

## <a name="removing-a-shard-from-hello-shardmap-after-a-shard-is-deleted"></a>Usuwanie niezależnych od hello ShardMap po usunięciu niezależnego fragmentu
Witaj [DetachShard metoda](https://msdn.microsoft.com/library/azure/dn842083.aspx) odłącza hello podany identyfikator niezależnego fragmentu z mapy niezależnego fragmentu hello i usuwa skojarzone z hello niezależnego fragmentu mapowania.  

* Parametr lokalizacja Hello jest hello niezależnego fragmentu lokalizacji, w szczególności nazwę serwera i nazwę bazy danych, niezależnych hello odłączany. 
* Parametr shardMapName Hello jest nazwa mapy hello niezależnego fragmentu. Jest to tylko wymagana, gdy wielu map niezależnego fragmentu są zarządzane przez hello samego menedżera mapy niezależnego fragmentu. Opcjonalny. 


> [!IMPORTANT]
> Użyj tej techniki tylko wtedy, gdy masz pewność, że zakres hello mapowania hello aktualizacji jest pusty. metody Hello powyżej sprawdza dane dla zakresu hello przenoszony, dlatego najlepiej jest tooinclude sprawdza w kodzie.
>

W tym przykładzie usuwa hello mapy niezależnych fragmentów. 

   ```
   rm.DetachShard(s.Location, customerMap);
   ``` 

mapy niezależnego fragmentu Hello odzwierciedla hello niezależnego fragmentu lokalizacji w hello GSM przed hello usunięcie hello niezależnego fragmentu. Ponieważ niezależnych hello został usunięty, zakłada się to było zamierzone i zakresem kluczy hello dzielenia na fragmenty nie jest już używana. Jeśli nie możesz wykonać przywracanie do punktu w czasie. toorecover hello niezależnych od wcześniejszej punktu w czasie. (W takim przypadku Przejrzyj powitania po niespójności niezależnego fragmentu toodetect sekcji). toorecover, zobacz [punktu w czasie odzyskiwania](sql-database-recovery-using-backups.md).

Ponieważ zakłada się, że usunięcie bazy danych hello było zamierzone, hello Akcja końcowego oczyszczania administracyjnych jest toodelete hello wpis toohello niezależnych w Menedżerze mapy niezależnego fragmentu hello. Zapobiega to aplikacja hello przypadkowo zapisywania informacji tooa zakresu, który nie jest oczekiwany.

## <a name="toodetect-mapping-differences"></a>różnice mapowania toodetect
Witaj [metody DetectMappingDifferences](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.detectmappingdifferences.aspx) wybiera i zwraca jedną hello niezależnego fragmentu map (lokalnego lub globalnego) jako źródło hello prawdy i uzgadnia mapowanie na obu mapach niezależnego fragmentu (GSM i LSM).

   ```
   rm.DetectMappingDifferences(location, shardMapName);
   ```

* Witaj *lokalizacji* określa hello nazwy serwera i bazy danych. 
* Witaj *shardMapName* parametru jest nazwa mapy hello niezależnego fragmentu. Jest to tylko wymagane, jeśli wiele map niezależnego fragmentu są zarządzane przez hello samego menedżera mapy niezależnego fragmentu. Opcjonalny. 

## <a name="tooresolve-mapping-differences"></a>różnice mapowania tooresolve
Witaj [metody ResolveMappingDifferences](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.resolvemappingdifferences.aspx) wybiera jeden hello niezależnego fragmentu map (lokalnego lub globalnego) jako źródło hello prawdy i uzgadnia mapowanie na obu mapach niezależnego fragmentu (GSM i LSM).

   ```
   ResolveMappingDifferences (RecoveryToken, MappingDifferenceResolution.KeepShardMapping);
   ```

* Witaj *RecoveryToken* parametru wylicza hello różnice w mapowaniach hello hello GSM i hello LSM dla określonych niezależnego fragmentu hello. 
* Witaj [wyliczenie MappingDifferenceResolution](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.mappingdifferenceresolution.aspx) jest używane tooindicate hello metody rozpoznawania hello różnica między hello niezależnego fragmentu mapowania. 
* **MappingDifferenceResolution.KeepShardMapping** zalecane jest podczas hello LSM zawiera hello mapowanie dokładne i w związku z tym mapowanie hello w niezależnych hello powinna być używana. Dotyczy to zwykle hello jest trybu failover: hello niezależnych znajduje się teraz na nowym serwerze. Ponieważ najpierw należy usunąć niezależnych hello hello GSM (przy użyciu metody RecoveryManager.DetachShard hello), mapowanie już nie istnieje na powitania GSM. W związku z tym hello LSM musi być używane toore-ustanowić hello niezależnego fragmentu mapowania.

## <a name="attach-a-shard-toohello-shardmap-after-a-shard-is-restored"></a>Dołącz toohello niezależnego fragmentu ShardMap po przywróceniu niezależnego fragmentu
Witaj [metody AttachShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.recovery.recoverymanager.attachshard.aspx) dołącza hello danego niezależnych toohello niezależnego fragmentu mapy. Następnie wykrycia niespójności mapy niezależnego fragmentu i aktualizuje niezależnego fragmentu hello toomatch mapowania hello w punkcie hello hello niezależnego fragmentu przywracania. Przyjęto, tej bazy danych hello jest również tooreflect zmieniono nazwę hello oryginalna nazwa bazy danych (przed niezależnych hello została przywrócona), ponieważ hello punktu w czasie przywracania domyślne nową bazę danych tooa dołączony hello sygnatury czasowej. 

   ```
   rm.AttachShard(location, shardMapName)
   ``` 

* Witaj *lokalizacji* parametr jest hello nazwę serwera i nazwę bazy danych, niezależnych hello dołączony. 
* Witaj *shardMapName* parametru jest nazwa mapy hello niezależnego fragmentu. Jest to tylko wymagana, gdy wielu map niezależnego fragmentu są zarządzane przez hello samego menedżera mapy niezależnego fragmentu. Opcjonalny. 

W tym przykładzie dodaje niezależnego fragmentu mapy niezależnego fragmentu toohello przywrócono ostatnio z wcześniejszego punktu w stanu. Ponieważ hello niezależnego fragmentu (to znaczy hello mapowanie niezależnych hello w hello LSM) została przywrócona, jest potencjalnie niezgodnych z wpisu niezależnego fragmentu hello hello GSM. Poza tym przykładowy kod niezależnych hello została przywrócona i zmieniono jego nazwę oryginalną nazwę toohello hello bazy danych. Ponieważ został przywrócony, zakłada się mapowanie hello w hello LSM jest hello zaufanych mapowania. 

   ```
   rm.AttachShard(s.Location, customerMap); 
   var gs = rm.DetectMappingDifferences(s.Location); 
      foreach (RecoveryToken g in gs) 
       { 
       rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
       } 
   ```

## <a name="updating-shard-locations-after-a-geo-failover-restore-of-hello-shards"></a>Trwa aktualizowanie lokalizacji niezależnego fragmentu po przełączeniu geograficznie (przywracanie) odłamków hello
W przypadku awarię geograficznie hello dodatkowej bazy danych jest udostępniane zapisu i staje się hello nowe podstawowej bazy danych. Witaj nazwy serwera hello i potencjalnie bazy danych hello (w zależności od konfiguracji), może być inny niż oryginalny podstawowy hello. W związku z tym hello wpisów mapowania dla niezależnych hello w hello GSM i LSM musi być stałą. Podobnie jeśli hello bazy danych jest przywracane tooa inną nazwę lub lokalizację lub tooan wcześniejszego punktu w czasie, może to spowodować niespójności w hello niezależnego fragmentu mapowania. Hello niezależnego fragmentu mapy Manager obsługuje dystrybucji hello otwarte połączenia toohello poprawną bazą danych. Dystrybucji są oparte na danych hello mapy niezależnego fragmentu hello i wartość hello hello dzielenia na fragmenty klucza, który jest elementem docelowym hello żądania aplikacji hello. Po przełączeniu geograficznie te informacje muszą zostać zaktualizowane nazwy serwera dokładne hello, nazwy bazy danych oraz mapowanie niezależnych hello odzyskanej bazy danych. 

## <a name="best-practices"></a>Najlepsze praktyki
Geograficznie pracy w trybie failover i odzyskiwania są operacje zazwyczaj zarządza administrator chmury aplikacji hello celowo przy użyciu jednej z funkcjach ciągłości biznesowej baz danych SQL Azure. Planowanie ciągłości biznesowej wymaga procesów, procedury i środki tooensure, że operacje biznesowe można nadal bez przeszkód. Witaj metody dostępne jako część hello klasy RecoveryManager powinien być używany w tym hello tooensure przepływu pracy GSM i LSM są aktualizowane oparte na powitania odzyskiwania działania podjęte. Istnieje pięć podstawowych kroków tooproperly zapewnienie hello GSM i LSM odzwierciedlają hello dokładnych informacji po wystąpieniu zdarzenia pracy awaryjnej. Witaj tooexecute kodu aplikacji, które tych kroków można zintegrować istniejących narzędzi i przepływ pracy. 

1. Pobrać hello RecoveryManager z hello ShardMapManager. 
2. Odłączyć hello starego niezależnego fragmentu z hello niezależnego fragmentu mapy.
3. Dołącz hello nowy identyfikator niezależnego fragmentu toohello niezależnego fragmentu mapy, w tym hello nowej lokalizacji niezależnego fragmentu.
4. Wykrył niespójności w hello mapowanie między hello GSM i LSM. 
5. Rozwiąż problemy dotyczące różnic między hello GSM i hello LSM, ufających hello LSM. 

W tym przykładzie przeprowadza hello następujące kroki:

1. Usuwa odłamków z hello mapy niezależnego fragmentu odzwierciedlenia lokalizacji niezależnego fragmentu przed hello zdarzenia pracy awaryjnej.
2. Dołącza odłamków toohello mapy niezależnego fragmentu odbicia hello nowych niezależnego fragmentu lokalizacji (parametr hello "Configuration.SecondaryServer" jest hello nowej nazwy serwera, ale hello same Nazwa bazy danych).
3. Pobiera tokeny odzyskiwania hello przez wykrywania różnic mapowania między hello GSM i hello LSM dla każdego niezależnego fragmentu. 
4. Rozpoznaje niespójności hello ufających mapowanie hello z hello LSM każdego niezależnego fragmentu. 
   
   ```
   var shards = smm.GetShards(); 
   foreach (shard s in shards) 
   { 
     if (s.Location.Server == Configuration.PrimaryServer) 
   
         { 
          ShardLocation slNew = new ShardLocation(Configuration.SecondaryServer, s.Location.Database); 
   
          rm.DetachShard(s.Location); 
   
          rm.AttachShard(slNew); 
   
          var gs = rm.DetectMappingDifferences(slNew); 
   
          foreach (RecoveryToken g in gs) 
            { 
               rm.ResolveMappingDifferences(g, MappingDifferenceResolution.KeepShardMapping); 
            } 
        } 
    } 
   ```

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-database-recovery-manager/recovery-manager.png

