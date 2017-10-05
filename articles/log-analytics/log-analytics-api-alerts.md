---
title: "Przy użyciu pakietu OMS dziennika analizy alertu REST API"
description: "Dziennik analizy alertu interfejsu API REST umożliwia tworzenie i Zarządzanie alertami w analizy dzienników, która jest częścią z Operations Management Suite (OMS).  Ten artykuł zawiera szczegółowe informacje o interfejsie API i kilka przykładów do wykonywania różnych operacji."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5ce72ffef4394bf3bbe39fa420c4fcaa965ae35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="24ae2-104">Tworzenie i zarządzanie nimi reguły alertów w analizy dzienników z interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="24ae2-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="24ae2-105">Dziennik analizy alertu interfejsu API REST umożliwia tworzenie i Zarządzanie alertami w Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="24ae2-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="24ae2-106">Ten artykuł zawiera szczegółowe informacje o interfejsie API i kilka przykładów do wykonywania różnych operacji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-106">This article provides details of the API and several examples for performing different operations.</span></span>

<span data-ttu-id="24ae2-107">Interfejsu API REST Search analizy dziennika jest RESTful i jest dostępny za pośrednictwem interfejsu REST API usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="24ae2-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="24ae2-108">W tym dokumencie można znaleźć przykłady którym dostęp do interfejsu API z wiersza polecenia programu PowerShell przy użyciu [ARMClient](https://github.com/projectkudu/ARMClient), narzędzie wiersza polecenia typu open source, który upraszcza wywoływanie interfejsu API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="24ae2-108">In this document you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="24ae2-109">Korzystanie z programu PowerShell i ARMClient jest jedną z wielu opcji, aby uzyskać dostęp do interfejsu API Search analizy dziennika.</span><span class="sxs-lookup"><span data-stu-id="24ae2-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="24ae2-110">Te narzędzia mogą korzystać z RESTful interfejs API Menedżera zasobów Azure do wykonywania wywołań do obszarów roboczych OMS i wykonywania poleceń wyszukiwania w nich.</span><span class="sxs-lookup"><span data-stu-id="24ae2-110">With these tools you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="24ae2-111">Interfejs API dane wyjściowe obejmują wyniki wyszukiwania do użytkownika w formacie JSON, co umożliwia używanie wyniki wyszukiwania na wiele różnych sposobów programowo.</span><span class="sxs-lookup"><span data-stu-id="24ae2-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24ae2-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="24ae2-112">Prerequisites</span></span>
<span data-ttu-id="24ae2-113">Obecnie usługa alertów można tworzyć tylko z zapisanej operacji wyszukiwania w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="24ae2-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="24ae2-114">Można to sprawdzić [interfejsu API REST wyszukiwania dziennika](log-analytics-log-search-api.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="24ae2-115">Harmonogramy</span><span class="sxs-lookup"><span data-stu-id="24ae2-115">Schedules</span></span>
<span data-ttu-id="24ae2-116">Zapisane wyszukiwanie może mieć co najmniej jeden harmonogram.</span><span class="sxs-lookup"><span data-stu-id="24ae2-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="24ae2-117">Harmonogram Określa, jak często wyszukiwania jest uruchamiania i przedział czasu, w którym określono kryteria.</span><span class="sxs-lookup"><span data-stu-id="24ae2-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span></span>
<span data-ttu-id="24ae2-118">Harmonogramy mają właściwości w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="24ae2-118">Schedules have the properties in the following table.</span></span>

