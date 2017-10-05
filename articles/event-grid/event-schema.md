---
title: "Azure schematu zdarzeń siatki zdarzeń"
description: "Opisuje właściwości, które są dostępne dla zdarzeń o Azure zdarzeń siatki."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 9e3c7b31ef23b29827d7184dc033227685ed92f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="4ad35-103">Schematu zdarzeń siatki zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4ad35-103">Event Grid event schema</span></span>

<span data-ttu-id="4ad35-104">Ten artykuł zawiera właściwości i schematu dla zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="4ad35-104">This article provides the properties and schema for events.</span></span> <span data-ttu-id="4ad35-105">Zdarzenia składają się z zestaw pięciu właściwości wymaganych parametrów i wymaganą **danych** obiektu.</span><span class="sxs-lookup"><span data-stu-id="4ad35-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="4ad35-106">Właściwości są wspólne dla wszystkich zdarzeń z dowolnego wydawcę.</span><span class="sxs-lookup"><span data-stu-id="4ad35-106">The properties are common to all events from any publisher.</span></span> <span data-ttu-id="4ad35-107">**Danych** obiektu zawiera właściwości, które są specyficzne dla każdego wydawcy.</span><span class="sxs-lookup"><span data-stu-id="4ad35-107">The **data** object contains properties that are specific to each publisher.</span></span> <span data-ttu-id="4ad35-108">Tematy systemu te właściwości są specyficzne dla dostawcy zasobu, takiego jak magazyn lub Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4ad35-108">For system topics, these properties are specific to the resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="4ad35-109">Zdarzenia są wysyłane do usługi Azure Event siatki w tablicy, która może zawierać wiele obiektów zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="4ad35-109">Events are sent to Azure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="4ad35-110">W przypadku pojedynczego zdarzenia tablicy ma długość 1.</span><span class="sxs-lookup"><span data-stu-id="4ad35-110">If there is only a single event, the array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="4ad35-111">Właściwości zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4ad35-111">Event properties</span></span>

<span data-ttu-id="4ad35-112">Wszystkie zdarzenia będzie zawierać tej samej następujących danych najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="4ad35-112">All events will contain the same following top level data.</span></span>

| <span data-ttu-id="4ad35-113">Właściwość</span><span class="sxs-lookup"><span data-stu-id="4ad35-113">Property</span></span> | <span data-ttu-id="4ad35-114">Typ</span><span class="sxs-lookup"><span data-stu-id="4ad35-114">Type</span></span> | <span data-ttu-id="4ad35-115">Opis</span><span class="sxs-lookup"><span data-stu-id="4ad35-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="4ad35-116">Temat</span><span class="sxs-lookup"><span data-stu-id="4ad35-116">topic</span></span> | <span data-ttu-id="4ad35-117">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4ad35-117">string</span></span> | <span data-ttu-id="4ad35-118">Zasobów Pełna ścieżka do źródła zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="4ad35-118">Full resource path to the event source.</span></span> <span data-ttu-id="4ad35-119">To pole nie jest zapisywalny.</span><span class="sxs-lookup"><span data-stu-id="4ad35-119">This field is not writeable.</span></span> |
| <span data-ttu-id="4ad35-120">Temat</span><span class="sxs-lookup"><span data-stu-id="4ad35-120">subject</span></span> | <span data-ttu-id="4ad35-121">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4ad35-121">string</span></span> | <span data-ttu-id="4ad35-122">Wydawca zdefiniowane ścieżki do podmiotu zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="4ad35-122">Publisher defined path to the event subject.</span></span> |
| <span data-ttu-id="4ad35-123">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="4ad35-123">eventType</span></span> | <span data-ttu-id="4ad35-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4ad35-124">string</span></span> | <span data-ttu-id="4ad35-125">Jeden z typów zdarzeń zarejestrowane dla tego źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4ad35-125">One of the registered event types for this event source.</span></span> |
| <span data-ttu-id="4ad35-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="4ad35-126">eventTime</span></span> | <span data-ttu-id="4ad35-127">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4ad35-127">string</span></span> | <span data-ttu-id="4ad35-128">Czas jest generowane zdarzenie oparte na czas UTC dostawcy.</span><span class="sxs-lookup"><span data-stu-id="4ad35-128">The time the event is generated based on the provider's UTC time.</span></span> |
| <span data-ttu-id="4ad35-129">id</span><span class="sxs-lookup"><span data-stu-id="4ad35-129">id</span></span> | <span data-ttu-id="4ad35-130">Ciąg</span><span class="sxs-lookup"><span data-stu-id="4ad35-130">string</span></span> | <span data-ttu-id="4ad35-131">Unikatowy identyfikator zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4ad35-131">Unique identifier for the event.</span></span> |
| <span data-ttu-id="4ad35-132">Dane</span><span class="sxs-lookup"><span data-stu-id="4ad35-132">data</span></span> | <span data-ttu-id="4ad35-133">Obiekt</span><span class="sxs-lookup"><span data-stu-id="4ad35-133">object</span></span> | <span data-ttu-id="4ad35-134">Dane zdarzenia specyficzne dla dostawcy zasobów.</span><span class="sxs-lookup"><span data-stu-id="4ad35-134">Event data specific to the resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="4ad35-135">Źródła zdarzeń dostępne</span><span class="sxs-lookup"><span data-stu-id="4ad35-135">Available event sources</span></span>

