---
title: "aaaAzure schemat zdarzenia dziennika aktywności | Dokumentacja firmy Microsoft"
description: "Zrozumienie schematu zdarzeń hello danych do hello dziennik aktywności"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a><span data-ttu-id="7f2e4-103">Schematu zdarzeń dziennika aktywności platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7f2e4-103">Azure Activity Log event schema</span></span>
<span data-ttu-id="7f2e4-104">Witaj **dziennika aktywności platformy Azure** jest dziennika, który zapewnia wgląd w wszelkie zdarzenia poziomu subskrypcji, które wystąpiły na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-104">hello **Azure Activity Log** is a log that provides insight into any subscription-level events that have occurred in Azure.</span></span> <span data-ttu-id="7f2e4-105">W tym artykule opisano schematu zdarzeń hello na kategorię danych.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-105">This article describes hello event schema per category of data.</span></span>

## <a name="administrative"></a><span data-ttu-id="7f2e4-106">Administracyjne</span><span class="sxs-lookup"><span data-stu-id="7f2e4-106">Administrative</span></span>
<span data-ttu-id="7f2e4-107">Ta kategoria zawiera rekord hello wszystkich utworzyć, update, delete i akcji operacje wykonywane za pomocą Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-107">This category contains hello record of all create, update, delete, and action operations performed through Resource Manager.</span></span> <span data-ttu-id="7f2e4-108">Przykłady powitalne typy zdarzeń, które można zobaczyć w tej kategorii "Utwórz maszynę wirtualną" i "usunąć grupy zabezpieczeń sieci" każdej akcji podjętej przez użytkownika lub aplikacji przy użyciu usługi Resource Manager ma formę operację określonego typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-108">Examples of hello types of events you would see in this category include "create virtual machine" and "delete network security group" Every action taken by a user or application using Resource Manager is modeled as an operation on a particular resource type.</span></span> <span data-ttu-id="7f2e4-109">Jeśli typ operacji hello jest zapisu, usuwania lub działania, rekordy hello hello start i powodzenie lub niepowodzenie tej operacji są rejestrowane w hello kategorii administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-109">If hello operation type is Write, Delete, or Action, hello records of both hello start and success or fail of that operation are recorded in hello Administrative category.</span></span> <span data-ttu-id="7f2e4-110">Kategoria administracyjna Hello także żadnych kontroli dostępu na podstawie toorole zmian w subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-110">hello Administrative category also includes any changes toorole-based access control in a subscription.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7f2e4-111">Zdarzenie próbkowania</span><span class="sxs-lookup"><span data-stu-id="7f2e4-111">Sample event</span></span>
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="7f2e4-112">Opisy właściwości</span><span class="sxs-lookup"><span data-stu-id="7f2e4-112">Property descriptions</span></span>
| <span data-ttu-id="7f2e4-113">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="7f2e4-113">Element Name</span></span> | <span data-ttu-id="7f2e4-114">Opis</span><span class="sxs-lookup"><span data-stu-id="7f2e4-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f2e4-115">Autoryzacji</span><span class="sxs-lookup"><span data-stu-id="7f2e4-115">authorization</span></span> |<span data-ttu-id="7f2e4-116">Obiekt typu blob właściwości RBAC hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-116">Blob of RBAC properties of hello event.</span></span> <span data-ttu-id="7f2e4-117">Obejmuje zazwyczaj hello właściwości "Akcja", "rola" i "zakresu".</span><span class="sxs-lookup"><span data-stu-id="7f2e4-117">Usually includes hello “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="7f2e4-118">obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="7f2e4-118">caller</span></span> |<span data-ttu-id="7f2e4-119">Adres e-mail użytkownika hello, który wykonał operację hello, oświadczenia UPN lub nazwy SPN oświadczenia na podstawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-119">Email address of hello user who has performed hello operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="7f2e4-120">Kanały</span><span class="sxs-lookup"><span data-stu-id="7f2e4-120">channels</span></span> |<span data-ttu-id="7f2e4-121">Jeden z hello następujące wartości: "Administrator", "Operacji"</span><span class="sxs-lookup"><span data-stu-id="7f2e4-121">One of hello following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="7f2e4-122">Oświadczenia</span><span class="sxs-lookup"><span data-stu-id="7f2e4-122">claims</span></span> |<span data-ttu-id="7f2e4-123">Hello JWT token używane przez usługi Active Directory tooauthenticate hello użytkownik lub aplikacja tooperform tej operacji w Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-123">hello JWT token used by Active Directory tooauthenticate hello user or application tooperform this operation in resource manager.</span></span> |
| <span data-ttu-id="7f2e4-124">correlationId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-124">correlationId</span></span> |<span data-ttu-id="7f2e4-125">Zazwyczaj identyfikator GUID w formacie ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-125">Usually a GUID in hello string format.</span></span> <span data-ttu-id="7f2e4-126">Zdarzenia, które mają correlationId należą toohello tę samą akcję pełny.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-126">Events that share a correlationId belong toohello same uber action.</span></span> |
| <span data-ttu-id="7f2e4-127">description</span><span class="sxs-lookup"><span data-stu-id="7f2e4-127">description</span></span> |<span data-ttu-id="7f2e4-128">Statyczny tekst opisu zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-128">Static text description of an event.</span></span> |
| <span data-ttu-id="7f2e4-129">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-129">eventDataId</span></span> |<span data-ttu-id="7f2e4-130">Unikatowy identyfikator zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-130">Unique identifier of an event.</span></span> |
| <span data-ttu-id="7f2e4-131">httpRequest</span><span class="sxs-lookup"><span data-stu-id="7f2e4-131">httpRequest</span></span> |<span data-ttu-id="7f2e4-132">Obiekt blob opisujący hello żądania Http.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-132">Blob describing hello Http Request.</span></span> <span data-ttu-id="7f2e4-133">Obejmuje zazwyczaj hello "clientRequestId", "clientIpAddress" i "method" (metoda HTTP.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-133">Usually includes hello “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="7f2e4-134">For example, PUT).</span><span class="sxs-lookup"><span data-stu-id="7f2e4-134">For example, PUT).</span></span> |
| <span data-ttu-id="7f2e4-135">poziom</span><span class="sxs-lookup"><span data-stu-id="7f2e4-135">level</span></span> |<span data-ttu-id="7f2e4-136">Poziom hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-136">Level of hello event.</span></span> <span data-ttu-id="7f2e4-137">Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne"</span><span class="sxs-lookup"><span data-stu-id="7f2e4-137">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="7f2e4-138">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="7f2e4-138">resourceGroupName</span></span> |<span data-ttu-id="7f2e4-139">Nazwa grupy zasobów hello hello wpływ na zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-139">Name of hello resource group for hello impacted resource.</span></span> |
| <span data-ttu-id="7f2e4-140">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-140">resourceProviderName</span></span> |<span data-ttu-id="7f2e4-141">Nazwa dostawcy zasobów hello hello wpływ na zasób</span><span class="sxs-lookup"><span data-stu-id="7f2e4-141">Name of hello resource provider for hello impacted resource</span></span> |
| <span data-ttu-id="7f2e4-142">resourceId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-142">resourceId</span></span> |<span data-ttu-id="7f2e4-143">Identyfikator zasobu hello wpływ na zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-143">Resource id of hello impacted resource.</span></span> |
| <span data-ttu-id="7f2e4-144">operationId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-144">operationId</span></span> |<span data-ttu-id="7f2e4-145">Identyfikator GUID współdzielenia hello zdarzenia, które odpowiadają tooa jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-145">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="7f2e4-146">operationName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-146">operationName</span></span> |<span data-ttu-id="7f2e4-147">Nazwa operacji hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-147">Name of hello operation.</span></span> |
| <span data-ttu-id="7f2e4-148">properties</span><span class="sxs-lookup"><span data-stu-id="7f2e4-148">properties</span></span> |<span data-ttu-id="7f2e4-149">Zestaw `<Key, Value>` pary (słowniku) opisujący szczegóły hello hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-149">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="7f2e4-150">status</span><span class="sxs-lookup"><span data-stu-id="7f2e4-150">status</span></span> |<span data-ttu-id="7f2e4-151">Ciąg opisujący stan hello hello operacji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-151">String describing hello status of hello operation.</span></span> <span data-ttu-id="7f2e4-152">Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-152">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="7f2e4-153">Podstan</span><span class="sxs-lookup"><span data-stu-id="7f2e4-153">subStatus</span></span> |<span data-ttu-id="7f2e4-154">Zazwyczaj hello kod stanu HTTP hello odpowiadającego wywołania REST, ale można również uwzględnić inne parametry opisujące podstanu, takich jak te wartości typowych: OK (kod stanu HTTP: 200), utworzony (kod stanu HTTP: 201), akceptowane (kod stanu HTTP: 202), nie zawartości (HTTP Kod stanu: 204), nieprawidłowe żądanie (kod stanu HTTP: 400), nie znaleziono (kod stanu HTTP: 404), konflikt (kod stanu HTTP: 409), wewnętrzny błąd serwera (kod stanu HTTP: 500), Usługa niedostępna (kod stanu HTTP: 503), limit czasu bramy (kod stanu HTTP: 504).</span><span class="sxs-lookup"><span data-stu-id="7f2e4-154">Usually hello HTTP status code of hello corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="7f2e4-155">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7f2e4-155">eventTimestamp</span></span> |<span data-ttu-id="7f2e4-156">Znacznik czasu w momencie hello zdarzeń został wygenerowany przez hello przetwarzania usługi Azure hello żądanie odpowiednie zdarzenie hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-156">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="7f2e4-157">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7f2e4-157">submissionTimestamp</span></span> |<span data-ttu-id="7f2e4-158">Znacznik czasu w momencie zdarzenia hello stały się dostępne na potrzeby zapytań.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-158">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="7f2e4-159">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-159">subscriptionId</span></span> |<span data-ttu-id="7f2e4-160">Identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-160">Azure Subscription Id.</span></span> |

