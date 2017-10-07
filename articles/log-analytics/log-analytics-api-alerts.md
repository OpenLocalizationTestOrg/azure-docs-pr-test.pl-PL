---
title: aaaUsing OMS dziennika analizy alertu interfejsu API REST
description: "Witaj interfejsu API REST alertu dziennika analizy pozwala toocreate alerty i zarządzaj nimi w analizy dzienników, która jest częścią z Operations Management Suite (OMS).  Ten artykuł zawiera szczegółowe informacje o hello interfejsu API i kilka przykładów do wykonywania różnych operacji."
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
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="6ede6-104">Tworzenie i zarządzanie nimi reguły alertów w analizy dzienników z interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="6ede6-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="6ede6-105">Witaj interfejsu API REST alertu dziennika analizy pozwala toocreate alerty i zarządzaj nimi w Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="6ede6-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="6ede6-106">Ten artykuł zawiera szczegółowe informacje o hello interfejsu API i kilka przykładów do wykonywania różnych operacji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="6ede6-107">Witaj interfejsu API REST Search analizy dziennika jest RESTful i jest możliwy za pośrednictwem hello Azure Resource Manager REST API.</span><span class="sxs-lookup"><span data-stu-id="6ede6-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="6ede6-108">W tym dokumencie można znaleźć przykłady gdzie hello interfejsu API jest dostępny z wiersza polecenia programu PowerShell przy użyciu [ARMClient](https://github.com/projectkudu/ARMClient), narzędzie wiersza polecenia typu open source, który upraszcza wywoływania hello interfejsu API usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6ede6-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="6ede6-109">Użycie Hello ARMClient i programu PowerShell jest jedną z wielu opcji hello tooaccess interfejsu API Search analizy dziennika.</span><span class="sxs-lookup"><span data-stu-id="6ede6-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="6ede6-110">Z tych narzędzi można wykorzystywać hello wywołania interfejsu API RESTful Menedżera zasobów Azure toomake obszarów roboczych o tooOMS i wykonywać polecenia wyszukiwania w nich.</span><span class="sxs-lookup"><span data-stu-id="6ede6-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="6ede6-111">Witaj interfejsu API dane wyjściowe obejmują tooyou wyników wyszukiwania w formacie JSON, umożliwiając wyniki wyszukiwania hello toouse na wiele różnych sposobów programowo.</span><span class="sxs-lookup"><span data-stu-id="6ede6-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ede6-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6ede6-112">Prerequisites</span></span>
<span data-ttu-id="6ede6-113">Obecnie usługa alertów można tworzyć tylko z zapisanej operacji wyszukiwania w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="6ede6-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="6ede6-114">Może się odwoływać toohello [interfejsu API REST wyszukiwania dziennika](log-analytics-log-search-api.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="6ede6-115">Harmonogramy</span><span class="sxs-lookup"><span data-stu-id="6ede6-115">Schedules</span></span>
<span data-ttu-id="6ede6-116">Zapisane wyszukiwanie może mieć co najmniej jeden harmonogram.</span><span class="sxs-lookup"><span data-stu-id="6ede6-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="6ede6-117">Hello harmonogram Określa, jak często hello wyszukiwania jest uruchamiany i interwał czasu hello za pośrednictwem których kryteria hello jest identyfikowany.</span><span class="sxs-lookup"><span data-stu-id="6ede6-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="6ede6-118">Harmonogramy mają właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6ede6-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="6ede6-119">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6ede6-119">Property</span></span> | <span data-ttu-id="6ede6-120">Opis</span><span class="sxs-lookup"><span data-stu-id="6ede6-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6ede6-121">Interwał</span><span class="sxs-lookup"><span data-stu-id="6ede6-121">Interval</span></span> |<span data-ttu-id="6ede6-122">Jak często hello wyszukiwania jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="6ede6-122">How often hello search is run.</span></span> <span data-ttu-id="6ede6-123">(W minutach).</span><span class="sxs-lookup"><span data-stu-id="6ede6-123">Measured in minutes.</span></span> |
| <span data-ttu-id="6ede6-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="6ede6-124">QueryTimeSpan</span></span> |<span data-ttu-id="6ede6-125">Interwał czasu Hello za pośrednictwem których hello oceny kryteriów.</span><span class="sxs-lookup"><span data-stu-id="6ede6-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="6ede6-126">Musi być większy niż interwał równy tooor.</span><span class="sxs-lookup"><span data-stu-id="6ede6-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="6ede6-127">(W minutach).</span><span class="sxs-lookup"><span data-stu-id="6ede6-127">Measured in minutes.</span></span> |
| <span data-ttu-id="6ede6-128">Wersja</span><span class="sxs-lookup"><span data-stu-id="6ede6-128">Version</span></span> |<span data-ttu-id="6ede6-129">Witaj używana wersja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6ede6-129">hello API version being used.</span></span>  <span data-ttu-id="6ede6-130">Obecnie ta powinna być zawsze ustawiony too1.</span><span class="sxs-lookup"><span data-stu-id="6ede6-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="6ede6-131">Rozważmy na przykład kwerendy zdarzeń z interwałem 15 minut i zakres czasu 30 minut.</span><span class="sxs-lookup"><span data-stu-id="6ede6-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="6ede6-132">W takim przypadku hello będzie uruchamiane zapytanie co 15 minut, a alert będzie uruchomiony, jeśli kryteria hello nadal tooresolve tootrue w danym okresie 30 minut.</span><span class="sxs-lookup"><span data-stu-id="6ede6-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="6ede6-133">Trwa pobieranie harmonogramów</span><span class="sxs-lookup"><span data-stu-id="6ede6-133">Retrieving schedules</span></span>
<span data-ttu-id="6ede6-134">Użyj hello Pobierz tooretrieve — metoda wszystkie harmonogramy dla zapisanego kryterium wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6ede6-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="6ede6-135">Użyj hello Get, metoda z tooretrieve identyfikator harmonogramu konkretny harmonogram dla zapisanego kryterium wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6ede6-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="6ede6-136">Poniżej znajduje się przykładowa odpowiedź dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-136">Following is a sample response for a schedule.</span></span>

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

