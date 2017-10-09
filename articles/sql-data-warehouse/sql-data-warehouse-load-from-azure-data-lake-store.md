---
title: aaaLoad - Azure Data Lake Store tooSQL Data Warehouse | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zewnętrzny PolyBase toouse tabele tooload dane z usługi Azure Data Lake Store do usługi Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a>Ładowanie danych z usługi Azure Data Lake Store do magazynu danych SQL
Ten dokument stanowi wszystkie czynności, które należy tooload własne dane z usługi Azure Data Lake magazyn (ADLS) do usługi SQL Data Warehouse przy użyciu programu PolyBase.
Podczas pracy zapytań ad hoc toorun mogli za pośrednictwem hello danych przechowywanych w ADLS przy użyciu tabel zewnętrznych hello jako najlepsze rozwiązanie zaleca się importowanie danych hello hello SQL Data Warehouse.
Szacowanie czasu: 10 minut, przy założeniu, że masz hello wymagań wstępnych konieczne toocomplete.
W tym samouczku przedstawiono sposób:

1. Utwórz tooload obiekty zewnętrznej bazy danych z usługi Azure Data Lake Store.
2. Połącz tooan Azure Data Lake magazynu katalogu.
3. Ładowanie danych do usługi Azure SQL Data Warehouse.

## <a name="before-you-begin"></a>Przed rozpoczęciem
toorun tego samouczka należy:

* Azure toouse aplikacji usługi Active Directory do usługi uwierzytelniania. toocreate, wykonaj [uwierzytelniania usługi Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)

>[!NOTE] 
> Wymagane hello Identyfikatora klienta, klucz i wartość tokenu punktu końcowego OAuth2.0 z Twojej aplikacji usługi Active Directory tooconnect tooyour usługi Azure Data Lake z magazynu danych SQL. Szczegóły dotyczące sposobu tooget te wartości są w powyższy link hello.
>Uwaga dotycząca rejestracji aplikacji Azure Active Directory użyj hello "Identyfikator aplikacji" jako hello identyfikator klienta.

* SQL Server Management Studio lub SQL Server Data Tools toodownload SSMS i połączenia zobacz [SSMS zapytania](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)

* Wykonaj toocreate jeden magazyn danych SQL Azure: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision

* Azure Data Lake Store, lub nie jest włączone szyfrowanie. Wykonaj jeden toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal




## <a name="configure-hello-data-source"></a>Konfigurowanie hello źródła danych
Program PolyBase używa lokalizacji hello toodefine zewnętrznych obiektów T-SQL i atrybuty hello danych zewnętrznych. Witaj zewnętrznych obiektów są przechowywane w SQL Data Warehouse i hello danych referencyjnych th jest przechowywana zewnętrznie.


