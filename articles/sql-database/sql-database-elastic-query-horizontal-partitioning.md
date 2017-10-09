---
title: aaaReporting dla baz danych w chmurze skalowalnych w poziomie | Dokumentacja firmy Microsoft
description: "jak tooset się elastycznej zapytania dotyczące poziomych partycji"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: f86eccb8-6323-4ba7-8559-8a7c039049f3
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: mlandzic
ms.openlocfilehash: 78986c2040bf308195bf7c77e64d4f37273fcf36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reporting-across-scaled-out-cloud-databases-preview"></a>Raportowanie w chmurze skalowalnych w poziomie bazy danych (wersja zapoznawcza)
![Wysyłanie zapytań na odłamków][1]

Bazy danych podzielonej rozpowszechniają wiersze danych skalowanej warstwy. Schemat Hello jest takie same na wszystkich uczestniczących baz danych, nazywany również poziomych partycji. Przy użyciu elastycznej kwerendy, możesz utworzyć raporty, obejmujące wszystkie bazy danych podzielonej bazy danych.

Aby uzyskać szybki start, zobacz [raportowania dla baz danych w chmurze skalowalnych w poziomie](sql-database-elastic-query-getting-started.md).

Podzielonej baz danych, zobacz [zapytania dla baz danych chmury z różnych schematach](sql-database-elastic-query-vertical-partitioning.md). 

## <a name="prerequisites"></a>Wymagania wstępne
* Tworzenie za pomocą biblioteki klienta elastycznej bazy danych hello mapy niezależnego fragmentu. zobacz [zarządzania mapy niezależnego fragmentu](sql-database-elastic-scale-shard-map-management.md). Lub użyj hello przykładową aplikację w [wprowadzenie do narzędzi elastycznej bazy danych](sql-database-elastic-scale-get-started.md).
* Zobacz też [migracji istniejącej bazy danych bazy danych poza tooscaled](sql-database-elastic-convert-to-use-elastic-tools.md).
* Witaj, użytkownik musi mieć uprawnienie ALTER ANY zewnętrznego źródła danych. To uprawnienie jest dołączany hello uprawnienie ALTER DATABASE.
* Uprawnienia ALTER ANY zewnętrznego źródła danych są wymagane toorefer toohello podstawowego źródła danych.

## <a name="overview"></a>Omówienie
Te instrukcje utwórz warstwę danych podzielonej reprezentację metadanych hello w hello elastycznej zapytanie do bazy danych. 

