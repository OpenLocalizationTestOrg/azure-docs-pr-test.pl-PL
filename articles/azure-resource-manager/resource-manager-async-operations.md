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
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="40f1a-103">Śledzenie Azure operacji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="40f1a-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="40f1a-104">Niektóre operacje Azure REST jest uruchamiane asynchronicznie, ponieważ nie można ukończyć operacji hello szybko.</span><span class="sxs-lookup"><span data-stu-id="40f1a-104">Some Azure REST operations run asynchronously because hello operation cannot be completed quickly.</span></span> <span data-ttu-id="40f1a-105">W tym temacie opisano, jak tootrack hello stanu operacji asynchronicznych za pomocą wartości zwracany w odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="40f1a-105">This topic describes how tootrack hello status of asynchronous operations through values returned in hello response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="40f1a-106">Kody stanu dla operacji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="40f1a-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="40f1a-107">Operacja asynchroniczna początkowo zwraca kod stanu HTTP albo:</span><span class="sxs-lookup"><span data-stu-id="40f1a-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="40f1a-108">201 (utworzono)</span><span class="sxs-lookup"><span data-stu-id="40f1a-108">201 (Created)</span></span>
* <span data-ttu-id="40f1a-109">202 (zaakceptowane)</span><span class="sxs-lookup"><span data-stu-id="40f1a-109">202 (Accepted)</span></span> 

<span data-ttu-id="40f1a-110">Po pomyślnym zakończeniu operacji hello, zwraca albo:</span><span class="sxs-lookup"><span data-stu-id="40f1a-110">When hello operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="40f1a-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="40f1a-111">200 (OK)</span></span>
* <span data-ttu-id="40f1a-112">204 (Brak zawartości)</span><span class="sxs-lookup"><span data-stu-id="40f1a-112">204 (No Content)</span></span> 

<span data-ttu-id="40f1a-113">Zobacz toohello [dokumentacja interfejsu API REST](/rest/api/) toosee hello odpowiedzi dla operacji hello są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="40f1a-113">Refer toohello [REST API documentation](/rest/api/) toosee hello responses for hello operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="40f1a-114">Monitor stanu operacji</span><span class="sxs-lookup"><span data-stu-id="40f1a-114">Monitor status of operation</span></span>
<span data-ttu-id="40f1a-115">Hello asynchroniczne REST operacji zwracane wartości nagłówka, wykorzystujących toodetermine hello stan hello operacji.</span><span class="sxs-lookup"><span data-stu-id="40f1a-115">hello asynchronous REST operations return header values, which you use toodetermine hello status of hello operation.</span></span> <span data-ttu-id="40f1a-116">Istnieją potencjalnie tooexamine wartości nagłówka trzy:</span><span class="sxs-lookup"><span data-stu-id="40f1a-116">There are potentially three header values tooexamine:</span></span>

* <span data-ttu-id="40f1a-117">`Azure-AsyncOperation`— Adres URL sprawdzania hello stan trwającej operacji hello.</span><span class="sxs-lookup"><span data-stu-id="40f1a-117">`Azure-AsyncOperation` - URL for checking hello ongoing status of hello operation.</span></span> <span data-ttu-id="40f1a-118">Jeśli operacja zwraca tę wartość, należy zawsze używać it (a nie lokalizacja) tootrack hello stan hello operacji.</span><span class="sxs-lookup"><span data-stu-id="40f1a-118">If your operation returns this value, always use it (instead of Location) tootrack hello status of hello operation.</span></span>
* <span data-ttu-id="40f1a-119">`Location`— Adres URL, określając po zakończeniu operacji.</span><span class="sxs-lookup"><span data-stu-id="40f1a-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="40f1a-120">Użyj tej wartości, tylko wtedy, gdy nie są zwracane przez operację asynchroniczną Azure.</span><span class="sxs-lookup"><span data-stu-id="40f1a-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="40f1a-121">`Retry-After`-hello liczbę sekund toowait przed sprawdzeniem stanu hello hello operację asynchroniczną.</span><span class="sxs-lookup"><span data-stu-id="40f1a-121">`Retry-After` - hello number of seconds toowait before checking hello status of hello asynchronous operation.</span></span>

<span data-ttu-id="40f1a-122">Jednak nie każda operacja asynchroniczna zwraca wszystkie te wartości.</span><span class="sxs-lookup"><span data-stu-id="40f1a-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="40f1a-123">Wartość nagłówka operację asynchroniczną Azure hello tooevaluate może być konieczne na przykład jedna operacja i wartości nagłówka lokalizacji hello inna operacja.</span><span class="sxs-lookup"><span data-stu-id="40f1a-123">For example, you may need tooevaluate hello Azure-AsyncOperation header value for one operation, and hello Location header value for another operation.</span></span> 

