---
title: "aaaMove danych z usługi magazynowania proste Amazon przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o danych toomove z prostego Amazon usługi Storage (S3) przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="4d6f8-103">Przenoszenia danych z usługi magazynowania proste Amazon przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="4d6f8-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="4d6f8-104">W tym artykule opisano, jak toouse hello aktywności kopiowania w fabryce danych Azure toomove danych z usługi magazynowania proste Amazon (S3).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="4d6f8-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="4d6f8-106">Można skopiować danych z magazynu danych zbiornika tooany obsługiwane Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="4d6f8-107">Lista danych obsługiwane magazyny wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="4d6f8-108">Fabryka danych aktualnie obsługuje tylko przenoszenia danych z baz danych tooother Amazon S3, ale nie przenoszenia danych z innych danych przechowuje tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="4d6f8-109">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="4d6f8-109">Required permissions</span></span>
<span data-ttu-id="4d6f8-110">toocopy danych z usługi Amazon S3, upewnij się, że zostały przyznane hello następujących uprawnień:</span><span class="sxs-lookup"><span data-stu-id="4d6f8-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="4d6f8-111">`s3:GetObject`i `s3:GetObjectVersion` Amazon S3 obiektu operacji.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="4d6f8-112">`s3:ListBucket`operacjach Amazon S3 zasobnika.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="4d6f8-113">Jeśli używasz hello kreatora kopiowania fabryki danych `s3:ListAllMyBuckets` jest również wymagany.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="4d6f8-114">Aby uzyskać więcej informacji o hello pełną listę uprawnień Amazon S3, zobacz [określanie uprawnień w zasadach](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="4d6f8-115">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="4d6f8-115">Getting started</span></span>
<span data-ttu-id="4d6f8-116">Można utworzyć potoku o działanie kopiowania, który przenosi dane ze źródła Amazon S3 przy użyciu różnych narzędzi lub interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="4d6f8-117">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="4d6f8-118">Przewodnik Szybki, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="4d6f8-119">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4d6f8-120">Aby uzyskać instrukcje krok po kroku toocreate potoku z działaniem kopiowania, zobacz hello [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="4d6f8-121">Czy za pomocą narzędzia lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="4d6f8-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="4d6f8-122">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="4d6f8-123">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="4d6f8-124">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="4d6f8-125">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4d6f8-126">Korzystając z narzędzia lub interfejsów API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="4d6f8-127">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z magazynu danych Amazon S3, zobacz hello [przykład JSON: kopiowanie danych z tooAzure Amazon S3 Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="4d6f8-128">Aby uzyskać więcej informacji o obsługiwanych formatów plików i kompresji dla działania kopiowania, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="4d6f8-129">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAmazon S3.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4d6f8-130">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="4d6f8-130">Linked service properties</span></span>
<span data-ttu-id="4d6f8-131">Połączona usługa łączy fabryki danych tooa magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="4d6f8-132">Tworzenie połączonej usługi typu **AwsAccessKey** toolink danych Amazon S3 przechowywać tooyour fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="4d6f8-133">Witaj w poniższej tabeli udostępnia usługę opis dla określonego tooAmazon elementów JSON S3 (AwsAccessKey) połączony.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="4d6f8-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4d6f8-134">Property</span></span> | <span data-ttu-id="4d6f8-135">Opis</span><span class="sxs-lookup"><span data-stu-id="4d6f8-135">Description</span></span> | <span data-ttu-id="4d6f8-136">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="4d6f8-136">Allowed values</span></span> | <span data-ttu-id="4d6f8-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4d6f8-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4d6f8-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="4d6f8-138">accessKeyID</span></span> |<span data-ttu-id="4d6f8-139">Identyfikator klucza tajnego dostępu hello.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-139">ID of hello secret access key.</span></span> |<span data-ttu-id="4d6f8-140">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4d6f8-140">string</span></span> |<span data-ttu-id="4d6f8-141">Tak</span><span class="sxs-lookup"><span data-stu-id="4d6f8-141">Yes</span></span> |
| <span data-ttu-id="4d6f8-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="4d6f8-142">secretAccessKey</span></span> |<span data-ttu-id="4d6f8-143">klucz tajny dostępu Hello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-143">hello secret access key itself.</span></span> |<span data-ttu-id="4d6f8-144">Zaszyfrowanego ciągu tajny</span><span class="sxs-lookup"><span data-stu-id="4d6f8-144">Encrypted secret string</span></span> |<span data-ttu-id="4d6f8-145">Tak</span><span class="sxs-lookup"><span data-stu-id="4d6f8-145">Yes</span></span> |

