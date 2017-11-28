---
title: "aaaUpload dużych ilości danych do usługi Data Lake Store za pomocą metod w trybie offline | Dokumentacja firmy Microsoft"
description: "TooData Lake — magazyn obiektów blob hello Użyj AdlCopy narzędzie toocopy danych z magazynu Azure"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="521c6-103">Korzystanie z usługi Import/Eksport Azure hello w trybie offline z kopiowaniem tooData data Lake — Magazyn</span><span class="sxs-lookup"><span data-stu-id="521c6-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="521c6-104">W tym artykule dowiesz się, jak zestawy danych ogromnych toocopy (> 200 GB) do usługi Azure Data Lake Store za pomocą metody kopiowania w trybie offline, takich jak hello [usługi Import/Eksport Azure](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="521c6-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="521c6-105">W szczególności plik hello używany na przykład w tym artykule jest 339,420,860,416 bajtów lub około 319 GB na dysku.</span><span class="sxs-lookup"><span data-stu-id="521c6-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="521c6-106">Umożliwia wywołanie 319GB.tsv tego pliku.</span><span class="sxs-lookup"><span data-stu-id="521c6-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="521c6-107">Witaj usługi Import/Eksport Azure ułatwia tootransfer dużych ilości danych więcej bezpiecznie tooAzure magazynu obiektów Blob przy wysyłaniu dysku twardego dyski tooan centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="521c6-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="521c6-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="521c6-108">Prerequisites</span></span>
<span data-ttu-id="521c6-109">Przed rozpoczęciem, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="521c6-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="521c6-110">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="521c6-110">**An Azure subscription**.</span></span> <span data-ttu-id="521c6-111">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="521c6-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="521c6-112">**Konto magazynu platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="521c6-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="521c6-113">**Konto usługi Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="521c6-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="521c6-114">Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="521c6-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="521c6-115">Przygotowywanie danych hello</span><span class="sxs-lookup"><span data-stu-id="521c6-115">Preparing hello data</span></span>
<span data-ttu-id="521c6-116">Przed rozpoczęciem korzystania z usługi Import/Eksport hello przekazywane podziału hello danych pliku toobe **do kopie, które są mniej niż 200 GB** rozmiar.</span><span class="sxs-lookup"><span data-stu-id="521c6-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="521c6-117">Narzędzie importu Hello nie działa z pliki większe niż 200 GB.</span><span class="sxs-lookup"><span data-stu-id="521c6-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="521c6-118">W tym samouczku możemy podzielić na fragmenty 100 GB hello pliku.</span><span class="sxs-lookup"><span data-stu-id="521c6-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="521c6-119">Można to zrobić za pomocą [programów Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="521c6-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="521c6-120">Programów Cygwin obsługuje polecenia systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="521c6-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="521c6-121">W takim przypadku należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="521c6-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="521c6-122">Operacja podziału Hello tworzy pliki z hello następujące nazwy.</span><span class="sxs-lookup"><span data-stu-id="521c6-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="521c6-123">Przygotowanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="521c6-123">Get disks ready with data</span></span>
<span data-ttu-id="521c6-124">Postępuj zgodnie z instrukcjami hello [za pomocą usługi Import/Eksport Azure hello](../storage/common/storage-import-export-service.md) (w obszarze hello **przygotowanie dysków** sekcji) tooprepare dyskach twardych.</span><span class="sxs-lookup"><span data-stu-id="521c6-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="521c6-125">Poniżej przedstawiono ogólną sekwencję hello:</span><span class="sxs-lookup"><span data-stu-id="521c6-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="521c6-126">Uzyskaj spełnia toobe wymaganie hello używany dla hello usługi Import/Eksport Azure dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="521c6-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="521c6-127">Określ konto magazynu Azure, w której zostanie skopiowany hello danych po jest dostarczany toohello centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="521c6-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="521c6-128">Użyj hello [narzędzie importu/eksportu Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), narzędzie wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="521c6-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="521c6-129">Oto fragment próbki, który pokazuje, jak toouse hello narzędzia.</span><span class="sxs-lookup"><span data-stu-id="521c6-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="521c6-130">Zobacz [za pomocą usługi Import/Eksport Azure hello](../storage/common/storage-import-export-service.md) dla więcej przykładowe fragmenty kodu.</span><span class="sxs-lookup"><span data-stu-id="521c6-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="521c6-131">Witaj poprzednie polecenie powoduje utworzenie dziennika pliku hello określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="521c6-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="521c6-132">Użyj tego toocreate pliku dziennika zadania importu z hello [klasycznego portalu Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="521c6-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="521c6-133">Utwórz zadania importu</span><span class="sxs-lookup"><span data-stu-id="521c6-133">Create an import job</span></span>
<span data-ttu-id="521c6-134">Teraz można utworzyć zadania importu za pomocą instrukcji hello w [za pomocą usługi Import/Eksport Azure hello](../storage/common/storage-import-export-service.md) (w obszarze hello **zadania importu hello Utwórz** sekcji).</span><span class="sxs-lookup"><span data-stu-id="521c6-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="521c6-135">W przypadku tego zadania importu z innych szczegółów zapewnić hello plik dziennika utworzony podczas przygotowywania dysków hello.</span><span class="sxs-lookup"><span data-stu-id="521c6-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="521c6-136">Fizycznie wysłać hello dysków</span><span class="sxs-lookup"><span data-stu-id="521c6-136">Physically ship hello disks</span></span>
<span data-ttu-id="521c6-137">Teraz można fizycznie wysłać hello dysków tooan centrum danych Azure.</span><span class="sxs-lookup"><span data-stu-id="521c6-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="521c6-138">Hello danych jest kopiowana za pośrednictwem obiektów blob magazynu Azure toohello, dostępne podczas tworzenia zadania importu hello.</span><span class="sxs-lookup"><span data-stu-id="521c6-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="521c6-139">Ponadto podczas tworzenia zadania hello, jeśli wybierze tooprovide hello później, informacje o monitorowaniu możesz teraz wrócić tooyour importu zadania i aktualizacji hello numer śledzenia.</span><span class="sxs-lookup"><span data-stu-id="521c6-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="521c6-140">Kopiowanie danych z magazynu Azure blob tooAzure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="521c6-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="521c6-141">Po hello stan hello zadania importu pokazuje, że zakończy pracę, można sprawdzić, czy dane hello są dostępne w obiektach blob magazynu Azure hello ma określone.</span><span class="sxs-lookup"><span data-stu-id="521c6-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="521c6-142">Następnie można użyć różnych metod toomove, że dane z hello obiektów blob tooAzure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="521c6-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="521c6-143">Dla wszystkich hello dostępne opcje dotyczące przekazywania danych, zobacz [wprowadzania danych do usługi Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="521c6-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="521c6-144">W tej sekcji możemy udostępnić definicji JSON hello kopiowania danych można toocreate potoku fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="521c6-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="521c6-145">Korzystając z tych definicji JSON z hello [portalu Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), lub [programu Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="521c6-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="521c6-146">Źródło połączone usługi (obiektu blob magazynu Azure)</span><span class="sxs-lookup"><span data-stu-id="521c6-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="521c6-147">Docelowe połączone usługi (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="521c6-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="521c6-148">Wejściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="521c6-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="521c6-149">Zestaw danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="521c6-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="521c6-150">Potok (działanie kopiowania)</span><span class="sxs-lookup"><span data-stu-id="521c6-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
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
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="521c6-151">Aby uzyskać więcej informacji, zobacz [przenoszenia danych z magazynu Azure blob tooAzure Data Lake Store przy użyciu fabryki danych Azure](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="521c6-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="521c6-152">Rekonstrukcji hello pliki danych w usłudze Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="521c6-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="521c6-153">Możemy korzystać z pliku, który został 319 GB i spowodowało przerwanie go w dół na pliki mają mniejszy rozmiar, dzięki czemu można dokonać transferu za pomocą usługi Import/Eksport Azure hello.</span><span class="sxs-lookup"><span data-stu-id="521c6-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="521c6-154">Teraz, hello dane pochodzą z usługi Azure Data Lake Store, możemy rekonstrukcji hello pliku tooits oryginalny rozmiar.</span><span class="sxs-lookup"><span data-stu-id="521c6-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="521c6-155">Możesz użyć hello, więc po toodo cmldts programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="521c6-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="521c6-156">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="521c6-156">Next steps</span></span>
* [<span data-ttu-id="521c6-157">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="521c6-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="521c6-158">Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="521c6-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="521c6-159">Korzystanie z usługi Azure HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="521c6-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
