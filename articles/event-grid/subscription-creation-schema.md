---
title: "Schemat subskrypcji zdarzeń siatki aaaAzure"
description: "Opisuje właściwości hello subskrybowanie zdarzeń tooan Azure zdarzeń siatki."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="59402-103">Schematu subskrypcji siatki zdarzeń</span><span class="sxs-lookup"><span data-stu-id="59402-103">Event Grid subscription schema</span></span>

<span data-ttu-id="59402-104">toocreate subskrypcji zdarzeń siatki, możesz wysłać toohello żądania operacji subskrypcji tworzenia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="59402-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="59402-105">Witaj Użyj następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="59402-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="59402-106">Na przykład toocreate subskrypcji zdarzeń dla konta magazynu o nazwie `examplestorage` w grupie zasobów o nazwie `examplegroup`, użyj hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="59402-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="59402-107">Hello artykule hello właściwości i schematu dla treści hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="59402-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="59402-108">Właściwości subskrypcji zdarzeń</span><span class="sxs-lookup"><span data-stu-id="59402-108">Event subscription properties</span></span>

| <span data-ttu-id="59402-109">Właściwość</span><span class="sxs-lookup"><span data-stu-id="59402-109">Property</span></span> | <span data-ttu-id="59402-110">Typ</span><span class="sxs-lookup"><span data-stu-id="59402-110">Type</span></span> | <span data-ttu-id="59402-111">Opis</span><span class="sxs-lookup"><span data-stu-id="59402-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="59402-112">Miejsce docelowe</span><span class="sxs-lookup"><span data-stu-id="59402-112">destination</span></span> | <span data-ttu-id="59402-113">Obiekt</span><span class="sxs-lookup"><span data-stu-id="59402-113">object</span></span> | <span data-ttu-id="59402-114">Witaj obiektu, który definiuje hello punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="59402-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="59402-115">Filtr</span><span class="sxs-lookup"><span data-stu-id="59402-115">filter</span></span> | <span data-ttu-id="59402-116">Obiekt</span><span class="sxs-lookup"><span data-stu-id="59402-116">object</span></span> | <span data-ttu-id="59402-117">Pole opcjonalne filtrowania hello typów zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="59402-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="59402-118">obiekt docelowy</span><span class="sxs-lookup"><span data-stu-id="59402-118">destination object</span></span>

| <span data-ttu-id="59402-119">Właściwość</span><span class="sxs-lookup"><span data-stu-id="59402-119">Property</span></span> | <span data-ttu-id="59402-120">Typ</span><span class="sxs-lookup"><span data-stu-id="59402-120">Type</span></span> | <span data-ttu-id="59402-121">Opis</span><span class="sxs-lookup"><span data-stu-id="59402-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="59402-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="59402-122">endpointType</span></span> | <span data-ttu-id="59402-123">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59402-123">string</span></span> | <span data-ttu-id="59402-124">Witaj typ punktu końcowego dla subskrypcji hello (webhook/HTTP Centrum zdarzeń i kolejki).</span><span class="sxs-lookup"><span data-stu-id="59402-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="59402-125">adres URL punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="59402-125">endpointUrl</span></span> | <span data-ttu-id="59402-126">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59402-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="59402-127">obiekt filtru</span><span class="sxs-lookup"><span data-stu-id="59402-127">filter object</span></span>

| <span data-ttu-id="59402-128">Właściwość</span><span class="sxs-lookup"><span data-stu-id="59402-128">Property</span></span> | <span data-ttu-id="59402-129">Typ</span><span class="sxs-lookup"><span data-stu-id="59402-129">Type</span></span> | <span data-ttu-id="59402-130">Opis</span><span class="sxs-lookup"><span data-stu-id="59402-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="59402-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="59402-131">includedEventTypes</span></span> | <span data-ttu-id="59402-132">Tablica</span><span class="sxs-lookup"><span data-stu-id="59402-132">array</span></span> | <span data-ttu-id="59402-133">Dopasowania, gdy typ zdarzenia hello w komunikacie zdarzenia hello jest tooone dokładnego dopasowania tych nazw typów zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="59402-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="59402-134">Zgłasza błąd, jeśli nazwa zdarzenia nie są zgodne z nazwy typów zdarzeń hello zarejestrowany dla hello źródła zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="59402-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="59402-135">Domyślne dopasowuje wszystkie typy zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="59402-135">Default matches all event types.</span></span> |
| <span data-ttu-id="59402-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="59402-136">subjectBeginsWith</span></span> | <span data-ttu-id="59402-137">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59402-137">string</span></span> | <span data-ttu-id="59402-138">Dopasowanie prefiksu toohello podmiotu pole filtru w wiadomości powitania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="59402-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="59402-139">domyślne Hello lub pusty ciąg pasuje do wszystkich.</span><span class="sxs-lookup"><span data-stu-id="59402-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="59402-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="59402-140">subjectEndsWith</span></span> | <span data-ttu-id="59402-141">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59402-141">string</span></span> | <span data-ttu-id="59402-142">Uwzględnij sufiks toohello podmiotu pole filtru w wiadomości powitania zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="59402-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="59402-143">domyślne Hello lub pusty ciąg pasuje do wszystkich.</span><span class="sxs-lookup"><span data-stu-id="59402-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="59402-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="59402-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="59402-145">Ciąg</span><span class="sxs-lookup"><span data-stu-id="59402-145">string</span></span> | <span data-ttu-id="59402-146">Formanty z uwzględnieniem wielkości liter dopasowanie filtrów.</span><span class="sxs-lookup"><span data-stu-id="59402-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="59402-147">Przykład subskrypcji schematu</span><span class="sxs-lookup"><span data-stu-id="59402-147">Example subscription schema</span></span>

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="59402-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="59402-148">Next steps</span></span>

* <span data-ttu-id="59402-149">Aby tooEvent wprowadzenie siatki, zobacz [co to jest zdarzenie siatki?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="59402-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