## <a name="service-health"></a><span data-ttu-id="7f2e4-161">Kondycja usługi</span><span class="sxs-lookup"><span data-stu-id="7f2e4-161">Service health</span></span>
<span data-ttu-id="7f2e4-162">Ta kategoria zawiera rekord hello określone zdarzenia kondycji usługi, które wystąpiły na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-162">This category contains hello record of any service health incidents that have occurred in Azure.</span></span> <span data-ttu-id="7f2e4-163">Przykład Witaj typu zdarzenia, które można zobaczyć w tej kategorii jest "Azure SQL w wschodnie stany USA występuje Przestój."</span><span class="sxs-lookup"><span data-stu-id="7f2e4-163">An example of hello type of event you would see in this category is "SQL Azure in East US is experiencing downtime."</span></span> <span data-ttu-id="7f2e4-164">Zdarzenia kondycji usługi są dostępne w pięciu odmian: wymagana akcja, wspierana odzyskiwania, zdarzenie, konserwacji, informacje lub zabezpieczeń i są wyświetlane tylko, jeśli zasób hello subskrypcji, która może wpływać na powitania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-164">Service health events come in five varieties: Action Required, Assisted Recovery, Incident, Maintenance, Information, or Security, and only appear if you have a resource in hello subscription that would be impacted by hello event.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7f2e4-165">Zdarzenie próbkowania</span><span class="sxs-lookup"><span data-stu-id="7f2e4-165">Sample event</span></span>
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a><span data-ttu-id="7f2e4-166">Opisy właściwości</span><span class="sxs-lookup"><span data-stu-id="7f2e4-166">Property descriptions</span></span>
<span data-ttu-id="7f2e4-167">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="7f2e4-167">Element Name</span></span> | <span data-ttu-id="7f2e4-168">Opis</span><span class="sxs-lookup"><span data-stu-id="7f2e4-168">Description</span></span>
-------- | -----------
<span data-ttu-id="7f2e4-169">Kanały</span><span class="sxs-lookup"><span data-stu-id="7f2e4-169">channels</span></span> | <span data-ttu-id="7f2e4-170">Jest jednym z hello następujące wartości: "Administrator", "Operacji"</span><span class="sxs-lookup"><span data-stu-id="7f2e4-170">Is one of hello following values: “Admin”, “Operation”</span></span>
<span data-ttu-id="7f2e4-171">correlationId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-171">correlationId</span></span> | <span data-ttu-id="7f2e4-172">Jest zazwyczaj identyfikator GUID w formacie ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-172">Is usually a GUID in hello string format.</span></span> <span data-ttu-id="7f2e4-173">Zdarzenia z tym należy toohello zwykle udostępnić tę samą akcję pełny hello correlationId tego samego.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-173">Events with that belong toohello same uber action usually share hello same correlationId.</span></span>
<span data-ttu-id="7f2e4-174">description</span><span class="sxs-lookup"><span data-stu-id="7f2e4-174">description</span></span> | <span data-ttu-id="7f2e4-175">Opis zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-175">Description of hello event.</span></span>
<span data-ttu-id="7f2e4-176">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-176">eventDataId</span></span> | <span data-ttu-id="7f2e4-177">Witaj Unikatowy identyfikator zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-177">hello unique identifier of an event.</span></span>
<span data-ttu-id="7f2e4-178">EventName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-178">eventName</span></span> | <span data-ttu-id="7f2e4-179">Tytuł Hello hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-179">hello title of hello event.</span></span>
<span data-ttu-id="7f2e4-180">poziom</span><span class="sxs-lookup"><span data-stu-id="7f2e4-180">level</span></span> | <span data-ttu-id="7f2e4-181">Poziom hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-181">Level of hello event.</span></span> <span data-ttu-id="7f2e4-182">Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne"</span><span class="sxs-lookup"><span data-stu-id="7f2e4-182">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span>
<span data-ttu-id="7f2e4-183">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-183">resourceProviderName</span></span> | <span data-ttu-id="7f2e4-184">Nazwa dostawcy zasobów hello hello wpływ na zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-184">Name of hello resource provider for hello impacted resource.</span></span> <span data-ttu-id="7f2e4-185">Jeśli nie jest znany, będzie to wartość null.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-185">If not known, this will be null.</span></span>
<span data-ttu-id="7f2e4-186">Typ zasobu</span><span class="sxs-lookup"><span data-stu-id="7f2e4-186">resourceType</span></span>| <span data-ttu-id="7f2e4-187">Typ zasobu hello Hello wpływ na zasobów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-187">hello type of resource of hello impacted resource.</span></span> <span data-ttu-id="7f2e4-188">Jeśli nie jest znany, będzie to wartość null.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-188">If not known, this will be null.</span></span>
<span data-ttu-id="7f2e4-189">Podstan</span><span class="sxs-lookup"><span data-stu-id="7f2e4-189">subStatus</span></span> | <span data-ttu-id="7f2e4-190">Zazwyczaj o wartości null dla zdarzenia kondycji usługi.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-190">Usually null for Service Health events.</span></span>
<span data-ttu-id="7f2e4-191">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7f2e4-191">eventTimestamp</span></span> | <span data-ttu-id="7f2e4-192">Znacznik czasu w momencie hello dziennik zdarzeń został wygenerowany i przesłać toohello dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-192">Timestamp when hello log event was generated and submitted toohello Activity Log.</span></span>
<span data-ttu-id="7f2e4-193">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7f2e4-193">submissionTimestamp</span></span> |   <span data-ttu-id="7f2e4-194">Znacznik czasu w momencie zdarzenia hello stały się dostępne w hello dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-194">Timestamp when hello event became available in hello Activity Log.</span></span>
<span data-ttu-id="7f2e4-195">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-195">subscriptionId</span></span> | <span data-ttu-id="7f2e4-196">Witaj w trakcie którego zarejestrowano to zdarzenie subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-196">hello Azure subscription in which this event was logged.</span></span>
<span data-ttu-id="7f2e4-197">status</span><span class="sxs-lookup"><span data-stu-id="7f2e4-197">status</span></span> | <span data-ttu-id="7f2e4-198">Ciąg opisujący stan hello hello operacji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-198">String describing hello status of hello operation.</span></span> <span data-ttu-id="7f2e4-199">Niektóre typowe wartości to: aktywne, rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-199">Some common values are: Active, Resolved.</span></span>
<span data-ttu-id="7f2e4-200">operationName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-200">operationName</span></span> | <span data-ttu-id="7f2e4-201">Nazwa operacji hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-201">Name of hello operation.</span></span> <span data-ttu-id="7f2e4-202">Zazwyczaj Microsoft.ServiceHealth/incident/action.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-202">Usually Microsoft.ServiceHealth/incident/action.</span></span>
<span data-ttu-id="7f2e4-203">category</span><span class="sxs-lookup"><span data-stu-id="7f2e4-203">category</span></span> | <span data-ttu-id="7f2e4-204">"ServiceHealth"</span><span class="sxs-lookup"><span data-stu-id="7f2e4-204">"ServiceHealth"</span></span>
<span data-ttu-id="7f2e4-205">resourceId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-205">resourceId</span></span> | <span data-ttu-id="7f2e4-206">Identyfikator zasobu hello wpływ na zasobu, jeśli znane.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-206">Resource id of hello impacted resource, if known.</span></span> <span data-ttu-id="7f2e4-207">W przeciwnym razie podany identyfikator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-207">Subscription ID is provided otherwise.</span></span>
<span data-ttu-id="7f2e4-208">Properties.Title</span><span class="sxs-lookup"><span data-stu-id="7f2e4-208">Properties.title</span></span> | <span data-ttu-id="7f2e4-209">Tytuł Hello zlokalizowane dla tej komunikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-209">hello localized title for this communication.</span></span> <span data-ttu-id="7f2e4-210">Język domyślny hello jest angielski.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-210">English is hello default language.</span></span>
<span data-ttu-id="7f2e4-211">Properties.Communication</span><span class="sxs-lookup"><span data-stu-id="7f2e4-211">Properties.communication</span></span> | <span data-ttu-id="7f2e4-212">Szczegóły Hello zlokalizowane hello komunikacji z kodu znaczników HTML.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-212">hello localized details of hello communication with HTML markup.</span></span> <span data-ttu-id="7f2e4-213">Domyślne hello jest angielski.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-213">English is hello default.</span></span>
<span data-ttu-id="7f2e4-214">Properties.incidentType</span><span class="sxs-lookup"><span data-stu-id="7f2e4-214">Properties.incidentType</span></span> | <span data-ttu-id="7f2e4-215">Możliwe wartości: AssistedRecovery, ActionRequired, informacje, zdarzenie, obsługi, zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="7f2e4-215">Possible values: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security</span></span>
<span data-ttu-id="7f2e4-216">Properties.trackingId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-216">Properties.trackingId</span></span> | <span data-ttu-id="7f2e4-217">Identyfikuje hello incydent, który jest skojarzony to zdarzenie.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-217">Identifies hello incident this event is associated with.</span></span> <span data-ttu-id="7f2e4-218">Użyj tego zdarzenia pokrewne tooan toocorrelate hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-218">Use this toocorrelate hello events related tooan incident.</span></span>
<span data-ttu-id="7f2e4-219">Properties.impactedServices</span><span class="sxs-lookup"><span data-stu-id="7f2e4-219">Properties.impactedServices</span></span> | <span data-ttu-id="7f2e4-220">Zmienionym obiektu blob JSON opisującą hello usług i regionów, które mają wpływ zdarzenia hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-220">An escaped JSON blob which describes hello services and regions that are impacted by hello incident.</span></span> <span data-ttu-id="7f2e4-221">Lista usług, z których każda ma elementy ServiceName i listę ImpactedRegions, z których każda ma RegionName.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-221">A list of Services, each of which has a ServiceName and a list of ImpactedRegions, each of which has a RegionName.</span></span>
<span data-ttu-id="7f2e4-222">Properties.defaultLanguageTitle</span><span class="sxs-lookup"><span data-stu-id="7f2e4-222">Properties.defaultLanguageTitle</span></span> | <span data-ttu-id="7f2e4-223">Komunikacja Hello w języku angielskim</span><span class="sxs-lookup"><span data-stu-id="7f2e4-223">hello communication in English</span></span>
<span data-ttu-id="7f2e4-224">Properties.defaultLanguageContent</span><span class="sxs-lookup"><span data-stu-id="7f2e4-224">Properties.defaultLanguageContent</span></span> | <span data-ttu-id="7f2e4-225">Komunikacja Hello w języku angielskim jako kod znaczników html i zwykły tekst</span><span class="sxs-lookup"><span data-stu-id="7f2e4-225">hello communication in English as either html markup or plain text</span></span>
<span data-ttu-id="7f2e4-226">Properties.Stage</span><span class="sxs-lookup"><span data-stu-id="7f2e4-226">Properties.stage</span></span> | <span data-ttu-id="7f2e4-227">Możliwe wartości AssistedRecovery, ActionRequired, informacje, zdarzenie, zabezpieczeń: są aktywne, rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-227">Possible values for AssistedRecovery, ActionRequired, Information, Incident, Security: are Active, Resolved.</span></span> <span data-ttu-id="7f2e4-228">W konserwacji są: aktywny, planowane, w toku, anulowane, Rescheduled, rozwiązane, Zakończ</span><span class="sxs-lookup"><span data-stu-id="7f2e4-228">For Maintenance they are: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete</span></span>
<span data-ttu-id="7f2e4-229">Properties.communicationId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-229">Properties.communicationId</span></span> | <span data-ttu-id="7f2e4-230">Komunikacja Hello to zdarzenie jest skojarzony.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-230">hello communication this event is associated.</span></span>