1. [TWORZENIE KLUCZA GŁÓWNEGO](https://msdn.microsoft.com/library/ms174382.aspx)
2. [UTWÓRZ BAZĘ DANYCH O ZAKRESIE POŚWIADCZEŃ](https://msdn.microsoft.com/library/mt270260.aspx)
3. [TWORZENIE ZEWNĘTRZNEGO ŹRÓDŁA DANYCH](https://msdn.microsoft.com/library/dn935022.aspx)
4. [TWORZENIE TABELI ZEWNĘTRZNEJ](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="11-create-database-scoped-master-key-and-credentials"></a>1.1 utworzyć klucz główny bazy danych i poświadczeń
poświadczenie Hello jest używany przez hello elastycznej zapytania tooconnect tooyour zdalnych baz danych.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Upewnij się, że hello *"\<username\>"* nie zawiera żadnych *"@servername"* sufiks. 
> 
> 

## <a name="12-create-external-data-sources"></a>1.2 Tworzenie zewnętrznych źródeł danych
Składnia:

    <External_Data_Source> ::=    
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH                                              
            (TYPE = SHARD_MAP_MANAGER,
                       LOCATION = '<fully_qualified_server_name>',
            DATABASE_NAME = ‘<shardmap_database_name>',
            CREDENTIAL = <credential_name>, 
            SHARD_MAP_NAME = ‘<shardmapname>’ 
                   ) [;] 

### <a name="example"></a>Przykład
    CREATE EXTERNAL DATA SOURCE MyExtSrc 
    WITH 
    ( 
        TYPE=SHARD_MAP_MANAGER,
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ShardMapDatabase', 
        CREDENTIAL= SMMUser, 
        SHARD_MAP_NAME='ShardMap' 
    );

Pobieranie listy hello bieżącego zewnętrznych źródeł danych: 

    select * from sys.external_data_sources; 

Witaj zewnętrznego źródła danych odwołuje się do mapy niezależnego fragmentu. Elastyczne zapytanie używa następnie hello zewnętrznego źródła danych i hello źródłowego niezależnego fragmentu mapy tooenumerate hello bazy danych należące do warstwy danych hello. Hello tych samych poświadczeń są używane tooread hello niezależnego fragmentu mapy i tooaccess hello danych na powitania odłamków podczas przetwarzania hello elastycznej zapytania. 

## <a name="13-create-external-tables"></a>1.3 tworzenia tabel zewnętrznych
Składnia:  

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name  
        ( { <column_definition> } [ ,...n ])     
        { WITH ( <sharded_external_table_options> ) }
    ) [;]  

    <sharded_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>,       
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 
      DISTRIBUTION = SHARDED(<sharding_column_name>) | REPLICATED |ROUND_ROBIN

**Przykład**

    CREATE EXTERNAL TABLE [dbo].[order_line]( 
         [ol_o_id] int NOT NULL, 
         [ol_d_id] tinyint NOT NULL,
         [ol_w_id] int NOT NULL, 
         [ol_number] tinyint NOT NULL, 
         [ol_i_id] int NOT NULL, 
         [ol_delivery_d] datetime NOT NULL, 
         [ol_amount] smallmoney NOT NULL, 
         [ol_supply_w_id] int NOT NULL, 
         [ol_quantity] smallint NOT NULL, 
         [ol_dist_info] char(24) NOT NULL 
    ) 

    WITH 
    ( 
        DATA_SOURCE = MyExtSrc, 
         SCHEMA_NAME = 'orders', 
         OBJECT_NAME = 'order_details', 
        DISTRIBUTION=SHARDED(ol_w_id)
    ); 

Pobieranie listy hello tabel zewnętrznych z hello bieżąca baza danych: 

    SELECT * from sys.external_tables; 

toodrop tabel zewnętrznych:

    DROP EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name[;]

### <a name="remarks"></a>Uwagi
Witaj danych\_hello zewnętrznego źródła danych (mapy niezależnego fragmentu) używany do tabeli zewnętrznej hello definiuje klauzuli źródła.  

Witaj SCHEMATU\_nazwy i obiektu\_klauzule Nazwa mapy Tabela tooa definicji tabeli zewnętrznej hello w innym schematem. Pominięcie schematu hello obiektu zdalnego hello przyjęto, że toobe "właściciela" i jego nazwa przyjęto, że nazwa tabeli zewnętrznej identyczne toohello toobe definiowanego. Jest to przydatne, zajętej hello nazwę zdalnego tabeli w bazie danych hello w odpowiednim miejscu toocreate hello zewnętrznych. Na przykład chcesz toodefine tooget tabeli zewnętrznej zagregowany widok widoków wykazu lub widoków DMV skalowanej danych w warstwie. Ponieważ widoków wykazu i widoków DMV już istnieje lokalnie, nie można używać ich nazwy hello definicji tabeli zewnętrznej. Zamiast tego użyj innej nazwy i użyj widoku wykazu hello lub hello DMV jego nazwę w hello SCHEMATU\_nazwę i/lub obiekt\_klauzule nazwy. (Zobacz poniższy przykład hello). 

Klauzula dystrybucji Hello określa hello danych dystrybucji używany dla tej tabeli. procesor zapytań Hello wykorzystuje hello informacji dostępnych w hello dystrybucji klauzuli toobuild hello najbardziej efektywny plany zapytań.  

1. **PODZIELONEJ** oznacza danych jest poziomo podzielonym na partycje w hello baz danych. Partycjonowanie klucza dystrybucji danych hello jest hello Hello **< sharding_column_name >** parametru.
2. **REPLIKOWANE** oznacza, że identycznych kopii tabeli hello są obecne w każdej bazie danych. Jest Twoje tooensure odpowiedzialność hello repliki są identyczne dla hello baz danych.
3. **ROUND\_działania OKRĘŻNEGO** oznacza tabeli hello poziomo na partycje za pomocą metody dystrybucji aplikacji zależnych. 

**Odwołanie do warstwy danych**: hello tabeli zewnętrznej DDL odwołuje się tooan zewnętrznego źródła danych. Witaj zewnętrznego źródła danych określa mapy niezależnego fragmentu, dzięki czemu dostępne tabeli zewnętrznej hello toolocate niezbędne informacje hello wszystkich baz danych hello warstwę danych. 

### <a name="security-considerations"></a>Zagadnienia związane z zabezpieczeniami
Użytkownicy z tabeli zewnętrznej toohello dostępu jest automatycznie uzyskują dostęp toohello zdalnego tabel w obszarze hello poświadczenia podane w definicji źródła danych zewnętrznych hello. Unikaj niepożądane podniesienia uprawnień za pomocą hello poświadczenia hello zewnętrznego źródła danych. Użyj GRANT lub REVOKE dla tabeli zewnętrznej, tak jakby był on zwykłą tabelę.  

Po zdefiniowaniu zewnętrznym źródle danych i tabele zewnętrzne mogą teraz używać pełnej T-SQL w tabelach zewnętrznych.

## <a name="example-querying-horizontal-partitioned-databases"></a>Przykład: badanie poziome partycjonowane baz danych
Hello następujące zapytanie wykonuje sprzężenie trzystopniowo magazynów, zamówienia i kolejność wierszy i używa kilku wartości zagregowanych i selektywnego filtru. Zakłada się (1) poziomych partycji (dzielenia na fragmenty), a (2) magazynów, zamówienia i kolejność wierszy są podzielonej przez hello w kolumnie Identyfikator magazynu, a hello zapytania elastycznej mogą kolokuj sprzężenia hello na powitania odłamków i przetwarzać hello kosztowne część zapytania hello na powitania odłamków równolegle. 

    select  
         w_id as warehouse,
         o_c_id as customer,
         count(*) as cnt_orderline,
         max(ol_quantity) as max_quantity,
         avg(ol_amount) as avg_amount, 
         min(ol_delivery_d) as min_deliv_date
    from warehouse 
    join orders 
    on w_id = o_w_id
    join order_line 
    on o_id = ol_o_id and o_w_id = ol_w_id 
    where w_id > 100 and w_id < 200 
    group by w_id, o_c_id 

## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Przechowywana procedura zdalne wykonywanie kodu T-SQL: sp\_execute_remote
Elastyczne zapytania wprowadza również procedury przechowywanej, która zapewnia bezpośredni dostęp odłamków toohello. Hello jest wywoływana procedura składowana [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) i tooexecute używane zdalne procedury składowane lub kod T-SQL na powitania zdalnych baz danych. Trwa hello następujące parametry: 

* Nazwa źródła danych (nvarchar): Nazwa hello hello zewnętrznego źródła danych RDBMS typu. 
* Zapytania (nvarchar): hello T-SQL toobe zapytanie wykonywane na każdej niezależnego fragmentu. 
* Deklaracja parametru (nvarchar) - opcjonalne: ciąg zawierający definicje typów danych parametrów hello hello parametr zapytania (na przykład sp_executesql). 
* Lista wartości parametrów - opcjonalne: rozdzielana przecinkami lista wartości parametrów (na przykład sp_executesql).

Hello sp\_wykonania\_zewnętrzne źródło danych podane w podanej instrukcji T-SQL w bazach danych, zdalnego hello hello wywołania parametry tooexecute hello hello używa zdalnego. Poświadczenie hello hello dane zewnętrzne źródło tooconnect toohello shardmap Menedżera bazy danych i baz danych, zdalnego hello jest używany.  

Przykład: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 

## <a name="connectivity-for-tools"></a>Połączenie narzędzi
Użyj regularne tooconnect ciągów połączenia programu SQL Server aplikacji, danych i BI integracji narzędzia toohello bazy danych za pomocą definicji tabeli zewnętrznej. Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi. Odwoływanie hello elastycznej kwerendy bazy danych jak dowolnego innego programu SQL Server połączone bazy danych toohello narzędzia, a następnie użyj tabel zewnętrznych z narzędzia lub aplikacji, tak jakby były lokalne tabele. 

## <a name="best-practices"></a>Najlepsze praktyki
* Upewnij się, że podano tej bazy danych punktu końcowego elastycznej zapytania hello shardmap toohello dostępu do bazy danych i wszystkie odłamków za pośrednictwem powitalne zapory bazy danych SQL.  
* Sprawdza, czy lub wymusić hello danych dystrybucji zdefiniowanych przez tabelę zewnętrzną hello. Jeśli dystrybucji rzeczywiste dane jest inna niż określona w definicji tabeli dystrybucji hello, kwerend może dać nieoczekiwane wyniki. 
* Elastyczne zapytania aktualnie nie wykonuje eliminacji niezależnego fragmentu podczas predykaty za pośrednictwem klucza dzielenia na fragmenty hello pozwala Wyklucz toosafely niektórych odłamków z przetwarzania.
* Zapytania elastycznej działa najlepiej dla zapytań gdzie na powitania odłamków można wykonać większość obliczeń hello. Zwykle uzyskać hello najlepszą wydajność zapytań z predykatu filtru selektywnego, które może przyjąć odłamków hello lub sprzężenia za pośrednictwem hello partycjonowania kluczy, które mogą być wykonywane w sposób wyrównany do partycji na wszystkich fragmentów. Innymi wzorcami zapytań może być konieczne tooload dużych ilości danych z węzłem głównym hello odłamków toohello i mogą działać nieprawidłowo

## <a name="next-steps"></a>Następne kroki

* Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).
* Samouczek partycjonowania pionowego, zobacz [wprowadzenie do korzystania z bazy danych między kwerendy (partycjonowanie pionowe)](sql-database-elastic-query-getting-started-vertical.md).
* Dla zapytań dotyczących danych pionowo podzielonym na partycje i składnię i przykład, zobacz [zapytań w pionie na partycje danych)](sql-database-elastic-query-vertical-partitioning.md)
* Samouczek poziomych partycji (dzielenia na fragmenty), zobacz [wprowadzenie elastycznej zapytania poziome partycjonowania (dzielenia na fragmenty)](sql-database-elastic-query-getting-started.md).
* Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-horizontal-partitioning/horizontalpartitioning.png
<!--anchors-->
