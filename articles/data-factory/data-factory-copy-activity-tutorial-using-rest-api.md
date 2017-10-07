---
title: "Samouczek: Użyj interfejsu API REST toocreate potoku fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "W tym samouczku należy użyć interfejsu API REST toocreate potoku fabryki danych Azure z toocopy działanie kopiowania danych z magazynu obiektów blob platformy Azure bazy danych Azure SQL."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a>Samouczek: Użyj interfejsu API REST toocreate danych toocopy potoku fabryki danych Azure 
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kreator kopiowania](data-factory-copy-data-wizard-tutorial.md)
> * [Witryna Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Program Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [Program PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Szablon usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [Interfejs API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [Interfejs API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

W tym artykule dowiesz się, jak toouse REST API toocreate fabryki danych z potok, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure. Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł przed wykonaniem tego samouczka.   

W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania). działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane. Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności. Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).

Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> W tym artykule nie opisano wszystkich hello interfejsu API REST fabryki danych. Pełna dokumentacja dotycząca poleceń cmdlet usługi Data Factory znajduje się w artykule [Data Factory Cmdlet Reference](/rest/api/datafactory/) (Dokumentacja dotycząca interfejsu API REST usługi Data Factory).
>  
> Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego. Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Wymagania wstępne
* Przejdź przez [— samouczek Przegląd](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) i pełne hello **wymagań wstępnych** czynności.
* Zainstaluj na komputerze narzędzie [Curl](https://curl.haxx.se/dlwiz/). Narzędzie Curl hello jest używany z toocreate polecenia REST fabryki danych. 
* Postępuj zgodnie z instrukcjami zawartymi w [tym artykule](../azure-resource-manager/resource-group-create-service-principal-portal.md), aby wykonać następujące czynności: 
  1. Utworzenie aplikacji sieci Web o nazwie **ADFCopyTutorialApp** w usłudze Azure Active Directory.
  2. Pobranie **identyfikatora klienta** i **klucza tajnego**. 
  3. Uzyskanie **identyfikatora dzierżawy**. 
  4. Przypisz hello **ADFCopyTutorialApp** toohello aplikacji **współautora fabryki danych** roli.  
* Zainstaluj program [Azure PowerShell](/powershell/azure/overview).  
* Uruchom **PowerShell** i hello następujące kroki. Nie zamykaj programu Azure PowerShell do momentu zakończenia hello tego samouczka. Zamknij i otwórz ponownie, należy najpierw polecenia hello toorun ponownie.
  
  1. Uruchom następujące polecenie hello i wprowadź hello nazwę użytkownika i hasło, użyj toosign w toohello portalu Azure:
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta:

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello. Zastąp  **&lt;NameOfAzureSubscription** &gt; o nazwie hello subskrypcji platformy Azure. 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie w środowiska PowerShell hello hello:  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      Jeśli hello grupy zasobów już istnieje, określić czy tooupdate go (Y) lub zachować go jako (N). 
     
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
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Zastąp wartości **accountname** i **accountkey** nazwą konta usługi Azure Storage oraz jego kluczem. toolearn jak tooget Twojego magazynu uzyskują dostęp do klucza, zobacz [widoku, kopiowania i regenerate magazynu klucze dostępu](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).

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

Aby uzyskać więcej informacji o właściwościach JSON, zobacz temat dotyczący [połączonej usługi Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service).

### <a name="azuersqllinkedservicejson"></a>azuersqllinkedservice.json
> [!IMPORTANT]
> Zastąp **servername**, **databasename**, **username**, i **hasło** z nazwą swojego serwera Azure SQL, nazwa bazy danych SQL, użytkownika Konto i hasło dla konta hello.  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Aby uzyskać szczegółowe informacje o właściwościach JSON, zobacz temat dotyczący [połączonej usługi Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "AzureStorageLinkedService",
    "typeProperties": {
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ","
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

| Właściwość | Opis |
|:--- |:--- |
| type | Właściwość type Hello ustawiono zbyt**AzureBlob** ponieważ danych znajduje się w magazynie obiektów blob platformy Azure. |
| linkedServiceName | Odwołuje się toohello **AzureStorageLinkedService** utworzony wcześniej. |
| folderPath | Określa obiekt blob hello **kontenera** i hello **folderu** zawiera obiekty BLOB wejściowego. W tym samouczku adftutorial jest hello kontenera obiektów blob i hello folderu głównego. | 
| fileName | Ta właściwość jest opcjonalna. W przypadku pominięcia tej właściwości, pobierane są wszystkie pliki z hello folderPath. W tym samouczku **emp.txt** określona dla hello nazwę pliku, tak aby plik zostaje pobrana do przetwarzania. |
| format -> type |Plik wejściowy Hello jest w formacie tekstowym hello, więc używamy **TextFormat**. |
| columnDelimiter | Witaj kolumn w pliku wejściowym hello są rozdzielane **przecinka (`,`)**. |
| frequency/interval | częstotliwość Hello ustawiono zbyt**godzina** i interwał jest ustawiany za**1**, co oznacza, że hello wejściowych dostępnych wycinków **co godzinę**. Innymi słowy, hello usługi fabryka danych sprawdza dane wejściowe co godzinę w folderze głównym hello kontenera obiektów blob (**adftutorial**) określone. Wyszukuje hello danych w ramach hello potoku rozpoczęcia i zakończenia godzin, nie przed lub po tych godzinach.  |
| external | Ta właściwość jest ustawiona zbyt**true** czy hello danych nie jest generowany przez tego potoku. Witaj danych wejściowych w tym samouczku jest hello emp.txt pliku, który nie jest generowany w tym potoku, możemy ustawić tootrue tej właściwości. |

Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika obiektu blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "emp"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
Witaj Poniższa tabela zawiera opisy właściwości JSON hello używane we fragmencie hello:

| Właściwość | Opis |
|:--- |:--- |
| type | Właściwość type Hello ustawiono zbyt**AzureSqlTable** , ponieważ dane są kopiowane tooa tabeli w bazie danych Azure SQL. |
| linkedServiceName | Odwołuje się toohello **AzureSqlLinkedService** utworzony wcześniej. |
| tableName | Określony hello **tabeli** toowhich hello dane są kopiowane. | 
| frequency/interval | Witaj częstotliwość ustawiono zbyt**godzina** i interwał **1**, co oznacza, że wycinki danych wyjściowych hello są produkowane **co godzinę** między hello potoku rozpoczęcia i zakończenia godzin przed nie lub Po tych godzinach.  |

Istnieją trzy kolumny — **identyfikator**, **imię**, i **nazwisko** — Witaj pustych elementów tabeli w bazie danych hello. Identyfikator jest kolumny tożsamości, więc musisz tylko toospecify **imię** i **nazwisko** tutaj.

Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika usługi Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).

### <a name="pipelinejson"></a>pipeline.json

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

Należy zwrócić uwagę hello następujące punkty:

- W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**. Aby uzyskać więcej informacji o działaniu kopiowania hello, zobacz [działań przepływu danych](data-factory-data-movement-activities.md). W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).
- Dane wejściowe dla działania hello jest ustawiony za**AzureBlobInput** i danych wyjściowych dla działania hello jest ustawiony za**AzureSqlOutput**. 
- W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello. Aby uzyskać pełną listę obsługiwanych przez działanie kopiowania hello jako źródła i wychwytywanie magazyny danych, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn jak przechowywać toouse określonych danych obsługiwane jako źródło/ujście, kliknij łącze hello hello tabeli.  
 
Zastąp wartość hello hello **start** właściwość o hello bieżącego dnia i **zakończenia** wartości z hello następnego dnia. Można określić tylko część daty hello i Pomiń hello czas część hello Data i godzina. Na przykład "2017-02-03", która odpowiada za "2017-02-03T00:00:00Z"
 
Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Przykładowo: 2016-10-14T16:32:41Z. Witaj **zakończenia** czasu jest opcjonalne, ale możemy użyć w tym samouczku. 
 
Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin**". potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości.
 
W hello poprzedzających przykład istnieją 24 wycinków danych, jak każdy wycinek danych jest tworzone co godzinę.

Opisy właściwości JSON w definicji potoku znajdują się w artykule dotyczącym [tworzenia potoków](data-factory-create-pipelines.md). Opisy właściwości JSON w definicji działania kopiowania znajdują się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md). Opisy właściwości JSON obsługiwanych przez BlobSource można znaleźć w [artykule dotyczącym łącznika usługi Azure Blob](data-factory-azure-blob-connector.md). Opisy właściwości JSON obsługiwanych przez SqlSink można znaleźć w artykule [dotyczącym łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md).

## <a name="set-global-variables"></a>Ustawianie zmiennych globalnych
W programie Azure PowerShell wykonaj następujące polecenia, po zastąpieniu hello wartości własnymi hello:

> [!IMPORTANT]
> Zobacz sekcję [Wymagania wstępne](#prerequisites), aby uzyskać instrukcje dotyczące pobierania identyfikatora klienta, klucza tajnego klienta, identyfikatora dzierżawy oraz identyfikatora subskrypcji.   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

Uruchom następujące polecenia, po zaktualizowaniu hello nazwa fabryki danych hello, którego używasz hello: 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>Uwierzytelnianie przy użyciu usługi AAD
Witaj uruchom następujące polecenie tooauthenticate usłudze Azure Active Directory (AAD): 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>Tworzenie fabryki danych
W tym kroku opisano tworzenie fabryki danych Azure o nazwie **ADFCopyTutorialDF**. Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Na przykład działanie kopiowania toocopy magazynu danych, z docelowym tooa źródła danych. HDInsight Hive działania toorun tootransform skryptu Hive wejściowe dane wyjściowe tooproduct danych. Uruchom powitania po fabryki danych hello toocreate polecenia: 

1. Przypisz hello toovariable polecenia o nazwie **cmd**. 
   
    > [!IMPORTANT]
    > Potwierdzić tę nazwę hello hello fabryki danych określone w tym miejscu (ADFCopyTutorialDF) dopasowań hello nazwa określona w hello **datafactory.json**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. Uruchom polecenie hello przy użyciu **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Wyświetl wyniki hello. Po pomyślnym utworzeniu hello fabryki danych Zobacz hello JSON dla fabryki danych hello w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.  
   
    ```
    Write-Host $results
    ```

Należy zwrócić uwagę hello następujące punkty:

* Nazwa Hello hello fabryki danych Azure musi być globalnie unikatowe. Jeśli zostanie wyświetlony błąd hello w wynikach: **nazwa fabryki danych "ADFCopyTutorialDF" nie jest dostępna**, hello następujące kroki:  
  
  1. Zmień nazwę hello (na przykład yournameADFCopyTutorialDF) w hello **datafactory.json** pliku.
  2. W pierwszym poleceniem hello gdzie hello **$cmd** zmiennej jest przypisywana wartość, Zamień ADFCopyTutorialDF hello nowej nazwy i uruchom polecenie hello. 
  3. Uruchamianie hello następne dwa polecenia tooinvoke hello interfejsu API REST toocreate hello danych fabryki i Drukuj hello wyników hello operacji. 
     
     Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.
* toocreate wystąpienia fabryki danych, należy toobe współautora/administrator hello subskrypcji platformy Azure
* Nazwa fabryki danych hello Hello mogą być zarejestrowana jako nazwa DNS w przyszłości hello i dlatego stać się publicznie widoczna.
* Jeśli wystąpi błąd hello: "**Ta subskrypcja nie jest zarejestrowany toouse przestrzeni nazw Microsoft.DataFactory**", wykonaj jedną z następujących hello i spróbuj ponownie opublikować: 
  
  * W programie Azure PowerShell Uruchom hello następujące polecenia tooregister hello fabryki danych dostawcy: 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Powitania po tooconfirm polecenie można uruchomić tego hello fabryki danych dostawca został zarejestrowany. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Logowanie przy użyciu hello subskrypcji platformy Azure do hello [portalu Azure](https://portal.azure.com) i przejdź do bloku usługi fabryka danych tooa tworzenie fabryki danych w hello portalu Azure (lub). Ta akcja rejestruje automatycznie hello dostawcy dla Ciebie.

Przed utworzeniem potoku, należy toocreate kilku jednostek fabryki danych najpierw. Najpierw Utwórz źródło toolink połączonych usług i miejsce docelowe danych przechowuje dane tooyour przechowywania. Następnie należy zdefiniować dane toorepresent wejściowych i wyjściowych zestawów danych w magazynach połączonych danych. Na koniec należy utworzyć potok hello do działania, która używa tych zestawów danych.

## <a name="create-linked-services"></a>Tworzenie połączonych usług
Połączone usługi są tworzone w toolink fabryki danych dane są przechowywane i obliczeniowe fabryki danych toohello usług. W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics. Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa). W związku z tym tworzy się dwie połączone usługi o nazwie AzureStorageLinkedService i AzureSqlLinkedService typu: AzureStorage i AzureSqlDatabase.  

Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure. To konto magazynu jest hello jedną w którym utworzono kontener i hello dane przekazane jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL. dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych. Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage
W tym kroku możesz połączyć fabrykę danych tooyour konta magazynu platformy Azure. W tej sekcji można określić nazwę hello i klucza konta magazynu Azure. Zobacz [połączonej usługi magazynu Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) szczegółowe informacje o toodefine właściwości używane w formacie JSON połączonej usługi magazynu Azure.  

1. Przypisz hello toovariable polecenia o nazwie **cmd**. 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Uruchom polecenie hello przy użyciu **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Wyświetl wyniki hello. Jeśli hello połączone usługi został utworzony pomyślnie, zobacz hello JSON usługi hello połączone w hello **wyniki**; w przeciwnym razie zostanie wyświetlony komunikat o błędzie.

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>Tworzenie połączonej usługi SQL Azure
W tym kroku możesz połączyć fabrykę danych tooyour bazy danych Azure SQL. W tej sekcji można określić nazwy serwera Azure SQL hello, nazwa bazy danych, nazwę użytkownika i hasło użytkownika. Zobacz [Azure SQL połączona usługa](data-factory-azure-sql-connector.md#linked-service-properties) szczegółowe informacje o toodefine właściwości używane w formacie JSON Azure SQL połączonej usługi.

1. Przypisz hello toovariable polecenia o nazwie **cmd**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
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
W poprzednim kroku hello utworzono toolink połączone usługi konta magazynu Azure i fabryki danych tooyour bazy danych Azure SQL. W tym kroku należy zdefiniować dwa zestawy danych o nazwie AzureBlobInput i AzureSqlOutput reprezentujące danych wejściowych i wyjściowych danych przechowywanych w magazynach danych hello odwołuje się AzureStorageLinkedService i AzureSqlLinkedService odpowiednio.

Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure. I zestawu danych wejściowych obiektu blob hello (AzureBlobInput) określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.  

Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL. I hello danych wyjściowych SQL tabeli dataset (OututDataset) określa hello tabeli w hello bazy danych toowhich powitalne dane z magazynu obiektów blob hello są kopiowane. 

### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych
W tym kroku utworzysz zestaw danych o nazwie AzureBlobInput, który wskazuje plik obiektu blob tooa (emp.txt) w folderze głównym hello kontenera obiektów blob (adftutorial) w hello reprezentowany przez hello AzureStorageLinkedService połączone usługi Magazyn Azure. Brak określić wartość dla nazwy pliku hello (lub Pomiń je), danych z wszystkich obiektów blob w folderze wejściowych hello są skopiowanych toohello docelowego. W tym samouczku należy określić wartość dla hello fileName. 

1. Przypisz hello toovariable polecenia o nazwie **cmd**. 

    ```PowerSHell   
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
Hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL. Utwórz w tym kroku Hello danych wyjściowych SQL tabeli dataset (OututDataset) określa, że tabela hello hello bazy danych toowhich hello danych z magazynu obiektów blob hello jest kopiowany.

1. Przypisz hello toovariable polecenia o nazwie **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
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
W tym kroku za pomocą **działania kopiowania** zostanie utworzony potok, w którym parametr **AzureBlobInput** jest używany jako dane wejściowe, a parametr **AzureSqlOutput** jako dane wyjściowe.

Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu. W tym samouczku wyjściowy zestaw danych jest skonfigurowane tooproduce wycinek godzinę. potok Hello ma czas rozpoczęcia i godzina zakończenia, będące w ciągu jednego dnia od siebie, który wynosi 24 godziny. W związku z tym 24 wycinków wyjściowy zestaw danych są produkowane przez hello potoku. 

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

**Gratulacje!** Pomyślnie utworzono fabryki danych Azure z potok, który kopiuje dane z bazy danych SQL tooAzure magazynu obiektów Blob Azure.

## <a name="monitor-pipeline"></a>Monitorowanie potoku
W tym kroku użyjesz tworzonym przez potok hello wycinków toomonitor interfejsu API REST fabryki danych.

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Upewnij się, hello początkową i końcową czas określony w powitania po polecenie start hello dopasowania i kończyć razy hello potoku. 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

Uruchom hello Invoke-Command i hello kolejnego do momentu wyświetlenia wycinek **gotowe** stanu lub **** stanu. Gdy wycinek hello jest w stanie gotowe, sprawdź hello **pustych elementów** tabeli w bazie danych Azure SQL hello danych wyjściowych. 

Każdy wycinek dwa wiersze danych z pliku źródłowego hello są kopiowane toohello pustych elementów tabeli w bazie danych Azure SQL hello. W związku z tym 24 nowych rekordów w tabeli pustych elementów hello wyświetlona w sytuacji, gdy wszystkie fragmenty hello są pomyślnie przetworzone (w stanie innym niż Ready). 

## <a name="summary"></a>Podsumowanie
W tym samouczku użyto toocreate interfejsu API REST usługi Azure data factory toocopy dane z bazy danych Azure SQL tooan obiektów blob platformy Azure. Poniżej przedstawiono ogólne kroki hello, wykonane w tym samouczku:  

1. Tworzenie **fabryki danych** Azure.
2. Tworzenie **połączonych usług**:
   1. Magazyn Azure połączone usługi toolink konta magazynu Azure, która przechowuje dane wejściowe.     
   2. Azure SQL połączone usługi toolink przechowujący dane wyjściowe hello bazy danych Azure SQL. 
3. Tworzenie **zestawów danych** opisujących dane wejściowe i wyjściowe dla potoków.
4. Tworzenie **potoku** za pomocą działania kopiowania, w którym źródłem jest element BlobSource, a ujściem element SqlSink. 

## <a name="next-steps"></a>Następne kroki
W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania. Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello.