| <span data-ttu-id="24ae2-119">Właściwość</span><span class="sxs-lookup"><span data-stu-id="24ae2-119">Property</span></span> | <span data-ttu-id="24ae2-120">Opis</span><span class="sxs-lookup"><span data-stu-id="24ae2-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="24ae2-121">Interwał</span><span class="sxs-lookup"><span data-stu-id="24ae2-121">Interval</span></span> |<span data-ttu-id="24ae2-122">Jak często jest wykonywane wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="24ae2-122">How often the search is run.</span></span> <span data-ttu-id="24ae2-123">(W minutach).</span><span class="sxs-lookup"><span data-stu-id="24ae2-123">Measured in minutes.</span></span> |
| <span data-ttu-id="24ae2-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="24ae2-124">QueryTimeSpan</span></span> |<span data-ttu-id="24ae2-125">Przedział czasu, w którym jest oceniana kryteria.</span><span class="sxs-lookup"><span data-stu-id="24ae2-125">The time interval over which the criteria is evaluated.</span></span> <span data-ttu-id="24ae2-126">Musi być równa lub większa od wartości interwału.</span><span class="sxs-lookup"><span data-stu-id="24ae2-126">Must be equal to or greater than Interval.</span></span> <span data-ttu-id="24ae2-127">(W minutach).</span><span class="sxs-lookup"><span data-stu-id="24ae2-127">Measured in minutes.</span></span> |
| <span data-ttu-id="24ae2-128">Wersja</span><span class="sxs-lookup"><span data-stu-id="24ae2-128">Version</span></span> |<span data-ttu-id="24ae2-129">Używana wersja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="24ae2-129">The API version being used.</span></span>  <span data-ttu-id="24ae2-130">Obecnie ta powinna zawsze być ustawiona na 1.</span><span class="sxs-lookup"><span data-stu-id="24ae2-130">Currently, this should always be set to 1.</span></span> |

