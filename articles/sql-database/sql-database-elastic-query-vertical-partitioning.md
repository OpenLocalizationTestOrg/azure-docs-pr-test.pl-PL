---
title: aaaQuery w chmurze baz danych z innym schematem | Dokumentacja firmy Microsoft
description: "jak tooset się kwerendy między bazami danych z partycji pionowej"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>Zapytanie dla baz danych chmury z różnych schematach (wersja zapoznawcza)
![Zapytanie między tabelami w różnych baz danych][1]

W pionie na partycje bazy danych używać różnych zestawów tabel na różnych baz danych. Oznacza to, że schemat hello różni się w różnych baz danych. Na przykład wszystkie tabele spisu są na jedną bazę danych, gdy wszystkie tabele powiązane ewidencjonowania aktywności znajdują się w drugiej bazy danych. 

## <a name="prerequisites"></a>Wymagania wstępne
* Witaj, użytkownik musi mieć uprawnienie ALTER ANY zewnętrznego źródła danych. To uprawnienie jest dołączany hello uprawnienie ALTER DATABASE.
* Uprawnienia ALTER ANY zewnętrznego źródła danych są wymagane toorefer toohello podstawowego źródła danych.

## <a name="overview"></a>Omówienie

> [!NOTE]
> W odróżnieniu od z partycjonowania poziomy tych instrukcji DDL nie zależą od Definiowanie warstwą danych z mapą niezależnego fragmentu za pomocą biblioteki klienta elastycznej bazy danych hello.
>

