---
title: "aaaCall elementu webhook alerty dziennika aktywności platformy Azure | Dokumentacja firmy Microsoft"
description: "Trasy działania dziennika zdarzeń tooother usługi akcji niestandardowych. Na przykład wysyłanie SMS dziennika błędów lub powiadomić zespołu za pomocą rozmowy/wiadomości usługi."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a><span data-ttu-id="7cb82-104">Wywołanie elementu webhook alerty dziennika aktywności platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7cb82-104">Call a webhook on Azure Activity Log alerts</span></span>
<span data-ttu-id="7cb82-105">Elementów Webhook pozwalają tooroute Azure alertów systemów tooother powiadomień dla akcje przetwarzania końcowego lub niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="7cb82-105">Webhooks allow you tooroute an Azure alert notification tooother systems for post-processing or custom actions.</span></span> <span data-ttu-id="7cb82-106">Możesz użyć elementu webhook w alertu tooroute on tooservices wysyłających programu SMS, dziennika błędów, powiadamiania zespołu za pomocą usług wiadomości rozmów/lub czy dowolna liczba innych działań.</span><span class="sxs-lookup"><span data-stu-id="7cb82-106">You can use a webhook on an alert tooroute it tooservices that send SMS, log bugs, notify a team via chat/messaging services, or do any number of other actions.</span></span> <span data-ttu-id="7cb82-107">W tym artykule opisano, jak tooset webhook toobe wywoływane, gdy generowane alertu dziennika aktywności platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb82-107">This article describes how tooset a webhook toobe called when an Azure Activity Log alert fires.</span></span> <span data-ttu-id="7cb82-108">Przedstawia on także jakie ładunku hello hello HTTP POST tooa elementu webhook wygląda jak.</span><span class="sxs-lookup"><span data-stu-id="7cb82-108">It also shows what hello payload for hello HTTP POST tooa webhook looks like.</span></span> <span data-ttu-id="7cb82-109">Informacje dotyczące instalacji hello i schematu dla alertu metryki Azure [wyświetlona następująca strona](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7cb82-109">For information on hello setup and schema for an Azure metric alert, [see this page instead](insights-webhooks-alerts.md).</span></span> <span data-ttu-id="7cb82-110">Można również skonfigurować wiadomości e-mail alertów toosend dziennik aktywności po uaktywnieniu.</span><span class="sxs-lookup"><span data-stu-id="7cb82-110">You can also set up an Activity Log alert toosend email when activated.</span></span>

> [!NOTE]
> <span data-ttu-id="7cb82-111">Ta funkcja jest obecnie w wersji zapoznawczej i zostanie usunięta w pewnym momencie w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="7cb82-111">This feature is currently in preview and will be removed at some point in hello future.</span></span>
>
>