<span data-ttu-id="24ae2-131">Rozważmy na przykład kwerendy zdarzeń z interwałem 15 minut i zakres czasu 30 minut.</span><span class="sxs-lookup"><span data-stu-id="24ae2-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="24ae2-132">W takim przypadku zapytanie zostanie uruchomione co 15 minut, a alert będzie uruchomiony, jeśli kryteria nadal rozpoznać na wartość true w zakres 30 minut.</span><span class="sxs-lookup"><span data-stu-id="24ae2-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="24ae2-133">Trwa pobieranie harmonogramów</span><span class="sxs-lookup"><span data-stu-id="24ae2-133">Retrieving schedules</span></span>
<span data-ttu-id="24ae2-134">Pobierz wszystkie harmonogramy dla zapisanego wyszukiwania za pomocą metody Get.</span><span class="sxs-lookup"><span data-stu-id="24ae2-134">Use the Get method to retrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="24ae2-135">Pobierz konkretny harmonogram dla zapisanego wyszukiwania za pomocą metody Get o identyfikatorze harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="24ae2-136">Poniżej znajduje się przykładowa odpowiedź dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="24ae2-137">Tworzenie harmonogramu</span><span class="sxs-lookup"><span data-stu-id="24ae2-137">Creating a schedule</span></span>
<span data-ttu-id="24ae2-138">Za pomocą metody Put identyfikator unikatowy harmonogram do utworzenia nowego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-138">Use the Put method with a unique schedule ID to create a new schedule.</span></span>  <span data-ttu-id="24ae2-139">Należy zauważyć, że dwa harmonogramy nie może sam identyfikator nawet, jeśli są one powiązane z różnymi zapisane wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="24ae2-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="24ae2-140">Po utworzeniu harmonogramu w konsoli OMS identyfikator GUID jest tworzona dla identyfikator harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="24ae2-141">Nazwa dla wszystkich zapisanych wyszukiwań, harmonogramów i akcje utworzone przy użyciu interfejsu API analizy dziennika musi być pisane małymi literami.</span><span class="sxs-lookup"><span data-stu-id="24ae2-141">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="24ae2-142">Edytowanie harmonogramu</span><span class="sxs-lookup"><span data-stu-id="24ae2-142">Editing a schedule</span></span>
<span data-ttu-id="24ae2-143">Za pomocą metody Put istniejący identyfikator harmonogramu dla tego samego zapisanego wyszukiwania można zmodyfikować tego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-143">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="24ae2-144">Treść żądania musi zawierać element etag harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-144">The body of the request must include the etag of the schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="24ae2-145">Usuwanie harmonogramów</span><span class="sxs-lookup"><span data-stu-id="24ae2-145">Deleting schedules</span></span>
<span data-ttu-id="24ae2-146">Za pomocą metody Delete identyfikator harmonogramu. Aby usunąć harmonogram.</span><span class="sxs-lookup"><span data-stu-id="24ae2-146">Use the Delete method with a schedule ID to delete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="24ae2-147">Akcje</span><span class="sxs-lookup"><span data-stu-id="24ae2-147">Actions</span></span>
<span data-ttu-id="24ae2-148">Harmonogram może mieć wiele akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="24ae2-149">Akcja może określić jeden lub więcej procesów do wykonywania takich jak wysyłanie wiadomości e-mail lub uruchamianie elementu runbook lub mogą określić próg określający, jeśli wyniki wyszukiwania zgodny pewne kryteria.</span><span class="sxs-lookup"><span data-stu-id="24ae2-149">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="24ae2-150">Niektóre akcje definiują zarówno tak, aby procesy są wykonywane po spełnieniu wartość progową.</span><span class="sxs-lookup"><span data-stu-id="24ae2-150">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="24ae2-151">Wszystkie działania mają właściwości w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="24ae2-151">All actions have the properties in the following table.</span></span>  <span data-ttu-id="24ae2-152">Różne typy alertów mają różne dodatkowe właściwości, które są opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="24ae2-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="24ae2-153">Właściwość</span><span class="sxs-lookup"><span data-stu-id="24ae2-153">Property</span></span> | <span data-ttu-id="24ae2-154">Opis</span><span class="sxs-lookup"><span data-stu-id="24ae2-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="24ae2-155">Typ</span><span class="sxs-lookup"><span data-stu-id="24ae2-155">Type</span></span> |<span data-ttu-id="24ae2-156">Typ akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-156">Type of the action.</span></span>  <span data-ttu-id="24ae2-157">Obecnie możliwe wartości to Alert i elementu Webhook.</span><span class="sxs-lookup"><span data-stu-id="24ae2-157">Currently the possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="24ae2-158">Nazwa</span><span class="sxs-lookup"><span data-stu-id="24ae2-158">Name</span></span> |<span data-ttu-id="24ae2-159">Nazwa wyświetlana alertu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-159">Display name for the alert.</span></span> |
| <span data-ttu-id="24ae2-160">Wersja</span><span class="sxs-lookup"><span data-stu-id="24ae2-160">Version</span></span> |<span data-ttu-id="24ae2-161">Używana wersja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="24ae2-161">The API version being used.</span></span>  <span data-ttu-id="24ae2-162">Obecnie ta powinna zawsze być ustawiona na 1.</span><span class="sxs-lookup"><span data-stu-id="24ae2-162">Currently, this should always be set to 1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="24ae2-163">Pobieranie akcji</span><span class="sxs-lookup"><span data-stu-id="24ae2-163">Retrieving actions</span></span>
<span data-ttu-id="24ae2-164">Pobierz wszystkie akcje dla harmonogramu za pomocą metody Get.</span><span class="sxs-lookup"><span data-stu-id="24ae2-164">Use the Get method to retrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="24ae2-165">Za pomocą metody Get identyfikator akcji można pobrać określonej akcji dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-165">Use the Get method with the action ID to retrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="24ae2-166">Tworzenie lub edytowanie akcji</span><span class="sxs-lookup"><span data-stu-id="24ae2-166">Creating or editing actions</span></span>
<span data-ttu-id="24ae2-167">Za pomocą metody Put identyfikator akcji, która jest unikatowa w harmonogramie, aby utworzyć nową akcję.</span><span class="sxs-lookup"><span data-stu-id="24ae2-167">Use the Put method with an action ID that is unique to the schedule to create a new action.</span></span>  <span data-ttu-id="24ae2-168">Po utworzeniu akcji w konsoli OMS identyfikator GUID jest identyfikatora akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-168">When you create an action in the OMS console, a GUID is for the action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="24ae2-169">Nazwa dla wszystkich zapisanych wyszukiwań, harmonogramów i akcje utworzone przy użyciu interfejsu API analizy dziennika musi być pisane małymi literami.</span><span class="sxs-lookup"><span data-stu-id="24ae2-169">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="24ae2-170">Za pomocą metody Put istniejącego Identyfikatora akcji dla tego samego zapisanego wyszukiwania można zmodyfikować tego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-170">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="24ae2-171">Treść żądania musi zawierać element etag harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-171">The body of the request must include the etag of the schedule.</span></span>

