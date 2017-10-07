---
title: aaaLog analizy dziennika wyszukiwania interfejsu API REST | Dokumentacja firmy Microsoft
description: "Ten przewodnik zawiera podstawowe opisujące, jak używasz hello samouczek analizy dzienników wyszukiwania interfejsu API REST hello Operations Management Suite (OMS) i zapewnia przykłady pokazujące jak toouse hello poleceń."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a>Analiza dzienników dziennika wyszukiwania interfejsu API REST
Ten przewodnik zawiera podstawowe — samouczek, włącznie z przykładami, jak używasz hello interfejsu API REST Search analizy dziennika. Analiza dzienników jest częścią hello Operations Management Suite (OMS).

> [!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), a następnie należy kontynuować język zapytań starszych hello toouse z wyszukiwania dziennika hello interfejsu API, zgodnie z opisem w tym artykule.  Nowy interfejs API, które zostaną wydane dla uaktualnionego obszarów roboczych i dokumentacji hello zostanie zaktualizowany w tym czasie. 

> [!NOTE]
> Analiza dzienników była wcześniej określana usługi Operational Insights, dlatego jest hello nazwę używaną w hello dostawcy zasobów.
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Omówienie hello interfejsu API REST wyszukiwania dziennika
Witaj interfejsu API REST Search analizy dziennika jest RESTful i jest możliwy za pośrednictwem hello interfejsu API usługi Azure Resource Manager. W tym artykule przedstawiono przykłady uzyskiwania dostępu do interfejsu API hello za pośrednictwem [ARMClient](https://github.com/projectkudu/ARMClient), narzędzie wiersza polecenia typu open source, które upraszcza wywoływania hello interfejsu API usługi Azure Resource Manager. Użycie Hello ARMClient jest jedną z wielu opcji hello tooaccess interfejsu API Search analizy dziennika. Innym rozwiązaniem jest modułu Azure PowerShell hello toouse dla OperationalInsights, który oferuje polecenia cmdlet do uzyskiwania dostępu do wyszukiwania. Z tych narzędzi można wykorzystywać hello wywołania interfejsu API usługi Azure Resource Manager toomake obszarów roboczych o tooOMS i wykonywać polecenia wyszukiwania w nich. Hello interfejsu API wyświetla wyniki wyszukiwania w formacie JSON, umożliwiając wyniki wyszukiwania hello toouse na wiele różnych sposobów programowo.

Witaj usługi Azure Resource Manager może służyć za pośrednictwem [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) i hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx). toolearn więcej, przejrzyj hello połączonych stron sieci web.

