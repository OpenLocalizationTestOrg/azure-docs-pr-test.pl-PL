---
title: "aaaGet wprowadzenie do usługi Data Lake Analytics przy użyciu interfejsu API REST | Dokumentacja firmy Microsoft"
description: "Użyj interfejsów API REST WebHDFS tooperform operacji na usługi Data Lake Analytics"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a>Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu interfejsów API REST
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Dowiedz się, jak toouse interfejsów API REST WebHDFS i Data Lake Analytics REST API toomanage usługi Data Lake Analytics kont, zadania i w katalogu. 

## <a name="prerequisites"></a>Wymagania wstępne
* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Utworzenie aplikacji usługi Azure Active Directory**. Używasz hello Azure AD aplikacji tooauthenticate hello usługi Data Lake Analytics aplikacji z usługą Azure AD. Istnieją różne podejścia tooauthenticate z usługą Azure AD, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**. Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniony przez usługi Data Lake Analytics przy użyciu usługi Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). W tym artykule wykorzystano toodemonstrate cURL jak wywołuje toomake interfejsu API REST względem konta usługi Data Lake Analytics.

## <a name="authenticate-with-azure-active-directory"></a>Uwierzytelnianie za pomocą usługi Azure Active Directory
Istnieją dwie metody uwierzytelniania za pomocą usługi Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Uwierzytelnianie użytkowników końcowych (interakcyjne)
Za pomocą tej metody, aplikacja wyświetli monit hello toolog użytkownika w i wszystkie operacje hello są wykonywane w kontekście hello hello użytkownika. 

Wykonaj następujące kroki, aby przeprowadzić uwierzytelnianie interakcyjne:

1. Za pomocą aplikacji Przekieruj toohello użytkownika hello następującego adresu URL:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<Identyfikator URI PRZEKIEROWANIA > musi toobe zakodowanego do użycia w adresie URL. Dlatego w celu zapisania adresu https://localhost użyj ciągu `https%3A%2F%2Flocalhost`
   > 
   > 
   
    Hello w celu tego samouczka możesz zastąpić symbole zastępcze hello w adresie URL hello powyżej i wklej go w pasku adresu przeglądarki sieci web. Będzie przekierowany tooauthenticate przy użyciu logowania do systemu Azure. Gdy pomyślnie się zalogujesz, odpowiedź hello jest wyświetlany w pasku adresu przeglądarki hello. odpowiedź Hello będą hello następującego formatu:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Przechwyć hello kod autoryzacji z odpowiedzi hello. W tym samouczku możesz skopiować kod autoryzacji hello z paska adresu przeglądarki sieci web hello hello i przekazać go w hello POST żądania toohello punktu końcowego tokena, jak pokazano poniżej:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > W takim przypadku hello \<REDIRECT-URI > nie trzeba kodować.
   > 
   > 
3. odpowiedź Hello jest obiekt JSON, który zawiera token dostępu (np. `"access_token": "<ACCESS_TOKEN>"`) oraz token odświeżania (np. `"refresh_token": "<REFRESH_TOKEN>"`). Aplikacja używa tokenu dostępu hello podczas uzyskiwania dostępu do usługi Azure Data Lake Store i tooget token odświeżania hello inny token dostępu po wygaśnięciu tokenu dostępu.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Po wygaśnięciu tokenu dostępu hello mogą żądać tokenu dostępu przy użyciu tokenu odświeżania hello, jak pokazano poniżej:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Więcej informacji na temat interakcyjnego uwierzytelniania użytkownika zawiera temat [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx) (Przepływ udzielania kodu autoryzacji).

### <a name="service-to-service-authentication-non-interactive"></a>Uwierzytelnianie między usługami (nieinterakcyjne)
Metoda ta aplikacja udostępnia własne poświadczenia tooperform hello operacji. W tym celu należy wygenerować żądanie POST, tak jak pokazano poniżej hello: 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

Witaj dane wyjściowe tego żądania będą zawierać token autoryzacji (wskazywane przez `access-token` w danych wyjściowych hello poniżej), który można następnie będzie przekazywany w wywołaniach interfejsu API REST. Zapisz ten token uwierzytelniania w pliku tekstowym. Będzie on potrzebny w dalszej części tego artykułu.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