<span data-ttu-id="24ae2-172">Format żądania do tworzenia nowej akcji zależy od typu akcji, te przykłady znajdują się w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="24ae2-172">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="24ae2-173">Usuwanie akcji</span><span class="sxs-lookup"><span data-stu-id="24ae2-173">Deleting actions</span></span>
<span data-ttu-id="24ae2-174">Za pomocą metody Delete identyfikator akcji można usunąć akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-174">Use the Delete method with the action ID to delete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="24ae2-175">Akcje alertu</span><span class="sxs-lookup"><span data-stu-id="24ae2-175">Alert Actions</span></span>
<span data-ttu-id="24ae2-176">Harmonogram ma jeden i tylko jeden Alert akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="24ae2-177">Akcje alertu występuje jeden lub kilka z sekcji w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="24ae2-177">Alert actions have one or more of the sections in the following table.</span></span>  <span data-ttu-id="24ae2-178">Każdy jest opisany bardziej szczegółowo poniżej.</span><span class="sxs-lookup"><span data-stu-id="24ae2-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="24ae2-179">Sekcja</span><span class="sxs-lookup"><span data-stu-id="24ae2-179">Section</span></span> | <span data-ttu-id="24ae2-180">Opis</span><span class="sxs-lookup"><span data-stu-id="24ae2-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="24ae2-181">Próg</span><span class="sxs-lookup"><span data-stu-id="24ae2-181">Threshold</span></span> |<span data-ttu-id="24ae2-182">Kryteria po uruchomieniu akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-182">Criteria for when the action is run.</span></span> |
| <span data-ttu-id="24ae2-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="24ae2-183">EmailNotification</span></span> |<span data-ttu-id="24ae2-184">Wysyłanie poczty do wielu adresatów.</span><span class="sxs-lookup"><span data-stu-id="24ae2-184">Send mail to multiple recipients.</span></span> |
| <span data-ttu-id="24ae2-185">Korygowania</span><span class="sxs-lookup"><span data-stu-id="24ae2-185">Remediation</span></span> |<span data-ttu-id="24ae2-186">Uruchom element runbook automatyzacji Azure, aby spróbować rozwiązać problem zidentyfikowane.</span><span class="sxs-lookup"><span data-stu-id="24ae2-186">Start a runbook in Azure Automation to attempt to correct identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="24ae2-187">Progi</span><span class="sxs-lookup"><span data-stu-id="24ae2-187">Thresholds</span></span>
<span data-ttu-id="24ae2-188">Akcja alertu powinna mieć jeden i tylko jeden próg.</span><span class="sxs-lookup"><span data-stu-id="24ae2-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="24ae2-189">Jeśli wyniki zapisanego kryterium wyszukiwania zgodne próg w akcji skojarzonej z tym wyszukiwania, są uruchamiane żadnych innych procesów w tej akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-189">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="24ae2-190">Akcja może również zawierać tylko wartości progowej, aby mogą być używane z akcjami innych typów, które nie zawierają wartości progowe.</span><span class="sxs-lookup"><span data-stu-id="24ae2-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="24ae2-191">Progi mają właściwości w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="24ae2-191">Thresholds have the properties in the following table.</span></span>

