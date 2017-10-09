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
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="7b22e-103">Ładowanie danych z usługi Azure Data Lake Store do magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="7b22e-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="7b22e-104">Ten dokument stanowi wszystkie czynności, które należy tooload własne dane z usługi Azure Data Lake magazyn (ADLS) do usługi SQL Data Warehouse przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="7b22e-104">This document gives you all steps you  need tooload your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="7b22e-105">Podczas pracy zapytań ad hoc toorun mogli za pośrednictwem hello danych przechowywanych w ADLS przy użyciu tabel zewnętrznych hello jako najlepsze rozwiązanie zaleca się importowanie danych hello hello SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7b22e-105">While you are able toorun adhoc queries over hello data stored in ADLS using hello External Tables, as a best practice we suggest importing hello data into hello SQL Data Warehouse.</span></span>
<span data-ttu-id="7b22e-106">Szacowanie czasu: 10 minut, przy założeniu, że masz hello wymagań wstępnych konieczne toocomplete.</span><span class="sxs-lookup"><span data-stu-id="7b22e-106">Time Estimate: 10 minutes assuming you have hello prerequisites need toocomplete.</span></span>
<span data-ttu-id="7b22e-107">W tym samouczku przedstawiono sposób:</span><span class="sxs-lookup"><span data-stu-id="7b22e-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="7b22e-108">Utwórz tooload obiekty zewnętrznej bazy danych z usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="7b22e-108">Create External Database objects tooload from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="7b22e-109">Połącz tooan Azure Data Lake magazynu katalogu.</span><span class="sxs-lookup"><span data-stu-id="7b22e-109">Connect tooan Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="7b22e-110">Ładowanie danych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7b22e-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7b22e-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="7b22e-111">Before you begin</span></span>
<span data-ttu-id="7b22e-112">toorun tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="7b22e-112">toorun this tutorial, you need:</span></span>