## <a name="alert"></a><span data-ttu-id="7f2e4-231">Alerty</span><span class="sxs-lookup"><span data-stu-id="7f2e4-231">Alert</span></span>
<span data-ttu-id="7f2e4-232">Ta kategoria zawiera rekord hello aktywacji wszystkich alertów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-232">This category contains hello record of all activations of Azure alerts.</span></span> <span data-ttu-id="7f2e4-233">Przykład Witaj typu zdarzenia, które można zobaczyć w tej kategorii jest "procent użycia procesora CPU na myVM została ponad 80 dla hello ostatnich 5 minut."</span><span class="sxs-lookup"><span data-stu-id="7f2e4-233">An example of hello type of event you would see in this category is "CPU % on myVM has been over 80 for hello past 5 minutes."</span></span> <span data-ttu-id="7f2e4-234">Z różnymi systemami Azure ma alertów koncepcji — można zdefiniować regułę jakiegoś i otrzymasz powiadomienie, gdy warunki reguły są zgodne.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-234">A variety of Azure systems have an alerting concept -- you can define a rule of some sort and receive a notification when conditions match that rule.</span></span> <span data-ttu-id="7f2e4-235">Zawsze Azure obsługiwanego typu alertu "aktywuje," lub hello są warunki niespełnienia toogenerate powiadomienie, rekord aktywacji hello również spoczywa toothis kategorii hello dziennik aktywności.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-235">Each time a supported Azure alert type 'activates,' or hello conditions are met toogenerate a notification, a record of hello activation is also pushed toothis category of hello Activity Log.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7f2e4-236">Zdarzenie próbkowania</span><span class="sxs-lookup"><span data-stu-id="7f2e4-236">Sample event</span></span>

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a><span data-ttu-id="7f2e4-237">Opisy właściwości</span><span class="sxs-lookup"><span data-stu-id="7f2e4-237">Property descriptions</span></span>
| <span data-ttu-id="7f2e4-238">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="7f2e4-238">Element Name</span></span> | <span data-ttu-id="7f2e4-239">Opis</span><span class="sxs-lookup"><span data-stu-id="7f2e4-239">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f2e4-240">obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="7f2e4-240">caller</span></span> | <span data-ttu-id="7f2e4-241">Zawsze Microsoft.Insights/alertRules</span><span class="sxs-lookup"><span data-stu-id="7f2e4-241">Always Microsoft.Insights/alertRules</span></span> |
| <span data-ttu-id="7f2e4-242">Kanały</span><span class="sxs-lookup"><span data-stu-id="7f2e4-242">channels</span></span> | <span data-ttu-id="7f2e4-243">Zawsze "Admin, operację"</span><span class="sxs-lookup"><span data-stu-id="7f2e4-243">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="7f2e4-244">Oświadczenia</span><span class="sxs-lookup"><span data-stu-id="7f2e4-244">claims</span></span> | <span data-ttu-id="7f2e4-245">Obiektu blob JSON hello głównej nazwy usługi (nazwy głównej usługi) lub zasób typu hello aparat alertów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-245">JSON blob with hello SPN (service principal name), or resource type, of hello alert engine.</span></span> |
| <span data-ttu-id="7f2e4-246">correlationId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-246">correlationId</span></span> | <span data-ttu-id="7f2e4-247">Identyfikator GUID w formacie ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-247">A GUID in hello string format.</span></span> |
| <span data-ttu-id="7f2e4-248">description</span><span class="sxs-lookup"><span data-stu-id="7f2e4-248">description</span></span> |<span data-ttu-id="7f2e4-249">Opis tekst statyczny hello zdarzenia alertu.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-249">Static text description of hello alert event.</span></span> |
| <span data-ttu-id="7f2e4-250">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-250">eventDataId</span></span> |<span data-ttu-id="7f2e4-251">Unikatowy identyfikator hello zdarzeń alertów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-251">Unique identifier of hello alert event.</span></span> |
| <span data-ttu-id="7f2e4-252">poziom</span><span class="sxs-lookup"><span data-stu-id="7f2e4-252">level</span></span> |<span data-ttu-id="7f2e4-253">Poziom hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-253">Level of hello event.</span></span> <span data-ttu-id="7f2e4-254">Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne"</span><span class="sxs-lookup"><span data-stu-id="7f2e4-254">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="7f2e4-255">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="7f2e4-255">resourceGroupName</span></span> |<span data-ttu-id="7f2e4-256">Nazwę grupy zasobów hello hello wpływ na zasobu, jeśli jest to alert metryki.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-256">Name of hello resource group for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="7f2e4-257">Inne typy alertów to hello nazwę grupy zasobów hello, która zawiera hello samego alertu.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-257">For other alert types, this is hello name of hello resource group that contains hello alert itself.</span></span> |
| <span data-ttu-id="7f2e4-258">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-258">resourceProviderName</span></span> |<span data-ttu-id="7f2e4-259">Nazwa dostawcy zasobów hello hello wpływ na zasobu, jeśli jest to alert metryki.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-259">Name of hello resource provider for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="7f2e4-260">Inne typy alertów to hello nazwę dostawcy zasobów hello hello samego alertu.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-260">For other alert types, this is hello name of hello resource provider for hello alert itself.</span></span> |
| <span data-ttu-id="7f2e4-261">resourceId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-261">resourceId</span></span> | <span data-ttu-id="7f2e4-262">Nazwę identyfikatora zasobu hello hello wpływ na zasobu, jeśli jest to alert metryki.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-262">Name of hello resource ID for hello impacted resource if it is a metric alert.</span></span> <span data-ttu-id="7f2e4-263">Inne typy alertów jest to identyfikator zasobu hello hello zasobu alertu sam.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-263">For other alert types, this is hello resource ID of hello alert resource itself.</span></span> |
| <span data-ttu-id="7f2e4-264">operationId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-264">operationId</span></span> |<span data-ttu-id="7f2e4-265">Identyfikator GUID współdzielenia hello zdarzenia, które odpowiadają tooa jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-265">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="7f2e4-266">operationName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-266">operationName</span></span> |<span data-ttu-id="7f2e4-267">Nazwa operacji hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-267">Name of hello operation.</span></span> |
| <span data-ttu-id="7f2e4-268">properties</span><span class="sxs-lookup"><span data-stu-id="7f2e4-268">properties</span></span> |<span data-ttu-id="7f2e4-269">Zestaw `<Key, Value>` pary (słowniku) opisujący szczegóły hello hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-269">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="7f2e4-270">status</span><span class="sxs-lookup"><span data-stu-id="7f2e4-270">status</span></span> |<span data-ttu-id="7f2e4-271">Ciąg opisujący stan hello hello operacji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-271">String describing hello status of hello operation.</span></span> <span data-ttu-id="7f2e4-272">Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-272">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="7f2e4-273">Podstan</span><span class="sxs-lookup"><span data-stu-id="7f2e4-273">subStatus</span></span> | <span data-ttu-id="7f2e4-274">Zazwyczaj o wartości null dla alertów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-274">Usually null for alerts.</span></span> |
| <span data-ttu-id="7f2e4-275">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7f2e4-275">eventTimestamp</span></span> |<span data-ttu-id="7f2e4-276">Znacznik czasu w momencie hello zdarzeń został wygenerowany przez hello przetwarzania usługi Azure hello żądanie odpowiednie zdarzenie hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-276">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="7f2e4-277">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7f2e4-277">submissionTimestamp</span></span> |<span data-ttu-id="7f2e4-278">Znacznik czasu w momencie zdarzenia hello stały się dostępne na potrzeby zapytań.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-278">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="7f2e4-279">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-279">subscriptionId</span></span> |<span data-ttu-id="7f2e4-280">Identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-280">Azure Subscription Id.</span></span> |

