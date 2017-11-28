---
title: "Zrozumienie schematu elementu webhook używane w alertach dziennika aktywności | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat schematu JSON, zamieszczony na adres URL elementu webhook, aktywuje alert dziennika aktywności."
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
ms.openlocfilehash: 75c71bcd16573d4f4dd3377c623aa9b414aa3906
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a><span data-ttu-id="e95f9-103">Elementów Webhook alertów dziennik aktywności platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e95f9-103">Webhooks for Azure activity log alerts</span></span>
<span data-ttu-id="e95f9-104">W ramach definicji grupę można skonfigurować elementu webhook punktów końcowych, aby otrzymywać powiadomienia o alertach dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="e95f9-104">As part of the definition of an action group, you can configure webhook endpoints to receive activity log alert notifications.</span></span> <span data-ttu-id="e95f9-105">Z elementów webhook można kierować te powiadomienia do innych systemów akcje przetwarzania końcowego lub niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="e95f9-105">With webhooks, you can route these notifications to other systems for post-processing or custom actions.</span></span> <span data-ttu-id="e95f9-106">W tym artykule opisano, jak wygląda ładunek dla HTTP POST do elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="e95f9-106">This article shows what the payload for the HTTP POST to a webhook looks like.</span></span>

<span data-ttu-id="e95f9-107">Aby uzyskać więcej informacji dotyczących alertów dziennika aktywności, zobacz temat jak [tworzyć działanie Azure alerty dziennika](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e95f9-107">For more information on activity log alerts, see how to [create Azure activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="e95f9-108">Informacji dotyczących grup akcji, zobacz temat jak [tworzenie grup akcji](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="e95f9-108">For information on action groups, see how to [create action groups](monitoring-action-groups.md).</span></span>

## <a name="authenticate-the-webhook"></a><span data-ttu-id="e95f9-109">Uwierzytelnianie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="e95f9-109">Authenticate the webhook</span></span>
<span data-ttu-id="e95f9-110">Elementu webhook można używać do uwierzytelniania opartego na tokenie autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="e95f9-110">The webhook can optionally use token-based authorization for authentication.</span></span> <span data-ttu-id="e95f9-111">Identyfikator URI jest na przykład zapisane przy użyciu Identyfikatora tokenu elementu webhook `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span><span class="sxs-lookup"><span data-stu-id="e95f9-111">The webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.</span></span>

## <a name="payload-schema"></a><span data-ttu-id="e95f9-112">Schemat ładunku</span><span class="sxs-lookup"><span data-stu-id="e95f9-112">Payload schema</span></span>
<span data-ttu-id="e95f9-113">Ładunek JSON zawarte w operacji POST różni się na podstawie w polu data.context.activityLog.eventSource ładunku.</span><span class="sxs-lookup"><span data-stu-id="e95f9-113">The JSON payload contained in the POST operation differs based on the payload's data.context.activityLog.eventSource field.</span></span>

###<a name="common"></a><span data-ttu-id="e95f9-114">Wspólne</span><span class="sxs-lookup"><span data-stu-id="e95f9-114">Common</span></span>
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
###<a name="administrative"></a><span data-ttu-id="e95f9-115">Administracyjne</span><span class="sxs-lookup"><span data-stu-id="e95f9-115">Administrative</span></span>
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
###<a name="servicehealth"></a><span data-ttu-id="e95f9-116">ServiceHealth</span><span class="sxs-lookup"><span data-stu-id="e95f9-116">ServiceHealth</span></span>
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

<span data-ttu-id="e95f9-117">Szczegółowe schematu usługi kondycji powiadomień działania dziennika alertów, patrz [usługi powiadomień o kondycji](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="e95f9-117">For specific schema details on service health notification activity log alerts, see [Service health notifications](monitoring-service-notifications.md).</span></span>

<span data-ttu-id="e95f9-118">Dla określonego schematu informacji na temat wszystkich innych alertów dziennika aktywności, zobacz [omówienie dziennik aktywności platformy Azure](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e95f9-118">For specific schema details on all other activity log alerts, see [Overview of the Azure activity log](monitoring-overview-activity-logs.md).</span></span>

| <span data-ttu-id="e95f9-119">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="e95f9-119">Element name</span></span> | <span data-ttu-id="e95f9-120">Opis</span><span class="sxs-lookup"><span data-stu-id="e95f9-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e95f9-121">status</span><span class="sxs-lookup"><span data-stu-id="e95f9-121">status</span></span> |<span data-ttu-id="e95f9-122">Używany w przypadku alertów metryki.</span><span class="sxs-lookup"><span data-stu-id="e95f9-122">Used for metric alerts.</span></span> <span data-ttu-id="e95f9-123">Zawsze ustawiony na "aktywowanego" dla alertów dotyczących działań w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="e95f9-123">Always set to "activated" for activity log alerts.</span></span> |
| <span data-ttu-id="e95f9-124">Kontekst</span><span class="sxs-lookup"><span data-stu-id="e95f9-124">context</span></span> |<span data-ttu-id="e95f9-125">Kontekst zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e95f9-125">Context of the event.</span></span> |
| <span data-ttu-id="e95f9-126">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="e95f9-126">resourceProviderName</span></span> |<span data-ttu-id="e95f9-127">Dostawca zasobów ryzyko zasobów.</span><span class="sxs-lookup"><span data-stu-id="e95f9-127">The resource provider of the impacted resource.</span></span> |
| <span data-ttu-id="e95f9-128">conditionType</span><span class="sxs-lookup"><span data-stu-id="e95f9-128">conditionType</span></span> |<span data-ttu-id="e95f9-129">Zawsze "Event".</span><span class="sxs-lookup"><span data-stu-id="e95f9-129">Always "Event."</span></span> |
| <span data-ttu-id="e95f9-130">name</span><span class="sxs-lookup"><span data-stu-id="e95f9-130">name</span></span> |<span data-ttu-id="e95f9-131">Nazwa reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="e95f9-131">Name of the alert rule.</span></span> |
| <span data-ttu-id="e95f9-132">id</span><span class="sxs-lookup"><span data-stu-id="e95f9-132">id</span></span> |<span data-ttu-id="e95f9-133">Identyfikator zasobu alertu.</span><span class="sxs-lookup"><span data-stu-id="e95f9-133">Resource ID of the alert.</span></span> |
| <span data-ttu-id="e95f9-134">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="e95f9-134">description</span></span> |<span data-ttu-id="e95f9-135">Opis alertu ustawić podczas tworzenia alertu.</span><span class="sxs-lookup"><span data-stu-id="e95f9-135">Alert description set when the alert is created.</span></span> |
| <span data-ttu-id="e95f9-136">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="e95f9-136">subscriptionId</span></span> |<span data-ttu-id="e95f9-137">Identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e95f9-137">Azure subscription ID.</span></span> |
| <span data-ttu-id="e95f9-138">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="e95f9-138">timestamp</span></span> |<span data-ttu-id="e95f9-139">Czas, w którym to zdarzenie zostało wygenerowane przez usługę Azure, który przetwarzał żądanie.</span><span class="sxs-lookup"><span data-stu-id="e95f9-139">Time at which the event was generated by the Azure service that processed the request.</span></span> |
| <span data-ttu-id="e95f9-140">resourceId</span><span class="sxs-lookup"><span data-stu-id="e95f9-140">resourceId</span></span> |<span data-ttu-id="e95f9-141">Identyfikator zasobu ryzyko zasobu.</span><span class="sxs-lookup"><span data-stu-id="e95f9-141">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="e95f9-142">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="e95f9-142">resourceGroupName</span></span> |<span data-ttu-id="e95f9-143">Nazwa grupy zasobów dla zasobu ryzyko.</span><span class="sxs-lookup"><span data-stu-id="e95f9-143">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="e95f9-144">properties</span><span class="sxs-lookup"><span data-stu-id="e95f9-144">properties</span></span> |<span data-ttu-id="e95f9-145">Zestaw `<Key, Value>` par (czyli `Dictionary<String, String>`) zawierającą szczegółowe informacje o zdarzeniu.</span><span class="sxs-lookup"><span data-stu-id="e95f9-145">Set of `<Key, Value>` pairs (that is, `Dictionary<String, String>`) that includes details about the event.</span></span> |
| <span data-ttu-id="e95f9-146">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="e95f9-146">event</span></span> |<span data-ttu-id="e95f9-147">Element zawierający metadane dotyczące zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e95f9-147">Element that contains metadata about the event.</span></span> |
| <span data-ttu-id="e95f9-148">Autoryzacji</span><span class="sxs-lookup"><span data-stu-id="e95f9-148">authorization</span></span> |<span data-ttu-id="e95f9-149">Właściwości kontroli dostępu opartej na rolach zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e95f9-149">The Role-Based Access Control properties of the event.</span></span> <span data-ttu-id="e95f9-150">Te właściwości obejmują zazwyczaj akcji, roli i zakresu.</span><span class="sxs-lookup"><span data-stu-id="e95f9-150">These properties usually include the action, the role, and the scope.</span></span> |
| <span data-ttu-id="e95f9-151">category</span><span class="sxs-lookup"><span data-stu-id="e95f9-151">category</span></span> |<span data-ttu-id="e95f9-152">Kategoria zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e95f9-152">Category of the event.</span></span> <span data-ttu-id="e95f9-153">Obsługiwane wartości to administracyjne, Alert zabezpieczeń, ServiceHealth i zalecenia.</span><span class="sxs-lookup"><span data-stu-id="e95f9-153">Supported values include Administrative, Alert, Security, ServiceHealth, and Recommendation.</span></span> |
| <span data-ttu-id="e95f9-154">obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="e95f9-154">caller</span></span> |<span data-ttu-id="e95f9-155">Adres e-mail użytkownika, który wykonał operację, oświadczenia UPN lub nazwy SPN oświadczenia na podstawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="e95f9-155">Email address of the user who performed the operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="e95f9-156">Może mieć wartości null dla niektórych wywołań systemowych.</span><span class="sxs-lookup"><span data-stu-id="e95f9-156">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="e95f9-157">correlationId</span><span class="sxs-lookup"><span data-stu-id="e95f9-157">correlationId</span></span> |<span data-ttu-id="e95f9-158">Zazwyczaj identyfikator GUID w postaci ciągu.</span><span class="sxs-lookup"><span data-stu-id="e95f9-158">Usually a GUID in string format.</span></span> <span data-ttu-id="e95f9-159">Zdarzenia z correlationId należą do tego samego działania większych i zazwyczaj udziału correlationId.</span><span class="sxs-lookup"><span data-stu-id="e95f9-159">Events with correlationId belong to the same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="e95f9-160">eventDescription</span><span class="sxs-lookup"><span data-stu-id="e95f9-160">eventDescription</span></span> |<span data-ttu-id="e95f9-161">Opis zdarzenia tekst statyczny.</span><span class="sxs-lookup"><span data-stu-id="e95f9-161">Static text description of the event.</span></span> |
| <span data-ttu-id="e95f9-162">eventDataId</span><span class="sxs-lookup"><span data-stu-id="e95f9-162">eventDataId</span></span> |<span data-ttu-id="e95f9-163">Unikatowy identyfikator zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e95f9-163">Unique identifier for the event.</span></span> |
| <span data-ttu-id="e95f9-164">Źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="e95f9-164">eventSource</span></span> |<span data-ttu-id="e95f9-165">Nazwa usługi Azure lub infrastruktury, który wygenerował zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="e95f9-165">Name of the Azure service or infrastructure that generated the event.</span></span> |
| <span data-ttu-id="e95f9-166">httpRequest</span><span class="sxs-lookup"><span data-stu-id="e95f9-166">httpRequest</span></span> |<span data-ttu-id="e95f9-167">Żądanie obejmuje zazwyczaj clientRequestId, clientIpAddress i metodę HTTP (na przykład umieścić).</span><span class="sxs-lookup"><span data-stu-id="e95f9-167">The request usually includes the clientRequestId, clientIpAddress, and HTTP method (for example, PUT).</span></span> |
| <span data-ttu-id="e95f9-168">poziom</span><span class="sxs-lookup"><span data-stu-id="e95f9-168">level</span></span> |<span data-ttu-id="e95f9-169">Jedną z następujących wartości: krytyczny, błąd, ostrzeżenie, informacyjny i pełne.</span><span class="sxs-lookup"><span data-stu-id="e95f9-169">One of the following values: Critical, Error, Warning, Informational, and Verbose.</span></span> |
| <span data-ttu-id="e95f9-170">operationId</span><span class="sxs-lookup"><span data-stu-id="e95f9-170">operationId</span></span> |<span data-ttu-id="e95f9-171">Zazwyczaj identyfikator GUID współdzielenia zdarzenia odpowiadające jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="e95f9-171">Usually a GUID shared among the events corresponding to single operation.</span></span> |
| <span data-ttu-id="e95f9-172">operationName</span><span class="sxs-lookup"><span data-stu-id="e95f9-172">operationName</span></span> |<span data-ttu-id="e95f9-173">Nazwa operacji.</span><span class="sxs-lookup"><span data-stu-id="e95f9-173">Name of the operation.</span></span> |
| <span data-ttu-id="e95f9-174">properties</span><span class="sxs-lookup"><span data-stu-id="e95f9-174">properties</span></span> |<span data-ttu-id="e95f9-175">Właściwości zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="e95f9-175">Properties of the event.</span></span> |
| <span data-ttu-id="e95f9-176">status</span><span class="sxs-lookup"><span data-stu-id="e95f9-176">status</span></span> |<span data-ttu-id="e95f9-177">Ciąg.</span><span class="sxs-lookup"><span data-stu-id="e95f9-177">String.</span></span> <span data-ttu-id="e95f9-178">Stan operacji.</span><span class="sxs-lookup"><span data-stu-id="e95f9-178">Status of the operation.</span></span> <span data-ttu-id="e95f9-179">Typowe wartości to rozpoczęte, w toku, zakończyło się pomyślnie, nie powiodło się, aktywnych i rozwiązanych.</span><span class="sxs-lookup"><span data-stu-id="e95f9-179">Common values include Started, In Progress, Succeeded, Failed, Active, and Resolved.</span></span> |
| <span data-ttu-id="e95f9-180">Podstan</span><span class="sxs-lookup"><span data-stu-id="e95f9-180">subStatus</span></span> |<span data-ttu-id="e95f9-181">Zwykle zawiera kod stanu HTTP odpowiedniego wywołania REST.</span><span class="sxs-lookup"><span data-stu-id="e95f9-181">Usually includes the HTTP status code of the corresponding REST call.</span></span> <span data-ttu-id="e95f9-182">Może również zawierać innych ciągów, które opisują podstanu.</span><span class="sxs-lookup"><span data-stu-id="e95f9-182">It might also include other strings that describe a substatus.</span></span> <span data-ttu-id="e95f9-183">Typowe wartości podstanu obejmują OK (kod stanu HTTP: 200), utworzony (kod stanu HTTP: 201), akceptowane (kod stanu HTTP: 202), nie zawartości (kod stanu HTTP: 204), nieprawidłowe żądanie (kod stanu HTTP: 400), nie znaleziono (kod stanu HTTP: 404), konflikt (kod stanu HTTP: 409), wewnętrzny błąd serwera (kod stanu HTTP: 500), Usługa niedostępna (kod stanu HTTP: 503) i limit czasu bramy (kod stanu HTTP : 504).</span><span class="sxs-lookup"><span data-stu-id="e95f9-183">Common substatus values include OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), and Gateway Timeout (HTTP Status Code: 504).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e95f9-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e95f9-184">Next steps</span></span>
* <span data-ttu-id="e95f9-185">[Dowiedz się więcej o dziennika aktywności](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="e95f9-185">[Learn more about the activity log](monitoring-overview-activity-logs.md).</span></span>
* <span data-ttu-id="e95f9-186">[Wykonywanie skryptów automatyzacji Azure (elementów Runbook) Azure alerty](http://go.microsoft.com/fwlink/?LinkId=627081).</span><span class="sxs-lookup"><span data-stu-id="e95f9-186">[Execute Azure automation scripts (Runbooks) on Azure alerts](http://go.microsoft.com/fwlink/?LinkId=627081).</span></span>
* <span data-ttu-id="e95f9-187">[Wyślij wiadomość SMS za pośrednictwem usługi Twilio z poziomu alertu Azure przy użyciu aplikacji logiki](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="e95f9-187">[Use a logic app to send an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="e95f9-188">W tym przykładzie jest metryki alertów, ale można go modyfikować do pracy z alert dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="e95f9-188">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="e95f9-189">[Użyj aplikacji logiki, aby wysłać wiadomość Slack z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="e95f9-189">[Use a logic app to send a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="e95f9-190">W tym przykładzie jest metryki alertów, ale można go modyfikować do pracy z alert dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="e95f9-190">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
* <span data-ttu-id="e95f9-191">[Użyj aplikacji logiki, aby wysłać komunikat do kolejki systemu Azure z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="e95f9-191">[Use a logic app to send a message to an Azure queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="e95f9-192">W tym przykładzie jest metryki alertów, ale można go modyfikować do pracy z alert dziennika aktywności.</span><span class="sxs-lookup"><span data-stu-id="e95f9-192">This example is for metric alerts, but it can be modified to work with an activity log alert.</span></span>
