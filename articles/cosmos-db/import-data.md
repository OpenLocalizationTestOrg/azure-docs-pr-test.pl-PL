---
title: "Narzędzie migracji aaaDatabase dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak otworzyć toouse hello źródłowej bazy danych Azure rozwiązania Cosmos danych migracji narzędzia tooimport danych tooAzure rozwiązania Cosmos bazy danych z różnych źródeł, takich jak pliki bazy danych MongoDB, SQL Server tabeli magazynu, Amazon DynamoDB, CSV i JSON. Konwersja tooJSON CSV."
keywords: "toojson CSV, narzędzi migracji bazy danych, przekonwertować csv toojson"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a><span data-ttu-id="b68ab-105">Jak tooimport danych do bazy danych rozwiązania Cosmos Azure dla hello interfejsu API usługi DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="b68ab-105">How tooimport data into Azure Cosmos DB for hello DocumentDB API?</span></span>

<span data-ttu-id="b68ab-106">Ten samouczek zawiera instrukcje dotyczące używania hello Azure DB rozwiązania Cosmos: narzędzia migracji danych interfejsu API usługi DocumentDB, które można importować dane z różnych źródeł, takich jak pliki w formacie JSON, CSV pliki, SQL, bazy danych MongoDB, Magazyn tabel Azure, Amazon DynamoDB oraz opcji Azure DocumentDB DB rozwiązania Cosmos Użyj interfejsu API kolekcji do kolekcji dla z bazy danych Azure rozwiązania Cosmos i hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="b68ab-106">This tutorial provides instructions on using hello Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and hello DocumentDB API.</span></span> <span data-ttu-id="b68ab-107">narzędzia migracji danych Hello można również podczas migracji z kolekcji wielu partycji tooa Kolekcja jednej partycji dla hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="b68ab-107">hello Data Migration tool can also be used when migrating from a single partition collection tooa multi-partition collection for hello DocumentDB API.</span></span>