<span data-ttu-id="4ad35-136">Następujące źródła zdarzeń publikowanie zdarzeń zużycia za pośrednictwem siatki zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="4ad35-136">The following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="4ad35-137">Grupy zasobów (operacje zarządzania)</span><span class="sxs-lookup"><span data-stu-id="4ad35-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="4ad35-138">Subskrypcje platformy Azure (operacje zarządzania)</span><span class="sxs-lookup"><span data-stu-id="4ad35-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="4ad35-139">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4ad35-139">Event Hubs</span></span>
* <span data-ttu-id="4ad35-140">Niestandardowe — tematy</span><span class="sxs-lookup"><span data-stu-id="4ad35-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="4ad35-141">Subskrypcje platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4ad35-141">Azure Subscriptions</span></span>

<span data-ttu-id="4ad35-142">Subskrypcje platformy Azure można teraz Emituj zdarzeń zarządzania z usługi Azure Resource Manager, np. po utworzeniu maszyny Wirtualnej lub konto magazynu zostało usunięte.</span><span class="sxs-lookup"><span data-stu-id="4ad35-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="4ad35-143">Typy dostępnych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4ad35-143">Available event types</span></span>

- <span data-ttu-id="4ad35-144">**Microsoft.Resources.ResourceWriteSuccess**: wywoływane, gdy zasób utworzyć ani zaktualizować operacji zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4ad35-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="4ad35-145">**Microsoft.Resources.ResourceWriteFailure**: wywoływane, gdy tworzenie zasobu lub operacja aktualizacji nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="4ad35-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="4ad35-146">**Microsoft.Resources.ResourceWriteCancel**: wywoływane, gdy zasób utworzyć ani zaktualizować operacji zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="4ad35-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="4ad35-147">**Microsoft.Resources.ResourceDeleteSuccess**: wywoływane, gdy operacja usunięcia zasobu zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4ad35-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="4ad35-148">**Microsoft.Resources.ResourceDeleteFailure**: wywoływane, gdy operacja usuwania zasobu nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="4ad35-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="4ad35-149">**Microsoft.Resources.ResourceDeleteCancel**: "zgłaszane w przypadku usunięcia zasobu zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="4ad35-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="4ad35-150">Dzieje się tak podczas wdrażania szablonu zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="4ad35-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="4ad35-151">Przykład schematu zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4ad35-151">Example event schema</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a><span data-ttu-id="4ad35-152">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="4ad35-152">Resource Groups</span></span>

<span data-ttu-id="4ad35-153">Grupy zasobów można teraz Emituj zdarzeń zarządzania z usługi Azure Resource Manager, np. po utworzeniu maszyny Wirtualnej lub konto magazynu zostało usunięte.</span><span class="sxs-lookup"><span data-stu-id="4ad35-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="4ad35-154">Typy dostępnych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4ad35-154">Available event types</span></span>

