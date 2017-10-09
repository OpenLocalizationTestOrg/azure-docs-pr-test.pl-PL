---
title: "aaaData zależnych routingu w usłudze Azure SQL Database | Dokumentacja firmy Microsoft"
description: "Jak toouse hello klasy ShardMapManager w aplikacjach .NET dla danych zależne od routingu, funkcja podzielonej baz danych w bazie danych SQL Azure"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a>Routing zależny od danych
**Dane zależne routingu** jest hello możliwości toouse hello danych z zapytania tooroute hello żądania tooan odpowiednie bazy danych. Podczas pracy z bazy danych podzielonej jest wzorzec podstawowych. kontekst żądania Hello mogą być również używane tooroute hello żądania, zwłaszcza, jeśli klucz dzielenia na fragmenty hello nie jest częścią zapytania hello. Każdej określonej kwerendy lub transakcji w aplikacji przy użyciu routingu zależnych danych jest ograniczone tooaccessing pojedynczej bazy danych na żądanie. Witaj narzędzi elastycznej bazy danych SQL Azure, marszruty jest realizowane za pomocą hello  **[klasy ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  w aplikacjach ADO.NET.

Aplikacja Hello nie jest konieczne tootrack różne parametry połączenia lub skojarzone z inną wycinków danych w środowisku podzielonej hello lokalizacji bazy danych. Zamiast tego hello [Menedżera Map niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md) otwiera połączeń toohello poprawne baz danych w razie potrzeby na podstawie hello danych mapy niezależnego fragmentu hello i wartość hello hello dzielenia na fragmenty klucza, który jest elementem docelowym hello żądania aplikacji hello. klucz Hello jest zwykle hello *customer_id*, *tenant_id*, *date_key*, lub niektóre określonym identyfikatorze, który jest parametrem podstawowym hello żądania bazy danych). 

