---
title: "Samouczek: korzystanie z interfejsu API REST w celu utworzenia potoku usługi Azure Data Factory | Microsoft Docs"
description: "W tym samouczku opisano korzystanie z interfejsu API REST w celu utworzenia potoku usługi Azure Data Factory z działaniem kopiowania, aby skopiować dane z magazynu obiektów blob Azure do bazy danych Azure SQL."
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
robots: noindex
ms.openlocfilehash: a573bb9880b70ea994fe622226987563f18e1a9f
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="tutorial-use-rest-api-to-create-an-azure-data-factory-pipeline-to-copy-data"></a>Samouczek: korzystanie z interfejsu API REST w celu utworzenia potoku usługi Azure Data Factory do kopiowania danych 
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

W tym artykule wyjaśniono, jak używać interfejsu API REST do tworzenia fabryki danych obejmującej potok, który kopiuje dane z usługi Azure Blob Storage do bazy danych Azure SQL. Jeśli jesteś nowym użytkownikiem usługi Azure Data Factory, przed wykonaniem instrukcji z tego samouczka zapoznaj się z artykułem [Wprowadzenie do usługi Azure Data Factory](data-factory-introduction.md).   

W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania). Działanie kopiowania kopiuje dane z obsługiwanego magazynu danych do obsługiwanego magazynu danych ujścia. Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Działanie jest obsługiwane przez globalnie dostępną usługę, która może kopiować dane między różnymi magazynami danych w sposób bezpieczny, niezawodny i skalowalny. Więcej informacji o działaniu kopiowania znajduje się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md).

Potok może obejmować więcej niż jedno działanie. Dwa działania można połączyć w łańcuch (uruchomić jedno działanie po drugim), ustawiając wyjściowy zestaw danych jednego działania jako zestaw wejściowy drugiego. Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Ten artykuł nie obejmuje całego interfejsu API REST usługi Data Factory. Pełna dokumentacja dotycząca poleceń cmdlet usługi Data Factory znajduje się w artykule [Data Factory Cmdlet Reference](/rest/api/datafactory/) (Dokumentacja dotycząca interfejsu API REST usługi Data Factory).
>  
> Potok danych przedstawiony w tym samouczku kopiuje dane ze źródłowego do docelowego magazynu danych. Aby zapoznać się z samouczkiem dotyczącym przekształcania danych za pomocą usługi Azure Data Factory, zobacz [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md) (Samouczek: Tworzenie potoku przekształcającego dane przy użyciu klastra Hadoop).

