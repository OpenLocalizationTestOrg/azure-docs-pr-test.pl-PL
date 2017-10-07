---
title: "aaaTransform danych przy użyciu skryptu U-SQL - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprocess lub Przekształcanie danych za pomocą skryptów U-SQL w usłudze Azure Data Lake Analytics obliczeniowe usługi."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a>Przekształcanie danych za pomocą skryptów U-SQL w usłudze Azure Data Lake Analytics 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Działanie gałęzi](data-factory-hive-activity.md) 
> * [Działanie pig](data-factory-pig-activity.md)
> * [Działania MapReduce](data-factory-map-reduce.md)
> * [Działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Działanie Spark](data-factory-spark.md)
> * [Działanie wykonywania wsadowego w usłudze Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Działania aktualizowania zasobów w usłudze Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Działania procedur składowanych](data-factory-stored-proc-activity.md)
> * [Działania języka U-SQL usługi Data Lake Analytics](data-factory-usql-activity.md)
> * [Działania niestandardowe .NET](data-factory-use-custom-activities.md)

Potok w fabryce danych Azure przetwarza dane w usługach magazynu połączone, przy użyciu obliczeniowego połączonej usługi. Zawiera sekwencję działań, gdzie każde działanie wykonuje operację przetwarzania specyficznego dla. W tym artykule opisano hello **Data Lake Analytics U-SQL działania** , na którym działa **U-SQL** skryptom na **Azure Data Lake Analytics** obliczeniowe połączonej usługi. 

> [!NOTE]
> Przed utworzeniem potoku z działaniem Data Lake Analytics U-SQL, należy utworzyć konto usługi Azure Data Lake Analytics. toolearn dotyczące usługi Azure Data Lake Analytics, zobacz [Rozpoczynanie pracy z usługą Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).
> 
> Przejrzyj hello [kompilacji pierwszy samouczek potoku](data-factory-build-your-first-pipeline.md) dla toocreate szczegółowy opis kroków fabryki danych, połączone usługi, zestawy danych i potoku. Za pomocą fragmenty kodu JSON Edytor fabryki danych i jednostek fabryki danych toocreate programu Visual Studio lub Azure PowerShell.

## <a name="supported-authentication-types"></a>Typy obsługiwane uwierzytelniania
Działanie U-SQL obsługuje poniżej typy uwierzytelniania względem usługi Data Lake Analytics:
* Uwierzytelnianie jednostki usługi
* Uwierzytelnianie użytkownika poświadczeń (OAuth) 

