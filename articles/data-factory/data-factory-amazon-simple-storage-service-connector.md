---
title: "Przenoszenie danych z usługi magazynowania proste Amazon przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z usługi magazynowania proste Amazon (S3) przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: 3e21f7dfccc3b235071344a28c7d94f65e6bf9ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="98068-103">Przenoszenia danych z usługi magazynowania proste Amazon przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="98068-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="98068-104">W tym artykule opisano sposób użycia działanie kopiowania w fabryce danych Azure, aby przenieść dane z usługi Amazon proste usługi Storage (S3).</span><span class="sxs-lookup"><span data-stu-id="98068-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="98068-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="98068-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="98068-106">Możesz skopiować dane z usługi Amazon S3 żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="98068-106">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="98068-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="98068-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="98068-108">Fabryka danych aktualnie obsługuje tylko przenoszenia danych z usługi Amazon S3 do innych magazynów danych, ale nie przenoszenia danych z innych danych są przechowywane na Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="98068-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="98068-109">Wymagane uprawnienia</span><span class="sxs-lookup"><span data-stu-id="98068-109">Required permissions</span></span>
<span data-ttu-id="98068-110">Aby skopiować dane z usługi Amazon S3, upewnij się, że przyznano następujące uprawnienia:</span><span class="sxs-lookup"><span data-stu-id="98068-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="98068-111">`s3:GetObject`i `s3:GetObjectVersion` Amazon S3 obiektu operacji.</span><span class="sxs-lookup"><span data-stu-id="98068-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="98068-112">`s3:ListBucket`operacjach Amazon S3 zasobnika.</span><span class="sxs-lookup"><span data-stu-id="98068-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="98068-113">Jeśli używasz kreatora kopiowania fabryki danych `s3:ListAllMyBuckets` jest również wymagany.</span><span class="sxs-lookup"><span data-stu-id="98068-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="98068-114">Aby uzyskać więcej informacji o pełną listę uprawnień Amazon S3, zobacz [określanie uprawnień w zasadach](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="98068-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="98068-115">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="98068-115">Getting started</span></span>
<span data-ttu-id="98068-116">Można utworzyć potoku o działanie kopiowania, który przenosi dane ze źródła Amazon S3 przy użyciu różnych narzędzi lub interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="98068-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="98068-117">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="98068-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="98068-118">Przewodnik Szybki, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="98068-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="98068-119">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="98068-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="98068-120">Aby uzyskać instrukcje utworzyć potok z działania kopiowania, zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="98068-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="98068-121">Czy za pomocą narzędzia lub interfejsów API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="98068-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="98068-122">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="98068-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="98068-123">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="98068-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="98068-124">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="98068-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="98068-125">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="98068-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="98068-126">Korzystając z narzędzia lub interfejsów API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="98068-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="98068-127">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych z magazynu danych Amazon S3, zobacz [przykład JSON: kopiowanie danych z usługi Amazon S3 do obiektów Blob platformy Azure](#json-example-copy-data-from-amazon-s3-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="98068-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="98068-128">Aby uzyskać więcej informacji o obsługiwanych formatów plików i kompresji dla działania kopiowania, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="98068-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="98068-129">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="98068-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="98068-130">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="98068-130">Linked service properties</span></span>
<span data-ttu-id="98068-131">Połączona usługa łączy magazynu danych z fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="98068-131">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="98068-132">Tworzenie połączonej usługi typu **AwsAccessKey** połączyć usługi Amazon S3 data store z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="98068-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="98068-133">Poniższa tabela zawiera opis określone elementy JSON do Amazon S3 (AwsAccessKey) połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="98068-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="98068-134">Właściwość</span><span class="sxs-lookup"><span data-stu-id="98068-134">Property</span></span> | <span data-ttu-id="98068-135">Opis</span><span class="sxs-lookup"><span data-stu-id="98068-135">Description</span></span> | <span data-ttu-id="98068-136">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="98068-136">Allowed values</span></span> | <span data-ttu-id="98068-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="98068-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98068-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="98068-138">accessKeyID</span></span> |<span data-ttu-id="98068-139">Identyfikator klucza tajnego dostępu.</span><span class="sxs-lookup"><span data-stu-id="98068-139">ID of the secret access key.</span></span> |<span data-ttu-id="98068-140">Ciąg</span><span class="sxs-lookup"><span data-stu-id="98068-140">string</span></span> |<span data-ttu-id="98068-141">Tak</span><span class="sxs-lookup"><span data-stu-id="98068-141">Yes</span></span> |
| <span data-ttu-id="98068-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="98068-142">secretAccessKey</span></span> |<span data-ttu-id="98068-143">Samego klucza tajnego dostępu.</span><span class="sxs-lookup"><span data-stu-id="98068-143">The secret access key itself.</span></span> |<span data-ttu-id="98068-144">Zaszyfrowanego ciągu tajny</span><span class="sxs-lookup"><span data-stu-id="98068-144">Encrypted secret string</span></span> |<span data-ttu-id="98068-145">Tak</span><span class="sxs-lookup"><span data-stu-id="98068-145">Yes</span></span> |

<span data-ttu-id="98068-146">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="98068-146">Here is an example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="98068-147">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="98068-147">Dataset properties</span></span>
<span data-ttu-id="98068-148">Aby określić zestaw danych do reprezentowania danych wejściowych w magazynie obiektów Blob platformy Azure, ustaw właściwość Typ zestawu danych do **AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="98068-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="98068-149">Ustaw **linkedServiceName** właściwości zestawu danych do nazwy Amazon S3 połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="98068-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="98068-150">Aby uzyskać pełną listę właściwości dostępnych do definiowania zestawów danych i sekcje, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="98068-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="98068-151">Sekcje, takie jak struktury, dostępności i zasady są podobne dla wszystkich typów zestawu danych (takich jak bazy danych SQL, obiektów blob platformy Azure i tabeli platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="98068-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="98068-152">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="98068-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="98068-153">**TypeProperties** sekcja dla zestawu danych typu **AmazonS3** (w tym zestawie danych Amazon S3) ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="98068-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="98068-154">Właściwość</span><span class="sxs-lookup"><span data-stu-id="98068-154">Property</span></span> | <span data-ttu-id="98068-155">Opis</span><span class="sxs-lookup"><span data-stu-id="98068-155">Description</span></span> | <span data-ttu-id="98068-156">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="98068-156">Allowed values</span></span> | <span data-ttu-id="98068-157">Wymagane</span><span class="sxs-lookup"><span data-stu-id="98068-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98068-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="98068-158">bucketName</span></span> |<span data-ttu-id="98068-159">Nazwa pakietu S3.</span><span class="sxs-lookup"><span data-stu-id="98068-159">The S3 bucket name.</span></span> |<span data-ttu-id="98068-160">Ciąg</span><span class="sxs-lookup"><span data-stu-id="98068-160">String</span></span> |<span data-ttu-id="98068-161">Tak</span><span class="sxs-lookup"><span data-stu-id="98068-161">Yes</span></span> |
| <span data-ttu-id="98068-162">key</span><span class="sxs-lookup"><span data-stu-id="98068-162">key</span></span> |<span data-ttu-id="98068-163">Klucz obiektu S3.</span><span class="sxs-lookup"><span data-stu-id="98068-163">The S3 object key.</span></span> |<span data-ttu-id="98068-164">Ciąg</span><span class="sxs-lookup"><span data-stu-id="98068-164">String</span></span> |<span data-ttu-id="98068-165">Nie</span><span class="sxs-lookup"><span data-stu-id="98068-165">No</span></span> |
| <span data-ttu-id="98068-166">Prefiks</span><span class="sxs-lookup"><span data-stu-id="98068-166">prefix</span></span> |<span data-ttu-id="98068-167">Prefiks klucza obiektu S3.</span><span class="sxs-lookup"><span data-stu-id="98068-167">Prefix for the S3 object key.</span></span> <span data-ttu-id="98068-168">Wybrano obiektów, w której klucze uruchomienia z tym prefiksem.</span><span class="sxs-lookup"><span data-stu-id="98068-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="98068-169">Ma zastosowanie tylko wtedy, gdy klucz jest pusty.</span><span class="sxs-lookup"><span data-stu-id="98068-169">Applies only when key is empty.</span></span> |<span data-ttu-id="98068-170">Ciąg</span><span class="sxs-lookup"><span data-stu-id="98068-170">String</span></span> |<span data-ttu-id="98068-171">Nie</span><span class="sxs-lookup"><span data-stu-id="98068-171">No</span></span> |
| <span data-ttu-id="98068-172">Wersja</span><span class="sxs-lookup"><span data-stu-id="98068-172">version</span></span> |<span data-ttu-id="98068-173">Wersja obiektu S3, jeśli włączono S3 przechowywania wersji.</span><span class="sxs-lookup"><span data-stu-id="98068-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="98068-174">Ciąg</span><span class="sxs-lookup"><span data-stu-id="98068-174">String</span></span> |<span data-ttu-id="98068-175">Nie</span><span class="sxs-lookup"><span data-stu-id="98068-175">No</span></span> |
| <span data-ttu-id="98068-176">Format</span><span class="sxs-lookup"><span data-stu-id="98068-176">format</span></span> | <span data-ttu-id="98068-177">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="98068-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="98068-178">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="98068-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="98068-179">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu JSON](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="98068-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="98068-180">Jeśli chcesz skopiować pliki jako — jest między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="98068-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="98068-181">Nie</span><span class="sxs-lookup"><span data-stu-id="98068-181">No</span></span> | |
| <span data-ttu-id="98068-182">Kompresja</span><span class="sxs-lookup"><span data-stu-id="98068-182">compression</span></span> | <span data-ttu-id="98068-183">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="98068-183">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="98068-184">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="98068-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="98068-185">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="98068-185">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="98068-186">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="98068-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="98068-187">Nie</span><span class="sxs-lookup"><span data-stu-id="98068-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="98068-188">**bucketName + klawisz** Określa lokalizację obiektu S3, gdzie zasobnika jest nadrzędny kontener dla obiektów S3, a klucz jest pełną ścieżką do obiektu S3.</span><span class="sxs-lookup"><span data-stu-id="98068-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="98068-189">Przykładowego zestawu danych z prefiksem</span><span class="sxs-lookup"><span data-stu-id="98068-189">Sample dataset with prefix</span></span>

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
### <a name="sample-dataset-with-version"></a><span data-ttu-id="98068-190">Przykładowego zestawu danych (z wersją)</span><span class="sxs-lookup"><span data-stu-id="98068-190">Sample dataset (with version)</span></span>

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

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="98068-191">Dynamiczne ścieżki S3</span><span class="sxs-lookup"><span data-stu-id="98068-191">Dynamic paths for S3</span></span>
<span data-ttu-id="98068-192">Wartości stałe dla korzysta z powyższego przykładu **klucza** i **bucketName** właściwości w elemencie dataset Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="98068-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="98068-193">Program może obliczyć te właściwości dynamicznie w czasie wykonywania za pomocą zmiennych systemowych, takich jak SliceStart fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="98068-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="98068-194">Wykonaj te same **prefiks** właściwości Amazon S3 zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="98068-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="98068-195">Aby uzyskać listę obsługiwanych funkcji i zmiennych, zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="98068-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="98068-196">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="98068-196">Copy activity properties</span></span>
<span data-ttu-id="98068-197">Pełną listę sekcje i właściwości dostępnych dla definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="98068-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="98068-198">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="98068-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="98068-199">Właściwości dostępne w **typeProperties** sekcji działania zależne od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="98068-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="98068-200">Dla działania kopiowania właściwości się różnić w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="98068-200">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="98068-201">Gdy źródła w przypadku działania kopiowania jest typu **FileSystemSource** (która obejmuje Amazon S3), jest dostępna w następujących właściwości **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="98068-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="98068-202">Właściwość</span><span class="sxs-lookup"><span data-stu-id="98068-202">Property</span></span> | <span data-ttu-id="98068-203">Opis</span><span class="sxs-lookup"><span data-stu-id="98068-203">Description</span></span> | <span data-ttu-id="98068-204">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="98068-204">Allowed values</span></span> | <span data-ttu-id="98068-205">Wymagane</span><span class="sxs-lookup"><span data-stu-id="98068-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="98068-206">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="98068-206">recursive</span></span> |<span data-ttu-id="98068-207">Określa, czy do rekursywnie lista S3 obiektów w katalogu.</span><span class="sxs-lookup"><span data-stu-id="98068-207">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="98068-208">wartość true, false</span><span class="sxs-lookup"><span data-stu-id="98068-208">true/false</span></span> |<span data-ttu-id="98068-209">Nie</span><span class="sxs-lookup"><span data-stu-id="98068-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="98068-210">Przykład JSON: kopiowanie danych z usługi Amazon S3 do magazynu obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="98068-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="98068-211">W tym przykładzie pokazano, jak skopiować dane z usługi Amazon S3 do magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="98068-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="98068-212">Jednak możesz skopiować dane bezpośrednio do [żadnego wychwytywanie, które są obsługiwane](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="98068-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="98068-213">Przykład zawiera definicje JSON dla następujących jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="98068-213">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="98068-214">Te definicje umożliwia tworzenie potoku, aby skopiować dane z usługi Amazon S3 do magazynu obiektów Blob za pomocą [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), lub [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="98068-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="98068-215">Połączonej usługi typu [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98068-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="98068-216">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="98068-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="98068-217">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98068-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="98068-218">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="98068-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="98068-219">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [FileSystemSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="98068-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="98068-220">Przykład kopiuje dane z usługi Amazon S3 obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="98068-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="98068-221">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="98068-221">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="98068-222">Usługi Amazon S3 połączone</span><span class="sxs-lookup"><span data-stu-id="98068-222">Amazon S3 linked service</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="98068-223">Połączona usługa Azure Storage</span><span class="sxs-lookup"><span data-stu-id="98068-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="98068-224">Zestaw danych wejściowych Amazon S3</span><span class="sxs-lookup"><span data-stu-id="98068-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="98068-225">Ustawienie **"external": true** informuje usługi fabryka danych z zestawu danych może być zewnętrzne fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="98068-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="98068-226">Ustaw tę właściwość na wartość true w wejściowy zestaw danych, który nie jest generowany przez działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="98068-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="98068-227">Wyjściowy zestaw danych obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="98068-227">Azure Blob output dataset</span></span>

<span data-ttu-id="98068-228">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="98068-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="98068-229">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="98068-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="98068-230">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="98068-230">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="98068-231">Działanie kopiowania w potoku ze źródłem Amazon S3 i ujście obiektów blob</span><span class="sxs-lookup"><span data-stu-id="98068-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="98068-232">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="98068-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="98068-233">W definicji JSON potoku **źródła** ustawiono typ **FileSystemSource**, i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="98068-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="98068-234">Aby mapować kolumn z zestawu źródła danych do kolumn z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="98068-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="98068-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98068-235">Next steps</span></span>
<span data-ttu-id="98068-236">Zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="98068-236">See the following articles:</span></span>

* <span data-ttu-id="98068-237">Informacje na temat kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w fabryce danych i zoptymalizować ją na różne sposoby, zobacz [skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="98068-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="98068-238">Aby uzyskać instrukcje tworzenia potoku z działaniem kopiowania, zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="98068-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