| <span data-ttu-id="24ae2-192">Właściwość</span><span class="sxs-lookup"><span data-stu-id="24ae2-192">Property</span></span> | <span data-ttu-id="24ae2-193">Opis</span><span class="sxs-lookup"><span data-stu-id="24ae2-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="24ae2-194">Operator</span><span class="sxs-lookup"><span data-stu-id="24ae2-194">Operator</span></span> |<span data-ttu-id="24ae2-195">Operator porównania wartości progowej.</span><span class="sxs-lookup"><span data-stu-id="24ae2-195">Operator for the threshold comparison.</span></span> <br> <span data-ttu-id="24ae2-196">gt = większe niż</span><span class="sxs-lookup"><span data-stu-id="24ae2-196">gt = Greater Than</span></span> <br> <span data-ttu-id="24ae2-197">lt = mniej niż</span><span class="sxs-lookup"><span data-stu-id="24ae2-197">lt = Less Than</span></span> |
| <span data-ttu-id="24ae2-198">Wartość</span><span class="sxs-lookup"><span data-stu-id="24ae2-198">Value</span></span> |<span data-ttu-id="24ae2-199">Wartość progu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-199">Value for the threshold.</span></span> |

<span data-ttu-id="24ae2-200">Rozważmy na przykład kwerendy interwał 15 minut, Timespan 30 minut, a próg większym niż 10.</span><span class="sxs-lookup"><span data-stu-id="24ae2-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="24ae2-201">W takim przypadku zapytanie zostanie uruchomione co 15 minut, a alert będzie uruchomiony, jeśli zwróceniem 10 zdarzeń, które zostały utworzone w danym okresie 30 minut.</span><span class="sxs-lookup"><span data-stu-id="24ae2-201">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="24ae2-202">Poniżej znajduje się przykładowa odpowiedź dla akcji z tylko wartości progowej.</span><span class="sxs-lookup"><span data-stu-id="24ae2-202">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="24ae2-203">Za pomocą metody Put identyfikator unikatowy akcji do utworzenia nowej akcji próg dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-203">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="24ae2-204">Za pomocą metody Put istniejącego Identyfikatora akcji można zmodyfikować akcję próg dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-204">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span></span>  <span data-ttu-id="24ae2-205">Treść żądania musi zawierać element etag akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-205">The body of the request must include the etag of the action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="24ae2-206">Powiadomienia e-mail</span><span class="sxs-lookup"><span data-stu-id="24ae2-206">Email Notification</span></span>
<span data-ttu-id="24ae2-207">Powiadomienia e-mail wysyłanie poczty do co najmniej jednego adresata.</span><span class="sxs-lookup"><span data-stu-id="24ae2-207">Email Notifications send mail to one or more recipients.</span></span>  <span data-ttu-id="24ae2-208">Obejmują one właściwości w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="24ae2-208">They include the properties in the following table.</span></span>

| <span data-ttu-id="24ae2-209">Właściwość</span><span class="sxs-lookup"><span data-stu-id="24ae2-209">Property</span></span> | <span data-ttu-id="24ae2-210">Opis</span><span class="sxs-lookup"><span data-stu-id="24ae2-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="24ae2-211">Adresaci</span><span class="sxs-lookup"><span data-stu-id="24ae2-211">Recipients</span></span> |<span data-ttu-id="24ae2-212">Lista adresów e-mail.</span><span class="sxs-lookup"><span data-stu-id="24ae2-212">List of mail addresses.</span></span> |
| <span data-ttu-id="24ae2-213">Temat</span><span class="sxs-lookup"><span data-stu-id="24ae2-213">Subject</span></span> |<span data-ttu-id="24ae2-214">Temat wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="24ae2-214">The subject of the mail.</span></span> |
| <span data-ttu-id="24ae2-215">Załącznika</span><span class="sxs-lookup"><span data-stu-id="24ae2-215">Attachment</span></span> |<span data-ttu-id="24ae2-216">Załączniki nie są obecnie obsługiwane, dlatego to zawsze będzie mieć wartość "None".</span><span class="sxs-lookup"><span data-stu-id="24ae2-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="24ae2-217">Poniżej znajduje się przykładowa odpowiedź dla akcji powiadomienia e-mail o progu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-217">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is the subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="24ae2-218">Za pomocą metody Put identyfikator unikatowy akcji można utworzyć nowej wiadomości e-mail akcji dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-218">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span></span>  <span data-ttu-id="24ae2-219">Poniższy przykład tworzy wiadomość e-mail z powiadomieniem o progu, więc poczty jest wysyłany, gdy wyniki wyszukiwania przekracza wartość progową.</span><span class="sxs-lookup"><span data-stu-id="24ae2-219">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="24ae2-220">Aby zmodyfikować działanie poczty e-mail dla harmonogramu, należy użyć metody Put z istniejącego Identyfikatora akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-220">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span></span>  <span data-ttu-id="24ae2-221">Treść żądania musi zawierać element etag akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-221">The body of the request must include the etag of the action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="24ae2-222">Akcji korygowania</span><span class="sxs-lookup"><span data-stu-id="24ae2-222">Remediation actions</span></span>
<span data-ttu-id="24ae2-223">Korygowaniami uruchomienia elementu runbook w automatyzacji Azure, które próbuje naprawić problem identyfikowana na podstawie alertu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-223">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span></span>  <span data-ttu-id="24ae2-224">Należy utworzyć elementu webhook dla elementu runbook, używany w Akcja korygowania i następnie określ identyfikator URI we właściwości WebhookUri.</span><span class="sxs-lookup"><span data-stu-id="24ae2-224">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span></span>  <span data-ttu-id="24ae2-225">Podczas tworzenia tej akcji, używając konsoli OMS nowego elementu webhook jest tworzona automatycznie dla elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="24ae2-225">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span></span>

