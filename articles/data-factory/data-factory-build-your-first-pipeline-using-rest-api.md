---
title: aaaBuild pierwszy fabryki danych (REST) | Dokumentacja firmy Microsoft
description: "W tym samouczku przedstawiono instrukcje tworzenia przykładowego potoku usługi Azure Data Factory przy użyciu interfejsu API REST usługi Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a>Samouczek: Tworzenie pierwszej fabryki danych Azure przy użyciu interfejsu API REST usługi Fabryka danych
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-build-your-first-pipeline.md)
> * [Witryna Azure Portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Program Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [Program PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Szablon usługi Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [Interfejs API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


W tym artykule Użyj interfejsu API REST fabryki danych toocreate Twojego pierwszego fabryki danych Azure. Samouczek hello toodo przy użyciu innych narzędzi/SDK, wybierz jedną z opcji hello z listy rozwijanej hello.

Witaj potoku, w tym samouczku ma jedno działanie: **działania HDInsight Hive**. To działanie uruchamia skrypt hive w klastrze Azure HDInsight czy transformacji wejściowych danych wyjściowych tooproduce danych. potok Hello jest zaplanowane toorun po miesiącu między hello określono godziny rozpoczęcia i zakończenia.

> [!NOTE]
> W tym artykule nie opisano wszystkich hello interfejsu API REST. Pełna dokumentacja dotycząca interfejsu API REST znajduje się w [Dokumentacji interfejsu API REST usługi Data Factory](/rest/api/datafactory/).
> 
> Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Więcej informacji znajduje się w artykule dotyczącym [planowania i wykonywania w usłudze Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="prerequisites"></a>Wymagania wstępne
* Zapoznaj się z artykułem [— samouczek Przegląd](data-factory-build-your-first-pipeline.md) artykułu i pełne hello **wymagań wstępnych** czynności.
* Zainstaluj na komputerze narzędzie [Curl](https://curl.haxx.se/dlwiz/). Narzędzie CURL hello jest używany z toocreate polecenia REST fabryki danych.
* Postępuj zgodnie z instrukcjami zawartymi w [tym artykule](../azure-resource-manager/resource-group-create-service-principal-portal.md), aby wykonać następujące czynności:
  1. Utworzenie aplikacji sieci Web o nazwie **ADFGetStartedApp** w usłudze Azure Active Directory.
  2. Pobranie **identyfikatora klienta** i **klucza tajnego**.
  3. Uzyskanie **identyfikatora dzierżawy**.
  4. Przypisz hello **ADFGetStartedApp** toohello aplikacji **współautora fabryki danych** roli.
* Zainstaluj program [Azure PowerShell](/powershell/azure/overview).
* Uruchom **PowerShell** i hello uruchom następujące polecenie. Nie zamykaj programu Azure PowerShell do momentu zakończenia hello tego samouczka. Zamknij i otwórz ponownie, należy najpierw polecenia hello toorun ponownie.
  1. Uruchom **Login-AzureRmAccount** , a następnie wprowadź hello nazwy użytkownika i hasła, użyj toosign w toohello portalu Azure.
  2. Uruchom **Get-AzureRmSubscription** tooview hello wszystkie subskrypcje dla tego konta.
  3. Uruchom **NameOfAzureSubscription Nazwa subskrypcji - Get-AzureRmSubscription | Set-AzureRmContext** tooselect hello subskrypcji, która ma toowork z. Zastąp **NameOfAzureSubscription** o nazwie hello subskrypcji platformy Azure.
* Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie w środowiska PowerShell hello hello:

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   Niektóre kroki hello w tym samouczku Załóżmy, że hello grupy zasobów o nazwie ADFTutorialResourceGroup. Jeśli używasz innej grupie zasobów, należy toouse hello Nazwa grupy zasobów, zamiast ADFTutorialResourceGroup w tym samouczku.

## <a name="create-json-definitions"></a>Tworzenie definicji JSON
Utwórz następujące pliki w folderze hello, w którym znajduje się curl.exe w formacie JSON.

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Nazwa musi być unikatowe globalnie, dlatego może być toomake ADFCopyTutorialDF tooprefix/sufiksu go unikatową nazwę.
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Zastąp wartości **accountname** i **accountkey** nazwą konta usługi Azure Storage oraz jego kluczem. toolearn sposób dostępu do magazynu tooget klucza, zobacz hello informacji na temat sposobu tooview, kopiowania i regenerate magazynu dostępu do kluczy w [Zarządzanie kontem magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).
>
>

```JSON
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

### <a name="hdinsightondemandlinkedservicejson"></a>hdinsightondemandlinkedservice.json

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

| Właściwość | Opis |
|:--- |:--- |
| ClusterSize |Rozmiar klastra usługi HDInsight hello. |
| TimeToLive |Określa czas bezczynności tej hello hello klastra usługi HDInsight, przed usunięciem. |
| linkedServiceName |Określa konto magazynu hello jest używany toostore hello dzienniki, generowanych przez usługi HDInsight |

Należy zwrócić uwagę hello następujące punkty:

* Witaj fabryki danych tworzy **opartych na systemie Linux** klastra usługi HDInsight za pomocą hello powyżej JSON. Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).
* Możesz użyć **własnego klastra usługi HDInsight** zamiast klastra usługi HDInsight na żądanie. Szczegółowe informacje znajdują się w artykule [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) (Połączona usługa HDInsight).
* Tworzy klaster usługi HDInsight Hello **domyślny kontener** w magazynie obiektów blob hello określone w hello JSON (**linkedServiceName**). Po usunięciu klastra hello HDInsight nie usunie tego kontenera. To zachowanie jest celowe. Z usługą HDInsight połączony na żądanie, tworzenia klastra usługi HDInsight za każdym razem, gdy wycinek jest przetwarzany, chyba że istnieje istniejącego klastra na żywo (**timeToLive**) i zostaną usunięte po zakończeniu przetwarzania hello.

    Po przetworzeniu większej liczby wycinków w usłudze Azure Blob Storage będzie widocznych wiele kontenerów. Jeśli nie ma potrzeby do rozwiązywania problemów hello zadań, możesz toodelete ich magazynu hello tooreduce kosztów. nazwy Hello kontenery wykonaj wzorca: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Użyj narzędzia takiego jak [Eksploratora magazynu](http://storageexplorer.com/) magazynu obiektów blob toodelete kontenerów w platformy Azure.

Szczegółowe informacje znajdują się w artykule [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) (Połączona usługa HDInsight na żądanie).

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
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

Witaj JSON definiuje zestaw danych o nazwie **AzureBlobInput**, który reprezentuje dane wejściowe dla działania w potoku hello. Ponadto określa ona, że danych wejściowych hello znajduje się w kontenerze obiektów blob hello o nazwie **adfgetstarted** i hello folder o nazwie **inputdata**.

Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

| Właściwość | Opis |
|:--- |:--- |
| type |Witaj właściwość type ma wartość tooAzureBlob, ponieważ dane znajdują się w magazynie obiektów blob platformy Azure. |
| linkedServiceName |odwołuje się toohello StorageLinkedService utworzony wcześniej. |
| fileName |Ta właściwość jest opcjonalna. W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki hello z hello folderPath. W takim przypadku tylko input.log hello jest przetwarzany. |
| type |pliki dziennika Hello są w formacie tekstowym, więc używamy TextFormat. |
| columnDelimiter |kolumn w plikach dziennika hello są rozdzielone znakiem przecinkami () |
| frequency/interval |tooMonth Ustaw częstotliwość i interwał wynosi 1, co oznacza, że wejściowy wycinków hello są dostępne co miesiąc. |
| external |Ta właściwość ma wartość tootrue, jeśli dane wejściowe hello nie jest generowany przez hello usługi fabryka danych. |

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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

### <a name="pipelinejson"></a>pipeline.json
> [!IMPORTANT]
> Zastąp wartość **storageaccountname** nazwą konta usługi Azure Storage.
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

We fragmencie JSON hello tworzysz potok, który składa się z jednego działania, który używa danych tooprocess gałęzi w klastrze usługi HDInsight.

plik skryptu Hive Hello, **partitionweblogs.hql**, są przechowywane w hello kontem magazynu platformy Azure (określonego przez element scriptLinkedService hello, nazywany **StorageLinkedService**) i w **skryptu**  folderu w kontenerze hello **adfgetstarted**.

Witaj **definiuje** sekcji określa ustawienia środowiska uruchomieniowego, które są przekazywane skryptu hive toohello jako wartości konfiguracji gałąź (np. ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).

Witaj **start** i **zakończenia** hello aktywny okres potoku hello określa właściwości hello potoku.

W działaniu hello JSON, możesz określić, tego skryptu Hive hello zostanie uruchomiona na określony przez hello obliczeń hello **linkedServiceName** — **HDInsightOnDemandLinkedService**.

> [!NOTE]
> Zobacz sekcję "JSON potoku" w [potoki i działań w fabryce danych Azure](data-factory-create-pipelines.md) szczegółowe informacje na temat właściwości JSON używane w hello poprzedzających przykład.
>
>

## <a name="set-global-variables"></a>Ustawianie zmiennych globalnych
W programie Azure PowerShell wykonaj następujące polecenia, po zastąpieniu hello wartości własnymi hello:

> [!IMPORTANT]
> Zobacz sekcję [Wymagania wstępne](#prerequisites), aby uzyskać instrukcje dotyczące pobierania identyfikatora klienta, klucza tajnego klienta, identyfikatora dzierżawy oraz identyfikatora subskrypcji.
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a>Uwierzytelnianie przy użyciu usługi AAD

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a>Tworzenie fabryki danych
W tym kroku opisano tworzenie fabryki danych Azure o nazwie **FirstDataFactoryREST**. Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Na przykład działanie kopiowania toocopy danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun danych tootransform skryptu Hive. Uruchom powitania po fabryki danych hello toocreate polecenia:

1. Przypisz hello toovariable polecenia o nazwie **cmd**.

    Potwierdzić tę nazwę hello hello fabryki danych określone w tym miejscu (ADFCopyTutorialDF) dopasowań hello nazwa określona w hello **datafactory.json**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. Uruchom polecenie hello przy użyciu **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Wyświetl wyniki hello. Po pomyślnym utworzeniu hello fabryki danych Zobacz hello JSON dla fabryki danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.

    ```PowerShell
    Write-Host $results
    ```

Należy zwrócić uwagę hello następujące punkty:

* Nazwa Hello hello fabryki danych Azure musi być globalnie unikatowe. Jeśli zostanie wyświetlony błąd hello w wynikach: **nazwa fabryki danych "FirstDataFactoryREST" nie jest dostępna**, hello następujące kroki:
  1. Zmień nazwę hello (na przykład yournameFirstDataFactoryREST) w hello **datafactory.json** pliku. Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.
  2. W pierwszym poleceniem hello gdzie hello **$cmd** zmiennej jest przypisywana wartość, Zamień FirstDataFactoryREST hello nowej nazwy i uruchom polecenie hello.
  3. Uruchamianie hello następne dwa polecenia tooinvoke hello interfejsu API REST toocreate hello danych fabryki i Drukuj hello wyników hello operacji.
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

Przed utworzeniem potoku, należy toocreate kilku jednostek fabryki danych najpierw. Najpierw utwórz danych toolink połączonych usług danych tooyour magazyny/oblicza przechowywania, zdefiniuj dane wejściowe i zestawów danych toorepresent dane w magazynach połączone dane wyjściowe.

## <a name="create-linked-services"></a>Tworzenie połączonych usług
W tym kroku możesz połączyć konta magazynu Azure i fabrykę danych tooyour klastra Azure HDInsight na żądanie. blokady konta usługi Azure Storage Hello hello danych wejściowych i wyjściowych do potoku hello w tym przykładzie. Hello usługi HDInsight połączony jest używane toorun określony w działaniu hello hello potoku, w tym przykładzie skrypt Hive.

### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage
W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu Azure. Z tego samouczka użyjesz hello tego samego konta magazynu Azure toostore wejścia/wyjścia danych i hello HQL plik skryptu.

1. Przypisz hello toovariable polecenia o nazwie **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Uruchom polecenie hello przy użyciu **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Wyświetl wyniki hello. Jeśli hello połączone usługi został utworzony pomyślnie, zobacz hello JSON usługi hello połączone w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a>Tworzenie połączonej usługi Azure HDInsight
W tym kroku możesz połączyć fabrykę danych tooyour klastra usługi HDInsight na żądanie. klaster usługi HDInsight Hello jest automatycznie tworzone w czasie wykonywania i usuwane po zakończeniu przetwarzania i bezczynności hello określoną ilość czasu. Możesz użyć własnego klastra usługi HDInsight zamiast klastra usługi HDInsight na żądanie. Szczegółowe informacje znajdują się w artykule [Compute Linked Services](data-factory-compute-linked-services.md) (Połączone usługi obliczeniowe).

1. Przypisz hello toovariable polecenia o nazwie **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. Uruchom polecenie hello przy użyciu **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Wyświetl wyniki hello. Jeśli hello połączone usługi został utworzony pomyślnie, zobacz hello JSON usługi hello połączone w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Tworzenie zestawów danych
W tym kroku utwórz wprowadzania hello toorepresent zestawów danych i wysyłania danych do przetwarzania Hive. Te zestawy danych można znaleźć toohello **StorageLinkedService** został utworzony we wcześniejszej części tego samouczka. Witaj tooan punktów połączonej usługi konta usługi Azure Storage i zestawów danych, określ kontener, folder, nazwa pliku w magazynie hello, która przechowuje dane wejściowe i wyjściowe danych.

### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych
W tym kroku utworzysz hello wejściowy zestaw danych toorepresent danych wejściowych przechowywanych w magazynie obiektów Blob platformy Azure hello.

1. Przypisz hello toovariable polecenia o nazwie **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Uruchom polecenie hello przy użyciu **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Wyświetl wyniki hello. Po pomyślnym utworzeniu zestawu danych hello Zobacz hello JSON dla zestawu danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Tworzenie wyjściowego zestawu danych
W tym kroku utworzysz hello wyjściowego zestawu danych toorepresent danych wyjściowych danych przechowywanych w hello magazynu obiektów Blob platformy Azure.

1. Przypisz hello toovariable polecenia o nazwie **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. Uruchom polecenie hello przy użyciu **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Wyświetl wyniki hello. Po pomyślnym utworzeniu zestawu danych hello Zobacz hello JSON dla zestawu danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a>Tworzenie potoku
W tym kroku opisano tworzenie pierwszego potoku za pomocą działania **HDInsightHive**. Wejściowy jest dostępny co miesiąc (częstotliwość: miesiąc, interwał: 1), wycinek danych wyjściowych jest tworzony co miesiąc, a właściwość harmonogramu hello działania hello jest ustawić toomonthly. Ustawienia Hello hello wyjściowego zestawu danych i harmonogram działania hello muszą być zgodne. Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu, dlatego należy utworzyć wyjściowy zestaw danych, nawet wtedy, gdy działanie hello nie generuje żadnego wyniku. Jeśli działanie hello nie przyjmuje żadnych danych, możesz pominąć tworzenie zestawu danych wejściowych hello.

Upewnij się, że widoczny hello **input.log** pliku w hello **adfgetstarted/inputdata** folderu w hello magazynu obiektów blob platformy Azure i hello uruchom następujące polecenie toodeploy hello potoku. Ponieważ hello **start** i **zakończenia** czasy są ustawiane w przeszłości hello i **isPaused** jest zestaw toofalse, potoku hello (działania w potoku hello) uruchamia natychmiast po wdrożeniu.

1. Przypisz hello toovariable polecenia o nazwie **cmd**.

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Uruchom polecenie hello przy użyciu **Invoke-Command**.

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Wyświetl wyniki hello. Po pomyślnym utworzeniu zestawu danych hello Zobacz hello JSON dla zestawu danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.

    ```PowerShell
    Write-Host $results
    ```
4. Gratulacje! Udało Ci się utworzyć pierwszy potok przy użyciu programu Azure PowerShell!

## <a name="monitor-pipeline"></a>Monitorowanie potoku
W tym kroku użyjesz tworzonym przez potok hello wycinków toomonitor interfejsu API REST fabryki danych.

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> Tworzenie klastra usługi HDInsight na żądanie zwykle trwa trochę czasu (około 20 minut). W związku z tym spodziewać się hello potoku tootake **około 30 minut** tooprocess hello wycinka.
>
>

Uruchom hello Invoke-Command i hello kolejnego do momentu wyświetlenia wycinek hello **gotowe** stanu lub **** stanu. Gdy wycinek hello jest w stanie gotowe, sprawdź hello **partitioneddata** folderu w hello **adfgetstarted** kontenera w magazynie obiektów blob na powitania dane wyjściowe.  Tworzenie klastra usługi HDInsight na żądanie Hello zazwyczaj trwa trochę czasu.

![Dane wyjściowe](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> Plik wejściowy Hello zostaje usunięta, gdy hello wycinek jest przetwarzany pomyślnie. W związku z tym hello plik wejściowy (input.log) toohello inputdata folder kontenera adfgetstarted hello przekazywania wycinek hello toorerun lub Witaj ponownie samouczek.
>
>

Można również użyć wycinków toomonitor portalu Azure i rozwiązać wszelkie napotkane problemy. Aby poznać szczegóły, zapoznaj się z informacjami dotyczącymi [monitorowania potoków w witrynie Azure Portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).

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
| [Dokumentacja interfejsu API REST usługi Data Factory](/rest/api/datafactory/) |Zobacz pełną dokumentację dotyczącą poleceń cmdlet w usłudze Fabryka danych. |
| [Potoki](data-factory-create-pipelines.md) |Ten artykuł pomaga w zrozumieniu potoki i działań w fabryce danych Azure i w jaki sposób toouse ich tooconstruct end-to-end danymi przepływy pracy dla Twojego scenariusza lub firmy. |
| [Zestawy danych](data-factory-create-datasets.md) |Ten artykuł ułatwia zapoznanie się z zestawami danych w usłudze Azure Data Factory. |
| [Planowanie i wykonywanie](data-factory-scheduling-and-execution.md) |W tym artykule opisano aspekty planowania i wykonywania hello modelu aplikacji fabryki danych Azure. |
| [Monitorowanie potoków i zarządzanie nimi za pomocą aplikacji do monitorowania](data-factory-monitor-manage-app.md) |W tym artykule opisano sposób toomonitor, zarządzania i debugowania potoki przy użyciu hello monitorowanie & aplikacji do zarządzania. |