W tym artykule wykorzystano hello **nieinterakcyjnym** podejście. Aby uzyskać więcej informacji na podejścia nieinterakcyjnego (wywołań service-to-service), zobacz [wywołania tooservice przy użyciu poświadczeń usługi](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-analytics-account"></a>Tworzenie konta Data Lake Analytics
Aby można było utworzyć konto usługi Data Lake Analytics, należy najpierw utworzyć grupę zasobów platformy Azure i konto usługi Data Lake Store.  Zobacz [Tworzenie konta usługi Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).

Witaj, jak po pokazuje polecenia Curl toocreate konta:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

Zastąp \< `REDACTED` \> tokenem autoryzacji hello \< `AzureSubscriptionID` \> z Identyfikatorem subskrypcji \< `AzureResourceGroupName` \> z istniejącym zasobem platformy Azure Nazwa grupy i \< `NewAzureDataLakeAnalyticsAccountName` \> z nową nazwą konta usługi Data Lake Analytics. Witaj ładunku żądania dla tego polecenia jest zawarty w hello **CreateDatalakeAnalyticsAccountRequest.json** pliku dostarczonego dla hello `-d` parametru powyżej. Witaj zawartość pliku input.json hello przypominać następujące hello:

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a>Wyświetlanie listy kont usługi Data Lake Analytics w subskrypcji
Witaj następującego polecenia Curl pokazuje, jak toolist kont w ramach subskrypcji:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

Zastąp \< `REDACTED` \> tokenem autoryzacji hello \< `AzureSubscriptionID` \> z identyfikatorem subskrypcji Witaj wynik jest podobny do:

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a>Uzyskiwanie informacji o koncie usługi Data Lake Analytics
Witaj, jak po pokazuje polecenia Curl tooget informacje o koncie:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

Zastąp \< `REDACTED` \> tokenem autoryzacji hello \< `AzureSubscriptionID` \> z Identyfikatorem subskrypcji \< `AzureResourceGroupName` \> z istniejącym zasobem platformy Azure Nazwa grupy i \< `DataLakeAnalyticsAccountName` \> o nazwie hello istniejącego konta Data Lake Analytics. Witaj wynik jest podobny do:

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a>Wyświetlanie listy magazynów usługi Data Lake Store na koncie usługi Data Lake Analytics
Witaj następującego polecenia Curl pokazuje, jak magazyny toolist Data Lake konta:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

Zastąp \< `REDACTED` \> tokenem autoryzacji hello \< `AzureSubscriptionID` \> z Identyfikatorem subskrypcji \< `AzureResourceGroupName` \> z istniejącym zasobem platformy Azure Nazwa grupy i \< `DataLakeAnalyticsAccountName` \> o nazwie hello istniejącego konta Data Lake Analytics. Witaj wynik jest podobny do:

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a>Przesyłanie zadań U-SQL
Witaj, jak po pokazuje polecenia Curl zadania toosubmit U-SQL:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

Zastąp \< `REDACTED` \> tokenem autoryzacji hello \< `DataLakeAnalyticsAccountName` \> o nazwie hello istniejącego konta Data Lake Analytics. Witaj ładunku żądania dla tego polecenia jest zawarty w hello **SubmitADLAJob.json** pliku dostarczonego dla hello `-d` parametru powyżej. Witaj zawartość pliku input.json hello przypominać następujące hello:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

Witaj wynik jest podobny do:

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a>Wyświetlenie listy zadań U-SQL
Witaj, jak po pokazuje polecenia Curl zadania toolist U-SQL:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

Zastąp \< `REDACTED` \> tokenem autoryzacji hello i \< `DataLakeAnalyticsAccountName` \> o nazwie hello istniejącego konta Data Lake Analytics. 

Witaj wynik jest podobny do:

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a>Pobieranie elementów katalogu
Witaj następującego polecenia Curl pokazuje, jak bazy danych hello tooget z hello katalogu:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

Witaj wynik jest podobny do:

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a>Zobacz też
* toosee bardziej złożonego zapytania, zobacz [witryny sieci Web analizowanie dzienników przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).
* tooget Rozpoczęto tworzenie aplikacji U-SQL, zobacz [skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn U-SQL, zobacz [wprowadzenie do języka Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).
* Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).
* Zobacz tooget Przegląd usługi Data Lake Analytics [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).
* toosee hello sam samouczek przy użyciu innych narzędzi, kliknij przycisk hello selektor karty w górnej części hello hello strony.

