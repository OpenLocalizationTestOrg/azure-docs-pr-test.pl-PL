---
title: Operacje asynchroniczne platformy Azure | Dokumentacja firmy Microsoft
description: "Informacje dotyczące śledzenia operacji asynchronicznych na platformie Azure."
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
ms.openlocfilehash: 9fe3d98cd345aae45722295b6c1b7fc3e9036e95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="6d58e-103">Śledzenie Azure operacji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="6d58e-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="6d58e-104">Niektóre operacje Azure REST jest uruchamiane asynchronicznie, ponieważ nie można ukończyć operacji, szybko.</span><span class="sxs-lookup"><span data-stu-id="6d58e-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span></span> <span data-ttu-id="6d58e-105">W tym temacie opisano, jak śledzić stan operacji asynchronicznych za pomocą wartości zwracanych w odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6d58e-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="6d58e-106">Kody stanu dla operacji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="6d58e-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="6d58e-107">Operacja asynchroniczna początkowo zwraca kod stanu HTTP albo:</span><span class="sxs-lookup"><span data-stu-id="6d58e-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="6d58e-108">201 (utworzono)</span><span class="sxs-lookup"><span data-stu-id="6d58e-108">201 (Created)</span></span>
* <span data-ttu-id="6d58e-109">202 (zaakceptowane)</span><span class="sxs-lookup"><span data-stu-id="6d58e-109">202 (Accepted)</span></span> 

<span data-ttu-id="6d58e-110">Po pomyślnym zakończeniu operacji zwraca albo:</span><span class="sxs-lookup"><span data-stu-id="6d58e-110">When the operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="6d58e-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="6d58e-111">200 (OK)</span></span>
* <span data-ttu-id="6d58e-112">204 (Brak zawartości)</span><span class="sxs-lookup"><span data-stu-id="6d58e-112">204 (No Content)</span></span> 

<span data-ttu-id="6d58e-113">Zapoznaj się [dokumentacja interfejsu API REST](/rest/api/) do odpowiedzi dla operacji są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="6d58e-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="6d58e-114">Monitor stanu operacji</span><span class="sxs-lookup"><span data-stu-id="6d58e-114">Monitor status of operation</span></span>
<span data-ttu-id="6d58e-115">Operacje asynchroniczne REST nagłówka wartości zwracane, które można określić stanu operacji.</span><span class="sxs-lookup"><span data-stu-id="6d58e-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span></span> <span data-ttu-id="6d58e-116">Istnieją potencjalnie trzy wartości nagłówka do sprawdzenia:</span><span class="sxs-lookup"><span data-stu-id="6d58e-116">There are potentially three header values to examine:</span></span>

* <span data-ttu-id="6d58e-117">`Azure-AsyncOperation`— Adres URL do sprawdzania stanu trwających operacji.</span><span class="sxs-lookup"><span data-stu-id="6d58e-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span></span> <span data-ttu-id="6d58e-118">Jeśli operacja zwraca tę wartość, zawsze używać go (a nie lokalizacja) do śledzenia stanu operacji.</span><span class="sxs-lookup"><span data-stu-id="6d58e-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span></span>
* <span data-ttu-id="6d58e-119">`Location`— Adres URL, określając po zakończeniu operacji.</span><span class="sxs-lookup"><span data-stu-id="6d58e-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="6d58e-120">Użyj tej wartości, tylko wtedy, gdy nie są zwracane przez operację asynchroniczną Azure.</span><span class="sxs-lookup"><span data-stu-id="6d58e-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="6d58e-121">`Retry-After`-Liczbę sekund oczekiwania przed sprawdzeniem stanu operacji asynchronicznej.</span><span class="sxs-lookup"><span data-stu-id="6d58e-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span></span>

<span data-ttu-id="6d58e-122">Jednak nie każda operacja asynchroniczna zwraca wszystkie te wartości.</span><span class="sxs-lookup"><span data-stu-id="6d58e-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="6d58e-123">Na przykład może być konieczne obliczyć wartość nagłówka operację asynchroniczną Azure dla jednej operacji, a wartość nagłówka lokalizacji innej operacji.</span><span class="sxs-lookup"><span data-stu-id="6d58e-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span></span> 