<span data-ttu-id="b68ab-108">narzędzia migracji danych Hello działa tylko importowania danych do bazy danych rozwiązania Cosmos Azure do użycia z hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="b68ab-108">hello Data Migration tool only works when importing data into Azure Cosmos DB for use with hello DocumentDB API.</span></span> <span data-ttu-id="b68ab-109">Importowanie danych do użycia z hello API tabeli lub interfejsu API programu Graph nie jest obsługiwane w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="b68ab-109">Importing data for use with hello Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="b68ab-110">tooimport dane do użycia z hello API bazy danych MongoDB, zobacz [bazy danych Azure rozwiązania Cosmos: jak dane toomigrate hello API bazy danych MongoDB?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="b68ab-110">tooimport data for use with hello MongoDB API, see [Azure Cosmos DB: How toomigrate data for hello MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="b68ab-111">Ten samouczek obejmuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="b68ab-111">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b68ab-112">Instalacja narzędzia do migracji danych hello</span><span class="sxs-lookup"><span data-stu-id="b68ab-112">Installing hello Data Migration tool</span></span>
> * <span data-ttu-id="b68ab-113">Importowanie danych z różnych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="b68ab-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="b68ab-114">Eksportowanie z tooJSON bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="b68ab-114">Exporting from Azure Cosmos DB tooJSON</span></span>

## <span data-ttu-id="b68ab-115"><a id="Prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b68ab-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="b68ab-116">Przed rozpoczęciem powitalne instrukcje w tym artykule, upewnij się, że mają zainstalowane następujące hello:</span><span class="sxs-lookup"><span data-stu-id="b68ab-116">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="b68ab-117">[Program Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b68ab-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="b68ab-118"><a id="Overviewl"></a>Omówienie narzędzia migracji danych hello</span><span class="sxs-lookup"><span data-stu-id="b68ab-118"><a id="Overviewl"></a>Overview of hello Data Migration tool</span></span>
<span data-ttu-id="b68ab-119">Narzędzie migracji danych Hello jest rozwiązaniem typu open source, który importuje dane tooAzure rozwiązania Cosmos bazy danych z różnych źródeł, takich jak:</span><span class="sxs-lookup"><span data-stu-id="b68ab-119">hello Data Migration tool is an open source solution that imports data tooAzure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="b68ab-120">Pliki JSON</span><span class="sxs-lookup"><span data-stu-id="b68ab-120">JSON files</span></span>
* <span data-ttu-id="b68ab-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="b68ab-121">MongoDB</span></span>
* <span data-ttu-id="b68ab-122">Oprogramowanie SQL Server</span><span class="sxs-lookup"><span data-stu-id="b68ab-122">SQL Server</span></span>
* <span data-ttu-id="b68ab-123">Pliki CSV</span><span class="sxs-lookup"><span data-stu-id="b68ab-123">CSV files</span></span>
* <span data-ttu-id="b68ab-124">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="b68ab-124">Azure Table storage</span></span>
* <span data-ttu-id="b68ab-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="b68ab-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="b68ab-126">HBase</span><span class="sxs-lookup"><span data-stu-id="b68ab-126">HBase</span></span>
* <span data-ttu-id="b68ab-127">Kolekcje usługi Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="b68ab-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="b68ab-128">Gdy narzędzie importowania hello zawiera graficzny interfejs użytkownika (dtui.exe), mogą być określane również z wiersza polecenia hello (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="b68ab-128">While hello import tool includes a graphical user interface (dtui.exe), it can also be driven from hello command line (dt.exe).</span></span> <span data-ttu-id="b68ab-129">W rzeczywistości istnieje opcja toooutput hello skojarzone polecenia po skonfigurowaniu importu za pośrednictwem hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b68ab-129">In fact, there is an option toooutput hello associated command after setting up an import through hello UI.</span></span> <span data-ttu-id="b68ab-130">Tabelaryczne źródła danych (np. programu SQL Server lub plików CSV) można je przekształcać w taki sposób, że relacje hierarchiczne (dokumentów podrzędnych) można utworzyć podczas importowania.</span><span class="sxs-lookup"><span data-stu-id="b68ab-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="b68ab-131">Zachowaj odczytywania toolearn więcej informacji na temat opcji źródła, przykładowe wiersze poleceń tooimport z każdego źródła, target — opcje i wyświetlić wyniki importu.</span><span class="sxs-lookup"><span data-stu-id="b68ab-131">Keep reading toolearn more about source options, sample command lines tooimport from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="b68ab-132"><a id="Install"></a>Zainstaluj narzędzia migracji danych hello</span><span class="sxs-lookup"><span data-stu-id="b68ab-132"><a id="Install"></a>Install hello Data Migration tool</span></span>
<span data-ttu-id="b68ab-133">Kod źródłowy narzędzia migracji Hello jest dostępna w witrynie GitHub w [to repozytorium](https://github.com/azure/azure-documentdb-datamigrationtool) i jest dostępny w wersji skompilowanej [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="b68ab-133">hello migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="b68ab-134">Może skompilować rozwiązanie hello lub po prostu pobierać i wyodrębniać hello skompilowanej wersji tooa katalogu.</span><span class="sxs-lookup"><span data-stu-id="b68ab-134">You may either compile hello solution or simply download and extract hello compiled version tooa directory of your choice.</span></span> <span data-ttu-id="b68ab-135">Następnie uruchom dowolne:</span><span class="sxs-lookup"><span data-stu-id="b68ab-135">Then run either:</span></span>

* <span data-ttu-id="b68ab-136">**Dtui.exe**: wersja interfejsu graficznego narzędzia hello</span><span class="sxs-lookup"><span data-stu-id="b68ab-136">**Dtui.exe**: Graphical interface version of hello tool</span></span>
* <span data-ttu-id="b68ab-137">**DT.exe**: wersja wiersza polecenia narzędzia hello</span><span class="sxs-lookup"><span data-stu-id="b68ab-137">**Dt.exe**: Command-line version of hello tool</span></span>

## <a name="import-data"></a><span data-ttu-id="b68ab-138">Importowanie danych</span><span class="sxs-lookup"><span data-stu-id="b68ab-138">Import data</span></span>

<span data-ttu-id="b68ab-139">Po zainstalowaniu narzędzia hello jest czas tooimport danych.</span><span class="sxs-lookup"><span data-stu-id="b68ab-139">Once you've installed hello tool, it's time tooimport your data.</span></span> <span data-ttu-id="b68ab-140">Jakiego typu dane chcesz tooimport?</span><span class="sxs-lookup"><span data-stu-id="b68ab-140">What kind of data do you want tooimport?</span></span>

* [<span data-ttu-id="b68ab-141">Pliki w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="b68ab-141">JSON files</span></span>](#JSON)
* [<span data-ttu-id="b68ab-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="b68ab-142">MongoDB</span></span>](#MongoDB)
* [<span data-ttu-id="b68ab-143">Pliki eksportu bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="b68ab-143">MongoDB Export files</span></span>](#MongoDBExport)
* [<span data-ttu-id="b68ab-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="b68ab-144">SQL Server</span></span>](#SQL)
* [<span data-ttu-id="b68ab-145">Pliki CSV</span><span class="sxs-lookup"><span data-stu-id="b68ab-145">CSV files</span></span>](#CSV)
* [<span data-ttu-id="b68ab-146">Azure Table storage</span><span class="sxs-lookup"><span data-stu-id="b68ab-146">Azure Table storage</span></span>](#AzureTableSource)
* [<span data-ttu-id="b68ab-147">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="b68ab-147">Amazon DynamoDB</span></span>](#DynamoDBSource)
* [<span data-ttu-id="b68ab-148">Obiekt blob</span><span class="sxs-lookup"><span data-stu-id="b68ab-148">Blob</span></span>](#BlobImport)
* [<span data-ttu-id="b68ab-149">Kolekcje usługi Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="b68ab-149">Azure Cosmos DB collections</span></span>](#DocumentDBSource)
* [<span data-ttu-id="b68ab-150">HBase</span><span class="sxs-lookup"><span data-stu-id="b68ab-150">HBase</span></span>](#HBaseSource)
* [<span data-ttu-id="b68ab-151">Importowania zbiorczego w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="b68ab-151">Azure Cosmos DB bulk import</span></span>](#DocumentDBBulkImport)
* [<span data-ttu-id="b68ab-152">Importowania platformy Azure kolejny rekord DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="b68ab-152">Azure Cosmos DB sequential record import</span></span>](#DocumentDSeqTarget)


## <span data-ttu-id="b68ab-153"><a id="JSON"></a>pliki w formacie JSON tooimport</span><span class="sxs-lookup"><span data-stu-id="b68ab-153"><a id="JSON"></a>tooimport JSON files</span></span>
<span data-ttu-id="b68ab-154">Witaj opcję importera źródło pliku JSON umożliwia tooimport jeden lub więcej plików JSON pojedynczego dokumentu lub pliki JSON, że każdy zawierać tablicę dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="b68ab-154">hello JSON file source importer option allows you tooimport one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="b68ab-155">Podczas dodawania folderów zawierających tooimport pliki JSON, dostępna jest opcja hello rekursywnie szukania plików w podfolderach.</span><span class="sxs-lookup"><span data-stu-id="b68ab-155">When adding folders that contain JSON files tooimport, you have hello option of recursively searching for files in subfolders.</span></span>

![Opcje źródłowego pliku zrzut ekranu JSON - narzędzia migracji bazy danych](./media/import-data/jsonsource.png)

<span data-ttu-id="b68ab-157">Poniżej przedstawiono niektóre pliki JSON tooimport przykłady wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="b68ab-157">Here are some command line samples tooimport JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="b68ab-158"><a id="MongoDB"></a>tooimport z bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="b68ab-158"><a id="MongoDB"></a>tooimport from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b68ab-159">Jeśli importujesz konto bazy danych Azure rozwiązania Cosmos tooan z obsługą bazy danych MongoDB, postępuj zgodnie z następującymi [instrukcje](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="b68ab-159">If you are importing tooan Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="b68ab-160">Hello opcja importera źródłowej bazy danych MongoDB pozwala tooimport z poszczególnych kolekcji bazy danych MongoDB i opcjonalnie filtrować dokumentów za pomocą zapytania i/lub modyfikowanie hello strukturę dokumentu przy użyciu projekcji.</span><span class="sxs-lookup"><span data-stu-id="b68ab-160">hello MongoDB source importer option allows you tooimport from an individual MongoDB collection and optionally filter documents using a query and/or modify hello document structure by using a projection.</span></span>  

![Zrzut ekranu MongoDB Opcje źródła](./media/import-data/mongodbsource.png)

<span data-ttu-id="b68ab-162">ciąg połączenia Hello jest w formacie bazy danych MongoDB hello:</span><span class="sxs-lookup"><span data-stu-id="b68ab-162">hello connection string is in hello standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="b68ab-163">Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie bazy danych MongoDB określony w polu Parametry połączenia hello są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b68ab-163">Use hello Verify command tooensure that hello MongoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="b68ab-164">Wprowadź nazwę hello hello kolekcji, w którym dane zostaną zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-164">Enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="b68ab-165">Opcjonalnie możesz określić lub udostępnić plik dla zapytania (np. {pop: {$gt: 5000}}) i/lub projekcji (np. {loc:0}) tooboth filtru i kształt hello danych toobe zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) tooboth filter and shape hello data toobe imported.</span></span>

<span data-ttu-id="b68ab-166">Poniżej przedstawiono niektóre tooimport przykłady wiersza polecenia z bazy danych MongoDB:</span><span class="sxs-lookup"><span data-stu-id="b68ab-166">Here are some command line samples tooimport from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="b68ab-167"><a id="MongoDBExport"></a>pliki eksportu tooimport bazy danych MongoDB</span><span class="sxs-lookup"><span data-stu-id="b68ab-167"><a id="MongoDBExport"></a>tooimport MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b68ab-168">Jeśli importujesz konto bazy danych Azure rozwiązania Cosmos tooan z obsługą bazy danych MongoDB, postępuj zgodnie z następującymi [instrukcje](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="b68ab-168">If you are importing tooan Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="b68ab-169">Hello opcję importera źródło pliku bazy danych MongoDB eksportu JSON umożliwia tooimport jeden lub więcej plików JSON wyprodukowane z hello mongoexport narzędzia.</span><span class="sxs-lookup"><span data-stu-id="b68ab-169">hello MongoDB export JSON file source importer option allows you tooimport one or more JSON files produced from hello mongoexport utility.</span></span>  

![Opcje źródła eksportu zrzut ekranu z bazy danych MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="b68ab-171">Podczas dodawania foldery zawierające pliki w formacie JSON eksportu bazy danych MongoDB do zaimportowania, dostępna jest opcja hello rekursywnie szukania plików w podfolderach.</span><span class="sxs-lookup"><span data-stu-id="b68ab-171">When adding folders that contain MongoDB export JSON files for import, you have hello option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="b68ab-172">Oto tooimport przykładowy wiersz polecenia z bazy danych MongoDB eksportu pliki w formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="b68ab-172">Here is a command line sample tooimport from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="b68ab-173"><a id="SQL"></a>tooimport z programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="b68ab-173"><a id="SQL"></a>tooimport from SQL Server</span></span>
<span data-ttu-id="b68ab-174">Hello opcji importera źródła SQL pozwala tooimport z poszczególnych bazy danych programu SQL Server i opcjonalnie filtrować toobe rekordów hello zaimportowany za pomocą zapytania.</span><span class="sxs-lookup"><span data-stu-id="b68ab-174">hello SQL source importer option allows you tooimport from an individual SQL Server database and optionally filter hello records toobe imported using a query.</span></span> <span data-ttu-id="b68ab-175">Ponadto można zmodyfikować hello strukturę dokumentu, określając zagnieżdżenia separatora (więcej informacji na temat którego za chwilę).</span><span class="sxs-lookup"><span data-stu-id="b68ab-175">In addition, you can modify hello document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Zrzut ekranu SQL źródła opcji - narzędzia migracji bazy danych](./media/import-data/sqlexportsource.png)

<span data-ttu-id="b68ab-177">format Hello hello ciągu połączenia jest format parametrów połączenia SQL hello standardowa.</span><span class="sxs-lookup"><span data-stu-id="b68ab-177">hello format of hello connection string is hello standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="b68ab-178">Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie serwera SQL określony w polu Parametry połączenia hello są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b68ab-178">Use hello Verify command tooensure that hello SQL Server instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="b68ab-179">Hello zagnieżdżania właściwości separatora jest używane toocreate hierarchicznych (podrzędne dokumenty) podczas importowania.</span><span class="sxs-lookup"><span data-stu-id="b68ab-179">hello nesting separator property is used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="b68ab-180">Należy wziąć pod uwagę następujące zapytanie SQL hello:</span><span class="sxs-lookup"><span data-stu-id="b68ab-180">Consider hello following SQL query:</span></span>

<span data-ttu-id="b68ab-181">*Wybierz RZUTOWANIA (BusinessEntityID AS varchar) jako identyfikator, nazwę, typ adresu jako [Address.AddressType], AddressLine1 jako [Address.AddressLine1], miasta jako [Address.Location.City], StateProvinceName jako [Address.Location.StateProvinceName], KodPocztowy jako [Address.PostalCode], CountryRegionName jako [Address.CountryRegionName] z Sales.vStoreWithAddresses gdzie typ adresu = "Urząd główny"*</span><span class="sxs-lookup"><span data-stu-id="b68ab-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="b68ab-182">Polecenie to zwraca hello następujące wyniki (częściowe):</span><span class="sxs-lookup"><span data-stu-id="b68ab-182">Which returns hello following (partial) results:</span></span>

![Zrzut ekranu SQL wyników zapytania](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="b68ab-184">Należy zwrócić uwagę hello aliasy, takie jak Address.AddressType i Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="b68ab-184">Note hello aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="b68ab-185">Określając zagnieżdżenia separatora z ".", narzędzia importu hello tworzy adres i zaimportować dokumenty podrzędne Address.Location podczas hello.</span><span class="sxs-lookup"><span data-stu-id="b68ab-185">By specifying a nesting separator of ‘.’, hello import tool creates Address and Address.Location subdocuments during hello import.</span></span> <span data-ttu-id="b68ab-186">Oto przykład wynikowy dokumentu w usłudze Azure DB rozwiązania Cosmos:</span><span class="sxs-lookup"><span data-stu-id="b68ab-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="b68ab-187">*{"id": "956", "Name": "Bardziej precyzyjną sprzedaży i usługa", "Adres": {"Typ adresu": "Urząd główny", "AddressLine1": "#500 75 O'Connor ulicy", "Lokalizacja": {"Miasto": "Ottawie", "StateProvinceName": "Ontario"}, "KodPocztowy": "K4B 1S2", "CountryRegionName": "Kanada"}}*</span><span class="sxs-lookup"><span data-stu-id="b68ab-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="b68ab-188">Poniżej przedstawiono niektóre wiersza polecenia tooimport przykłady z programu SQL Server:</span><span class="sxs-lookup"><span data-stu-id="b68ab-188">Here are some command line samples tooimport from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="b68ab-189"><a id="CSV"></a>pliki CSV tooimport i przekonwertować tooJSON CSV</span><span class="sxs-lookup"><span data-stu-id="b68ab-189"><a id="CSV"></a>tooimport CSV files and convert CSV tooJSON</span></span>
<span data-ttu-id="b68ab-190">Hello opcję importera źródło pliku CSV umożliwia możesz tooimport jeden lub więcej plików CSV.</span><span class="sxs-lookup"><span data-stu-id="b68ab-190">hello CSV file source importer option enables you tooimport one or more CSV files.</span></span> <span data-ttu-id="b68ab-191">Podczas dodawania foldery zawierające pliki CSV do zaimportowania, dostępna jest opcja hello rekursywnie szukania plików w podfolderach.</span><span class="sxs-lookup"><span data-stu-id="b68ab-191">When adding folders that contain CSV files for import, you have hello option of recursively searching for files in subfolders.</span></span>

![Zrzut ekranu CSV źródła opcji - CSV tooJSON](media/import-data/csvsource.png)

<span data-ttu-id="b68ab-193">Podobne toohello SQL źródło hello zagnieżdżania separatora właściwości może być używane toocreate hierarchicznych (podrzędne dokumenty) podczas importowania.</span><span class="sxs-lookup"><span data-stu-id="b68ab-193">Similar toohello SQL source, hello nesting separator property may be used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="b68ab-194">Należy wziąć pod uwagę hello wiersz nagłówka CSV i wierszy danych:</span><span class="sxs-lookup"><span data-stu-id="b68ab-194">Consider hello following CSV header row and data rows:</span></span>

![Zrzut ekranu CSV przykładowych rekordów - CSV tooJSON](./media/import-data/csvsample.png)

<span data-ttu-id="b68ab-196">Należy zwrócić uwagę hello aliasy, takie jak DomainInfo.Domain_Name i RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="b68ab-196">Note hello aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="b68ab-197">Określając zagnieżdżenia separatora z ".", narzędzia importu hello utworzy DomainInfo i zaimportować dokumenty podrzędne RedirectInfo podczas hello.</span><span class="sxs-lookup"><span data-stu-id="b68ab-197">By specifying a nesting separator of ‘.’, hello import tool will create DomainInfo and RedirectInfo subdocuments during hello import.</span></span> <span data-ttu-id="b68ab-198">Oto przykład wynikowy dokumentu w usłudze Azure DB rozwiązania Cosmos:</span><span class="sxs-lookup"><span data-stu-id="b68ab-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="b68ab-199">*{"DomainInfo": {"Nazwa_domeny": "ACUS.GOV", "Domain_Name_Address": "http://www. ACUS.GOV"},"Federalne agencji":"Administracyjne konferencji hello Stanów Zjednoczonych","RedirectInfo": {"Przekierowywanie":"0","Redirect_Destination":" "},"id":"9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d"}*</span><span class="sxs-lookup"><span data-stu-id="b68ab-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of hello United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="b68ab-200">Narzędzie importu Hello podejmie tooinfer informacji o typie wartości bez cudzysłowów w plikach CSV (wartości w cudzysłowie zawsze są traktowane jako ciągi).</span><span class="sxs-lookup"><span data-stu-id="b68ab-200">hello import tool will attempt tooinfer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="b68ab-201">Typy są identyfikowane w następującej kolejności hello: numer, datetime, boolean.</span><span class="sxs-lookup"><span data-stu-id="b68ab-201">Types are identified in hello following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="b68ab-202">Istnieją dwa inne toonote zagadnienia dotyczące importowania danych CSV:</span><span class="sxs-lookup"><span data-stu-id="b68ab-202">There are two other things toonote about CSV import:</span></span>

1. <span data-ttu-id="b68ab-203">Domyślnie bez cudzysłowów wartości są zawsze usuwane dla kart i spacje, gdy wartości w cudzysłowie są zachowywane jako — jest.</span><span class="sxs-lookup"><span data-stu-id="b68ab-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="b68ab-204">To zachowanie może zostać zastąpiona przez powitalne przycinanie podane wartości pola wyboru lub hello /s.TrimQuoted opcji wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b68ab-204">This behavior can be overridden with hello Trim quoted values checkbox or hello /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="b68ab-205">Domyślnie bez cudzysłowów wartość null jest traktowana jako wartość null.</span><span class="sxs-lookup"><span data-stu-id="b68ab-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="b68ab-206">To zachowanie można przesłonić (tj. Traktuj bez cudzysłowów null jako ciąg "null") z hello Traktuj nienotowane NULL jako ciąg wyboru lub hello /s.NoUnquotedNulls opcji wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="b68ab-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with hello Treat unquoted NULL as string checkbox or hello /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="b68ab-207">Oto przykład wiersza polecenia do importowania danych CSV:</span><span class="sxs-lookup"><span data-stu-id="b68ab-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="b68ab-208"><a id="AzureTableSource"></a>tooimport z magazynem tabel Azure</span><span class="sxs-lookup"><span data-stu-id="b68ab-208"><a id="AzureTableSource"></a>tooimport from Azure Table storage</span></span>
<span data-ttu-id="b68ab-209">Hello opcji importera źródłowego magazynu tabel Azure pozwala tooimport z pojedynczej tabeli magazynu tabel Azure i opcjonalnie filtrować toobe jednostek tabeli hello zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-209">hello Azure Table storage source importer option allows you tooimport from an individual Azure Table storage table and optionally filter hello table entities toobe imported.</span></span> <span data-ttu-id="b68ab-210">Pamiętaj, że danych magazynu tabel Azure tooimport narzędzia migracji danych hello nie można używać do bazy danych Azure rozwiązania Cosmos do użytku z hello tabeli interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b68ab-210">Note that you cannot use hello Data Migration tool tooimport Azure Table storage data into Azure Cosmos DB for use with hello Table API.</span></span> <span data-ttu-id="b68ab-211">Tylko importowanie tooAzure rozwiązania Cosmos DB do użycia z hello interfejsu API usługi DocumentDB jest obsługiwane w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="b68ab-211">Only importing tooAzure Cosmos DB for use with hello DocumentDB API is supported at this time.</span></span>

![Opcje źródłowego magazynu tabel zrzut ekranu Azure](./media/import-data/azuretablesource.png)

<span data-ttu-id="b68ab-213">format Hello hello parametry połączenia magazynu tabel Azure jest:</span><span class="sxs-lookup"><span data-stu-id="b68ab-213">hello format of hello Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="b68ab-214">Użyj hello Sprawdź polecenie tooensure, który hello określonego w polu Parametry połączenia hello wystąpienia magazynu tabel Azure są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b68ab-214">Use hello Verify command tooensure that hello Azure Table storage instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="b68ab-215">Wprowadź nazwę hello hello Azure tabeli, w którym dane zostaną zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-215">Enter hello name of hello Azure table from which data will be imported.</span></span> <span data-ttu-id="b68ab-216">Opcjonalnie można określić [filtru](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="b68ab-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="b68ab-217">Witaj opcji importera źródłowego magazynu tabel Azure ma hello następujące dodatkowe opcje:</span><span class="sxs-lookup"><span data-stu-id="b68ab-217">hello Azure Table storage source importer option has hello following additional options:</span></span>

1. <span data-ttu-id="b68ab-218">Uwzględnij pola wewnętrznego</span><span class="sxs-lookup"><span data-stu-id="b68ab-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="b68ab-219">-Obejmują wszystkie pola wewnętrzne (PartitionKey RowKey i sygnatura czasowa)</span><span class="sxs-lookup"><span data-stu-id="b68ab-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="b68ab-220">Brak — Wyklucz wszystkie pola wewnętrznego</span><span class="sxs-lookup"><span data-stu-id="b68ab-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="b68ab-221">RowKey - zawierać tylko pola RowKey hello</span><span class="sxs-lookup"><span data-stu-id="b68ab-221">RowKey - Only include hello RowKey field</span></span>
2. <span data-ttu-id="b68ab-222">Wybierz kolumny</span><span class="sxs-lookup"><span data-stu-id="b68ab-222">Select Columns</span></span>
   1. <span data-ttu-id="b68ab-223">Filtrów magazynu tabel Azure nie obsługuje prognoz.</span><span class="sxs-lookup"><span data-stu-id="b68ab-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="b68ab-224">Jeśli chcesz tooonly importu określonych właściwości jednostki tabel Azure, dodać je toohello wybierz kolumny listy.</span><span class="sxs-lookup"><span data-stu-id="b68ab-224">If you want tooonly import specific Azure Table entity properties, add them toohello Select Columns list.</span></span> <span data-ttu-id="b68ab-225">Wszystkie inne właściwości jednostki zostanie zignorowany.</span><span class="sxs-lookup"><span data-stu-id="b68ab-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="b68ab-226">Oto tooimport przykładowy wiersz polecenia z magazynem tabel Azure:</span><span class="sxs-lookup"><span data-stu-id="b68ab-226">Here is a command line sample tooimport from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="b68ab-227"><a id="DynamoDBSource"></a>tooimport z Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="b68ab-227"><a id="DynamoDBSource"></a>tooimport from Amazon DynamoDB</span></span>
<span data-ttu-id="b68ab-228">Hello opcję importera źródło Amazon DynamoDB pozwala tooimport z pojedynczej tabeli Amazon DynamoDB i opcjonalnie filtrować toobe jednostek hello zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-228">hello Amazon DynamoDB source importer option allows you tooimport from an individual Amazon DynamoDB table and optionally filter hello entities toobe imported.</span></span> <span data-ttu-id="b68ab-229">Kilka szablonów znajdują się tak, aby ustawienie importu jest równie proste, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="b68ab-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Zrzut ekranu Amazon DynamoDB Opcje źródła - narzędzia migracji bazy danych](./media/import-data/dynamodbsource1.png)

![Zrzut ekranu Amazon DynamoDB Opcje źródła - narzędzia migracji bazy danych](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="b68ab-232">format Hello hello Amazon DynamoDB ciągu połączenia jest:</span><span class="sxs-lookup"><span data-stu-id="b68ab-232">hello format of hello Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="b68ab-233">Użyj hello Sprawdź polecenie tooensure, który hello Amazon DynamoDB wystąpienia określonego w polu Parametry połączenia hello są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b68ab-233">Use hello Verify command tooensure that hello Amazon DynamoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="b68ab-234">Oto tooimport przykładowy wiersz polecenia z Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="b68ab-234">Here is a command line sample tooimport from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="b68ab-235"><a id="BlobImport"></a>tooimport pliki z magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b68ab-235"><a id="BlobImport"></a>tooimport files from Azure Blob storage</span></span>
<span data-ttu-id="b68ab-236">Witaj pliku JSON, plik eksportu bazy danych MongoDB i opcje importera źródło pliku CSV pozwala tooimport co najmniej jeden plik z magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b68ab-236">hello JSON file, MongoDB export file, and CSV file source importer options allow you tooimport one or more files from Azure Blob storage.</span></span> <span data-ttu-id="b68ab-237">Po określeniu adresu URL kontenera obiektów Blob i klucza konta, wystarczy podać wyrażenie regularne tooselect hello pliki tooimport.</span><span class="sxs-lookup"><span data-stu-id="b68ab-237">After specifying a Blob container URL and Account Key, simply provide a regular expression tooselect hello file(s) tooimport.</span></span>

![Opcje źródłowego pliku zrzutu ekranu obiektów Blob](./media/import-data/blobsource.png)

<span data-ttu-id="b68ab-239">Poniżej przedstawiono pliki JSON tooimport przykładowy wiersz polecenia z magazynu obiektów Blob platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="b68ab-239">Here is command line sample tooimport JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="b68ab-240"><a id="DocumentDBSource"></a>tooimport z kolekcji interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b68ab-240"><a id="DocumentDBSource"></a>tooimport from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="b68ab-241">Hello opcja importera źródłowej bazy danych Azure rozwiązania Cosmos pozwala tooimport danych z jednej lub kilku kolekcjach bazy danych Azure rozwiązania Cosmos i opcjonalnie filtrować dokumentów za pomocą zapytania.</span><span class="sxs-lookup"><span data-stu-id="b68ab-241">hello Azure Cosmos DB source importer option allows you tooimport data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Opcje źródła zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/documentdbsource.png)

<span data-ttu-id="b68ab-243">format Hello hello parametry połączenia bazy danych Azure rozwiązania Cosmos jest:</span><span class="sxs-lookup"><span data-stu-id="b68ab-243">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="b68ab-244">Witaj parametry połączenia bazy danych Azure rozwiązania Cosmos konta można pobrać z bloku klucze hello hello portalu Azure, zgodnie z opisem w [jak toomanage konta bazy danych Azure rozwiązania Cosmos](manage-account.md), ale nazwa hello hello bazy danych musi toohello toobe dołączone Parametry połączenia w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="b68ab-244">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="b68ab-245">Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie bazy danych Azure rozwiązania Cosmos w polu Parametry połączenia hello są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b68ab-245">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="b68ab-246">tooimport z jednej bazy danych Azure rozwiązania Cosmos kolekcji, wprowadź nazwę hello hello kolekcji, w którym dane zostaną zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-246">tooimport from a single Azure Cosmos DB collection, enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="b68ab-247">tooimport z wielu kolekcji bazy danych Azure rozwiązania Cosmos, podaj toomatch wyrażenia regularnego co najmniej jedną nazwę kolekcji (np. collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="b68ab-247">tooimport from multiple Azure Cosmos DB collections, provide a regular expression toomatch one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="b68ab-248">Może opcjonalnie określić, lub określ plik dla filtru tooboth zapytania i kształtu toobe danych hello zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-248">You may optionally specify, or provide a file for, a query tooboth filter and shape hello data toobe imported.</span></span>

> [!NOTE]
> <span data-ttu-id="b68ab-249">Ponieważ pola kolekcji hello akceptuje wyrażeń regularnych, jeśli import odbywa się z jednej kolekcji, których nazwa zawiera znaki wyrażenie regularne, te znaki muszą wyjściowym odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="b68ab-249">Since hello collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="b68ab-250">Hello opcja importera źródłowej bazy danych Azure rozwiązania Cosmos ma następujące hello zaawansowane opcje:</span><span class="sxs-lookup"><span data-stu-id="b68ab-250">hello Azure Cosmos DB source importer option has hello following advanced options:</span></span>

1. <span data-ttu-id="b68ab-251">Obejmują pola wewnętrzne: Określa, czy właściwości systemu dokumentu tooinclude bazy danych Azure rozwiązania Cosmos w hello eksportu (np. _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="b68ab-251">Include Internal Fields: Specifies whether or not tooinclude Azure Cosmos DB document system properties in hello export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="b68ab-252">Liczba ponownych prób w przypadku niepowodzenia: Określa hello liczba tooretry hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).</span><span class="sxs-lookup"><span data-stu-id="b68ab-252">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="b68ab-253">Interwał ponawiania prób: Określa, jak długo toowait między ponawianie próby hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).</span><span class="sxs-lookup"><span data-stu-id="b68ab-253">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="b68ab-254">Tryb połączenia: Określa toouse tryb połączenia hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b68ab-254">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="b68ab-255">dostępne opcje Hello są DirectTcp, DirectHttps i bramy.</span><span class="sxs-lookup"><span data-stu-id="b68ab-255">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="b68ab-256">tryby bezpośrednie połączenie Hello są szybsze, gdy tryb bramy hello jest więcej zapory przyjazną, ponieważ używa ona tylko port 443.</span><span class="sxs-lookup"><span data-stu-id="b68ab-256">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Zaawansowane opcje źródła zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="b68ab-258">Witaj zaimportować tryb tooconnection domyślne narzędzie DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="b68ab-258">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="b68ab-259">Występują problemy z zaporą, Przełącz tryb tooconnection bramy, ponieważ wymaga ona tylko portu 443.</span><span class="sxs-lookup"><span data-stu-id="b68ab-259">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="b68ab-260">Poniżej przedstawiono niektóre tooimport przykłady wiersza polecenia z bazy danych rozwiązania Cosmos Azure:</span><span class="sxs-lookup"><span data-stu-id="b68ab-260">Here are some command line samples tooimport from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="b68ab-261">Hello narzędzia importowania danych DB rozwiązania Cosmos Azure obsługuje również importowanie danych z hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="b68ab-261">hello Azure Cosmos DB Data Import Tool also supports import of data from hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="b68ab-262">Podczas importowania danych z lokalnego emulatora, ustaw punkt końcowy hello zbyt`https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="b68ab-262">When importing data from a local emulator, set hello endpoint too`https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="b68ab-263"><a id="HBaseSource"></a>tooimport z bazy danych HBase</span><span class="sxs-lookup"><span data-stu-id="b68ab-263"><a id="HBaseSource"></a>tooimport from HBase</span></span>
<span data-ttu-id="b68ab-264">Hello opcję importera źródło HBase pozwala tooimport dane z tabel HBase i opcjonalnie filtrowanie hello danych.</span><span class="sxs-lookup"><span data-stu-id="b68ab-264">hello HBase source importer option allows you tooimport data from an HBase table and optionally filter hello data.</span></span> <span data-ttu-id="b68ab-265">Kilka szablonów znajdują się tak, aby ustawienie importu jest równie proste, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="b68ab-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Zrzut ekranu HBase Opcje źródła](./media/import-data/hbasesource1.png)

![Zrzut ekranu HBase Opcje źródła](./media/import-data/hbasesource2.png)

<span data-ttu-id="b68ab-268">format Hello hello parametry połączenia bazy danych HBase Stargate jest:</span><span class="sxs-lookup"><span data-stu-id="b68ab-268">hello format of hello HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="b68ab-269">Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie bazy danych HBase w polu Parametry połączenia hello są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b68ab-269">Use hello Verify command tooensure that hello HBase instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="b68ab-270">Oto tooimport przykładowy wiersz polecenia z bazy danych HBase:</span><span class="sxs-lookup"><span data-stu-id="b68ab-270">Here is a command line sample tooimport from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="b68ab-271"><a id="DocumentDBBulkTarget"></a>toohello tooimport interfejsu API usługi DocumentDB (importowania zbiorczego)</span><span class="sxs-lookup"><span data-stu-id="b68ab-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="b68ab-272">importer Azure rozwiązania Cosmos DB zbiorczego Hello umożliwia tooimport z dowolnego z opcjami dostępnego źródła hello przy użyciu procedury przechowywane bazy danych rozwiązania Cosmos Azure w celu zwiększenia wydajności.</span><span class="sxs-lookup"><span data-stu-id="b68ab-272">hello Azure Cosmos DB Bulk importer allows you tooimport from any of hello available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="b68ab-273">Narzędzie Hello obsługuje importu tooone podzielona na partycje pojedynczej bazy danych Azure rozwiązania Cosmos kolekcji, a także podzielonej importu, zgodnie z którymi danych jest podzielonym na partycje w wielu kolekcji podzielone na partycje pojedynczej bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b68ab-273">hello tool supports import tooone single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="b68ab-274">Aby uzyskać więcej informacji na temat partycjonowania danych, zobacz [dzielenia na partycje i skalowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="b68ab-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="b68ab-275">Narzędzie Hello będzie utworzyć, wykonanie, a następnie usuń hello przechowywane procedury hello kolekcji docelowej.</span><span class="sxs-lookup"><span data-stu-id="b68ab-275">hello tool will create, execute, and then delete hello stored procedure from hello target collection(s).</span></span>  

![Opcje zbiorczego zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/documentdbbulk.png)

<span data-ttu-id="b68ab-277">format Hello hello parametry połączenia bazy danych Azure rozwiązania Cosmos jest:</span><span class="sxs-lookup"><span data-stu-id="b68ab-277">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="b68ab-278">Witaj parametry połączenia bazy danych Azure rozwiązania Cosmos konta można pobrać z bloku klucze hello hello portalu Azure, zgodnie z opisem w [jak toomanage konta bazy danych Azure rozwiązania Cosmos](manage-account.md), ale nazwa hello hello bazy danych musi toohello toobe dołączone Parametry połączenia w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="b68ab-278">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="b68ab-279">Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie bazy danych Azure rozwiązania Cosmos w polu Parametry połączenia hello są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b68ab-279">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="b68ab-280">tooimport tooa pojedynczy kolekcji, wprowadź nazwę hello hello kolekcji toowhich dane zostaną zaimportowane i kliknij przycisk Dodaj hello.</span><span class="sxs-lookup"><span data-stu-id="b68ab-280">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="b68ab-281">tooimport toomultiple kolekcje, wprowadź nazwy kolekcji indywidualnie lub użyj następującej składni toospecify hello wielu kolekcji: *collection_prefix*[Indeks - end indeks początkowy].</span><span class="sxs-lookup"><span data-stu-id="b68ab-281">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="b68ab-282">Podczas określania wielu kolekcji za pomocą składni wyżej wymienione hello, pamiętać o następujących hello:</span><span class="sxs-lookup"><span data-stu-id="b68ab-282">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="b68ab-283">Obsługiwane są tylko liczby całkowitej wzorce nazwy zakresu.</span><span class="sxs-lookup"><span data-stu-id="b68ab-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="b68ab-284">Na przykład określenie kolekcji [0-3] utworzy hello następujące kolekcje: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="b68ab-284">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="b68ab-285">Za pomocą składni skróconej: kolekcji [3] będzie emitować tego samego zestawu kolekcje wymienionych w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="b68ab-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="b68ab-286">Można podać więcej niż jeden podstawienia.</span><span class="sxs-lookup"><span data-stu-id="b68ab-286">More than one substitution can be provided.</span></span> <span data-ttu-id="b68ab-287">Na przykład, Kolekcja [0-1] [0-9] wygeneruje 20 nazwy kolekcji z zerami (collection01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="b68ab-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="b68ab-288">Po hello kolekcji nazwy zostały określone, wybrać żądaną przepływność hello hello kolekcji (400 RUs too10, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="b68ab-288">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too10,000 RUs).</span></span> <span data-ttu-id="b68ab-289">Aby uzyskać najlepszą wydajność importu wybierz wyższej przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b68ab-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="b68ab-290">Aby uzyskać więcej informacji na temat poziomów wydajności, zobacz [poziomy wydajności w usłudze Azure DB rozwiązania Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="b68ab-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b68ab-291">Witaj wydajności przepływności ustawienie dotyczy tylko tworzenie toocollection.</span><span class="sxs-lookup"><span data-stu-id="b68ab-291">hello performance throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="b68ab-292">Witaj określona kolekcja już istnieje, jej przepływności nie zostaną zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-292">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="b68ab-293">Podczas importowania toomultiple kolekcje, narzędzia importu hello obsługuje skrótu na podstawie dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="b68ab-293">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="b68ab-294">W tym scenariuszu, określ właściwość dokumentu hello mają toouse jako klucza partycji hello (Jeśli klucz partycji jest puste, dokumenty będą podzielonej losowo w kolekcji docelowej hello).</span><span class="sxs-lookup"><span data-stu-id="b68ab-294">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="b68ab-295">Opcjonalnie można określić które pole w źródle importu hello powinna być używana jako hello właściwość identyfikatora dokumentu bazy danych Azure rozwiązania Cosmos podczas importowania hello (należy pamiętać, że jeśli dokumenty nie zawierają tej właściwości, następnie narzędzia importu hello wygeneruje GUID jako wartość właściwości identyfikator hello).</span><span class="sxs-lookup"><span data-stu-id="b68ab-295">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="b68ab-296">Brak dostępnych kilka opcji zaawansowanych podczas importowania.</span><span class="sxs-lookup"><span data-stu-id="b68ab-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="b68ab-297">Najpierw gdy narzędzie hello zawiera zbiorczego domyślne importowania procedury składowanej (BulkInsert.js), można wybrać toospecify procedura przechowywana importu:</span><span class="sxs-lookup"><span data-stu-id="b68ab-297">First, while hello tool includes a default bulk import stored procedure (BulkInsert.js), you may choose toospecify your own import stored procedure:</span></span>

 ![Opcje sproc wstawiania zbiorczego zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="b68ab-299">Ponadto podczas importowania typów danych (np. z serwera SQL lub bazy danych MongoDB), można wybrać jedną z trzech opcji importowania:</span><span class="sxs-lookup"><span data-stu-id="b68ab-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Opcje importowania czasu Data zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="b68ab-301">Ciąg: Wartość ciągu utrzymana</span><span class="sxs-lookup"><span data-stu-id="b68ab-301">String: Persist as a string value</span></span>
* <span data-ttu-id="b68ab-302">Epoka: Utrwalić jako wartość liczbową epoka.</span><span class="sxs-lookup"><span data-stu-id="b68ab-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="b68ab-303">Zarówno: Utrwalanie zarówno ciąg, jak i epoki wartości liczbowe.</span><span class="sxs-lookup"><span data-stu-id="b68ab-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="b68ab-304">Ta opcja spowoduje utworzenie podrzędnego, na przykład: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "epoki": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="b68ab-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="b68ab-305">Hello Azure rozwiązania Cosmos DB zbiorczego importer ma hello następujące dodatkowe opcje zaawansowane:</span><span class="sxs-lookup"><span data-stu-id="b68ab-305">hello Azure Cosmos DB Bulk importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="b68ab-306">Rozmiar partii: hello narzędzia domyślne tooa rozmiar partii 50.</span><span class="sxs-lookup"><span data-stu-id="b68ab-306">Batch Size: hello tool defaults tooa batch size of 50.</span></span>  <span data-ttu-id="b68ab-307">W przypadku dużych toobe dokumenty hello zaimportowane należy wziąć pod uwagę obniżenia hello rozmiar partii.</span><span class="sxs-lookup"><span data-stu-id="b68ab-307">If hello documents toobe imported are large, consider lowering hello batch size.</span></span> <span data-ttu-id="b68ab-308">Z drugiej strony w przypadku małych toobe dokumenty hello zaimportowane należy rozważyć zwiększenie rozmiaru partii hello.</span><span class="sxs-lookup"><span data-stu-id="b68ab-308">Conversely, if hello documents toobe imported are small, consider raising hello batch size.</span></span>
2. <span data-ttu-id="b68ab-309">Maksymalny rozmiar skryptu (w bajtach): narzędzie hello domyślne tooa skryptu Maksymalny rozmiar 512 KB</span><span class="sxs-lookup"><span data-stu-id="b68ab-309">Max Script Size (bytes): hello tool defaults tooa max script size of 512KB</span></span>
3. <span data-ttu-id="b68ab-310">Wyłącz automatyczne generowanie identyfikator: Jeśli każdego toobe dokumentu zaimportowane zawiera pole identyfikatora, wybierając tę opcję można zwiększyć wydajność.</span><span class="sxs-lookup"><span data-stu-id="b68ab-310">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="b68ab-311">Brak pola Unikatowy identyfikator dokumenty nie zostaną zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="b68ab-312">Aktualizacja istniejące dokumenty: hello toonot domyślne narzędzie zastępowanie istniejących dokumentów konflikt identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="b68ab-312">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="b68ab-313">Wybranie tej opcji pozwoli zastępowanie istniejących dokumentów ze zgodnymi identyfikatorami.</span><span class="sxs-lookup"><span data-stu-id="b68ab-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="b68ab-314">Ta funkcja jest przydatne w przypadku migracji danych zaplanowane, które zaktualizować istniejące dokumenty.</span><span class="sxs-lookup"><span data-stu-id="b68ab-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="b68ab-315">Liczba ponownych prób w przypadku niepowodzenia: Określa hello liczba tooretry hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).</span><span class="sxs-lookup"><span data-stu-id="b68ab-315">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="b68ab-316">Interwał ponawiania prób: Określa, jak długo toowait między ponawianie próby hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).</span><span class="sxs-lookup"><span data-stu-id="b68ab-316">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="b68ab-317">Tryb połączenia: Określa toouse tryb połączenia hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b68ab-317">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="b68ab-318">dostępne opcje Hello są DirectTcp, DirectHttps i bramy.</span><span class="sxs-lookup"><span data-stu-id="b68ab-318">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="b68ab-319">tryby bezpośrednie połączenie Hello są szybsze, gdy tryb bramy hello jest więcej zapory przyjazną, ponieważ używa ona tylko port 443.</span><span class="sxs-lookup"><span data-stu-id="b68ab-319">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Zaawansowane opcje importowania zbiorczego zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="b68ab-321">Witaj zaimportować tryb tooconnection domyślne narzędzie DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="b68ab-321">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="b68ab-322">Występują problemy z zaporą, Przełącz tryb tooconnection bramy, ponieważ wymaga ona tylko portu 443.</span><span class="sxs-lookup"><span data-stu-id="b68ab-322">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="b68ab-323"><a id="DocumentDBSeqTarget"></a>toohello tooimport interfejsu API usługi DocumentDB (sekwencyjnych importowanie rekordów)</span><span class="sxs-lookup"><span data-stu-id="b68ab-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="b68ab-324">importer sekwencyjnych rekordu bazy danych Azure rozwiązania Cosmos Hello umożliwia tooimport z Opcje dostępnego źródła hello na podstawie rekordu na podstawie.</span><span class="sxs-lookup"><span data-stu-id="b68ab-324">hello Azure Cosmos DB sequential record importer allows you tooimport from any of hello available source options on a record by record basis.</span></span> <span data-ttu-id="b68ab-325">Możesz wybrać tę opcję, jeśli importowany tooan istniejącą kolekcję, która osiągnęła limit przydziału procedur składowanych.</span><span class="sxs-lookup"><span data-stu-id="b68ab-325">You might choose this option if you’re importing tooan existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="b68ab-326">Witaj narzędzie obsługuje importu tooa pojedynczy kolekcji bazy danych Azure rozwiązania Cosmos (jednej partycji i wielu partycji), a także podzielonej importu, zgodnie z którymi danych jest podzielona na partycje w wielu kolekcjach bazy danych Azure rozwiązania Cosmos jednej partycji i/lub wielu partycji.</span><span class="sxs-lookup"><span data-stu-id="b68ab-326">hello tool supports import tooa single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="b68ab-327">Aby uzyskać więcej informacji na temat partycjonowania danych, zobacz [dzielenia na partycje i skalowania w usłudze Azure DB rozwiązania Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="b68ab-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Zrzut ekranu Azure DB rozwiązania Cosmos opcje sekwencyjnych importowania rekordów](./media/import-data/documentdbsequential.png)

<span data-ttu-id="b68ab-329">format Hello hello parametry połączenia bazy danych Azure rozwiązania Cosmos jest:</span><span class="sxs-lookup"><span data-stu-id="b68ab-329">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="b68ab-330">Witaj parametry połączenia bazy danych Azure rozwiązania Cosmos konta można pobrać z bloku klucze hello hello portalu Azure, zgodnie z opisem w [jak toomanage konta bazy danych Azure rozwiązania Cosmos](manage-account.md), ale nazwa hello hello bazy danych musi toohello toobe dołączone Parametry połączenia w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="b68ab-330">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="b68ab-331">Użyj hello Sprawdź polecenie tooensure, który hello wystąpienie bazy danych Azure rozwiązania Cosmos w polu Parametry połączenia hello są dostępne.</span><span class="sxs-lookup"><span data-stu-id="b68ab-331">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="b68ab-332">tooimport tooa pojedynczy kolekcji, wprowadź nazwę hello hello kolekcji toowhich dane zostaną zaimportowane i kliknij przycisk Dodaj hello.</span><span class="sxs-lookup"><span data-stu-id="b68ab-332">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="b68ab-333">tooimport toomultiple kolekcje, wprowadź nazwy kolekcji indywidualnie lub użyj następującej składni toospecify hello wielu kolekcji: *collection_prefix*[Indeks - end indeks początkowy].</span><span class="sxs-lookup"><span data-stu-id="b68ab-333">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="b68ab-334">Podczas określania wielu kolekcji za pomocą składni wyżej wymienione hello, pamiętać o następujących hello:</span><span class="sxs-lookup"><span data-stu-id="b68ab-334">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="b68ab-335">Obsługiwane są tylko liczby całkowitej wzorce nazwy zakresu.</span><span class="sxs-lookup"><span data-stu-id="b68ab-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="b68ab-336">Na przykład określenie kolekcji [0-3] utworzy hello następujące kolekcje: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="b68ab-336">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="b68ab-337">Za pomocą składni skróconej: kolekcji [3] będzie emitować tego samego zestawu kolekcje wymienionych w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="b68ab-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="b68ab-338">Można podać więcej niż jeden podstawienia.</span><span class="sxs-lookup"><span data-stu-id="b68ab-338">More than one substitution can be provided.</span></span> <span data-ttu-id="b68ab-339">Na przykład, Kolekcja [0-1] [0-9] wygeneruje 20 nazwy kolekcji z zerami (collection01,... 02... 03).</span><span class="sxs-lookup"><span data-stu-id="b68ab-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="b68ab-340">Po hello kolekcji nazwy zostały określone, wybrać żądaną przepływność hello hello kolekcji (400 RUs too250, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="b68ab-340">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too250,000 RUs).</span></span> <span data-ttu-id="b68ab-341">Aby uzyskać najlepszą wydajność importu wybierz wyższej przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b68ab-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="b68ab-342">Aby uzyskać więcej informacji na temat poziomów wydajności, zobacz [poziomy wydajności w usłudze Azure DB rozwiązania Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="b68ab-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="b68ab-343">Wszelkie zaimportować toocollections o przepływności > 10 000 RUs będzie wymagać klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="b68ab-343">Any import toocollections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="b68ab-344">Jeśli wybierzesz toohave więcej niż 250 000 RUs, konieczne będzie toofile żądania w portalu toohave hello zwiększyć Twoje konto.</span><span class="sxs-lookup"><span data-stu-id="b68ab-344">If you choose toohave more than 250,000 RUs, you will need toofile a request in hello portal toohave your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="b68ab-345">Witaj przepływności ustawienie dotyczy tylko tworzenie toocollection.</span><span class="sxs-lookup"><span data-stu-id="b68ab-345">hello throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="b68ab-346">Witaj określona kolekcja już istnieje, jej przepływności nie zostaną zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-346">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="b68ab-347">Podczas importowania toomultiple kolekcje, narzędzia importu hello obsługuje skrótu na podstawie dzielenia na fragmenty.</span><span class="sxs-lookup"><span data-stu-id="b68ab-347">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="b68ab-348">W tym scenariuszu, określ właściwość dokumentu hello mają toouse jako klucza partycji hello (Jeśli klucz partycji jest puste, dokumenty będą podzielonej losowo w kolekcji docelowej hello).</span><span class="sxs-lookup"><span data-stu-id="b68ab-348">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="b68ab-349">Opcjonalnie można określić które pole w źródle importu hello powinna być używana jako hello właściwość identyfikatora dokumentu bazy danych Azure rozwiązania Cosmos podczas importowania hello (należy pamiętać, że jeśli dokumenty nie zawierają tej właściwości, następnie narzędzia importu hello wygeneruje GUID jako wartość właściwości identyfikator hello).</span><span class="sxs-lookup"><span data-stu-id="b68ab-349">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="b68ab-350">Brak dostępnych kilka opcji zaawansowanych podczas importowania.</span><span class="sxs-lookup"><span data-stu-id="b68ab-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="b68ab-351">Po pierwsze podczas importowania typów danych (np. z serwera SQL lub bazy danych MongoDB), można wybrać jedną z trzech opcji importowania:</span><span class="sxs-lookup"><span data-stu-id="b68ab-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Opcje importowania czasu Data zrzut ekranu z rozwiązania Cosmos bazy danych Azure](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="b68ab-353">Ciąg: Wartość ciągu utrzymana</span><span class="sxs-lookup"><span data-stu-id="b68ab-353">String: Persist as a string value</span></span>
* <span data-ttu-id="b68ab-354">Epoka: Utrwalić jako wartość liczbową epoka.</span><span class="sxs-lookup"><span data-stu-id="b68ab-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="b68ab-355">Zarówno: Utrwalanie zarówno ciąg, jak i epoki wartości liczbowe.</span><span class="sxs-lookup"><span data-stu-id="b68ab-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="b68ab-356">Ta opcja spowoduje utworzenie podrzędnego, na przykład: "date_joined": {"Value": "2013-10-21T21:17:25.2410000Z", "epoki": 1382390245}</span><span class="sxs-lookup"><span data-stu-id="b68ab-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="b68ab-357">Hello Azure DB rozwiązania Cosmos — importer kolejny rekord ma hello następujące dodatkowe opcje zaawansowane:</span><span class="sxs-lookup"><span data-stu-id="b68ab-357">hello Azure Cosmos DB - Sequential record importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="b68ab-358">Liczba żądań równoległych: narzędzie hello domyślne too2 równoległych żądań.</span><span class="sxs-lookup"><span data-stu-id="b68ab-358">Number of Parallel Requests: hello tool defaults too2 parallel requests.</span></span> <span data-ttu-id="b68ab-359">W przypadku małych toobe dokumenty hello zaimportowane należy rozważyć zwiększenie numeru hello równoległych żądań.</span><span class="sxs-lookup"><span data-stu-id="b68ab-359">If hello documents toobe imported are small, consider raising hello number of parallel requests.</span></span> <span data-ttu-id="b68ab-360">Należy pamiętać, że jeśli ta liczba jest wywoływane zbyt dużo hello importu mogą wystąpić ograniczenia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b68ab-360">Note that if this number is raised too much, hello import may experience throttling.</span></span>
2. <span data-ttu-id="b68ab-361">Wyłącz automatyczne generowanie identyfikator: Jeśli każdego toobe dokumentu zaimportowane zawiera pole identyfikatora, wybierając tę opcję można zwiększyć wydajność.</span><span class="sxs-lookup"><span data-stu-id="b68ab-361">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="b68ab-362">Brak pola Unikatowy identyfikator dokumenty nie zostaną zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="b68ab-363">Aktualizacja istniejące dokumenty: hello toonot domyślne narzędzie zastępowanie istniejących dokumentów konflikt identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="b68ab-363">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="b68ab-364">Wybranie tej opcji pozwoli zastępowanie istniejących dokumentów ze zgodnymi identyfikatorami.</span><span class="sxs-lookup"><span data-stu-id="b68ab-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="b68ab-365">Ta funkcja jest przydatne w przypadku migracji danych zaplanowane, które zaktualizować istniejące dokumenty.</span><span class="sxs-lookup"><span data-stu-id="b68ab-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="b68ab-366">Liczba ponownych prób w przypadku niepowodzenia: Określa hello liczba tooretry hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).</span><span class="sxs-lookup"><span data-stu-id="b68ab-366">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="b68ab-367">Interwał ponawiania prób: Określa, jak długo toowait między ponawianie próby hello połączenia tooAzure DB rozwiązania Cosmos w przypadku błędów przejściowych (np. łączność przerwy w działaniu sieci).</span><span class="sxs-lookup"><span data-stu-id="b68ab-367">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="b68ab-368">Tryb połączenia: Określa toouse tryb połączenia hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b68ab-368">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="b68ab-369">dostępne opcje Hello są DirectTcp, DirectHttps i bramy.</span><span class="sxs-lookup"><span data-stu-id="b68ab-369">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="b68ab-370">tryby bezpośrednie połączenie Hello są szybsze, gdy tryb bramy hello jest więcej zapory przyjazną, ponieważ używa ona tylko port 443.</span><span class="sxs-lookup"><span data-stu-id="b68ab-370">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Zrzut ekranu z rozwiązania Cosmos bazy danych platformy Azure kolejny rekord importu zaawansowane opcje](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="b68ab-372">Witaj zaimportować tryb tooconnection domyślne narzędzie DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="b68ab-372">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="b68ab-373">Występują problemy z zaporą, Przełącz tryb tooconnection bramy, ponieważ wymaga ona tylko portu 443.</span><span class="sxs-lookup"><span data-stu-id="b68ab-373">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="b68ab-374"><a id="IndexingPolicy"></a>Określ zasady indeksowania, podczas tworzenia kolekcji bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="b68ab-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="b68ab-375">Jeśli zezwolisz na powitania migracji kolekcji toocreate narzędzie podczas importowania, można określić zasady indeksowania hello hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="b68ab-375">When you allow hello migration tool toocreate collections during import, you can specify hello indexing policy of hello collections.</span></span> <span data-ttu-id="b68ab-376">W hello zaawansowane opcje sekcji hello pomocą importowania zbiorczego DB rozwiązania Cosmos Azure oraz Azure rozwiązania Cosmos DB sekwencyjnych opcje rekordu Przejdź toohello zasady indeksowania sekcji.</span><span class="sxs-lookup"><span data-stu-id="b68ab-376">In hello advanced options section of hello Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate toohello Indexing Policy section.</span></span>

![Zrzut ekranu Azure rozwiązania Cosmos DB indeksowania zasad opcje zaawansowane](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="b68ab-378">Przy użyciu hello opcja zasady indeksowania, zaawansowane, wybierz plik zasady indeksowania, ręcznie wprowadzić zasady indeksowania lub wybierać zestaw domyślnych szablonów (przez kliknięcie prawym przyciskiem myszy w hello indeksowania pola tekstowego zasad).</span><span class="sxs-lookup"><span data-stu-id="b68ab-378">Using hello Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in hello indexing policy textbox).</span></span>

<span data-ttu-id="b68ab-379">Szablony zasad Hello, które udostępnia narzędzie hello są:</span><span class="sxs-lookup"><span data-stu-id="b68ab-379">hello policy templates hello tool provides are:</span></span>

* <span data-ttu-id="b68ab-380">Domyślne.</span><span class="sxs-lookup"><span data-stu-id="b68ab-380">Default.</span></span> <span data-ttu-id="b68ab-381">Ta zasada jest najlepszy, gdy jest wykonywanie zapytań o równość dotyczących ciągów oraz przy użyciu ORDER BY, zakresu i zapytań o równość dotyczących liczb.</span><span class="sxs-lookup"><span data-stu-id="b68ab-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="b68ab-382">Ta zasada ma mniejszy narzut magazynu indeksu niż zakres.</span><span class="sxs-lookup"><span data-stu-id="b68ab-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="b68ab-383">Zakres.</span><span class="sxs-lookup"><span data-stu-id="b68ab-383">Range.</span></span> <span data-ttu-id="b68ab-384">Ta zasada jest najlepszym, że używasz zapytań ORDER BY, o zakres i równości na liczb i ciągów.</span><span class="sxs-lookup"><span data-stu-id="b68ab-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="b68ab-385">Ta zasada ma wyższy narzut na przechowywanie indeksu niż domyślne lub wyznaczania wartości skrótu.</span><span class="sxs-lookup"><span data-stu-id="b68ab-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Zrzut ekranu Azure rozwiązania Cosmos DB indeksowania zasad opcje zaawansowane](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="b68ab-387">Jeśli nie określisz zasady indeksowania, hello domyślne zasady zostaną zastosowane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-387">If you do not specify an indexing policy, then hello default policy will be applied.</span></span> <span data-ttu-id="b68ab-388">Aby uzyskać więcej informacji na temat zasad indeksowania, zobacz [Azure DB rozwiązania Cosmos zasady indeksowania](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b68ab-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-toojson-file"></a><span data-ttu-id="b68ab-389">Eksportuj plik tooJSON</span><span class="sxs-lookup"><span data-stu-id="b68ab-389">Export tooJSON file</span></span>
<span data-ttu-id="b68ab-390">Hello Azure rozwiązania Cosmos bazy danych JSON eksportera umożliwia tooexport żadnego hello dostępnego źródła opcje tooa pliku JSON, który zawiera tablicę dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="b68ab-390">hello Azure Cosmos DB JSON exporter allows you tooexport any of hello available source options tooa JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="b68ab-391">Narzędzie Hello obsłuży hello eksportu dla Ciebie lub polecenie tooview hello wynikowy migracji i uruchom polecenie hello samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="b68ab-391">hello tool will handle hello export for you, or you can choose tooview hello resulting migration command and run hello command yourself.</span></span> <span data-ttu-id="b68ab-392">Wynikowy plik JSON Hello mogą być przechowywane lokalnie lub w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="b68ab-392">hello resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Opcja eksportowania pliku lokalnego zrzut ekranu z Azure rozwiązania Cosmos bazy danych JSON](./media/import-data/jsontarget.png)

![Opcja eksportowania magazynu zrzut ekranu z rozwiązania Cosmos bazy danych JSON Azure obiektów Blob platformy Azure](./media/import-data/jsontarget2.png)

<span data-ttu-id="b68ab-395">Opcjonalnie można hello tooprettify wynikowa JSON, który spowoduje zwiększenie rozmiaru hello hello utworzonego dokumentu, podczas wprowadzania hello zawartości więcej do odczytu.</span><span class="sxs-lookup"><span data-stu-id="b68ab-395">You may optionally choose tooprettify hello resulting JSON, which will increase hello size of hello resulting document while making hello contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="b68ab-396">Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="b68ab-396">Advanced configuration</span></span>
<span data-ttu-id="b68ab-397">Na ekranie konfiguracji zaawansowanej hello Określ lokalizację hello toowhich pliku dziennika hello ma błędy zapisane.</span><span class="sxs-lookup"><span data-stu-id="b68ab-397">In hello Advanced configuration screen, specify hello location of hello log file toowhich you would like any errors written.</span></span> <span data-ttu-id="b68ab-398">następujące reguły Hello stosowanie toothis strony:</span><span class="sxs-lookup"><span data-stu-id="b68ab-398">hello following rules apply toothis page:</span></span>

1. <span data-ttu-id="b68ab-399">Jeśli nie podano nazwy pliku, na stronie wyników hello zwracane jest wszystkie błędy.</span><span class="sxs-lookup"><span data-stu-id="b68ab-399">If a file name is not provided, then all errors will be returned on hello Results page.</span></span>
2. <span data-ttu-id="b68ab-400">Jeśli nazwa pliku bez katalogu, zostanie następnie hello plik zostanie utworzony (lub zastąpione) w katalogu bieżącego środowiska hello.</span><span class="sxs-lookup"><span data-stu-id="b68ab-400">If a file name is provided without a directory, then hello file will be created (or overwritten) in hello current environment directory.</span></span>
3. <span data-ttu-id="b68ab-401">W przypadku wybrania istniejącego pliku, a następnie hello plik zostanie zastąpiony, nie jest dostępna opcja dołączania.</span><span class="sxs-lookup"><span data-stu-id="b68ab-401">If you select an existing file, then hello file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="b68ab-402">Następnie wybierz pozycję czy toolog wszystkie, krytyczne, lub żadne komunikaty o błędach.</span><span class="sxs-lookup"><span data-stu-id="b68ab-402">Then, choose whether toolog all, critical, or no error messages.</span></span> <span data-ttu-id="b68ab-403">Na koniec zdecyduj, jak często zostaną zaktualizowane hello na ekranie transferu wiadomości o postępie.</span><span class="sxs-lookup"><span data-stu-id="b68ab-403">Finally, decide how frequently hello on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="b68ab-404">Potwierdź ustawienia importowania i widok wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="b68ab-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="b68ab-405">Po określeniu informacji o źródle, informacji o docelowej i konfiguracji zaawansowanej, Przejrzyj podsumowanie migracji hello i, opcjonalnie, widok/kopiowania hello co polecenia migracji (kopiowanie polecenie hello jest przydatne tooautomate operacji importowania):</span><span class="sxs-lookup"><span data-stu-id="b68ab-405">After specifying source information, target information, and advanced configuration, review hello migration summary and, optionally, view/copy hello resulting migration command (copying hello command is useful tooautomate import operations):</span></span>
   
    ![Zrzut ekranu przedstawiający ekran podsumowania](./media/import-data/summary.png)
   
    ![Zrzut ekranu przedstawiający ekran podsumowania](./media/import-data/summarycommand.png)
2. <span data-ttu-id="b68ab-408">Po zakończeniu opcje źródłowego i docelowego kliknij **importu**.</span><span class="sxs-lookup"><span data-stu-id="b68ab-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="b68ab-409">czas, który upłynął Hello, liczba przekazanych i informacje o błędzie (Jeśli nie podasz nazwę pliku w konfiguracji zaawansowanej hello) zaktualizuje importu hello jest w toku.</span><span class="sxs-lookup"><span data-stu-id="b68ab-409">hello elapsed time, transferred count, and failure information (if you didn't provide a file name in hello Advanced configuration) will update as hello import is in process.</span></span> <span data-ttu-id="b68ab-410">Po wykonaniu tych czynności możesz wyeksportować wyniki hello (np. toodeal o niepowodzeniach import).</span><span class="sxs-lookup"><span data-stu-id="b68ab-410">Once complete, you can export hello results (e.g. toodeal with any import failures).</span></span>
   
    ![Zrzut ekranu z Azure rozwiązania Cosmos bazy danych JSON opcji eksportu](./media/import-data/viewresults.png)
3. <span data-ttu-id="b68ab-412">Może także uruchomić nowy import, albo utrzymywanie hello istniejących ustawień (np. ciąg połączenia wybór informacji, źródłowa i docelowa itp.) lub zresetowanie wszystkich wartości.</span><span class="sxs-lookup"><span data-stu-id="b68ab-412">You may also start a new import, either keeping hello existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Zrzut ekranu z Azure rozwiązania Cosmos bazy danych JSON opcji eksportu](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="b68ab-414">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b68ab-414">Next steps</span></span>

<span data-ttu-id="b68ab-415">W tym samouczku wykonaniu hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="b68ab-415">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b68ab-416">Zainstalowane narzędzie migracji danych hello</span><span class="sxs-lookup"><span data-stu-id="b68ab-416">Installed hello Data Migration tool</span></span>
> * <span data-ttu-id="b68ab-417">Importowane dane z różnych źródeł danych</span><span class="sxs-lookup"><span data-stu-id="b68ab-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="b68ab-418">Wyeksportowane z bazy danych Azure rozwiązania Cosmos tooJSON</span><span class="sxs-lookup"><span data-stu-id="b68ab-418">Exported from Azure Cosmos DB tooJSON</span></span>

<span data-ttu-id="b68ab-419">Można teraz kontynuować toohello następny samouczek i Dowiedz się, jak tooquery danych przy użyciu bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b68ab-419">You can now proceed toohello next tutorial and learn how tooquery data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="b68ab-420">Jak tooquery danych?</span><span class="sxs-lookup"><span data-stu-id="b68ab-420">How tooquery data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