### <a name="creating-a-schedule"></a><span data-ttu-id="6ede6-137">Tworzenie harmonogramu</span><span class="sxs-lookup"><span data-stu-id="6ede6-137">Creating a schedule</span></span>
<span data-ttu-id="6ede6-138">Za pomocą metody Put hello harmonogram Unikatowy identyfikator toocreate nowy harmonogram.</span><span class="sxs-lookup"><span data-stu-id="6ede6-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="6ede6-139">Należy pamiętać, że dwa harmonogramy nie może mieć hello takim samym identyfikatorze nawet, jeśli są one powiązane z różnymi, zapisane wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6ede6-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="6ede6-140">Po utworzeniu harmonogramu w konsoli OMS hello identyfikator GUID jest tworzony dla identyfikatora hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="6ede6-141">Nazwa Hello wszystkie zapisane wyszukiwania, harmonogramów i działania utworzone za pomocą hello API analizy dziennika musi być pisane małymi literami.</span><span class="sxs-lookup"><span data-stu-id="6ede6-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="6ede6-142">Edytowanie harmonogramu</span><span class="sxs-lookup"><span data-stu-id="6ede6-142">Editing a schedule</span></span>
<span data-ttu-id="6ede6-143">Za pomocą metody Put hello identyfikator hello sam zapisane wyszukiwanie toomodify, który zaplanować istniejącego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="6ede6-144">Hello treści żądania hello musi zawierać element etag hello hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="6ede6-145">Usuwanie harmonogramów</span><span class="sxs-lookup"><span data-stu-id="6ede6-145">Deleting schedules</span></span>
<span data-ttu-id="6ede6-146">Za pomocą metody Delete hello toodelete identyfikator harmonogramu zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="6ede6-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="6ede6-147">Akcje</span><span class="sxs-lookup"><span data-stu-id="6ede6-147">Actions</span></span>
<span data-ttu-id="6ede6-148">Harmonogram może mieć wiele akcji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="6ede6-149">Akcja może zdefiniować co najmniej jeden tooperform procesy, takie jak wysyłanie wiadomości e-mail lub uruchamianie elementu runbook lub mogą określić próg, określająca, kiedy hello wyniki wyszukiwania kryteriom niektórych.</span><span class="sxs-lookup"><span data-stu-id="6ede6-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="6ede6-150">Niektóre akcje definiują zarówno tak, aby procesy hello są wykonywane po spełnieniu hello próg.</span><span class="sxs-lookup"><span data-stu-id="6ede6-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="6ede6-151">Wszystkie działania mają właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6ede6-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="6ede6-152">Różne typy alertów mają różne dodatkowe właściwości, które są opisane poniżej.</span><span class="sxs-lookup"><span data-stu-id="6ede6-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="6ede6-153">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6ede6-153">Property</span></span> | <span data-ttu-id="6ede6-154">Opis</span><span class="sxs-lookup"><span data-stu-id="6ede6-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6ede6-155">Typ</span><span class="sxs-lookup"><span data-stu-id="6ede6-155">Type</span></span> |<span data-ttu-id="6ede6-156">Typ akcji hello.</span><span class="sxs-lookup"><span data-stu-id="6ede6-156">Type of hello action.</span></span>  <span data-ttu-id="6ede6-157">Obecnie hello możliwe wartości to Alert i elementu Webhook.</span><span class="sxs-lookup"><span data-stu-id="6ede6-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="6ede6-158">Nazwa</span><span class="sxs-lookup"><span data-stu-id="6ede6-158">Name</span></span> |<span data-ttu-id="6ede6-159">Nazwa wyświetlana hello alertu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="6ede6-160">Wersja</span><span class="sxs-lookup"><span data-stu-id="6ede6-160">Version</span></span> |<span data-ttu-id="6ede6-161">Witaj używana wersja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="6ede6-161">hello API version being used.</span></span>  <span data-ttu-id="6ede6-162">Obecnie ta powinna być zawsze ustawiony too1.</span><span class="sxs-lookup"><span data-stu-id="6ede6-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="6ede6-163">Pobieranie akcji</span><span class="sxs-lookup"><span data-stu-id="6ede6-163">Retrieving actions</span></span>
<span data-ttu-id="6ede6-164">Użyj hello Pobierz tooretrieve — metoda wszystkie akcje dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="6ede6-165">Użyj hello Get, metoda z tooretrieve identyfikator akcji hello określonej akcji dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="6ede6-166">Tworzenie lub edytowanie akcji</span><span class="sxs-lookup"><span data-stu-id="6ede6-166">Creating or editing actions</span></span>
<span data-ttu-id="6ede6-167">Użyj metody Put hello o identyfikatorze akcji, który jest unikatowy toohello harmonogram toocreate nową akcję.</span><span class="sxs-lookup"><span data-stu-id="6ede6-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="6ede6-168">Po utworzeniu akcji w konsoli OMS hello identyfikator GUID jest identyfikatora hello akcji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="6ede6-169">Nazwa Hello wszystkie zapisane wyszukiwania, harmonogramów i działania utworzone za pomocą hello API analizy dziennika musi być pisane małymi literami.</span><span class="sxs-lookup"><span data-stu-id="6ede6-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="6ede6-170">Użyj metody Put hello z akcją istniejący identyfikator hello sam zapisane wyszukiwanie toomodify, który harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="6ede6-171">Hello treści żądania hello musi zawierać element etag hello hello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="6ede6-172">format żądania Hello do tworzenia nowych akcji zależy od typu akcji, te przykłady znajdują się w poniższych sekcjach hello.</span><span class="sxs-lookup"><span data-stu-id="6ede6-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="6ede6-173">Usuwanie akcji</span><span class="sxs-lookup"><span data-stu-id="6ede6-173">Deleting actions</span></span>
<span data-ttu-id="6ede6-174">Za pomocą metody Delete hello toodelete identyfikator akcji hello akcji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="6ede6-175">Akcje alertu</span><span class="sxs-lookup"><span data-stu-id="6ede6-175">Alert Actions</span></span>
<span data-ttu-id="6ede6-176">Harmonogram ma jeden i tylko jeden Alert akcji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="6ede6-177">Akcje alertu występuje jeden lub kilka z sekcji hello hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6ede6-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="6ede6-178">Każdy jest opisany bardziej szczegółowo poniżej.</span><span class="sxs-lookup"><span data-stu-id="6ede6-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="6ede6-179">Sekcja</span><span class="sxs-lookup"><span data-stu-id="6ede6-179">Section</span></span> | <span data-ttu-id="6ede6-180">Opis</span><span class="sxs-lookup"><span data-stu-id="6ede6-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6ede6-181">Próg</span><span class="sxs-lookup"><span data-stu-id="6ede6-181">Threshold</span></span> |<span data-ttu-id="6ede6-182">Po uruchomieniu akcji hello kryteria.</span><span class="sxs-lookup"><span data-stu-id="6ede6-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="6ede6-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="6ede6-183">EmailNotification</span></span> |<span data-ttu-id="6ede6-184">Wysyłanie poczty toomultiple adresatów.</span><span class="sxs-lookup"><span data-stu-id="6ede6-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="6ede6-185">Korygowania</span><span class="sxs-lookup"><span data-stu-id="6ede6-185">Remediation</span></span> |<span data-ttu-id="6ede6-186">Uruchom element runbook w automatyzacji Azure tooattempt toocorrect zidentyfikować problem.</span><span class="sxs-lookup"><span data-stu-id="6ede6-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="6ede6-187">Progi</span><span class="sxs-lookup"><span data-stu-id="6ede6-187">Thresholds</span></span>
<span data-ttu-id="6ede6-188">Akcja alertu powinna mieć jeden i tylko jeden próg.</span><span class="sxs-lookup"><span data-stu-id="6ede6-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="6ede6-189">Jeśli wyniki hello zapisanego kryterium wyszukiwania zgodne próg hello w akcji skojarzonej z tym wyszukiwania, są uruchamiane żadnych innych procesów w tej akcji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="6ede6-190">Akcja może również zawierać tylko wartości progowej, aby mogą być używane z akcjami innych typów, które nie zawierają wartości progowe.</span><span class="sxs-lookup"><span data-stu-id="6ede6-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="6ede6-191">Progi mają właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6ede6-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="6ede6-192">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6ede6-192">Property</span></span> | <span data-ttu-id="6ede6-193">Opis</span><span class="sxs-lookup"><span data-stu-id="6ede6-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6ede6-194">Operator</span><span class="sxs-lookup"><span data-stu-id="6ede6-194">Operator</span></span> |<span data-ttu-id="6ede6-195">Operator porównania próg hello.</span><span class="sxs-lookup"><span data-stu-id="6ede6-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="6ede6-196">gt = większe niż</span><span class="sxs-lookup"><span data-stu-id="6ede6-196">gt = Greater Than</span></span> <br> <span data-ttu-id="6ede6-197">lt = mniej niż</span><span class="sxs-lookup"><span data-stu-id="6ede6-197">lt = Less Than</span></span> |
| <span data-ttu-id="6ede6-198">Wartość</span><span class="sxs-lookup"><span data-stu-id="6ede6-198">Value</span></span> |<span data-ttu-id="6ede6-199">Wartość progu hello.</span><span class="sxs-lookup"><span data-stu-id="6ede6-199">Value for hello threshold.</span></span> |

