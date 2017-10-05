---
title: Azure API Management buforowanie zasad | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat zasad buforowania dostępne do użycia w usłudze Azure API Management."
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
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="f4db5-103">Zarządzanie interfejsami API zasad buforowania</span><span class="sxs-lookup"><span data-stu-id="f4db5-103">API Management caching policies</span></span>
<span data-ttu-id="f4db5-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="f4db5-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="f4db5-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="f4db5-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="f4db5-106"><a name="CachingPolicies"></a>Buforowanie zasad</span><span class="sxs-lookup"><span data-stu-id="f4db5-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="f4db5-107">Zasad buforowania odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f4db5-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="f4db5-108">[Pobierz z pamięci podręcznej](api-management-caching-policies.md#GetFromCache) — wykonaj pamięci podręcznej wyszukiwania i zwracać prawidłowy odpowiedzi pamięci podręcznej, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="f4db5-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="f4db5-109">[Magazynu pamięci podręcznej](api-management-caching-policies.md#StoreToCache) -buforuje odpowiedzi zgodnie z określonym pamięci podręcznej konfiguracji kontroli.</span><span class="sxs-lookup"><span data-stu-id="f4db5-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="f4db5-110">Wartość zasad buforowania</span><span class="sxs-lookup"><span data-stu-id="f4db5-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="f4db5-111">[Pobiera wartość z pamięci podręcznej](#GetFromCacheByKey) -pobrania elementu pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="f4db5-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="f4db5-112">[Przechowywana wartość w pamięci podręcznej](#StoreToCacheByKey) -przechowywania elementu w pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="f4db5-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="f4db5-113">[Usuń wartość z pamięci podręcznej](#RemoveCacheByKey) -usunięcie elementu w pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="f4db5-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <span data-ttu-id="f4db5-114"><a name="GetFromCache"></a>Pobierz z pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f4db5-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="f4db5-115">Użyj `cache-lookup` zasady w celu wykonania pamięci podręcznej wyszukiwania i zwracać prawidłową odpowiedź buforowana, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="f4db5-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="f4db5-116">Te zasady mogą być stosowane w przypadkach, gdy odpowiedzi zawartość pozostaje statyczna w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="f4db5-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="f4db5-117">Buforowanie odpowiedzi redukuje przepustowość i wymagania dotyczące przetwarzania nałożone na opóźnienie serwera i obniża sieci web zaplecza postrzegane przez konsumentów interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f4db5-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f4db5-118">Ta zasada musi mieć odpowiednią [magazynu pamięci podręcznej](api-management-caching-policies.md#StoreToCache) zasad.</span><span class="sxs-lookup"><span data-stu-id="f4db5-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f4db5-119">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="f4db5-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
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
  
### <a name="examples"></a><span data-ttu-id="f4db5-120">Przykłady</span><span class="sxs-lookup"><span data-stu-id="f4db5-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="f4db5-121">Przykład</span><span class="sxs-lookup"><span data-stu-id="f4db5-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="f4db5-122">Przykład za pomocą wyrażeń zasad</span><span class="sxs-lookup"><span data-stu-id="f4db5-122">Example using policy expressions</span></span>  
 <span data-ttu-id="f4db5-123">W tym przykładzie pokazano, jak do konfigurowania czas trwania odpowiadającego buforowanie odpowiedzi usługi wewnętrznej bazy danych jako buforowania odpowiedzi interfejsu API zarządzania określona przez usługę kopii `Cache-Control` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="f4db5-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="f4db5-124">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybkie przewijanie do przodu do 25:25.</span><span class="sxs-lookup"><span data-stu-id="f4db5-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="f4db5-125">Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="f4db5-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="f4db5-126">Elementy</span><span class="sxs-lookup"><span data-stu-id="f4db5-126">Elements</span></span>  
  
|<span data-ttu-id="f4db5-127">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4db5-127">Name</span></span>|<span data-ttu-id="f4db5-128">Opis</span><span class="sxs-lookup"><span data-stu-id="f4db5-128">Description</span></span>|<span data-ttu-id="f4db5-129">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4db5-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f4db5-130">wyszukiwania w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f4db5-130">cache-lookup</span></span>|<span data-ttu-id="f4db5-131">Element główny.</span><span class="sxs-lookup"><span data-stu-id="f4db5-131">Root element.</span></span>|<span data-ttu-id="f4db5-132">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-132">Yes</span></span>|  
|<span data-ttu-id="f4db5-133">różnią się w nagłówku</span><span class="sxs-lookup"><span data-stu-id="f4db5-133">vary-by-header</span></span>|<span data-ttu-id="f4db5-134">Rozpoczynają buforowanie odpowiedzi na wartość określony nagłówek Accept, Accept-Charset, Accept-Encoding, Accept-Language autoryzacji, oczekiwania, np. Z hosta i If-Match.</span><span class="sxs-lookup"><span data-stu-id="f4db5-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="f4db5-135">Nie</span><span class="sxs-lookup"><span data-stu-id="f4db5-135">No</span></span>|  
|<span data-ttu-id="f4db5-136">różnią się za--parametru zapytania</span><span class="sxs-lookup"><span data-stu-id="f4db5-136">vary-by-query-parameter</span></span>|<span data-ttu-id="f4db5-137">Firmy rozpoczynają buforowanie odpowiedzi na wartości parametrów określonego zapytania.</span><span class="sxs-lookup"><span data-stu-id="f4db5-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="f4db5-138">Wprowadź jeden lub wiele parametrów.</span><span class="sxs-lookup"><span data-stu-id="f4db5-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="f4db5-139">Użyj średnika jako separatora.</span><span class="sxs-lookup"><span data-stu-id="f4db5-139">Use semicolon as a separator.</span></span> <span data-ttu-id="f4db5-140">Jeśli nie jest określona, używane są wszystkie parametry zapytania.</span><span class="sxs-lookup"><span data-stu-id="f4db5-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="f4db5-141">Nie</span><span class="sxs-lookup"><span data-stu-id="f4db5-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f4db5-142">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="f4db5-142">Attributes</span></span>  
  
|<span data-ttu-id="f4db5-143">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4db5-143">Name</span></span>|<span data-ttu-id="f4db5-144">Opis</span><span class="sxs-lookup"><span data-stu-id="f4db5-144">Description</span></span>|<span data-ttu-id="f4db5-145">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4db5-145">Required</span></span>|<span data-ttu-id="f4db5-146">Domyślne</span><span class="sxs-lookup"><span data-stu-id="f4db5-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f4db5-147">Zezwalaj na prywatny odpowiedzi buforowania</span><span class="sxs-lookup"><span data-stu-id="f4db5-147">allow-private-response-caching</span></span>|<span data-ttu-id="f4db5-148">Jeśli wartość `true`, umożliwia buforowanie żądań zawierających nagłówek uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="f4db5-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="f4db5-149">Nie</span><span class="sxs-lookup"><span data-stu-id="f4db5-149">No</span></span>|<span data-ttu-id="f4db5-150">wartość false</span><span class="sxs-lookup"><span data-stu-id="f4db5-150">false</span></span>|  
|<span data-ttu-id="f4db5-151">typ podrzędny dla buforowania</span><span class="sxs-lookup"><span data-stu-id="f4db5-151">downstream-caching-type</span></span>|<span data-ttu-id="f4db5-152">Ten atrybut musi mieć ustawioną jedną z następujących wartości.</span><span class="sxs-lookup"><span data-stu-id="f4db5-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="f4db5-153">-none - podrzędne buforowanie jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="f4db5-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="f4db5-154">-prywatny - podrzędne buforowanie prywatnej jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="f4db5-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="f4db5-155">-publiczny - prywatnych i udostępnionych podrzędne buforowanie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="f4db5-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="f4db5-156">Nie</span><span class="sxs-lookup"><span data-stu-id="f4db5-156">No</span></span>|<span data-ttu-id="f4db5-157">Brak</span><span class="sxs-lookup"><span data-stu-id="f4db5-157">none</span></span>|  
|<span data-ttu-id="f4db5-158">musi revalidate</span><span class="sxs-lookup"><span data-stu-id="f4db5-158">must-revalidate</span></span>|<span data-ttu-id="f4db5-159">Gdy włączone jest buforowanie podrzędne tego atrybutu Włącza lub wyłącza `must-revalidate` dyrektywy sterowania pamięci podręcznej w odpowiedzi bramy.</span><span class="sxs-lookup"><span data-stu-id="f4db5-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="f4db5-160">Nie</span><span class="sxs-lookup"><span data-stu-id="f4db5-160">No</span></span>|<span data-ttu-id="f4db5-161">Wartość true</span><span class="sxs-lookup"><span data-stu-id="f4db5-161">true</span></span>|  
|<span data-ttu-id="f4db5-162">różnią się przez dewelopera</span><span class="sxs-lookup"><span data-stu-id="f4db5-162">vary-by-developer</span></span>|<span data-ttu-id="f4db5-163">Ustaw `true` do pamięci podręcznej odpowiedzi na klucz developer.</span><span class="sxs-lookup"><span data-stu-id="f4db5-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="f4db5-164">Nie</span><span class="sxs-lookup"><span data-stu-id="f4db5-164">No</span></span>|<span data-ttu-id="f4db5-165">wartość false</span><span class="sxs-lookup"><span data-stu-id="f4db5-165">false</span></span>|  
|<span data-ttu-id="f4db5-166">różnią się przez developer grupy</span><span class="sxs-lookup"><span data-stu-id="f4db5-166">vary-by-developer-groups</span></span>|<span data-ttu-id="f4db5-167">Ustaw `true` do odpowiedzi z pamięci podręcznej dla każdej roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f4db5-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="f4db5-168">Nie</span><span class="sxs-lookup"><span data-stu-id="f4db5-168">No</span></span>|<span data-ttu-id="f4db5-169">wartość false</span><span class="sxs-lookup"><span data-stu-id="f4db5-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f4db5-170">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="f4db5-170">Usage</span></span>  
 <span data-ttu-id="f4db5-171">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="f4db5-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f4db5-172">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="f4db5-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="f4db5-173">**Zakresy zasad:** interfejsu API, działania, produktu</span><span class="sxs-lookup"><span data-stu-id="f4db5-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="f4db5-174"><a name="StoreToCache"></a>Przechowywanie w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f4db5-174"><a name="StoreToCache"></a> Store to cache</span></span>  
 <span data-ttu-id="f4db5-175">`cache-store` Zasad buforuje odpowiedzi zgodnie z ustawieniami określonego pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f4db5-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="f4db5-176">Te zasady mogą być stosowane w przypadkach, gdy odpowiedzi zawartość pozostaje statyczna w danym okresie czasu.</span><span class="sxs-lookup"><span data-stu-id="f4db5-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="f4db5-177">Buforowanie odpowiedzi redukuje przepustowość i wymagania dotyczące przetwarzania nałożone na opóźnienie serwera i obniża sieci web zaplecza postrzegane przez konsumentów interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f4db5-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f4db5-178">Ta zasada musi mieć odpowiednią [pobrać z pamięci podręcznej](api-management-caching-policies.md#GetFromCache) zasad.</span><span class="sxs-lookup"><span data-stu-id="f4db5-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f4db5-179">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="f4db5-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="f4db5-180">Przykłady</span><span class="sxs-lookup"><span data-stu-id="f4db5-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="f4db5-181">Przykład</span><span class="sxs-lookup"><span data-stu-id="f4db5-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="f4db5-182">Przykład za pomocą wyrażeń zasad</span><span class="sxs-lookup"><span data-stu-id="f4db5-182">Example using policy expressions</span></span>  
 <span data-ttu-id="f4db5-183">W tym przykładzie pokazano, jak do konfigurowania czas trwania odpowiadającego buforowanie odpowiedzi usługi wewnętrznej bazy danych jako buforowania odpowiedzi interfejsu API zarządzania określona przez usługę kopii `Cache-Control` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="f4db5-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="f4db5-184">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybkie przewijanie do przodu do 25:25.</span><span class="sxs-lookup"><span data-stu-id="f4db5-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="f4db5-185">Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="f4db5-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="f4db5-186">Elementy</span><span class="sxs-lookup"><span data-stu-id="f4db5-186">Elements</span></span>  
  
|<span data-ttu-id="f4db5-187">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4db5-187">Name</span></span>|<span data-ttu-id="f4db5-188">Opis</span><span class="sxs-lookup"><span data-stu-id="f4db5-188">Description</span></span>|<span data-ttu-id="f4db5-189">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4db5-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f4db5-190">magazynu pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f4db5-190">cache-store</span></span>|<span data-ttu-id="f4db5-191">Element główny.</span><span class="sxs-lookup"><span data-stu-id="f4db5-191">Root element.</span></span>|<span data-ttu-id="f4db5-192">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f4db5-193">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="f4db5-193">Attributes</span></span>  
  
|<span data-ttu-id="f4db5-194">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4db5-194">Name</span></span>|<span data-ttu-id="f4db5-195">Opis</span><span class="sxs-lookup"><span data-stu-id="f4db5-195">Description</span></span>|<span data-ttu-id="f4db5-196">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4db5-196">Required</span></span>|<span data-ttu-id="f4db5-197">Domyślne</span><span class="sxs-lookup"><span data-stu-id="f4db5-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f4db5-198">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="f4db5-198">duration</span></span>|<span data-ttu-id="f4db5-199">Czas wygaśnięcia wpisów pamięci podręcznej wyrażony w sekundach.</span><span class="sxs-lookup"><span data-stu-id="f4db5-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="f4db5-200">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-200">Yes</span></span>|<span data-ttu-id="f4db5-201">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="f4db5-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f4db5-202">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="f4db5-202">Usage</span></span>  
 <span data-ttu-id="f4db5-203">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="f4db5-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f4db5-204">**Sekcje zasad:** ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="f4db5-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="f4db5-205">**Zakresy zasad:** interfejsu API, działania, produktu</span><span class="sxs-lookup"><span data-stu-id="f4db5-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="f4db5-206"><a name="GetFromCacheByKey"></a>Pobiera wartość z pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f4db5-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="f4db5-207">Użyj `cache-lookup-value` zasad wykonywania wyszukiwania w pamięci podręcznej przez klucz i zwraca wartość w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f4db5-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="f4db5-208">Klucz może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.</span><span class="sxs-lookup"><span data-stu-id="f4db5-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f4db5-209">Ta zasada musi mieć odpowiednią [przechowywana wartość w pamięci podręcznej](#StoreToCacheByKey) zasad.</span><span class="sxs-lookup"><span data-stu-id="f4db5-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f4db5-210">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="f4db5-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="f4db5-211">Przykład</span><span class="sxs-lookup"><span data-stu-id="f4db5-211">Example</span></span>  
 <span data-ttu-id="f4db5-212">Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [niestandardowych buforowanie w usłudze Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="f4db5-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="f4db5-213">Elementy</span><span class="sxs-lookup"><span data-stu-id="f4db5-213">Elements</span></span>  
  
|<span data-ttu-id="f4db5-214">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4db5-214">Name</span></span>|<span data-ttu-id="f4db5-215">Opis</span><span class="sxs-lookup"><span data-stu-id="f4db5-215">Description</span></span>|<span data-ttu-id="f4db5-216">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4db5-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f4db5-217">wartość w pamięci podręcznej wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="f4db5-217">cache-lookup-value</span></span>|<span data-ttu-id="f4db5-218">Element główny.</span><span class="sxs-lookup"><span data-stu-id="f4db5-218">Root element.</span></span>|<span data-ttu-id="f4db5-219">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f4db5-220">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="f4db5-220">Attributes</span></span>  
  
|<span data-ttu-id="f4db5-221">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4db5-221">Name</span></span>|<span data-ttu-id="f4db5-222">Opis</span><span class="sxs-lookup"><span data-stu-id="f4db5-222">Description</span></span>|<span data-ttu-id="f4db5-223">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4db5-223">Required</span></span>|<span data-ttu-id="f4db5-224">Domyślne</span><span class="sxs-lookup"><span data-stu-id="f4db5-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f4db5-225">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="f4db5-225">default-value</span></span>|<span data-ttu-id="f4db5-226">Chybienia w wyniku wartość, która zostanie przypisana do zmiennej Jeśli wyszukiwanie klucza pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f4db5-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="f4db5-227">Jeśli ten atrybut nie jest określony, `null` jest przypisany.</span><span class="sxs-lookup"><span data-stu-id="f4db5-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="f4db5-228">Nie</span><span class="sxs-lookup"><span data-stu-id="f4db5-228">No</span></span>|`null`|  
|<span data-ttu-id="f4db5-229">key</span><span class="sxs-lookup"><span data-stu-id="f4db5-229">key</span></span>|<span data-ttu-id="f4db5-230">Wartość klucza do użycia w polu wyszukiwania w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f4db5-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="f4db5-231">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-231">Yes</span></span>|<span data-ttu-id="f4db5-232">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="f4db5-232">N/A</span></span>|  
|<span data-ttu-id="f4db5-233">Nazwa zmiennej</span><span class="sxs-lookup"><span data-stu-id="f4db5-233">variable-name</span></span>|<span data-ttu-id="f4db5-234">Nazwa [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables) looked się wartość zostanie przypisana do użytkownika, jeśli wyszukiwanie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="f4db5-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="f4db5-235">Jeśli wyszukiwanie powoduje Chybienie, zmienna zostanie przypisana wartość `default-value` atrybutu lub `null`, jeśli `default-value` atrybut nie jest określony.</span><span class="sxs-lookup"><span data-stu-id="f4db5-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="f4db5-236">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-236">Yes</span></span>|<span data-ttu-id="f4db5-237">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="f4db5-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f4db5-238">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="f4db5-238">Usage</span></span>  
 <span data-ttu-id="f4db5-239">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="f4db5-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f4db5-240">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="f4db5-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="f4db5-241">**Zakresy zasad:** globalnych, interfejsu API, działania, produktu</span><span class="sxs-lookup"><span data-stu-id="f4db5-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="f4db5-242"><a name="StoreToCacheByKey"></a>Wartość magazynu w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f4db5-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="f4db5-243">`cache-store-value` Wykonuje magazynu pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="f4db5-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="f4db5-244">Klucz może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.</span><span class="sxs-lookup"><span data-stu-id="f4db5-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="f4db5-245">Ta zasada musi mieć odpowiednią [pobrać wartości z pamięci podręcznej](#GetFromCacheByKey) zasad.</span><span class="sxs-lookup"><span data-stu-id="f4db5-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="f4db5-246">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="f4db5-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="f4db5-247">Przykład</span><span class="sxs-lookup"><span data-stu-id="f4db5-247">Example</span></span>  
 <span data-ttu-id="f4db5-248">Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [niestandardowych buforowanie w usłudze Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="f4db5-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="f4db5-249">Elementy</span><span class="sxs-lookup"><span data-stu-id="f4db5-249">Elements</span></span>  
  
|<span data-ttu-id="f4db5-250">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4db5-250">Name</span></span>|<span data-ttu-id="f4db5-251">Opis</span><span class="sxs-lookup"><span data-stu-id="f4db5-251">Description</span></span>|<span data-ttu-id="f4db5-252">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4db5-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f4db5-253">wartość w przypadku magazynu pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f4db5-253">cache-store-value</span></span>|<span data-ttu-id="f4db5-254">Element główny.</span><span class="sxs-lookup"><span data-stu-id="f4db5-254">Root element.</span></span>|<span data-ttu-id="f4db5-255">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="f4db5-256">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="f4db5-256">Attributes</span></span>  
  
|<span data-ttu-id="f4db5-257">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4db5-257">Name</span></span>|<span data-ttu-id="f4db5-258">Opis</span><span class="sxs-lookup"><span data-stu-id="f4db5-258">Description</span></span>|<span data-ttu-id="f4db5-259">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4db5-259">Required</span></span>|<span data-ttu-id="f4db5-260">Domyślne</span><span class="sxs-lookup"><span data-stu-id="f4db5-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f4db5-261">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="f4db5-261">duration</span></span>|<span data-ttu-id="f4db5-262">Wartość będą buforowane przez podany czas trwania wybrana, w sekundach.</span><span class="sxs-lookup"><span data-stu-id="f4db5-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="f4db5-263">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-263">Yes</span></span>|<span data-ttu-id="f4db5-264">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="f4db5-264">N/A</span></span>|  
|<span data-ttu-id="f4db5-265">key</span><span class="sxs-lookup"><span data-stu-id="f4db5-265">key</span></span>|<span data-ttu-id="f4db5-266">W obszarze będzie przechowywany klucz pamięci podręcznej wartość.</span><span class="sxs-lookup"><span data-stu-id="f4db5-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="f4db5-267">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-267">Yes</span></span>|<span data-ttu-id="f4db5-268">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="f4db5-268">N/A</span></span>|  
|<span data-ttu-id="f4db5-269">wartość</span><span class="sxs-lookup"><span data-stu-id="f4db5-269">value</span></span>|<span data-ttu-id="f4db5-270">Wartość w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f4db5-270">The value to be cached.</span></span>|<span data-ttu-id="f4db5-271">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-271">Yes</span></span>|<span data-ttu-id="f4db5-272">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="f4db5-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="f4db5-273">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="f4db5-273">Usage</span></span>  
 <span data-ttu-id="f4db5-274">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="f4db5-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="f4db5-275">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="f4db5-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="f4db5-276">**Zakresy zasad:** globalnych, interfejsu API, działania, produktu</span><span class="sxs-lookup"><span data-stu-id="f4db5-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="f4db5-277"><a name="RemoveCacheByKey"></a>Usuń wartość z pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f4db5-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="f4db5-278">`cache-remove-value` Usuwa element pamięci podręcznej identyfikowane za pomocą klucza.</span><span class="sxs-lookup"><span data-stu-id="f4db5-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="f4db5-279">Klucz może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.</span><span class="sxs-lookup"><span data-stu-id="f4db5-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="f4db5-280">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="f4db5-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="f4db5-281">Przykład</span><span class="sxs-lookup"><span data-stu-id="f4db5-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="f4db5-282">Elementy</span><span class="sxs-lookup"><span data-stu-id="f4db5-282">Elements</span></span>  
  
|<span data-ttu-id="f4db5-283">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4db5-283">Name</span></span>|<span data-ttu-id="f4db5-284">Opis</span><span class="sxs-lookup"><span data-stu-id="f4db5-284">Description</span></span>|<span data-ttu-id="f4db5-285">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4db5-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="f4db5-286">remove wartość w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f4db5-286">cache-remove-value</span></span>|<span data-ttu-id="f4db5-287">Element główny.</span><span class="sxs-lookup"><span data-stu-id="f4db5-287">Root element.</span></span>|<span data-ttu-id="f4db5-288">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="f4db5-289">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="f4db5-289">Attributes</span></span>  
  
|<span data-ttu-id="f4db5-290">Nazwa</span><span class="sxs-lookup"><span data-stu-id="f4db5-290">Name</span></span>|<span data-ttu-id="f4db5-291">Opis</span><span class="sxs-lookup"><span data-stu-id="f4db5-291">Description</span></span>|<span data-ttu-id="f4db5-292">Wymagane</span><span class="sxs-lookup"><span data-stu-id="f4db5-292">Required</span></span>|<span data-ttu-id="f4db5-293">Domyślne</span><span class="sxs-lookup"><span data-stu-id="f4db5-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="f4db5-294">key</span><span class="sxs-lookup"><span data-stu-id="f4db5-294">key</span></span>|<span data-ttu-id="f4db5-295">Klucz buforowanych wartość ma zostać usunięty z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f4db5-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="f4db5-296">Tak</span><span class="sxs-lookup"><span data-stu-id="f4db5-296">Yes</span></span>|<span data-ttu-id="f4db5-297">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="f4db5-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="f4db5-298">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="f4db5-298">Usage</span></span>  
 <span data-ttu-id="f4db5-299">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="f4db5-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="f4db5-300">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="f4db5-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="f4db5-301">**Zakresy zasad:** globalnych, interfejsu API, działania, produktu</span><span class="sxs-lookup"><span data-stu-id="f4db5-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="f4db5-302">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f4db5-302">Next steps</span></span>
<span data-ttu-id="f4db5-303">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f4db5-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  