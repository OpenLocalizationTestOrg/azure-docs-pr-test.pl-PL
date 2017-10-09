---
title: tooalerts aaaResponses w OMS Log Analytics | Dokumentacja firmy Microsoft
description: "Alerty w analizy dzienników zidentyfikować ważne informacje zawarte w repozytorium OMS i aktywne powiadamia użytkownika o problemy lub wywołanie akcji tooattempt toocorrect je.  W tym artykule opisano, jak toocreate regułę alertu i szczegóły hello różne akcje mogą przyjmować."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d24bb726a96e7143985f111c0599dc4e7898b4f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-actions-tooalert-rules-in-log-analytics"></a><span data-ttu-id="e665e-104">Dodaj reguły tooalert akcje w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="e665e-104">Add actions tooalert rules in Log Analytics</span></span>
<span data-ttu-id="e665e-105">Gdy [alert jest tworzony w analizy dzienników](log-analytics-alerts.md), dostępna opcja hello [konfigurowania reguły alertu hello](log-analytics-alerts.md) tooperform co najmniej jednej akcji.</span><span class="sxs-lookup"><span data-stu-id="e665e-105">When an [alert is created in Log Analytics](log-analytics-alerts.md), you have hello option of [configuring hello alert rule](log-analytics-alerts.md) tooperform one or more actions.</span></span>  <span data-ttu-id="e665e-106">W tym artykule opisano hello różne akcje, które są dostępne i szczegółowe informacje na temat konfigurowania każdego rodzaju.</span><span class="sxs-lookup"><span data-stu-id="e665e-106">This article describes hello different actions that are available and details on configuring each kind.</span></span>