<span data-ttu-id="7cb82-112">Można skonfigurować przy użyciu hello alertu dziennik aktywności [poleceń cmdlet programu PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [interfejsu wiersza polecenia i Platform](insights-cli-samples.md#work-with-alerts), lub [interfejsu API REST Monitor Azure](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span><span class="sxs-lookup"><span data-stu-id="7cb82-112">You can set up an Activity Log alert using hello [Azure PowerShell Cmdlets](insights-powershell-samples.md#create-metric-alerts), [Cross-Platform CLI](insights-cli-samples.md#work-with-alerts), or [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn933805.aspx).</span></span> <span data-ttu-id="7cb82-113">Obecnie nie można ustawić jedną przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb82-113">Currently, you cannot set one up using hello Azure portal.</span></span>

## <a name="authenticating-hello-webhook"></a><span data-ttu-id="7cb82-114">Uwierzytelnianie hello elementu webhook</span><span class="sxs-lookup"><span data-stu-id="7cb82-114">Authenticating hello webhook</span></span>
<span data-ttu-id="7cb82-115">Element webhook Hello uwierzytelniania z użyciem jednej z tych metod:</span><span class="sxs-lookup"><span data-stu-id="7cb82-115">hello webhook can authenticate using either of these methods:</span></span>

1. <span data-ttu-id="7cb82-116">**Autoryzacji opartej na tokenach** — Witaj identyfikatora URI jest na przykład zapisane przy użyciu Identyfikatora token elementu webhook`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span><span class="sxs-lookup"><span data-stu-id="7cb82-116">**Token-based authorization** - hello webhook URI is saved with a token ID, for example, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`</span></span>
2. <span data-ttu-id="7cb82-117">**Podstawowe autoryzacji** — Witaj identyfikatora URI jest zapisane przy użyciu nazwy użytkownika i hasła, na przykład elementu webhook`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span><span class="sxs-lookup"><span data-stu-id="7cb82-117">**Basic authorization** - hello webhook URI is saved with a username and password, for example, `https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`</span></span>

## <a name="payload-schema"></a><span data-ttu-id="7cb82-118">Schemat ładunku</span><span class="sxs-lookup"><span data-stu-id="7cb82-118">Payload schema</span></span>
<span data-ttu-id="7cb82-119">Witaj operację POST zawiera hello ładunek JSON i schematu dla wszystkich dziennik aktywności na podstawie alertów.</span><span class="sxs-lookup"><span data-stu-id="7cb82-119">hello POST operation contains hello following JSON payload and schema for all Activity Log-based alerts.</span></span> <span data-ttu-id="7cb82-120">Ten schemat jest podobne toohello co najmniej jedna używana przez alerty na podstawie metryki.</span><span class="sxs-lookup"><span data-stu-id="7cb82-120">This schema is similar toohello one used by metric-based alerts.</span></span>

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| <span data-ttu-id="7cb82-121">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="7cb82-121">Element Name</span></span> | <span data-ttu-id="7cb82-122">Opis</span><span class="sxs-lookup"><span data-stu-id="7cb82-122">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7cb82-123">status</span><span class="sxs-lookup"><span data-stu-id="7cb82-123">status</span></span> |<span data-ttu-id="7cb82-124">Używany w przypadku alertów metryki.</span><span class="sxs-lookup"><span data-stu-id="7cb82-124">Used for metric alerts.</span></span> <span data-ttu-id="7cb82-125">Zawsze ustawiona zbyt "aktywowanego" alertów dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="7cb82-125">Always set too"activated" for Activity Log alerts.</span></span> |
| <span data-ttu-id="7cb82-126">Kontekst</span><span class="sxs-lookup"><span data-stu-id="7cb82-126">context</span></span> |<span data-ttu-id="7cb82-127">Kontekst hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7cb82-127">Context of hello event.</span></span> |
| <span data-ttu-id="7cb82-128">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7cb82-128">resourceProviderName</span></span> |<span data-ttu-id="7cb82-129">Dostawca zasobów Hello hello wpływ na zasobów.</span><span class="sxs-lookup"><span data-stu-id="7cb82-129">hello resource provider of hello impacted resource.</span></span> |
| <span data-ttu-id="7cb82-130">conditionType</span><span class="sxs-lookup"><span data-stu-id="7cb82-130">conditionType</span></span> |<span data-ttu-id="7cb82-131">Zawsze "Event".</span><span class="sxs-lookup"><span data-stu-id="7cb82-131">Always "Event."</span></span> |
| <span data-ttu-id="7cb82-132">name</span><span class="sxs-lookup"><span data-stu-id="7cb82-132">name</span></span> |<span data-ttu-id="7cb82-133">Nazwa reguły alertów hello.</span><span class="sxs-lookup"><span data-stu-id="7cb82-133">Name of hello alert rule.</span></span> |
| <span data-ttu-id="7cb82-134">id</span><span class="sxs-lookup"><span data-stu-id="7cb82-134">id</span></span> |<span data-ttu-id="7cb82-135">Identyfikator zasobu hello alertu.</span><span class="sxs-lookup"><span data-stu-id="7cb82-135">Resource ID of hello alert.</span></span> |
| <span data-ttu-id="7cb82-136">description</span><span class="sxs-lookup"><span data-stu-id="7cb82-136">description</span></span> |<span data-ttu-id="7cb82-137">Opis alertu jako zestaw podczas tworzenia alertu hello.</span><span class="sxs-lookup"><span data-stu-id="7cb82-137">Alert description as set during creation of hello alert.</span></span> |
| <span data-ttu-id="7cb82-138">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7cb82-138">subscriptionId</span></span> |<span data-ttu-id="7cb82-139">Identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7cb82-139">Azure Subscription ID.</span></span> |
| <span data-ttu-id="7cb82-140">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="7cb82-140">timestamp</span></span> |<span data-ttu-id="7cb82-141">Czas, w którym hello zdarzeń został wygenerowany przez hello usługa Azure, która hello żądanie.</span><span class="sxs-lookup"><span data-stu-id="7cb82-141">Time at which hello event was generated by hello Azure service that processed hello request.</span></span> |
| <span data-ttu-id="7cb82-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="7cb82-142">resourceId</span></span> |<span data-ttu-id="7cb82-143">Identyfikator zasobu hello wpływ na zasobów.</span><span class="sxs-lookup"><span data-stu-id="7cb82-143">Resource ID of hello impacted resource.</span></span> |
| <span data-ttu-id="7cb82-144">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="7cb82-144">resourceGroupName</span></span> |<span data-ttu-id="7cb82-145">Nazwa grupy zasobów hello hello wpływ na zasób</span><span class="sxs-lookup"><span data-stu-id="7cb82-145">Name of hello resource group for hello impacted resource</span></span> |
| <span data-ttu-id="7cb82-146">properties</span><span class="sxs-lookup"><span data-stu-id="7cb82-146">properties</span></span> |<span data-ttu-id="7cb82-147">Zestaw `<Key, Value>` par (tj. `Dictionary<String, String>`) zawierającą szczegóły dotyczące zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7cb82-147">Set of `<Key, Value>` pairs (i.e. `Dictionary<String, String>`) that includes details about hello event.</span></span> |
| <span data-ttu-id="7cb82-148">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="7cb82-148">event</span></span> |<span data-ttu-id="7cb82-149">Element zawierający metadane dotyczące zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7cb82-149">Element containing metadata about hello event.</span></span> |
| <span data-ttu-id="7cb82-150">Autoryzacji</span><span class="sxs-lookup"><span data-stu-id="7cb82-150">authorization</span></span> |<span data-ttu-id="7cb82-151">właściwości RBAC Hello hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7cb82-151">hello RBAC properties of hello event.</span></span> <span data-ttu-id="7cb82-152">Obejmują one zazwyczaj hello "Akcja" i "rola" hello "zakresu."</span><span class="sxs-lookup"><span data-stu-id="7cb82-152">These usually include hello “action”, “role” and hello “scope.”</span></span> |
| <span data-ttu-id="7cb82-153">category</span><span class="sxs-lookup"><span data-stu-id="7cb82-153">category</span></span> |<span data-ttu-id="7cb82-154">Kategoria zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7cb82-154">Category of hello event.</span></span> <span data-ttu-id="7cb82-155">Obsługiwane wartości to: administracyjne, alertów zabezpieczeń, ServiceHealth, zalecenie.</span><span class="sxs-lookup"><span data-stu-id="7cb82-155">Supported values include: Administrative, Alert, Security, ServiceHealth, Recommendation.</span></span> |
| <span data-ttu-id="7cb82-156">obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="7cb82-156">caller</span></span> |<span data-ttu-id="7cb82-157">Adres e-mail użytkownika hello, który wykonał operację hello, oświadczenia UPN lub nazwy SPN oświadczenia na podstawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="7cb82-157">Email address of hello user who performed hello operation, UPN claim, or SPN claim based on availability.</span></span> <span data-ttu-id="7cb82-158">Może mieć wartości null dla niektórych wywołań systemowych.</span><span class="sxs-lookup"><span data-stu-id="7cb82-158">Can be null for certain system calls.</span></span> |
| <span data-ttu-id="7cb82-159">correlationId</span><span class="sxs-lookup"><span data-stu-id="7cb82-159">correlationId</span></span> |<span data-ttu-id="7cb82-160">Zazwyczaj identyfikator GUID w postaci ciągu.</span><span class="sxs-lookup"><span data-stu-id="7cb82-160">Usually a GUID in string format.</span></span> <span data-ttu-id="7cb82-161">Zdarzenia z correlationId należą toohello tę samą akcję większych i zwykle udostępnianie correlationId.</span><span class="sxs-lookup"><span data-stu-id="7cb82-161">Events with correlationId belong toohello same larger action and usually share a correlationId.</span></span> |
| <span data-ttu-id="7cb82-162">eventDescription</span><span class="sxs-lookup"><span data-stu-id="7cb82-162">eventDescription</span></span> |<span data-ttu-id="7cb82-163">Opis zdarzenia hello tekst statyczny.</span><span class="sxs-lookup"><span data-stu-id="7cb82-163">Static text description of hello event.</span></span> |
| <span data-ttu-id="7cb82-164">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7cb82-164">eventDataId</span></span> |<span data-ttu-id="7cb82-165">Unikatowy identyfikator dla hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7cb82-165">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="7cb82-166">Źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="7cb82-166">eventSource</span></span> |<span data-ttu-id="7cb82-167">Nazwa hello infrastruktury i usługa Azure hello wygenerowane zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="7cb82-167">Name of hello Azure service or infrastructure that generated hello event.</span></span> |
| <span data-ttu-id="7cb82-168">httpRequest</span><span class="sxs-lookup"><span data-stu-id="7cb82-168">httpRequest</span></span> |<span data-ttu-id="7cb82-169">Obejmuje zazwyczaj hello "clientRequestId", "clientIpAddress" i "method" (np. umieścić metoda HTTP).</span><span class="sxs-lookup"><span data-stu-id="7cb82-169">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method e.g. PUT).</span></span> |
| <span data-ttu-id="7cb82-170">poziom</span><span class="sxs-lookup"><span data-stu-id="7cb82-170">level</span></span> |<span data-ttu-id="7cb82-171">Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne."</span><span class="sxs-lookup"><span data-stu-id="7cb82-171">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose.”</span></span> |
| <span data-ttu-id="7cb82-172">operationId</span><span class="sxs-lookup"><span data-stu-id="7cb82-172">operationId</span></span> |<span data-ttu-id="7cb82-173">Zazwyczaj identyfikator GUID współdzielenia zdarzenia hello odpowiadającego toosingle operacji.</span><span class="sxs-lookup"><span data-stu-id="7cb82-173">Usually a GUID shared among hello events corresponding toosingle operation.</span></span> |
| <span data-ttu-id="7cb82-174">operationName</span><span class="sxs-lookup"><span data-stu-id="7cb82-174">operationName</span></span> |<span data-ttu-id="7cb82-175">Nazwa operacji hello.</span><span class="sxs-lookup"><span data-stu-id="7cb82-175">Name of hello operation.</span></span> |
| <span data-ttu-id="7cb82-176">properties</span><span class="sxs-lookup"><span data-stu-id="7cb82-176">properties</span></span> |<span data-ttu-id="7cb82-177">Właściwości zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7cb82-177">Properties of hello event.</span></span> |
| <span data-ttu-id="7cb82-178">status</span><span class="sxs-lookup"><span data-stu-id="7cb82-178">status</span></span> |<span data-ttu-id="7cb82-179">Ciąg.</span><span class="sxs-lookup"><span data-stu-id="7cb82-179">String.</span></span> <span data-ttu-id="7cb82-180">Stan operacji hello.</span><span class="sxs-lookup"><span data-stu-id="7cb82-180">Status of hello operation.</span></span> <span data-ttu-id="7cb82-181">Typowe wartości to: "Uruchomiona", "W toku", "Powiodło się", "Nie powiodło się", "Active", "Rozwiązany".</span><span class="sxs-lookup"><span data-stu-id="7cb82-181">Common values include: "Started", "In Progress", "Succeeded", "Failed", "Active", "Resolved".</span></span> |
| <span data-ttu-id="7cb82-182">Podstan</span><span class="sxs-lookup"><span data-stu-id="7cb82-182">subStatus</span></span> |<span data-ttu-id="7cb82-183">Zwykle zawiera kod stanu HTTP hello hello odpowiedniego wywołania REST.</span><span class="sxs-lookup"><span data-stu-id="7cb82-183">Usually includes hello HTTP status code of hello corresponding REST call.</span></span> <span data-ttu-id="7cb82-184">Może również zawierać inne parametry opisujące podstanu.</span><span class="sxs-lookup"><span data-stu-id="7cb82-184">It might also include other strings describing a substatus.</span></span> <span data-ttu-id="7cb82-185">Obejmują wartości typowych podstanu: OK (kod stanu HTTP: 200), utworzony (kod stanu HTTP: 201), akceptowane (kod stanu HTTP: 202), nie zawartości (kod stanu HTTP: 204), nieprawidłowe żądanie (kod stanu HTTP: 400), nie znaleziono (kod stanu HTTP: 404), konflikt (kod stanu HTTP: 409), wewnętrzny błąd serwera (kod stanu HTTP: 500), Usługa niedostępna (kod stanu HTTP: 503), limit czasu bramy (kod stanu HTTP: 504)</span><span class="sxs-lookup"><span data-stu-id="7cb82-185">Common substatus values include: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7cb82-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7cb82-186">Next steps</span></span>
* [<span data-ttu-id="7cb82-187">Dowiedz się więcej o hello dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="7cb82-187">Learn more about hello Activity Log</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="7cb82-188">Wykonywanie skryptów automatyzacji Azure (elementów Runbook) Azure alertów</span><span class="sxs-lookup"><span data-stu-id="7cb82-188">Execute Azure Automation scripts (Runbooks) on Azure alerts</span></span>](http://go.microsoft.com/fwlink/?LinkId=627081)
* <span data-ttu-id="7cb82-189">[Użyj aplikacji logiki toosend programu SMS za pośrednictwem usługi Twilio z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="7cb82-189">[Use Logic App toosend an SMS via Twilio from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app).</span></span> <span data-ttu-id="7cb82-190">W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="7cb82-190">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="7cb82-191">[Użyj aplikacji logiki toosend Slack wiadomości z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="7cb82-191">[Use Logic App toosend a Slack message from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app).</span></span> <span data-ttu-id="7cb82-192">W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="7cb82-192">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
* <span data-ttu-id="7cb82-193">[Użyj aplikacji logiki toosend tooan komunikatów kolejek platformy Azure z poziomu alertu Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span><span class="sxs-lookup"><span data-stu-id="7cb82-193">[Use Logic App toosend a message tooan Azure Queue from an Azure alert](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app).</span></span> <span data-ttu-id="7cb82-194">W tym przykładzie jest metryki alertów, ale może być zmodyfikowany toowork alert dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="7cb82-194">This example is for metric alerts, but could be modified toowork with an Activity Log alert.</span></span>
