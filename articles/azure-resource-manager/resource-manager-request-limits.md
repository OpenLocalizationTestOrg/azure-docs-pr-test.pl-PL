---
title: "Limity żądań usługi Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Informacje dotyczące używania przepustowości z żądaniami usługi Azure Resource Manager po osiągnięciu limitu subskrypcji."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 6d7eeaf460674c3ab98425a5412ffa465b9ffd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="9fa2b-103">Ograniczanie żądań Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9fa2b-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="9fa2b-104">Dla każdej subskrypcji i dzierżawy Resource Manager limity żądań do 15 000 na godzinę do odczytu i zapisu żądania 1200 na godzinę.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="9fa2b-105">Te limity mają zastosowanie do każdego wystąpienia usługi Azure Resource Manager; istnieje wiele wystąpień w każdym regionie Azure i wdrożeniu usługi Azure Resource Manager wszystkie regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-105">These limits apply to each Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed to all Azure regions.</span></span>  <span data-ttu-id="9fa2b-106">Zatem w praktyce limity są wydajnie znacznie wyższa niż wymienione powyżej, jako użytkownik żądań są zazwyczaj obsługiwane przez wiele różnych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="9fa2b-107">Jeśli aplikacji lub skryptu osiągnie tych ograniczeń, należy do ograniczania własnych żądań.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-107">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="9fa2b-108">W tym temacie przedstawiono sposób określania pozostałych żądań, które mają przed przekroczeniem limitu oraz sposobu odpowiedzi po osiągnięciu limitu.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-108">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="9fa2b-109">Po osiągnięciu limitu, otrzymasz kod stanu HTTP **429 zbyt wiele żądań**.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-109">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="9fa2b-110">Liczba żądań, które obejmuje subskrypcję lub dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-110">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="9fa2b-111">Jeśli masz wiele równoczesnych aplikacje wysyłania żądań w ramach subskrypcji, żądania z tych aplikacji są dodawane ze sobą w celu określenia liczby pozostałych żądań.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-111">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="9fa2b-112">Subskrypcja zakres żądania są te dotyczą przekazywanie identyfikator subskrypcji, takie jak pobieranie zasobu grup w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-112">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="9fa2b-113">Żądania dzierżawy w zakresie nie ma identyfikator subskrypcji, takie jak pobieranie prawidłowych lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="9fa2b-114">Pozostałych żądań</span><span class="sxs-lookup"><span data-stu-id="9fa2b-114">Remaining requests</span></span>
<span data-ttu-id="9fa2b-115">Liczba pozostałych żądań, które można określić, sprawdzając nagłówków odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-115">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="9fa2b-116">Każde żądanie zawiera wartości dla wielu żądań zapisu i odczytu pozostałych.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-116">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="9fa2b-117">W poniższej tabeli opisano nagłówki odpowiedzi, który można sprawdzić dla tych wartości:</span><span class="sxs-lookup"><span data-stu-id="9fa2b-117">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="9fa2b-118">Nagłówek odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="9fa2b-118">Response header</span></span> | <span data-ttu-id="9fa2b-119">Opis</span><span class="sxs-lookup"><span data-stu-id="9fa2b-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9fa2b-120">x-MS-ratelimit-Remaining-Subscription-Reads</span><span class="sxs-lookup"><span data-stu-id="9fa2b-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="9fa2b-121">Odczytuje subskrypcji zakres pozostałych</span><span class="sxs-lookup"><span data-stu-id="9fa2b-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="9fa2b-122">x-MS-ratelimit-Remaining-Subscription-Writes</span><span class="sxs-lookup"><span data-stu-id="9fa2b-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="9fa2b-123">Zapisuje zakres subskrypcji pozostałych</span><span class="sxs-lookup"><span data-stu-id="9fa2b-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="9fa2b-124">x-MS-ratelimit-Remaining-tenant-Reads</span><span class="sxs-lookup"><span data-stu-id="9fa2b-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="9fa2b-125">Zakres dzierżawy odczytuje pozostałych</span><span class="sxs-lookup"><span data-stu-id="9fa2b-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="9fa2b-126">x-MS-ratelimit-Remaining-tenant-Writes</span><span class="sxs-lookup"><span data-stu-id="9fa2b-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="9fa2b-127">Zapisuje zakres dzierżawy pozostałych</span><span class="sxs-lookup"><span data-stu-id="9fa2b-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="9fa2b-128">x-MS-ratelimit-Remaining-Subscription-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="9fa2b-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="9fa2b-129">Subskrypcja zakresu pozostałych żądań typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="9fa2b-130">Wartość tego nagłówka jest zwracany tylko wtedy, jeśli usługa ma zastąpić domyślny limit.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-130">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="9fa2b-131">Menedżer zasobów dodaje tej wartości, zamiast subskrypcji odczytów i zapisów.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-131">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="9fa2b-132">x-MS-ratelimit-Remaining-Subscription-Resource-ENTITIES-Read</span><span class="sxs-lookup"><span data-stu-id="9fa2b-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="9fa2b-133">Subskrypcja zakresu pozostałych żądania kolekcji dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="9fa2b-134">Wartość tego nagłówka jest zwracany tylko wtedy, jeśli usługa ma zastąpić domyślny limit.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-134">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="9fa2b-135">Ta wartość określa liczbę pozostałych żądań kolekcji (listy zasobów).</span><span class="sxs-lookup"><span data-stu-id="9fa2b-135">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="9fa2b-136">x-MS-ratelimit-Remaining-tenant-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="9fa2b-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="9fa2b-137">Zakres dzierżawy pozostałych żądań typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="9fa2b-138">Ten nagłówek jest dodawać tylko dla żądań na poziomie dzierżawy, a tylko wtedy, gdy usługa ma zastąpić domyślny limit.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-138">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="9fa2b-139">Menedżer zasobów dodaje tej wartości, zamiast dzierżawy odczytów i zapisów.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-139">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="9fa2b-140">x-MS-ratelimit-Remaining-tenant-Resource-ENTITIES-Read</span><span class="sxs-lookup"><span data-stu-id="9fa2b-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="9fa2b-141">Dzierżawy zakresu pozostałych żądania kolekcji dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="9fa2b-142">Ten nagłówek jest dodawać tylko dla żądań na poziomie dzierżawy, a tylko wtedy, gdy usługa ma zastąpić domyślny limit.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-142">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="9fa2b-143">Pobieranie wartości nagłówka</span><span class="sxs-lookup"><span data-stu-id="9fa2b-143">Retrieving the header values</span></span>
<span data-ttu-id="9fa2b-144">Nie różni się od pobierania wartości nagłówka się podczas pobierania tych wartości nagłówka w tym kod lub skrypt.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="9fa2b-145">Na przykład w **C#**, możesz pobrać wartość nagłówka z **HttpWebResponse** obiektu o nazwie **odpowiedzi** następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="9fa2b-145">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="9fa2b-146">W **PowerShell**, pobrać wartość nagłówka podczas operacji Invoke WebRequest.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-146">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="9fa2b-147">Lub, jeśli chcesz zobaczyć pozostałych żądań do debugowania, możesz podać **-Debug** parametru na Twojej **środowiska PowerShell** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-147">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="9fa2b-148">Która zwraca wiele wartości, z uwzględnieniem następujących wartości odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="9fa2b-148">Which returns many values, including the following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="9fa2b-149">W **interfejsu wiersza polecenia Azure**, pobrać wartość nagłówka przy użyciu opcji na pełniejsze.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-149">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="9fa2b-150">Która zwraca wiele wartości, w tym następujący obiekt:</span><span class="sxs-lookup"><span data-stu-id="9fa2b-150">Which returns many values, including the following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="9fa2b-151">Oczekiwania przed wysłaniem żądania dalej</span><span class="sxs-lookup"><span data-stu-id="9fa2b-151">Waiting before sending next request</span></span>
<span data-ttu-id="9fa2b-152">Po osiągnięciu limitu żądań, Menedżer zasobów zwraca **429** kod stanu HTTP i **ponownych prób po** wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-152">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="9fa2b-153">**Ponownych prób po** wartość określa liczbę sekund oczekiwania w aplikacji (lub uśpienia) przed wysłaniem następnego żądania.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-153">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="9fa2b-154">Po wysłaniu żądania, przed upływem wartość ponownych prób, Twoje żądanie nie jest przetwarzane i nowa wartość ponownych prób jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="9fa2b-154">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fa2b-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9fa2b-155">Next steps</span></span>

* <span data-ttu-id="9fa2b-156">Aby uzyskać więcej informacji na temat limitów i przydziały zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="9fa2b-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="9fa2b-157">Informacje na temat obsługi żądań asynchronicznych REST, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="9fa2b-157">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