## <a name="prerequisites"></a>Wymagania wstępne
* Zapoznaj się z artykułem [Omówienie samouczka](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) i wykonaj kroki **wymagań wstępnych**.
* Zainstaluj na komputerze narzędzie [Curl](https://curl.haxx.se/dlwiz/). W połączeniu z poleceniami REST umożliwia ono utworzenie fabryki danych. 
* Postępuj zgodnie z instrukcjami zawartymi w [tym artykule](../../azure-resource-manager/resource-group-create-service-principal-portal.md), aby wykonać następujące czynności: 
  1. Utworzenie aplikacji sieci Web o nazwie **ADFCopyTutorialApp** w usłudze Azure Active Directory.
  2. Pobranie **identyfikatora klienta** i **klucza tajnego**. 
  3. Uzyskanie **identyfikatora dzierżawy**. 
  4. Przypisanie aplikacji **ADFCopyTutorialApp** do roli **Współautor Data Factory**.  
* Zainstaluj program [Azure PowerShell](/powershell/azure/overview).  
* Uruchom program **PowerShell** i wykonaj następujące czynności. Nie zamykaj programu Azure PowerShell, zanim nie wykonasz wszystkich instrukcji z tego samouczka. Jeśli go zamkniesz i otworzysz ponownie, musisz uruchomić te polecenia jeszcze raz.
  
  1. Uruchom poniższe polecenie i wprowadź nazwę użytkownika oraz hasło, których używasz do logowania się w witrynie Azure Portal:
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. Uruchom poniższe polecenie, aby wyświetlić wszystkie subskrypcje dla tego konta:

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. Uruchom poniższe polecenie, aby wybrać subskrypcję, z którą chcesz pracować. Zastąp ciąg **&lt;NameOfAzureSubscription**&gt; nazwą subskrypcji platformy Azure. 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. Utwórz grupę zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** przez uruchomienie następującego polecenia w programie PowerShell:  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      Jeśli istnieje już grupa zasobów, można określić, czy należy ją zaktualizować (Y), czy zachować (N). 
     
      W niektórych krokach w tym samouczku zakłada się, że używana jest grupa zasobów o nazwie ADFTutorialResourceGroup. Jeśli używasz innej grupy zasobów, podczas wykonywania instrukcji w tym samouczku trzeba będzie wstawić jej nazwę zamiast nazwy ADFTutorialResourceGroup.

## <a name="create-json-definitions"></a>Tworzenie definicji JSON
W folderze, w którym znajduje się narzędzie curl.exe, utwórz następujące pliki w formacie JSON. 

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Nazwa musi być globalnie unikatowa — można o to zadbać, dodając do niej prefiks/sufiks ADFCopyTutorialDF. 
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
> Zastąp wartości **accountname** i **accountkey** nazwą konta usługi Azure Storage oraz jego kluczem. Informacje na temat pobierania klucza dostępu do magazynu znajdują się w artykule [Wyświetlanie, kopiowanie i ponowne generowanie kluczy dostępu do magazynu](../../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).

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
> Zastąp parametry **servername**, **databasename**, **username** oraz **password** nazwą serwera SQL Azure, bazy danych, konta użytkownika i hasłem do konta.  
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

Poniższa tabela zawiera opis właściwości kodu JSON użytych w tym fragmencie kodu:

| Właściwość | Opis |
|:--- |:--- |
| type | Właściwość typu jest ustawiona na wartość **AzureBlob**, ponieważ dane znajdują się w magazynie obiektów blob na platformie Azure. |
| linkedServiceName | Odnosi się do utworzonego wcześniej elementu **AzureStorageLinkedService**. |
| folderPath | Określa **kontener** obiektów blob oraz **folder**, który zawiera wejściowe obiekty blob. W tym samouczku kontenerem obiektów blob jest adftutorial, a folderem — katalog główny. | 
| fileName | Ta właściwość jest opcjonalna. Jeśli pominiesz tę właściwość, zostaną wybrane wszystkie pliki z folderu folderPath. W tym samouczku dla fileName określono plik **emp.txt**, więc tylko on zostanie wybrany do przetwarzania. |
| format -> type |Plik wejściowy jest w formacie tekstowym, więc należy użyć właściwości **TextFormat**. |
| columnDelimiter | Kolumny w pliku wejściowym są rozdzielane **przecinkami (`,`)**. |
| frequency/interval | Właściwość frequency (częstotliwość) jest ustawiona na wartość **Hour** (Godzina), a wartość interwału wynosi **1**, co oznacza, że wycinki wejściowe są dostępne **co godzinę**. Innymi słowy, usługa Data Factory szuka danych wejściowych co godzinę w folderze głównym określonego kontenera obiektów blob (**adftutorial**). Wyszukuje dane między godzinami rozpoczęcia i zakończenia potoku, a nie przed nimi ani po nich.  |
| external | Ta właściwość ma wartość **true** (prawda), jeśli dane nie są generowane przez ten potok. Dane wejściowe w tym samouczku znajdują się w pliku emp.txt, który nie jest generowany w tym potoku, więc możemy ustawić tę właściwość na true. |

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
Poniższa tabela zawiera opis właściwości kodu JSON użytych w tym fragmencie kodu:

| Właściwość | Opis |
|:--- |:--- |
| type | Właściwość typu jest ustawiona na **AzureSqlTable**, ponieważ dane są kopiowane do tabeli w bazie danych SQL na platformie Azure. |
| linkedServiceName | Odnosi się do utworzonego wcześniej elementu **AzureSqlLinkedService**. |
| tableName | Określa **tabelę** , do której są kopiowane dane. | 
| frequency/interval | Właściwość frequency (częstotliwość) jest ustawiona na wartość **Hour** (Godzina), a wartość interwału wynosi **1**, co oznacza, że wycinki wyjściowe są tworzone **co godzinę** między godziną rozpoczęcia i zakończenia potoku, a nie przed tą godziną lub po niej.  |

Tabela emp bazy danych zawiera trzy kolumny — **ID**, **FirstName** i **LastName**. ID to kolumna tożsamości, więc należy określić tylko wartości **FirstName** i **LastName**.

Aby uzyskać więcej informacji o tych właściwościach JSON, zobacz [artykuł dotyczący łącznika usługi Azure SQL](data-factory-azure-sql-connector.md#dataset-properties).

### <a name="pipelinejson"></a>pipeline.json

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data to Azure SQL database",
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

Pamiętaj o następujących kwestiach:

- W sekcji działań jest tylko jedno działanie, którego parametr **type** (typ) został ustawiony na wartość **Copy**. Więcej informacji o działaniu kopiowania znajduje się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md). W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).
- Dane wejściowe dla działania mają ustawienie **AzureBlobInput**, a dane wyjściowe — **AzureSqlOutput**. 
- W sekcji **typeProperties** parametr **BlobSource** został określony jako typ źródłowy, a parametr **SqlSink** został określony jako typ ujścia. Aby uzyskać pełną listę magazynów danych obsługiwanych przez działanie kopiowania jako źródła i ujścia, zobacz informacje dotyczące [obsługiwanych magazynów danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Aby dowiedzieć się, jak używać określonego obsługiwanego magazynu danych jako źródła/ujścia, kliknij link w tabeli.  
 
Zastąp wartość właściwości **start** datą bieżącą, a wartość **end** datą jutrzejszą. Możesz określić tylko część daty i pominąć część godziny parametru data/godzina. Na przykład „2017-02-03” jest odpowiednikiem „2017-02-03T00:00:00Z”.
 
Zarówno data/godzina rozpoczęcia, jak i data/godzina zakończenia muszą być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Przykładowo: 2016-10-14T16:32:41Z. Czas **end** jest opcjonalny, ale w tym samouczku zostanie użyty. 
 
Jeśli nie określisz wartości dla właściwości **end**, zostanie ona obliczona jako „**czas rozpoczęcia + 48 godzin**”. Aby uruchomić potok bezterminowo, określ **9999-09-09** jako wartość właściwości **end**.
 
W powyższym przykładzie występują 24 wycinki danych, gdyż poszczególne wycinki są generowane co godzinę.

Opisy właściwości JSON w definicji potoku znajdują się w artykule dotyczącym [tworzenia potoków](data-factory-create-pipelines.md). Opisy właściwości JSON w definicji działania kopiowania znajdują się w artykule dotyczącym [działań związanych z przenoszeniem danych](data-factory-data-movement-activities.md). Opisy właściwości JSON obsługiwanych przez BlobSource można znaleźć w [artykule dotyczącym łącznika usługi Azure Blob](data-factory-azure-blob-connector.md). Opisy właściwości JSON obsługiwanych przez SqlSink można znaleźć w artykule [dotyczącym łącznika usługi Azure SQL Database](data-factory-azure-sql-connector.md).

## <a name="set-global-variables"></a>Ustawianie zmiennych globalnych
Po zastąpieniu wartości własnymi wykonaj następujące polecenia w programie Azure PowerShell:

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

Po zaktualizowaniu nazwy fabryki danych, której używasz, uruchom następujące polecenie: 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>Uwierzytelnianie przy użyciu usługi AAD
Uruchom następujące polecenie w celu uwierzytelniania za pomocą usługi Azure Active Directory (AAD): 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>Tworzenie fabryki danych
W tym kroku opisano tworzenie fabryki danych Azure o nazwie **ADFCopyTutorialDF**. Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Na przykład działanie kopiowania w celu kopiowania danych ze źródła do docelowego magazynu danych. Działanie technologii Hive w usłudze HDInsight służące do uruchamiania skryptu Hive używanego do przekształcenia danych wejściowych w dane wyjściowe produktu. Uruchom następujące polecenia, aby utworzyć fabrykę danych: 

1. Przypisz polecenie do zmiennej o nazwie **cmd**. 
   
    > [!IMPORTANT]
    > Upewnij się, że określona tutaj nazwa fabryki danych (ADFCopyTutorialDF) odpowiada nazwie podanej w pliku **datafactory.json**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Przejrzyj wyniki. Jeśli fabryka danych została utworzona pomyślnie, w **wynikach** będzie widoczny kod JSON tej fabryki. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.  
   
    ```
    Write-Host $results
    ```

Pamiętaj o następujących kwestiach:

* Nazwa fabryki danych Azure musi być globalnie unikatowa. Jeśli w wynikach jest wyświetlany błąd: **Nazwa fabryki danych „ADFCopyTutorialDF” jest niedostępna**, wykonaj następujące czynności:  
  
  1. Zmień nazwę fabryki (np. twojanazwaADFCopyTutorialDF) w pliku **datafactory.json**.
  2. W pierwszym poleceniu, w którym zmiennej **$cmd** jest przypisywana wartość, zastąp nazwę ADFCopyTutorialDF nową nazwą i uruchom to polecenie. 
  3. Uruchom kolejne dwa polecenia, aby wywołać interfejs API REST w celu utworzenia fabryki danych i wyświetlić wyniki tej operacji. 
     
     Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.
* Aby tworzyć wystąpienia usługi Fabryka danych, musisz być współautorem/administratorem subskrypcji Azure
* W przyszłości nazwa fabryki danych może zostać zarejestrowana jako nazwa DNS, a wówczas stanie się widoczna publicznie.
* Jeśli zostanie wyświetlony komunikat o błędzie: „**Subskrypcja nie jest zarejestrowana w celu używania przestrzeni nazw Microsoft.DataFactory**”, wykonaj jedną z następujących czynności i spróbuj opublikować ponownie: 
  
  * W programie Azure PowerShell uruchom następujące polecenie, aby zarejestrować dostawcę usługi Data Factory: 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Można uruchomić następujące polecenie, aby potwierdzić, że dostawca usługi Data Factory jest zarejestrowany. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Zaloguj się przy użyciu subskrypcji Azure do [portalu Azure](https://portal.azure.com) i przejdź do bloku Fabryka danych lub utwórz fabrykę danych w portalu Azure. Ta akcja powoduje automatyczne zarejestrowanie dostawcy.

Przed utworzeniem potoku musisz utworzyć kilka jednostek usługi Fabryka danych. Najpierw utwórz połączone usługi, aby połączyć źródłowy i docelowy magazyn danych ze swoim magazynem danych. Następnie zdefiniuj wejściowy i wyjściowy zestaw danych w celu reprezentowania danych w połączonych magazynach danych. Na koniec utwórz potok z działaniem używającym tych zestawów danych.

## <a name="create-linked-services"></a>Tworzenie połączonych usług
Połączone usługi tworzy się w fabryce danych w celu połączenia magazynów danych i usług obliczeniowych z fabryką danych. W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics. Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa). W związku z tym tworzy się dwie połączone usługi o nazwie AzureStorageLinkedService i AzureSqlLinkedService typu: AzureStorage i AzureSqlDatabase.  

Polecenie AzureStorageLinkedService łączy konto usługi Azure Storage z fabryką danych. Na tym koncie magazynu utworzono kontener i przekazano na nie dane w ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

Polecenie AzureSqlLinkedService łączy bazę danych SQL na platformie Azure z fabryką danych. W tej bazie danych są przechowywane dane skopiowane z magazynu obiektów blob. Tabelę emp w tej bazie danych utworzono w ramach [wymagań wstępnych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Tworzenie połączonej usługi Azure Storage
W tym kroku opisano łączenie konta usługi Azure Storage z fabryką danych. W tej sekcji określa się nazwę i klucz konta magazynu platformy Azure. Szczegóły dotyczące właściwości JSON używanych do definiowania połączonej usługi Azure Storage zawiera temat [Połączona usługa Azure Storage](data-factory-azure-blob-connector.md#azure-storage-linked-service).  

1. Przypisz polecenie do zmiennej o nazwie **cmd**. 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Przejrzyj wyniki. Jeśli połączona usługa została utworzona pomyślnie, w **wynikach** będzie widoczny kod JSON tej usługi. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>Tworzenie połączonej usługi SQL Azure
W tym kroku opisano łączenie bazy danych Azure SQL Database z fabryką danych. W tej sekcji określa się nazwę serwera usługi Azure SQL, nazwę bazy danych, nazwę użytkownika i hasło użytkownika. Szczegóły dotyczące właściwości JSON używanych do definiowania połączonej usługi Azure SQL zawiera temat [Połączona usługa Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).

1. Przypisz polecenie do zmiennej o nazwie **cmd**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Przejrzyj wyniki. Jeśli połączona usługa została utworzona pomyślnie, w **wynikach** będzie widoczny kod JSON tej usługi. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Tworzenie zestawów danych
W poprzednim kroku zostały utworzone połączone usługi używane do połączenia konta usługi Azure Storage i bazy danych Azure SQL z fabryką danych. W tym kroku zostaną zdefiniowane dwa zestawy danych o nazwach AzureBlobInput i AzureSqlOutput zawierające dane wejściowe i wyjściowe przechowywane w magazynach danych, do których odwołują się usługi AzureStorageLinkedService i AzureSqlLinkedService.

Połączona usługa magazynu Azure określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z kontem magazynu Azure. Natomiast wejściowy zestaw danych obiektów blob (AzureBlobInput) określa kontener oraz folder, który zawiera dane wejściowe.  

W analogiczny sposób połączona usługa Azure SQL Database określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z bazą danych SQL usługi Azure. Wyjściowy zestaw danych tabeli SQL (OutputDataset) określa tabelę w bazie danych, do której są kopiowane dane z magazynu obiektów blob. 

### <a name="create-input-dataset"></a>Tworzenie wejściowego zestawu danych
W tym kroku zostanie utworzony zestaw danych o nazwie AzureBlobInput wskazujący na plik obiektów blob (emp.txt) w katalogu głównym kontenera obiektów blob (adftutorial) w usłudze Azure Storage reprezentowany przez połączoną usługę AzureStorageLinkedService. Jeśli nie określisz wartości obiektu fileName lub ją pominiesz, dane ze wszystkich obiektów blob w folderze wejściowym zostaną skopiowane do lokalizacji docelowej. W tym samouczku wartość obiektu fileName jest określona. 

1. Przypisz polecenie do zmiennej o nazwie **cmd**. 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Przejrzyj wyniki. Jeśli zestaw danych został utworzony pomyślnie, w **wynikach** będzie widoczny kod JSON tego zestawu. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Tworzenie wyjściowego zestawu danych
Połączona usługa Azure SQL Database określa parametry połączenia, z których korzysta usługa Data Factory w czasie wykonywania, aby połączyć się z bazą danych SQL usługi Azure. Wyjściowy zestaw danych tabeli SQL (OutputDataset) tworzony w tym kroku określa tabelę w bazie danych, do której są kopiowane dane z magazynu obiektów blob.

1. Przypisz polecenie do zmiennej o nazwie **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Przejrzyj wyniki. Jeśli zestaw danych został utworzony pomyślnie, w **wynikach** będzie widoczny kod JSON tego zestawu. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a>Tworzenie potoku
W tym kroku za pomocą **działania kopiowania** zostanie utworzony potok, w którym parametr **AzureBlobInput** jest używany jako dane wejściowe, a parametr **AzureSqlOutput** jako dane wyjściowe.

Obecnie harmonogram jest prowadzony przy użyciu wyjściowego zestawu danych. W tym samouczku wyjściowy zestaw danych jest konfigurowany do tworzenia wycinka co godzinę. Potok ma godzinę rozpoczęcia i zakończenia, między którymi następuje jeden dzień różnicy (dokładnie 24 godziny). Potok tworzy więc 24 wycinki wyjściowego zestawu danych. 

1. Przypisz polecenie do zmiennej o nazwie **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Uruchom to polecenie przy użyciu polecenia **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Przejrzyj wyniki. Jeśli zestaw danych został utworzony pomyślnie, w **wynikach** będzie widoczny kod JSON tego zestawu. W przeciwnym razie zostanie wyświetlony komunikat o błędzie.  

    ```PowerShell   
    Write-Host $results
    ```

**Gratulacje!** Fabryka danych Azure z potokiem kopiującym dane z usługi Azure Blob Storage do bazy danych Azure SQL Database została pomyślnie utworzona.

## <a name="monitor-pipeline"></a>Monitorowanie potoku
W tym kroku interfejs API REST usługi Data Factory służy do monitorowania wycinków generowanych przez potok.

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Upewnij się, że godziny rozpoczęcia i zakończenia określone w następującym poleceniu są zgodne z godzinami rozpoczęcia i zakończenia potoku. 

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

Uruchom polecenie Invoke-Command i kolejne polecenie, aż zobaczysz, że wycinek jest w stanie **Gotowe** lub **Niepowodzenie**. Gdy wycinek jest w stanie Gotowe, sprawdź, czy w tabeli **emp** w bazie danych Azure SQL Database znajdują się dane wyjściowe. 

Dla każdego wycinka do tabeli emp w bazie danych Azure SQL Database zostają skopiowane dwa wiersze danych z pliku źródłowego. Po pomyślnym przetworzeniu wycinków (stan Gotowe) w tabeli emp będą widoczne 24 nowe rekordy. 

## <a name="summary"></a>Podsumowanie
W tym samouczku opisano tworzenie fabryki danych Azure za pomocą interfejsu API REST w celu kopiowania danych z obiektu blob Azure do bazy danych Azure SQL Database. Główne kroki opisane w tym samouczku:  

1. Tworzenie **fabryki danych** Azure.
2. Tworzenie **połączonych usług**:
   1. Połączona usługa Azure Storage, która ma nawiązać połączenie z kontem usługi Azure Storage, na którym przechowywane są dane wejściowe.     
   2. Połączona usługa SQL Azure, która ma nawiązać połączenie z bazą danych Azure SQL Database, w której przechowywane są dane wyjściowe. 
3. Tworzenie **zestawów danych** opisujących dane wejściowe i wyjściowe dla potoków.
4. Tworzenie **potoku** za pomocą działania kopiowania, w którym źródłem jest element BlobSource, a ujściem element SqlSink. 

## <a name="next-steps"></a>Następne kroki
W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania. Poniższa tabela zawiera listę magazynów danych obsługiwanych przez działanie kopiowania jako źródła i lokalizacje docelowe: 

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

Aby uzyskać informacje dotyczące kopiowania danych do/z magazynu danych, kliknij link do magazynu danych w tabeli.