### <a name="properties-field-per-alert-type"></a><span data-ttu-id="7f2e4-281">Pole właściwości typu alertu</span><span class="sxs-lookup"><span data-stu-id="7f2e4-281">Properties field per alert type</span></span>
<span data-ttu-id="7f2e4-282">pole właściwości Hello będzie zawierać różne wartości w zależności od źródła hello hello zdarzenia alertu.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-282">hello properties field will contain different values depending on hello source of hello alert event.</span></span> <span data-ttu-id="7f2e4-283">Dwóch dostawców typowych zdarzeń alertów są alerty dziennika aktywności i metryki alerty.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-283">Two common alert event providers are Activity Log alerts and metric alerts.</span></span>

#### <a name="properties-for-activity-log-alerts"></a><span data-ttu-id="7f2e4-284">Właściwości alertów dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="7f2e4-284">Properties for Activity Log alerts</span></span>
| <span data-ttu-id="7f2e4-285">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="7f2e4-285">Element Name</span></span> | <span data-ttu-id="7f2e4-286">Opis</span><span class="sxs-lookup"><span data-stu-id="7f2e4-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f2e4-287">properties.subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-287">properties.subscriptionId</span></span> | <span data-ttu-id="7f2e4-288">Identyfikator subskrypcji Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-288">hello subscription ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7f2e4-289">properties.eventDataId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-289">properties.eventDataId</span></span> | <span data-ttu-id="7f2e4-290">Identyfikator danych zdarzenia Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-290">hello event data ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7f2e4-291">properties.resourceGroup</span><span class="sxs-lookup"><span data-stu-id="7f2e4-291">properties.resourceGroup</span></span> | <span data-ttu-id="7f2e4-292">Grupa zasobów Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-292">hello resource group from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7f2e4-293">properties.resourceId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-293">properties.resourceId</span></span> | <span data-ttu-id="7f2e4-294">Identyfikator zasobu Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-294">hello resource ID from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7f2e4-295">properties.eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7f2e4-295">properties.eventTimestamp</span></span> | <span data-ttu-id="7f2e4-296">Witaj zdarzeń sygnatura czasowa hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-296">hello event timestamp of hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7f2e4-297">properties.operationName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-297">properties.operationName</span></span> | <span data-ttu-id="7f2e4-298">Nazwa operacji Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-298">hello operation name from hello activity log event which caused this activity log alert rule toobe activated.</span></span> |
| <span data-ttu-id="7f2e4-299">Properties.status</span><span class="sxs-lookup"><span data-stu-id="7f2e4-299">properties.status</span></span> | <span data-ttu-id="7f2e4-300">Stan Hello z hello działania dziennika zdarzeń, który spowodował tego działania toobe reguły alertu dziennika aktywowany.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-300">hello status from hello activity log event which caused this activity log alert rule toobe activated.</span></span>|

