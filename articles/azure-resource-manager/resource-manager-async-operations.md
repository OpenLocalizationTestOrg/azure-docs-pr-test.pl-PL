---
title: Operacje asynchroniczne aaaAzure | Dokumentacja firmy Microsoft
description: "Opisuje sposób tootrack operacji asynchronicznych na platformie Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a>Śledzenie Azure operacji asynchronicznych
Niektóre operacje Azure REST jest uruchamiane asynchronicznie, ponieważ nie można ukończyć operacji hello szybko. W tym temacie opisano, jak tootrack hello stanu operacji asynchronicznych za pomocą wartości zwracany w odpowiedzi hello.  

## <a name="status-codes-for-asynchronous-operations"></a>Kody stanu dla operacji asynchronicznych
Operacja asynchroniczna początkowo zwraca kod stanu HTTP albo:

* 201 (utworzono)
* 202 (zaakceptowane) 

Po pomyślnym zakończeniu operacji hello, zwraca albo:

* 200 (OK)
* 204 (Brak zawartości) 

Zobacz toohello [dokumentacja interfejsu API REST](/rest/api/) toosee hello odpowiedzi dla operacji hello są wykonywane. 

## <a name="monitor-status-of-operation"></a>Monitor stanu operacji
Hello asynchroniczne REST operacji zwracane wartości nagłówka, wykorzystujących toodetermine hello stan hello operacji. Istnieją potencjalnie tooexamine wartości nagłówka trzy:

* `Azure-AsyncOperation`— Adres URL sprawdzania hello stan trwającej operacji hello. Jeśli operacja zwraca tę wartość, należy zawsze używać it (a nie lokalizacja) tootrack hello stan hello operacji.
* `Location`— Adres URL, określając po zakończeniu operacji. Użyj tej wartości, tylko wtedy, gdy nie są zwracane przez operację asynchroniczną Azure.
* `Retry-After`-hello liczbę sekund toowait przed sprawdzeniem stanu hello hello operację asynchroniczną.

Jednak nie każda operacja asynchroniczna zwraca wszystkie te wartości. Wartość nagłówka operację asynchroniczną Azure hello tooevaluate może być konieczne na przykład jedna operacja i wartości nagłówka lokalizacji hello inna operacja. 

Możesz pobrać hello wartości nagłówka, ponieważ może pobrać wartości nagłówka żądania. Na przykład w języku C#, możesz pobrać wartość nagłówka hello `HttpWebResponse` obiektu o nazwie `response` z hello następującego kodu:

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Azure AsyncOperation żądań i odpowiedzi

tooget hello stan operacji asynchronicznej hello, Wyślij adres URL toohello żądania GET w wartości nagłówka operację asynchroniczną na platformie Azure.

Hello treść odpowiedzi hello z tej operacji zawiera informacje na temat operacji hello. Witaj poniższy przykład przedstawia hello możliwe wartości zwracane z operacji hello:

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

Tylko `status` są zwracane do wszystkich odpowiedzi. Witaj błąd obiekt jest zwracany, gdy hello stan to niepowodzenie lub anulowane. Wszystkie inne wartości są opcjonalne; w związku z tym hello odpowiedzi, które otrzymujesz mogą wyglądać inaczej niż przykład Witaj.

## <a name="provisioningstate-values"></a>wartości właściwości provisioningState

Operacje, które tworzenie, aktualizowanie lub usuwanie (PUT, PATCH, Usuń) zasobu zwracają zazwyczaj `provisioningState` wartość. Po ukończeniu operacji, zwracany jest jeden z trzech następujących wartości: 

* Powodzenie
* Nie powiodło się
* Anulowane

Wszystkie inne wartości oznaczają, że operacji hello jest nadal uruchomiona. Dostawca zasobów Hello może zwrócić dostosowanych wartości wskazującej, jego stan. Na przykład może zostać wyświetlony **zaakceptowane** podczas żądania hello jest odebrane i uruchomiona.

## <a name="example-requests-and-responses"></a>Przykład żądań i odpowiedzi

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>Uruchom maszynę wirtualną (202 z operację asynchroniczną Azure)
W tym przykładzie pokazano, jak toodetermine hello stan **start** operacji dla maszyn wirtualnych. żądanie początkowej Hello jest hello następującego formatu:

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

Zwraca kod stanu 202. Wśród hello wartości nagłówka wyświetlane są:

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

Stan hello toocheck hello operację asynchroniczną, wysyłanie inny adres URL toothat żądania.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

treść odpowiedzi Hello zawiera hello stanu operacji hello:

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>Wdrażanie zasobów (201 z operację asynchroniczną Azure)

W tym przykładzie pokazano, jak toodetermine hello stan **wdrożeń** operacji wdrażania tooAzure zasobów. żądanie początkowej Hello jest hello następującego formatu:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

Zwraca kod stanu 201. Witaj treść odpowiedzi hello obejmuje:

```json
"provisioningState":"Accepted",
```

Wśród hello wartości nagłówka wyświetlane są:

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

Stan hello toocheck hello operację asynchroniczną, wysyłanie inny adres URL toothat żądania.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

treść odpowiedzi Hello zawiera hello stanu operacji hello:

```json
{"status":"Running"}
```

Po zakończeniu wdrażania hello hello odpowiedź zawiera:

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>Tworzenie konta magazynu (202 z lokalizacji i ponów próbę po)

W tym przykładzie pokazano, jak toodetermine hello stan hello **utworzyć** operacji dla kont magazynu. żądanie początkowej Hello jest hello następującego formatu:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

I treści żądania hello zawiera właściwości konta magazynu hello:

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

Zwraca kod stanu 202. Wśród wartości nagłówka hello zobacz temat powitania po dwóch wartości:

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

Po upływie liczby sekund określony w ponownych prób po, sprawdź stan operacji asynchronicznej hello hello wysyłając inny adres URL toothat żądania.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

Jeśli Żądanie hello jest nadal uruchomiony, zostanie wyświetlony kod stanu 202. Jeśli hello żądania zostało ukończone, z kodem stanu 200 odbierania i hello treść odpowiedzi hello zawiera właściwości hello hello konta magazynu, który został utworzony.

## <a name="next-steps"></a>Następne kroki

* Aby uzyskać dokumentację każdej operacji REST, zobacz [dokumentacja interfejsu API REST](/rest/api/).
* Informacje o zarządzaniu zasobami za pośrednictwem hello interfejsu REST API usługi Resource Manager, zobacz [hello używanie interfejsu REST API usługi Resource Manager](resource-manager-rest-api.md).
* informacje o wdrażaniu szablonów za pośrednictwem hello interfejsu REST API usługi Resource Manager, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu REST API usługi Resource Manager](resource-group-template-deploy-rest.md).
