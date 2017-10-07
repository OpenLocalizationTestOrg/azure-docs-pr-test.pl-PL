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
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="2526a-103">Analiza dzienników dziennika wyszukiwania interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="2526a-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="2526a-104">Ten przewodnik zawiera podstawowe — samouczek, włącznie z przykładami, jak używasz hello interfejsu API REST Search analizy dziennika.</span><span class="sxs-lookup"><span data-stu-id="2526a-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="2526a-105">Analiza dzienników jest częścią hello Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="2526a-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="2526a-106">Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), a następnie należy kontynuować język zapytań starszych hello toouse z wyszukiwania dziennika hello interfejsu API, zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="2526a-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="2526a-107">Nowy interfejs API, które zostaną wydane dla uaktualnionego obszarów roboczych i dokumentacji hello zostanie zaktualizowany w tym czasie.</span><span class="sxs-lookup"><span data-stu-id="2526a-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="2526a-108">Analiza dzienników była wcześniej określana usługi Operational Insights, dlatego jest hello nazwę używaną w hello dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="2526a-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="2526a-109">Omówienie hello interfejsu API REST wyszukiwania dziennika</span><span class="sxs-lookup"><span data-stu-id="2526a-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="2526a-110">Witaj interfejsu API REST Search analizy dziennika jest RESTful i jest możliwy za pośrednictwem hello interfejsu API usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2526a-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="2526a-111">W tym artykule przedstawiono przykłady uzyskiwania dostępu do interfejsu API hello za pośrednictwem [ARMClient](https://github.com/projectkudu/ARMClient), narzędzie wiersza polecenia typu open source, które upraszcza wywoływania hello interfejsu API usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2526a-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="2526a-112">Użycie Hello ARMClient jest jedną z wielu opcji hello tooaccess interfejsu API Search analizy dziennika.</span><span class="sxs-lookup"><span data-stu-id="2526a-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="2526a-113">Innym rozwiązaniem jest modułu Azure PowerShell hello toouse dla OperationalInsights, który oferuje polecenia cmdlet do uzyskiwania dostępu do wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2526a-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="2526a-114">Z tych narzędzi można wykorzystywać hello wywołania interfejsu API usługi Azure Resource Manager toomake obszarów roboczych o tooOMS i wykonywać polecenia wyszukiwania w nich.</span><span class="sxs-lookup"><span data-stu-id="2526a-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="2526a-115">Hello interfejsu API wyświetla wyniki wyszukiwania w formacie JSON, umożliwiając wyniki wyszukiwania hello toouse na wiele różnych sposobów programowo.</span><span class="sxs-lookup"><span data-stu-id="2526a-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="2526a-116">Witaj usługi Azure Resource Manager może służyć za pośrednictwem [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) i hello [interfejsu API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="2526a-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="2526a-117">toolearn więcej, przejrzyj hello połączonych stron sieci web.</span><span class="sxs-lookup"><span data-stu-id="2526a-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="2526a-118">Użycie agregacji polecenia takie jak `|measure count()` lub `distinct`, każdy toosearch wywołanie może zwrócić maksymalnie 500 000 rekordów.</span><span class="sxs-lookup"><span data-stu-id="2526a-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="2526a-119">Wyszukiwania, które nie zawierają polecenia agregacji zwraca maksymalnie 5000 rekordów.</span><span class="sxs-lookup"><span data-stu-id="2526a-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="2526a-120">Podstawowy samouczek interfejsu API REST Search analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="2526a-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="2526a-121">toouse ARMClient</span><span class="sxs-lookup"><span data-stu-id="2526a-121">toouse ARMClient</span></span>
1. <span data-ttu-id="2526a-122">Zainstaluj [Chocolatey](https://chocolatey.org/), która jest Otwórz Menedżera pakietu źródłowego dla systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="2526a-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="2526a-123">Otwórz okno Wiersz polecenia jako administrator, a następnie uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2526a-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="2526a-124">Zainstaluj ARMClient, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="2526a-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="2526a-125">tooperform wyszukiwany przy użyciu ARMClient</span><span class="sxs-lookup"><span data-stu-id="2526a-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="2526a-126">Zaloguj się za pomocą konta Microsoft lub konta służbowego:</span><span class="sxs-lookup"><span data-stu-id="2526a-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="2526a-127">Pomyślne logowanie zawiera listę wszystkich toohello subskrypcji powiązane z danego konta:</span><span class="sxs-lookup"><span data-stu-id="2526a-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="2526a-128">Pobierz obszary robocze Operations Management Suite hello:</span><span class="sxs-lookup"><span data-stu-id="2526a-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="2526a-129">Pomyślne wywołanie Get czy danych wyjściowych wszystkie obszary robocze powiązane toohello subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="2526a-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

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
3. <span data-ttu-id="2526a-130">Utwórz zmiennej użytkownika wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="2526a-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="2526a-131">Wyszukiwanie za pomocą do nowej zmiennej wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="2526a-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="2526a-132">Zaloguj się przykłady odwołanie do interfejsu API REST wyszukiwania analityka</span><span class="sxs-lookup"><span data-stu-id="2526a-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="2526a-133">Hello następujące przykłady pokazują, jak można korzystać hello wyszukiwania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2526a-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="2526a-134">Wyszukiwanie — Akcja/Odczyt</span><span class="sxs-lookup"><span data-stu-id="2526a-134">Search - Action/Read</span></span>
<span data-ttu-id="2526a-135">**Przykładowy adres Url:**</span><span class="sxs-lookup"><span data-stu-id="2526a-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="2526a-136">**Żądanie:**</span><span class="sxs-lookup"><span data-stu-id="2526a-136">**Request:**</span></span>

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
<span data-ttu-id="2526a-137">Witaj w poniższej tabeli opisano właściwości hello, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="2526a-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="2526a-138">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="2526a-138">**Property**</span></span> | <span data-ttu-id="2526a-139">**Opis**</span><span class="sxs-lookup"><span data-stu-id="2526a-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="2526a-140">Do góry</span><span class="sxs-lookup"><span data-stu-id="2526a-140">top</span></span> |<span data-ttu-id="2526a-141">Witaj maksymalna liczba wyników tooreturn.</span><span class="sxs-lookup"><span data-stu-id="2526a-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="2526a-142">Wyróżnij</span><span class="sxs-lookup"><span data-stu-id="2526a-142">highlight</span></span> |<span data-ttu-id="2526a-143">Zawiera parametry przed i po używane zwykle do wyróżnianie pasujących pól</span><span class="sxs-lookup"><span data-stu-id="2526a-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="2526a-144">wstępnie</span><span class="sxs-lookup"><span data-stu-id="2526a-144">pre</span></span> |<span data-ttu-id="2526a-145">Prefiksy hello podane pola tooyour dopasowany ciąg.</span><span class="sxs-lookup"><span data-stu-id="2526a-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="2526a-146">POST</span><span class="sxs-lookup"><span data-stu-id="2526a-146">post</span></span> |<span data-ttu-id="2526a-147">Dołącza podane pola tooyour dopasowany ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="2526a-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="2526a-148">query</span><span class="sxs-lookup"><span data-stu-id="2526a-148">query</span></span> |<span data-ttu-id="2526a-149">zapytania wyszukiwania Hello używane toocollect i zwracają wyniki.</span><span class="sxs-lookup"><span data-stu-id="2526a-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="2526a-150">rozpoczynanie</span><span class="sxs-lookup"><span data-stu-id="2526a-150">start</span></span> |<span data-ttu-id="2526a-151">Początek Hello hello odcinek czasu ma toobe wyników znalezionych w.</span><span class="sxs-lookup"><span data-stu-id="2526a-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="2526a-152">Koniec</span><span class="sxs-lookup"><span data-stu-id="2526a-152">end</span></span> |<span data-ttu-id="2526a-153">koniec Hello hello odcinek czasu ma toobe wyników znalezionych w.</span><span class="sxs-lookup"><span data-stu-id="2526a-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="2526a-154">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="2526a-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="2526a-155">Wyszukiwanie i {ID} - odczytu akcji</span><span class="sxs-lookup"><span data-stu-id="2526a-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="2526a-156">**Zawartość hello żądanie zapisane wyszukiwania:**</span><span class="sxs-lookup"><span data-stu-id="2526a-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="2526a-157">Jeżeli hello wyszukiwania zwraca ze stanem "Oczekujące", sondowania hello zaktualizowane wyniki, możesz to zrobić za pośrednictwem tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="2526a-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="2526a-158">Po 6 min hello wynik wyszukiwania hello zostanie usunięty z pamięci podręcznej hello i usunięty HTTP zostanie zwrócony.</span><span class="sxs-lookup"><span data-stu-id="2526a-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="2526a-159">Hello początkowego żądania wyszukiwania natychmiast zwraca stan "Powiodło się", hello wyniki nie zostaną dodane toohello pamięci podręcznej spowodować to tooreturn interfejsu API nie ma HTTP, jeśli zapytanie.</span><span class="sxs-lookup"><span data-stu-id="2526a-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="2526a-160">zawartość Hello wynik 200 protokołu HTTP jest w hello takiego samego formatu jak hello początkowe wyszukiwanie żądania tylko ze zaktualizowanymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="2526a-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="2526a-161">Zapisane wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="2526a-161">Saved searches</span></span>
<span data-ttu-id="2526a-162">**Żądania listy zapisanych wyszukiwań:**</span><span class="sxs-lookup"><span data-stu-id="2526a-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="2526a-163">Obsługiwane metody: GET, PUT usunąć</span><span class="sxs-lookup"><span data-stu-id="2526a-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="2526a-164">Obsługiwane metody kolekcji: GET</span><span class="sxs-lookup"><span data-stu-id="2526a-164">Supported collection methods: GET</span></span>

<span data-ttu-id="2526a-165">Witaj w poniższej tabeli opisano właściwości hello, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="2526a-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="2526a-166">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2526a-166">Property</span></span> | <span data-ttu-id="2526a-167">Opis</span><span class="sxs-lookup"><span data-stu-id="2526a-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2526a-168">Identyfikator</span><span class="sxs-lookup"><span data-stu-id="2526a-168">Id</span></span> |<span data-ttu-id="2526a-169">Witaj Unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="2526a-169">hello unique identifier.</span></span> |
| <span data-ttu-id="2526a-170">Element etag</span><span class="sxs-lookup"><span data-stu-id="2526a-170">Etag</span></span> |<span data-ttu-id="2526a-171">**Wymagane poprawki**.</span><span class="sxs-lookup"><span data-stu-id="2526a-171">**Required for Patch**.</span></span> <span data-ttu-id="2526a-172">Zaktualizowany przez serwer podczas każdego zapisu.</span><span class="sxs-lookup"><span data-stu-id="2526a-172">Updated by server on each write.</span></span> <span data-ttu-id="2526a-173">Wartość musi być równa toohello bieżącej przechowywana wartość lub ' *' tooupdate.</span><span class="sxs-lookup"><span data-stu-id="2526a-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="2526a-174">409 zwracane wartości stary lub jest ono nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="2526a-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="2526a-175">Properties.Query</span><span class="sxs-lookup"><span data-stu-id="2526a-175">properties.query</span></span> |<span data-ttu-id="2526a-176">**Wymagane**.</span><span class="sxs-lookup"><span data-stu-id="2526a-176">**Required**.</span></span> <span data-ttu-id="2526a-177">Witaj zapytania wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2526a-177">hello search query.</span></span> |
| <span data-ttu-id="2526a-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="2526a-178">properties.displayName</span></span> |<span data-ttu-id="2526a-179">**Wymagane**.</span><span class="sxs-lookup"><span data-stu-id="2526a-179">**Required**.</span></span> <span data-ttu-id="2526a-180">Nazwa wyświetlana użytkownika Hello hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="2526a-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="2526a-181">Properties.category</span><span class="sxs-lookup"><span data-stu-id="2526a-181">properties.category</span></span> |<span data-ttu-id="2526a-182">**Wymagane**.</span><span class="sxs-lookup"><span data-stu-id="2526a-182">**Required**.</span></span> <span data-ttu-id="2526a-183">Kategoria użytkownika Hello hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="2526a-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="2526a-184">Witaj API wyszukiwania usługi Analiza dzienników zwraca aktualnie utworzonych przez użytkownika zapisane wyszukiwania podczas sondowania zapisane wyszukiwania w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="2526a-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="2526a-185">Witaj interfejsu API nie zwraca zapisanych wyszukiwań udostępniane przez rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="2526a-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="2526a-186">Tworzenie zapisanych wyszukiwań</span><span class="sxs-lookup"><span data-stu-id="2526a-186">Create saved searches</span></span>
<span data-ttu-id="2526a-187">**Żądanie:**</span><span class="sxs-lookup"><span data-stu-id="2526a-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="2526a-188">Nazwa Hello wszystkie zapisane wyszukiwania, harmonogramów i działania utworzone za pomocą hello API analizy dziennika musi być pisane małymi literami.</span><span class="sxs-lookup"><span data-stu-id="2526a-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="2526a-189">Usuń zapisane wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="2526a-189">Delete saved searches</span></span>
<span data-ttu-id="2526a-190">**Żądanie:**</span><span class="sxs-lookup"><span data-stu-id="2526a-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="2526a-191">Aktualizowanie zapisanych wyszukiwań</span><span class="sxs-lookup"><span data-stu-id="2526a-191">Update saved searches</span></span>
 <span data-ttu-id="2526a-192">**Żądanie:**</span><span class="sxs-lookup"><span data-stu-id="2526a-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="2526a-193">Metadane — tylko w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="2526a-193">Metadata - JSON only</span></span>
<span data-ttu-id="2526a-194">Poniżej przedstawiono sposób wyświetlania pól hello toosee dla wszystkich typów dziennika hello danych zebranych w obszarze roboczym.</span><span class="sxs-lookup"><span data-stu-id="2526a-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="2526a-195">Na przykład jeśli chcesz się, że wiesz, że jeśli hello typ zdarzenia zawiera pole o nazwie komputera to zapytanie jest jednokierunkowej toocheck.</span><span class="sxs-lookup"><span data-stu-id="2526a-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="2526a-196">**Żądanie dla pola:**</span><span class="sxs-lookup"><span data-stu-id="2526a-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="2526a-197">**Odpowiedź:**</span><span class="sxs-lookup"><span data-stu-id="2526a-197">**Response:**</span></span>

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

<span data-ttu-id="2526a-198">Witaj w poniższej tabeli opisano właściwości hello, które są dostępne.</span><span class="sxs-lookup"><span data-stu-id="2526a-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="2526a-199">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="2526a-199">**Property**</span></span> | <span data-ttu-id="2526a-200">**Opis**</span><span class="sxs-lookup"><span data-stu-id="2526a-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="2526a-201">name</span><span class="sxs-lookup"><span data-stu-id="2526a-201">name</span></span> |<span data-ttu-id="2526a-202">Nazwa pola.</span><span class="sxs-lookup"><span data-stu-id="2526a-202">Field name.</span></span> |
| <span data-ttu-id="2526a-203">Nazwa wyświetlana</span><span class="sxs-lookup"><span data-stu-id="2526a-203">displayName</span></span> |<span data-ttu-id="2526a-204">Nazwa pola hello wyświetlana Hello.</span><span class="sxs-lookup"><span data-stu-id="2526a-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="2526a-205">type</span><span class="sxs-lookup"><span data-stu-id="2526a-205">type</span></span> |<span data-ttu-id="2526a-206">Typ wartości pola hello Hello.</span><span class="sxs-lookup"><span data-stu-id="2526a-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="2526a-207">Tworzenie aspektów</span><span class="sxs-lookup"><span data-stu-id="2526a-207">facetable</span></span> |<span data-ttu-id="2526a-208">Kombinacja bieżącego indeksowane, "przechowywane" i właściwości "aspektu".</span><span class="sxs-lookup"><span data-stu-id="2526a-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="2526a-209">Wyświetl</span><span class="sxs-lookup"><span data-stu-id="2526a-209">display</span></span> |<span data-ttu-id="2526a-210">Bieżący właściwości "display".</span><span class="sxs-lookup"><span data-stu-id="2526a-210">Current ‘display’ property.</span></span> <span data-ttu-id="2526a-211">Wartość true, jeśli pole jest widoczne w obszarze wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2526a-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="2526a-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="2526a-212">ownerType</span></span> |<span data-ttu-id="2526a-213">Typy zmniejszenie tooonly należących tooonboarded IP.</span><span class="sxs-lookup"><span data-stu-id="2526a-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="2526a-214">Parametry opcjonalne</span><span class="sxs-lookup"><span data-stu-id="2526a-214">Optional parameters</span></span>
<span data-ttu-id="2526a-215">Witaj następujących informacji opisano dostępne następujące parametry opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="2526a-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="2526a-216">Wyróżnianie</span><span class="sxs-lookup"><span data-stu-id="2526a-216">Highlighting</span></span>
<span data-ttu-id="2526a-217">Parametr "Highlight" Hello jest opcjonalny parametr może używać podsystem usługi wyszukiwanie hello toorequest obejmują zestaw znaczników w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="2526a-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="2526a-218">Te znaczniki wskazują hello rozpoczęcia i zakończenia zaznaczony tekst, który pasuje warunki hello podane w kwerendzie wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2526a-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="2526a-219">Może określić hello start i kończyć znaczniki, które są używane przez hello wyróżnione toowrap wyszukiwany.</span><span class="sxs-lookup"><span data-stu-id="2526a-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="2526a-220">**Przykładowe zapytanie wyszukiwania**</span><span class="sxs-lookup"><span data-stu-id="2526a-220">**Example search query**</span></span>

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

<span data-ttu-id="2526a-221">**Przykładowe wyniki:**</span><span class="sxs-lookup"><span data-stu-id="2526a-221">**Sample result:**</span></span>

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

<span data-ttu-id="2526a-222">Należy zauważyć, że hello wyniku poprzedniej zawiera komunikat o błędzie i jest poprzedzony a dołączone.</span><span class="sxs-lookup"><span data-stu-id="2526a-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="2526a-223">Grupy komputerów</span><span class="sxs-lookup"><span data-stu-id="2526a-223">Computer groups</span></span>
<span data-ttu-id="2526a-224">Grupy komputerów są specjalne zapisanych wyszukiwań, które zwracają zestaw komputerów.</span><span class="sxs-lookup"><span data-stu-id="2526a-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="2526a-225">W innych zapytań toolimit hello wyniki toohello komputerów w grupie hello można użyć grupy komputerów.</span><span class="sxs-lookup"><span data-stu-id="2526a-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="2526a-226">Grupa komputerów jest implementowany jako zapisanego kryterium wyszukiwania z tagiem grupy o wartości komputera.</span><span class="sxs-lookup"><span data-stu-id="2526a-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="2526a-227">Poniżej znajduje się przykładowa odpowiedź dla grupy komputerów.</span><span class="sxs-lookup"><span data-stu-id="2526a-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="2526a-228">Pobieranie grupy komputerów</span><span class="sxs-lookup"><span data-stu-id="2526a-228">Retrieving computer groups</span></span>
<span data-ttu-id="2526a-229">tooretrieve nazwę grupy komputerów, użyj hello metody Get z grupą hello.</span><span class="sxs-lookup"><span data-stu-id="2526a-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="2526a-230">Tworzenie lub aktualizowanie grupy komputerów</span><span class="sxs-lookup"><span data-stu-id="2526a-230">Creating or updating a computer group</span></span>
<span data-ttu-id="2526a-231">toocreate grupy komputerów, użyj hello metody Put identyfikator unikatowy zapisanego kryterium wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2526a-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="2526a-232">Użycie istniejącego Identyfikatora grupy komputerów, co jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="2526a-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="2526a-233">Po utworzeniu grupy komputerów w portalu usługi Analiza dzienników hello identyfikator hello jest tworzony z hello grupy i nazwy.</span><span class="sxs-lookup"><span data-stu-id="2526a-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="2526a-234">kwerendy Hello używana do definicja grupy hello musi zwracać zestaw komputerów dla toofunction grupy hello poprawnie.</span><span class="sxs-lookup"><span data-stu-id="2526a-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="2526a-235">Zaleca się kończyć się zapytanie o `| Distinct Computer` hello tooensure poprawne dane są zwracane.</span><span class="sxs-lookup"><span data-stu-id="2526a-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="2526a-236">Definicja Hello hello zapisanego wyszukiwania musi zawierać tag o nazwie grupy o wartości komputera toobe wyszukiwania hello sklasyfikowane jako grupę komputerów.</span><span class="sxs-lookup"><span data-stu-id="2526a-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="2526a-237">Usuwanie grupy komputerów</span><span class="sxs-lookup"><span data-stu-id="2526a-237">Deleting computer groups</span></span>
<span data-ttu-id="2526a-238">toodelete nazwę grupy komputerów, użyj hello metody Delete z grupą hello.</span><span class="sxs-lookup"><span data-stu-id="2526a-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="2526a-239">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2526a-239">Next steps</span></span>
* <span data-ttu-id="2526a-240">Dowiedz się więcej o [dziennika wyszukiwania](log-analytics-log-searches.md) toobuild zapytania przy użyciu pól niestandardowych kryteriów.</span><span class="sxs-lookup"><span data-stu-id="2526a-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