#### <a name="properties-for-metric-alerts"></a><span data-ttu-id="7f2e4-301">Właściwości alertów metryki</span><span class="sxs-lookup"><span data-stu-id="7f2e4-301">Properties for metric alerts</span></span>
| <span data-ttu-id="7f2e4-302">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="7f2e4-302">Element Name</span></span> | <span data-ttu-id="7f2e4-303">Opis</span><span class="sxs-lookup"><span data-stu-id="7f2e4-303">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f2e4-304">właściwości. RuleUri</span><span class="sxs-lookup"><span data-stu-id="7f2e4-304">properties.RuleUri</span></span> | <span data-ttu-id="7f2e4-305">Identyfikator zasobu hello metryki reguły alertu samej siebie.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-305">Resource ID of hello metric alert rule itself.</span></span> |
| <span data-ttu-id="7f2e4-306">właściwości. RuleName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-306">properties.RuleName</span></span> | <span data-ttu-id="7f2e4-307">Nazwa Hello hello metryki reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-307">hello name of hello metric alert rule.</span></span> |
| <span data-ttu-id="7f2e4-308">właściwości. RuleDescription</span><span class="sxs-lookup"><span data-stu-id="7f2e4-308">properties.RuleDescription</span></span> | <span data-ttu-id="7f2e4-309">Opis Hello hello metryki reguły alertu (zgodnie z definicją w regule alertu hello).</span><span class="sxs-lookup"><span data-stu-id="7f2e4-309">hello description of hello metric alert rule (as defined in hello alert rule).</span></span> |
| <span data-ttu-id="7f2e4-310">właściwości. Próg</span><span class="sxs-lookup"><span data-stu-id="7f2e4-310">properties.Threshold</span></span> | <span data-ttu-id="7f2e4-311">wartość progowa Hello przy ocenie hello hello metryki reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-311">hello threshold value used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7f2e4-312">właściwości. WindowSizeInMinutes</span><span class="sxs-lookup"><span data-stu-id="7f2e4-312">properties.WindowSizeInMinutes</span></span> | <span data-ttu-id="7f2e4-313">rozmiar okna Hello przy ocenie hello hello metryki reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-313">hello window size used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7f2e4-314">właściwości. Agregacji</span><span class="sxs-lookup"><span data-stu-id="7f2e4-314">properties.Aggregation</span></span> | <span data-ttu-id="7f2e4-315">Typ agregacji Hello zdefiniowane w regule alertu metryki hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-315">hello aggregation type defined in hello metric alert rule.</span></span> |
| <span data-ttu-id="7f2e4-316">właściwości. Operator</span><span class="sxs-lookup"><span data-stu-id="7f2e4-316">properties.Operator</span></span> | <span data-ttu-id="7f2e4-317">operator warunkowy Hello przy ocenie hello hello metryki reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-317">hello conditional operator used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7f2e4-318">właściwości. MetricName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-318">properties.MetricName</span></span> | <span data-ttu-id="7f2e4-319">Nazwa metryki Hello metryki hello przy ocenie hello hello metryki reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-319">hello metric name of hello metric used in hello evaluation of hello metric alert rule.</span></span> |
| <span data-ttu-id="7f2e4-320">właściwości. MetricUnit</span><span class="sxs-lookup"><span data-stu-id="7f2e4-320">properties.MetricUnit</span></span> | <span data-ttu-id="7f2e4-321">Jednostka metryki Hello metryki hello przy ocenie hello hello metryki reguły alertów.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-321">hello metric unit for hello metric used in hello evaluation of hello metric alert rule.</span></span> |

