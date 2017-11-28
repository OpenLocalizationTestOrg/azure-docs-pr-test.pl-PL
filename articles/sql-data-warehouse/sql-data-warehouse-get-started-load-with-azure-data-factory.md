---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: "aaaLoad dane z fabryką danych Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się tooload dane z fabryką danych Azure"
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="cf9d1-103">Ładowanie danych przy użyciu usługi Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cf9d1-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf9d1-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="cf9d1-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="cf9d1-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="cf9d1-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="cf9d1-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="cf9d1-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="cf9d1-107">BCP</span><span class="sxs-lookup"><span data-stu-id="cf9d1-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="cf9d1-108">W tym samouczku przedstawiono sposób toocreate potok w fabryce danych Azure toomove danych z tooAzure obiektu Blob magazynu Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-108">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="cf9d1-109">Następujące kroki hello umożliwi:</span><span class="sxs-lookup"><span data-stu-id="cf9d1-109">With hello following steps you will:</span></span>

* <span data-ttu-id="cf9d1-110">Konfigurowanie przykładowych danych w rozszerzeniu Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="cf9d1-111">Łączenie zasobów tooAzure fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-111">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="cf9d1-112">Utwórz dane toomove potoku tooSQL magazynu obiektów blob magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-112">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="cf9d1-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="cf9d1-113">Before you begin</span></span>
<span data-ttu-id="cf9d1-114">toofamiliarize sobie z fabryką danych Azure, zobacz [tooAzure wprowadzenie fabryki danych][Introduction tooAzure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-114">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="cf9d1-115">Tworzenie lub identyfikowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="cf9d1-115">Create or identify resources</span></span>
<span data-ttu-id="cf9d1-116">Przed rozpoczęciem tego samouczka potrzebne hello toohave następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="cf9d1-116">Before starting this tutorial, you need toohave hello following resources:</span></span>

* <span data-ttu-id="cf9d1-117">**Obiekt Blob magazynu Azure**: w tym samouczku korzysta z obiektu Blob magazynu Azure jako źródła danych hello hello potoku fabryki danych Azure, a zatem potrzebny będzie toohave jeden dostępny toostore hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="cf9d1-118">Jeśli nie masz już, Dowiedz się, jak za[Utwórz konto magazynu][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-118">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="cf9d1-119">**Usługa SQL Data Warehouse**: ten samouczek przenosi dane hello z obiektu Blob magazynu Azure zbyt SQL Data Warehouse i dlatego należy toohave magazyn danych online, który jest ładowany z hello przykładowe dane AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-119">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="cf9d1-120">Jeśli nie masz już magazyn danych, Dowiedz się, jak za[je udostępnić][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-120">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="cf9d1-121">Jeśli masz magazyn danych, ale bez hello przykładowych danych, możesz [ręcznie załadować][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-121">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="cf9d1-122">**Fabryka danych Azure**: fabryki danych Azure kończy hello rzeczywiste obciążenie i dlatego należy toohave jeden służy potoku przepływu danych hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-122">**Azure Data Factory**: Azure Data Factory completes hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.</span></span> <span data-ttu-id="cf9d1-123">Dowiedz się, jeśli nie masz już, jak toocreate co w kroku 1 z [Rozpoczynanie pracy z fabryką danych Azure (Edytor fabryki danych)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-123">If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="cf9d1-124">**Narzędzie AZCopy**: należy AZCopy toocopy hello przykładowych danych z lokalnego klienta tooyour obiektu Blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-124">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="cf9d1-125">Aby uzyskać instrukcje instalacji, zobacz hello [dokumentację programu AZCopy][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-125">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="cf9d1-126">Krok 1: Kopiowanie przykładowych danych tooAzure obiektu Blob magazynu</span><span class="sxs-lookup"><span data-stu-id="cf9d1-126">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="cf9d1-127">Gdy wszystkie elementy hello są gotowe, jest gotowy toocopy przykładowych danych tooyour obiektu Blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-127">Once you have all hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="cf9d1-128">[Pobierz przykładowe dane][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="cf9d1-129">Te dane dodaje innego trzech lat od danych sprzedaży tooyour przykładowe dane AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-129">This data adds another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="cf9d1-130">Użyj tego narzędzia AZCopy polecenia toocopy hello trzech lat tooyour danych obiektu Blob magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-130">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="cf9d1-131">Krok 2: Łączenie zasobów tooAzure fabryki danych</span><span class="sxs-lookup"><span data-stu-id="cf9d1-131">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="cf9d1-132">Teraz, dane hello znajdują się w miejscu, możemy utworzyć hello fabryki danych Azure potoku toomove hello danych z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-132">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="cf9d1-133">tooget uruchomiony, otwórz hello [portalu Azure] [ Azure portal] i wybierz fabrykę danych z menu po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-133">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="cf9d1-134">Krok 2.1: tworzenie usługi połączonej</span><span class="sxs-lookup"><span data-stu-id="cf9d1-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="cf9d1-135">Połącz z kontem magazynu platformy Azure i fabryki danych tooyour SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-135">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="cf9d1-136">Najpierw Rozpocznij proces rejestracji hello, klikając sekcję "Połączone usługi" hello fabrykę danych, a następnie kliknij przycisk "Nowy magazyn danych".</span><span class="sxs-lookup"><span data-stu-id="cf9d1-136">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="cf9d1-137">Wybierz magazyn azure w obszarze, wybierz magazyn Azure jako typ tooregister nazwę, a następnie wprowadź nazwę konta i klucz konta.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-137">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="cf9d1-138">tooregister SQL Data Warehouse przejdź do sekcji "Utwórz i wdróż" toohello, wybierz pozycję "Nowy magazyn danych", a następnie "Azure SQL Data Warehouse".</span><span class="sxs-lookup"><span data-stu-id="cf9d1-138">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="cf9d1-139">Skopiuj dane i wklej w tym szablonie, a następnie uzupełnij go swoimi danymi.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
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

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="cf9d1-140">Krok 2.2: Definiowanie hello zestawu danych</span><span class="sxs-lookup"><span data-stu-id="cf9d1-140">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="cf9d1-141">Po utworzenia hello połączone usługi, mamy zestawów danych hello toodefine.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-141">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="cf9d1-142">W tym miejscu oznacza to, definiowania struktury hello hello danych, które są przenoszone z magazynu danych tooyour magazynu.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-142">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="cf9d1-143">Więcej informacji na temat tworzenia</span><span class="sxs-lookup"><span data-stu-id="cf9d1-143">You can read more about creating</span></span>

1. <span data-ttu-id="cf9d1-144">Uruchom ten proces, przechodząc toohello sekcji "Utwórz i wdróż" w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-144">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="cf9d1-145">Kliknij nowy zestaw danych, a następnie "Azure Blob storage" toolink fabrykę danych tooyour magazynu.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-145">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="cf9d1-146">Program hello poniżej toodefine skryptu danych w magazynie obiektów Blob platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="cf9d1-146">You can use hello below script toodefine your data in Azure Blob storage:</span></span>
   
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
3. <span data-ttu-id="cf9d1-147">Teraz zdefiniujemy także zestaw danych dla usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="cf9d1-148">Rozpoczynamy w hello tak samo, klikając nowy zestaw danych, a następnie "Azure SQL Data Warehouse".</span><span class="sxs-lookup"><span data-stu-id="cf9d1-148">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="cf9d1-149">Krok 3: tworzenie i uruchamianie potoku</span><span class="sxs-lookup"><span data-stu-id="cf9d1-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="cf9d1-150">Na koniec mamy ustawiania i uruchom hello potok w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-150">Finally, we set up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="cf9d1-151">Jest to operacja hello, która kończy hello rzeczywiste przeniesienie danych.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-151">This is hello operation that completes hello actual data movement.</span></span>  <span data-ttu-id="cf9d1-152">Pełny wgląd hello operacje, które można wykonać przy użyciu usługi SQL Data Warehouse i fabryki danych Azure można znaleźć [tutaj][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-152">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="cf9d1-153">W sekcji "Utwórz i wdróż" hello kliknij przycisk "Więcej poleceń", a następnie klikając przycisk "Nowy potok".</span><span class="sxs-lookup"><span data-stu-id="cf9d1-153">In hello 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="cf9d1-154">Po utworzeniu potoku hello program hello poniżej kod tootransfer hello danych tooyour danych magazynu:</span><span class="sxs-lookup"><span data-stu-id="cf9d1-154">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cf9d1-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cf9d1-155">Next steps</span></span>
<span data-ttu-id="cf9d1-156">toolearn, Rozpocznij od wyświetlenia:</span><span class="sxs-lookup"><span data-stu-id="cf9d1-156">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="cf9d1-157">[Ścieżka szkoleniowa usługi Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="cf9d1-158">[Łącznik usługi Azure SQL Data Warehouse][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="cf9d1-159">Jest to podstawy temat referencyjny hello korzystania z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-159">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="cf9d1-160">Te tematy zawierają szczegółowe informacje na temat usługi Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="cf9d1-161">Omówiono w nich usługi Azure SQL Database lub HDInsight, ale informacje hello mają zastosowanie również tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-161">They discuss Azure SQL Database or HDInsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="cf9d1-162">[Samouczek: Rozpoczynanie pracy z fabryką danych Azure] [ Tutorial: Get started with Azure Data Factory] to hello podstawowy samouczek dotyczący przetwarzania danych przy użyciu fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="cf9d1-163">W tym samouczku możesz utworzyć swój pierwszy potok, który używa HDInsight tootransform i analizy dzienników sieci web co miesiąc.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-163">In this tutorial, you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="cf9d1-164">Zauważ, że w tym samouczku nie ma czynności kopiowania.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="cf9d1-165">[Samouczek: Kopiowanie danych z obiektu Blob magazynu Azure tooAzure bazy danych SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="cf9d1-165">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="cf9d1-166">W tym samouczku utworzysz potok w fabryce danych Azure toocopy danych z obiektu Blob magazynu Azure tooAzure bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="cf9d1-166">In this tutorial, you create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

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