<span data-ttu-id="6d58e-124">Można pobrać wartości nagłówka, ponieważ może pobrać wartości nagłówka żądania.</span><span class="sxs-lookup"><span data-stu-id="6d58e-124">You retrieve the header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="6d58e-125">Na przykład w języku C#, możesz pobrać wartość nagłówka z `HttpWebResponse` obiektu o nazwie `response` z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="6d58e-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="6d58e-126">Azure AsyncOperation żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6d58e-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="6d58e-127">Aby uzyskać stan operacji asynchronicznej, Wyślij żądanie GET do adresu URL w wartości nagłówka operację asynchroniczną na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6d58e-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="6d58e-128">Treść odpowiedzi z tej operacji zawiera informacje na temat operacji.</span><span class="sxs-lookup"><span data-stu-id="6d58e-128">The body of the response from this operation contains information about the operation.</span></span> <span data-ttu-id="6d58e-129">W poniższym przykładzie przedstawiono możliwe wartości zwrócony przez operację:</span><span class="sxs-lookup"><span data-stu-id="6d58e-129">The following example shows the possible values returned from the operation:</span></span>

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

<span data-ttu-id="6d58e-130">Tylko `status` są zwracane do wszystkich odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="6d58e-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="6d58e-131">Obiekt błąd jest zwracany, gdy stan to niepowodzenie lub anulowane.</span><span class="sxs-lookup"><span data-stu-id="6d58e-131">The error object is returned when the status is Failed or Canceled.</span></span> <span data-ttu-id="6d58e-132">Wszystkie inne wartości są opcjonalne; w związku z tym odpowiedzi otrzymywanych może różnić się od tego przykładu.</span><span class="sxs-lookup"><span data-stu-id="6d58e-132">All other values are optional; therefore, the response you receive may look different than the example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="6d58e-133">wartości właściwości provisioningState</span><span class="sxs-lookup"><span data-stu-id="6d58e-133">provisioningState values</span></span>

<span data-ttu-id="6d58e-134">Operacje, które tworzenie, aktualizowanie lub usuwanie (PUT, PATCH, Usuń) zasobu zwracają zazwyczaj `provisioningState` wartość.</span><span class="sxs-lookup"><span data-stu-id="6d58e-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="6d58e-135">Po ukończeniu operacji, zwracany jest jeden z trzech następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="6d58e-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="6d58e-136">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="6d58e-136">Succeeded</span></span>
* <span data-ttu-id="6d58e-137">Nie powiodło się</span><span class="sxs-lookup"><span data-stu-id="6d58e-137">Failed</span></span>
* <span data-ttu-id="6d58e-138">Anulowane</span><span class="sxs-lookup"><span data-stu-id="6d58e-138">Canceled</span></span>