Firma Microsoft zaleca korzystanie z uwierzytelniania głównej usługi, zwłaszcza w przypadku zaplanowane wykonanie U-SQL. Zachowanie wygaśnięcia tokenu może wystąpić przy użyciu uwierzytelniania poświadczeń użytkownika. Szczegółowe informacje dotyczące konfiguracji, zobacz hello [połączona usługa właściwości](#azure-data-lake-analytics-linked-service) sekcji.

## <a name="azure-data-lake-analytics-linked-service"></a>Usługi Azure Data Lake Analytics połączona usługa
Możesz utworzyć **Azure Data Lake Analytics** połączone toolink usługi fabryki danych Azure tooan usługi Azure Data Lake Analytics obliczeń. Data Lake Analytics U-SQL działania w potoku hello Hello odwołuje się toothis połączone usługi. 

Witaj Poniższa tabela zawiera opisy hello ogólne właściwości używane w hello definicji JSON. Dodatkowo można wybrać nazwy głównej usługi i uwierzytelnianie poświadczeń użytkownika.

| Właściwość | Opis | Wymagane |
| --- | --- | --- |
| **Typ** |powinien mieć ustawioną właściwość type Hello: **AzureDataLakeAnalytics**. |Tak |
| **Nazwa konta** |Nazwa konta usługi Azure Data Lake Analytics. |Tak |
| **Element dataLakeAnalyticsUri** |Identyfikator URI, usługi Azure Data Lake Analytics. |Nie |
| **Identyfikator subskrypcji** |Identyfikator subskrypcji platformy Azure |Nie (Jeśli nie określono subskrypcji hello jest używana fabryka danych). |
| **grupy zasobów o nazwie** |Nazwa grupy zasobów platformy Azure |Nie (Jeśli nie określono grupy zasobów hello jest używana fabryka danych). |

### <a name="service-principal-authentication-recommended"></a>Uwierzytelnianie główna usługi (zalecane)
główne uwierzytelnianie usługi toouse rejestru jednostki aplikacji w usłudze Azure Active Directory (Azure AD) i udziel go hello dostępu tooData Lake Store. Aby uzyskać szczegółowe instrukcje, zobacz [do usługi uwierzytelniania](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Zwróć uwagę na powitania następujące wartości, których używasz toodefine hello połączonej usługi:
* Identyfikator aplikacji
* Klucz aplikacji 
* Identyfikator dzierżawy

Uwierzytelnianie usługi głównej określając hello następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| **servicePrincipalId** | Określ identyfikator aplikacji hello klienta. | Tak |
| **servicePrincipalKey** | Określ klucz aplikacji hello. | Tak |
| **dzierżawy** | Określ informacje dzierżawy hello (identyfikator nazwy lub dzierżawy domeny), w którym znajduje się aplikacja. Można go pobrać aktywowania hello myszy w prawym górnym narożniku hello hello portalu Azure. | Tak |

**Przykład: Usługa podmiotu zabezpieczeń uwierzytelniania**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Uwierzytelnianie poświadczeń użytkownika
Alternatywnie można uwierzytelnienia poświadczeń użytkownika dla usługi Data Lake Analytics, określając hello następujące właściwości:

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| **autoryzacji** | Kliknij przycisk hello **autoryzacji** przycisku na powitania Edytor fabryki danych i wprowadź Twoje poświadczenia przypisującej właściwość toothis hello wygenerowana automatycznie autoryzacji URL. | Tak |
| **Identyfikator sesji** | Identyfikator sesji OAuth z sesji autoryzacji OAuth hello. Każdy identyfikator sesji jest unikatowy i mogą być użyte tylko raz. To ustawienie jest automatycznie generowany, gdy używasz hello Edytor fabryki danych. | Tak |

**Przykład: Użytkownik poświadczeń uwierzytelniania**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Wygaśnięcia tokenu
Witaj kod autoryzacji wygenerowanych przy użyciu hello **autoryzacji** przycisk wygaśnie po upływie pewnego czasu. Zobacz hello na powitania czas wygaśnięcia dla różnych typów kont użytkowników w poniższej tabeli. Może zostać wyświetlony następujący komunikat o błędzie hello hello podczas uwierzytelniania **wygaśnięcia tokenu**: poświadczeń błąd operacji: invalid_grant - AADSTS70002: błąd podczas sprawdzania poprawności poświadczeń. AADSTS70008: hello podać Udziel dostępu jest wygasnąć lub zostać odwołane. Identyfikator śledzenia: Identyfikator korelacji d18629e8-af88-43c5-88e3-d8419eb1fca1: sygnatura czasowa fac30a0c-6be6-4e02-8d69-a776d2ffefd7: 2015-12-15 21:09:31Z

| Typ użytkownika | Wygasa po |
|:--- |:--- |
| Konta użytkowników, które nie są zarządzane przez usługę Azure Active Directory (@hotmail.com, @live.comitp.) |12 godzin |
| Konta użytkowników zarządzanych przez usługi Azure Active Directory (AAD) |Uruchom 14 dni od ostatniego wycinek hello. <br/><br/>90 dni, jeśli wycinek oparte na podstawie OAuth połączonej usługi jest uruchamiana co najmniej raz na 14 dni. |

tooavoid/Rozwiąż ten błąd, ponownie autoryzować przy użyciu hello **autoryzacji** przycisku hello **wygaśnięcia tokenu** i wdrożenie usługi hello połączone. Można również tworzyć wartości **sessionId** i **autoryzacji** właściwości programowo przy użyciu kodu w następujący sposób:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Zobacz [klasy AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [klasy AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), i [klasy AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tematy, aby uzyskać więcej informacji informacje o klasach fabryki danych hello używane w kodzie hello. Dodaj odwołanie do: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll dla hello WindowsFormsWebAuthenticationDialog klasy. 

## <a name="data-lake-analytics-u-sql-activity"></a>Działania języka U-SQL usługi Data Lake Analytics
powitania po fragment kodu JSON definiuje potoku z działaniem Data Lake Analytics U-SQL. Definicja działania Hello ma toohello odwołanie do usługi Azure Data Lake Analytics połączone, utworzony wcześniej.   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

Witaj poniższej tabeli opisano nazwy i opisy właściwości, które są określone toothis działania. 

| Właściwość | Opis | Wymagane |
|:--- |:--- |:--- |
| type |zbyt należy ustawić właściwość typu Hello**DataLakeAnalyticsU SQL**. |Tak |
| scriptPath |Ścieżka toofolder, zawierający skrypt hello U-SQL. Nazwa pliku hello jest rozróżniana wielkość liter. |Nie (Jeśli używasz skryptu) |
| Element scriptLinkedService |Połączonej usługi, która łączy hello magazynu, który zawiera hello skryptu toohello usługi fabryka danych |Nie (Jeśli używasz skryptu) |
| Skrypt |Określ skrypt wbudowany zamiast określania scriptPath i scriptLinkedService. Na przykład: `"script": "CREATE DATABASE test"`. |Nie (Jeśli używasz scriptPath i scriptLinkedService) |
| degreeOfParallelism |Maksymalna liczba węzłów Hello używać jednocześnie toorun hello zadania. |Nie |
| Priorytet |Określa, które spośród wszystkich znajdujących się w kolejce zadań powinna być wybranego toorun najpierw. Witaj hello niższą, wyższy priorytet hello hello. |Nie |
| parameters |Parametry skryptu hello U-SQL |Nie |
| runtimeVersion | Wersja środowiska uruchomieniowego toouse aparat hello U-SQL | Nie | 
| właściwość compilationMode | <p>Tryb kompilacji U-SQL. Musi być jedną z następujących wartości:</p> <ul><li>**Semantycznej:** wykonywać tylko semantycznego kontroli i potrzeby związane z poprawnością kontroli.</li><li>**Pełna:** wykonania pełnej kompilacji hello, w tym sprawdzanie składni, optymalizacja, generowanie kodu itp.</li><li>**SingleBox:** wykonania pełnej kompilacji hello z tooSingleBox ustawienie TargetType.</li></ul><p>Jeśli nie określisz wartości dla tej właściwości, powitania serwera określa tryb kompilacji optymalne hello. </p>| Nie | 

Zobacz [definicji skryptu SearchLogProcessing.txt](#sample-u-sql-script) hello definicji skryptu. 

## <a name="sample-input-and-output-datasets"></a>Przykładowe dane wejściowe i wyjściowe zestawy danych
### <a name="input-dataset"></a>Wejściowy zestaw danych
W tym przykładzie danych wejściowych hello znajduje się w usłudze Azure Data Lake Store (plik SearchLog.tsv plik w folderze datalake/wprowadzania hello). 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a>Wyjściowy zestaw danych
W tym przykładzie danych wyjściowych hello utworzonego przez hello skryptu U-SQL jest przechowywane w Azure Data Lake Store (datalake/wyjścia folder). 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a>Przykładowe Data Lake Store połączona usługa
Oto definicji hello próbki hello Azure Data Lake Store połączonej usługi używana przez zestaw danych hello wejścia/wyjścia. 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

Zobacz [przenieść tooand danych z usługi Azure Data Lake Store](data-factory-azure-datalake-connector.md) artykułu Opis właściwości JSON. 

## <a name="sample-u-sql-script"></a>Przykładowy skrypt U-SQL

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

Witaj wartości  **@in**  i  **@out**  Parametry skryptu U-SQL hello są przekazywane dynamicznie przez ADF z sekcją "parameters" hello. Zobacz sekcję "parameters" hello w definicji potoku hello.

Inne właściwości, takie jak degreeOfParallelism i priorytet można określić również w definicji potoku prac hello działające na powitania usługi Azure Data Lake Analytics.

## <a name="dynamic-parameters"></a>Parametry dynamiczne
W definicji potoku próbki hello i wylogowywanie parametry są przypisywane z zakodowanych wartości. 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

Zamiast niego jest możliwe toouse parametrów dynamicznych. Na przykład: 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

W takim przypadku pliki wejściowe nadal są pobierane z folderu /datalake/input hello i pliki wyjściowe są generowane w folderze /datalake/output hello. nazwy plików Hello są dynamiczne na podstawie czasu rozpoczęcia hello wycinka.  

