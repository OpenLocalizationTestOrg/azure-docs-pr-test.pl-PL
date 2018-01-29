---
title: "Schematu zdarzeń magazynu obiektów blob Azure siatki zdarzeń"
description: "Opisuje właściwości, które są dostępne dla zdarzenia magazynu obiektów blob Azure zdarzeń siatki"
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 11/08/2017
ms.author: tomfitz
ms.openlocfilehash: bdc64733b75fd809cf0245986aa96370343c1a34
ms.sourcegitcommit: 6a22af82b88674cd029387f6cedf0fb9f8830afd
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/11/2017
---
# <a name="azure-event-grid-event-schema-for-blob-storage"></a>Azure schematu zdarzeń siatki zdarzeń dla magazynu obiektów Blob

Ten artykuł zawiera właściwości i schematu dla zdarzenia magazynu obiektów blob. Aby obejrzeć wprowadzenie do schematów zdarzeń, zobacz [schematu zdarzeń siatki zdarzeń Azure](event-schema.md).

## <a name="available-event-types"></a>Typy dostępnych zdarzeń

Magazyn obiektów blob emituje następujące typy zdarzeń:

| Typ zdarzenia | Opis |
| ---------- | ----------- |
| Microsoft.Storage.BlobCreated | Uruchamiany po utworzeniu obiektu blob. |
| Microsoft.Storage.BlobDeleted | Uruchamiany po usunięciu obiektu blob. |

## <a name="example-event"></a>Przykład zdarzeń

W poniższym przykładzie przedstawiono schematu obiektu blob utworzone zdarzenie: 

```json
[{
  "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
  "subject": "/blobServices/default/containers/testcontainer/blobs/testfile.txt",
  "eventType": "Microsoft.Storage.BlobCreated",
  "eventTime": "2017-06-26T18:41:00.9584103Z",
  "id": "831e1650-001e-001b-66ab-eeb76e069631",
  "data": {
    "api": "PutBlockList",
    "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
    "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
    "eTag": "0x8D4BCC2E4835CD0",
    "contentType": "text/plain",
    "contentLength": 524288,
    "blobType": "BlockBlob",
    "url": "https://example.blob.core.windows.net/testcontainer/testfile.txt",
    "sequencer": "00000000000004420000000000028963",
    "storageDiagnostics": {
      "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
    }
  }
}]
```

Schemat dla zdarzenia usunąć obiektu blob jest podobne: 

```json
[{
  "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
  "subject": "/blobServices/default/containers/testcontainer/blobs/testfile.txt",
  "eventType": "Microsoft.Storage.BlobDeleted",
  "eventTime": "2017-11-07T20:09:22.5674003Z",
  "id": "4c2359fe-001e-00ba-0e04-58586806d298",
  "data": {
    "api": "DeleteBlob",
    "requestId": "4c2359fe-001e-00ba-0e04-585868000000",
    "contentType": "text/plain",
    "blobType": "BlockBlob",
    "url": "https://example.blob.core.windows.net/testcontainer/testfile.txt",
    "sequencer": "0000000000000281000000000002F5CA",
    "storageDiagnostics": {
      "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
    }
  }
}]
```
 
## <a name="event-properties"></a>Właściwości zdarzenia

Zdarzenie ma następujące dane najwyższego poziomu:

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| Temat | Ciąg | Zasobów Pełna ścieżka do źródła zdarzeń. To pole nie jest zapisywalny. |
| Temat | Ciąg | Ścieżka zdefiniowana wydawcy podmiotem zdarzeń. |
| Typ zdarzenia | Ciąg | Jeden z typów zdarzeń zarejestrowane dla tego źródła zdarzenia. |
| eventTime | Ciąg | Czas jest generowane zdarzenie oparte na czas UTC dostawcy. |
| id | Ciąg | Unikatowy identyfikator zdarzenia. |
| Dane | Obiekt | Dane zdarzenia magazynu obiektów blob. |

Obiekt danych ma następujące właściwości:

| Właściwość | Typ | Opis |
| -------- | ---- | ----------- |
| api | Ciąg | Operacja, który wywołał zdarzenie. |
| ClientRequestId | Ciąg | Generowane przez klientów, nieprzezroczyste wartość Limit znaków 1 KB. Włączenie rejestrowania analityka magazynu jest rejestrowane w dziennikach analytics. |
| Identyfikator żądania | Ciąg | Unikatowy identyfikator dla żądania. Użyj go do rozwiązywania problemów z żądania. |
| Element ETag | Ciąg | Wartość, która służy do wykonywania operacji warunkowo. |
| Typ zawartości | Ciąg | Typ zawartości określony dla obiektu blob. |
| contentLength | Liczba całkowita | Rozmiar obiektu blob w bajtach. |
| BlobType | Ciąg | Typ obiektu blob. |
| adres URL | Ciąg | Ścieżka do obiektu blob. |
| Program Sequencer | Ciąg | Wartość kontrolowane przez użytkownika, która służy do śledzenia żądań. |
| storageDiagnostics | Obiekt | Informacje o diagnostyki magazynu. |
 
## <a name="next-steps"></a>Następne kroki

* Aby obejrzeć wprowadzenie do usługi Azure Event siatki, zobacz [co to jest zdarzenie siatki?](overview.md)
* Aby uzyskać więcej informacji o tworzeniu subskrypcji platformy Azure zdarzeń siatki, zobacz [schematu subskrypcji zdarzeń siatki](subscription-creation-schema.md).
* Wprowadzenie do pracy z zdarzenia magazynu obiektów blob, zobacz [zdarzenia magazynu obiektów Blob trasy - Azure CLI](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json). 