## <a name="autoscale"></a><span data-ttu-id="7f2e4-322">Automatyczne skalowanie</span><span class="sxs-lookup"><span data-stu-id="7f2e4-322">Autoscale</span></span>
<span data-ttu-id="7f2e4-323">Ta kategoria zawiera rekord hello żadnych operacji toohello powiązane zdarzenia aparatu skalowania automatycznego hello oparte na ustawienia skalowania automatycznego zdefiniowanych w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-323">This category contains hello record of any events related toohello operation of hello autoscale engine based on any autoscale settings you have defined in your subscription.</span></span> <span data-ttu-id="7f2e4-324">Przykład Witaj typu zdarzenia, które można zobaczyć w tej kategorii jest "Skalowania automatycznego skalowania w górę akcja nie powiodła się".</span><span class="sxs-lookup"><span data-stu-id="7f2e4-324">An example of hello type of event you would see in this category is "Autoscale scale up action failed."</span></span> <span data-ttu-id="7f2e4-325">Przy użyciu automatycznego skalowania, można automatycznie skalować w poziomie lub skalować w hello liczbę wystąpień w typie zasobów obsługiwanych na podstawie czasu dnia i/lub obciążenia () dane przy użyciu ustawienia skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-325">Using autoscale, you can automatically scale out or scale in hello number of instances in a supported resource type based on time of day and/or load (metric) data using an autoscale setting.</span></span> <span data-ttu-id="7f2e4-326">Po spełnieniu warunków hello tooscale w górę i w dół hello start i zakończyło się pomyślnie lub niepowodzeniem zdarzenia będą rejestrowane w tej kategorii.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-326">When hello conditions are met tooscale up or down, hello start and succeeded or failed events will be recorded in this category.</span></span>

