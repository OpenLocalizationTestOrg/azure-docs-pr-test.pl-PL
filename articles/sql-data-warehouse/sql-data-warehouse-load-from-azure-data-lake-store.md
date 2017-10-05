---
title: "Obciążenie — usługi Azure Data Lake Store SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak ładowanie danych z usługi Azure Data Lake Store do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase tabel zewnętrznych."
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
ms.openlocfilehash: ab951c30aae0d4afdd931e245f25d4645bba1681
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="c53d7-103">Ładowanie danych z usługi Azure Data Lake Store do magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="c53d7-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="c53d7-104">Ten dokument stanowi wszystkie czynności, które należy załadować własne dane z usługi Azure Data Lake magazyn (ADLS) do usługi SQL Data Warehouse przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="c53d7-104">This document gives you all steps you  need to load your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="c53d7-105">Gdy jesteś w stanie uruchamianie zapytań ad hoc przez dane przechowywane w ADLS przy użyciu tabel zewnętrznych, jako najlepsze rozwiązanie zaleca się importowania danych do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c53d7-105">While you are able to run adhoc queries over the data stored in ADLS using the External Tables, as a best practice we suggest importing the data into the SQL Data Warehouse.</span></span>
<span data-ttu-id="c53d7-106">Szacowanie czasu: 10 minut, przy założeniu, że zostały spełnione wymagania wstępne, trzeba wykonać.</span><span class="sxs-lookup"><span data-stu-id="c53d7-106">Time Estimate: 10 minutes assuming you have the prerequisites need to complete.</span></span>
<span data-ttu-id="c53d7-107">W tym samouczku przedstawiono sposób:</span><span class="sxs-lookup"><span data-stu-id="c53d7-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="c53d7-108">Tworzenie obiektów zewnętrznej bazy danych można załadować z usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c53d7-108">Create External Database objects to load from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="c53d7-109">Nawiązać katalog usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c53d7-109">Connect to an Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="c53d7-110">Ładowanie danych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c53d7-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c53d7-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c53d7-111">Before you begin</span></span>
<span data-ttu-id="c53d7-112">Aby uruchomić ten samouczek, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="c53d7-112">To run this tutorial, you need:</span></span>