<span data-ttu-id="24ae2-226">Korygowaniami obejmują właściwości w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="24ae2-226">Remediations include the properties in the following table.</span></span>

| <span data-ttu-id="24ae2-227">Właściwość</span><span class="sxs-lookup"><span data-stu-id="24ae2-227">Property</span></span> | <span data-ttu-id="24ae2-228">Opis</span><span class="sxs-lookup"><span data-stu-id="24ae2-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="24ae2-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="24ae2-229">RunbookName</span></span> |<span data-ttu-id="24ae2-230">Nazwa elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="24ae2-230">Name of the runbook.</span></span> <span data-ttu-id="24ae2-231">To musi być zgodna opublikowanego elementu runbook w ramach konta automatyzacji skonfigurowane w rozwiązaniu automatyzacji w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="24ae2-231">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="24ae2-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="24ae2-232">WebhookUri</span></span> |<span data-ttu-id="24ae2-233">Identyfikator URI elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="24ae2-233">URI of the webhook.</span></span> |
| <span data-ttu-id="24ae2-234">Wygaśnięcia</span><span class="sxs-lookup"><span data-stu-id="24ae2-234">Expiry</span></span> |<span data-ttu-id="24ae2-235">Data wygaśnięcia i godzina elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="24ae2-235">The expiration date and time of the webhook.</span></span>  <span data-ttu-id="24ae2-236">Jeśli elementu webhook nie ma wygaśnięcia, może to być wszystkie prawidłową datą przyszłą.</span><span class="sxs-lookup"><span data-stu-id="24ae2-236">If the webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="24ae2-237">Poniżej znajduje się przykładowa odpowiedź dla akcji korygowania o progu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-237">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="24ae2-238">Za pomocą metody Put identyfikator unikatowy akcji do utworzenia nowej akcji korygowania harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-238">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span></span>  <span data-ttu-id="24ae2-239">Poniższy przykład tworzy korygowania o progu, aby uruchomić elementu runbook, gdy wyniki wyszukiwania przekracza wartość progową.</span><span class="sxs-lookup"><span data-stu-id="24ae2-239">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="24ae2-240">Za pomocą metody Put istniejącego Identyfikatora akcji można zmodyfikować akcji korygowania, harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-240">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span></span>  <span data-ttu-id="24ae2-241">Treść żądania musi zawierać element etag akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-241">The body of the request must include the etag of the action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="24ae2-242">Przykład</span><span class="sxs-lookup"><span data-stu-id="24ae2-242">Example</span></span>
<span data-ttu-id="24ae2-243">Poniżej znajduje się pełny przykład można utworzyć nowy alert e-mail.</span><span class="sxs-lookup"><span data-stu-id="24ae2-243">Following is a complete example to create a new email alert.</span></span>  <span data-ttu-id="24ae2-244">Spowoduje to utworzenie nowego harmonogramu wraz z akcji zawierający próg i poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="24ae2-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="24ae2-245">Akcje elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="24ae2-245">Webhook actions</span></span>
<span data-ttu-id="24ae2-246">Akcje elementu Webhook uruchomienia procesu podczas wywoływania adresu URL i opcjonalnie podając ładunku do wysłania.</span><span class="sxs-lookup"><span data-stu-id="24ae2-246">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span>  <span data-ttu-id="24ae2-247">Są one podobne do akcji korygowania, z wyjątkiem są przeznaczone dla elementów webhook, które może wywołać procesy inne niż elementy runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="24ae2-247">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="24ae2-248">Zawierają także dodatkowe opcja podania ładunku mają zostać dostarczone do zdalnego procesu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-248">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="24ae2-249">Akcje elementu Webhook nie mają tego progu, ale zamiast tego powinni zostać dodani do harmonogram, który ma akcję alertu o progu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-249">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="24ae2-250">Można dodawać wiele akcji elementu Webhook, które zostaną wszystkie uruchomione po spełnieniu wartość progową.</span><span class="sxs-lookup"><span data-stu-id="24ae2-250">You can add multiple Webhook actions that will all be run when the threshold is met.</span></span>

