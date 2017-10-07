---
title: "schematu zdarzeń aaaAzure siatki zdarzeń"
description: "Opisuje właściwości hello, które są dostępne dla zdarzeń o Azure zdarzeń siatki."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="b8311-103">Schematu zdarzeń siatki zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b8311-103">Event Grid event schema</span></span>

<span data-ttu-id="b8311-104">Ten artykuł zawiera właściwości hello i schematu dla zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b8311-104">This article provides hello properties and schema for events.</span></span> <span data-ttu-id="b8311-105">Zdarzenia składają się z zestaw pięciu właściwości wymaganych parametrów i wymaganą **danych** obiektu.</span><span class="sxs-lookup"><span data-stu-id="b8311-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="b8311-106">właściwości Hello są typowe zdarzenia tooall z dowolnego wydawcę.</span><span class="sxs-lookup"><span data-stu-id="b8311-106">hello properties are common tooall events from any publisher.</span></span> <span data-ttu-id="b8311-107">Witaj **danych** obiekt zawiera właściwości, które są określone tooeach wydawcy.</span><span class="sxs-lookup"><span data-stu-id="b8311-107">hello **data** object contains properties that are specific tooeach publisher.</span></span> <span data-ttu-id="b8311-108">Tematy systemu te właściwości są toohello określonego dostawcy zasobów, takiego jak magazyn lub Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="b8311-108">For system topics, these properties are specific toohello resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="b8311-109">Zdarzenia są wysyłane tooAzure siatki zdarzeń w tablicy, która może zawierać wiele obiektów zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b8311-109">Events are sent tooAzure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="b8311-110">W przypadku pojedynczego zdarzenia hello tablicy ma długość 1.</span><span class="sxs-lookup"><span data-stu-id="b8311-110">If there is only a single event, hello array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="b8311-111">Właściwości zdarzenia</span><span class="sxs-lookup"><span data-stu-id="b8311-111">Event properties</span></span>

<span data-ttu-id="b8311-112">Wszystkie zdarzenia będzie zawierać hello tego samego następujących danych najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="b8311-112">All events will contain hello same following top level data.</span></span>

| <span data-ttu-id="b8311-113">Właściwość</span><span class="sxs-lookup"><span data-stu-id="b8311-113">Property</span></span> | <span data-ttu-id="b8311-114">Typ</span><span class="sxs-lookup"><span data-stu-id="b8311-114">Type</span></span> | <span data-ttu-id="b8311-115">Opis</span><span class="sxs-lookup"><span data-stu-id="b8311-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="b8311-116">Temat</span><span class="sxs-lookup"><span data-stu-id="b8311-116">topic</span></span> | <span data-ttu-id="b8311-117">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b8311-117">string</span></span> | <span data-ttu-id="b8311-118">Źródło zdarzenia toohello ścieżka pełna zasobów.</span><span class="sxs-lookup"><span data-stu-id="b8311-118">Full resource path toohello event source.</span></span> <span data-ttu-id="b8311-119">To pole nie jest zapisywalny.</span><span class="sxs-lookup"><span data-stu-id="b8311-119">This field is not writeable.</span></span> |
| <span data-ttu-id="b8311-120">Temat</span><span class="sxs-lookup"><span data-stu-id="b8311-120">subject</span></span> | <span data-ttu-id="b8311-121">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b8311-121">string</span></span> | <span data-ttu-id="b8311-122">Temat zdarzeń toohello ścieżki zdefiniowane wydawcy.</span><span class="sxs-lookup"><span data-stu-id="b8311-122">Publisher defined path toohello event subject.</span></span> |
| <span data-ttu-id="b8311-123">Typ zdarzenia</span><span class="sxs-lookup"><span data-stu-id="b8311-123">eventType</span></span> | <span data-ttu-id="b8311-124">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b8311-124">string</span></span> | <span data-ttu-id="b8311-125">Jedna z hello zarejestrowana typów zdarzeń dla tego źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="b8311-125">One of hello registered event types for this event source.</span></span> |
| <span data-ttu-id="b8311-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="b8311-126">eventTime</span></span> | <span data-ttu-id="b8311-127">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b8311-127">string</span></span> | <span data-ttu-id="b8311-128">Zdarzenie hello czasu Hello jest generowany na podstawie czasu UTC hello dostawcy.</span><span class="sxs-lookup"><span data-stu-id="b8311-128">hello time hello event is generated based on hello provider's UTC time.</span></span> |
| <span data-ttu-id="b8311-129">id</span><span class="sxs-lookup"><span data-stu-id="b8311-129">id</span></span> | <span data-ttu-id="b8311-130">Ciąg</span><span class="sxs-lookup"><span data-stu-id="b8311-130">string</span></span> | <span data-ttu-id="b8311-131">Unikatowy identyfikator dla hello zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="b8311-131">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="b8311-132">Dane</span><span class="sxs-lookup"><span data-stu-id="b8311-132">data</span></span> | <span data-ttu-id="b8311-133">Obiekt</span><span class="sxs-lookup"><span data-stu-id="b8311-133">object</span></span> | <span data-ttu-id="b8311-134">Dostawca zasobów toohello określonych danych zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="b8311-134">Event data specific toohello resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="b8311-135">Źródła zdarzeń dostępne</span><span class="sxs-lookup"><span data-stu-id="b8311-135">Available event sources</span></span>

