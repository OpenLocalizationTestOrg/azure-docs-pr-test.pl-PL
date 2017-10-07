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
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a>Korzystanie z usługi Import/Eksport Azure hello w trybie offline z kopiowaniem tooData data Lake — Magazyn
W tym artykule dowiesz się, jak zestawy danych ogromnych toocopy (> 200 GB) do usługi Azure Data Lake Store za pomocą metody kopiowania w trybie offline, takich jak hello [usługi Import/Eksport Azure](../storage/common/storage-import-export-service.md). W szczególności plik hello używany na przykład w tym artykule jest 339,420,860,416 bajtów lub około 319 GB na dysku. Umożliwia wywołanie 319GB.tsv tego pliku.

Witaj usługi Import/Eksport Azure ułatwia tootransfer dużych ilości danych więcej bezpiecznie tooAzure magazynu obiektów Blob przy wysyłaniu dysku twardego dyski tooan centrum danych Azure.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem, musi mieć następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Konto magazynu platformy Azure**.
* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)

## <a name="preparing-hello-data"></a>Przygotowywanie danych hello
Przed rozpoczęciem korzystania z usługi Import/Eksport hello przekazywane podziału hello danych pliku toobe **do kopie, które są mniej niż 200 GB** rozmiar. Narzędzie importu Hello nie działa z pliki większe niż 200 GB. W tym samouczku możemy podzielić na fragmenty 100 GB hello pliku. Można to zrobić za pomocą [programów Cygwin](https://cygwin.com/install.html). Programów Cygwin obsługuje polecenia systemu Linux. W takim przypadku należy użyć hello następujące polecenie:

    split -b 100m 319GB.tsv

Operacja podziału Hello tworzy pliki z hello następujące nazwy.

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a>Przygotowanie dysków z danymi
Postępuj zgodnie z instrukcjami hello [za pomocą usługi Import/Eksport Azure hello](../storage/common/storage-import-export-service.md) (w obszarze hello **przygotowanie dysków** sekcji) tooprepare dyskach twardych. Poniżej przedstawiono ogólną sekwencję hello:

1. Uzyskaj spełnia toobe wymaganie hello używany dla hello usługi Import/Eksport Azure dysku twardego.
2. Określ konto magazynu Azure, w której zostanie skopiowany hello danych po jest dostarczany toohello centrum danych Azure.
3. Użyj hello [narzędzie importu/eksportu Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), narzędzie wiersza polecenia. Oto fragment próbki, który pokazuje, jak toouse hello narzędzia.

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    Zobacz [za pomocą usługi Import/Eksport Azure hello](../storage/common/storage-import-export-service.md) dla więcej przykładowe fragmenty kodu.
4. Witaj poprzednie polecenie powoduje utworzenie dziennika pliku hello określonej lokalizacji. Użyj tego toocreate pliku dziennika zadania importu z hello [klasycznego portalu Azure](https://manage.windowsazure.com).

## <a name="create-an-import-job"></a>Utwórz zadania importu
Teraz można utworzyć zadania importu za pomocą instrukcji hello w [za pomocą usługi Import/Eksport Azure hello](../storage/common/storage-import-export-service.md) (w obszarze hello **zadania importu hello Utwórz** sekcji). W przypadku tego zadania importu z innych szczegółów zapewnić hello plik dziennika utworzony podczas przygotowywania dysków hello.

## <a name="physically-ship-hello-disks"></a>Fizycznie wysłać hello dysków
Teraz można fizycznie wysłać hello dysków tooan centrum danych Azure. Hello danych jest kopiowana za pośrednictwem obiektów blob magazynu Azure toohello, dostępne podczas tworzenia zadania importu hello. Ponadto podczas tworzenia zadania hello, jeśli wybierze tooprovide hello później, informacje o monitorowaniu możesz teraz wrócić tooyour importu zadania i aktualizacji hello numer śledzenia.

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a>Kopiowanie danych z magazynu Azure blob tooAzure Data Lake Store
Po hello stan hello zadania importu pokazuje, że zakończy pracę, można sprawdzić, czy dane hello są dostępne w obiektach blob magazynu Azure hello ma określone. Następnie można użyć różnych metod toomove, że dane z hello obiektów blob tooAzure Data Lake Store. Dla wszystkich hello dostępne opcje dotyczące przekazywania danych, zobacz [wprowadzania danych do usługi Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).

W tej sekcji możemy udostępnić definicji JSON hello kopiowania danych można toocreate potoku fabryki danych Azure. Korzystając z tych definicji JSON z hello [portalu Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), lub [programu Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), lub [programu Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).

### <a name="source-linked-service-azure-storage-blob"></a>Źródło połączone usługi (obiektu blob magazynu Azure)
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

### <a name="target-linked-service-azure-data-lake-store"></a>Docelowe połączone usługi (Azure Data Lake Store)
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
### <a name="input-data-set"></a>Wejściowy zestaw danych
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
### <a name="output-data-set"></a>Zestaw danych wyjściowych
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
### <a name="pipeline-copy-activity"></a>Potok (działanie kopiowania)
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
Aby uzyskać więcej informacji, zobacz [przenoszenia danych z magazynu Azure blob tooAzure Data Lake Store przy użyciu fabryki danych Azure](../data-factory/data-factory-azure-datalake-connector.md).

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a>Rekonstrukcji hello pliki danych w usłudze Azure Data Lake Store
Możemy korzystać z pliku, który został 319 GB i spowodowało przerwanie go w dół na pliki mają mniejszy rozmiar, dzięki czemu można dokonać transferu za pomocą usługi Import/Eksport Azure hello. Teraz, hello dane pochodzą z usługi Azure Data Lake Store, możemy rekonstrukcji hello pliku tooits oryginalny rozmiar. Możesz użyć hello, więc po toodo cmldts programu Azure PowerShell.

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

## <a name="next-steps"></a>Następne kroki
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