### <a name="sample-event"></a><span data-ttu-id="7f2e4-327">Zdarzenie próbkowania</span><span class="sxs-lookup"><span data-stu-id="7f2e4-327">Sample event</span></span>
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a><span data-ttu-id="7f2e4-328">Opisy właściwości</span><span class="sxs-lookup"><span data-stu-id="7f2e4-328">Property descriptions</span></span>
| <span data-ttu-id="7f2e4-329">Nazwa elementu</span><span class="sxs-lookup"><span data-stu-id="7f2e4-329">Element Name</span></span> | <span data-ttu-id="7f2e4-330">Opis</span><span class="sxs-lookup"><span data-stu-id="7f2e4-330">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f2e4-331">obiekt wywołujący</span><span class="sxs-lookup"><span data-stu-id="7f2e4-331">caller</span></span> | <span data-ttu-id="7f2e4-332">Zawsze Microsoft.Insights/autoscaleSettings</span><span class="sxs-lookup"><span data-stu-id="7f2e4-332">Always Microsoft.Insights/autoscaleSettings</span></span> |
| <span data-ttu-id="7f2e4-333">Kanały</span><span class="sxs-lookup"><span data-stu-id="7f2e4-333">channels</span></span> | <span data-ttu-id="7f2e4-334">Zawsze "Admin, operację"</span><span class="sxs-lookup"><span data-stu-id="7f2e4-334">Always “Admin, Operation”</span></span> |
| <span data-ttu-id="7f2e4-335">Oświadczenia</span><span class="sxs-lookup"><span data-stu-id="7f2e4-335">claims</span></span> | <span data-ttu-id="7f2e4-336">Obiektu blob JSON z hello głównej nazwy usługi (nazwy głównej usługi) lub zasobu typu, hello skalowania automatycznego aparatu.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-336">JSON blob with hello SPN (service principal name), or resource type, of hello autoscale engine.</span></span> |
| <span data-ttu-id="7f2e4-337">correlationId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-337">correlationId</span></span> | <span data-ttu-id="7f2e4-338">Identyfikator GUID w formacie ciągu hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-338">A GUID in hello string format.</span></span> |
| <span data-ttu-id="7f2e4-339">description</span><span class="sxs-lookup"><span data-stu-id="7f2e4-339">description</span></span> |<span data-ttu-id="7f2e4-340">Opis tekst statyczny hello skalowania automatycznego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-340">Static text description of hello autoscale event.</span></span> |
| <span data-ttu-id="7f2e4-341">eventDataId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-341">eventDataId</span></span> |<span data-ttu-id="7f2e4-342">Unikatowy identyfikator zdarzenia skalowania automatycznego hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-342">Unique identifier of hello autoscale event.</span></span> |
| <span data-ttu-id="7f2e4-343">poziom</span><span class="sxs-lookup"><span data-stu-id="7f2e4-343">level</span></span> |<span data-ttu-id="7f2e4-344">Poziom hello zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-344">Level of hello event.</span></span> <span data-ttu-id="7f2e4-345">Jeden z hello następujące wartości: "Krytyczne", "Błąd", "Ostrzeżenie", "Informacyjny" i "Pełne"</span><span class="sxs-lookup"><span data-stu-id="7f2e4-345">One of hello following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="7f2e4-346">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="7f2e4-346">resourceGroupName</span></span> |<span data-ttu-id="7f2e4-347">Nazwa grupy zasobów hello hello ustawieniu skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-347">Name of hello resource group for hello autoscale setting.</span></span> |
| <span data-ttu-id="7f2e4-348">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-348">resourceProviderName</span></span> |<span data-ttu-id="7f2e4-349">Nazwa dostawcy zasobów hello hello ustawieniu skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-349">Name of hello resource provider for hello autoscale setting.</span></span> |
| <span data-ttu-id="7f2e4-350">resourceId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-350">resourceId</span></span> |<span data-ttu-id="7f2e4-351">Identyfikator zasobu hello ustawieniu skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-351">Resource id of hello autoscale setting.</span></span> |
| <span data-ttu-id="7f2e4-352">operationId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-352">operationId</span></span> |<span data-ttu-id="7f2e4-353">Identyfikator GUID współdzielenia hello zdarzenia, które odpowiadają tooa jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-353">A GUID shared among hello events that correspond tooa single operation.</span></span> |
| <span data-ttu-id="7f2e4-354">operationName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-354">operationName</span></span> |<span data-ttu-id="7f2e4-355">Nazwa operacji hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-355">Name of hello operation.</span></span> |
| <span data-ttu-id="7f2e4-356">properties</span><span class="sxs-lookup"><span data-stu-id="7f2e4-356">properties</span></span> |<span data-ttu-id="7f2e4-357">Zestaw `<Key, Value>` pary (słowniku) opisujący szczegóły hello hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-357">Set of `<Key, Value>` pairs (that is, a Dictionary) describing hello details of hello event.</span></span> |
| <span data-ttu-id="7f2e4-358">właściwości. Opis elementu</span><span class="sxs-lookup"><span data-stu-id="7f2e4-358">properties.Description</span></span> | <span data-ttu-id="7f2e4-359">Szczegółowy opis wykonywanych jakie hello skalowania automatycznego aparatu.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-359">Detailed description of what hello autoscale engine was doing.</span></span> |
| <span data-ttu-id="7f2e4-360">właściwości. ResourceName</span><span class="sxs-lookup"><span data-stu-id="7f2e4-360">properties.ResourceName</span></span> | <span data-ttu-id="7f2e4-361">Identyfikator zasobu hello wpływ na zasobów (hello zasobu, na które hello wykonywania akcji skalowania)</span><span class="sxs-lookup"><span data-stu-id="7f2e4-361">Resource ID of hello impacted resource (hello resource on which hello scale action was being performed)</span></span> |
| <span data-ttu-id="7f2e4-362">właściwości. OldInstancesCount</span><span class="sxs-lookup"><span data-stu-id="7f2e4-362">properties.OldInstancesCount</span></span> | <span data-ttu-id="7f2e4-363">Hello liczbę wystąpień przed akcji skalowania automatycznego hello weszły w życie.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-363">hello number of instances before hello autoscale action took effect.</span></span> |
| <span data-ttu-id="7f2e4-364">właściwości. NewInstancesCount</span><span class="sxs-lookup"><span data-stu-id="7f2e4-364">properties.NewInstancesCount</span></span> | <span data-ttu-id="7f2e4-365">Witaj liczba wystąpień po akcji skalowania automatycznego hello weszły w życie.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-365">hello number of instances after hello autoscale action took effect.</span></span> |
| <span data-ttu-id="7f2e4-366">właściwości. LastScaleActionTime</span><span class="sxs-lookup"><span data-stu-id="7f2e4-366">properties.LastScaleActionTime</span></span> | <span data-ttu-id="7f2e4-367">Witaj sygnatura czasowa wystąpienia hello akcji skalowania automatycznego.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-367">hello timestamp of when hello autoscale action occurred.</span></span> |
| <span data-ttu-id="7f2e4-368">status</span><span class="sxs-lookup"><span data-stu-id="7f2e4-368">status</span></span> |<span data-ttu-id="7f2e4-369">Ciąg opisujący stan hello hello operacji.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-369">String describing hello status of hello operation.</span></span> <span data-ttu-id="7f2e4-370">Niektóre typowe wartości to: pracy w toku, zakończyło się pomyślnie, nie powiodło się, aktywne, rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-370">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="7f2e4-371">Podstan</span><span class="sxs-lookup"><span data-stu-id="7f2e4-371">subStatus</span></span> | <span data-ttu-id="7f2e4-372">Zazwyczaj o wartości null dla automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-372">Usually null for autoscale.</span></span> |
| <span data-ttu-id="7f2e4-373">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="7f2e4-373">eventTimestamp</span></span> |<span data-ttu-id="7f2e4-374">Znacznik czasu w momencie hello zdarzeń został wygenerowany przez hello przetwarzania usługi Azure hello żądanie odpowiednie zdarzenie hello.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-374">Timestamp when hello event was generated by hello Azure service processing hello request corresponding hello event.</span></span> |
| <span data-ttu-id="7f2e4-375">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="7f2e4-375">submissionTimestamp</span></span> |<span data-ttu-id="7f2e4-376">Znacznik czasu w momencie zdarzenia hello stały się dostępne na potrzeby zapytań.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-376">Timestamp when hello event became available for querying.</span></span> |
| <span data-ttu-id="7f2e4-377">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="7f2e4-377">subscriptionId</span></span> |<span data-ttu-id="7f2e4-378">Identyfikator subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7f2e4-378">Azure Subscription Id.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7f2e4-379">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f2e4-379">Next steps</span></span>
* [<span data-ttu-id="7f2e4-380">Dowiedz się więcej o hello dziennik aktywności (dawniej dzienników inspekcji)</span><span class="sxs-lookup"><span data-stu-id="7f2e4-380">Learn more about hello Activity Log (formerly Audit Logs)</span></span>](monitoring-overview-activity-logs.md)
* [<span data-ttu-id="7f2e4-381">Strumienia tooEvent dziennika aktywności platformy Azure hello koncentratory</span><span class="sxs-lookup"><span data-stu-id="7f2e4-381">Stream hello Azure Activity Log tooEvent Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
