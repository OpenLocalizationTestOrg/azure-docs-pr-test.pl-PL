---
title: "limity żądań aaaAzure Resource Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse ograniczania z usługi Azure Resource Manager zażąda po osiągnięciu limitu subskrypcji."
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
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="f9351-103">Ograniczanie żądań Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f9351-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="f9351-104">Dla każdej subskrypcji i dzierżawy limity Resource Manager too15 żądania, 000 na godzinę i zapis too1 żądania, 200 na godzinę.</span><span class="sxs-lookup"><span data-stu-id="f9351-104">For each subscription and tenant, Resource Manager limits read requests too15,000 per hour and write requests too1,200 per hour.</span></span> <span data-ttu-id="f9351-105">Te limity mają zastosowanie wystąpienia usługi Azure Resource Manager tooeach; istnieje wiele wystąpień w każdym regionie Azure i usługi Azure Resource Manager jest wdrożony tooall Azure regionów.</span><span class="sxs-lookup"><span data-stu-id="f9351-105">These limits apply tooeach Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed tooall Azure regions.</span></span>  <span data-ttu-id="f9351-106">Zatem w praktyce limity są wydajnie znacznie wyższa niż wymienione powyżej, jako użytkownik żądań są zazwyczaj obsługiwane przez wiele różnych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="f9351-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="f9351-107">Jeśli aplikacji lub skryptu osiągnie tych ograniczeń, należy toothrottle Twojego żądania.</span><span class="sxs-lookup"><span data-stu-id="f9351-107">If your application or script reaches these limits, you need toothrottle your requests.</span></span> <span data-ttu-id="f9351-108">W tym temacie pokazano, jak hello toodetermine pozostałych żądań przed osiągnięciem limitu hello i jak toorespond po osiągnięciu limitu hello.</span><span class="sxs-lookup"><span data-stu-id="f9351-108">This topic shows you how toodetermine hello remaining requests you have before reaching hello limit, and how toorespond when you have reached hello limit.</span></span>

<span data-ttu-id="f9351-109">Po osiągnięciu limitu hello, otrzymasz kod stanu hello HTTP **429 zbyt wiele żądań**.</span><span class="sxs-lookup"><span data-stu-id="f9351-109">When you reach hello limit, you receive hello HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="f9351-110">Liczba żądań Hello jest tooeither zakresie subskrypcji lub dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="f9351-110">hello number of requests is scoped tooeither your subscription or your tenant.</span></span> <span data-ttu-id="f9351-111">Jeśli masz wiele, aplikacjami wysyłania żądań w ramach subskrypcji, hello żądań z tymi aplikacjami zostaną dodane razem toodetermine hello liczba pozostałych żądań.</span><span class="sxs-lookup"><span data-stu-id="f9351-111">If you have multiple, concurrent applications making requests in your subscription, hello requests from those applications are added together toodetermine hello number of remaining requests.</span></span>

<span data-ttu-id="f9351-112">Subskrypcja zakres żądania są hello obejmują przekazywanie identyfikator subskrypcji, takie jak pobieranie hello grup zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f9351-112">Subscription scoped requests are ones hello involve passing your subscription id, such as retrieving hello resource groups in your subscription.</span></span> <span data-ttu-id="f9351-113">Żądania dzierżawy w zakresie nie ma identyfikator subskrypcji, takie jak pobieranie prawidłowych lokalizacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f9351-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="f9351-114">Pozostałych żądań</span><span class="sxs-lookup"><span data-stu-id="f9351-114">Remaining requests</span></span>
<span data-ttu-id="f9351-115">Można określić hello liczbę pozostałych żądań, sprawdzając nagłówków odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f9351-115">You can determine hello number of remaining requests by examining response headers.</span></span> <span data-ttu-id="f9351-116">Każde żądanie zawiera wartości hello liczbę żądań zapisu i odczytu pozostałych.</span><span class="sxs-lookup"><span data-stu-id="f9351-116">Each request includes values for hello number of remaining read and write requests.</span></span> <span data-ttu-id="f9351-117">Witaj poniższej tabeli opisano hello nagłówki odpowiedzi, który można sprawdzić dla tych wartości:</span><span class="sxs-lookup"><span data-stu-id="f9351-117">hello following table describes hello response headers you can examine for those values:</span></span>