<span data-ttu-id="40f1a-124">Możesz pobrać hello wartości nagłówka, ponieważ może pobrać wartości nagłówka żądania.</span><span class="sxs-lookup"><span data-stu-id="40f1a-124">You retrieve hello header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="40f1a-125">Na przykład w języku C#, możesz pobrać wartość nagłówka hello `HttpWebResponse` obiektu o nazwie `response` z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="40f1a-125">For example, in C#, you retrieve hello header value from an `HttpWebResponse` object named `response` with hello following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="40f1a-126">Azure AsyncOperation żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="40f1a-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="40f1a-127">tooget hello stan operacji asynchronicznej hello, Wyślij adres URL toohello żądania GET w wartości nagłówka operację asynchroniczną na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="40f1a-127">tooget hello status of hello asynchronous operation, send a GET request toohello URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="40f1a-128">Hello treść odpowiedzi hello z tej operacji zawiera informacje na temat operacji hello.</span><span class="sxs-lookup"><span data-stu-id="40f1a-128">hello body of hello response from this operation contains information about hello operation.</span></span> <span data-ttu-id="40f1a-129">Witaj poniższy przykład przedstawia hello możliwe wartości zwracane z operacji hello:</span><span class="sxs-lookup"><span data-stu-id="40f1a-129">hello following example shows hello possible values returned from hello operation:</span></span>

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

<span data-ttu-id="40f1a-130">Tylko `status` są zwracane do wszystkich odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="40f1a-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="40f1a-131">Witaj błąd obiekt jest zwracany, gdy hello stan to niepowodzenie lub anulowane.</span><span class="sxs-lookup"><span data-stu-id="40f1a-131">hello error object is returned when hello status is Failed or Canceled.</span></span> <span data-ttu-id="40f1a-132">Wszystkie inne wartości są opcjonalne; w związku z tym hello odpowiedzi, które otrzymujesz mogą wyglądać inaczej niż przykład Witaj.</span><span class="sxs-lookup"><span data-stu-id="40f1a-132">All other values are optional; therefore, hello response you receive may look different than hello example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="40f1a-133">wartości właściwości provisioningState</span><span class="sxs-lookup"><span data-stu-id="40f1a-133">provisioningState values</span></span>

<span data-ttu-id="40f1a-134">Operacje, które tworzenie, aktualizowanie lub usuwanie (PUT, PATCH, Usuń) zasobu zwracają zazwyczaj `provisioningState` wartość.</span><span class="sxs-lookup"><span data-stu-id="40f1a-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="40f1a-135">Po ukończeniu operacji, zwracany jest jeden z trzech następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="40f1a-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="40f1a-136">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="40f1a-136">Succeeded</span></span>
* <span data-ttu-id="40f1a-137">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="40f1a-137">Failed</span></span>
* <span data-ttu-id="40f1a-138">Anulowane</span><span class="sxs-lookup"><span data-stu-id="40f1a-138">Canceled</span></span>