1. [TWORZENIE KLUCZA GŁÓWNEGO](https://msdn.microsoft.com/library/ms174382.aspx)
2. [UTWÓRZ BAZĘ DANYCH O ZAKRESIE POŚWIADCZEŃ](https://msdn.microsoft.com/library/mt270260.aspx)
3. [TWORZENIE ZEWNĘTRZNEGO ŹRÓDŁA DANYCH](https://msdn.microsoft.com/library/dn935022.aspx)
4. [TWORZENIE TABELI ZEWNĘTRZNEJ](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>Tworzenie klucza głównego bazy danych i poświadczeń
poświadczenie Hello jest używany przez hello elastycznej zapytania tooconnect tooyour zdalnych baz danych.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Upewnij się, że hello `<username>` nie zawiera żadnych **"@servername"** sufiks. 
>

## <a name="create-external-data-sources"></a>Tworzenie zewnętrznych źródeł danych
Składnia:

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> Parametr typu Hello musi ustawić także**RDBMS**. 
>

### <a name="example"></a>Przykład
Witaj poniższy przykład przedstawia użycie hello hello instrukcji CREATE zewnętrznych źródeł danych. 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

tooretrieve hello listę bieżących źródeł danych zewnętrznych: 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>Tabele zewnętrzne
Składnia:

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>Przykład
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

Hello poniższy przykład przedstawia, jak tooretrieve hello listy tabel zewnętrznych z hello bieżąca baza danych: 

    select * from sys.external_tables; 

### <a name="remarks"></a>Uwagi
Elastyczne zapytania rozszerza hello istniejącej tabeli zewnętrznej składni toodefine tabel zewnętrznych korzystających z zewnętrznych źródeł danych typu RDBMS. Definicja tabeli zewnętrznej dla partycjonowanie pionowe obejmuje hello następujące aspekty: 

* **Schemat**: hello tabeli zewnętrznej DDL definiuje schemat, który można użyć zapytań. Schemat Hello w definicji tabeli zewnętrznej wymaga schematu hello toomatch hello tabel w zdalnej bazy danych hello przechowywania hello rzeczywiste dane. 
* **Odwołanie do zdalnej bazy danych**: hello tabeli zewnętrznej DDL odwołuje się tooan zewnętrznego źródła danych. Witaj zewnętrznego źródła danych określa nazwę serwera logicznego hello i zdalnej bazy danych hello przechowywania danych rzeczywistych tabeli hello Nazwa bazy danych. 

Za pomocą zewnętrznego źródła danych, zgodnie z opisem w poprzedniej sekcji hello, hello tabel zewnętrznych toocreate składnia jest następująca: 

Klauzula DATA_SOURCE Hello definiuje hello zewnętrznego źródła danych (tj. hello zdalnej bazy danych w przypadku partycjonowanie pionowe) służący do hello tabeli zewnętrznej.  

klauzule SCHEMA_NAME i OBJECT_NAME Hello odpowiednio zawierają hello możliwości toomap hello tabeli zewnętrznej definicji tooa tabeli do innego schematu na hello zdalnej bazy danych lub tabeli tooa pod inną nazwą. Jest to przydatne, jeśli chcesz toodefine widoku wykazu tooa tabeli zewnętrznej lub DMV na zdalnej bazy danych — lub w innej sytuacji, gdy nazwa tabeli zdalnej hello jest już zajęta lokalnie.  

Witaj następująca instrukcja DDL porzuca istniejącej definicji tabeli zewnętrznej z katalogu lokalnego hello. Nie ma ona wpływu hello zdalnej bazy danych. 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**Uprawnienia CREATE/DROP tabeli zewnętrznej**: dla tabeli zewnętrznej DDL, który jest także niezbędne toorefer toohello źródła danych, potrzebne są uprawnienia ALTER ANY zewnętrznego źródła danych.  

## <a name="security-considerations"></a>Zagadnienia związane z zabezpieczeniami
Użytkownicy z tabeli zewnętrznej toohello dostępu jest automatycznie uzyskują dostęp toohello zdalnego tabel w obszarze hello poświadczenia podane w definicji źródła danych zewnętrznych hello. Należy uważnie zarządzać tabeli zewnętrznej toohello dostępu w kolejności tooavoid niepożądane podniesienie uprawnień poprzez hello poświadczenia hello zewnętrznego źródła danych. Regularne uprawnienia SQL można tooGRANT używane lub ODWOŁAĆ dostępu tooan zewnętrzna tabela, tak jakby był on zwykłą tabelę.  

## <a name="example-querying-vertically-partitioned-databases"></a>Przykład: zapytanie w pionie na partycje baz danych
Witaj następujące zapytanie wykonuje trzystopniowego sprzężenie hello dwóch tabel lokalnych dla zleceń i kolejność wierszy tabeli zdalnej hello dla klientów. Jest to przykład przypadek użycia danych hello odwołania dla elastycznej zapytania: 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


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
Regularne tooconnect ciągów połączenia programu SQL Server można użyć toodatabases narzędzi integracji BI i danych na serwerze bazy danych SQL hello, który ma elastycznej zapytań włączone i tabel zewnętrznych zdefiniowane. Upewnij się, czy program SQL Server jest obsługiwana jako źródło danych dla własnych narzędzi. Następnie można znaleźć toohello elastycznej zapytanie do bazy danych i jego tabele zewnętrzne, podobnie jak wszystkie inne bazy danych SQL Server czy można połączyć toowith własnych narzędzi. 

## <a name="best-practices"></a>Najlepsze praktyki
* Upewnij się, że tej bazy danych punktu końcowego elastycznej zapytania hello została podana zdalnej bazy danych programu access toohello przez umożliwienie dostępu do usług platformy Azure w konfiguracji zapory bazy danych SQL. Upewnij się również to poświadczenie hello danych zewnętrznych hello definicji źródła może pomyślnie zalogować się do zdalnej bazy danych hello i ma tabeli zdalnej tooaccess hello hello uprawnienia.  
* Zapytania elastycznej działa najlepiej dla zapytań gdzie na powitania zdalnych baz danych można wykonać większość obliczeń hello. Zwykle uzyskać najlepszą wydajność zapytań hello z predykatu filtru selektywnego, które można oszacować na powitania zdalnych baz danych lub sprzężenia, które mogą być wykonywane całkowicie na powitania zdalnej bazy danych. Innymi wzorcami zapytań może być konieczne tooload dużych ilości danych z hello zdalnej bazy danych i mogą działać nieprawidłowo. 

## <a name="next-steps"></a>Następne kroki

* Omówienie elastycznej zapytania, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).
* Samouczek partycjonowania pionowego, zobacz [wprowadzenie do korzystania z bazy danych między kwerendy (partycjonowanie pionowe)](sql-database-elastic-query-getting-started-vertical.md).
* Samouczek poziomych partycji (dzielenia na fragmenty), zobacz [wprowadzenie elastycznej zapytania poziome partycjonowania (dzielenia na fragmenty)](sql-database-elastic-query-getting-started.md).
* Dla zapytań dotyczących danych poziomie podzielonym na partycje i składnię i przykład, zobacz [zapytań w poziomie na partycje danych)](sql-database-elastic-query-horizontal-partitioning.md)
* Zobacz [sp\_wykonania \_zdalnego](https://msdn.microsoft.com/library/mt703714) dla procedury składowanej, która wykonuje instrukcję Transact-SQL w jednym zdalnej bazy danych SQL Azure lub zestaw baz danych, służąc jako odłamków w poziomie schemat partycjonowania.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