- <span data-ttu-id="4ad35-155">**Microsoft.Resources.ResourceWriteSuccess**: wywoływane, gdy zasób utworzyć ani zaktualizować operacji zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4ad35-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="4ad35-156">**Microsoft.Resources.ResourceWriteFailure**: wywoływane, gdy tworzenie zasobu lub operacja aktualizacji nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="4ad35-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="4ad35-157">**Microsoft.Resources.ResourceWriteCancel**: wywoływane, gdy zasób utworzyć ani zaktualizować operacji zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="4ad35-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="4ad35-158">**Microsoft.Resources.ResourceDeleteSuccess**: wywoływane, gdy operacja usunięcia zasobu zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="4ad35-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="4ad35-159">**Microsoft.Resources.ResourceDeleteFailure**: wywoływane, gdy operacja usuwania zasobu nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="4ad35-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="4ad35-160">**Microsoft.Resources.ResourceDeleteCancel**: "zgłaszane w przypadku usunięcia zasobu zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="4ad35-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="4ad35-161">Dzieje się tak podczas wdrażania szablonu zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="4ad35-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="4ad35-162">Przykład zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4ad35-162">Example event</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a><span data-ttu-id="4ad35-163">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="4ad35-163">Event Hubs</span></span>

<span data-ttu-id="4ad35-164">Zdarzenia centra zdarzeń są obecnie tylko wysyłanego, gdy plik jest automatycznie przesyłany do magazynu przy użyciu funkcji przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="4ad35-164">Event Hubs events are currently only emitted when a file is automatically sent to storage using the Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="4ad35-165">Typy dostępnych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4ad35-165">Available event types</span></span>

- <span data-ttu-id="4ad35-166">**Microsoft.EventHub.CaptureFileCreated**: wywoływane po utworzeniu pliku przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="4ad35-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="4ad35-167">Przykład zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4ad35-167">Example event</span></span>

<span data-ttu-id="4ad35-168">To zdarzenie próbkowania zawiera schemat usługi Event Hubs zdarzenia wywoływane, gdy przechwytywanie przechowuje plik.</span><span class="sxs-lookup"><span data-stu-id="4ad35-168">This sample event shows the schema of an Event Hubs event raised when Capture stores a file.</span></span> 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a><span data-ttu-id="4ad35-169">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="4ad35-169">Azure Blob Storage</span></span>

<span data-ttu-id="4ad35-170">Azure Blob Storage w prywatnej wersji zapoznawczej z przystąpić do integracji z siatki zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="4ad35-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="4ad35-171">Typy dostępnych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4ad35-171">Available event types</span></span>

- <span data-ttu-id="4ad35-172">**Microsoft.Storage.BlobCreated**: wywoływane po utworzeniu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ad35-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="4ad35-173">**Microsoft.Storage.BlobDeleted**: wywoływane po usunięciu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ad35-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="4ad35-174">Przykład zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4ad35-174">Example event</span></span>

<span data-ttu-id="4ad35-175">To zdarzenie próbkowania zawiera schemat magazynu zdarzenia wywoływane po utworzeniu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="4ad35-175">This sample event shows the schema of a storage event raised when a blob is created.</span></span> 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a><span data-ttu-id="4ad35-176">Niestandardowe — tematy</span><span class="sxs-lookup"><span data-stu-id="4ad35-176">Custom Topics</span></span>

<span data-ttu-id="4ad35-177">Ładunek danych zdarzenia niestandardowe jest zdefiniowane przez użytkownika i może być dowolnym dobrze sformatowany JSON.</span><span class="sxs-lookup"><span data-stu-id="4ad35-177">The data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="4ad35-178">Danych najwyższego poziomu powinien zawierać te same pola jako zasób standardowa definicja zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="4ad35-178">The top level data should contain the same fields as standard resource defined events.</span></span> <span data-ttu-id="4ad35-179">Podczas publikowania zdarzeń w niestandardowych tematów należy rozważyć modelowania przedmiotem zdarzeń ułatwiających routingu i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="4ad35-179">When publishing events to custom topics you should consider modeling the subject of your events to aid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="4ad35-180">Przykład zdarzeń</span><span class="sxs-lookup"><span data-stu-id="4ad35-180">Example event</span></span>

<span data-ttu-id="4ad35-181">W poniższym przykładzie przedstawiono zdarzenie dla niestandardowego tematu:</span><span class="sxs-lookup"><span data-stu-id="4ad35-181">The following example shows an event for a custom topic:</span></span>
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a><span data-ttu-id="4ad35-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4ad35-182">Next steps</span></span>

* <span data-ttu-id="4ad35-183">Aby obejrzeć wprowadzenie do siatki zdarzeń, zobacz [co to jest zdarzenie siatki?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="4ad35-183">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="4ad35-184">Aby dowiedzieć się więcej o tworzeniu subskrypcji zdarzeń siatki, zobacz [schematu subskrypcji zdarzeń siatki](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="4ad35-184">To learn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