<span data-ttu-id="b8311-136">następujące źródła zdarzeń Hello publikowanie zdarzeń zużycia za pośrednictwem siatki zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="b8311-136">hello following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="b8311-137">Grupy zasobów (operacje zarządzania)</span><span class="sxs-lookup"><span data-stu-id="b8311-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="b8311-138">Subskrypcje platformy Azure (operacje zarządzania)</span><span class="sxs-lookup"><span data-stu-id="b8311-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="b8311-139">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b8311-139">Event Hubs</span></span>
* <span data-ttu-id="b8311-140">Niestandardowe — tematy</span><span class="sxs-lookup"><span data-stu-id="b8311-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="b8311-141">Subskrypcje platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b8311-141">Azure Subscriptions</span></span>

<span data-ttu-id="b8311-142">Subskrypcje platformy Azure można teraz Emituj zdarzeń zarządzania z usługi Azure Resource Manager, np. po utworzeniu maszyny Wirtualnej lub konto magazynu zostało usunięte.</span><span class="sxs-lookup"><span data-stu-id="b8311-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="b8311-143">Typy dostępnych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b8311-143">Available event types</span></span>

- <span data-ttu-id="b8311-144">**Microsoft.Resources.ResourceWriteSuccess**: wywoływane, gdy zasób utworzyć ani zaktualizować operacji zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b8311-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="b8311-145">**Microsoft.Resources.ResourceWriteFailure**: wywoływane, gdy tworzenie zasobu lub operacja aktualizacji nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="b8311-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="b8311-146">**Microsoft.Resources.ResourceWriteCancel**: wywoływane, gdy zasób utworzyć ani zaktualizować operacji zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="b8311-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="b8311-147">**Microsoft.Resources.ResourceDeleteSuccess**: wywoływane, gdy operacja usunięcia zasobu zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b8311-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="b8311-148">**Microsoft.Resources.ResourceDeleteFailure**: wywoływane, gdy operacja usuwania zasobu nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="b8311-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="b8311-149">**Microsoft.Resources.ResourceDeleteCancel**: "zgłaszane w przypadku usunięcia zasobu zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="b8311-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="b8311-150">Dzieje się tak podczas wdrażania szablonu zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="b8311-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="b8311-151">Przykład schematu zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b8311-151">Example event schema</span></span>

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



## <a name="resource-groups"></a><span data-ttu-id="b8311-152">Grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="b8311-152">Resource Groups</span></span>

<span data-ttu-id="b8311-153">Grupy zasobów można teraz Emituj zdarzeń zarządzania z usługi Azure Resource Manager, np. po utworzeniu maszyny Wirtualnej lub konto magazynu zostało usunięte.</span><span class="sxs-lookup"><span data-stu-id="b8311-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="b8311-154">Typy dostępnych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b8311-154">Available event types</span></span>

- <span data-ttu-id="b8311-155">**Microsoft.Resources.ResourceWriteSuccess**: wywoływane, gdy zasób utworzyć ani zaktualizować operacji zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b8311-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="b8311-156">**Microsoft.Resources.ResourceWriteFailure**: wywoływane, gdy tworzenie zasobu lub operacja aktualizacji nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="b8311-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="b8311-157">**Microsoft.Resources.ResourceWriteCancel**: wywoływane, gdy zasób utworzyć ani zaktualizować operacji zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="b8311-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="b8311-158">**Microsoft.Resources.ResourceDeleteSuccess**: wywoływane, gdy operacja usunięcia zasobu zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="b8311-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="b8311-159">**Microsoft.Resources.ResourceDeleteFailure**: wywoływane, gdy operacja usuwania zasobu nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="b8311-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="b8311-160">**Microsoft.Resources.ResourceDeleteCancel**: "zgłaszane w przypadku usunięcia zasobu zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="b8311-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="b8311-161">Dzieje się tak podczas wdrażania szablonu zostało anulowane.</span><span class="sxs-lookup"><span data-stu-id="b8311-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="b8311-162">Przykład zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b8311-162">Example event</span></span>

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