###  <a name="create-a-credential"></a>Utwórz poświadczenia
tooaccess Twojego Azure Data Lake przechowywania, konieczne będzie toocreate tooencrypt klucz główny bazy danych klucz tajny poświadczenie używane w hello następnego kroku.
Następnie można utworzyć poświadczenia bazy danych, której są przechowywane poświadczenia główne usługi hello skonfigurowane w usłudze AAD. Dla osób, które zostały użyte PolyBase tooconnect tooWindows obiektach blob magazynu Azure, należy pamiętać, że poświadczenie hello składni jest inny.
tooAzure tooconnect usługi Data Lake Store, należy najpierw **pierwszy** tworzenie aplikacji Azure Active Directory, Utwórz klucz dostępu, a następnie przyznać hello aplikacji dostępu toohello usługi Azure Data Lake zasobów. Instrucitons tooperform znajdują się następujące kroki [tutaj](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a>Utwórz hello zewnętrznego źródła danych
Użyj tej [Tworzenie zewnętrznego źródła danych] [ CREATE EXTERNAL DATA SOURCE] polecenia toostore lokalizacji hello hello danych i hello typu danych.
Witaj ADL URI można znaleźć w hello portalu Azure i www.portal.azure.com.

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a>Skonfiguruj format danych
dane hello tooimport z ADLS, należy toospecify hello zewnętrznego formatu pliku. To polecenie ma toodescribe opcje związane z formatem danych.
Poniżej przedstawiono przykład często używane formacie, który jest plikiem tekstowym rozdzielany potoku.
Szukaj w naszej dokumentacji T-SQL, aby uzyskać pełną listę [Tworzenie zewnętrznych FORMAT pliku][CREATE EXTERNAL FILE FORMAT]

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE
                    )
);
```

## <a name="create-hello-external-tables"></a>Tworzenie tabel zewnętrznych hello
Określono hello danych źródła i format pliku, użytkownik jest tabel zewnętrznych hello toocreate gotowe. Tabele zewnętrzne są interakcje z danymi zewnętrznymi. Program PolyBase używa cyklicznego katalogu przechodzenie tooread wszystkie pliki w wszystkie podkatalogi katalogu hello określony w parametrze lokalizacji hello. Ponadto hello poniższy przykład pokazuje, jak toocreate hello obiektu. Należy toocustomize hello instrukcji toowork z danych hello w ADLS.

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a>Zagadnienia dotyczące tabeli zewnętrznej
Tworzenie tabeli zewnętrznej jest proste, ale istnieją pewne różnice wymagające toobe omówione.

Ładowanie danych przy użyciu programu PolyBase jest silnie typizowane. Oznacza to, że każdy wiersz danych hello jest pozyskanych muszą spełniać definicja schematu tabeli hello.
Jeśli danego wiersza nie jest zgodny z definicji schematu hello, wiersz hello jest odrzucona z hello obciążenia.

Witaj REJECT_TYPE i REJECT_VALUE opcje pozwalają toodefine liczby wierszy lub wartość procentowa danych hello musi znajdować się w tabeli końcowej hello.
Podczas ładowania po osiągnięciu wartości Odrzuć hello obciążenia hello kończy się niepowodzeniem. Najczęstszą przyczyną Hello odrzucone wierszy jest niezgodność definicji schematu.
Na przykład jeśli kolumny niepoprawnie podano schematu hello int, gdy hello dane w pliku hello jest ciągiem, każdy wiersz zakończy się niepowodzeniem tooload.

Witaj Lokalizacja określa hello katalogu najwyższego poziomu tooread danych z.
W takim przypadku, gdyby podkatalogów w obszarze /DimProduct/ PolyBase jaki są importowane wszystkich danych hello w Witaj podkatalogi.

## <a name="load-hello-data"></a>Ładowanie danych hello
tooload dane z usługi Azure Data Lake Store Użyj hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrukcji. Podczas ładowania z CTAS hello używa silnie typizowane tabeli zewnętrznej, które zostały utworzone.

CTAS tworzy nową tabelę i wypełnia hello wyników w instrukcji select. CTAS definiuje hello nowej tabeli toohave hello tej samej kolumny i typy danych jak wyniki hello hello wybierz instrukcji. Po wybraniu wszystkich hello kolumn z tabeli zewnętrznej nową tabelę hello jest repliką hello kolumn i typy danych w tabeli zewnętrznej hello.

W tym przykładzie tworzymy tabeli rozproszonej wyznaczania wartości skrótu o nazwie DimProduct z naszych zewnętrznych DimProduct_external tabeli.

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a>Optymalizacja magazynu kolumn kompresji
Domyślnie usługa SQL Data Warehouse przechowuje hello tabeli jako klastrowany indeks magazynu kolumn. Po zakończeniu obciążenia nie może być niektóre wiersze danych hello skompresowane w hello magazynu kolumn.  Brak z różnych powodów, dlaczego jest to możliwe. toolearn więcej, zobacz [Zarządzaj indeksami magazynu kolumn][manage columnstore indexes].

toooptimize wydajność zapytań i ich kompresji magazynu kolumn po załadowaniu, Odbuduj hello tabeli tooforce hello magazynu kolumn indeksu toocompress wszystkie wiersze hello.

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

Aby uzyskać więcej informacji na temat zachowania indeksy magazynu kolumn, zobacz hello [Zarządzaj indeksami magazynu kolumn] [ manage columnstore indexes] artykułu.

## <a name="optimize-statistics"></a>Optymalizacja statystyki
Najważniejsze dane statystyczne pojedynczej kolumny toocreate jest natychmiast po załadowaniu. Dostępne są niektóre opcje wyboru statystyk. Na przykład jeśli tworzenie statystyk pojedynczej kolumny w każdej kolumnie może potrwać toorebuild długo wszystkie statystyki hello. Jeśli wiesz, że niektóre kolumny nie będą toobe w predykatach kwerendy, można pominąć tworzenie statystyk na podstawie tych kolumn.

Jeśli zdecydujesz toocreate statystyki pojedynczej kolumny w każdej kolumnie każda tabela służy przykładowy kod procedury składowanej hello `prc_sqldw_create_stats` w hello [statystyki] [ statistics] artykułu.

Poniższy przykład Hello jest dobry punkt wyjścia do tworzenia statystyk. W każdej kolumnie w tabeli wymiarów hello i w każdej kolumnie łącząca w tabelach faktów hello tworzy statystyki pojedynczej kolumny. Później można dodać kolumny tabeli faktów tooother statystyki jednego lub wielu kolumn.


## <a name="achievement-unlocked"></a>Osiągnięcia odblokowane!
Dane zostały pomyślnie załadowane do magazynu danych SQL Azure. Dobra robota!

##<a name="next-steps"></a>Następne kroki
Podczas ładowania danych jest hello pierwszy krok toodeveloping rozwiązania magazynu danych przy użyciu usługi SQL Data Warehouse. Zobacz nasze zasoby projektowe na [tabel](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) i [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).


<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