<span data-ttu-id="6ede6-200">Rozważmy na przykład kwerendy interwał 15 minut, Timespan 30 minut, a próg większym niż 10.</span><span class="sxs-lookup"><span data-stu-id="6ede6-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="6ede6-201">W takim przypadku hello będzie uruchamiane zapytanie co 15 minut, a alert będzie uruchomiony, jeśli zwróceniem 10 zdarzeń, które zostały utworzone w danym okresie 30 minut.</span><span class="sxs-lookup"><span data-stu-id="6ede6-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="6ede6-202">Poniżej znajduje się przykładowa odpowiedź dla akcji z tylko wartości progowej.</span><span class="sxs-lookup"><span data-stu-id="6ede6-202">Following is a sample response for an action with only a threshold.</span></span>  

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

<span data-ttu-id="6ede6-203">Za pomocą metody Put hello akcji Unikatowy identyfikator toocreate nową akcję próg dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="6ede6-204">Za pomocą metody Put hello istniejących toomodify identyfikator akcji akcji próg dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="6ede6-205">Witaj treści żądania hello musi zawierać etag hello hello akcji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="6ede6-206">Powiadomienia e-mail</span><span class="sxs-lookup"><span data-stu-id="6ede6-206">Email Notification</span></span>
<span data-ttu-id="6ede6-207">Powiadomienia e-mail wysyłanie poczty tooone lub więcej adresatów.</span><span class="sxs-lookup"><span data-stu-id="6ede6-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="6ede6-208">Obejmują one właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6ede6-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="6ede6-209">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6ede6-209">Property</span></span> | <span data-ttu-id="6ede6-210">Opis</span><span class="sxs-lookup"><span data-stu-id="6ede6-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6ede6-211">Adresaci</span><span class="sxs-lookup"><span data-stu-id="6ede6-211">Recipients</span></span> |<span data-ttu-id="6ede6-212">Lista adresów e-mail.</span><span class="sxs-lookup"><span data-stu-id="6ede6-212">List of mail addresses.</span></span> |
| <span data-ttu-id="6ede6-213">Temat</span><span class="sxs-lookup"><span data-stu-id="6ede6-213">Subject</span></span> |<span data-ttu-id="6ede6-214">temat Hello hello poczty.</span><span class="sxs-lookup"><span data-stu-id="6ede6-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="6ede6-215">Załącznika</span><span class="sxs-lookup"><span data-stu-id="6ede6-215">Attachment</span></span> |<span data-ttu-id="6ede6-216">Załączniki nie są obecnie obsługiwane, dlatego to zawsze będzie mieć wartość "None".</span><span class="sxs-lookup"><span data-stu-id="6ede6-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="6ede6-217">Poniżej znajduje się przykładowa odpowiedź dla akcji powiadomienia e-mail o progu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-217">Following is a sample response for an email notification action with a threshold.</span></span>  

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
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="6ede6-218">Za pomocą metody Put hello akcji Unikatowy identyfikator toocreate nową akcję poczty e-mail dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="6ede6-219">Witaj poniższy przykład tworzy wiadomość e-mail z powiadomieniem o progu tak poczty hello jest wysyłany, gdy wyniki hello hello zapisanego wyszukiwania przekracza próg hello.</span><span class="sxs-lookup"><span data-stu-id="6ede6-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="6ede6-220">Za pomocą metody Put hello istniejących toomodify identyfikator akcji akcji poczty e-mail dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="6ede6-221">Witaj treści żądania hello musi zawierać etag hello hello akcji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="6ede6-222">Akcji korygowania</span><span class="sxs-lookup"><span data-stu-id="6ede6-222">Remediation actions</span></span>
<span data-ttu-id="6ede6-223">Korygowaniami uruchomienia elementu runbook w automatyzacji Azure, która próbuje problem hello toocorrect identyfikowane przez hello alert.</span><span class="sxs-lookup"><span data-stu-id="6ede6-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="6ede6-224">Należy utworzyć elementu webhook dla elementu runbook hello używany w Akcja korygowania, a następnie określ hello identyfikatora URI w hello WebhookUri właściwości.</span><span class="sxs-lookup"><span data-stu-id="6ede6-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="6ede6-225">Podczas tworzenia tej akcji, używając konsoli OMS hello nowego elementu webhook jest tworzony automatycznie hello elementu runbook.</span><span class="sxs-lookup"><span data-stu-id="6ede6-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="6ede6-226">Korygowaniami dołączyć właściwości hello hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6ede6-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="6ede6-227">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6ede6-227">Property</span></span> | <span data-ttu-id="6ede6-228">Opis</span><span class="sxs-lookup"><span data-stu-id="6ede6-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6ede6-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="6ede6-229">RunbookName</span></span> |<span data-ttu-id="6ede6-230">Nazwa elementu hello runbook.</span><span class="sxs-lookup"><span data-stu-id="6ede6-230">Name of hello runbook.</span></span> <span data-ttu-id="6ede6-231">To musi być zgodna opublikowanego elementu runbook na koncie automatyzacji hello skonfigurowane w hello rozwiązanie do automatyzacji w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="6ede6-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="6ede6-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="6ede6-232">WebhookUri</span></span> |<span data-ttu-id="6ede6-233">Identyfikator URI elementu webhook hello.</span><span class="sxs-lookup"><span data-stu-id="6ede6-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="6ede6-234">Wygaśnięcia</span><span class="sxs-lookup"><span data-stu-id="6ede6-234">Expiry</span></span> |<span data-ttu-id="6ede6-235">Witaj datę i godzinę wygaśnięcia elementu hello webhook.</span><span class="sxs-lookup"><span data-stu-id="6ede6-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="6ede6-236">Jeśli hello elementu webhook nie ma wygaśnięcia, może to być wszystkie prawidłową datą przyszłą.</span><span class="sxs-lookup"><span data-stu-id="6ede6-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="6ede6-237">Poniżej znajduje się przykładowa odpowiedź dla akcji korygowania o progu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-237">Following is a sample response for a remediation action with a threshold.</span></span>

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