## <a name="event-hubs"></a><span data-ttu-id="b8311-163">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b8311-163">Event Hubs</span></span>

<span data-ttu-id="b8311-164">Zdarzenia centra zdarzeń są obecnie tylko wysyłanego, gdy plik jest automatycznie przesyłany toostorage za pomocą funkcji przechwytywania hello.</span><span class="sxs-lookup"><span data-stu-id="b8311-164">Event Hubs events are currently only emitted when a file is automatically sent toostorage using hello Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="b8311-165">Typy dostępnych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b8311-165">Available event types</span></span>

- <span data-ttu-id="b8311-166">**Microsoft.EventHub.CaptureFileCreated**: wywoływane po utworzeniu pliku przechwytywania.</span><span class="sxs-lookup"><span data-stu-id="b8311-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="b8311-167">Przykład zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b8311-167">Example event</span></span>

<span data-ttu-id="b8311-168">To zdarzenie próbkowania zawiera schemat hello usługi Event Hubs zdarzenia wywoływane, gdy przechwytywanie przechowuje plik.</span><span class="sxs-lookup"><span data-stu-id="b8311-168">This sample event shows hello schema of an Event Hubs event raised when Capture stores a file.</span></span> 

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



## <a name="azure-blob-storage"></a><span data-ttu-id="b8311-169">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="b8311-169">Azure Blob Storage</span></span>

<span data-ttu-id="b8311-170">Azure Blob Storage w prywatnej wersji zapoznawczej z przystąpić do integracji z siatki zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="b8311-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="b8311-171">Typy dostępnych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b8311-171">Available event types</span></span>

- <span data-ttu-id="b8311-172">**Microsoft.Storage.BlobCreated**: wywoływane po utworzeniu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="b8311-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="b8311-173">**Microsoft.Storage.BlobDeleted**: wywoływane po usunięciu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="b8311-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="b8311-174">Przykład zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b8311-174">Example event</span></span>

<span data-ttu-id="b8311-175">To zdarzenie próbkowania pokazuje hello schematu magazynu zdarzenia wywoływane po utworzeniu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="b8311-175">This sample event shows hello schema of a storage event raised when a blob is created.</span></span> 

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




## <a name="custom-topics"></a><span data-ttu-id="b8311-176">Niestandardowe — tematy</span><span class="sxs-lookup"><span data-stu-id="b8311-176">Custom Topics</span></span>

<span data-ttu-id="b8311-177">ładunek danych Hello zdarzenia niestandardowe jest zdefiniowane przez użytkownika i może być dowolnym dobrze sformatowany JSON.</span><span class="sxs-lookup"><span data-stu-id="b8311-177">hello data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="b8311-178">danych najwyższego poziomu Hello powinien zawierać hello same pola jako zasób standardowa definicja zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="b8311-178">hello top level data should contain hello same fields as standard resource defined events.</span></span> <span data-ttu-id="b8311-179">Podczas publikowania zdarzenia toocustom tematy należy rozważyć modelowania hello przedmiotem tooaid Twojego zdarzenia do routingu i filtrowania.</span><span class="sxs-lookup"><span data-stu-id="b8311-179">When publishing events toocustom topics you should consider modeling hello subject of your events tooaid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="b8311-180">Przykład zdarzeń</span><span class="sxs-lookup"><span data-stu-id="b8311-180">Example event</span></span>

<span data-ttu-id="b8311-181">Witaj poniższy przykład przedstawia zdarzenie dla niestandardowego tematu:</span><span class="sxs-lookup"><span data-stu-id="b8311-181">hello following example shows an event for a custom topic:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="b8311-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8311-182">Next steps</span></span>

* <span data-ttu-id="b8311-183">Aby tooEvent wprowadzenie siatki, zobacz [co to jest zdarzenie siatki?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="b8311-183">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="b8311-184">Zobacz toolearn o tworzeniu subskrypcji zdarzeń siatki [schematu subskrypcji zdarzeń siatki](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="b8311-184">toolearn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