Aby uzyskać więcej informacji, zobacz [skalowanie limit programu SQL Server z routingiem zależnych danych](https://technet.microsoft.com/library/cc966448.aspx).

## <a name="download-hello-client-library"></a>Pobierz powitania klienta biblioteki
Klasa hello tooget, hello instalacji [elastycznej bazy danych klienta biblioteki](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a>Przy użyciu ShardMapManager w danych zależnych aplikacji routingu
Aplikacje powinny wystąpienia hello **ShardMapManager** podczas inicjowania przy użyciu wywołania fabryki hello  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**. W tym przykładzie zarówno **ShardMapManager** i określony **ShardMap** zawierający są zainicjowane. W tym przykładzie przedstawiono hello GetSqlShardMapManager i [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) metody.

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a>Użyj najniższy poświadczeń uprawnień możliwe uzyskania hello niezależnego fragmentu mapy
Jeśli aplikacja nie jest manipulowanie hello niezależnego fragmentu mapy, używany w metodzie fabryki hello poświadczenia hello powinni mieć uprawnienia tylko do odczytu na powitania **globalne mapy niezależnego fragmentu** bazy danych. Te poświadczenia zwykle różnią się od menedżera map niezależnego fragmentu toohello poświadczenia używane tooopen połączenia. Zobacz też [poświadczenia używane biblioteki klienta elastycznej bazy danych hello tooaccess](sql-database-elastic-scale-manage-credentials.md). 

## <a name="call-hello-openconnectionforkey-method"></a>Wywołaj metodę OpenConnectionForKey hello
Witaj  **[metody ShardMap.OpenConnectionForKey](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  zwraca połączenia ADO.Net gotowe do wydania poleceń toohello odpowiednie bazy danych na podstawie wartości hello hello **klucza**parametru. Identyfikator niezależnego fragmentu informacje są buforowane w aplikacji hello przez hello **ShardMapManager**, więc te żądania nie obejmują zazwyczaj wyszukiwania w bazie danych przed hello **globalne mapy niezależnego fragmentu** bazy danych. 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* Witaj **klucza** parametr jest używany jako klucz wyszukiwania do hello niezależnego fragmentu mapy toodetermine hello odpowiednie bazy danych dla żądania hello. 
* Witaj **connectionString** jest toopass używanych tylko poświadczenia użytkownika hello hello żądanego połączenia. Nie nazwy bazy danych lub nazwa serwera znajdują się w tym *connectionString* ponieważ metoda hello określi hello bazy danych i serwera przy użyciu hello **ShardMap**. 
* Witaj  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  powinna być ustawiona zbyt**ConnectionOptions.Validate** mogą ulec zmianie w środowisku, gdzie mapuje niezależnego fragmentu czy wierszy może przenoszenia baz danych tooother jako wynik operacji dzielenie i scalanie. Obejmuje to mapa lokalnych niezależnego fragmentu toohello zapytania krótkie hello docelowej bazy danych (nie toohello globalne niezależnych map) przed połączenia hello jest dostarczany toohello aplikacji. 

W przypadku niepowodzenia weryfikacji hello względem mapy niezależnych lokalne powitania (co oznacza, że pamięć podręczna hello jest niepoprawny) hello Menedżera Map niezależnego fragmentu będzie hello globalne niezależnych mapy tooobtain hello nowe poprawne wartość zapytania do wyszukiwania hello aktualizacji pamięci podręcznej hello i uzyskać i zwracają hello połączenie z odpowiednią bazą danych. 

Użyj **ConnectionOptions.None** tylko podczas zmiany mapowania niezależnego fragmentu nie powinny podczas, gdy aplikacja jest w trybie online. W takim przypadku hello buforowane wartości można założyć tooalways są poprawne i bezpiecznie pominięte hello bardzo obustronne weryfikacji wywołania toohello docelowej bazy danych. Która zmniejsza ruch bazy danych. Witaj **connectionOptions** również mogą zostać ustawione za pomocą wartości w tooindicate pliku konfiguracji, czy zmiany dzielenia na fragmenty są oczekiwane lub nie w danym okresie czasu.  

W tym przykładzie użyto hello wartość klucza **CustomerID**za pomocą **ShardMap** obiektu o nazwie **customerShardMap**.  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

Witaj **OpenConnectionForKey** metoda zwraca nową już otwarte połączenia toohello poprawną bazę danych. Połączenia używane w ten sposób nadal w pełni korzystać z buforowania połączenia ADO.Net. Ile transakcji i żądań można spełnić przez jednego niezależnego fragmentu w czasie, powinno to być hello modyfikacji tylko niezbędne w aplikacji już za pomocą ADO.Net. 

Witaj  **[metody OpenConnectionForKeyAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  jest również dostępna w przypadku aplikacji sprawia, że użycie programowanie asynchroniczne z ADO.Net. Jego zachowanie jest hello danych zależnych routingu odpowiednik ADO. W sieci  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  metody.

## <a name="integrating-with-transient-fault-handling"></a>Integrowanie z obsługi błędu przejściowego
Najlepszym rozwiązaniem w tworzeniu aplikacji dostęp do danych w chmurze hello jest tooensure błędów przejściowych są objęte aplikacji hello oraz operacje hello są zwalniane kilka razy przed generowaniem błędu. Wystąpienia błędu przejściowego obsługi dla aplikacji w chmurze została szczegółowo opisana w [obsługi błędów przejściowych](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx). 

Obsługa błędu przejściowego mogą współistnieć naturalnie wzorem hello danych zależnych routingu. Hello decydujące znaczenie jest tooretry hello danych żądanie dostępu tym hello **przy użyciu** bloku uzyskiwanej hello zależne od danych routingu połączenia. w powyższym przykładzie Hello można ulegną w następujący sposób (Uwaga: zmiana wyróżnione). 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a>Przykład — danych zależnych routingu z obsługą błędu przejściowego
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


Pakiety obsługi błędu przejściowego tooimplement niezbędne są pobierane automatycznie podczas budowania hello elastycznej bazy danych przykładowej aplikacji. Pakiety są także dostępne oddzielnie w [Enterprise Library – bloku aplikacji obsługi błędów przejściowych](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/). Użyj wersji 6.0 lub nowszej. 

## <a name="transactional-consistency"></a>Spójności transakcyjnej
Wszystkie operacje lokalnego tooa niezależnych gwarancję właściwości transakcyjnych. Na przykład transakcji przesłane za pośrednictwem routingu zależne od danych wykonywania w zakresie hello hello docelowy identyfikator niezależnego fragmentu hello połączenia. W tej chwili jest nie możliwości przewidzianych rejestrowanie wiele połączeń w transakcji, a w związku z tym nie bez gwarancji transakcyjne dla operacji wykonywanych przez odłamków.

## <a name="next-steps"></a>Następne kroki
Zobacz toodetach niezależnych lub tooreattach niezależnych [przy użyciu hello RecoveryManager klasy toofix niezależnego fragmentu mapy problemów](sql-database-elastic-database-recovery-manager.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