* <span data-ttu-id="7b22e-113">Azure toouse aplikacji usługi Active Directory do usługi uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="7b22e-113">Azure Active Directory Application toouse for Service-to-Service authentication.</span></span> <span data-ttu-id="7b22e-114">toocreate, wykonaj [uwierzytelniania usługi Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="7b22e-114">toocreate, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="7b22e-115">Wymagane hello Identyfikatora klienta, klucz i wartość tokenu punktu końcowego OAuth2.0 z Twojej aplikacji usługi Active Directory tooconnect tooyour usługi Azure Data Lake z magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="7b22e-115">You need hello client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application tooconnect tooyour Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="7b22e-116">Szczegóły dotyczące sposobu tooget te wartości są w powyższy link hello.</span><span class="sxs-lookup"><span data-stu-id="7b22e-116">Details for how tooget these values are in hello link above.</span></span>
><span data-ttu-id="7b22e-117">Uwaga dotycząca rejestracji aplikacji Azure Active Directory użyj hello "Identyfikator aplikacji" jako hello identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="7b22e-117">Note for Azure Active Directory App Registration use hello 'Application ID' as hello Client ID.</span></span>

* <span data-ttu-id="7b22e-118">SQL Server Management Studio lub SQL Server Data Tools toodownload SSMS i połączenia zobacz [SSMS zapytania](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="7b22e-118">SQL Server Management Studio or SQL Server Data Tools, toodownload SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="7b22e-119">Wykonaj toocreate jeden magazyn danych SQL Azure: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="7b22e-119">An Azure SQL Data Warehouse, toocreate one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="7b22e-120">Azure Data Lake Store, lub nie jest włączone szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="7b22e-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="7b22e-121">Wykonaj jeden toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="7b22e-121">toocreate one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-hello-data-source"></a><span data-ttu-id="7b22e-122">Konfigurowanie hello źródła danych</span><span class="sxs-lookup"><span data-stu-id="7b22e-122">Configure hello data source</span></span>
<span data-ttu-id="7b22e-123">Program PolyBase używa lokalizacji hello toodefine zewnętrznych obiektów T-SQL i atrybuty hello danych zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="7b22e-123">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="7b22e-124">Witaj zewnętrznych obiektów są przechowywane w SQL Data Warehouse i hello danych referencyjnych th jest przechowywana zewnętrznie.</span><span class="sxs-lookup"><span data-stu-id="7b22e-124">hello external objects are stored in SQL Data Warehouse and reference hello data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="7b22e-125">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="7b22e-125">Create a credential</span></span>
<span data-ttu-id="7b22e-126">tooaccess Twojego Azure Data Lake przechowywania, konieczne będzie toocreate tooencrypt klucz główny bazy danych klucz tajny poświadczenie używane w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="7b22e-126">tooaccess your Azure Data Lake Store, you will need toocreate a Database Master Key tooencrypt your credential secret used in hello next step.</span></span>
<span data-ttu-id="7b22e-127">Następnie można utworzyć poświadczenia bazy danych, której są przechowywane poświadczenia główne usługi hello skonfigurowane w usłudze AAD.</span><span class="sxs-lookup"><span data-stu-id="7b22e-127">You then create a Database scoped credential, which stores hello service principal credentials set up in AAD.</span></span> <span data-ttu-id="7b22e-128">Dla osób, które zostały użyte PolyBase tooconnect tooWindows obiektach blob magazynu Azure, należy pamiętać, że poświadczenie hello składni jest inny.</span><span class="sxs-lookup"><span data-stu-id="7b22e-128">For those of you who have used PolyBase tooconnect tooWindows Azure Storage Blobs, note that hello credential syntax is different.</span></span>
<span data-ttu-id="7b22e-129">tooAzure tooconnect usługi Data Lake Store, należy najpierw **pierwszy** tworzenie aplikacji Azure Active Directory, Utwórz klucz dostępu, a następnie przyznać hello aplikacji dostępu toohello usługi Azure Data Lake zasobów.</span><span class="sxs-lookup"><span data-stu-id="7b22e-129">tooconnect tooAzure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant hello application access toohello Azure Data Lake resource.</span></span> <span data-ttu-id="7b22e-130">Instrucitons tooperform znajdują się następujące kroki [tutaj](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="7b22e-130">Instrucitons tooperform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

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


### <a name="create-hello-external-data-source"></a><span data-ttu-id="7b22e-131">Utwórz hello zewnętrznego źródła danych</span><span class="sxs-lookup"><span data-stu-id="7b22e-131">Create hello external data source</span></span>
<span data-ttu-id="7b22e-132">Użyj tej [Tworzenie zewnętrznego źródła danych] [ CREATE EXTERNAL DATA SOURCE] polecenia toostore lokalizacji hello hello danych i hello typu danych.</span><span class="sxs-lookup"><span data-stu-id="7b22e-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span>
<span data-ttu-id="7b22e-133">Witaj ADL URI można znaleźć w hello portalu Azure i www.portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="7b22e-133">You can find hello ADL URI in hello Azure portal and www.portal.azure.com.</span></span>

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



## <a name="configure-data-format"></a><span data-ttu-id="7b22e-134">Skonfiguruj format danych</span><span class="sxs-lookup"><span data-stu-id="7b22e-134">Configure data format</span></span>
<span data-ttu-id="7b22e-135">dane hello tooimport z ADLS, należy toospecify hello zewnętrznego formatu pliku.</span><span class="sxs-lookup"><span data-stu-id="7b22e-135">tooimport hello data from ADLS, you need toospecify hello external file format.</span></span> <span data-ttu-id="7b22e-136">To polecenie ma toodescribe opcje związane z formatem danych.</span><span class="sxs-lookup"><span data-stu-id="7b22e-136">This command has format-specific options toodescribe your data.</span></span>
<span data-ttu-id="7b22e-137">Poniżej przedstawiono przykład często używane formacie, który jest plikiem tekstowym rozdzielany potoku.</span><span class="sxs-lookup"><span data-stu-id="7b22e-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="7b22e-138">Szukaj w naszej dokumentacji T-SQL, aby uzyskać pełną listę [Tworzenie zewnętrznych FORMAT pliku][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="7b22e-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

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

## <a name="create-hello-external-tables"></a><span data-ttu-id="7b22e-139">Tworzenie tabel zewnętrznych hello</span><span class="sxs-lookup"><span data-stu-id="7b22e-139">Create hello external tables</span></span>
<span data-ttu-id="7b22e-140">Określono hello danych źródła i format pliku, użytkownik jest tabel zewnętrznych hello toocreate gotowe.</span><span class="sxs-lookup"><span data-stu-id="7b22e-140">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> <span data-ttu-id="7b22e-141">Tabele zewnętrzne są interakcje z danymi zewnętrznymi.</span><span class="sxs-lookup"><span data-stu-id="7b22e-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="7b22e-142">Program PolyBase używa cyklicznego katalogu przechodzenie tooread wszystkie pliki w wszystkie podkatalogi katalogu hello określony w parametrze lokalizacji hello.</span><span class="sxs-lookup"><span data-stu-id="7b22e-142">PolyBase uses recursive directory traversal tooread all files in all subdirectories of hello directory specified in hello location parameter.</span></span> <span data-ttu-id="7b22e-143">Ponadto hello poniższy przykład pokazuje, jak toocreate hello obiektu.</span><span class="sxs-lookup"><span data-stu-id="7b22e-143">Also, hello following example shows how toocreate hello object.</span></span> <span data-ttu-id="7b22e-144">Należy toocustomize hello instrukcji toowork z danych hello w ADLS.</span><span class="sxs-lookup"><span data-stu-id="7b22e-144">You need toocustomize hello statement toowork with hello data you have in ADLS.</span></span>

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

## <a name="external-table-considerations"></a><span data-ttu-id="7b22e-145">Zagadnienia dotyczące tabeli zewnętrznej</span><span class="sxs-lookup"><span data-stu-id="7b22e-145">External Table Considerations</span></span>
<span data-ttu-id="7b22e-146">Tworzenie tabeli zewnętrznej jest proste, ale istnieją pewne różnice wymagające toobe omówione.</span><span class="sxs-lookup"><span data-stu-id="7b22e-146">Creating an external table is easy, but there are some nuances that need toobe discussed.</span></span>

<span data-ttu-id="7b22e-147">Ładowanie danych przy użyciu programu PolyBase jest silnie typizowane.</span><span class="sxs-lookup"><span data-stu-id="7b22e-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="7b22e-148">Oznacza to, że każdy wiersz danych hello jest pozyskanych muszą spełniać definicja schematu tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="7b22e-148">This means that each row of hello data being ingested must satisfy hello table schema definition.</span></span>
<span data-ttu-id="7b22e-149">Jeśli danego wiersza nie jest zgodny z definicji schematu hello, wiersz hello jest odrzucona z hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7b22e-149">If a given row does not match hello schema definition, hello row is rejected from hello load.</span></span>

<span data-ttu-id="7b22e-150">Witaj REJECT_TYPE i REJECT_VALUE opcje pozwalają toodefine liczby wierszy lub wartość procentowa danych hello musi znajdować się w tabeli końcowej hello.</span><span class="sxs-lookup"><span data-stu-id="7b22e-150">hello REJECT_TYPE and REJECT_VALUE options allow you toodefine how many rows or what percentage of hello data must be present in hello final table.</span></span>
<span data-ttu-id="7b22e-151">Podczas ładowania po osiągnięciu wartości Odrzuć hello obciążenia hello kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="7b22e-151">During load, if hello reject value is reached, hello load fails.</span></span> <span data-ttu-id="7b22e-152">Najczęstszą przyczyną Hello odrzucone wierszy jest niezgodność definicji schematu.</span><span class="sxs-lookup"><span data-stu-id="7b22e-152">hello most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="7b22e-153">Na przykład jeśli kolumny niepoprawnie podano schematu hello int, gdy hello dane w pliku hello jest ciągiem, każdy wiersz zakończy się niepowodzeniem tooload.</span><span class="sxs-lookup"><span data-stu-id="7b22e-153">For example, if a column is incorrectly given hello schema of int when hello data in hello file is a string, every row will fail tooload.</span></span>

<span data-ttu-id="7b22e-154">Witaj Lokalizacja określa hello katalogu najwyższego poziomu tooread danych z.</span><span class="sxs-lookup"><span data-stu-id="7b22e-154">hello Location specifies hello topmost directory that you want tooread data from.</span></span>
<span data-ttu-id="7b22e-155">W takim przypadku, gdyby podkatalogów w obszarze /DimProduct/ PolyBase jaki są importowane wszystkich danych hello w Witaj podkatalogi.</span><span class="sxs-lookup"><span data-stu-id="7b22e-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all hello data within hello subdirectories.</span></span>

## <a name="load-hello-data"></a><span data-ttu-id="7b22e-156">Ładowanie danych hello</span><span class="sxs-lookup"><span data-stu-id="7b22e-156">Load hello data</span></span>
<span data-ttu-id="7b22e-157">tooload dane z usługi Azure Data Lake Store Użyj hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="7b22e-157">tooload data from Azure Data Lake Store use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="7b22e-158">Podczas ładowania z CTAS hello używa silnie typizowane tabeli zewnętrznej, które zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="7b22e-158">Loading with CTAS uses hello strongly typed external table you have created.</span></span>

<span data-ttu-id="7b22e-159">CTAS tworzy nową tabelę i wypełnia hello wyników w instrukcji select.</span><span class="sxs-lookup"><span data-stu-id="7b22e-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="7b22e-160">CTAS definiuje hello nowej tabeli toohave hello tej samej kolumny i typy danych jak wyniki hello hello wybierz instrukcji.</span><span class="sxs-lookup"><span data-stu-id="7b22e-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="7b22e-161">Po wybraniu wszystkich hello kolumn z tabeli zewnętrznej nową tabelę hello jest repliką hello kolumn i typy danych w tabeli zewnętrznej hello.</span><span class="sxs-lookup"><span data-stu-id="7b22e-161">If you select all hello columns from an external table, hello new table is a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="7b22e-162">W tym przykładzie tworzymy tabeli rozproszonej wyznaczania wartości skrótu o nazwie DimProduct z naszych zewnętrznych DimProduct_external tabeli.</span><span class="sxs-lookup"><span data-stu-id="7b22e-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="7b22e-163">Optymalizacja magazynu kolumn kompresji</span><span class="sxs-lookup"><span data-stu-id="7b22e-163">Optimize columnstore compression</span></span>
<span data-ttu-id="7b22e-164">Domyślnie usługa SQL Data Warehouse przechowuje hello tabeli jako klastrowany indeks magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="7b22e-164">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="7b22e-165">Po zakończeniu obciążenia nie może być niektóre wiersze danych hello skompresowane w hello magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="7b22e-165">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="7b22e-166">Brak z różnych powodów, dlaczego jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="7b22e-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="7b22e-167">toolearn więcej, zobacz [Zarządzaj indeksami magazynu kolumn][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="7b22e-167">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="7b22e-168">toooptimize wydajność zapytań i ich kompresji magazynu kolumn po załadowaniu, Odbuduj hello tabeli tooforce hello magazynu kolumn indeksu toocompress wszystkie wiersze hello.</span><span class="sxs-lookup"><span data-stu-id="7b22e-168">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="7b22e-169">Aby uzyskać więcej informacji na temat zachowania indeksy magazynu kolumn, zobacz hello [Zarządzaj indeksami magazynu kolumn] [ manage columnstore indexes] artykułu.</span><span class="sxs-lookup"><span data-stu-id="7b22e-169">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="7b22e-170">Optymalizacja statystyki</span><span class="sxs-lookup"><span data-stu-id="7b22e-170">Optimize statistics</span></span>
<span data-ttu-id="7b22e-171">Najważniejsze dane statystyczne pojedynczej kolumny toocreate jest natychmiast po załadowaniu.</span><span class="sxs-lookup"><span data-stu-id="7b22e-171">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="7b22e-172">Dostępne są niektóre opcje wyboru statystyk.</span><span class="sxs-lookup"><span data-stu-id="7b22e-172">There are some choices for statistics.</span></span> <span data-ttu-id="7b22e-173">Na przykład jeśli tworzenie statystyk pojedynczej kolumny w każdej kolumnie może potrwać toorebuild długo wszystkie statystyki hello.</span><span class="sxs-lookup"><span data-stu-id="7b22e-173">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="7b22e-174">Jeśli wiesz, że niektóre kolumny nie będą toobe w predykatach kwerendy, można pominąć tworzenie statystyk na podstawie tych kolumn.</span><span class="sxs-lookup"><span data-stu-id="7b22e-174">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="7b22e-175">Jeśli zdecydujesz toocreate statystyki pojedynczej kolumny w każdej kolumnie każda tabela służy przykładowy kod procedury składowanej hello `prc_sqldw_create_stats` w hello [statystyki] [ statistics] artykułu.</span><span class="sxs-lookup"><span data-stu-id="7b22e-175">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="7b22e-176">Poniższy przykład Hello jest dobry punkt wyjścia do tworzenia statystyk.</span><span class="sxs-lookup"><span data-stu-id="7b22e-176">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="7b22e-177">W każdej kolumnie w tabeli wymiarów hello i w każdej kolumnie łącząca w tabelach faktów hello tworzy statystyki pojedynczej kolumny.</span><span class="sxs-lookup"><span data-stu-id="7b22e-177">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="7b22e-178">Później można dodać kolumny tabeli faktów tooother statystyki jednego lub wielu kolumn.</span><span class="sxs-lookup"><span data-stu-id="7b22e-178">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="7b22e-179">Osiągnięcia odblokowane!</span><span class="sxs-lookup"><span data-stu-id="7b22e-179">Achievement unlocked!</span></span>
<span data-ttu-id="7b22e-180">Dane zostały pomyślnie załadowane do magazynu danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7b22e-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="7b22e-181">Dobra robota!</span><span class="sxs-lookup"><span data-stu-id="7b22e-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="7b22e-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7b22e-182">Next Steps</span></span>
<span data-ttu-id="7b22e-183">Podczas ładowania danych jest hello pierwszy krok toodeveloping rozwiązania magazynu danych przy użyciu usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7b22e-183">Loading data is hello first step toodeveloping a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="7b22e-184">Zobacz nasze zasoby projektowe na [tabel](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) i [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="7b22e-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
