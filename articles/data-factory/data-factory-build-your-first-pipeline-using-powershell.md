---
title: aaaBuild pierwszy fabryki danych (PowerShell) | Dokumentacja firmy Microsoft
description: "W tym samouczku przedstawiono tworzenie przykładowego potoku usługi Azure Data Factory przy użyciu programu Azure PowerShell."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a>Samouczek: tworzenie pierwszej fabryki danych platformy Azure przy użyciu programu Azure PowerShell
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-build-your-first-pipeline.md)
> * [Witryna Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Program Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [Program PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Szablon usługi Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [Interfejs API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

W tym artykule Użyj programu Azure PowerShell toocreate Twojego pierwszego fabryki danych Azure. Samouczek hello toodo przy użyciu innych narzędzi/SDK, wybierz jedną z opcji hello z listy rozwijanej hello.

Witaj potoku, w tym samouczku ma jedno działanie: **działania HDInsight Hive**. To działanie uruchamia skrypt hive w klastrze Azure HDInsight czy transformacji wejściowych danych wyjściowych tooproduce danych. potok Hello jest zaplanowane toorun po miesiącu między hello określono godziny rozpoczęcia i zakończenia. 

> [!NOTE]
> Witaj potoku danych w tym samouczku przekształca dane wyjściowe tooproduce danych wejściowych. Nie kopiuje danych z magazynu danych źródła danych magazynu tooa docelowego. Samouczek na temat danych toocopy przy użyciu fabryki danych Azure, zobacz [samouczek: kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

## <a name="prerequisites"></a>Wymagania wstępne
* Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) artykułu i pełne hello **wymagań wstępnych** czynności.
* Postępuj zgodnie z instrukcjami wyświetlanymi w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu tooinstall najnowszą wersję programu Azure PowerShell na komputerze.
* (opcjonalnie) W tym artykule nie opisano wszystkich poleceń cmdlet fabryki danych hello. Pełna dokumentacja dotycząca poleceń cmdlet dla usługi Fabryka danych znajduje się w artykule [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) (Dokumentacja dotycząca poleceń cmdlet dla usługi Fabryka danych).

## <a name="create-data-factory"></a>Tworzenie fabryki danych
W tym kroku użyjesz programu Azure PowerShell toocreate fabryki danych Azure o nazwie **FirstDataFactoryPSH**. Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Na przykład dane wejściowe toocopy działanie kopiowania danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun tootransform skryptu Hive. Zacznijmy od utworzenia hello fabryki danych w tym kroku.

1. Uruchom program Azure PowerShell i uruchom następujące polecenie hello. Nie zamykaj programu Azure PowerShell do momentu zakończenia hello tego samouczka. Zamknij i otwórz ponownie, należy najpierw toorun tych poleceń ponownie.
   * Uruchom następujące polecenie hello, a następnie wprowadź hello nazwy użytkownika i hasła, użyj toosign w toohello portalu Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta.
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello. Ta subskrypcja powinien Witaj, taka sama, jak hello jedną używaną w hello portalu Azure.
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie hello:
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    Niektóre kroki hello w tym samouczku Załóżmy, że hello grupy zasobów o nazwie ADFTutorialResourceGroup. Jeśli używasz innej grupie zasobów, należy toouse go zamiast ADFTutorialResourceGroup w tym samouczku.
3. Uruchom hello **AzureRmDataFactory nowy** polecenie cmdlet tworzy fabrykę danych o nazwie **FirstDataFactoryPSH**.

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
Należy zwrócić uwagę hello następujące punkty:

* Nazwa Hello hello fabryki danych Azure musi być globalnie unikatowe. Jeśli wystąpi błąd hello **nazwa fabryki danych "FirstDataFactoryPSH" nie jest dostępna**, Zmień nazwę hello (na przykład yournameFirstDataFactoryPSH). Użyj tej nazwy zamiast ADFTutorialFactoryPSH podczas wykonywania kroków w tym samouczku. Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.
* toocreate wystąpienia fabryki danych, należy toobe współautora/administrator hello subskrypcji platformy Azure
* Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.
* Jeśli wystąpi błąd hello: "**Ta subskrypcja nie jest zarejestrowany toouse przestrzeni nazw Microsoft.DataFactory**", wykonaj jedną z następujących hello i spróbuj ponownie opublikować:

  * W programie Azure PowerShell Uruchom hello następujące polecenia tooregister hello fabryki danych dostawcy:

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      Powitania po tooconfirm polecenie można uruchomić tej fabryki danych w zarejestrowany dostawca hello:

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Logowanie przy użyciu hello subskrypcji platformy Azure do hello [portalu Azure](https://portal.azure.com) i przejdź do bloku usługi fabryka danych tooa tworzenie fabryki danych w hello portalu Azure (lub). Ta akcja rejestruje automatycznie hello dostawcy dla Ciebie.

Przed utworzeniem potoku, należy toocreate kilku jednostek fabryki danych najpierw. Najpierw utwórz danych toolink połączonych usług danych tooyour magazyny/oblicza przechowywania, zdefiniuj dane wejściowe i zestawów danych toorepresent wejścia/wyjścia dane w magazynach połączone dane wyjściowe, a następnie utwórz hello potoku do działania, która używa tych zestawów danych.

## <a name="create-linked-services"></a>Tworzenie połączonych usług
W tym kroku możesz połączyć konta magazynu Azure i fabrykę danych tooyour klastra Azure HDInsight na żądanie. blokady konta usługi Azure Storage Hello hello danych wejściowych i wyjściowych do potoku hello w tym przykładzie. Hello usługi HDInsight połączony jest używane toorun określony w działaniu hello hello potoku, w tym przykładzie skrypt Hive. Określenie, jakie dane magazynu/obliczeń usług są używane w danym scenariuszu i łączenie fabryki danych toohello tych usług za tworzenie połączonych usług.

### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage
W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu Azure. Użyj hello tego samego konta magazynu Azure toostore wejścia/wyjścia danych i hello HQL plik skryptu.

1. Utwórz plik JSON o nazwie StorageLinkedService.json w folderze C:\ADFGetStarted hello z powitania po zawartości. Utwórz hello folder ADFGetStarted, jeśli jeszcze nie istnieje.

    ```json
    {
        "name": "StorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "description": "",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
    }
    ```
    Zastąp **nazwa konta** hello nazwą konta magazynu Azure i **klucz konta** z klucz dostępu hello hello kontem magazynu platformy Azure. toolearn sposób dostępu do magazynu tooget klucza, zobacz hello informacji na temat sposobu tooview, kopiowania i regenerate magazynu dostępu do kluczy w [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
2. W programie Azure PowerShell przełącznika toohello ADFGetStarted folderu.
3. Można użyć hello **AzureRmDataFactoryLinkedService nowy** polecenie cmdlet tworzy połączonej usługi. To polecenie cmdlet i innych poleceń cmdlet z fabryki danych użycia w ramach tego samouczka wymaga wartości toopass dla hello *ResourceGroupName* i *DataFactoryName* parametrów. Alternatywnie można użyć **Get-AzureRmDataFactory** tooget **DataFactory** obiektu i przekazać obiekt hello bez wprowadzania *ResourceGroupName* i  *DataFactoryName* zawsze należy uruchomić polecenie cmdlet. Witaj uruchom następujące polecenie dane wyjściowe hello tooassign hello **Get-AzureRmDataFactory** tooa polecenia cmdlet **$df** zmiennej.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. Teraz uruchom hello **AzureRmDataFactoryLinkedService nowy** połączone polecenie cmdlet tworzy hello **StorageLinkedService** usługi.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    Jeżeli nie uruchomisz hello **Get-AzureRmDataFactory** toohello wyjściowe polecenia cmdlet i przypisane hello **$df** zmiennej, konieczne będzie toospecify wartości hello *ResourceGroupName*i *DataFactoryName* parametrów w następujący sposób.

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    Jeśli zamkniesz programu Azure PowerShell w środku hello samouczka hello masz toorun hello **Get-AzureRmDataFactory** polecenia cmdlet następnym uruchomieniu programu Azure PowerShell toocomplete hello samouczka.

### <a name="create-azure-hdinsight-linked-service"></a>Tworzenie połączonej usługi Azure HDInsight
W tym kroku możesz połączyć fabrykę danych tooyour klastra usługi HDInsight na żądanie. klaster usługi HDInsight Hello jest automatycznie tworzone w czasie wykonywania i usuwane po zakończeniu przetwarzania i bezczynności hello określoną ilość czasu. Możesz użyć własnego klastra usługi HDInsight zamiast klastra usługi HDInsight na żądanie. Szczegółowe informacje znajdują się w artykule [Compute Linked Services](data-factory-compute-linked-services.md) (Połączone usługi obliczeniowe).

1. Utwórz plik JSON o nazwie **HDInsightOnDemandLinkedService**JSON w hello **C:\ADFGetStarted** folder o powitania po zawartości.

    ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

   | Właściwość | Opis |
   |:--- |:--- |
   | ClusterSize |Określa rozmiar hello hello klastra usługi HDInsight. |
   | TimeToLive |Określa czas bezczynności tej hello hello klastra usługi HDInsight, przed usunięciem. |
   | linkedServiceName |Określa konto magazynu hello jest używany toostore hello dzienniki, generowanych przez usługi HDInsight |

    Należy zwrócić uwagę hello następujące punkty:

   * Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight za pomocą hello JSON. Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).
   * Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie. Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).
   * Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**). Po usunięciu klastra hello HDInsight nie usunie tego kontenera. To zachowanie jest celowe. W przypadku połączonej usługi HDInsight na żądanie klaster usługi HDInsight jest tworzony przy każdym przetwarzaniu wycinka — o ile w tym momencie nie istnieje aktywny klaster (**timeToLive**). klaster Hello są automatycznie usuwane po zakończeniu przetwarzania hello.

       Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów. Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów. nazwy Hello kontenery wykonaj wzorca: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.

     Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).
2. Uruchom hello **AzureRmDataFactoryLinkedService nowy** polecenie cmdlet tworzy hello połączona usługa o nazwie HDInsightOnDemandLinkedService.
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a>Tworzenie zestawów danych
W tym kroku utwórz wprowadzania hello toorepresent zestawów danych i wysyłania danych do przetwarzania Hive. Te zestawy danych można znaleźć toohello **StorageLinkedService** został utworzony we wcześniejszej części tego samouczka. Witaj tooan punktów połączonej usługi konta usługi Azure Storage i zestawów danych, określ kontener, folder, nazwa pliku w magazynie hello, która przechowuje dane wejściowe i wyjściowe danych.

### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych
1. Utwórz plik JSON o nazwie **InputTable.json** w hello **C:\ADFGetStarted** folder o hello następującej zawartości:

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    Witaj JSON definiuje zestaw danych o nazwie **AzureBlobInput**, który reprezentuje dane wejściowe dla działania w potoku hello. Ponadto określa ona, że danych wejściowych hello znajduje się w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **inputdata**.

    Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

   | Właściwość | Opis |
   |:--- |:--- |
   | type |Witaj właściwość type ma wartość tooAzureBlob, ponieważ dane znajdują się w magazynie obiektów blob platformy Azure. |
   | linkedServiceName |odwołuje się toohello StorageLinkedService utworzony wcześniej. |
   | fileName |Ta właściwość jest opcjonalna. W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki hello z hello folderPath. W takim przypadku tylko input.log hello jest przetwarzany. |
   | type |pliki dziennika Hello są w formacie tekstowym, więc używamy TextFormat. |
   | columnDelimiter |kolumn w plikach dziennika hello są rozdzielone znakiem hello przecinkami (,). |
   | frequency/interval |tooMonth Ustaw częstotliwość i interwał wynosi 1, co oznacza, że wejściowy wycinków hello są dostępne co miesiąc. |
   | external |Ta właściwość ma wartość tootrue, jeśli dane wejściowe hello nie jest generowany przez hello usługi fabryka danych. |
2. Uruchom następujące polecenie w środowiska Azure PowerShell toocreate hello fabryki danych w zestawie danych hello:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a>Tworzenie wyjściowego zestawu danych
Można teraz utworzyć hello wyjściowego zestawu danych toorepresent hello danych wyjściowych danych przechowywanych w hello magazynu obiektów Blob platformy Azure.

1. Utwórz plik JSON o nazwie **OutputTable.json** w hello **C:\ADFGetStarted** folder o hello następującej zawartości:

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    Witaj JSON definiuje zestaw danych o nazwie **AzureBlobOutput**, który reprezentuje danych wyjściowych dla działania w potoku hello. Ponadto określa ona, że wyniki hello są przechowywane w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **partitioneddata**. Witaj **dostępności** sekcja określa, że wyjściowy zestaw danych hello jest tworzony co miesiąc.
2. Uruchom następujące polecenie w środowiska Azure PowerShell toocreate hello fabryki danych w zestawie danych hello:

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a>Tworzenie potoku
W tym kroku opisano tworzenie pierwszego potoku za pomocą działania **HDInsightHive**. Wejściowy jest dostępny co miesiąc (częstotliwość: miesiąc, interwał: 1), wycinek danych wyjściowych jest tworzony co miesiąc, a właściwość harmonogramu hello działania hello jest ustawić toomonthly. Ustawienia Hello hello wyjściowego zestawu danych i harmonogram działania hello muszą być zgodne. Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu, dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku. Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello. na końcu hello w tej sekcji opisano Hello właściwości używane w hello następującego formatu JSON.

1. Utwórz plik JSON o nazwie MyFirstPipelinePSH.json w folderze C:\ADFGetStarted hello z powitania po zawartości:

   > [!IMPORTANT]
   > Zastąp **storageaccountname** hello nazwą konta magazynu w hello JSON.
   >
   >

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "StorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```
    We fragmencie JSON hello tworzysz potok, który składa się z jednego działania używającej tooprocess Hive danych w klastrze usługi HDInsight.

    plik skryptu Hive Hello, **partitionweblogs.hql**, są przechowywane w hello kontem magazynu platformy Azure (określonego przez element scriptLinkedService hello, nazywany **StorageLinkedService**) i w **skryptu**  folderu w kontenerze hello **adfgetstarted**.

    Hello **definiuje** sekcja jest używane toospecify hello środowiska uruchomieniowego ustawień, które można przekazać skryptu hive toohello jako wartości konfiguracji gałąź (np. ${hiveconf: inputtable}, ${hiveconf:partitionedtable}).

    Witaj **start** i **zakończenia** hello aktywny okres potoku hello określa właściwości hello potoku.

    W działaniu hello JSON, możesz określić, tego skryptu Hive hello zostanie uruchomiona na określony przez hello obliczeń hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.

   > [!NOTE]
   > Zobacz sekcję "JSON potoku" w [potoki i działań w fabryce danych Azure](data-factory-create-pipelines.md) szczegółowe informacje na temat właściwości JSON, które są używane w przykładzie hello.

2. Upewnij się, że widoczny hello **input.log** pliku w hello **adfgetstarted/inputdata** folderu w hello magazynu obiektów blob platformy Azure i hello uruchom następujące polecenie toodeploy hello potoku. Ponieważ hello **start** i **zakończenia** czasy są ustawiane w przeszłości hello i **isPaused** jest zestaw toofalse, potoku hello (działania w potoku hello) uruchamia natychmiast po wdrożeniu.

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. Gratulacje! Udało Ci się utworzyć pierwszy potok przy użyciu programu Azure PowerShell!

## <a name="monitor-pipeline"></a>Monitorowanie potoku
W tym kroku użyjesz programu Azure PowerShell toomonitor co się dzieje w fabryce danych Azure.

1. Uruchom **Get-AzureRmDataFactory** i przypisz hello dane wyjściowe tooa **$df** zmiennej.

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. Uruchom **Get-AzureRmDataFactorySlice** tooget szczegóły wszystkie fragmenty hello **EmpSQLTable**, która jest tabela wyjściowa hello hello potoku.

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    Należy zauważyć, że hello StartDateTime określone w tym miejscu jest hello sam określono godzinę rozpoczęcia w potoku hello JSON. Oto hello przykładowe dane wyjściowe:

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. Uruchom **Get-AzureRmDataFactoryRun** tooget hello szczegółów działania jest uruchamiana dla określonych wycinka.

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    Oto hello przykładowe dane wyjściowe: 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    Możesz można zachować uruchomienie tego polecenia cmdlet do momentu wyświetlenia wycinek hello **gotowe** stanu lub **** stanu. Gdy wycinek hello jest w stanie gotowe, sprawdź hello **partitioneddata** folderu w hello **adfgetstarted** kontenera w magazynie obiektów blob na powitania dane wyjściowe.  Tworzenie klastra usługi HDInsight na żądanie zwykle zajmuje trochę czasu.

    ![Dane wyjściowe](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut). W związku z tym spodziewać się hello potoku tootake **około 30 minut** tooprocess hello wycinka.
>
> Plik wejściowy Hello zostaje usunięta, gdy hello wycinek jest przetwarzany pomyślnie. W związku z tym hello plik wejściowy (input.log) toohello inputdata folder kontenera adfgetstarted hello przekazywania wycinek hello toorerun lub Witaj ponownie samouczek.
>
>

## <a name="summary"></a>Podsumowanie
W tym samouczku danych tooprocess fabryki danych Azure została utworzona przez uruchomienie skryptu Hive w klastrze HDInsight hadoop. Użyto hello Edytor fabryki danych w hello Azure toodo portalu hello następujące kroki:

1. Tworzenie **fabryki danych** Azure.
2. Utworzyć dwie **połączone usługi**:
   1. **Usługa Azure Storage** połączone usługi toolink Twojego magazynu Azure blob storage przechowuje pliki danych wejściowych/wyjściowych toohello usługi fabryka danych.
   2. **Usługa Azure HDInsight** na żądanie połączone usługi toolink fabrykę danych toohello klastra usługi HDInsight Hadoop na żądanie. Fabryka danych Azure tworzy HDInsight Hadoop dane wejściowe w czasie tooprocess klastra i danych wyjściowych produktu.
3. Utworzone dwie **zestawów danych**, które opisują danych wejściowych i wyjściowych dla działania HDInsight Hive w potoku hello.
4. Utworzyć **potok** za pomocą działania **programu Hive w usłudze HDInsight**.

## <a name="next-steps"></a>Następne kroki
W tym artykule opisano tworzenie potoku za pomocą działania przekształcania (działanie usługi HDInsight), które uruchamia skrypt programu Hive w klastrze usługi HDInsight platformy Azure na żądanie. toosee toouse toocopy działanie kopiowania danych z tooAzure obiektów Blob platformy Azure SQL, zobacz temat [samouczek: kopiowanie danych z obiektu Blob Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="see-also"></a>Zobacz też
| Temat | Opis |
|:--- |:--- |
| [Dokumentacja dotycząca poleceń cmdlet usługi Data Factory](/powershell/module/azurerm.datafactories) |Zobacz pełną dokumentację dotyczącą poleceń cmdlet w usłudze Fabryka danych. |
| [Potoki](data-factory-create-pipelines.md) |Ten artykuł pomaga w zrozumieniu potoki i działań w fabryce danych Azure i w jaki sposób toouse ich tooconstruct end-to-end danymi przepływy pracy dla Twojego scenariusza lub firmy. |
| [Zestawy danych](data-factory-create-datasets.md) |Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory. |
| [Planowanie i wykonywanie](data-factory-scheduling-and-execution.md) |W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji fabryki danych Azure. |
| [Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania](data-factory-monitor-manage-app.md) |W tym artykule opisano sposób toomonitor, zarządzania i debugowania potoki przy użyciu hello monitorowanie & aplikacji do zarządzania. |
