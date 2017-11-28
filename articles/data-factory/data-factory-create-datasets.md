---
title: zestawy danych aaaCreate w fabryce danych Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak zestawy danych toocreate w fabryce danych Azure, wraz z przykładami, które używają właściwości, takie jak przesunięcie i anchorDateTime."
keywords: "Tworzenie zestawu danych, przykładowe zestawu danych, przesunięcie przykład"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="0d8c3-104">Zestawy danych w fabryce danych Azure</span><span class="sxs-lookup"><span data-stu-id="0d8c3-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="0d8c3-105">W tym artykule opisano, jakie zestawy danych są, jak są definiowane w formacie JSON i w jaki sposób są one używane w fabryce danych Azure potoków.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="0d8c3-106">Dostarcza szczegółowe informacje na temat każdej sekcji (na przykład struktury, dostępności i zasad) w definicji JSON hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-106">It provides details about each section (for example, structure, availability, and policy) in hello dataset JSON definition.</span></span> <span data-ttu-id="0d8c3-107">Witaj podano także przykłady dotyczące używania hello **przesunięcie**, **anchorDateTime**, i **styl** właściwości w definicji zestawu danych JSON.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-107">hello article also provides examples for using hello **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="0d8c3-108">Jeśli nowy tooData fabryki, zobacz [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) omówienie.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-108">If you are new tooData Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="0d8c3-109">Jeśli nie ma praktyczne doświadczenie w tworzeniu fabryki danych, można uzyskać lepsze zrozumienie za odczytywanie hello [samouczek przekształcania danych](data-factory-build-your-first-pipeline.md) i hello [samouczek przepływu danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading hello [data transformation tutorial](data-factory-build-your-first-pipeline.md) and hello [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="0d8c3-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-110">Overview</span></span>
<span data-ttu-id="0d8c3-111">Fabryka danych może obejmować jeden lub wiele potoków.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="0d8c3-112">A **potoku** to logiczne grupowanie **działania** który razem wykonania zadania.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="0d8c3-113">Hello działań w potoku zdefiniuj akcje tooperform na podstawie danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-113">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="0d8c3-114">Na przykład można użyć danych toocopy działania kopiowania z lokalnego programu SQL Server tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-114">For example, you might use a copy activity toocopy data from an on-premises SQL Server tooAzure Blob storage.</span></span> <span data-ttu-id="0d8c3-115">Następnie należy użyć działania Hive, które uruchamia skrypt Hive w usłudze Azure HDInsight klastra tooprocess danych z danych wyjściowych tooproduce magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess data from Blob storage tooproduce output data.</span></span> <span data-ttu-id="0d8c3-116">Ponadto można użyć drugiego kopiowania działania toocopy hello danych wyjściowych danych tooAzure SQL Data Warehouse, na które raportowania są wbudowane rozwiązania analizy biznesowej (BI).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-116">Finally, you might use a second copy activity toocopy hello output data tooAzure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="0d8c3-117">Aby uzyskać więcej informacji na temat potoków i działania, zobacz [potoki i działań w fabryce danych Azure](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="0d8c3-118">Działanie może zająć zero lub więcej danych wejściowych **zestawów danych**i utworzyć co najmniej jeden wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="0d8c3-119">Zestaw danych wejściowych reprezentuje dane wejściowe hello działania w potoku hello, a wyjściowy zestaw danych reprezentuje hello wyjściowy dla działania hello.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-119">An input dataset represents hello input for an activity in hello pipeline, and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="0d8c3-120">Zestawy danych identyfikują dane w różnych magazynach danych, takich jak tabele, pliki, foldery i dokumenty.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="0d8c3-121">Na przykład zestaw danych obiektów Blob platformy Azure określa hello kontenera obiektów blob i folder w magazynie obiektów Blob, z których hello potoku odczytywane dane hello.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-121">For example, an Azure Blob dataset specifies hello blob container and folder in Blob storage from which hello pipeline should read hello data.</span></span> 

<span data-ttu-id="0d8c3-122">Przed utworzeniem zestawu danych, należy utworzyć **połączona usługa** toolink toohello fabryki danych magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-122">Before you create a dataset, create a **linked service** toolink your data store toohello data factory.</span></span> <span data-ttu-id="0d8c3-123">Połączone usługi są podobne do parametrów połączenia, które definiują informacje o połączeniu hello wymagane dla fabryki danych tooconnect tooexternal zasobów.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-123">Linked services are much like connection strings, which define hello connection information needed for Data Factory tooconnect tooexternal resources.</span></span> <span data-ttu-id="0d8c3-124">Zestawy danych identyfikowanie danych w ramach hello połączonych magazynów danych, takich jak tabele SQL, pliki, foldery i dokumenty.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-124">Datasets identify data within hello linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="0d8c3-125">Na przykład usługi Azure Storage połączone usługi łączy fabryki danych toohello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-125">For example, an Azure Storage linked service links a storage account toohello data factory.</span></span> <span data-ttu-id="0d8c3-126">Zestaw danych obiektów Blob platformy Azure reprezentuje hello kontenera obiektów blob i hello folderu, który zawiera toobe wejściowych obiekty BLOB hello przetworzone.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-126">An Azure Blob dataset represents hello blob container and hello folder that contains hello input blobs toobe processed.</span></span> 

<span data-ttu-id="0d8c3-127">Oto przykładowy scenariusz.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-127">Here is a sample scenario.</span></span> <span data-ttu-id="0d8c3-128">toocopy danych z obiektu Blob magazynu tooa SQL database, Utwórz dwie połączonej usługi: Magazyn Azure i bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-128">toocopy data from Blob storage tooa SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="0d8c3-129">Następnie utwórz dwa zestawy danych: zestaw danych obiektów Blob platformy Azure, (do którego odwołuje się toohello połączoną usługą magazynu Azure), a tabeli SQL Azure zestawu danych (odwołuje się toohello bazy danych SQL Azure połączone usługi).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-129">Then, create two datasets: Azure Blob dataset (which refers toohello Azure Storage linked service) and Azure SQL Table dataset (which refers toohello Azure SQL Database linked service).</span></span> <span data-ttu-id="0d8c3-130">Witaj usługi Azure Storage i połączone usługi zawiera parametry połączeń, które fabryka danych używa odpowiednio tooyour tooconnect środowiska uruchomieniowego usługi Azure Storage i Azure SQL Database, baza danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-130">hello Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime tooconnect tooyour Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="0d8c3-131">zestaw danych obiektów Blob platformy Azure Hello określa hello kontenera obiektów blob i folderu obiektów blob, który zawiera hello wejściowych obiekty BLOB w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-131">hello Azure Blob dataset specifies hello blob container and blob folder that contains hello input blobs in your Blob storage.</span></span> <span data-ttu-id="0d8c3-132">zestaw danych z tabeli SQL Azure Hello Określa, że hello tabeli SQL w danych hello toowhich bazy danych SQL jest toobe skopiowane.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-132">hello Azure SQL Table dataset specifies hello SQL table in your SQL database toowhich hello data is toobe copied.</span></span>

<span data-ttu-id="0d8c3-133">Witaj Poniższy diagram przedstawia relacje hello potoku, działania, zestawu danych i połączonej usługi fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-133">hello following diagram shows hello relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relacja między potoku, działania, zestaw danych, połączone usługi](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="0d8c3-135">JSON dla zestawu danych</span><span class="sxs-lookup"><span data-stu-id="0d8c3-135">Dataset JSON</span></span>
<span data-ttu-id="0d8c3-136">Zestaw danych z fabryki danych jest zdefiniowany w formacie JSON w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="0d8c3-137">Witaj w poniższej tabeli opisano właściwości w hello powyżej JSON:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-137">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="0d8c3-138">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0d8c3-138">Property</span></span> | <span data-ttu-id="0d8c3-139">Opis</span><span class="sxs-lookup"><span data-stu-id="0d8c3-139">Description</span></span> | <span data-ttu-id="0d8c3-140">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0d8c3-140">Required</span></span> | <span data-ttu-id="0d8c3-141">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0d8c3-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d8c3-142">name</span><span class="sxs-lookup"><span data-stu-id="0d8c3-142">name</span></span> |<span data-ttu-id="0d8c3-143">Nazwa zestawu danych hello.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-143">Name of hello dataset.</span></span> <span data-ttu-id="0d8c3-144">Zobacz [fabryki danych Azure - reguły nazewnictwa](data-factory-naming-rules.md) dla reguły nazewnictwa.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="0d8c3-145">Tak</span><span class="sxs-lookup"><span data-stu-id="0d8c3-145">Yes</span></span> |<span data-ttu-id="0d8c3-146">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-146">NA</span></span> |
| <span data-ttu-id="0d8c3-147">type</span><span class="sxs-lookup"><span data-stu-id="0d8c3-147">type</span></span> |<span data-ttu-id="0d8c3-148">Typ hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-148">Type of hello dataset.</span></span> <span data-ttu-id="0d8c3-149">Określ jeden z typów hello obsługiwane przez fabrykę danych (na przykład: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-149">Specify one of hello types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="0d8c3-150">Aby uzyskać więcej informacji, zobacz [typ zestawu](#Type).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="0d8c3-151">Tak</span><span class="sxs-lookup"><span data-stu-id="0d8c3-151">Yes</span></span> |<span data-ttu-id="0d8c3-152">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-152">NA</span></span> |
| <span data-ttu-id="0d8c3-153">Struktura</span><span class="sxs-lookup"><span data-stu-id="0d8c3-153">structure</span></span> |<span data-ttu-id="0d8c3-154">Schemat hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-154">Schema of hello dataset.</span></span><br/><br/><span data-ttu-id="0d8c3-155">Aby uzyskać więcej informacji, zobacz [struktury zestawu danych](#Structure).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="0d8c3-156">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-156">No</span></span> |<span data-ttu-id="0d8c3-157">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-157">NA</span></span> |
| <span data-ttu-id="0d8c3-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="0d8c3-158">typeProperties</span></span> | <span data-ttu-id="0d8c3-159">właściwości typu Hello są różne dla każdego typu (na przykład: obiektów Blob platformy Azure, tabeli Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-159">hello type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="0d8c3-160">Aby uzyskać szczegółowe informacje na ich właściwości i typów hello obsługiwane, zobacz [typ zestawu](#Type).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-160">For details on hello supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="0d8c3-161">Tak</span><span class="sxs-lookup"><span data-stu-id="0d8c3-161">Yes</span></span> |<span data-ttu-id="0d8c3-162">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-162">NA</span></span> |
| <span data-ttu-id="0d8c3-163">external</span><span class="sxs-lookup"><span data-stu-id="0d8c3-163">external</span></span> | <span data-ttu-id="0d8c3-164">Wartość logiczna Flaga toospecify, czy zestaw danych jawnie jest generowany przez potok fabryki danych lub nie.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-164">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="0d8c3-165">Jeśli hello wejściowy zestaw danych działania nie jest generowany przez potok bieżącego hello, należy ustawić tej flagi tootrue.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-165">If hello input dataset for an activity is not produced by hello current pipeline, set this flag tootrue.</span></span> <span data-ttu-id="0d8c3-166">Ustaw tootrue tej flagi dla hello wejściowego zestawu danych hello pierwsze działanie w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-166">Set this flag tootrue for hello input dataset of hello first activity in hello pipeline.</span></span>  |<span data-ttu-id="0d8c3-167">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-167">No</span></span> |<span data-ttu-id="0d8c3-168">wartość false</span><span class="sxs-lookup"><span data-stu-id="0d8c3-168">false</span></span> |
| <span data-ttu-id="0d8c3-169">availability</span><span class="sxs-lookup"><span data-stu-id="0d8c3-169">availability</span></span> | <span data-ttu-id="0d8c3-170">Definiuje hello okno przetwarzania (na przykład co godzinę lub codziennie) lub hello fragmentowania modelu hello zestawu danych produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-170">Defines hello processing window (for example, hourly or daily) or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="0d8c3-171">Każda jednostka danych używane i produkowane przez uruchomienia działania nosi nazwę wycinka danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="0d8c3-172">Jeśli zestaw toodaily (częstotliwość - Day, interwał - 1) jest dostępność hello wyjściowy zestaw danych, wycinek jest tworzony codziennie.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-172">If hello availability of an output dataset is set toodaily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="0d8c3-173">Aby uzyskać więcej informacji, zobacz [dostępności zestawu danych](#Availability).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="0d8c3-174">Szczegółowe informacje na temat zestawu danych hello fragmentowania modelu, zobacz hello [planowania i wykonywania](data-factory-scheduling-and-execution.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-174">For details on hello dataset slicing model, see hello [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="0d8c3-175">Tak</span><span class="sxs-lookup"><span data-stu-id="0d8c3-175">Yes</span></span> |<span data-ttu-id="0d8c3-176">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-176">NA</span></span> |
| <span data-ttu-id="0d8c3-177">policy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-177">policy</span></span> |<span data-ttu-id="0d8c3-178">Definiuje kryteria hello lub hello warunek, który należy spełnić hello wycinków zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-178">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="0d8c3-179">Aby uzyskać więcej informacji, zobacz hello [zestawie danych zasad](#Policy) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-179">For details, see hello [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="0d8c3-180">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-180">No</span></span> |<span data-ttu-id="0d8c3-181">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="0d8c3-182">Przykład zestawu danych</span><span class="sxs-lookup"><span data-stu-id="0d8c3-182">Dataset example</span></span>
<span data-ttu-id="0d8c3-183">W hello poniższy przykład, zestaw danych hello reprezentuje tabela o nazwie **MyTable** w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-183">In hello following example, hello dataset represents a table named **MyTable** in a SQL database.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="0d8c3-184">Należy zwrócić uwagę hello następujące punkty:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-184">Note hello following points:</span></span>

* <span data-ttu-id="0d8c3-185">**Typ** ustawiono tooAzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-185">**type** is set tooAzureSqlTable.</span></span>
* <span data-ttu-id="0d8c3-186">**tableName** właściwość type (typ określonych tooAzureSqlTable) ma wartość tooMyTable.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-186">**tableName** type property (specific tooAzureSqlTable type) is set tooMyTable.</span></span>
* <span data-ttu-id="0d8c3-187">**linkedServiceName** odwołuje się tooa połączone usługi typu AzureSqlDatabase, zdefiniowanego w hello dalej fragment JSON.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-187">**linkedServiceName** refers tooa linked service of type AzureSqlDatabase, which is defined in hello next JSON snippet.</span></span> 
* <span data-ttu-id="0d8c3-188">**częstotliwość dostępności** ustawiono tooDay, i **interwał** ustawiono too1.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-188">**availability frequency** is set tooDay, and **interval** is set too1.</span></span> <span data-ttu-id="0d8c3-189">Oznacza to, że hello wycinek zestawu danych jest tworzony codziennie.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-189">This means that hello dataset slice is produced daily.</span></span>  

<span data-ttu-id="0d8c3-190">**AzureSqlLinkedService** jest zdefiniowane w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-190">**AzureSqlLinkedService** is defined as follows:</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="0d8c3-191">W hello poprzedzających fragment kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-191">In hello preceding JSON snippet:</span></span>

* <span data-ttu-id="0d8c3-192">**Typ** ustawiono tooAzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-192">**type** is set tooAzureSqlDatabase.</span></span>
* <span data-ttu-id="0d8c3-193">**connectionString** właściwość type określa informacje tooconnect tooa SQL w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-193">**connectionString** type property specifies information tooconnect tooa SQL database.</span></span>  

<span data-ttu-id="0d8c3-194">Jak widać, hello połączonej usługi definiuje sposób tooconnect tooa SQL w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-194">As you can see, hello linked service defines how tooconnect tooa SQL database.</span></span> <span data-ttu-id="0d8c3-195">Hello dataset definiuje, jakie tabela jest używane jako dane wejściowe i wyjściowe dla hello działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-195">hello dataset defines what table is used as an input and output for hello activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="0d8c3-196">Jeśli zestaw danych jest tworzonym przez potok hello, powinien być oznaczony jako **zewnętrznych**.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-196">Unless a dataset is being produced by hello pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="0d8c3-197">To ustawienie dotyczy tooinputs pierwsze działanie w potoku.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-197">This setting generally applies tooinputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="0d8c3-198"><a name="Type"></a>Typ zestawu danych</span><span class="sxs-lookup"><span data-stu-id="0d8c3-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="0d8c3-199">Typ Hello hello zestawu danych jest zależny od hello magazynu danych, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-199">hello type of hello dataset depends on hello data store you use.</span></span> <span data-ttu-id="0d8c3-200">Zobacz hello w poniższej tabeli listę magazynów danych obsługiwane przez fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-200">See hello following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="0d8c3-201">Kliknij przycisk toolearn magazynu danych jak toocreate połączonej usługi i zestawu danych dla tych danych magazynu.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-201">Click a data store toolearn how toocreate a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="0d8c3-202">Przechowuje dane z * można lokalnie lub na Azure infrastruktura jako usługa (IaaS).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="0d8c3-203">Te magazyny danych wymagają tooinstall [brama zarządzania danymi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-203">These data stores require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="0d8c3-204">W przykładzie hello w poprzedniej sekcji hello hello DataSet hello ustawiono zbyt**AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-204">In hello example in hello previous section, hello type of hello dataset is set too**AzureSqlTable**.</span></span> <span data-ttu-id="0d8c3-205">Podobnie dla zestawu danych obiektów Blob platformy Azure, hello typ zestawu danych hello jest ustawiona zbyt**AzureBlob**, jak pokazano w powitania po JSON:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-205">Similarly, for an Azure Blob dataset, hello type of hello dataset is set too**AzureBlob**, as shown in hello following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <span data-ttu-id="0d8c3-206"><a name="Structure"></a>Struktura zestawu danych</span><span class="sxs-lookup"><span data-stu-id="0d8c3-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="0d8c3-207">Witaj **struktury** sekcja jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-207">hello **structure** section is optional.</span></span> <span data-ttu-id="0d8c3-208">Definiuje hello schemat zestawu danych hello przez zawierający kolekcję nazwy i typy danych kolumn.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-208">It defines hello schema of hello dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="0d8c3-209">Możesz użyć hello struktura sekcji tooprovide typ informacji o tooconvert używane typy i mapy kolumny z hello źródłowego toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-209">You use hello structure section tooprovide type information that is used tooconvert types and map columns from hello source toohello destination.</span></span> <span data-ttu-id="0d8c3-210">W hello poniższy przykład, hello dataset zawiera trzy kolumny: `slicetimestamp`, `projectname`, i `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-210">In hello following example, hello dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="0d8c3-211">Są one typu String, typ String i dziesiętnych, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="0d8c3-212">Każda kolumna w strukturze hello zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-212">Each column in hello structure contains hello following properties:</span></span>

| <span data-ttu-id="0d8c3-213">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0d8c3-213">Property</span></span> | <span data-ttu-id="0d8c3-214">Opis</span><span class="sxs-lookup"><span data-stu-id="0d8c3-214">Description</span></span> | <span data-ttu-id="0d8c3-215">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0d8c3-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d8c3-216">name</span><span class="sxs-lookup"><span data-stu-id="0d8c3-216">name</span></span> |<span data-ttu-id="0d8c3-217">Nazwa kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-217">Name of hello column.</span></span> |<span data-ttu-id="0d8c3-218">Tak</span><span class="sxs-lookup"><span data-stu-id="0d8c3-218">Yes</span></span> |
| <span data-ttu-id="0d8c3-219">type</span><span class="sxs-lookup"><span data-stu-id="0d8c3-219">type</span></span> |<span data-ttu-id="0d8c3-220">Typ danych kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-220">Data type of hello column.</span></span>  |<span data-ttu-id="0d8c3-221">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-221">No</span></span> |
| <span data-ttu-id="0d8c3-222">Kultury</span><span class="sxs-lookup"><span data-stu-id="0d8c3-222">culture</span></span> |<span data-ttu-id="0d8c3-223">. Toobe kulturę opartą na sieci używany, gdy typ hello jest typ architektury .NET: `Datetime` lub `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-223">.NET-based culture toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="0d8c3-224">Domyślnie Hello `en-us`.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-224">hello default is `en-us`.</span></span> |<span data-ttu-id="0d8c3-225">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-225">No</span></span> |
| <span data-ttu-id="0d8c3-226">Format</span><span class="sxs-lookup"><span data-stu-id="0d8c3-226">format</span></span> |<span data-ttu-id="0d8c3-227">Format ciągu toobe używany, gdy typ hello jest typ architektury .NET: `Datetime` lub `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-227">Format string toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="0d8c3-228">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-228">No</span></span> |

<span data-ttu-id="0d8c3-229">Witaj poniższe wskazówki pomocne w określeniu po tooinclude struktury informacji i jakie tooinclude w hello **struktury** sekcji.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-229">hello following guidelines help you determine when tooinclude structure information, and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="0d8c3-230">**Dla źródeł danych strukturalnych**, określ hello struktura sekcji tylko wtedy, gdy ma mapowanie kolumn toosink kolumny źródłowej, a ich nazwy nie są hello takie same.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-230">**For structured data sources**, specify hello structure section only if you want map source columns toosink columns, and their names are not hello same.</span></span> <span data-ttu-id="0d8c3-231">Tego rodzaju źródła danych strukturalnych przechowuje informacje schematu i typu danych wraz z danymi hello.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-231">This kind of structured data source stores data schema and type information along with hello data itself.</span></span> <span data-ttu-id="0d8c3-232">Przykładami źródeł danych strukturalnych programu SQL Server, Oracle i tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="0d8c3-233">Ponieważ informacje o typie jest już dostępne dla źródeł danych strukturalnych, nie może zawierać informacje o typie zawierają hello struktura sekcji.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-233">As type information is already available for structured data sources, you should not include type information when you do include hello structure section.</span></span>
* <span data-ttu-id="0d8c3-234">**Do schematu w źródłach danych odczytu (w szczególności magazynu obiektów Blob)**, można wybrać toostore danych bez żadnych informacji schematu i typu danych hello przechowywania.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-234">**For schema on read data sources (specifically Blob storage)**, you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="0d8c3-235">W przypadku tych typów źródeł danych mają strukturę należy toomap źródła kolumny toosink kolumny.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-235">For these types of data sources, include structure when you want toomap source columns toosink columns.</span></span> <span data-ttu-id="0d8c3-236">Gdy hello zestawu danych jest wartością wejściową dla działania kopiowania i typy danych zestawu źródła danych powinny być przekonwertowana toonative typy dla obiekt sink hello także struktury.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-236">Also include structure when hello dataset is an input for a copy activity, and data types of source dataset should be converted toonative types for hello sink.</span></span> 
    
    <span data-ttu-id="0d8c3-237">Fabryka danych obsługuje następujące wartości udostępnienie informacji o typie w strukturze hello: **Int16, Int32, Int64, pojedynczego, Double, Decimal bajtów [], wartość logiczna, ciąg, Guid, Datetime, Datetimeoffset i Timespan**.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-237">Data Factory supports hello following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="0d8c3-238">Te wartości są specyfikacja języka wspólnego (CLS)-zgodne,. Wartości typu opartej na sieci.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="0d8c3-239">Fabryka danych automatycznie wykonuje konwersje typów przemieszczając się, że magazyn danych ze źródła danych magazynu danych tooa ujścia.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-239">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="0d8c3-240">Dostępność zestawu danych</span><span class="sxs-lookup"><span data-stu-id="0d8c3-240">Dataset availability</span></span>
<span data-ttu-id="0d8c3-241">Witaj **dostępności** hello okna przetwarzania (na przykład co godzinę, codziennie lub co tydzień) dla zestawu danych hello definiuje sekcję w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-241">hello **availability** section in a dataset defines hello processing window (for example, hourly, daily, or weekly) for hello dataset.</span></span> <span data-ttu-id="0d8c3-242">Aby uzyskać więcej informacji na temat działania systemu windows, zobacz [planowania i wykonywania](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="0d8c3-243">powitania po sekcji dostępności Określa, że hello wyjściowy zestaw danych jest albo tworzone co godzinę lub co godzinę hello wejściowy zestaw danych jest dostępne:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-243">hello following availability section specifies that hello output dataset is either produced hourly, or hello input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="0d8c3-244">Jeśli potoku hello ma powitania od godziny rozpoczęcia i zakończenia:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-244">If hello pipeline has hello following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="0d8c3-245">Witaj wyjściowy zestaw danych jest tworzony co godzinę w potoku hello godziny rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-245">hello output dataset is produced hourly within hello pipeline start and end times.</span></span> <span data-ttu-id="0d8c3-246">W związku z tym ma pięć wycinków zestaw danych utworzonych w ramach tego potoku, po jednej dla każdego działania okna (00: 00 - 1 AM, 1: 00 - 2 AM, 2 AM - 3 AM, 3 AM — 4 AM, 4: 00 - 5: 00).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="0d8c3-247">Witaj poniższej tabeli opisano właściwości, które można użyć w sekcji dostępności hello:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-247">hello following table describes properties you can use in hello availability section:</span></span>

| <span data-ttu-id="0d8c3-248">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0d8c3-248">Property</span></span> | <span data-ttu-id="0d8c3-249">Opis</span><span class="sxs-lookup"><span data-stu-id="0d8c3-249">Description</span></span> | <span data-ttu-id="0d8c3-250">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0d8c3-250">Required</span></span> | <span data-ttu-id="0d8c3-251">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0d8c3-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d8c3-252">frequency</span><span class="sxs-lookup"><span data-stu-id="0d8c3-252">frequency</span></span> |<span data-ttu-id="0d8c3-253">Określa jednostkę czasu hello w środowisku produkcyjnym wycinek zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-253">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="0d8c3-254"><b>Obsługiwana częstotliwość</b>: minuty, godziny, dnia, tygodnia, miesiąca</span><span class="sxs-lookup"><span data-stu-id="0d8c3-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="0d8c3-255">Tak</span><span class="sxs-lookup"><span data-stu-id="0d8c3-255">Yes</span></span> |<span data-ttu-id="0d8c3-256">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-256">NA</span></span> |
| <span data-ttu-id="0d8c3-257">interval</span><span class="sxs-lookup"><span data-stu-id="0d8c3-257">interval</span></span> |<span data-ttu-id="0d8c3-258">Określa mnożnik częstotliwości.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="0d8c3-259">"Interwał częstotliwości x" Określa, jak często hello wycinek jest generowany.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-259">"Frequency x interval" determines how often hello slice is produced.</span></span> <span data-ttu-id="0d8c3-260">Na przykład, jeśli konieczne hello podzielona na godzinę toobe zestawu danych, należy ustawić <b>częstotliwość</b> za<b>godzina</b>, i <b>interwał</b> za<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-260">For example, if you need hello dataset toobe sliced on an hourly basis, you set <b>frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="0d8c3-261">Należy pamiętać, że jeśli określisz **częstotliwość** jako **minutę**, należy ustawić hello interwał toono mniej niż 15.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-261">Note that if you specify **frequency** as **Minute**, you should set hello interval toono less than 15.</span></span> |<span data-ttu-id="0d8c3-262">Tak</span><span class="sxs-lookup"><span data-stu-id="0d8c3-262">Yes</span></span> |<span data-ttu-id="0d8c3-263">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-263">NA</span></span> |
| <span data-ttu-id="0d8c3-264">Styl</span><span class="sxs-lookup"><span data-stu-id="0d8c3-264">style</span></span> |<span data-ttu-id="0d8c3-265">Określa, czy wycinek hello powinien zostać utworzony w hello początek lub koniec interwału powitania.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-265">Specifies whether hello slice should be produced at hello start or end of hello interval.</span></span><ul><li><span data-ttu-id="0d8c3-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="0d8c3-266">StartOfInterval</span></span></li><li><span data-ttu-id="0d8c3-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="0d8c3-267">EndOfInterval</span></span></li></ul><span data-ttu-id="0d8c3-268">Jeśli **częstotliwość** ustawiono zbyt**miesiąca**, i **styl** ustawiono zbyt**EndOfInterval**, wycinek hello jest generowany na powitania ostatni dzień miesiąca.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-268">If **frequency** is set too**Month**, and **style** is set too**EndOfInterval**, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="0d8c3-269">Jeśli **styl** ustawiono zbyt**StartOfInterval**, wycinek hello jest generowany na powitania pierwszego dnia miesiąca.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-269">If **style** is set too**StartOfInterval**, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="0d8c3-270">Jeśli **częstotliwość** ustawiono zbyt**dzień**, i **styl** ustawiono zbyt**EndOfInterval**, wycinek hello jest generowany w hello ostatniej godziny hello dnia.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-270">If **frequency** is set too**Day**, and **style** is set too**EndOfInterval**, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="0d8c3-271">Jeśli **częstotliwość** ustawiono zbyt**godzina**, i **styl** ustawiono zbyt**EndOfInterval**, wycinek hello jest generowany na końcu hello hello godzinę.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-271">If **frequency** is set too**Hour**, and **style** is set too**EndOfInterval**, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="0d8c3-272">Na przykład dla wycinek hello okres 13: 00 - 14: 00, wycinek hello jest generowany na 14: 00.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-272">For example, for a slice for hello 1 PM - 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="0d8c3-273">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-273">No</span></span> |<span data-ttu-id="0d8c3-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="0d8c3-274">EndOfInterval</span></span> |
| <span data-ttu-id="0d8c3-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="0d8c3-275">anchorDateTime</span></span> |<span data-ttu-id="0d8c3-276">Definiuje położenie bezwzględne hello w czasie używane przez hello harmonogramu toocompute dataset wycinek granic.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-276">Defines hello absolute position in time used by hello scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="0d8c3-277">Należy pamiętać, że jeśli ta propoerty ma części daty, które są bardziej szczegółowego niż hello określa częstotliwość hello części bardziej szczegółowego są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-277">Note that if this propoerty has date parts that are more granular than hello specified frequency, hello more granular parts are ignored.</span></span> <span data-ttu-id="0d8c3-278">Na przykład, jeśli hello **interwał** jest **co godzinę** (częstotliwość: godzinę i interwał: 1), a hello **anchorDateTime** zawiera **minut i sekund**, następnie hello części minut i sekund **anchorDateTime** są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-278">For example, if hello **interval** is **hourly** (frequency: hour and interval: 1), and hello **anchorDateTime** contains **minutes and seconds**, then hello minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="0d8c3-279">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-279">No</span></span> |<span data-ttu-id="0d8c3-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="0d8c3-280">01/01/0001</span></span> |
| <span data-ttu-id="0d8c3-281">Przesunięcie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-281">offset</span></span> |<span data-ttu-id="0d8c3-282">Zakres czasu, przez który hello przesunięte początku i końcu wszystkie fragmenty zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-282">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="0d8c3-283">Należy pamiętać, że jeśli obie **anchorDateTime** i **przesunięcie** są określone, wynik hello jest shift hello połączone.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-283">Note that if both **anchorDateTime** and **offset** are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="0d8c3-284">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-284">No</span></span> |<span data-ttu-id="0d8c3-285">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="0d8c3-286">przykład przesunięcia</span><span class="sxs-lookup"><span data-stu-id="0d8c3-286">offset example</span></span>
<span data-ttu-id="0d8c3-287">Domyślnie codziennie (`"frequency": "Day", "interval": 1`) wycinków Rozpocznij od 00: 00 (północ) uniwersalny czas koordynowany (UTC).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="0d8c3-288">Czas UTC 6: 00 toobe czas rozpoczęcia hello zamiast tego, ustawić hello przesunięcie pokazane na powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-288">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="0d8c3-289">przykład anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="0d8c3-289">anchorDateTime example</span></span>
<span data-ttu-id="0d8c3-290">W hello poniższy przykład hello dataset jest tworzony co 23 godz.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-290">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="0d8c3-291">Witaj pierwszego wycinka rozpoczyna się od czasu hello określonego przez **anchorDateTime**, która wartość jest zbyt`2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-291">hello first slice starts at hello time specified by **anchorDateTime**, which is set too`2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="0d8c3-292">przykład przesunięcie i stylu</span><span class="sxs-lookup"><span data-stu-id="0d8c3-292">offset/style example</span></span>
<span data-ttu-id="0d8c3-293">Witaj następujący zestaw danych jest co miesiąc i jest generowany na powitania 3rd każdego miesiąca o godzinie 8:00 AM (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="0d8c3-293">hello following dataset is monthly, and is produced on hello 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="0d8c3-294"><a name="Policy"></a>Zestaw danych zasad</span><span class="sxs-lookup"><span data-stu-id="0d8c3-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="0d8c3-295">Witaj **zasad** sekcja w definicji zestawu danych hello definiuje kryteria hello lub konieczne jest spełnienie warunku hello hello wycinków zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-295">hello **policy** section in hello dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="0d8c3-296">Zasady sprawdzania poprawności</span><span class="sxs-lookup"><span data-stu-id="0d8c3-296">Validation policies</span></span>
| <span data-ttu-id="0d8c3-297">Nazwa zasad</span><span class="sxs-lookup"><span data-stu-id="0d8c3-297">Policy name</span></span> | <span data-ttu-id="0d8c3-298">Opis</span><span class="sxs-lookup"><span data-stu-id="0d8c3-298">Description</span></span> | <span data-ttu-id="0d8c3-299">Stosowane za</span><span class="sxs-lookup"><span data-stu-id="0d8c3-299">Applied too</span></span>| <span data-ttu-id="0d8c3-300">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0d8c3-300">Required</span></span> | <span data-ttu-id="0d8c3-301">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0d8c3-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0d8c3-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="0d8c3-302">minimumSizeMB</span></span> |<span data-ttu-id="0d8c3-303">Sprawdza poprawność danych hello w **magazynu obiektów Blob Azure** spełnia hello wymagań minimalny rozmiar (w MB).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-303">Validates that hello data in **Azure Blob storage** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="0d8c3-304">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="0d8c3-304">Azure Blob storage</span></span> |<span data-ttu-id="0d8c3-305">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-305">No</span></span> |<span data-ttu-id="0d8c3-306">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-306">NA</span></span> |
| <span data-ttu-id="0d8c3-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="0d8c3-307">minimumRows</span></span> |<span data-ttu-id="0d8c3-308">Sprawdza poprawność danych hello w **bazy danych Azure SQL** lub **tabeli platformy Azure** zawiera hello minimalną liczbę wierszy.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-308">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="0d8c3-309">Baza danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0d8c3-309">Azure SQL database</span></span></li><li><span data-ttu-id="0d8c3-310">Tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0d8c3-310">Azure table</span></span></li></ul> |<span data-ttu-id="0d8c3-311">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-311">No</span></span> |<span data-ttu-id="0d8c3-312">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0d8c3-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="0d8c3-313">Przykłady</span><span class="sxs-lookup"><span data-stu-id="0d8c3-313">Examples</span></span>
<span data-ttu-id="0d8c3-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="0d8c3-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="0d8c3-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="0d8c3-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="0d8c3-316">Zewnętrznych zestawów danych</span><span class="sxs-lookup"><span data-stu-id="0d8c3-316">External datasets</span></span>
<span data-ttu-id="0d8c3-317">Zewnętrznych zestawów danych są hello te, które nie są produkowane przez uruchomione potok w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-317">External datasets are hello ones that are not produced by a running pipeline in hello data factory.</span></span> <span data-ttu-id="0d8c3-318">Jeśli hello zestawu danych jest oznaczona jako **zewnętrznych**, hello **ExternalData** zasad może być tooinfluence zdefiniowanego zachowania hello hello dataset wycinek dostępności.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-318">If hello dataset is marked as **external**, hello **ExternalData** policy may be defined tooinfluence hello behavior of hello dataset slice availability.</span></span>

<span data-ttu-id="0d8c3-319">Jeśli zestaw danych jest tworzonym przez fabrykę danych, powinien być oznaczony jako **zewnętrznych**.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="0d8c3-320">To ustawienie dotyczy wejść toohello pierwszy aktywności w potoku, chyba że działania lub łańcucha potoku jest używany.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-320">This setting generally applies toohello inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="0d8c3-321">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0d8c3-321">Name</span></span> | <span data-ttu-id="0d8c3-322">Opis</span><span class="sxs-lookup"><span data-stu-id="0d8c3-322">Description</span></span> | <span data-ttu-id="0d8c3-323">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0d8c3-323">Required</span></span> | <span data-ttu-id="0d8c3-324">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="0d8c3-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d8c3-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="0d8c3-325">dataDelay</span></span> |<span data-ttu-id="0d8c3-326">czas Hello toodelay hello sprawdzanie dostępności hello hello danych zewnętrznych dla hello podany wycinka.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-326">hello time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="0d8c3-327">Na przykład za pomocą tego ustawienia można opóźnić wyboru co godzinę.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="0d8c3-328">Witaj ustawienie dotyczy tylko toohello obecny czas.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-328">hello setting only applies toohello present time.</span></span>  <span data-ttu-id="0d8c3-329">Na przykład jeśli 1:00 PM od razu i ta wartość to 10 minut, weryfikacji hello rozpoczyna się od 1:22:00.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-329">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="0d8c3-330">Należy zwrócić uwagę, to ustawienie nie wpływa na wycinki hello ostatnich.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-330">Note that this setting does not affect slices in hello past.</span></span> <span data-ttu-id="0d8c3-331">Wycinków z **czas zakończenia wycinek** + **dataDelay** < **teraz** są przetwarzane bez opóźnień.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="0d8c3-332">Godzinach większą niż 23:59 godziny należy określić przy użyciu hello `day.hours:minutes:seconds` format.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-332">Times greater than 23:59 hours should be specified by using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="0d8c3-333">Na przykład toospecify 24 godziny, nie używaj 24:00:00.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-333">For example, toospecify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="0d8c3-334">Zamiast tego należy użyć 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="0d8c3-335">Jeśli używasz 24:00:00, będzie traktowane jako 24 dni (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="0d8c3-336">1 dzień i 4 godziny Określ 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="0d8c3-337">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-337">No</span></span> |<span data-ttu-id="0d8c3-338">0</span><span class="sxs-lookup"><span data-stu-id="0d8c3-338">0</span></span> |
| <span data-ttu-id="0d8c3-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="0d8c3-339">retryInterval</span></span> |<span data-ttu-id="0d8c3-340">czas oczekiwania Hello między błędu i hello ponowieniem próby.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-340">hello wait time between a failure and hello next attempt.</span></span> <span data-ttu-id="0d8c3-341">To ustawienie dotyczy toopresent czasu.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-341">This setting applies toopresent time.</span></span> <span data-ttu-id="0d8c3-342">Jeśli poprzednie spróbuj hello zakończyło się niepowodzeniem, po hello jest hello następnej próbie **retryInterval** okresu.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-342">If hello previous try failed, hello next try is after hello **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="0d8c3-343">Jeśli jest 1:00 PM od razu, możemy rozpocząć hello pierwszej próby.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-343">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="0d8c3-344">W przypadku 1 minutę i nie można wykonać operacji hello hello czas trwania toocomplete hello pierwsze sprawdzanie poprawności hello Następna ponowna próba nastąpi na 1:00 1 min (czas trwania) + 1min (interwał ponawiania) = 13:02:00.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-344">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="0d8c3-345">Wycinki w przeszłości hello nie ma żadnego opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-345">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="0d8c3-346">Ponów próbę Hello odbywa się natychmiast.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-346">hello retry happens immediately.</span></span> |<span data-ttu-id="0d8c3-347">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-347">No</span></span> |<span data-ttu-id="0d8c3-348">00:01:00 (1 minuta)</span><span class="sxs-lookup"><span data-stu-id="0d8c3-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="0d8c3-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="0d8c3-349">retryTimeout</span></span> |<span data-ttu-id="0d8c3-350">Witaj limitu czasu dla każdego ponowienia próby.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-350">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="0d8c3-351">Jeśli ta właściwość jest ustawiona minut too10 weryfikacji hello powinna zostać ukończona w ciągu 10 minut.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-351">If this property is set too10 minutes, hello validation should be completed within 10 minutes.</span></span> <span data-ttu-id="0d8c3-352">Jeśli trwa dłużej niż 10 minut tooperform hello weryfikacji, hello ponów limit.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-352">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="0d8c3-353">Jeśli wszystkie próby dla limitu czasu sprawdzania poprawności hello, hello wycinek jest oznaczony jako **upłynął limit czasu**.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-353">If all attempts for hello validation time out, hello slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="0d8c3-354">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-354">No</span></span> |<span data-ttu-id="0d8c3-355">00:10:00 (10 minut)</span><span class="sxs-lookup"><span data-stu-id="0d8c3-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="0d8c3-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="0d8c3-356">maximumRetry</span></span> |<span data-ttu-id="0d8c3-357">Witaj liczba toocheck dostępności hello hello danych zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-357">hello number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="0d8c3-358">Witaj maksymalna dozwolona wartość to 10.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-358">hello maximum allowed value is 10.</span></span> |<span data-ttu-id="0d8c3-359">Nie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-359">No</span></span> |<span data-ttu-id="0d8c3-360">3</span><span class="sxs-lookup"><span data-stu-id="0d8c3-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="0d8c3-361">Tworzenie zestawów danych</span><span class="sxs-lookup"><span data-stu-id="0d8c3-361">Create datasets</span></span>
<span data-ttu-id="0d8c3-362">Zestawy danych można utworzyć za pomocą jednej z tych narzędzi i zestawy SDK:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="0d8c3-363">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="0d8c3-363">Copy Wizard</span></span> 
- <span data-ttu-id="0d8c3-364">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0d8c3-364">Azure portal</span></span>
- <span data-ttu-id="0d8c3-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0d8c3-365">Visual Studio</span></span>
- <span data-ttu-id="0d8c3-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d8c3-366">PowerShell</span></span>
- <span data-ttu-id="0d8c3-367">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0d8c3-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="0d8c3-368">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="0d8c3-368">REST API</span></span>
- <span data-ttu-id="0d8c3-369">Interfejs API .NET</span><span class="sxs-lookup"><span data-stu-id="0d8c3-369">.NET API</span></span>

<span data-ttu-id="0d8c3-370">Zobacz hello następujące samouczki instrukcje krok po kroku dotyczące tworzenia potoki i zestawów danych przy użyciu jednej z tych narzędzi i zestawy SDK:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-370">See hello following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="0d8c3-371">Tworzenie potoku z działaniem przekształcania danych</span><span class="sxs-lookup"><span data-stu-id="0d8c3-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="0d8c3-372">Tworzenie potoku z działaniem przepływu danych</span><span class="sxs-lookup"><span data-stu-id="0d8c3-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="0d8c3-373">Po utworzeniu i wdrożeniu potoku można zarządzać i monitorować Twoje potoki przy użyciu hello Azure bloki portalu lub aplikacji hello monitorowanie i zarządzanie.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using hello Azure portal blades, or hello Monitoring and Management app.</span></span> <span data-ttu-id="0d8c3-374">Zobacz następujące tematy, aby uzyskać instrukcje krok po kroku hello:</span><span class="sxs-lookup"><span data-stu-id="0d8c3-374">See hello following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="0d8c3-375">Monitorowanie i zarządzanie nimi potoki przy użyciu bloków portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0d8c3-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="0d8c3-376">Monitorowanie i zarządzanie nimi potoki przy użyciu aplikacji hello monitorowanie i zarządzanie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-376">Monitor and manage pipelines by using hello Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="0d8c3-377">Zestawy danych w zakresie</span><span class="sxs-lookup"><span data-stu-id="0d8c3-377">Scoped datasets</span></span>
<span data-ttu-id="0d8c3-378">Możesz utworzyć zestawy danych, które są potoku o zakresie tooa przy użyciu hello **zestawów danych** właściwości.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-378">You can create datasets that are scoped tooa pipeline by using hello **datasets** property.</span></span> <span data-ttu-id="0d8c3-379">Te zestawy danych można używać tylko przez działania w ramach tego potoku, a nie przez działania w innych potoków.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="0d8c3-380">Poniższy przykład Hello definiuje potoku z dwóch zestawów danych (InputDataset rdc i kompresji rdc OutputDataset) toobe używane w ramach hello potoku.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-380">hello following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) toobe used within hello pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="0d8c3-381">Zestawy danych w zakresie są obsługiwane tylko w przypadku jednorazowego potoki (gdzie **pipelineMode** ustawiono zbyt**OneTime**).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set too**OneTime**).</span></span> <span data-ttu-id="0d8c3-382">Zobacz [potoku Onetime](data-factory-create-pipelines.md#onetime-pipeline) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0d8c3-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="0d8c3-383">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d8c3-383">Next steps</span></span>
- <span data-ttu-id="0d8c3-384">Aby uzyskać więcej informacji na temat potoków, zobacz [tworzenie potoków](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="0d8c3-385">Aby uzyskać więcej informacji o sposobie planowania i wykonywania potoków, zobacz [planowania i wykonywania w fabryce danych Azure](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="0d8c3-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