<span data-ttu-id="40f1a-139">Wszystkie inne wartości oznaczają, że operacji hello jest nadal uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="40f1a-139">All other values indicate hello operation is still running.</span></span> <span data-ttu-id="40f1a-140">Dostawca zasobów Hello może zwrócić dostosowanych wartości wskazującej, jego stan.</span><span class="sxs-lookup"><span data-stu-id="40f1a-140">hello resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="40f1a-141">Na przykład może zostać wyświetlony **zaakceptowane** podczas żądania hello jest odebrane i uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="40f1a-141">For example, you may receive **Accepted** when hello request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="40f1a-142">Przykład żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="40f1a-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="40f1a-143">Uruchom maszynę wirtualną (202 z operację asynchroniczną Azure)</span><span class="sxs-lookup"><span data-stu-id="40f1a-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="40f1a-144">W tym przykładzie pokazano, jak toodetermine hello stan **start** operacji dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="40f1a-144">This example shows how toodetermine hello status of **start** operation for virtual machines.</span></span> <span data-ttu-id="40f1a-145">żądanie początkowej Hello jest hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="40f1a-145">hello initial request is in hello following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="40f1a-146">Zwraca kod stanu 202.</span><span class="sxs-lookup"><span data-stu-id="40f1a-146">It returns status code 202.</span></span> <span data-ttu-id="40f1a-147">Wśród hello wartości nagłówka wyświetlane są:</span><span class="sxs-lookup"><span data-stu-id="40f1a-147">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="40f1a-148">Stan hello toocheck hello operację asynchroniczną, wysyłanie inny adres URL toothat żądania.</span><span class="sxs-lookup"><span data-stu-id="40f1a-148">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="40f1a-149">treść odpowiedzi Hello zawiera hello stanu operacji hello:</span><span class="sxs-lookup"><span data-stu-id="40f1a-149">hello response body contains hello status of hello operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="40f1a-150">Wdrażanie zasobów (201 z operację asynchroniczną Azure)</span><span class="sxs-lookup"><span data-stu-id="40f1a-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="40f1a-151">W tym przykładzie pokazano, jak toodetermine hello stan **wdrożeń** operacji wdrażania tooAzure zasobów.</span><span class="sxs-lookup"><span data-stu-id="40f1a-151">This example shows how toodetermine hello status of **deployments** operation for deploying resources tooAzure.</span></span> <span data-ttu-id="40f1a-152">żądanie początkowej Hello jest hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="40f1a-152">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="40f1a-153">Zwraca kod stanu 201.</span><span class="sxs-lookup"><span data-stu-id="40f1a-153">It returns status code 201.</span></span> <span data-ttu-id="40f1a-154">Witaj treść odpowiedzi hello obejmuje:</span><span class="sxs-lookup"><span data-stu-id="40f1a-154">hello body of hello response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="40f1a-155">Wśród hello wartości nagłówka wyświetlane są:</span><span class="sxs-lookup"><span data-stu-id="40f1a-155">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="40f1a-156">Stan hello toocheck hello operację asynchroniczną, wysyłanie inny adres URL toothat żądania.</span><span class="sxs-lookup"><span data-stu-id="40f1a-156">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="40f1a-157">treść odpowiedzi Hello zawiera hello stanu operacji hello:</span><span class="sxs-lookup"><span data-stu-id="40f1a-157">hello response body contains hello status of hello operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="40f1a-158">Po zakończeniu wdrażania hello hello odpowiedź zawiera:</span><span class="sxs-lookup"><span data-stu-id="40f1a-158">When hello deployment is finished, hello response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="40f1a-159">Tworzenie konta magazynu (202 z lokalizacji i ponów próbę po)</span><span class="sxs-lookup"><span data-stu-id="40f1a-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="40f1a-160">W tym przykładzie pokazano, jak toodetermine hello stan hello **utworzyć** operacji dla kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="40f1a-160">This example shows how toodetermine hello status of hello **create** operation for storage accounts.</span></span> <span data-ttu-id="40f1a-161">żądanie początkowej Hello jest hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="40f1a-161">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="40f1a-162">I treści żądania hello zawiera właściwości konta magazynu hello:</span><span class="sxs-lookup"><span data-stu-id="40f1a-162">And hello request body contains properties for hello storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="40f1a-163">Zwraca kod stanu 202.</span><span class="sxs-lookup"><span data-stu-id="40f1a-163">It returns status code 202.</span></span> <span data-ttu-id="40f1a-164">Wśród wartości nagłówka hello zobacz temat powitania po dwóch wartości:</span><span class="sxs-lookup"><span data-stu-id="40f1a-164">Among hello header values, you see hello following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="40f1a-165">Po upływie liczby sekund określony w ponownych prób po, sprawdź stan operacji asynchronicznej hello hello wysyłając inny adres URL toothat żądania.</span><span class="sxs-lookup"><span data-stu-id="40f1a-165">After waiting for number of seconds specified in Retry-After, check hello status of hello asynchronous operation by sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="40f1a-166">Jeśli Żądanie hello jest nadal uruchomiony, zostanie wyświetlony kod stanu 202.</span><span class="sxs-lookup"><span data-stu-id="40f1a-166">If hello request is still running, you receive a status code 202.</span></span> <span data-ttu-id="40f1a-167">Jeśli hello żądania zostało ukończone, z kodem stanu 200 odbierania i hello treść odpowiedzi hello zawiera właściwości hello hello konta magazynu, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="40f1a-167">If hello request has completed, your receive a status code 200, and hello body of hello response contains hello properties of hello storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40f1a-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="40f1a-168">Next steps</span></span>

* <span data-ttu-id="40f1a-169">Aby uzyskać dokumentację każdej operacji REST, zobacz [dokumentacja interfejsu API REST](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="40f1a-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="40f1a-170">Informacje o zarządzaniu zasobami za pośrednictwem hello interfejsu REST API usługi Resource Manager, zobacz [hello używanie interfejsu REST API usługi Resource Manager](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="40f1a-170">For information about managing resources through hello Resource Manager REST API, see [Using hello Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="40f1a-171">informacje o wdrażaniu szablonów za pośrednictwem hello interfejsu REST API usługi Resource Manager, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu REST API usługi Resource Manager](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="40f1a-171">for information about deploying templates through hello Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>
