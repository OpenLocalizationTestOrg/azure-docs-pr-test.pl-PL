---
title: "aaaMove dane z usługi Amazon Redshift przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toomove dane z usługi Amazon Redshift przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="2f683-103">Przenoszenie danych z Redshift Amazon przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="2f683-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="2f683-104">W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="2f683-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from Amazon Redshift.</span></span> <span data-ttu-id="2f683-105">Artykuł Hello opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2f683-105">hello article builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="2f683-106">Można skopiować danych z magazynu danych zbiornika tooany obsługiwane Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="2f683-106">You can copy data from Amazon Redshift tooany supported sink data store.</span></span> <span data-ttu-id="2f683-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania hello, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2f683-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="2f683-108">Fabryka danych obecnie obsługuje przenoszenia danych z magazynów danych tooother Amazon Redshift, ale nie do przenoszenia danych z innych tooAmazon magazynów danych Redshift.</span><span class="sxs-lookup"><span data-stu-id="2f683-108">Data factory currently supports moving data from Amazon Redshift tooother data stores, but not for moving data from other data stores tooAmazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f683-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2f683-109">Prerequisites</span></span>
* <span data-ttu-id="2f683-110">Jeśli chcesz przenieść magazyn danych lokalnych tooan danych, zainstaluj [brama zarządzania danymi](data-factory-data-management-gateway.md) na maszynie lokalnej.</span><span class="sxs-lookup"><span data-stu-id="2f683-110">If you are moving data tooan on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="2f683-111">Następnie brama zarządzania danymi Grant (Użyj adresu IP maszyny hello) hello dostępu tooAmazon Redshift klastra.</span><span class="sxs-lookup"><span data-stu-id="2f683-111">Then, Grant Data Management Gateway (use IP address of hello machine) hello access tooAmazon Redshift cluster.</span></span> <span data-ttu-id="2f683-112">Zobacz [klastra toohello dostępu autoryzacji](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="2f683-112">See [Authorize access toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="2f683-113">Jeśli przenosisz magazynu danych Azure tooan danych, zobacz [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653) dla adresu IP obliczeniowe hello i zakresów SQL używane przez hello centrach danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2f683-113">If you are moving data tooan Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for hello Compute IP address and SQL ranges used by hello Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2f683-114">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="2f683-114">Getting started</span></span>
<span data-ttu-id="2f683-115">Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła Amazon Redshift przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="2f683-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="2f683-116">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="2f683-116">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="2f683-117">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="2f683-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="2f683-118">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="2f683-118">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2f683-119">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2f683-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2f683-120">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="2f683-120">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="2f683-121">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="2f683-121">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="2f683-122">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2f683-122">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="2f683-123">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="2f683-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2f683-124">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="2f683-124">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="2f683-125">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="2f683-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="2f683-126">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych Amazon Redshift, zobacz [przykład JSON: kopiowanie danych z tooAzure Amazon Redshift Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="2f683-126">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2f683-127">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAmazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="2f683-127">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="2f683-128">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="2f683-128">Linked service properties</span></span>
<span data-ttu-id="2f683-129">Witaj w poniższej tabeli przedstawiono opis dla określonych elementów JSON — tooAmazon Redshift połączone usługi.</span><span class="sxs-lookup"><span data-stu-id="2f683-129">hello following table provides description for JSON elements specific tooAmazon Redshift linked service.</span></span>

| <span data-ttu-id="2f683-130">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2f683-130">Property</span></span> | <span data-ttu-id="2f683-131">Opis</span><span class="sxs-lookup"><span data-stu-id="2f683-131">Description</span></span> | <span data-ttu-id="2f683-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2f683-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f683-133">type</span><span class="sxs-lookup"><span data-stu-id="2f683-133">type</span></span> |<span data-ttu-id="2f683-134">musi mieć ustawioną właściwość type Hello: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="2f683-134">hello type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="2f683-135">Tak</span><span class="sxs-lookup"><span data-stu-id="2f683-135">Yes</span></span> |
| <span data-ttu-id="2f683-136">serwer</span><span class="sxs-lookup"><span data-stu-id="2f683-136">server</span></span> |<span data-ttu-id="2f683-137">Adres IP lub hosta nazwę hello Amazon Redshift serwera.</span><span class="sxs-lookup"><span data-stu-id="2f683-137">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="2f683-138">Tak</span><span class="sxs-lookup"><span data-stu-id="2f683-138">Yes</span></span> |
| <span data-ttu-id="2f683-139">port</span><span class="sxs-lookup"><span data-stu-id="2f683-139">port</span></span> |<span data-ttu-id="2f683-140">Witaj liczbę hello port TCP, którego hello Amazon Redshift serwer używa toolisten dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="2f683-140">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="2f683-141">Nie, wartość domyślna: 5439</span><span class="sxs-lookup"><span data-stu-id="2f683-141">No, default value: 5439</span></span> |
| <span data-ttu-id="2f683-142">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="2f683-142">database</span></span> |<span data-ttu-id="2f683-143">Nazwa bazy danych usługi Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="2f683-143">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="2f683-144">Tak</span><span class="sxs-lookup"><span data-stu-id="2f683-144">Yes</span></span> |
| <span data-ttu-id="2f683-145">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="2f683-145">username</span></span> |<span data-ttu-id="2f683-146">Nazwa użytkownika, który ma toohello dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2f683-146">Name of user who has access toohello database.</span></span> |<span data-ttu-id="2f683-147">Tak</span><span class="sxs-lookup"><span data-stu-id="2f683-147">Yes</span></span> |
| <span data-ttu-id="2f683-148">hasło</span><span class="sxs-lookup"><span data-stu-id="2f683-148">password</span></span> |<span data-ttu-id="2f683-149">Hasło dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="2f683-149">Password for hello user account.</span></span> |<span data-ttu-id="2f683-150">Tak</span><span class="sxs-lookup"><span data-stu-id="2f683-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="2f683-151">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="2f683-151">Dataset properties</span></span>
<span data-ttu-id="2f683-152">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2f683-152">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2f683-153">Sekcje, takie jak struktury, dostępności i zasady są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="2f683-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2f683-154">Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="2f683-154">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="2f683-155">Zawiera informacje o lokalizacji hello hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="2f683-155">It provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2f683-156">Witaj typeProperties sekcja dla zestawu danych typu **RelationalTable** (w tym Amazon Redshift zestawu danych) ma następujące właściwości hello</span><span class="sxs-lookup"><span data-stu-id="2f683-156">hello typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has hello following properties</span></span>

| <span data-ttu-id="2f683-157">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2f683-157">Property</span></span> | <span data-ttu-id="2f683-158">Opis</span><span class="sxs-lookup"><span data-stu-id="2f683-158">Description</span></span> | <span data-ttu-id="2f683-159">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2f683-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f683-160">tableName</span><span class="sxs-lookup"><span data-stu-id="2f683-160">tableName</span></span> |<span data-ttu-id="2f683-161">Nazwa tabeli hello w bazie danych usługi Amazon Redshift hello, których połączonej usługi odwołuje się do.</span><span class="sxs-lookup"><span data-stu-id="2f683-161">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="2f683-162">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="2f683-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2f683-163">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="2f683-163">Copy activity properties</span></span>
<span data-ttu-id="2f683-164">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2f683-164">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2f683-165">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="2f683-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="2f683-166">Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania.</span><span class="sxs-lookup"><span data-stu-id="2f683-166">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="2f683-167">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="2f683-167">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="2f683-168">Gdy źródło działanie kopiowania jest typu **RelationalSource** (która obejmuje Amazon Redshift), hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="2f683-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="2f683-169">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2f683-169">Property</span></span> | <span data-ttu-id="2f683-170">Opis</span><span class="sxs-lookup"><span data-stu-id="2f683-170">Description</span></span> | <span data-ttu-id="2f683-171">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="2f683-171">Allowed values</span></span> | <span data-ttu-id="2f683-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2f683-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f683-173">query</span><span class="sxs-lookup"><span data-stu-id="2f683-173">query</span></span> |<span data-ttu-id="2f683-174">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="2f683-174">Use hello custom query tooread data.</span></span> |<span data-ttu-id="2f683-175">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="2f683-175">SQL query string.</span></span> <span data-ttu-id="2f683-176">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="2f683-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="2f683-177">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="2f683-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a><span data-ttu-id="2f683-178">Przykład JSON: kopiowanie danych z tooAzure Amazon Redshift obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="2f683-178">JSON example: Copy data from Amazon Redshift tooAzure Blob</span></span>
<span data-ttu-id="2f683-179">W tym przykładzie pokazano, jak dane toocopy z Redshift Amazon bazy danych tooan magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2f683-179">This sample shows how toocopy data from an Amazon Redshift database tooan Azure Blob Storage.</span></span> <span data-ttu-id="2f683-180">Jednak dane mogą być kopiowane **bezpośrednio** tooany wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="2f683-180">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="2f683-181">przykład Witaj ma hello następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="2f683-181">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="2f683-182">Połączonej usługi typu [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2f683-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="2f683-183">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2f683-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="2f683-184">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2f683-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="2f683-185">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2f683-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="2f683-186">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2f683-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="2f683-187">przykład Witaj kopiuje dane z wyniku kwerendy w obiekcie blob tooa Amazon Redshift, co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2f683-187">hello sample copies data from a query result in Amazon Redshift tooa blob every hour.</span></span> <span data-ttu-id="2f683-188">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="2f683-188">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="2f683-189">**Amazon Redshift połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="2f683-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="2f683-190">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="2f683-190">**Azure Storage linked service:**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="2f683-191">**Zestaw danych wejściowych Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="2f683-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="2f683-192">Ustawienie `"external": true` informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="2f683-192">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="2f683-193">Wejściowy zestaw danych, który nie jest generowany przez działania w potoku hello ustawić tootrue tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="2f683-193">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="2f683-194">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="2f683-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2f683-195">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="2f683-195">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2f683-196">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="2f683-196">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="2f683-197">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="2f683-197">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="2f683-198">**Działanie kopiowania w potoku ze źródłem Azure Redshift (RelationalSource) i ujście obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="2f683-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="2f683-199">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2f683-199">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="2f683-200">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**RelationalSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2f683-200">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="2f683-201">Zapytanie SQL Hello określone dla hello **zapytania** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="2f683-201">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="2f683-202">Mapowanie typu dla Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="2f683-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="2f683-203">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie:</span><span class="sxs-lookup"><span data-stu-id="2f683-203">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="2f683-204">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="2f683-204">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="2f683-205">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="2f683-205">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="2f683-206">Podczas przenoszenia danych tooAmazon Redshift, hello następującego mapowania są używane z typów too.NET typy Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="2f683-206">When moving data tooAmazon Redshift, hello following mappings are used from Amazon Redshift types too.NET types.</span></span>

| <span data-ttu-id="2f683-207">Typ Redshift Amazon</span><span class="sxs-lookup"><span data-stu-id="2f683-207">Amazon Redshift Type</span></span> | <span data-ttu-id="2f683-208">Typ na podstawie .NET</span><span class="sxs-lookup"><span data-stu-id="2f683-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="2f683-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="2f683-209">SMALLINT</span></span> |<span data-ttu-id="2f683-210">Int16</span><span class="sxs-lookup"><span data-stu-id="2f683-210">Int16</span></span> |
| <span data-ttu-id="2f683-211">LICZBA CAŁKOWITA</span><span class="sxs-lookup"><span data-stu-id="2f683-211">INTEGER</span></span> |<span data-ttu-id="2f683-212">Int32</span><span class="sxs-lookup"><span data-stu-id="2f683-212">Int32</span></span> |
| <span data-ttu-id="2f683-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="2f683-213">BIGINT</span></span> |<span data-ttu-id="2f683-214">Int64</span><span class="sxs-lookup"><span data-stu-id="2f683-214">Int64</span></span> |
| <span data-ttu-id="2f683-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="2f683-215">DECIMAL</span></span> |<span data-ttu-id="2f683-216">Decimal</span><span class="sxs-lookup"><span data-stu-id="2f683-216">Decimal</span></span> |
| <span data-ttu-id="2f683-217">RZECZYWISTE</span><span class="sxs-lookup"><span data-stu-id="2f683-217">REAL</span></span> |<span data-ttu-id="2f683-218">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="2f683-218">Single</span></span> |
| <span data-ttu-id="2f683-219">PODWÓJNEJ PRECYZJI</span><span class="sxs-lookup"><span data-stu-id="2f683-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="2f683-220">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="2f683-220">Double</span></span> |
| <span data-ttu-id="2f683-221">WARTOŚĆ LOGICZNA</span><span class="sxs-lookup"><span data-stu-id="2f683-221">BOOLEAN</span></span> |<span data-ttu-id="2f683-222">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2f683-222">String</span></span> |
| <span data-ttu-id="2f683-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="2f683-223">CHAR</span></span> |<span data-ttu-id="2f683-224">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2f683-224">String</span></span> |
| <span data-ttu-id="2f683-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="2f683-225">VARCHAR</span></span> |<span data-ttu-id="2f683-226">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2f683-226">String</span></span> |
| <span data-ttu-id="2f683-227">DATA</span><span class="sxs-lookup"><span data-stu-id="2f683-227">DATE</span></span> |<span data-ttu-id="2f683-228">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="2f683-228">DateTime</span></span> |
| <span data-ttu-id="2f683-229">ZNACZNIK CZASU</span><span class="sxs-lookup"><span data-stu-id="2f683-229">TIMESTAMP</span></span> |<span data-ttu-id="2f683-230">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="2f683-230">DateTime</span></span> |
| <span data-ttu-id="2f683-231">TEKST</span><span class="sxs-lookup"><span data-stu-id="2f683-231">TEXT</span></span> |<span data-ttu-id="2f683-232">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2f683-232">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="2f683-233">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="2f683-233">Map source toosink columns</span></span>
<span data-ttu-id="2f683-234">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2f683-234">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2f683-235">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="2f683-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="2f683-236">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="2f683-236">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="2f683-237">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="2f683-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2f683-238">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="2f683-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2f683-239">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="2f683-239">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2f683-240">Zobacz [Repeatable odczytywać relacyjne źródła](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="2f683-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2f683-241">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="2f683-241">Performance and Tuning</span></span>
<span data-ttu-id="2f683-242">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="2f683-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f683-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2f683-243">Next Steps</span></span>
<span data-ttu-id="2f683-244">Zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="2f683-244">See hello following articles:</span></span>

* <span data-ttu-id="2f683-245">[Samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku do tworzenia potoku z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2f683-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