| <span data-ttu-id="f9351-118">Nagłówek odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f9351-118">Response header</span></span> | <span data-ttu-id="f9351-119">Opis</span><span class="sxs-lookup"><span data-stu-id="f9351-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f9351-120">x-MS-ratelimit-Remaining-Subscription-Reads</span><span class="sxs-lookup"><span data-stu-id="f9351-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="f9351-121">Odczytuje subskrypcji zakres pozostałych</span><span class="sxs-lookup"><span data-stu-id="f9351-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="f9351-122">x-MS-ratelimit-Remaining-Subscription-Writes</span><span class="sxs-lookup"><span data-stu-id="f9351-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="f9351-123">Zapisuje zakres subskrypcji pozostałych</span><span class="sxs-lookup"><span data-stu-id="f9351-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="f9351-124">x-MS-ratelimit-Remaining-tenant-Reads</span><span class="sxs-lookup"><span data-stu-id="f9351-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="f9351-125">Zakres dzierżawy odczytuje pozostałych</span><span class="sxs-lookup"><span data-stu-id="f9351-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="f9351-126">x-MS-ratelimit-Remaining-tenant-Writes</span><span class="sxs-lookup"><span data-stu-id="f9351-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="f9351-127">Zapisuje zakres dzierżawy pozostałych</span><span class="sxs-lookup"><span data-stu-id="f9351-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="f9351-128">x-MS-ratelimit-Remaining-Subscription-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="f9351-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="f9351-129">Subskrypcja zakresu pozostałych żądań typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="f9351-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="f9351-130">Wartość tego nagłówka jest zwracany tylko wtedy, jeśli usługa została zastąpiona hello domyślny limit.</span><span class="sxs-lookup"><span data-stu-id="f9351-130">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="f9351-131">Menedżer zasobów dodaje tej wartości, zamiast hello subskrypcji odczytów i zapisów.</span><span class="sxs-lookup"><span data-stu-id="f9351-131">Resource Manager adds this value instead of hello subscription reads or writes.</span></span> |
| <span data-ttu-id="f9351-132">x-MS-ratelimit-Remaining-Subscription-Resource-ENTITIES-Read</span><span class="sxs-lookup"><span data-stu-id="f9351-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="f9351-133">Subskrypcja zakresu pozostałych żądania kolekcji dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="f9351-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="f9351-134">Wartość tego nagłówka jest zwracany tylko wtedy, jeśli usługa została zastąpiona hello domyślny limit.</span><span class="sxs-lookup"><span data-stu-id="f9351-134">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="f9351-135">Ta wartość określa hello liczba pozostałych żądań kolekcji (listy zasobów).</span><span class="sxs-lookup"><span data-stu-id="f9351-135">This value provides hello number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="f9351-136">x-MS-ratelimit-Remaining-tenant-Resource-Requests</span><span class="sxs-lookup"><span data-stu-id="f9351-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="f9351-137">Zakres dzierżawy pozostałych żądań typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="f9351-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="f9351-138">Ten nagłówek jest dodawać tylko dla żądań na poziomie dzierżawy, a tylko wtedy, gdy usługa została zastąpiona hello domyślny limit.</span><span class="sxs-lookup"><span data-stu-id="f9351-138">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> <span data-ttu-id="f9351-139">Menedżer zasobów dodaje tej wartości, zamiast hello dzierżawy odczytów i zapisów.</span><span class="sxs-lookup"><span data-stu-id="f9351-139">Resource Manager adds this value instead of hello tenant reads or writes.</span></span> |
| <span data-ttu-id="f9351-140">x-MS-ratelimit-Remaining-tenant-Resource-ENTITIES-Read</span><span class="sxs-lookup"><span data-stu-id="f9351-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="f9351-141">Dzierżawy zakresu pozostałych żądania kolekcji dla typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="f9351-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="f9351-142">Ten nagłówek jest dodawać tylko dla żądań na poziomie dzierżawy, a tylko wtedy, gdy usługa została zastąpiona hello domyślny limit.</span><span class="sxs-lookup"><span data-stu-id="f9351-142">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> |

