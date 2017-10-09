---
title: "zasad buforowania interfejsu API zarządzania aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello buforowanie zasad dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="0e9c6-103">Zarządzanie interfejsami API zasad buforowania</span><span class="sxs-lookup"><span data-stu-id="0e9c6-103">API Management caching policies</span></span>
<span data-ttu-id="0e9c6-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management hello.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="0e9c6-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="0e9c6-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="0e9c6-106"><a name="CachingPolicies"></a>Buforowanie zasad</span><span class="sxs-lookup"><span data-stu-id="0e9c6-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="0e9c6-107">Zasad buforowania odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="0e9c6-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="0e9c6-108">[Pobierz z pamięci podręcznej](api-management-caching-policies.md#GetFromCache) — wykonaj pamięci podręcznej wyszukiwania i zwracać prawidłowy odpowiedzi pamięci podręcznej, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="0e9c6-109">[Przechowywanie toocache](api-management-caching-policies.md#StoreToCache) — zgodnie z konfiguracji kontroli określonego pamięci podręcznej toohello odpowiedzi pamięci podręcznych.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-109">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches responses according toohello specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="0e9c6-110">Wartość zasad buforowania</span><span class="sxs-lookup"><span data-stu-id="0e9c6-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="0e9c6-111">[Pobiera wartość z pamięci podręcznej](#GetFromCacheByKey) -pobrania elementu pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="0e9c6-112">[Przechowywana wartość w pamięci podręcznej](#StoreToCacheByKey) -przechowywania elementu w pamięci podręcznej hello według klucza.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-112">[Store value in cache](#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="0e9c6-113">[Usuń wartość z pamięci podręcznej](#RemoveCacheByKey) -usunięcie elementu w pamięci podręcznej hello według klucza.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
##  <span data-ttu-id="0e9c6-114"><a name="GetFromCache"></a>Pobierz z pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="0e9c6-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="0e9c6-115">Użyj hello `cache-lookup` pamięci podręcznej zasad tooperform strzałki w górę i zwracać prawidłową odpowiedź buforowana, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-115">Use hello `cache-lookup` policy tooperform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="0e9c6-116">Te zasady mogą być stosowane w przypadkach, gdy odpowiedzi zawartość pozostaje statyczna w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="0e9c6-117">Buforowanie odpowiedzi redukuje przepustowość i wymagania dotyczące przetwarzania nałożone na powitania wewnętrznej bazy danych w sieci web serwera i obniża opóźnienia postrzegane przez konsumentów interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-117">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0e9c6-118">Ta zasada musi mieć odpowiednią [toocache magazynu](api-management-caching-policies.md#StoreToCache) zasad.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-118">This policy must have a corresponding [Store toocache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0e9c6-119">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="0e9c6-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a><span data-ttu-id="0e9c6-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="0e9c6-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="0e9c6-121">Przykład</span><span class="sxs-lookup"><span data-stu-id="0e9c6-121">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="0e9c6-122">Przykład za pomocą wyrażeń zasad</span><span class="sxs-lookup"><span data-stu-id="0e9c6-122">Example using policy expressions</span></span>  
 <span data-ttu-id="0e9c6-123">W tym przykładzie pokazano, jak czas trwania, że dopasowań hello buforowanie odpowiedzi usługi zaplecza hello określony przez hello buforowania odpowiedzi interfejsu API zarządzania tootooconfigure kopii usługi `Cache-Control` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-123">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="0e9c6-124">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too25:25.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="0e9c6-125">Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="0e9c6-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="0e9c6-126">Elementy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-126">Elements</span></span>  
  
|<span data-ttu-id="0e9c6-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0e9c6-127">Name</span></span>|<span data-ttu-id="0e9c6-128">Opis</span><span class="sxs-lookup"><span data-stu-id="0e9c6-128">Description</span></span>|<span data-ttu-id="0e9c6-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e9c6-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0e9c6-130">wyszukiwania w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="0e9c6-130">cache-lookup</span></span>|<span data-ttu-id="0e9c6-131">Element główny.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-131">Root element.</span></span>|<span data-ttu-id="0e9c6-132">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-132">Yes</span></span>|  
|<span data-ttu-id="0e9c6-133">różnią się w nagłówku</span><span class="sxs-lookup"><span data-stu-id="0e9c6-133">vary-by-header</span></span>|<span data-ttu-id="0e9c6-134">Rozpoczynają buforowanie odpowiedzi na wartość określony nagłówek Accept, Accept-Charset, Accept-Encoding, Accept-Language autoryzacji, oczekiwania, np. Z hosta i If-Match.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="0e9c6-135">Nie</span><span class="sxs-lookup"><span data-stu-id="0e9c6-135">No</span></span>|  
|<span data-ttu-id="0e9c6-136">różnią się za--parametru zapytania</span><span class="sxs-lookup"><span data-stu-id="0e9c6-136">vary-by-query-parameter</span></span>|<span data-ttu-id="0e9c6-137">Firmy rozpoczynają buforowanie odpowiedzi na wartości parametrów określonego zapytania.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="0e9c6-138">Wprowadź jeden lub wiele parametrów.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="0e9c6-139">Użyj średnika jako separatora.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-139">Use semicolon as a separator.</span></span> <span data-ttu-id="0e9c6-140">Jeśli nie jest określona, używane są wszystkie parametry zapytania.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="0e9c6-141">Nie</span><span class="sxs-lookup"><span data-stu-id="0e9c6-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0e9c6-142">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="0e9c6-142">Attributes</span></span>  
  
|<span data-ttu-id="0e9c6-143">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0e9c6-143">Name</span></span>|<span data-ttu-id="0e9c6-144">Opis</span><span class="sxs-lookup"><span data-stu-id="0e9c6-144">Description</span></span>|<span data-ttu-id="0e9c6-145">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e9c6-145">Required</span></span>|<span data-ttu-id="0e9c6-146">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0e9c6-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0e9c6-147">Zezwalaj na prywatny odpowiedzi buforowania</span><span class="sxs-lookup"><span data-stu-id="0e9c6-147">allow-private-response-caching</span></span>|<span data-ttu-id="0e9c6-148">Gdy ustawiona zbyt`true`, umożliwia buforowanie żądań zawierających nagłówek uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-148">When set too`true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="0e9c6-149">Nie</span><span class="sxs-lookup"><span data-stu-id="0e9c6-149">No</span></span>|<span data-ttu-id="0e9c6-150">wartość false</span><span class="sxs-lookup"><span data-stu-id="0e9c6-150">false</span></span>|  
|<span data-ttu-id="0e9c6-151">typ podrzędny dla buforowania</span><span class="sxs-lookup"><span data-stu-id="0e9c6-151">downstream-caching-type</span></span>|<span data-ttu-id="0e9c6-152">Ten atrybut musi określać tooone hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-152">This attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="0e9c6-153">-none - podrzędne buforowanie jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="0e9c6-154">-prywatny - podrzędne buforowanie prywatnej jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="0e9c6-155">-publiczny - prywatnych i udostępnionych podrzędne buforowanie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="0e9c6-156">Nie</span><span class="sxs-lookup"><span data-stu-id="0e9c6-156">No</span></span>|<span data-ttu-id="0e9c6-157">Brak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-157">none</span></span>|  
|<span data-ttu-id="0e9c6-158">musi revalidate</span><span class="sxs-lookup"><span data-stu-id="0e9c6-158">must-revalidate</span></span>|<span data-ttu-id="0e9c6-159">Gdy włączone jest buforowanie podrzędne tego atrybutu Włącza lub wyłącza hello `must-revalidate` dyrektywy sterowania pamięci podręcznej w odpowiedzi bramy.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-159">When downstream caching is enabled this attribute turns on or off  hello `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="0e9c6-160">Nie</span><span class="sxs-lookup"><span data-stu-id="0e9c6-160">No</span></span>|<span data-ttu-id="0e9c6-161">Wartość true</span><span class="sxs-lookup"><span data-stu-id="0e9c6-161">true</span></span>|  
|<span data-ttu-id="0e9c6-162">różnią się przez dewelopera</span><span class="sxs-lookup"><span data-stu-id="0e9c6-162">vary-by-developer</span></span>|<span data-ttu-id="0e9c6-163">Ustaw zbyt`true` toocache odpowiedzi na klucz developer.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-163">Set too`true` toocache responses per developer key.</span></span>|<span data-ttu-id="0e9c6-164">Nie</span><span class="sxs-lookup"><span data-stu-id="0e9c6-164">No</span></span>|<span data-ttu-id="0e9c6-165">wartość false</span><span class="sxs-lookup"><span data-stu-id="0e9c6-165">false</span></span>|  
|<span data-ttu-id="0e9c6-166">różnią się przez developer grupy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-166">vary-by-developer-groups</span></span>|<span data-ttu-id="0e9c6-167">Ustaw zbyt`true` toocache odpowiedzi dla każdej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-167">Set too`true` toocache responses per user role.</span></span>|<span data-ttu-id="0e9c6-168">Nie</span><span class="sxs-lookup"><span data-stu-id="0e9c6-168">No</span></span>|<span data-ttu-id="0e9c6-169">wartość false</span><span class="sxs-lookup"><span data-stu-id="0e9c6-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0e9c6-170">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="0e9c6-170">Usage</span></span>  
 <span data-ttu-id="0e9c6-171">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="0e9c6-171">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0e9c6-172">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="0e9c6-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="0e9c6-173">**Zakresy zasad:** interfejsu API, działania, produktu</span><span class="sxs-lookup"><span data-stu-id="0e9c6-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="0e9c6-174"><a name="StoreToCache"></a>Toocache magazynu</span><span class="sxs-lookup"><span data-stu-id="0e9c6-174"><a name="StoreToCache"></a> Store toocache</span></span>  
 <span data-ttu-id="0e9c6-175">Witaj `cache-store` odpowiedzi pamięci podręcznej zasad zgodnie z toohello określić ustawienia pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-175">hello `cache-store` policy caches responses according toohello specified cache settings.</span></span> <span data-ttu-id="0e9c6-176">Te zasady mogą być stosowane w przypadkach, gdy odpowiedzi zawartość pozostaje statyczna w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="0e9c6-177">Buforowanie odpowiedzi redukuje przepustowość i wymagania dotyczące przetwarzania nałożone na powitania wewnętrznej bazy danych w sieci web serwera i obniża opóźnienia postrzegane przez konsumentów interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-177">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0e9c6-178">Ta zasada musi mieć odpowiednią [pobrać z pamięci podręcznej](api-management-caching-policies.md#GetFromCache) zasad.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0e9c6-179">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="0e9c6-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="0e9c6-180">Przykłady</span><span class="sxs-lookup"><span data-stu-id="0e9c6-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="0e9c6-181">Przykład</span><span class="sxs-lookup"><span data-stu-id="0e9c6-181">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="0e9c6-182">Przykład za pomocą wyrażeń zasad</span><span class="sxs-lookup"><span data-stu-id="0e9c6-182">Example using policy expressions</span></span>  
 <span data-ttu-id="0e9c6-183">W tym przykładzie pokazano, jak czas trwania, że dopasowań hello buforowanie odpowiedzi usługi zaplecza hello określony przez hello buforowania odpowiedzi interfejsu API zarządzania tootooconfigure kopii usługi `Cache-Control` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-183">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="0e9c6-184">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too25:25.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="0e9c6-185">Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="0e9c6-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="0e9c6-186">Elementy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-186">Elements</span></span>  
  
|<span data-ttu-id="0e9c6-187">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0e9c6-187">Name</span></span>|<span data-ttu-id="0e9c6-188">Opis</span><span class="sxs-lookup"><span data-stu-id="0e9c6-188">Description</span></span>|<span data-ttu-id="0e9c6-189">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e9c6-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0e9c6-190">magazynu pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="0e9c6-190">cache-store</span></span>|<span data-ttu-id="0e9c6-191">Element główny.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-191">Root element.</span></span>|<span data-ttu-id="0e9c6-192">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0e9c6-193">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="0e9c6-193">Attributes</span></span>  
  
|<span data-ttu-id="0e9c6-194">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0e9c6-194">Name</span></span>|<span data-ttu-id="0e9c6-195">Opis</span><span class="sxs-lookup"><span data-stu-id="0e9c6-195">Description</span></span>|<span data-ttu-id="0e9c6-196">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e9c6-196">Required</span></span>|<span data-ttu-id="0e9c6-197">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0e9c6-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0e9c6-198">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="0e9c6-198">duration</span></span>|<span data-ttu-id="0e9c6-199">Czas wygaśnięcia elementu hello buforowane wpisów, określona w sekundach.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-199">Time-to-live of hello cached entries, specified in seconds.</span></span>|<span data-ttu-id="0e9c6-200">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-200">Yes</span></span>|<span data-ttu-id="0e9c6-201">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0e9c6-202">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="0e9c6-202">Usage</span></span>  
 <span data-ttu-id="0e9c6-203">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="0e9c6-203">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0e9c6-204">**Sekcje zasad:** ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="0e9c6-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="0e9c6-205">**Zakresy zasad:** interfejsu API, działania, produktu</span><span class="sxs-lookup"><span data-stu-id="0e9c6-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="0e9c6-206"><a name="GetFromCacheByKey"></a>Pobiera wartość z pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="0e9c6-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="0e9c6-207">Użyj hello `cache-lookup-value` tooperform zasad przez klucz pamięci podręcznej wyszukiwania i zwraca wartość w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-207">Use hello `cache-lookup-value` policy tooperform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="0e9c6-208">klucz Hello może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-208">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0e9c6-209">Ta zasada musi mieć odpowiednią [przechowywana wartość w pamięci podręcznej](#StoreToCacheByKey) zasad.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0e9c6-210">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="0e9c6-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="0e9c6-211">Przykład</span><span class="sxs-lookup"><span data-stu-id="0e9c6-211">Example</span></span>  
 <span data-ttu-id="0e9c6-212">Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [niestandardowych buforowanie w usłudze Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="0e9c6-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="0e9c6-213">Elementy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-213">Elements</span></span>  
  
|<span data-ttu-id="0e9c6-214">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0e9c6-214">Name</span></span>|<span data-ttu-id="0e9c6-215">Opis</span><span class="sxs-lookup"><span data-stu-id="0e9c6-215">Description</span></span>|<span data-ttu-id="0e9c6-216">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e9c6-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0e9c6-217">wartość w pamięci podręcznej wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="0e9c6-217">cache-lookup-value</span></span>|<span data-ttu-id="0e9c6-218">Element główny.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-218">Root element.</span></span>|<span data-ttu-id="0e9c6-219">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0e9c6-220">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="0e9c6-220">Attributes</span></span>  
  
|<span data-ttu-id="0e9c6-221">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0e9c6-221">Name</span></span>|<span data-ttu-id="0e9c6-222">Opis</span><span class="sxs-lookup"><span data-stu-id="0e9c6-222">Description</span></span>|<span data-ttu-id="0e9c6-223">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e9c6-223">Required</span></span>|<span data-ttu-id="0e9c6-224">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0e9c6-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0e9c6-225">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="0e9c6-225">default-value</span></span>|<span data-ttu-id="0e9c6-226">Wartość, która zostanie przypisana zmienna toohello Jeśli wyszukiwanie klucza pamięci podręcznej hello spowodowała nie trafienia.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-226">A value that will be assigned toohello variable if hello cache key lookup resulted in a miss.</span></span> <span data-ttu-id="0e9c6-227">Jeśli ten atrybut nie jest określony, `null` jest przypisany.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="0e9c6-228">Nie</span><span class="sxs-lookup"><span data-stu-id="0e9c6-228">No</span></span>|`null`|  
|<span data-ttu-id="0e9c6-229">key</span><span class="sxs-lookup"><span data-stu-id="0e9c6-229">key</span></span>|<span data-ttu-id="0e9c6-230">Wartość klucza toouse w hello wyszukiwania w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-230">Cache key value toouse in hello lookup.</span></span>|<span data-ttu-id="0e9c6-231">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-231">Yes</span></span>|<span data-ttu-id="0e9c6-232">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-232">N/A</span></span>|  
|<span data-ttu-id="0e9c6-233">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="0e9c6-233">variable-name</span></span>|<span data-ttu-id="0e9c6-234">Nazwa hello [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables) hello przeszukiwać wartość zostanie przypisana do użytkownika, jeśli wyszukiwanie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-234">Name of hello [context variable](api-management-policy-expressions.md#ContextVariables) hello looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="0e9c6-235">Jeśli wyszukiwanie powoduje Chybienie, zmienna hello zostaną przypisane wartości hello hello `default-value` atrybutu lub `null`, jeśli hello `default-value` atrybut nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-235">If lookup results in a miss, hello variable will be assigned hello value of hello `default-value` attribute or `null`, if hello `default-value` attribute is omitted.</span></span>|<span data-ttu-id="0e9c6-236">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-236">Yes</span></span>|<span data-ttu-id="0e9c6-237">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0e9c6-238">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="0e9c6-238">Usage</span></span>  
 <span data-ttu-id="0e9c6-239">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="0e9c6-239">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0e9c6-240">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="0e9c6-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="0e9c6-241">**Zakresy zasad:** globalnych, interfejsu API, działania, produktu</span><span class="sxs-lookup"><span data-stu-id="0e9c6-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="0e9c6-242"><a name="StoreToCacheByKey"></a>Wartość magazynu w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="0e9c6-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="0e9c6-243">Witaj `cache-store-value` wykonuje magazynu pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-243">hello `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="0e9c6-244">klucz Hello może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-244">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0e9c6-245">Ta zasada musi mieć odpowiednią [pobrać wartości z pamięci podręcznej](#GetFromCacheByKey) zasad.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="0e9c6-246">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="0e9c6-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="0e9c6-247">Przykład</span><span class="sxs-lookup"><span data-stu-id="0e9c6-247">Example</span></span>  
 <span data-ttu-id="0e9c6-248">Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [niestandardowych buforowanie w usłudze Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="0e9c6-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="0e9c6-249">Elementy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-249">Elements</span></span>  
  
|<span data-ttu-id="0e9c6-250">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0e9c6-250">Name</span></span>|<span data-ttu-id="0e9c6-251">Opis</span><span class="sxs-lookup"><span data-stu-id="0e9c6-251">Description</span></span>|<span data-ttu-id="0e9c6-252">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e9c6-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0e9c6-253">wartość w przypadku magazynu pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="0e9c6-253">cache-store-value</span></span>|<span data-ttu-id="0e9c6-254">Element główny.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-254">Root element.</span></span>|<span data-ttu-id="0e9c6-255">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="0e9c6-256">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="0e9c6-256">Attributes</span></span>  
  
|<span data-ttu-id="0e9c6-257">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0e9c6-257">Name</span></span>|<span data-ttu-id="0e9c6-258">Opis</span><span class="sxs-lookup"><span data-stu-id="0e9c6-258">Description</span></span>|<span data-ttu-id="0e9c6-259">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e9c6-259">Required</span></span>|<span data-ttu-id="0e9c6-260">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0e9c6-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0e9c6-261">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="0e9c6-261">duration</span></span>|<span data-ttu-id="0e9c6-262">Wartość będą buforowane na powitania podane wartości czasu trwania, określona w sekundach.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-262">Value will be cached for hello provided duration value, specified in seconds.</span></span>|<span data-ttu-id="0e9c6-263">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-263">Yes</span></span>|<span data-ttu-id="0e9c6-264">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-264">N/A</span></span>|  
|<span data-ttu-id="0e9c6-265">key</span><span class="sxs-lookup"><span data-stu-id="0e9c6-265">key</span></span>|<span data-ttu-id="0e9c6-266">Wartość klucza hello pamięci podręcznej będą przechowywane w obszarze.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-266">Cache key hello value will be stored under.</span></span>|<span data-ttu-id="0e9c6-267">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-267">Yes</span></span>|<span data-ttu-id="0e9c6-268">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-268">N/A</span></span>|  
|<span data-ttu-id="0e9c6-269">wartość</span><span class="sxs-lookup"><span data-stu-id="0e9c6-269">value</span></span>|<span data-ttu-id="0e9c6-270">Witaj toobe wartość w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-270">hello value toobe cached.</span></span>|<span data-ttu-id="0e9c6-271">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-271">Yes</span></span>|<span data-ttu-id="0e9c6-272">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="0e9c6-273">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="0e9c6-273">Usage</span></span>  
 <span data-ttu-id="0e9c6-274">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="0e9c6-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="0e9c6-275">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="0e9c6-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="0e9c6-276">**Zakresy zasad:** globalnych, interfejsu API, działania, produktu</span><span class="sxs-lookup"><span data-stu-id="0e9c6-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="0e9c6-277"><a name="RemoveCacheByKey"></a>Usuń wartość z pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="0e9c6-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="0e9c6-278">Witaj `cache-remove-value` usuwa element pamięci podręcznej identyfikowane za pomocą klucza.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-278">hello             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="0e9c6-279">klucz Hello może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-279">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="0e9c6-280">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="0e9c6-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="0e9c6-281">Przykład</span><span class="sxs-lookup"><span data-stu-id="0e9c6-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="0e9c6-282">Elementy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-282">Elements</span></span>  
  
|<span data-ttu-id="0e9c6-283">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0e9c6-283">Name</span></span>|<span data-ttu-id="0e9c6-284">Opis</span><span class="sxs-lookup"><span data-stu-id="0e9c6-284">Description</span></span>|<span data-ttu-id="0e9c6-285">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e9c6-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="0e9c6-286">remove wartość w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="0e9c6-286">cache-remove-value</span></span>|<span data-ttu-id="0e9c6-287">Element główny.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-287">Root element.</span></span>|<span data-ttu-id="0e9c6-288">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="0e9c6-289">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="0e9c6-289">Attributes</span></span>  
  
|<span data-ttu-id="0e9c6-290">Nazwa</span><span class="sxs-lookup"><span data-stu-id="0e9c6-290">Name</span></span>|<span data-ttu-id="0e9c6-291">Opis</span><span class="sxs-lookup"><span data-stu-id="0e9c6-291">Description</span></span>|<span data-ttu-id="0e9c6-292">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0e9c6-292">Required</span></span>|<span data-ttu-id="0e9c6-293">Domyślne</span><span class="sxs-lookup"><span data-stu-id="0e9c6-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="0e9c6-294">key</span><span class="sxs-lookup"><span data-stu-id="0e9c6-294">key</span></span>|<span data-ttu-id="0e9c6-295">klucz Hello hello buforowane wcześniej usuniętych z pamięci podręcznej hello toobe wartość.</span><span class="sxs-lookup"><span data-stu-id="0e9c6-295">hello key of hello previously cached value toobe removed from hello cache.</span></span>|<span data-ttu-id="0e9c6-296">Tak</span><span class="sxs-lookup"><span data-stu-id="0e9c6-296">Yes</span></span>|<span data-ttu-id="0e9c6-297">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="0e9c6-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="0e9c6-298">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="0e9c6-298">Usage</span></span>  
 <span data-ttu-id="0e9c6-299">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="0e9c6-299">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="0e9c6-300">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="0e9c6-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="0e9c6-301">**Zakresy zasad:** globalnych, interfejsu API, działania, produktu</span><span class="sxs-lookup"><span data-stu-id="0e9c6-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="0e9c6-302">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0e9c6-302">Next steps</span></span>
<span data-ttu-id="0e9c6-303">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="0e9c6-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  