<span data-ttu-id="6ede6-238">Za pomocą metody Put hello akcji Unikatowy identyfikator toocreate nowa akcja korygowania harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="6ede6-239">Witaj poniższy przykład tworzy korygowania o progu tak hello elementu runbook została uruchomiona, wyniki hello hello zapisanego wyszukiwania przekracza próg hello.</span><span class="sxs-lookup"><span data-stu-id="6ede6-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="6ede6-240">Za pomocą metody Put hello istniejących toomodify identyfikator akcji Akcja korygowania harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="6ede6-241">Witaj treści żądania hello musi zawierać etag hello hello akcji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="6ede6-242">Przykład</span><span class="sxs-lookup"><span data-stu-id="6ede6-242">Example</span></span>
<span data-ttu-id="6ede6-243">Poniżej znajduje się pełny przykład toocreate nowy alert e-mail.</span><span class="sxs-lookup"><span data-stu-id="6ede6-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="6ede6-244">Spowoduje to utworzenie nowego harmonogramu wraz z akcji zawierający próg i poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="6ede6-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="6ede6-245">Akcje elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="6ede6-245">Webhook actions</span></span>
<span data-ttu-id="6ede6-246">Akcje elementu Webhook uruchomienia procesu podczas wywoływania adresu URL i opcjonalnie podając toobe ładunku, wysyłane.</span><span class="sxs-lookup"><span data-stu-id="6ede6-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="6ede6-247">Są one podobne akcje tooRemediation, z wyjątkiem są przeznaczone dla elementów webhook, które może wywołać procesów innych niż element runbook usługi Automatyzacja Azure.</span><span class="sxs-lookup"><span data-stu-id="6ede6-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="6ede6-248">Zapewniają także hello dodatkowa opcja udostępniania procesu zdalnego toohello toobe dostarczyć ładunku.</span><span class="sxs-lookup"><span data-stu-id="6ede6-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="6ede6-249">Akcje elementu Webhook nie ma wartości progowej, ale zamiast tego należy dodać tooa harmonogram, który ma akcję alertu o progu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="6ede6-250">Można dodawać wiele akcji elementu Webhook, które zostaną wszystkie uruchomione po spełnieniu hello próg.</span><span class="sxs-lookup"><span data-stu-id="6ede6-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="6ede6-251">Akcje elementu Webhook dołączyć właściwości hello hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="6ede6-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="6ede6-252">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6ede6-252">Property</span></span> | <span data-ttu-id="6ede6-253">Opis</span><span class="sxs-lookup"><span data-stu-id="6ede6-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6ede6-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="6ede6-254">WebhookUri</span></span> |<span data-ttu-id="6ede6-255">temat Hello hello poczty.</span><span class="sxs-lookup"><span data-stu-id="6ede6-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="6ede6-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="6ede6-256">CustomPayload</span></span> |<span data-ttu-id="6ede6-257">Niestandardowy ładunek toobe wysyłane toohello elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="6ede6-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="6ede6-258">Hello format będzie zależeć od elementu webhook jakie hello jest oczekiwany.</span><span class="sxs-lookup"><span data-stu-id="6ede6-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="6ede6-259">Poniżej znajduje się przykładowa odpowiedź dla elementu webhook akcji i skojarzonych alertach o progu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

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

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="6ede6-260">Utwórz lub Edytuj akcji elementu webhook</span><span class="sxs-lookup"><span data-stu-id="6ede6-260">Create or edit a webhook action</span></span>
<span data-ttu-id="6ede6-261">Za pomocą metody Put hello akcji Unikatowy identyfikator toocreate nową akcję elementu webhook dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="6ede6-262">Witaj poniższy przykład tworzy akcji elementu Webhook i alertów o progu tak, aby wyniki hello hello zapisanego wyszukiwania przekracza próg hello zostanie wywołane hello elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="6ede6-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="6ede6-263">Za pomocą metody Put hello istniejących toomodify identyfikator akcji akcji elementu webhook dla harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="6ede6-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="6ede6-264">Witaj treści żądania hello musi zawierać etag hello hello akcji.</span><span class="sxs-lookup"><span data-stu-id="6ede6-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="6ede6-265">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ede6-265">Next steps</span></span>
* <span data-ttu-id="6ede6-266">Użyj hello [interfejsu API REST tooperform dziennik wyszukiwania](log-analytics-log-search-api.md) w analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="6ede6-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

