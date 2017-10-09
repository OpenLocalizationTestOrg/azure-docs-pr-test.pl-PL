---
title: "Schemat elementu webhook hello aaaUnderstand używane w alertach dziennika aktywności | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat schematu hello hello JSON publikowanego adresu URL elementu webhook tooa gdy aktywuje alert dziennika aktywności."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="7a825-103">Elementów Webhook alertów dziennik aktywności platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7a825-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="7a825-104">W ramach definicji hello grupę można skonfigurować elementu webhook punkty końcowe tooreceive działania dziennik powiadomień o alertach.</span><span class="sxs-lookup"><span data-stu-id="7a825-104">As part of hello definition of an action group, you can configure webhook endpoints tooreceive activity log alert notifications.</span></span> <span data-ttu-id="7a825-105">Z elementów webhook można kierować te systemy tooother powiadomienia dla akcje przetwarzania końcowego lub niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="7a825-105">With webhooks, you can route these notifications tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="7a825-106">W tym artykule opisano, jakie ładunku hello hello HTTP POST tooa elementu webhook wygląda jak.</span><span class="sxs-lookup"><span data-stu-id="7a825-106">This article shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span>

<span data-ttu-id="7a825-107">Aby uzyskać więcej informacji dotyczących alertów dziennika aktywności, zobacz jak zbyt[tworzyć działanie Azure alerty dziennika](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7a825-107">For more information on activity log alerts, see how too[create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="7a825-108">Informacji dotyczących grup akcji, zobacz temat jak zbyt[tworzenie grup akcji](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="7a825-108">For information on action groups, see how too[create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-hello-webhook"></a><span data-ttu-id="7a825-109">Uwierzytelnianie hello elementu webhook</span><span class="sxs-lookup"><span data-stu-id="7a825-109">Authenticate hello webhook</span></span>
<span data-ttu-id="7a825-110">Element webhook Hello można używać autoryzacji na podstawie tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="7a825-110">hello webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="7a825-111">Witaj webhook identyfikatora URI jest zapisane przy użyciu Identyfikatora tokenu, na przykład `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="7a825-111">hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="7a825-112">Schemat ładunku</span><span class="sxs-lookup"><span data-stu-id="7a825-112">Payload schema</span></span>
<span data-ttu-id="7a825-113">ładunek JSON Hello zawarte w hello operację POST różni się na podstawie w polu data.context.activityLog.eventSource hello ładunku.</span><span class="sxs-lookup"><span data-stu-id="7a825-113">hello JSON payload contained in hello POST operation differs based on hello payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="7a825-114">Wspólne</span><span class="sxs-lookup"><span data-stu-id="7a825-114">Common</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a><span data-ttu-id="7a825-115">Administracyjne</span><span class="sxs-lookup"><span data-stu-id="7a825-115">Administrative</span></span>
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a><span data-ttu-id="7a825-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="7a825-116">ServiceHealth</span></span>
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

<span data-ttu-id="7a825-117">Szczegółowe schematu usługi kondycji powiadomień działania dziennika alertów, patrz [usługi powiadomień o kondycji](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="7a825-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="7a825-118">Dla określonego schematu informacji na temat wszystkich innych alertów dziennika aktywności, zobacz [omówienie dziennik aktywności platformy Azure hello](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="7a825-118">For specific schema details on all other activity log alerts, see [Overview of hello Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="7a825-119">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="7a825-119">Element name</span></span> | <span data-ttu-id="7a825-120">Opis</span><span class="sxs-lookup"><span data-stu-id="7a825-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7a825-121">status</span><span class="sxs-lookup"><span data-stu-id="7a825-121">status</span></span> |<span data-ttu-id="7a825-122">Używany w przypadku alertów metryki.</span><span class="sxs-lookup"><span data-stu-id="7a825-122">Used for metric alerts.</span></span> <span data-ttu-id="7a825-123">Zawsze ustawiona zbyt "aktywowanego" dla alertów dotyczących działań w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="7a825-123">Always set too"activated" for activity log alerts.</span></span> |
| <span data-ttu-id="7a825-124">Kontekst</span><span class="sxs-lookup"><span data-stu-id="7a825-124">context</span></span> |<span data-ttu-id="7a825-125">Kontekst hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7a825-125">Context of hello event.</span></span> |
| <span data-ttu-id="7a825-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7a825-126">resourceProviderName</span></span> |<span data-ttu-id="7a825-127">Dostawca zasobów Hello hello wpływ na zasobów.</span><span class="sxs-lookup"><span data-stu-id="7a825-127">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="7a825-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="7a825-128">conditionType</span></span> |<span data-ttu-id="7a825-129">Zawsze "Event".</span><span class="sxs-lookup"><span data-stu-id="7a825-129">Always "Event."</span></span> |
| <span data-ttu-id="7a825-130">name</span><span class="sxs-lookup"><span data-stu-id="7a825-130">name</span></span> |<span data-ttu-id="7a825-131">Nazwa reguły alertów hello.</span><span class="sxs-lookup"><span data-stu-id="7a825-131">Name of hello alert rule.</span></span> |
| <span data-ttu-id="7a825-132">id</span><span class="sxs-lookup"><span data-stu-id="7a825-132">id</span></span> |<span data-ttu-id="7a825-133">Identyfikator zasobu hello alertu.</span><span class="sxs-lookup"><span data-stu-id="7a825-133">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="7a825-134">description</span><span class="sxs-lookup"><span data-stu-id="7a825-134">description</span></span> |<span data-ttu-id="7a825-135">Opis alertu ustawić po utworzeniu hello alertu.</span><span class="sxs-lookup"><span data-stu-id="7a825-135">Alert description set when hello alert is created.</span></span> |
| <span data-ttu-id="7a825-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7a825-136">subscriptionId</span></span> |<span data-ttu-id="7a825-137">Identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7a825-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="7a825-138">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="7a825-138">timestamp</span></span> |<span data-ttu-id="7a825-139">Czas, w którym hello zdarzeń został wygenerowany przez hello usługa Azure, która hello żądanie.</span><span class="sxs-lookup"><span data-stu-id="7a825-139">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="7a825-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="7a825-140">resourceId</span></span> |<span data-ttu-id="7a825-141">Identyfikator zasobu hello wpływ na zasobów.</span><span class="sxs-lookup"><span data-stu-id="7a825-141">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="7a825-142">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="7a825-142">resourceGroupName</span></span> |<span data-ttu-id="7a825-143">Nazwa grupy zasobów hello hello wpływ na zasobów.</span><span class="sxs-lookup"><span data-stu-id="7a825-143">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="7a825-144">properties</span><span class="sxs-lookup"><span data-stu-id="7a825-144">properties</span></span> |<span data-ttu-id="7a825-145">Zestaw `<Key, Value>` par (czyli `Dictionary<String, String>`) zawierającą szczegóły dotyczące zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7a825-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="7a825-146">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="7a825-146">event</span></span> |<span data-ttu-id="7a825-147">Element zawierający metadane dotyczące zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7a825-147">Element that contains metadata about hello event.</span></span> |
| <span data-ttu-id="7a825-148">Autoryzacji</span><span class="sxs-lookup"><span data-stu-id="7a825-148">authorization</span></span> |<span data-ttu-id="7a825-149">właściwości kontroli dostępu opartej na rolach Hello hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7a825-149">hello Role-Based Access Control properties of hello event.</span></span> <span data-ttu-id="7a825-150">Te właściwości obejmują zazwyczaj hello akcji, hello roli i hello zakresu.</span><span class="sxs-lookup"><span data-stu-id="7a825-150">These properties usually include hello action, hello role, and hello scope.</span></span> |
| <span data-ttu-id="7a825-151">category</span><span class="sxs-lookup"><span data-stu-id="7a825-151">category</span></span> |<span data-ttu-id="7a825-152">Kategoria zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7a825-152">Category of hello event.</span></span> <span data-ttu-id="7a825-153">Obsługiwane wartości to administracyjne, Alert zabezpieczeń, ServiceHealth i zalecenia.</span><span class="sxs-lookup"><span data-stu-id="7a825-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="7a825-154">obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="7a825-154">caller</span></span> |<span data-ttu-id="7a825-155">Adres e-mail użytkownika hello, który wykonał operację hello, oświadczenia UPN lub nazwy SPN oświadczenia na podstawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="7a825-155">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="7a825-156">Może mieć wartości null dla niektórych wywołań systemowych.</span><span class="sxs-lookup"><span data-stu-id="7a825-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="7a825-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="7a825-157">correlationId</span></span> |<span data-ttu-id="7a825-158">Zazwyczaj identyfikator GUID w postaci ciągu.</span><span class="sxs-lookup"><span data-stu-id="7a825-158">Usually a GUID in string format.</span></span> <span data-ttu-id="7a825-159">Zdarzenia z correlationId należą toohello tę samą akcję większych i zwykle udostępnianie correlationId.</span><span class="sxs-lookup"><span data-stu-id="7a825-159">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="7a825-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="7a825-160">eventDescription</span></span> |<span data-ttu-id="7a825-161">Opis zdarzenia hello tekst statyczny.</span><span class="sxs-lookup"><span data-stu-id="7a825-161">Static text description of hello event.</span></span> |
| <span data-ttu-id="7a825-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7a825-162">eventDataId</span></span> |<span data-ttu-id="7a825-163">Unikatowy identyfikator dla hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7a825-163">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="7a825-164">Źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="7a825-164">eventSource</span></span> |<span data-ttu-id="7a825-165">Nazwa hello infrastruktury i usługa Azure hello wygenerowane zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="7a825-165">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="7a825-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="7a825-166">httpRequest</span></span> |<span data-ttu-id="7a825-167">Witaj żądanie obejmuje zazwyczaj hello clientRequestId, clientIpAddress i metodę HTTP (na przykład umieścić).</span><span class="sxs-lookup"><span data-stu-id="7a825-167">hello request usually includes hello clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="7a825-168">poziom</span><span class="sxs-lookup"><span data-stu-id="7a825-168">level</span></span> |<span data-ttu-id="7a825-169">Jeden z hello następujące wartości: krytyczny, błąd, ostrzeżenie, informacyjny i pełne.</span><span class="sxs-lookup"><span data-stu-id="7a825-169">One of hello following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="7a825-170">operationId</span><span class="sxs-lookup"><span data-stu-id="7a825-170">operationId</span></span> |<span data-ttu-id="7a825-171">Zazwyczaj identyfikator GUID współdzielenia zdarzenia hello odpowiadającego toosingle operacji.</span><span class="sxs-lookup"><span data-stu-id="7a825-171">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="7a825-172">operationName</span><span class="sxs-lookup"><span data-stu-id="7a825-172">operationName</span></span> |<span data-ttu-id="7a825-173">Nazwa operacji hello.</span><span class="sxs-lookup"><span data-stu-id="7a825-173">Name of hello operation.</span></span> |
| <span data-ttu-id="7a825-174">properties</span><span class="sxs-lookup"><span data-stu-id="7a825-174">properties</span></span> |<span data-ttu-id="7a825-175">Właściwości zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7a825-175">Properties of hello event.</span></span> |
| <span data-ttu-id="7a825-176">status</span><span class="sxs-lookup"><span data-stu-id="7a825-176">status</span></span> |<span data-ttu-id="7a825-177">Ciąg.</span><span class="sxs-lookup"><span data-stu-id="7a825-177">String.</span></span> <span data-ttu-id="7a825-178">Stan operacji hello.</span><span class="sxs-lookup"><span data-stu-id="7a825-178">Status of hello operation.</span></span> <span data-ttu-id="7a825-179">Typowe wartości to rozpoczęte, w toku, zakończyło się pomyślnie, nie powiodło się, aktywnych i rozwiązanych.</span><span class="sxs-lookup"><span data-stu-id="7a825-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="7a825-180">Podstan</span><span class="sxs-lookup"><span data-stu-id="7a825-180">subStatus</span></span> |<span data-ttu-id="7a825-181">Zwykle zawiera kod stanu HTTP hello hello odpowiedniego wywołania REST.</span><span class="sxs-lookup"><span data-stu-id="7a825-181">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="7a825-182">Może również zawierać innych ciągów, które opisują podstanu.</span><span class="sxs-lookup"><span data-stu-id="7a825-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="7a825-183">Typowe wartości podstanu obejmują OK (kod stanu HTTP: 200), utworzony (kod stanu HTTP: 201), akceptowane (kod stanu HTTP: 202), nie zawartości (kod stanu HTTP: 204), nieprawidłowe żądanie (kod stanu HTTP: 400), nie znaleziono (kod stanu HTTP: 404), konflikt (kod stanu HTTP: 409), wewnętrzny błąd serwera (kod stanu HTTP: 500), Usługa niedostępna (kod stanu HTTP: 503) i limit czasu bramy (kod stanu HTTP : 504).</span><span class="sxs-lookup"><span data-stu-id="7a825-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7a825-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7a825-184">Next steps</span></span>
* <span data-ttu-id="7a825-185">[Dowiedz się więcej o dziennik aktywności hello](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="7a825-185">[Learn more about hello activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="7a825-186">[Wykonywanie skryptów automatyzacji Azure (elementów Runbook) Azure alerty](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="7a825-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="7a825-187">[Użyj toosend aplikacji logiki programu SMS za pośrednictwem usługi Twilio z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="7a825-187">[Use a logic app toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="7a825-188">W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="7a825-188">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="7a825-189">[Użyj logiki aplikacji toosend Slack wiadomości z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="7a825-189">[Use a logic app toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="7a825-190">W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="7a825-190">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
* <span data-ttu-id="7a825-191">[Użyj toosend aplikacji logiki, kolejka wiadomości tooan Azure z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="7a825-191">[Use a logic app toosend a message tooan Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="7a825-192">W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="7a825-192">This example is for metric alerts, but it can be modified toowork with an activity log alert.</span></span>