<span data-ttu-id="4d6f8-146">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="4d6f8-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="4d6f8-147">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="4d6f8-147">Dataset properties</span></span>
<span data-ttu-id="4d6f8-148">toospecify toorepresent zestawu danych wejściowych danych w magazynie obiektów Blob platformy Azure, właściwość type hello zestawu DataSet hello zbyt**AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="4d6f8-149">Zestaw hello **linkedServiceName** właściwości zestawu danych hello toohello nazwę hello Amazon S3 połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="4d6f8-150">Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="4d6f8-151">Sekcje, takie jak struktury, dostępności i zasady są podobne dla wszystkich typów zestawu danych (takich jak bazy danych SQL, obiektów blob platformy Azure i tabeli platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="4d6f8-152">Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="4d6f8-153">Witaj **typeProperties** sekcja dla zestawu danych typu **AmazonS3** (w tym dataset hello Amazon S3) ma następujące właściwości hello:</span><span class="sxs-lookup"><span data-stu-id="4d6f8-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="4d6f8-154">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4d6f8-154">Property</span></span> | <span data-ttu-id="4d6f8-155">Opis</span><span class="sxs-lookup"><span data-stu-id="4d6f8-155">Description</span></span> | <span data-ttu-id="4d6f8-156">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="4d6f8-156">Allowed values</span></span> | <span data-ttu-id="4d6f8-157">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4d6f8-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4d6f8-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="4d6f8-158">bucketName</span></span> |<span data-ttu-id="4d6f8-159">Nazwa pakietu Hello S3.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-159">hello S3 bucket name.</span></span> |<span data-ttu-id="4d6f8-160">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4d6f8-160">String</span></span> |<span data-ttu-id="4d6f8-161">Tak</span><span class="sxs-lookup"><span data-stu-id="4d6f8-161">Yes</span></span> |
| <span data-ttu-id="4d6f8-162">key</span><span class="sxs-lookup"><span data-stu-id="4d6f8-162">key</span></span> |<span data-ttu-id="4d6f8-163">Klucz obiektu Hello S3.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-163">hello S3 object key.</span></span> |<span data-ttu-id="4d6f8-164">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4d6f8-164">String</span></span> |<span data-ttu-id="4d6f8-165">Nie</span><span class="sxs-lookup"><span data-stu-id="4d6f8-165">No</span></span> |
| <span data-ttu-id="4d6f8-166">Prefiks</span><span class="sxs-lookup"><span data-stu-id="4d6f8-166">prefix</span></span> |<span data-ttu-id="4d6f8-167">Prefiks hello S3 obiektu klucza.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="4d6f8-168">Wybrano obiektów, w której klucze uruchomienia z tym prefiksem.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="4d6f8-169">Ma zastosowanie tylko wtedy, gdy klucz jest pusty.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-169">Applies only when key is empty.</span></span> |<span data-ttu-id="4d6f8-170">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4d6f8-170">String</span></span> |<span data-ttu-id="4d6f8-171">Nie</span><span class="sxs-lookup"><span data-stu-id="4d6f8-171">No</span></span> |
| <span data-ttu-id="4d6f8-172">Wersja</span><span class="sxs-lookup"><span data-stu-id="4d6f8-172">version</span></span> |<span data-ttu-id="4d6f8-173">Wersja Hello hello S3 obiektu, jeśli włączono S3 przechowywania wersji.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="4d6f8-174">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4d6f8-174">String</span></span> |<span data-ttu-id="4d6f8-175">Nie</span><span class="sxs-lookup"><span data-stu-id="4d6f8-175">No</span></span> |
| <span data-ttu-id="4d6f8-176">Format</span><span class="sxs-lookup"><span data-stu-id="4d6f8-176">format</span></span> | <span data-ttu-id="4d6f8-177">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="4d6f8-178">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="4d6f8-179">Aby uzyskać więcej informacji, zobacz hello [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet format ](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="4d6f8-180">Jeśli chcesz, aby pliki toocopy-między opartych na plikach magazynów (kopia binarnego), Pomiń hello format sekcji w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="4d6f8-181">Nie</span><span class="sxs-lookup"><span data-stu-id="4d6f8-181">No</span></span> | |
| <span data-ttu-id="4d6f8-182">Kompresja</span><span class="sxs-lookup"><span data-stu-id="4d6f8-182">compression</span></span> | <span data-ttu-id="4d6f8-183">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="4d6f8-184">Witaj, obsługiwane typy: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="4d6f8-185">Witaj obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="4d6f8-186">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="4d6f8-187">Nie</span><span class="sxs-lookup"><span data-stu-id="4d6f8-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="4d6f8-188">**bucketName + klawisz** Określa lokalizację hello hello S3 obiektu, którym zasobnika jest hello nadrzędny kontener dla obiektów S3, a klucz hello pełną ścieżkę toohello S3 obiektu.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="4d6f8-189">Przykładowego zestawu danych z prefiksem</span><span class="sxs-lookup"><span data-stu-id="4d6f8-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="4d6f8-190">Przykładowego zestawu danych (z wersją)</span><span class="sxs-lookup"><span data-stu-id="4d6f8-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="4d6f8-191">Dynamiczne ścieżki S3</span><span class="sxs-lookup"><span data-stu-id="4d6f8-191">Dynamic paths for S3</span></span>
<span data-ttu-id="4d6f8-192">Witaj powyższego przykładu użyto stałej wartości dla hello **klucza** i **bucketName** właściwości w elemencie dataset hello Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="4d6f8-193">Program może obliczyć te właściwości dynamicznie w czasie wykonywania za pomocą zmiennych systemowych, takich jak SliceStart fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="4d6f8-194">Możesz zrobić hello takie same dla hello **prefiks** właściwości Amazon S3 zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="4d6f8-195">Aby uzyskać listę obsługiwanych funkcji i zmiennych, zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="4d6f8-196">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="4d6f8-196">Copy activity properties</span></span>
<span data-ttu-id="4d6f8-197">Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="4d6f8-198">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="4d6f8-199">Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="4d6f8-200">Dla działania kopiowania hello właściwości różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="4d6f8-201">Gdy źródła w przypadku działania kopiowania hello jest typu **FileSystemSource** (która obejmuje Amazon S3), hello następujące właściwości są dostępne w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="4d6f8-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="4d6f8-202">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4d6f8-202">Property</span></span> | <span data-ttu-id="4d6f8-203">Opis</span><span class="sxs-lookup"><span data-stu-id="4d6f8-203">Description</span></span> | <span data-ttu-id="4d6f8-204">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="4d6f8-204">Allowed values</span></span> | <span data-ttu-id="4d6f8-205">Wymagane</span><span class="sxs-lookup"><span data-stu-id="4d6f8-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4d6f8-206">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="4d6f8-206">recursive</span></span> |<span data-ttu-id="4d6f8-207">Określa, czy lista toorecursively S3 obiekty w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="4d6f8-208">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="4d6f8-208">true/false</span></span> |<span data-ttu-id="4d6f8-209">Nie</span><span class="sxs-lookup"><span data-stu-id="4d6f8-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="4d6f8-210">Przykład JSON: kopiowanie danych z tooAzure Amazon S3 magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="4d6f8-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="4d6f8-211">W tym przykładzie pokazano sposób toocopy danych z tooan Amazon S3 magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="4d6f8-212">Jednak dane mogą być kopiowane bezpośrednio za[żadnego wychwytywanie hello, które są obsługiwane](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania hello w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="4d6f8-213">przykład Witaj definicje JSON powitania po jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="4d6f8-214">Te definicje toocreate potoku toocopy danych z magazynu tooBlob Amazon S3, można użyć przy użyciu hello [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="4d6f8-215">Połączonej usługi typu [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="4d6f8-216">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="4d6f8-217">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="4d6f8-218">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="4d6f8-219">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="4d6f8-220">przykład Witaj kopiuje dane z tooan Amazon S3 obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="4d6f8-221">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="4d6f8-222">Usługi Amazon S3 połączone</span><span class="sxs-lookup"><span data-stu-id="4d6f8-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="4d6f8-223">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="4d6f8-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="4d6f8-224">Zestaw danych wejściowych Amazon S3</span><span class="sxs-lookup"><span data-stu-id="4d6f8-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="4d6f8-225">Ustawienie **"external": true** informuje usługi fabryka danych hello tego zestawu danych hello jest zewnętrznych toohello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="4d6f8-226">Wejściowy zestaw danych, który nie jest generowany przez działania w potoku hello ustawić tootrue tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="4d6f8-227">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4d6f8-227">Azure Blob output dataset</span></span>

<span data-ttu-id="4d6f8-228">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4d6f8-229">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4d6f8-230">Ścieżka folderu Hello używa hello rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="4d6f8-231">Działanie kopiowania w potoku ze źródłem Amazon S3 i ujście obiektów blob</span><span class="sxs-lookup"><span data-stu-id="4d6f8-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="4d6f8-232">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="4d6f8-233">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**FileSystemSource**, i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="4d6f8-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="4d6f8-234">toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4d6f8-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4d6f8-235">Next steps</span></span>
<span data-ttu-id="4d6f8-236">Zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="4d6f8-236">See hello following articles:</span></span>

* <span data-ttu-id="4d6f8-237">toolearn o kluczu czynniki tego wydajności wpływ przenoszenia danych (działanie kopiowania) w fabryce danych i różne sposoby toooptimize, zobacz hello [skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="4d6f8-238">Aby uzyskać instrukcje tworzenia potoku z działaniem kopiowania, zobacz hello [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4d6f8-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