<span data-ttu-id="6d58e-139">Wszystkie inne wartości oznaczają, że operacji jest nadal uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6d58e-139">All other values indicate the operation is still running.</span></span> <span data-ttu-id="6d58e-140">Dostawca zasobów można zwrócić dostosowanych wartości wskazującej, jego stan.</span><span class="sxs-lookup"><span data-stu-id="6d58e-140">The resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="6d58e-141">Na przykład może zostać wyświetlony **zaakceptowane** podczas żądania jest odebrane i uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="6d58e-141">For example, you may receive **Accepted** when the request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="6d58e-142">Przykład żądań i odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="6d58e-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="6d58e-143">Uruchom maszynę wirtualną (202 z operację asynchroniczną Azure)</span><span class="sxs-lookup"><span data-stu-id="6d58e-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="6d58e-144">W tym przykładzie pokazano, jak ustalić stan **start** operacji dla maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6d58e-144">This example shows how to determine the status of **start** operation for virtual machines.</span></span> <span data-ttu-id="6d58e-145">Początkowe żądanie znajduje się w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="6d58e-145">The initial request is in the following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="6d58e-146">Zwraca kod stanu 202.</span><span class="sxs-lookup"><span data-stu-id="6d58e-146">It returns status code 202.</span></span> <span data-ttu-id="6d58e-147">Wśród wartości nagłówka wyświetlane są:</span><span class="sxs-lookup"><span data-stu-id="6d58e-147">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="6d58e-148">Aby sprawdzić stan operacji asynchronicznej, wysyłanie innego żądania do tego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="6d58e-148">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="6d58e-149">Treść odpowiedzi zawiera stan operacji:</span><span class="sxs-lookup"><span data-stu-id="6d58e-149">The response body contains the status of the operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="6d58e-150">Wdrażanie zasobów (201 z operację asynchroniczną Azure)</span><span class="sxs-lookup"><span data-stu-id="6d58e-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="6d58e-151">W tym przykładzie pokazano, jak ustalić stan **wdrożeń** Operacja wdrażania zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6d58e-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span></span> <span data-ttu-id="6d58e-152">Początkowe żądanie znajduje się w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="6d58e-152">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="6d58e-153">Zwraca kod stanu 201.</span><span class="sxs-lookup"><span data-stu-id="6d58e-153">It returns status code 201.</span></span> <span data-ttu-id="6d58e-154">Treść odpowiedzi zawiera:</span><span class="sxs-lookup"><span data-stu-id="6d58e-154">The body of the response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="6d58e-155">Wśród wartości nagłówka wyświetlane są:</span><span class="sxs-lookup"><span data-stu-id="6d58e-155">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="6d58e-156">Aby sprawdzić stan operacji asynchronicznej, wysyłanie innego żądania do tego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="6d58e-156">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="6d58e-157">Treść odpowiedzi zawiera stan operacji:</span><span class="sxs-lookup"><span data-stu-id="6d58e-157">The response body contains the status of the operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="6d58e-158">Po zakończeniu wdrożenia, zawiera odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="6d58e-158">When the deployment is finished, the response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="6d58e-159">Tworzenie konta magazynu (202 z lokalizacji i ponów próbę po)</span><span class="sxs-lookup"><span data-stu-id="6d58e-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="6d58e-160">W tym przykładzie pokazano, jak ustalić stan **utworzyć** operacji dla kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="6d58e-160">This example shows how to determine the status of the **create** operation for storage accounts.</span></span> <span data-ttu-id="6d58e-161">Początkowe żądanie znajduje się w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="6d58e-161">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="6d58e-162">I treść żądania zawiera właściwości konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="6d58e-162">And the request body contains properties for the storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="6d58e-163">Zwraca kod stanu 202.</span><span class="sxs-lookup"><span data-stu-id="6d58e-163">It returns status code 202.</span></span> <span data-ttu-id="6d58e-164">Wśród wartości nagłówka zobacz temat dwóch wartości:</span><span class="sxs-lookup"><span data-stu-id="6d58e-164">Among the header values, you see the following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="6d58e-165">Po oczekiwanie na liczbę sekund określonej w ponownych prób po, sprawdź stan operacji asynchronicznej, wysyłając innego żądania do tego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="6d58e-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="6d58e-166">Jeśli żądanie jest nadal uruchomiony, zostanie wyświetlony kod stanu 202.</span><span class="sxs-lookup"><span data-stu-id="6d58e-166">If the request is still running, you receive a status code 202.</span></span> <span data-ttu-id="6d58e-167">Jeśli żądanie zostało ukończone, z kodem stanu 200 odbierania i treść odpowiedzi zawiera właściwości konta magazynu, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="6d58e-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d58e-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6d58e-168">Next steps</span></span>

* <span data-ttu-id="6d58e-169">Aby uzyskać dokumentację każdej operacji REST, zobacz [dokumentacja interfejsu API REST](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="6d58e-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="6d58e-170">Informacje o zarządzaniu zasobami za pośrednictwem interfejsu REST API usługi Resource Manager, zobacz [przy użyciu interfejsu REST API usługi Resource Manager](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="6d58e-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="6d58e-171">informacje o wdrażaniu szablonów za pomocą interfejsu REST API usługi Resource Manager, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i interfejsu REST API usługi Resource Manager](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="6d58e-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>