> [!NOTE]
> Użycie agregacji polecenia takie jak `|measure count()` lub `distinct`, każdy toosearch wywołanie może zwrócić maksymalnie 500 000 rekordów. Wyszukiwania, które nie zawierają polecenia agregacji zwraca maksymalnie 5000 rekordów.
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>Podstawowy samouczek interfejsu API REST Search analizy dzienników
### <a name="toouse-armclient"></a>toouse ARMClient
1. Zainstaluj [Chocolatey](https://chocolatey.org/), która jest Otwórz Menedżera pakietu źródłowego dla systemu Windows. Otwórz okno Wiersz polecenia jako administrator, a następnie uruchom następujące polecenie hello:

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. Zainstaluj ARMClient, uruchamiając następujące polecenie hello:

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>tooperform wyszukiwany przy użyciu ARMClient
1. Zaloguj się za pomocą konta Microsoft lub konta służbowego:

    ```
    armclient login
    ```

    Pomyślne logowanie zawiera listę wszystkich toohello subskrypcji powiązane z danego konta:

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. Pobierz obszary robocze Operations Management Suite hello:

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    Pomyślne wywołanie Get czy danych wyjściowych wszystkie obszary robocze powiązane toohello subskrypcji:

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. Utwórz zmiennej użytkownika wyszukiwania:

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. Wyszukiwanie za pomocą do nowej zmiennej wyszukiwania:

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Zaloguj się przykłady odwołanie do interfejsu API REST wyszukiwania analityka
Hello następujące przykłady pokazują, jak można korzystać hello wyszukiwania interfejsu API.

### <a name="search---actionread"></a>Wyszukiwanie — Akcja/Odczyt
**Przykładowy adres Url:**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**Żądanie:**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
Witaj w poniższej tabeli opisano właściwości hello, które są dostępne.

| **Właściwość** | **Opis** |
| --- | --- |
| Do góry |Witaj maksymalna liczba wyników tooreturn. |
| Wyróżnij |Zawiera parametry przed i po używane zwykle do wyróżnianie pasujących pól |
| wstępnie |Prefiksy hello podane pola tooyour dopasowany ciąg. |
| POST |Dołącza podane pola tooyour dopasowany ciąg hello. |
| query |zapytania wyszukiwania Hello używane toocollect i zwracają wyniki. |
| rozpoczynanie |Początek Hello hello odcinek czasu ma toobe wyników znalezionych w. |
| Koniec |koniec Hello hello odcinek czasu ma toobe wyników znalezionych w. |

**Odpowiedź:**

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a>Wyszukiwanie i {ID} - odczytu akcji
**Zawartość hello żądanie zapisane wyszukiwania:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> Jeżeli hello wyszukiwania zwraca ze stanem "Oczekujące", sondowania hello zaktualizowane wyniki, możesz to zrobić za pośrednictwem tego interfejsu API. Po 6 min hello wynik wyszukiwania hello zostanie usunięty z pamięci podręcznej hello i usunięty HTTP zostanie zwrócony. Hello początkowego żądania wyszukiwania natychmiast zwraca stan "Powiodło się", hello wyniki nie zostaną dodane toohello pamięci podręcznej spowodować to tooreturn interfejsu API nie ma HTTP, jeśli zapytanie. zawartość Hello wynik 200 protokołu HTTP jest w hello takiego samego formatu jak hello początkowe wyszukiwanie żądania tylko ze zaktualizowanymi wartościami.
>
>

### <a name="saved-searches"></a>Zapisane wyszukiwania
**Żądania listy zapisanych wyszukiwań:**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

Obsługiwane metody: GET, PUT usunąć

Obsługiwane metody kolekcji: GET

Witaj w poniższej tabeli opisano właściwości hello, które są dostępne.

| Właściwość | Opis |
| --- | --- |
| Identyfikator |Witaj Unikatowy identyfikator. |
| Element etag |**Wymagane poprawki**. Zaktualizowany przez serwer podczas każdego zapisu. Wartość musi być równa toohello bieżącej przechowywana wartość lub ' *' tooupdate. 409 zwracane wartości stary lub jest ono nieprawidłowe. |
| Properties.Query |**Wymagane**. Witaj zapytania wyszukiwania. |
| properties.displayName |**Wymagane**. Nazwa wyświetlana użytkownika Hello hello zapytania. |
| Properties.category |**Wymagane**. Kategoria użytkownika Hello hello zapytania. |

> [!NOTE]
> Witaj API wyszukiwania usługi Analiza dzienników zwraca aktualnie utworzonych przez użytkownika zapisane wyszukiwania podczas sondowania zapisane wyszukiwania w obszarze roboczym. Witaj interfejsu API nie zwraca zapisanych wyszukiwań udostępniane przez rozwiązania.
>
>

### <a name="create-saved-searches"></a>Tworzenie zapisanych wyszukiwań
**Żądanie:**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> Nazwa Hello wszystkie zapisane wyszukiwania, harmonogramów i działania utworzone za pomocą hello API analizy dziennika musi być pisane małymi literami.

### <a name="delete-saved-searches"></a>Usuń zapisane wyszukiwania
**Żądanie:**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>Aktualizowanie zapisanych wyszukiwań
 **Żądanie:**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>Metadane — tylko w formacie JSON
Poniżej przedstawiono sposób wyświetlania pól hello toosee dla wszystkich typów dziennika hello danych zebranych w obszarze roboczym. Na przykład jeśli chcesz się, że wiesz, że jeśli hello typ zdarzenia zawiera pole o nazwie komputera to zapytanie jest jednokierunkowej toocheck.

**Żądanie dla pola:**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**Odpowiedź:**

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

Witaj w poniższej tabeli opisano właściwości hello, które są dostępne.

| **Właściwość** | **Opis** |
| --- | --- |
| name |Nazwa pola. |
| Nazwa wyświetlana |Nazwa pola hello wyświetlana Hello. |
| type |Typ wartości pola hello Hello. |
| Tworzenie aspektów |Kombinacja bieżącego indeksowane, "przechowywane" i właściwości "aspektu". |
| Wyświetl |Bieżący właściwości "display". Wartość true, jeśli pole jest widoczne w obszarze wyszukiwania. |
| ownerType |Typy zmniejszenie tooonly należących tooonboarded IP. |

## <a name="optional-parameters"></a>Parametry opcjonalne
Witaj następujących informacji opisano dostępne następujące parametry opcjonalne.

### <a name="highlighting"></a>Wyróżnianie
Parametr "Highlight" Hello jest opcjonalny parametr może używać podsystem usługi wyszukiwanie hello toorequest obejmują zestaw znaczników w odpowiedzi.

Te znaczniki wskazują hello rozpoczęcia i zakończenia zaznaczony tekst, który pasuje warunki hello podane w kwerendzie wyszukiwania.
Może określić hello start i kończyć znaczniki, które są używane przez hello wyróżnione toowrap wyszukiwany.

**Przykładowe zapytanie wyszukiwania**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

**Przykładowe wyniki:**

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

Należy zauważyć, że hello wyniku poprzedniej zawiera komunikat o błędzie i jest poprzedzony a dołączone.

## <a name="computer-groups"></a>Grupy komputerów
Grupy komputerów są specjalne zapisanych wyszukiwań, które zwracają zestaw komputerów.  W innych zapytań toolimit hello wyniki toohello komputerów w grupie hello można użyć grupy komputerów.  Grupa komputerów jest implementowany jako zapisanego kryterium wyszukiwania z tagiem grupy o wartości komputera.

Poniżej znajduje się przykładowa odpowiedź dla grupy komputerów.

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a>Pobieranie grupy komputerów
tooretrieve nazwę grupy komputerów, użyj hello metody Get z grupą hello.

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>Tworzenie lub aktualizowanie grupy komputerów
toocreate grupy komputerów, użyj hello metody Put identyfikator unikatowy zapisanego kryterium wyszukiwania. Użycie istniejącego Identyfikatora grupy komputerów, co jest modyfikowany. Po utworzeniu grupy komputerów w portalu usługi Analiza dzienników hello identyfikator hello jest tworzony z hello grupy i nazwy.

kwerendy Hello używana do definicja grupy hello musi zwracać zestaw komputerów dla toofunction grupy hello poprawnie.  Zaleca się kończyć się zapytanie o `| Distinct Computer` hello tooensure poprawne dane są zwracane.

Definicja Hello hello zapisanego wyszukiwania musi zawierać tag o nazwie grupy o wartości komputera toobe wyszukiwania hello sklasyfikowane jako grupę komputerów.

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>Usuwanie grupy komputerów
toodelete nazwę grupy komputerów, użyj hello metody Delete z grupą hello.

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) toobuild zapytania przy użyciu pól niestandardowych kryteriów.