* <span data-ttu-id="c53d7-113">Azure aplikacji usługi Active Directory do użycia na potrzeby uwierzytelniania do usługi.</span><span class="sxs-lookup"><span data-stu-id="c53d7-113">Azure Active Directory Application to use for Service-to-Service authentication.</span></span> <span data-ttu-id="c53d7-114">Aby utworzyć, wykonaj [uwierzytelniania usługi Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="c53d7-114">To create, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="c53d7-115">Potrzebujesz Identyfikatora klienta, klucz i wartość tokenu punktu końcowego OAuth2.0 aplikacji Active Directory do nawiązania połączenia z usługi Azure Data Lake z magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="c53d7-115">You need the client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application to connect to your Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="c53d7-116">Szczegóły dotyczące sposobu uzyskania tych wartości znajdują się w łącze powyżej.</span><span class="sxs-lookup"><span data-stu-id="c53d7-116">Details for how to get these values are in the link above.</span></span>
><span data-ttu-id="c53d7-117">Uwaga dotycząca rejestracji aplikacji Azure Active Directory, użyj Identyfikatora aplikacji jako identyfikator klienta.</span><span class="sxs-lookup"><span data-stu-id="c53d7-117">Note for Azure Active Directory App Registration use the 'Application ID' as the Client ID.</span></span>

* <span data-ttu-id="c53d7-118">SQL Server Management Studio lub SQL Server Data Tools, aby pobrać narzędzia SSMS i połączyć zobacz [SSMS zapytania](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="c53d7-118">SQL Server Management Studio or SQL Server Data Tools, to download SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="c53d7-119">Magazyn danych SQL Azure, aby utworzyć wykonaj jedną: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="c53d7-119">An Azure SQL Data Warehouse, to create one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="c53d7-120">Azure Data Lake Store, lub nie jest włączone szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="c53d7-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="c53d7-121">Aby utworzyć wykonaj jedną: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="c53d7-121">To create one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-the-data-source"></a><span data-ttu-id="c53d7-122">Konfigurowanie źródła danych</span><span class="sxs-lookup"><span data-stu-id="c53d7-122">Configure the data source</span></span>
<span data-ttu-id="c53d7-123">Aparat PolyBase używa obiektów zewnętrznych T-SQL w celu zdefiniowania lokalizacji i atrybuty danych zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="c53d7-123">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="c53d7-124">Obiekty zewnętrzne są przechowywane w usłudze SQL Data Warehouse i odwołują się dane, które th są przechowywane zewnętrznie.</span><span class="sxs-lookup"><span data-stu-id="c53d7-124">The external objects are stored in SQL Data Warehouse and reference the data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="c53d7-125">Utwórz poświadczenia</span><span class="sxs-lookup"><span data-stu-id="c53d7-125">Create a credential</span></span>
<span data-ttu-id="c53d7-126">Aby uzyskać dostęp do usługi Azure Data Lake Store, należy utworzyć klucz główny bazy danych, aby zaszyfrować klucz tajny poświadczenie użyte w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="c53d7-126">To access your Azure Data Lake Store, you will need to create a Database Master Key to encrypt your credential secret used in the next step.</span></span>
<span data-ttu-id="c53d7-127">Następnie można utworzyć poświadczenia bazy danych, której są przechowywane poświadczenia główne usługi skonfigurowane w usłudze AAD.</span><span class="sxs-lookup"><span data-stu-id="c53d7-127">You then create a Database scoped credential, which stores the service principal credentials set up in AAD.</span></span> <span data-ttu-id="c53d7-128">Dla osób, które użyto który można podłączyć do obiektów blob magazynu Azure z systemem Windows, należy pamiętać, że składnia poświadczeń różnych PolyBase.</span><span class="sxs-lookup"><span data-stu-id="c53d7-128">For those of you who have used PolyBase to connect to Windows Azure Storage Blobs, note that the credential syntax is different.</span></span>
<span data-ttu-id="c53d7-129">Aby połączyć się z usługi Azure Data Lake Store, należy najpierw **pierwszy** tworzenie aplikacji Azure Active Directory Utwórz klucz dostępu i umożliwić aplikacji dostęp do zasobów usługi Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c53d7-129">To connect to Azure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant the application access to the Azure Data Lake resource.</span></span> <span data-ttu-id="c53d7-130">Instrucitons, aby wykonać te czynności znajdują się [tutaj](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="c53d7-130">Instrucitons to perform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass the client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
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


### <a name="create-the-external-data-source"></a><span data-ttu-id="c53d7-131">Tworzenie zewnętrznego źródła danych</span><span class="sxs-lookup"><span data-stu-id="c53d7-131">Create the external data source</span></span>
<span data-ttu-id="c53d7-132">Użyj tej [Tworzenie zewnętrznego źródła danych] [ CREATE EXTERNAL DATA SOURCE] polecenia do przechowywania lokalizacji danych i typu danych.</span><span class="sxs-lookup"><span data-stu-id="c53d7-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span>
<span data-ttu-id="c53d7-133">Identyfikator URI ADL można znaleźć w portalu Azure i www.portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="c53d7-133">You can find the ADL URI in the Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="c53d7-134">Skonfiguruj format danych</span><span class="sxs-lookup"><span data-stu-id="c53d7-134">Configure data format</span></span>
<span data-ttu-id="c53d7-135">Aby zaimportować dane z ADLS, należy określić format pliku zewnętrznego.</span><span class="sxs-lookup"><span data-stu-id="c53d7-135">To import the data from ADLS, you need to specify the external file format.</span></span> <span data-ttu-id="c53d7-136">To polecenie ma format opcje do opisywania danych.</span><span class="sxs-lookup"><span data-stu-id="c53d7-136">This command has format-specific options to describe your data.</span></span>
<span data-ttu-id="c53d7-137">Poniżej przedstawiono przykład często używane formacie, który jest plikiem tekstowym rozdzielany potoku.</span><span class="sxs-lookup"><span data-stu-id="c53d7-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="c53d7-138">Szukaj w naszej dokumentacji T-SQL, aby uzyskać pełną listę [Tworzenie zewnętrznych FORMAT pliku][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="c53d7-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks the end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies the field terminator for data of type string in the text-delimited file.
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

## <a name="create-the-external-tables"></a><span data-ttu-id="c53d7-139">Tworzenie tabel zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="c53d7-139">Create the external tables</span></span>
<span data-ttu-id="c53d7-140">Teraz, gdy został określony format źródła i plików danych, możesz przystąpić do tworzenia tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="c53d7-140">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> <span data-ttu-id="c53d7-141">Tabele zewnętrzne są interakcje z danymi zewnętrznymi.</span><span class="sxs-lookup"><span data-stu-id="c53d7-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="c53d7-142">Program PolyBase używa cyklicznego katalogu Przechodzenie do odczytu wszystkich plików w podkatalogach katalogu określonego w parametrze lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c53d7-142">PolyBase uses recursive directory traversal to read all files in all subdirectories of the directory specified in the location parameter.</span></span> <span data-ttu-id="c53d7-143">Ponadto poniższy przykład pokazuje, jak utworzyć obiektu.</span><span class="sxs-lookup"><span data-stu-id="c53d7-143">Also, the following example shows how to create the object.</span></span> <span data-ttu-id="c53d7-144">Należy dostosować instrukcję do pracy z danymi w ADLS.</span><span class="sxs-lookup"><span data-stu-id="c53d7-144">You need to customize the statement to work with the data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under the ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object to use.
-- FILE_FORMAT: Specifies which File Format Object to use
-- REJECT_TYPE: Specifies how you want to deal with rejected rows. Either Value or percentage of the total
-- REJECT_VALUE: Sets the Reject value based on the reject type.

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

## <a name="external-table-considerations"></a><span data-ttu-id="c53d7-145">Zagadnienia dotyczące tabeli zewnętrznej</span><span class="sxs-lookup"><span data-stu-id="c53d7-145">External Table Considerations</span></span>
<span data-ttu-id="c53d7-146">Tworzenie tabeli zewnętrznej jest proste, ale istnieją pewne różnice, które muszą zostać omówione.</span><span class="sxs-lookup"><span data-stu-id="c53d7-146">Creating an external table is easy, but there are some nuances that need to be discussed.</span></span>

<span data-ttu-id="c53d7-147">Ładowanie danych przy użyciu programu PolyBase jest silnie typizowane.</span><span class="sxs-lookup"><span data-stu-id="c53d7-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="c53d7-148">Oznacza to, że każdy wiersz danych jest pozyskanych muszą spełniać definicja schematu tabeli.</span><span class="sxs-lookup"><span data-stu-id="c53d7-148">This means that each row of the data being ingested must satisfy the table schema definition.</span></span>
<span data-ttu-id="c53d7-149">Jeśli dany wiersz jest niezgodny z definicji schematu, wiersz został odrzucony z obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c53d7-149">If a given row does not match the schema definition, the row is rejected from the load.</span></span>

<span data-ttu-id="c53d7-150">Opcje REJECT_TYPE i REJECT_VALUE umożliwiają definiowanie, ile wierszy lub wartość procentowa danych musi być obecny w końcowym tabeli.</span><span class="sxs-lookup"><span data-stu-id="c53d7-150">The REJECT_TYPE and REJECT_VALUE options allow you to define how many rows or what percentage of the data must be present in the final table.</span></span>
<span data-ttu-id="c53d7-151">Podczas ładowania po osiągnięciu wartości Odrzuć obciążenia kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="c53d7-151">During load, if the reject value is reached, the load fails.</span></span> <span data-ttu-id="c53d7-152">Najczęstszą przyczyną odrzuconych wierszy jest niezgodność definicji schematu.</span><span class="sxs-lookup"><span data-stu-id="c53d7-152">The most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="c53d7-153">Na przykład kolumny niepoprawnie podano schematu int, gdy dane w pliku jest ciągiem, każdy wiersz zakończy się niepowodzeniem do załadowania.</span><span class="sxs-lookup"><span data-stu-id="c53d7-153">For example, if a column is incorrectly given the schema of int when the data in the file is a string, every row will fail to load.</span></span>

<span data-ttu-id="c53d7-154">Lokalizacja określa katalogu najwyższego poziomu, który chcesz odczytać danych z.</span><span class="sxs-lookup"><span data-stu-id="c53d7-154">The Location specifies the topmost directory that you want to read data from.</span></span>
<span data-ttu-id="c53d7-155">W takim przypadku, gdyby podkatalogów w obszarze /DimProduct/ PolyBase jaki są importowane wszystkich danych w podkatalogach.</span><span class="sxs-lookup"><span data-stu-id="c53d7-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all the data within the subdirectories.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="c53d7-156">Ładowanie danych</span><span class="sxs-lookup"><span data-stu-id="c53d7-156">Load the data</span></span>
<span data-ttu-id="c53d7-157">Aby załadować dane z użycia usługi Azure Data Lake Store [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrukcji.</span><span class="sxs-lookup"><span data-stu-id="c53d7-157">To load data from Azure Data Lake Store use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="c53d7-158">Ładowanie z CTAS używa jednoznacznie tabeli zewnętrznej, które utworzono.</span><span class="sxs-lookup"><span data-stu-id="c53d7-158">Loading with CTAS uses the strongly typed external table you have created.</span></span>

<span data-ttu-id="c53d7-159">CTAS tworzy nową tabelę i wypełnia wyników w instrukcji select.</span><span class="sxs-lookup"><span data-stu-id="c53d7-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="c53d7-160">CTAS definiuje nowa tabela na tej samej kolumny i typy danych wyników w instrukcji select.</span><span class="sxs-lookup"><span data-stu-id="c53d7-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="c53d7-161">Po wybraniu wszystkich kolumn z tabeli zewnętrznej nowa tabela jest repliką kolumn i typy danych w tabeli zewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="c53d7-161">If you select all the columns from an external table, the new table is a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="c53d7-162">W tym przykładzie tworzymy tabeli rozproszonej wyznaczania wartości skrótu o nazwie DimProduct z naszych zewnętrznych DimProduct_external tabeli.</span><span class="sxs-lookup"><span data-stu-id="c53d7-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="c53d7-163">Optymalizacja magazynu kolumn kompresji</span><span class="sxs-lookup"><span data-stu-id="c53d7-163">Optimize columnstore compression</span></span>
<span data-ttu-id="c53d7-164">Domyślnie usługa SQL Data Warehouse przechowuje tabeli jako klastrowany indeks magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="c53d7-164">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="c53d7-165">Po zakończeniu obciążenia niektóre wiersze danych może nie można skompresować do magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="c53d7-165">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="c53d7-166">Brak z różnych powodów, dlaczego jest to możliwe.</span><span class="sxs-lookup"><span data-stu-id="c53d7-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="c53d7-167">Aby dowiedzieć się więcej, zobacz [Zarządzaj indeksami magazynu kolumn][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="c53d7-167">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="c53d7-168">Aby zoptymalizować wydajność zapytań i ich kompresji magazynu kolumn po załadowaniu, Odbuduj tabelę, aby wymusić indeksu magazynu kolumn do skompresowania wszystkie wiersze.</span><span class="sxs-lookup"><span data-stu-id="c53d7-168">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="c53d7-169">Aby uzyskać więcej informacji na temat zachowania indeksy magazynu kolumn, zobacz [Zarządzaj indeksami magazynu kolumn] [ manage columnstore indexes] artykułu.</span><span class="sxs-lookup"><span data-stu-id="c53d7-169">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="c53d7-170">Optymalizacja statystyki</span><span class="sxs-lookup"><span data-stu-id="c53d7-170">Optimize statistics</span></span>
<span data-ttu-id="c53d7-171">Najlepiej utworzyć statystyki dla pojedynczej kolumny natychmiast po załadowaniu.</span><span class="sxs-lookup"><span data-stu-id="c53d7-171">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="c53d7-172">Dostępne są niektóre opcje wyboru statystyk.</span><span class="sxs-lookup"><span data-stu-id="c53d7-172">There are some choices for statistics.</span></span> <span data-ttu-id="c53d7-173">Na przykład jeśli tworzenie statystyk pojedynczej kolumny w każdej kolumnie go może zająć dużo czasu odbudować wszystkie statystyki.</span><span class="sxs-lookup"><span data-stu-id="c53d7-173">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="c53d7-174">Jeśli wiesz, że niektóre kolumny nie będą znajdować się w predykatach kwerendy, można pominąć tworzenie statystyk na podstawie tych kolumn.</span><span class="sxs-lookup"><span data-stu-id="c53d7-174">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="c53d7-175">Jeśli zdecydujesz się tworzenie statystyk pojedynczej kolumny w każdej kolumnie każdej tabeli, można użyć procedury składowanej przykładowy kod `prc_sqldw_create_stats` w [statystyki] [ statistics] artykułu.</span><span class="sxs-lookup"><span data-stu-id="c53d7-175">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="c53d7-176">Poniższy przykład jest dobry punkt wyjścia do tworzenia statystyk.</span><span class="sxs-lookup"><span data-stu-id="c53d7-176">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="c53d7-177">Tworzy statystyki pojedynczej kolumny w każdej kolumnie w tabeli wymiarów i w każdej kolumnie łącząca w tabelach faktów.</span><span class="sxs-lookup"><span data-stu-id="c53d7-177">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="c53d7-178">Można dodać jednego lub wielu kolumn statystyki do kolumn tabeli faktów później.</span><span class="sxs-lookup"><span data-stu-id="c53d7-178">You can always add single or multi-column statistics to other fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="c53d7-179">Osiągnięcia odblokowane!</span><span class="sxs-lookup"><span data-stu-id="c53d7-179">Achievement unlocked!</span></span>
<span data-ttu-id="c53d7-180">Dane zostały pomyślnie załadowane do magazynu danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c53d7-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="c53d7-181">Dobra robota!</span><span class="sxs-lookup"><span data-stu-id="c53d7-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="c53d7-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c53d7-182">Next Steps</span></span>
<span data-ttu-id="c53d7-183">Podczas ładowania danych jest pierwszy krok projektowania rozwiązania magazynu danych przy użyciu usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c53d7-183">Loading data is the first step to developing a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="c53d7-184">Zobacz nasze zasoby projektowe na [tabel](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) i [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="c53d7-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