| <span data-ttu-id="e665e-107">Akcja</span><span class="sxs-lookup"><span data-stu-id="e665e-107">Action</span></span> | <span data-ttu-id="e665e-108">Opis</span><span class="sxs-lookup"><span data-stu-id="e665e-108">Description</span></span> |
|:--|:--|
| [<span data-ttu-id="e665e-109">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="e665e-109">Email</span></span>](#email-actions) | <span data-ttu-id="e665e-110">Wyślij wiadomość e-mail ze szczegółami hello hello tooone alertu lub więcej adresatów.</span><span class="sxs-lookup"><span data-stu-id="e665e-110">Send an e-mail with hello details of hello alert tooone or more recipients.</span></span> |
| [<span data-ttu-id="e665e-111">Element Webhook</span><span class="sxs-lookup"><span data-stu-id="e665e-111">Webhook</span></span>](#webhook-actions) | <span data-ttu-id="e665e-112">Wywołaj procesu zewnętrznego przez pojedyncze żądanie HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="e665e-112">Invoke an external process through a single HTTP POST request.</span></span> |
| [<span data-ttu-id="e665e-113">Element Runbook</span><span class="sxs-lookup"><span data-stu-id="e665e-113">Runbook</span></span>](#runbook-actions) | <span data-ttu-id="e665e-114">Uruchom element runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="e665e-114">Start a runbook in Azure Automation.</span></span> |


## <a name="email-actions"></a><span data-ttu-id="e665e-115">Akcje poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="e665e-115">Email actions</span></span>
<span data-ttu-id="e665e-116">Akcje e-mail Wyślij wiadomość e-mail ze szczegółami hello hello tooone alertu lub więcej adresatów.</span><span class="sxs-lookup"><span data-stu-id="e665e-116">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>  <span data-ttu-id="e665e-117">Można określić podmiotu hello hello poczty, ale jego zawartość jest standardowym formacie tworzony przez analizy dzienników.</span><span class="sxs-lookup"><span data-stu-id="e665e-117">You can specify hello subject of hello mail, but it's content is a standard format constructed by Log Analytics.</span></span>  <span data-ttu-id="e665e-118">Zawiera informacje podsumowania, takie jak nazwa hello alertu hello toodetails dodanie z tooten rekordów zwróconych hello dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e665e-118">It includes summary information such as hello name of hello alert in addition toodetails of up tooten records returned by hello log search.</span></span>  <span data-ttu-id="e665e-119">Zawiera również link tooa dziennik wyszukiwania w analizy dzienników, która zwróci hello cały zestaw rekordów z tej kwerendy.</span><span class="sxs-lookup"><span data-stu-id="e665e-119">It also includes a link tooa log search in Log Analytics that will return hello entire set of records from that query.</span></span>   <span data-ttu-id="e665e-120">nadawca Hello poczty hello jest *Microsoft Operations Management Suite Team &lt; noreply@oms.microsoft.com &gt;* .</span><span class="sxs-lookup"><span data-stu-id="e665e-120">hello sender of hello mail is *Microsoft Operations Management Suite Team &lt;noreply@oms.microsoft.com&gt;*.</span></span> 

<span data-ttu-id="e665e-121">Akcje poczty e-mail wymaga właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="e665e-121">Email actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="e665e-122">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e665e-122">Property</span></span> | <span data-ttu-id="e665e-123">Opis</span><span class="sxs-lookup"><span data-stu-id="e665e-123">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e665e-124">Temat</span><span class="sxs-lookup"><span data-stu-id="e665e-124">Subject</span></span> |<span data-ttu-id="e665e-125">Podmiotu w hello wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="e665e-125">Subject in hello email.</span></span>  <span data-ttu-id="e665e-126">Nie można zmodyfikować hello treści wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="e665e-126">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="e665e-127">Adresaci</span><span class="sxs-lookup"><span data-stu-id="e665e-127">Recipients</span></span> |<span data-ttu-id="e665e-128">Adresy wszystkich adresatów wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="e665e-128">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="e665e-129">Jeśli określono więcej niż jeden adres, a następnie hello oddzielne adresy średnikiem (;).</span><span class="sxs-lookup"><span data-stu-id="e665e-129">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |


## <a name="webhook-actions"></a><span data-ttu-id="e665e-130">Akcje elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="e665e-130">Webhook actions</span></span>

<span data-ttu-id="e665e-131">Akcje elementu Webhook pozwalają tooinvoke procesu zewnętrznego przez pojedyncze żądanie HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="e665e-131">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>  <span data-ttu-id="e665e-132">Usługa Hello wywoływana powinien obsługuje elementów webhook i określić, jak używać żadnych ładunku odbiera.</span><span class="sxs-lookup"><span data-stu-id="e665e-132">hello service being called should support webhooks and determine how it will use any payload it receives.</span></span>  <span data-ttu-id="e665e-133">Można także wywołać interfejs API REST w szczególności nie obsługuje elementów webhook, jak długo Żądanie hello jest w formacie tego powitalne rozumie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e665e-133">You could also call a REST API that doesn't specifically support webhooks as long as hello request is in a format that hello API understands.</span></span>  <span data-ttu-id="e665e-134">Przykłady użycia elementu webhook w odpowiedzi tooan alert wysyłania wiadomości [Slack](http://slack.com) lub Tworzenie zdarzenia w [PagerDuty](http://pagerduty.com/).</span><span class="sxs-lookup"><span data-stu-id="e665e-134">Examples of using a webhook in response tooan alert are sending a message in [Slack](http://slack.com) or creating an incident in [PagerDuty](http://pagerduty.com/).</span></span>  <span data-ttu-id="e665e-135">Pełny Przewodnik tworzenia reguły alertu z elementu webhook toocall zapas czasu jest dostępna na [elementów Webhook w alertach analizy dzienników](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="e665e-135">A complete walkthrough of creating an alert rule with a webhook toocall Slack is available at [Webhooks in Log Analytics alerts](log-analytics-alerts-webhooks.md).</span></span>

<span data-ttu-id="e665e-136">Akcje elementu Webhook wymagają właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="e665e-136">Webhook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="e665e-137">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e665e-137">Property</span></span> | <span data-ttu-id="e665e-138">Opis</span><span class="sxs-lookup"><span data-stu-id="e665e-138">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e665e-139">Adres URL elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="e665e-139">Webhook URL</span></span> |<span data-ttu-id="e665e-140">adres URL Hello hello elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="e665e-140">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="e665e-141">Niestandardowy ładunek JSON</span><span class="sxs-lookup"><span data-stu-id="e665e-141">Custom JSON payload</span></span> |<span data-ttu-id="e665e-142">Niestandardowy ładunek toosend z hello elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="e665e-142">Custom payload toosend with hello webhook.</span></span>  <span data-ttu-id="e665e-143">Aby uzyskać więcej informacji, zobacz poniżej.</span><span class="sxs-lookup"><span data-stu-id="e665e-143">See below for details.</span></span> |


<span data-ttu-id="e665e-144">Elementów Webhook zawierały adres URL i zapisany w formacie JSON, ilości danych hello ładunku wysyłane toohello zewnętrznej usługi.</span><span class="sxs-lookup"><span data-stu-id="e665e-144">Webhooks include a URL and a payload formatted in JSON that is hello data sent toohello external service.</span></span>  <span data-ttu-id="e665e-145">Domyślnie ładunku hello będzie zawierać wartości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="e665e-145">By default, hello payload will include hello values in hello following table.</span></span>  <span data-ttu-id="e665e-146">Możesz wybrać tooreplace tego ładunku z niestandardowych jeden własny.</span><span class="sxs-lookup"><span data-stu-id="e665e-146">You can choose tooreplace this payload with a custom one of your own.</span></span>  <span data-ttu-id="e665e-147">W takim przypadku można używać hello zmiennych w tabeli powitania dla każdego tooinclude parametry hello ich wartości w niestandardowy ładunek.</span><span class="sxs-lookup"><span data-stu-id="e665e-147">In that case you can use hello variables in hello table for each of hello parameters tooinclude their value in your custom payload.</span></span>

| <span data-ttu-id="e665e-148">Parametr</span><span class="sxs-lookup"><span data-stu-id="e665e-148">Parameter</span></span> | <span data-ttu-id="e665e-149">Zmienna</span><span class="sxs-lookup"><span data-stu-id="e665e-149">Variable</span></span> | <span data-ttu-id="e665e-150">Opis</span><span class="sxs-lookup"><span data-stu-id="e665e-150">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="e665e-151">AlertRuleName</span><span class="sxs-lookup"><span data-stu-id="e665e-151">AlertRuleName</span></span> |<span data-ttu-id="e665e-152">#alertrulename</span><span class="sxs-lookup"><span data-stu-id="e665e-152">#alertrulename</span></span> |<span data-ttu-id="e665e-153">Nazwa reguły alertów hello.</span><span class="sxs-lookup"><span data-stu-id="e665e-153">Name of hello alert rule.</span></span> |
| <span data-ttu-id="e665e-154">AlertThresholdOperator</span><span class="sxs-lookup"><span data-stu-id="e665e-154">AlertThresholdOperator</span></span> |<span data-ttu-id="e665e-155">#thresholdoperator</span><span class="sxs-lookup"><span data-stu-id="e665e-155">#thresholdoperator</span></span> |<span data-ttu-id="e665e-156">Operator próg hello reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="e665e-156">Threshold operator for hello alert rule.</span></span>  <span data-ttu-id="e665e-157">*Większa niż* lub *mniej niż*.</span><span class="sxs-lookup"><span data-stu-id="e665e-157">*Greater than* or *Less than*.</span></span> |
| <span data-ttu-id="e665e-158">AlertThresholdValue</span><span class="sxs-lookup"><span data-stu-id="e665e-158">AlertThresholdValue</span></span> |<span data-ttu-id="e665e-159">#thresholdvalue</span><span class="sxs-lookup"><span data-stu-id="e665e-159">#thresholdvalue</span></span> |<span data-ttu-id="e665e-160">Wartość progowa hello reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="e665e-160">Threshold value for hello alert rule.</span></span> |
| <span data-ttu-id="e665e-161">LinkToSearchResults</span><span class="sxs-lookup"><span data-stu-id="e665e-161">LinkToSearchResults</span></span> |<span data-ttu-id="e665e-162">#linktosearchresults</span><span class="sxs-lookup"><span data-stu-id="e665e-162">#linktosearchresults</span></span> |<span data-ttu-id="e665e-163">Łącze tooLog analizy dziennika wyszukiwania, które zwraca hello rekordów w kwerendzie hello utworzony hello alert.</span><span class="sxs-lookup"><span data-stu-id="e665e-163">Link tooLog Analytics log search that returns hello records from hello query that created hello alert.</span></span> |
| <span data-ttu-id="e665e-164">ResultCount</span><span class="sxs-lookup"><span data-stu-id="e665e-164">ResultCount</span></span> |<span data-ttu-id="e665e-165">#searchresultcount</span><span class="sxs-lookup"><span data-stu-id="e665e-165">#searchresultcount</span></span> |<span data-ttu-id="e665e-166">Liczba rekordów w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="e665e-166">Number of records in hello search results.</span></span> |
| <span data-ttu-id="e665e-167">SearchIntervalEndtimeUtc</span><span class="sxs-lookup"><span data-stu-id="e665e-167">SearchIntervalEndtimeUtc</span></span> |<span data-ttu-id="e665e-168">#searchintervalendtimeutc</span><span class="sxs-lookup"><span data-stu-id="e665e-168">#searchintervalendtimeutc</span></span> |<span data-ttu-id="e665e-169">Godzina zakończenia hello zapytania w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="e665e-169">End time for hello query in UTC format.</span></span> |
| <span data-ttu-id="e665e-170">SearchIntervalInSeconds</span><span class="sxs-lookup"><span data-stu-id="e665e-170">SearchIntervalInSeconds</span></span> |<span data-ttu-id="e665e-171">#searchinterval</span><span class="sxs-lookup"><span data-stu-id="e665e-171">#searchinterval</span></span> |<span data-ttu-id="e665e-172">Przedział czasu dla hello reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="e665e-172">Time window for hello alert rule.</span></span> |
| <span data-ttu-id="e665e-173">SearchIntervalStartTimeUtc</span><span class="sxs-lookup"><span data-stu-id="e665e-173">SearchIntervalStartTimeUtc</span></span> |<span data-ttu-id="e665e-174">#searchintervalstarttimeutc</span><span class="sxs-lookup"><span data-stu-id="e665e-174">#searchintervalstarttimeutc</span></span> |<span data-ttu-id="e665e-175">Godzina rozpoczęcia dla zapytania hello w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="e665e-175">Start time for hello query in UTC format.</span></span> |
| <span data-ttu-id="e665e-176">SearchQuery</span><span class="sxs-lookup"><span data-stu-id="e665e-176">SearchQuery</span></span> |<span data-ttu-id="e665e-177">#searchquery</span><span class="sxs-lookup"><span data-stu-id="e665e-177">#searchquery</span></span> |<span data-ttu-id="e665e-178">Używane przez reguły alertu hello zapytania wyszukiwania dziennika.</span><span class="sxs-lookup"><span data-stu-id="e665e-178">Log search query used by hello alert rule.</span></span> |
| <span data-ttu-id="e665e-179">Wynikówwyszukiwania</span><span class="sxs-lookup"><span data-stu-id="e665e-179">SearchResults</span></span> |<span data-ttu-id="e665e-180">Zobacz poniżej</span><span class="sxs-lookup"><span data-stu-id="e665e-180">See below</span></span> |<span data-ttu-id="e665e-181">Rekordów zwróconych przez zapytanie hello w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="e665e-181">Records returned by hello query in JSON format.</span></span>  <span data-ttu-id="e665e-182">Ograniczone toohello najpierw 5000 rekordów.</span><span class="sxs-lookup"><span data-stu-id="e665e-182">Limited toohello first 5,000 records.</span></span> |
| <span data-ttu-id="e665e-183">WorkspaceID</span><span class="sxs-lookup"><span data-stu-id="e665e-183">WorkspaceID</span></span> |<span data-ttu-id="e665e-184">#workspaceid</span><span class="sxs-lookup"><span data-stu-id="e665e-184">#workspaceid</span></span> |<span data-ttu-id="e665e-185">Identyfikator obszaru roboczego OMS.</span><span class="sxs-lookup"><span data-stu-id="e665e-185">ID of your OMS workspace.</span></span> |

<span data-ttu-id="e665e-186">Na przykład można określić następujące niestandardowy ładunek, który zawiera jeden parametr o nazwie hello *tekstu*.</span><span class="sxs-lookup"><span data-stu-id="e665e-186">For example, you might specify hello following custom payload that includes a single parameter called *text*.</span></span>  <span data-ttu-id="e665e-187">Usługa Hello, który odwołuje się ten element webhook czy oczekiwano tego parametru.</span><span class="sxs-lookup"><span data-stu-id="e665e-187">hello service that this webhook calls would be expecting this parameter.</span></span>

    {
        "text":"#alertrulename fired with #searchresultcount over threshold of #thresholdvalue."
    }

<span data-ttu-id="e665e-188">Ten przykładowy ładunek rozwiąże toosomething jak powitania po kiedy wysłanych toohello elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="e665e-188">This example payload would resolve toosomething like hello following when sent toohello webhook.</span></span>

    {
        "text":"My Alert Rule fired with 18 records over threshold of 10 ."
    }

<span data-ttu-id="e665e-189">wyniki wyszukiwania tooinclude w ładunku niestandardowego, Dodaj powitania po wierszu jako właściwość najwyższego poziomu w ładunku json hello.</span><span class="sxs-lookup"><span data-stu-id="e665e-189">tooinclude search results in a custom payload, add hello following line as a top level property in hello json payload.</span></span>  

    "IncludeSearchResults":true

<span data-ttu-id="e665e-190">Na przykład toocreate niestandardowy ładunek, zawierający tylko nazwę alertu hello i hello wyniki wyszukiwania można powitania po.</span><span class="sxs-lookup"><span data-stu-id="e665e-190">For example, toocreate a custom payload that includes just hello alert name and hello search results, you could use hello following.</span></span> 

    {
       "alertname":"#alertrulename",
       "IncludeSearchResults":true
    }


<span data-ttu-id="e665e-191">Można przeprowadzić za pomocą pełny przykład tworzenie reguły alertu z toostart elementu webhook zewnętrznej usługi na [utworzenie alertu elementu webhook w tooSlack komunikat toosend analizy dzienników OMS](log-analytics-alerts-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="e665e-191">You can walk through a complete example of creating an alert rule with a webhook toostart an external service at [Create an alert webhook action in OMS Log Analytics toosend message tooSlack](log-analytics-alerts-webhooks.md).</span></span>

## <a name="runbook-actions"></a><span data-ttu-id="e665e-192">Działania elementu Runbook</span><span class="sxs-lookup"><span data-stu-id="e665e-192">Runbook actions</span></span>
<span data-ttu-id="e665e-193">Działania elementu Runbook uruchamiania elementu runbook automatyzacji Azure.</span><span class="sxs-lookup"><span data-stu-id="e665e-193">Runbook actions start a runbook in Azure Automation.</span></span>  <span data-ttu-id="e665e-194">W celu toouse tego typu akcji, musisz mieć hello [rozwiązania automatyzacja](log-analytics-add-solutions.md) zainstalowany i skonfigurowany w obszarze roboczym pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="e665e-194">In order toouse this type of action, you must have hello [Automation solution](log-analytics-add-solutions.md) installed and configured in your OMS workspace.</span></span>  <span data-ttu-id="e665e-195">Możesz wybrać elementów runbook hello na koncie automatyzacji hello, skonfigurowanego w hello rozwiązanie Automatyzacja.</span><span class="sxs-lookup"><span data-stu-id="e665e-195">You can select from hello runbooks in hello automation account that you configured in hello Automation solution.</span></span>

<span data-ttu-id="e665e-196">Działania elementu Runbook wymagają właściwości hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="e665e-196">Runbook actions require hello properties in hello following table.</span></span>

| <span data-ttu-id="e665e-197">Właściwość</span><span class="sxs-lookup"><span data-stu-id="e665e-197">Property</span></span> | <span data-ttu-id="e665e-198">Opis</span><span class="sxs-lookup"><span data-stu-id="e665e-198">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="e665e-199">Element Runbook</span><span class="sxs-lookup"><span data-stu-id="e665e-199">Runbook</span></span> | <span data-ttu-id="e665e-200">Element Runbook ma toostart, podczas tworzenia alertu.</span><span class="sxs-lookup"><span data-stu-id="e665e-200">Runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="e665e-201">Uruchom na</span><span class="sxs-lookup"><span data-stu-id="e665e-201">Run on</span></span> | <span data-ttu-id="e665e-202">Określ **Azure** toorun runbook hello w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="e665e-202">Specify **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="e665e-203">Określ **hybrydowy proces roboczy** toorun runbook hello na agenta o [hybrydowy proces roboczy elementu Runbook](../automation/automation-hybrid-runbook-worker.md ) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="e665e-203">Specify **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |

<span data-ttu-id="e665e-204">Działania elementu Runbook start hello runbook za pomocą [webhook](../automation/automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="e665e-204">Runbook actions start hello runbook using a [webhook](../automation/automation-webhooks.md).</span></span>  <span data-ttu-id="e665e-205">Podczas tworzenia reguły alertu hello automatycznie zostanie utworzony nowy element webhook dla elementu runbook hello o nazwie hello **OMS Alert korygowania** następuje identyfikator GUID.</span><span class="sxs-lookup"><span data-stu-id="e665e-205">When you create hello alert rule, it will automatically create a new webhook for hello runbook with hello name **OMS Alert Remediation** followed by a GUID.</span></span>  

<span data-ttu-id="e665e-206">Nie można bezpośrednio wypełnić żadnych parametrów elementu hello runbook ale hello [parametru $WebhookData](../automation/automation-webhooks.md) będzie zawierał hello szczegółów alertu hello, w tym hello wyniki wyszukiwania hello dziennika, który go utworzył.</span><span class="sxs-lookup"><span data-stu-id="e665e-206">You cannot directly populate any parameters of hello runbook, but hello [$WebhookData parameter](../automation/automation-webhooks.md) will include hello details of hello alert, including hello results of hello log search that created it.</span></span>  <span data-ttu-id="e665e-207">Witaj runbook należy toodefine **$WebhookData** jako parametru dla niego tooaccess hello właściwości hello alertu.</span><span class="sxs-lookup"><span data-stu-id="e665e-207">hello runbook will need toodefine **$WebhookData** as a parameter for it tooaccess hello properties of hello alert.</span></span>  <span data-ttu-id="e665e-208">Witaj dane alertów jest dostępny w formacie json w jedną właściwość o nazwie **wynikówwyszukiwania** w hello **RequestBody** właściwość **$WebhookData**.</span><span class="sxs-lookup"><span data-stu-id="e665e-208">hello alert data is available in json format in a single property called **SearchResults** in hello **RequestBody** property of **$WebhookData**.</span></span>  <span data-ttu-id="e665e-209">Będzie to mieć z właściwościami hello w hello w poniższej tabeli.</span><span class="sxs-lookup"><span data-stu-id="e665e-209">This will have with hello properties in hello following table.</span></span>

| <span data-ttu-id="e665e-210">Węzeł</span><span class="sxs-lookup"><span data-stu-id="e665e-210">Node</span></span> | <span data-ttu-id="e665e-211">Opis</span><span class="sxs-lookup"><span data-stu-id="e665e-211">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e665e-212">id</span><span class="sxs-lookup"><span data-stu-id="e665e-212">id</span></span> |<span data-ttu-id="e665e-213">Ścieżka i identyfikator GUID hello wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e665e-213">Path and GUID of hello search.</span></span> |
| <span data-ttu-id="e665e-214">__metadata</span><span class="sxs-lookup"><span data-stu-id="e665e-214">__metadata</span></span> |<span data-ttu-id="e665e-215">Informacje o hello alertu łącznie hello liczba rekordów i stanie hello wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e665e-215">Information about hello alert including hello number of records and status of hello search results.</span></span> |
| <span data-ttu-id="e665e-216">wartość</span><span class="sxs-lookup"><span data-stu-id="e665e-216">value</span></span> |<span data-ttu-id="e665e-217">Oddzielny wpis dla każdego rekordu w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="e665e-217">Separate entry for each record in hello search results.</span></span>  <span data-ttu-id="e665e-218">Szczegóły Hello hello wpis będzie zgodny hello właściwości i wartości rekordu hello.</span><span class="sxs-lookup"><span data-stu-id="e665e-218">hello details of hello entry will match hello properties and values of hello record.</span></span> |

<span data-ttu-id="e665e-219">Na przykład hello następujący element runbook będzie wyodrębnienie hello rekordów zwróconych przez hello dziennik wyszukiwania i przypisać różne właściwości na podstawie typu hello każdego rekordu.</span><span class="sxs-lookup"><span data-stu-id="e665e-219">For example, hello following runbook would extract hello records returned by hello log search  and assign different properties based on hello type of each record.</span></span>  <span data-ttu-id="e665e-220">Należy zwrócić uwagę hello elementu runbook rozpoczyna się od konwertowanie **RequestBody** z formatu json, którego nie można pracować z jako obiekt w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e665e-220">Note that hello runbook starts by converting **RequestBody** from json so that it can be worked with as an object in PowerShell.</span></span>

    param ( 
        [object]$WebhookData
    )

    $RequestBody = ConvertFrom-JSON -InputObject $WebhookData.RequestBody
    $Records     = $RequestBody.SearchResults.value

    foreach ($Record in $Records)
    {
        $Computer = $Record.Computer

        if ($Record.Type -eq 'Event')
        {
            $EventNo    = $Record.EventID
            $EventLevel = $Record.EventLevelName
            $EventData  = $Record.EventData
        }

        if ($Record.Type -eq 'Perf')
        {
            $Object    = $Record.ObjectName
            $Counter   = $Record.CounterName
            $Instance  = $Record.InstanceName
            $Value     = $Record.CounterValue
        }
    }


## <a name="next-steps"></a><span data-ttu-id="e665e-221">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e665e-221">Next steps</span></span>
- <span data-ttu-id="e665e-222">Zakończenie wskazówki dla [Konfigurowanie webook](log-analytics-alerts-webhooks.md) z reguły alertu.</span><span class="sxs-lookup"><span data-stu-id="e665e-222">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
- <span data-ttu-id="e665e-223">Dowiedz się, jak toowrite [elementy runbook automatyzacji Azure](https://azure.microsoft.com/documentation/services/automation) problemów tooremediate identyfikowana na podstawie alertów.</span><span class="sxs-lookup"><span data-stu-id="e665e-223">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>