<span data-ttu-id="24ae2-251">Akcje elementu Webhook obejmują właściwości w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="24ae2-251">Webhook actions include the properties in the following table.</span></span>

| <span data-ttu-id="24ae2-252">Właściwość</span><span class="sxs-lookup"><span data-stu-id="24ae2-252">Property</span></span> | <span data-ttu-id="24ae2-253">Opis</span><span class="sxs-lookup"><span data-stu-id="24ae2-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="24ae2-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="24ae2-254">WebhookUri</span></span> |<span data-ttu-id="24ae2-255">Temat wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="24ae2-255">The subject of the mail.</span></span> |
| <span data-ttu-id="24ae2-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="24ae2-256">CustomPayload</span></span> |<span data-ttu-id="24ae2-257">Niestandardowy ładunek do wysłania do elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="24ae2-257">Custom payload to be sent to the webhook.</span></span>  <span data-ttu-id="24ae2-258">Format będzie zależeć od tego, czego oczekuje elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="24ae2-258">The format will depend on what the webhook is expecting.</span></span> |

<span data-ttu-id="24ae2-259">Poniżej znajduje się przykładowa odpowiedź dla elementu webhook akcji i skojarzonych alertach o progu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="24ae2-260">Utwórz lub Edytuj akcji elementu webhook</span><span class="sxs-lookup"><span data-stu-id="24ae2-260">Create or edit a webhook action</span></span>
<span data-ttu-id="24ae2-261">Za pomocą metody Put identyfikator unikatowy akcji do utworzenia nowej akcji elementu webhook dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-261">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span></span>  <span data-ttu-id="24ae2-262">Poniższy przykład tworzy akcji elementu Webhook i alertów o progu, dzięki czemu elementu webhook będą wyzwalane, gdy wyniki wyszukiwania przekracza wartość progową.</span><span class="sxs-lookup"><span data-stu-id="24ae2-262">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="24ae2-263">Za pomocą metody Put istniejącego Identyfikatora akcji można zmodyfikować akcję elementu webhook dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="24ae2-263">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span></span>  <span data-ttu-id="24ae2-264">Treść żądania musi zawierać element etag akcji.</span><span class="sxs-lookup"><span data-stu-id="24ae2-264">The body of the request must include the etag of the action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="24ae2-265">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="24ae2-265">Next steps</span></span>
* <span data-ttu-id="24ae2-266">Użyj [interfejsu API REST do wyszukiwania dziennika](log-analytics-log-search-api.md) w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="24ae2-266">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

