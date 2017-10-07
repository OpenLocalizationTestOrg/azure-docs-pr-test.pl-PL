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
# <a name="event-grid-subscription-schema"></a>Schematu subskrypcji siatki zdarzeń

toocreate subskrypcji zdarzeń siatki, możesz wysłać toohello żądania operacji subskrypcji tworzenia zdarzeń. Witaj Użyj następującego formatu:

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Na przykład toocreate subskrypcji zdarzeń dla konta magazynu o nazwie `examplestorage` w grupie zasobów o nazwie `examplegroup`, użyj hello następującego formatu:

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Hello artykule hello właściwości i schematu dla treści hello hello żądania.
 
## <a name="event-subscription-properties"></a>Właściwości subskrypcji zdarzeń

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| Miejsce docelowe | Obiekt | Witaj obiektu, który definiuje hello punktu końcowego. |
| Filtr | Obiekt | Pole opcjonalne filtrowania hello typów zdarzeń. |

### <a name="destination-object"></a>obiekt docelowy

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| endpointType | Ciąg | Witaj typ punktu końcowego dla subskrypcji hello (webhook/HTTP Centrum zdarzeń i kolejki). | 
| adres URL punktu końcowego | Ciąg |  | 

### <a name="filter-object"></a>obiekt filtru

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| includedEventTypes | Tablica | Dopasowania, gdy typ zdarzenia hello w komunikacie zdarzenia hello jest tooone dokładnego dopasowania tych nazw typów zdarzeń. Zgłasza błąd, jeśli nazwa zdarzenia nie są zgodne z nazwy typów zdarzeń hello zarejestrowany dla hello źródła zdarzenia. Domyślne dopasowuje wszystkie typy zdarzeń. |
| subjectBeginsWith | Ciąg | Dopasowanie prefiksu toohello podmiotu pole filtru w wiadomości powitania zdarzeń. domyślne Hello lub pusty ciąg pasuje do wszystkich. | 
| subjectEndsWith | Ciąg | Uwzględnij sufiks toohello podmiotu pole filtru w wiadomości powitania zdarzeń. domyślne Hello lub pusty ciąg pasuje do wszystkich. |
| subjectIsCaseSensitive | Ciąg | Formanty z uwzględnieniem wielkości liter dopasowanie filtrów. |


## <a name="example-subscription-schema"></a>Przykład subskrypcji schematu

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

## <a name="next-steps"></a>Następne kroki

* Aby tooEvent wprowadzenie siatki, zobacz [co to jest zdarzenie siatki?](overview.md)