## <a name="retrieving-hello-header-values"></a><span data-ttu-id="f9351-143">Pobieranie wartości nagłówka hello</span><span class="sxs-lookup"><span data-stu-id="f9351-143">Retrieving hello header values</span></span>
<span data-ttu-id="f9351-144">Nie różni się od pobierania wartości nagłówka się podczas pobierania tych wartości nagłówka w tym kod lub skrypt.</span><span class="sxs-lookup"><span data-stu-id="f9351-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="f9351-145">Na przykład w **C#**, możesz pobrać wartość nagłówka hello **HttpWebResponse** obiektu o nazwie **odpowiedzi** z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="f9351-145">For example, in **C#**, you retrieve hello header value from an **HttpWebResponse** object named **response** with hello following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="f9351-146">W **PowerShell**, pobrać wartość nagłówka hello z operacji Invoke WebRequest.</span><span class="sxs-lookup"><span data-stu-id="f9351-146">In **PowerShell**, you retrieve hello header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="f9351-147">Lub, jeśli chcesz toosee hello pozostałych żądań do debugowania, możesz podać hello **-Debug** parametru na Twojej **środowiska PowerShell** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f9351-147">Or, if want toosee hello remaining requests for debugging, you can provide hello **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="f9351-148">Która zwraca wiele wartości, w tym powitania po wartość odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="f9351-148">Which returns many values, including hello following response value:</span></span>

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

<span data-ttu-id="f9351-149">W **interfejsu wiersza polecenia Azure**, pobrać wartość nagłówka hello za pomocą hello na pełniejsze opcji.</span><span class="sxs-lookup"><span data-stu-id="f9351-149">In **Azure CLI**, you retrieve hello header value by using hello more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="f9351-150">Która zwraca wiele wartości, w tym hello następującego obiektu:</span><span class="sxs-lookup"><span data-stu-id="f9351-150">Which returns many values, including hello following object:</span></span>

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

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="f9351-151">Oczekiwania przed wysłaniem żądania dalej</span><span class="sxs-lookup"><span data-stu-id="f9351-151">Waiting before sending next request</span></span>
<span data-ttu-id="f9351-152">Po osiągnięciu limitu żądań hello Resource Manager zwraca hello **429** kod stanu HTTP i **ponownych prób po** wartość w nagłówku hello.</span><span class="sxs-lookup"><span data-stu-id="f9351-152">When you reach hello request limit, Resource Manager returns hello **429** HTTP status code and a **Retry-After** value in hello header.</span></span> <span data-ttu-id="f9351-153">Witaj **ponownych prób po** wartość określa hello liczbę sekund oczekiwania w aplikacji (lub uśpienia) przed wysłaniem hello następnego żądania.</span><span class="sxs-lookup"><span data-stu-id="f9351-153">hello **Retry-After** value specifies hello number of seconds your application should wait (or sleep) before sending hello next request.</span></span> <span data-ttu-id="f9351-154">Po wysłaniu żądania, przed upływem hello wartość ponownych prób, Twoje żądanie nie jest przetwarzane i nowa wartość ponownych prób jest zwracany.</span><span class="sxs-lookup"><span data-stu-id="f9351-154">If you send a request before hello retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9351-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9351-155">Next steps</span></span>

* <span data-ttu-id="f9351-156">Aby uzyskać więcej informacji na temat limitów i przydziały zobacz [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="f9351-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="f9351-157">toolearn dotyczące obsługi żądań asynchronicznych REST, zobacz [śledzić operacje asynchroniczne Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f9351-157">toolearn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
