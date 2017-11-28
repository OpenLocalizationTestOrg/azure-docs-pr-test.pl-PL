---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "Magazyn obiektów blob aaaLoad danych z platformy Azure do usługi Azure SQL Data Warehouse (fabryka danych Azure) | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooload dane z fabryką danych Azure"
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: 29a220679a11cedefb0dfd06c0a6838f81a90447
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a><span data-ttu-id="2856d-103">Ładowanie danych z usługi Azure Blob Storage do usługi Azure SQL Data Warehouse (Azure Data Factory)</span><span class="sxs-lookup"><span data-stu-id="2856d-103">Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2856d-104">Data Factory</span><span class="sxs-lookup"><span data-stu-id="2856d-104">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="2856d-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="2856d-105">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 <span data-ttu-id="2856d-106">W tym samouczku przedstawiono sposób toocreate potok w fabryce danych Azure toomove danych z tooSQL obiektu Blob magazynu Azure magazyn danych.</span><span class="sxs-lookup"><span data-stu-id="2856d-106">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooSQL Data Warehouse.</span></span> <span data-ttu-id="2856d-107">Następujące kroki hello umożliwi:</span><span class="sxs-lookup"><span data-stu-id="2856d-107">With hello following steps you will:</span></span>

* <span data-ttu-id="2856d-108">Konfigurowanie przykładowych danych w rozszerzeniu Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="2856d-108">Set-up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="2856d-109">Łączenie zasobów tooAzure fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="2856d-109">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="2856d-110">Utwórz dane toomove potoku tooSQL magazynu obiektów blob magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="2856d-110">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="2856d-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="2856d-111">Before you begin</span></span>
<span data-ttu-id="2856d-112">toofamiliarize sobie z fabryką danych Azure, zobacz [tooAzure wprowadzenie fabryki danych][Introduction tooAzure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="2856d-112">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="2856d-113">Tworzenie lub identyfikowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="2856d-113">Create or identify resources</span></span>
<span data-ttu-id="2856d-114">Przed rozpoczęciem tego samouczka należy hello toohave następujące zasoby.</span><span class="sxs-lookup"><span data-stu-id="2856d-114">Before starting this tutorial, you need toohave hello following resources.</span></span>

* <span data-ttu-id="2856d-115">**Obiekt Blob magazynu Azure**: w tym samouczku korzysta z obiektu Blob magazynu Azure jako źródła danych hello hello potoku fabryki danych Azure, a zatem potrzebny będzie toohave jeden dostępny toostore hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="2856d-115">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="2856d-116">Jeśli nie masz już, Dowiedz się, jak za[Utwórz konto magazynu][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="2856d-116">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="2856d-117">**Usługa SQL Data Warehouse**: ten samouczek przenosi dane hello z obiektu Blob magazynu Azure zbyt SQL Data Warehouse i dlatego należy toohave magazyn danych online, który jest ładowany z hello przykładowe dane AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="2856d-117">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="2856d-118">Jeśli nie masz już magazyn danych, Dowiedz się, jak za[je udostępnić][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2856d-118">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="2856d-119">Jeśli masz magazyn danych, ale bez hello przykładowych danych, możesz [ręcznie załadować][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2856d-119">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="2856d-120">**Fabryka danych Azure**: fabryka danych Azure zostanie ukończona hello rzeczywiste obciążenie i dlatego należy toohave jeden służy potoku przepływu danych hello toobuild. Dowiedz się, jeśli nie masz już, jak toocreate co w kroku 1 z [Rozpoczynanie pracy z fabryką danych Azure (Edytor fabryki danych)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="2856d-120">**Azure Data Factory**: Azure Data Factory will complete hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="2856d-121">**Narzędzie AZCopy**: należy AZCopy toocopy hello przykładowych danych z lokalnego klienta tooyour obiektu Blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="2856d-121">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="2856d-122">Aby uzyskać instrukcje instalacji, zobacz hello [dokumentację programu AZCopy][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="2856d-122">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="2856d-123">Krok 1: Kopiowanie przykładowych danych tooAzure obiektu Blob magazynu</span><span class="sxs-lookup"><span data-stu-id="2856d-123">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="2856d-124">Gdy wszystkie elementy hello są gotowe, jest gotowy toocopy przykładowych danych tooyour obiektu Blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="2856d-124">Once you have all of hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="2856d-125">[Pobierz przykładowe dane][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="2856d-125">[Download sample data][Download sample data].</span></span> <span data-ttu-id="2856d-126">Te dane zostaną dodane innego trzech lat od danych sprzedaży tooyour przykładowe dane AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="2856d-126">This data will add another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="2856d-127">Użyj tego narzędzia AZCopy polecenia toocopy hello trzech lat tooyour danych obiektu Blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="2856d-127">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="2856d-128">Krok 2: Łączenie zasobów tooAzure fabryki danych</span><span class="sxs-lookup"><span data-stu-id="2856d-128">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="2856d-129">Teraz, dane hello znajdują się w miejscu, możemy utworzyć hello fabryki danych Azure potoku toomove hello danych z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2856d-129">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="2856d-130">tooget uruchomiony, otwórz hello [portalu Azure] [ Azure portal] i wybierz fabrykę danych z menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="2856d-130">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="2856d-131">Krok 2.1: tworzenie usługi połączonej</span><span class="sxs-lookup"><span data-stu-id="2856d-131">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="2856d-132">Połącz z kontem magazynu platformy Azure i fabryki danych tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2856d-132">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="2856d-133">Najpierw Rozpocznij proces rejestracji hello, klikając sekcję "Połączone usługi" hello fabrykę danych, a następnie kliknij przycisk "Nowy magazyn danych".</span><span class="sxs-lookup"><span data-stu-id="2856d-133">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="2856d-134">Wybierz magazyn azure w obszarze, wybierz magazyn Azure jako typ tooregister nazwę, a następnie wprowadź nazwę konta i klucz konta.</span><span class="sxs-lookup"><span data-stu-id="2856d-134">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="2856d-135">tooregister SQL Data Warehouse przejdź do sekcji "Utwórz i wdróż" toohello, wybierz pozycję "Nowy magazyn danych", a następnie "Azure SQL Data Warehouse".</span><span class="sxs-lookup"><span data-stu-id="2856d-135">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="2856d-136">Skopiuj dane i wklej w tym szablonie, a następnie uzupełnij go swoimi danymi.</span><span class="sxs-lookup"><span data-stu-id="2856d-136">Copy and paste in this template, and then fill in your specific information.</span></span>

```JSON
{
    "name": "<Linked Service Name>",
    "properties": {
        "description": "",
        "type": "AzureSqlDW",
        "typeProperties": {
             "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
         }
    }
}
```

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="2856d-137">Krok 2.2: Definiowanie hello zestawu danych</span><span class="sxs-lookup"><span data-stu-id="2856d-137">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="2856d-138">Po utworzenia hello połączone usługi, mamy zestawów danych hello toodefine.</span><span class="sxs-lookup"><span data-stu-id="2856d-138">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="2856d-139">W tym miejscu oznacza to, definiowania struktury hello hello danych, które są przenoszone z magazynu danych tooyour magazynu.</span><span class="sxs-lookup"><span data-stu-id="2856d-139">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="2856d-140">Więcej informacji na temat tworzenia</span><span class="sxs-lookup"><span data-stu-id="2856d-140">You can read more about creating</span></span>

1. <span data-ttu-id="2856d-141">Uruchom ten proces, przechodząc toohello sekcji "Utwórz i wdróż" w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="2856d-141">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="2856d-142">Kliknij nowy zestaw danych, a następnie "Azure Blob storage" toolink fabrykę danych tooyour magazynu.</span><span class="sxs-lookup"><span data-stu-id="2856d-142">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="2856d-143">Program hello poniżej toodefine skryptu danych w magazynie obiektów Blob platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="2856d-143">You can use hello below script toodefine your data in Azure Blob storage:</span></span>

```JSON
{
    "name": "<Dataset Name>",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "<linked storage name>",
        "typeProperties": {
            "folderPath": "<containter name>",
            "fileName": "FactInternetSales.csv",
            "format": {
            "type": "TextFormat",
            "columnDelimiter": ",",
            "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```


1. <span data-ttu-id="2856d-144">Teraz zdefiniujemy także zestaw danych dla usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2856d-144">Now we will also define our dataset for SQL Data Warehouse.</span></span>  <span data-ttu-id="2856d-145">Rozpoczynamy w hello tak samo, klikając nowy zestaw danych, a następnie "Azure SQL Data Warehouse".</span><span class="sxs-lookup"><span data-stu-id="2856d-145">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>

```JSON
{
    "name": "DWDataset",
    "properties": {
        "type": "AzureSqlDWTable",
        "linkedServiceName": "AzureSqlDWLinkedService",
        "typeProperties": {
            "tableName": "FactInternetSales"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="2856d-146">Krok 3: tworzenie i uruchamianie potoku</span><span class="sxs-lookup"><span data-stu-id="2856d-146">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="2856d-147">Na koniec zostaną wykonane konfiguracji i uruchamianie potoku hello w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="2856d-147">Finally, we will set-up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="2856d-148">Jest to hello operacja spowoduje hello rzeczywiste przeniesienie danych.</span><span class="sxs-lookup"><span data-stu-id="2856d-148">This is hello operation that will complete hello actual data movement.</span></span>  <span data-ttu-id="2856d-149">Pełny wgląd hello operacje, które można wykonać przy użyciu usługi SQL Data Warehouse i fabryki danych Azure można znaleźć [tutaj][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="2856d-149">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="2856d-150">W sekcji "Utwórz i wdróż" powitania kliknij przycisk "Więcej poleceń", a następnie klikając przycisk "Nowy potok".</span><span class="sxs-lookup"><span data-stu-id="2856d-150">In hello 'Author and Deploy' section now click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="2856d-151">Po utworzeniu potoku hello program hello poniżej kod tootransfer hello danych tooyour danych magazynu:</span><span class="sxs-lookup"><span data-stu-id="2856d-151">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
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
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="2856d-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2856d-152">Next steps</span></span>
<span data-ttu-id="2856d-153">toolearn, Rozpocznij od wyświetlenia:</span><span class="sxs-lookup"><span data-stu-id="2856d-153">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="2856d-154">[Ścieżka szkoleniowa usługi Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="2856d-154">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="2856d-155">[Łącznik usługi Azure SQL Data Warehouse][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="2856d-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="2856d-156">Jest to podstawy temat referencyjny hello korzystania z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="2856d-156">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="2856d-157">Te tematy zawierają szczegółowe informacje na temat usługi Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2856d-157">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="2856d-158">Omówiono w nich usługi Azure SQL Database lub HDinsight, ale informacje hello mają zastosowanie również tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2856d-158">They discuss Azure SQL Database or HDinsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="2856d-159">[Samouczek: Rozpoczynanie pracy z fabryką danych Azure] [ Tutorial: Get started with Azure Data Factory] to hello podstawowy samouczek dotyczący przetwarzania danych przy użyciu fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="2856d-159">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="2856d-160">W tym samouczku będzie utworzyć swój pierwszy potok, który używa HDInsight tootransform i analizowanie dzienników sieci web co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="2856d-160">In this tutorial you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="2856d-161">Zauważ, że w tym samouczku nie ma czynności kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2856d-161">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="2856d-162">[Samouczek: Kopiowanie danych z obiektu Blob magazynu Azure tooAzure bazy danych SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="2856d-162">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="2856d-163">W tym samouczku utworzysz potok w fabryce danych Azure toocopy danych z obiektu Blob magazynu Azure tooAzure bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="2856d-163">In this tutorial, you will create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
