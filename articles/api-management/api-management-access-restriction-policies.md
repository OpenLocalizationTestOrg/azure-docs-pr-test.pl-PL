---
title: "zasady ograniczeń dostępu do interfejsu API zarządzania aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad ograniczeń dostępu hello dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="96493-103">Zasady ograniczeń dostępu do interfejsu API zarządzania</span><span class="sxs-lookup"><span data-stu-id="96493-103">API Management access restriction policies</span></span>
<span data-ttu-id="96493-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management hello.</span><span class="sxs-lookup"><span data-stu-id="96493-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="96493-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="96493-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="96493-106"><a name="AccessRestrictionPolicies"></a>Zasady ograniczeń dostępu</span><span class="sxs-lookup"><span data-stu-id="96493-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="96493-107">[Nagłówek HTTP wyboru](api-management-access-restriction-policies.md#CheckHTTPHeader) — wymusza istnienia i/lub wartość nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="96493-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="96493-108">[Limit szybkości wywołanie przez subskrypcji](api-management-access-restriction-policies.md#LimitCallRate) — użycie uniemożliwia API wzrósł poprzez ograniczenie wywołań szybkości, na podstawie subskrypcji na.</span><span class="sxs-lookup"><span data-stu-id="96493-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="96493-109">[Limit szybkości wywołanie przez klucz](#LimitCallRateByKey) — użycie uniemożliwia API wzrósł ograniczając szybkość połączenia, na podstawie na klucz.</span><span class="sxs-lookup"><span data-stu-id="96493-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="96493-110">[Ograniczenia adresów IP wywołującego](api-management-access-restriction-policies.md#RestrictCallerIPs) -wywołania filtrów (umożliwia/nie zezwala na) z określonych adresów IP i/lub zakresów adresów.</span><span class="sxs-lookup"><span data-stu-id="96493-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="96493-111">[Przydział użycia zestawu subskrypcji](api-management-access-restriction-policies.md#SetUsageQuota) — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="96493-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="96493-112">[Przydział użycia zestawu przez klucz](#SetUsageQuotaByKey) — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie według klucza.</span><span class="sxs-lookup"><span data-stu-id="96493-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="96493-113">[Sprawdź poprawność JWT](api-management-access-restriction-policies.md#ValidateJWT) — wymusza istnienia i ważności wyodrębniony z określonego nagłówka HTTP lub parametr zapytania określony token JWT.</span><span class="sxs-lookup"><span data-stu-id="96493-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="96493-114"><a name="CheckHTTPHeader"></a>Sprawdź nagłówka HTTP</span><span class="sxs-lookup"><span data-stu-id="96493-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="96493-115">Użyj hello `check-header` tooenforce zasady, czy żądanie ma określonego nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="96493-115">Use hello `check-header` policy tooenforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="96493-116">Opcjonalnie można sprawdzić toosee, jeśli nagłówek hello ma określoną wartość lub sprawdź, czy zakres wartości dozwolonych.</span><span class="sxs-lookup"><span data-stu-id="96493-116">You can optionally check toosee if hello header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="96493-117">W przypadku niepowodzenia sprawdzania hello zasad hello kończy przetwarzanie żądań i zwraca hello komunikat stanu HTTP kodu i błąd określone przez zasady hello.</span><span class="sxs-lookup"><span data-stu-id="96493-117">If hello check fails, hello policy terminates request processing and returns hello HTTP status code and error message specified by hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="96493-118">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="96493-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="96493-119">Przykład</span><span class="sxs-lookup"><span data-stu-id="96493-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="96493-120">Elementy</span><span class="sxs-lookup"><span data-stu-id="96493-120">Elements</span></span>  
  
|<span data-ttu-id="96493-121">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-121">Name</span></span>|<span data-ttu-id="96493-122">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-122">Description</span></span>|<span data-ttu-id="96493-123">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="96493-124">Sprawdź — nagłówek</span><span class="sxs-lookup"><span data-stu-id="96493-124">check-header</span></span>|<span data-ttu-id="96493-125">Element główny.</span><span class="sxs-lookup"><span data-stu-id="96493-125">Root element.</span></span>|<span data-ttu-id="96493-126">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-126">Yes</span></span>|  
|<span data-ttu-id="96493-127">wartość</span><span class="sxs-lookup"><span data-stu-id="96493-127">value</span></span>|<span data-ttu-id="96493-128">Dozwolone wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="96493-128">Allowed HTTP header value.</span></span> <span data-ttu-id="96493-129">Jeśli wiele elementów wartości są określone, wyboru hello jest uznawany sukcesu, jeśli jedno hello wartości są zgodne.</span><span class="sxs-lookup"><span data-stu-id="96493-129">When multiple value elements are specified, hello check is considered a success if any one of hello values is a match.</span></span>|<span data-ttu-id="96493-130">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="96493-131">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="96493-131">Attributes</span></span>  
  
|<span data-ttu-id="96493-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-132">Name</span></span>|<span data-ttu-id="96493-133">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-133">Description</span></span>|<span data-ttu-id="96493-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-134">Required</span></span>|<span data-ttu-id="96493-135">Domyślne</span><span class="sxs-lookup"><span data-stu-id="96493-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="96493-136">nie powiodło się wyboru komunikatów o błędach</span><span class="sxs-lookup"><span data-stu-id="96493-136">failed-check-error-message</span></span>|<span data-ttu-id="96493-137">Błąd tooreturn wiadomość w treści odpowiedzi hello HTTP, jeśli nagłówek hello nie istnieje lub ma nieprawidłową wartość.</span><span class="sxs-lookup"><span data-stu-id="96493-137">Error message tooreturn in hello HTTP response body if hello header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="96493-138">Ta wiadomość musi mieć żadnych znaków specjalnych prawidłowo wpisywany.</span><span class="sxs-lookup"><span data-stu-id="96493-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="96493-139">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-139">Yes</span></span>|<span data-ttu-id="96493-140">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-140">N/A</span></span>|  
|<span data-ttu-id="96493-141">nie powiodło się wyboru httpcode</span><span class="sxs-lookup"><span data-stu-id="96493-141">failed-check-httpcode</span></span>|<span data-ttu-id="96493-142">Tooreturn kod stanu HTTP, jeśli nagłówek hello nie istnieje lub ma nieprawidłową wartość.</span><span class="sxs-lookup"><span data-stu-id="96493-142">HTTP Status code tooreturn if hello header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="96493-143">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-143">Yes</span></span>|<span data-ttu-id="96493-144">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-144">N/A</span></span>|  
|<span data-ttu-id="96493-145">Nazwa nagłówka</span><span class="sxs-lookup"><span data-stu-id="96493-145">header-name</span></span>|<span data-ttu-id="96493-146">Nazwa Hello hello toocheck nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="96493-146">hello name of hello HTTP Header toocheck.</span></span>|<span data-ttu-id="96493-147">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-147">Yes</span></span>|<span data-ttu-id="96493-148">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-148">N/A</span></span>|  
|<span data-ttu-id="96493-149">Ignoruj case</span><span class="sxs-lookup"><span data-stu-id="96493-149">ignore-case</span></span>|<span data-ttu-id="96493-150">Można ustawić tooTrue, lub FAŁSZ.</span><span class="sxs-lookup"><span data-stu-id="96493-150">Can be set tooTrue or False.</span></span> <span data-ttu-id="96493-151">Jeśli zestaw tooTrue w wielkość liter jest ignorowana, gdy wartość nagłówka hello jest porównywana hello zbiór dopuszczalnych wartości.</span><span class="sxs-lookup"><span data-stu-id="96493-151">If set tooTrue case is ignored when hello header value is compared against hello set of acceptable values.</span></span>|<span data-ttu-id="96493-152">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-152">Yes</span></span>|<span data-ttu-id="96493-153">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="96493-154">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="96493-154">Usage</span></span>  
 <span data-ttu-id="96493-155">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="96493-155">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="96493-156">**Sekcje zasad:** przychodzące, wychodzące</span><span class="sxs-lookup"><span data-stu-id="96493-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="96493-157">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="96493-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="96493-158"><a name="LimitCallRate"></a>Limit szybkości wywołanie przez subskrypcję</span><span class="sxs-lookup"><span data-stu-id="96493-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="96493-159">Witaj `rate-limit` zasad uniemożliwia użycie API nagłego na podstawie subskrypcji na ograniczając hello wywołać tooa szybkość określony numer na określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="96493-159">hello `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="96493-160">Po wyzwoleniu tych zasad wywołującego hello odbiera `429 Too Many Requests` kod stanu odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="96493-160">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="96493-161">Te zasady mogą być użyte tylko raz na dokument zasad.</span><span class="sxs-lookup"><span data-stu-id="96493-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="96493-162">[Wyrażenie zasad](api-management-policy-expressions.md) nie można użyć w żadnym hello atrybuty zasady dla tych zasad.</span><span class="sxs-lookup"><span data-stu-id="96493-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="96493-163">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="96493-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="96493-164">Przykład</span><span class="sxs-lookup"><span data-stu-id="96493-164">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="96493-165">Elementy</span><span class="sxs-lookup"><span data-stu-id="96493-165">Elements</span></span>  
  
|<span data-ttu-id="96493-166">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-166">Name</span></span>|<span data-ttu-id="96493-167">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-167">Description</span></span>|<span data-ttu-id="96493-168">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="96493-169">Ustaw limit</span><span class="sxs-lookup"><span data-stu-id="96493-169">set-limit</span></span>|<span data-ttu-id="96493-170">Element główny.</span><span class="sxs-lookup"><span data-stu-id="96493-170">Root element.</span></span>|<span data-ttu-id="96493-171">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-171">Yes</span></span>|  
|<span data-ttu-id="96493-172">api</span><span class="sxs-lookup"><span data-stu-id="96493-172">api</span></span>|<span data-ttu-id="96493-173">Dodaj co najmniej jednego z tych elementów tooimpose limit szybkości wywołanie w interfejsach API w ramach produktu hello.</span><span class="sxs-lookup"><span data-stu-id="96493-173">Add one  or more of these elements tooimpose a call rate limit on APIs within hello product.</span></span> <span data-ttu-id="96493-174">Produktu i interfejsu API wywołać szybkość, z jaką ograniczenia są stosowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="96493-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="96493-175">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-175">No</span></span>|  
|<span data-ttu-id="96493-176">Operacja</span><span class="sxs-lookup"><span data-stu-id="96493-176">operation</span></span>|<span data-ttu-id="96493-177">Dodaj co najmniej jednego z tych elementów tooimpose limit szybkości wywołania na operacje w interfejsie API.</span><span class="sxs-lookup"><span data-stu-id="96493-177">Add one  or more of these elements tooimpose a call rate limit on operations within an API.</span></span> <span data-ttu-id="96493-178">Produkt, interfejsu API i operacji należy wywołać szybkość, z jaką ograniczenia są stosowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="96493-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="96493-179">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="96493-180">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="96493-180">Attributes</span></span>  
  
|<span data-ttu-id="96493-181">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-181">Name</span></span>|<span data-ttu-id="96493-182">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-182">Description</span></span>|<span data-ttu-id="96493-183">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-183">Required</span></span>|<span data-ttu-id="96493-184">Domyślne</span><span class="sxs-lookup"><span data-stu-id="96493-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="96493-185">name</span><span class="sxs-lookup"><span data-stu-id="96493-185">name</span></span>|<span data-ttu-id="96493-186">Witaj nazwa hello interfejsu API dla których limit szybkości hello tooapply.</span><span class="sxs-lookup"><span data-stu-id="96493-186">hello name of hello API for which tooapply hello rate limit.</span></span>|<span data-ttu-id="96493-187">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-187">Yes</span></span>|<span data-ttu-id="96493-188">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-188">N/A</span></span>|  
|<span data-ttu-id="96493-189">wywołania</span><span class="sxs-lookup"><span data-stu-id="96493-189">calls</span></span>|<span data-ttu-id="96493-190">Maksymalna całkowita liczba połączeń dozwolona interwale hello określone w hello Hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="96493-190">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="96493-191">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-191">Yes</span></span>|<span data-ttu-id="96493-192">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-192">N/A</span></span>|  
|<span data-ttu-id="96493-193">okres odnawiania</span><span class="sxs-lookup"><span data-stu-id="96493-193">renewal-period</span></span>|<span data-ttu-id="96493-194">czas w sekundach, po których hello przydziału resetuje Hello.</span><span class="sxs-lookup"><span data-stu-id="96493-194">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="96493-195">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-195">Yes</span></span>|<span data-ttu-id="96493-196">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="96493-197">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="96493-197">Usage</span></span>  
 <span data-ttu-id="96493-198">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="96493-198">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="96493-199">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="96493-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="96493-200">**Zakresy zasad:** produktu</span><span class="sxs-lookup"><span data-stu-id="96493-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="96493-201"><a name="LimitCallRateByKey"></a>Limit szybkości wywołanie przez klucz</span><span class="sxs-lookup"><span data-stu-id="96493-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="96493-202">Witaj `rate-limit-by-key` zasad uniemożliwia użycie API nagłego na podstawie na klucz, ograniczając hello wywołać tooa szybkość określony numer na określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="96493-202">hello `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="96493-203">klucz Hello może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.</span><span class="sxs-lookup"><span data-stu-id="96493-203">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="96493-204">Toospecify żądaniach powinno być liczone się limitu hello można dodać warunku opcjonalnie przyrostu.</span><span class="sxs-lookup"><span data-stu-id="96493-204">Optional increment condition can be added toospecify which requests should be counted towards hello limit.</span></span> <span data-ttu-id="96493-205">Po wyzwoleniu tych zasad wywołującego hello odbiera `429 Too Many Requests` kod stanu odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="96493-205">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="96493-206">Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [Zaawansowane żądanie ograniczania z usługą Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="96493-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="96493-207">Te zasady mogą być użyte tylko raz na dokument zasad.</span><span class="sxs-lookup"><span data-stu-id="96493-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="96493-208">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="96493-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="96493-209">Przykład</span><span class="sxs-lookup"><span data-stu-id="96493-209">Example</span></span>  
 <span data-ttu-id="96493-210">W hello poniższy przykład limit szybkości hello jest kluczem według adresu IP hello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="96493-210">In hello following example, hello rate limit is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="96493-211">Elementy</span><span class="sxs-lookup"><span data-stu-id="96493-211">Elements</span></span>  
  
|<span data-ttu-id="96493-212">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-212">Name</span></span>|<span data-ttu-id="96493-213">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-213">Description</span></span>|<span data-ttu-id="96493-214">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="96493-215">Ustaw limit</span><span class="sxs-lookup"><span data-stu-id="96493-215">set-limit</span></span>|<span data-ttu-id="96493-216">Element główny.</span><span class="sxs-lookup"><span data-stu-id="96493-216">Root element.</span></span>|<span data-ttu-id="96493-217">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="96493-218">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="96493-218">Attributes</span></span>  
  
|<span data-ttu-id="96493-219">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-219">Name</span></span>|<span data-ttu-id="96493-220">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-220">Description</span></span>|<span data-ttu-id="96493-221">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-221">Required</span></span>|<span data-ttu-id="96493-222">Domyślne</span><span class="sxs-lookup"><span data-stu-id="96493-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="96493-223">wywołania</span><span class="sxs-lookup"><span data-stu-id="96493-223">calls</span></span>|<span data-ttu-id="96493-224">Maksymalna całkowita liczba połączeń dozwolona interwale hello określone w hello Hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="96493-224">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="96493-225">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-225">Yes</span></span>|<span data-ttu-id="96493-226">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-226">N/A</span></span>|  
|<span data-ttu-id="96493-227">klucz liczników</span><span class="sxs-lookup"><span data-stu-id="96493-227">counter-key</span></span>|<span data-ttu-id="96493-228">Witaj toouse klucza dla zasad limitu szybkości hello.</span><span class="sxs-lookup"><span data-stu-id="96493-228">hello key toouse for hello rate limit policy.</span></span>|<span data-ttu-id="96493-229">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-229">Yes</span></span>|<span data-ttu-id="96493-230">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-230">N/A</span></span>|  
|<span data-ttu-id="96493-231">Stan przyrostowy</span><span class="sxs-lookup"><span data-stu-id="96493-231">increment-condition</span></span>|<span data-ttu-id="96493-232">wyrażenie warunkowe Hello określenie, czy hello żądanie powinno być liczone kierunku hello przydziału (`true`).</span><span class="sxs-lookup"><span data-stu-id="96493-232">hello boolean expression specifying if hello request should be counted towards hello quota (`true`).</span></span>|<span data-ttu-id="96493-233">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-233">No</span></span>|<span data-ttu-id="96493-234">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-234">N/A</span></span>|  
|<span data-ttu-id="96493-235">okres odnawiania</span><span class="sxs-lookup"><span data-stu-id="96493-235">renewal-period</span></span>|<span data-ttu-id="96493-236">czas w sekundach, po których hello przydziału resetuje Hello.</span><span class="sxs-lookup"><span data-stu-id="96493-236">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="96493-237">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-237">Yes</span></span>|<span data-ttu-id="96493-238">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="96493-239">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="96493-239">Usage</span></span>  
 <span data-ttu-id="96493-240">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="96493-240">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="96493-241">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="96493-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="96493-242">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="96493-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="96493-243"><a name="RestrictCallerIPs"></a>Ograniczenia adresów IP wywołującego</span><span class="sxs-lookup"><span data-stu-id="96493-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="96493-244">Witaj `ip-filter` (umożliwia/nie zezwala na) wywołania z określonych adresów IP i/lub zakresów adresów filtry zasad.</span><span class="sxs-lookup"><span data-stu-id="96493-244">hello `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="96493-245">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="96493-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="96493-246">Przykład</span><span class="sxs-lookup"><span data-stu-id="96493-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="96493-247">Elementy</span><span class="sxs-lookup"><span data-stu-id="96493-247">Elements</span></span>  
  
|<span data-ttu-id="96493-248">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-248">Name</span></span>|<span data-ttu-id="96493-249">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-249">Description</span></span>|<span data-ttu-id="96493-250">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="96493-251">Filtr IP</span><span class="sxs-lookup"><span data-stu-id="96493-251">ip-filter</span></span>|<span data-ttu-id="96493-252">Element główny.</span><span class="sxs-lookup"><span data-stu-id="96493-252">Root element.</span></span>|<span data-ttu-id="96493-253">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-253">Yes</span></span>|  
|<span data-ttu-id="96493-254">Adres</span><span class="sxs-lookup"><span data-stu-id="96493-254">address</span></span>|<span data-ttu-id="96493-255">Określa pojedynczy adres IP, na których toofilter.</span><span class="sxs-lookup"><span data-stu-id="96493-255">Specifies a single IP address on which toofilter.</span></span>|<span data-ttu-id="96493-256">Co najmniej jeden `address` lub `address-range` element jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="96493-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="96493-257">zakres adresów z = "address" Aby = "address"</span><span class="sxs-lookup"><span data-stu-id="96493-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="96493-258">Określa adres zakresu adresów IP, na których toofilter.</span><span class="sxs-lookup"><span data-stu-id="96493-258">Specifies a range of IP address on which toofilter.</span></span>|<span data-ttu-id="96493-259">Co najmniej jeden `address` lub `address-range` element jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="96493-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="96493-260">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="96493-260">Attributes</span></span>  
  
|<span data-ttu-id="96493-261">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-261">Name</span></span>|<span data-ttu-id="96493-262">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-262">Description</span></span>|<span data-ttu-id="96493-263">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-263">Required</span></span>|<span data-ttu-id="96493-264">Domyślne</span><span class="sxs-lookup"><span data-stu-id="96493-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="96493-265">zakres adresów z = "address" Aby = "address"</span><span class="sxs-lookup"><span data-stu-id="96493-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="96493-266">Zakres IP adresów tooallow lub odmówić dostępu.</span><span class="sxs-lookup"><span data-stu-id="96493-266">A range of IP addresses tooallow or deny access for.</span></span>|<span data-ttu-id="96493-267">Wymagana, gdy hello `address-range` element jest używany.</span><span class="sxs-lookup"><span data-stu-id="96493-267">Required when hello `address-range` element is used.</span></span>|<span data-ttu-id="96493-268">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-268">N/A</span></span>|  
|<span data-ttu-id="96493-269">Filtr IP akcji = "Zezwalaj na &#124; zabraniać"</span><span class="sxs-lookup"><span data-stu-id="96493-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="96493-270">Określa, czy powinno być dozwolone lub nie dla hello określonych adresów IP i zakresów.</span><span class="sxs-lookup"><span data-stu-id="96493-270">Specifies whether calls should be allowed or not for hello specified IP addresses and ranges.</span></span>|<span data-ttu-id="96493-271">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-271">Yes</span></span>|<span data-ttu-id="96493-272">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="96493-273">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="96493-273">Usage</span></span>  
 <span data-ttu-id="96493-274">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="96493-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="96493-275">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="96493-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="96493-276">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="96493-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="96493-277"><a name="SetUsageQuota"></a>Ustaw przydział użycia przez subskrypcję</span><span class="sxs-lookup"><span data-stu-id="96493-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="96493-278">Witaj `quota` zasady wymuszają zastosowanie odnawialnymi lub okres istnienia wywołania woluminu i/lub przepustowości limit przydziału, na podstawie na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="96493-278">hello `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="96493-279">Te zasady mogą być użyte tylko raz na dokument zasad.</span><span class="sxs-lookup"><span data-stu-id="96493-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="96493-280">[Wyrażenie zasad](api-management-policy-expressions.md) nie można użyć w żadnym hello atrybuty zasady dla tych zasad.</span><span class="sxs-lookup"><span data-stu-id="96493-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="96493-281">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="96493-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="96493-282">Przykład</span><span class="sxs-lookup"><span data-stu-id="96493-282">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="96493-283">Elementy</span><span class="sxs-lookup"><span data-stu-id="96493-283">Elements</span></span>  
  
|<span data-ttu-id="96493-284">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-284">Name</span></span>|<span data-ttu-id="96493-285">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-285">Description</span></span>|<span data-ttu-id="96493-286">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="96493-287">limit przydziału</span><span class="sxs-lookup"><span data-stu-id="96493-287">quota</span></span>|<span data-ttu-id="96493-288">Element główny.</span><span class="sxs-lookup"><span data-stu-id="96493-288">Root element.</span></span>|<span data-ttu-id="96493-289">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-289">Yes</span></span>|  
|<span data-ttu-id="96493-290">api</span><span class="sxs-lookup"><span data-stu-id="96493-290">api</span></span>|<span data-ttu-id="96493-291">Dodaj co najmniej jednego z tych elementów tooimpose limit przydziału w ramach produktu hello w interfejsach API.</span><span class="sxs-lookup"><span data-stu-id="96493-291">Add one  or more of these elements tooimpose a quota on APIs within hello product.</span></span> <span data-ttu-id="96493-292">Przydziały produktu i interfejsu API są stosowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="96493-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="96493-293">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-293">No</span></span>|  
|<span data-ttu-id="96493-294">Operacja</span><span class="sxs-lookup"><span data-stu-id="96493-294">operation</span></span>|<span data-ttu-id="96493-295">Dodaj co najmniej jednego z tych elementów tooimpose limit przydziału na operacje w interfejsie API.</span><span class="sxs-lookup"><span data-stu-id="96493-295">Add one  or more of these elements tooimpose a quota on operations within an API.</span></span> <span data-ttu-id="96493-296">Przydziały produktu, interfejsu API i operacji są stosowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="96493-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="96493-297">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="96493-298">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="96493-298">Attributes</span></span>  
  
|<span data-ttu-id="96493-299">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-299">Name</span></span>|<span data-ttu-id="96493-300">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-300">Description</span></span>|<span data-ttu-id="96493-301">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-301">Required</span></span>|<span data-ttu-id="96493-302">Domyślne</span><span class="sxs-lookup"><span data-stu-id="96493-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="96493-303">name</span><span class="sxs-lookup"><span data-stu-id="96493-303">name</span></span>|<span data-ttu-id="96493-304">Nazwa Hello hello API lub operacji, które hello dotyczy limitu przydziału.</span><span class="sxs-lookup"><span data-stu-id="96493-304">hello name of hello API or operation for which hello quota applies.</span></span>|<span data-ttu-id="96493-305">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-305">Yes</span></span>|<span data-ttu-id="96493-306">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-306">N/A</span></span>|  
|<span data-ttu-id="96493-307">Przepustowość</span><span class="sxs-lookup"><span data-stu-id="96493-307">bandwidth</span></span>|<span data-ttu-id="96493-308">Witaj maksymalną liczbę kilobajtów dozwolone interwale hello określone w hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="96493-308">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="96493-309">Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.</span><span class="sxs-lookup"><span data-stu-id="96493-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="96493-310">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-310">N/A</span></span>|  
|<span data-ttu-id="96493-311">wywołania</span><span class="sxs-lookup"><span data-stu-id="96493-311">calls</span></span>|<span data-ttu-id="96493-312">Maksymalna całkowita liczba połączeń dozwolona interwale hello określone w hello Hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="96493-312">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="96493-313">Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.</span><span class="sxs-lookup"><span data-stu-id="96493-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="96493-314">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-314">N/A</span></span>|  
|<span data-ttu-id="96493-315">okres odnawiania</span><span class="sxs-lookup"><span data-stu-id="96493-315">renewal-period</span></span>|<span data-ttu-id="96493-316">czas w sekundach, po których hello przydziału resetuje Hello.</span><span class="sxs-lookup"><span data-stu-id="96493-316">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="96493-317">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-317">Yes</span></span>|<span data-ttu-id="96493-318">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="96493-319">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="96493-319">Usage</span></span>  
 <span data-ttu-id="96493-320">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="96493-320">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="96493-321">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="96493-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="96493-322">**Zakresy zasad:** produktu</span><span class="sxs-lookup"><span data-stu-id="96493-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="96493-323"><a name="SetUsageQuotaByKey"></a>Ustaw przydział użycia według klucza</span><span class="sxs-lookup"><span data-stu-id="96493-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="96493-324">Witaj `quota-by-key` zasady wymuszają zastosowanie odnawialnymi lub okres istnienia wywołania woluminu i/lub przepustowości limit przydziału, na podstawie według klucza.</span><span class="sxs-lookup"><span data-stu-id="96493-324">hello `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="96493-325">klucz Hello może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.</span><span class="sxs-lookup"><span data-stu-id="96493-325">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="96493-326">Toospecify żądaniach powinno być liczone kierunku hello przydziału można dodać warunku opcjonalnie przyrostu.</span><span class="sxs-lookup"><span data-stu-id="96493-326">Optional increment condition can be added toospecify which requests should be counted towards hello quota.</span></span>  
  
 <span data-ttu-id="96493-327">Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [Zaawansowane żądanie ograniczania z usługą Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="96493-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="96493-328">Te zasady mogą być użyte tylko raz na dokument zasad.</span><span class="sxs-lookup"><span data-stu-id="96493-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="96493-329">[Wyrażenie zasad](api-management-policy-expressions.md) nie można użyć w żadnym hello atrybuty zasady dla tych zasad.</span><span class="sxs-lookup"><span data-stu-id="96493-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="96493-330">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="96493-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="96493-331">Przykład</span><span class="sxs-lookup"><span data-stu-id="96493-331">Example</span></span>  
 <span data-ttu-id="96493-332">W hello poniższy przykład przydział hello jest wyznaczaną przez adres IP hello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="96493-332">In hello following example, hello quota is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="96493-333">Elementy</span><span class="sxs-lookup"><span data-stu-id="96493-333">Elements</span></span>  
  
|<span data-ttu-id="96493-334">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-334">Name</span></span>|<span data-ttu-id="96493-335">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-335">Description</span></span>|<span data-ttu-id="96493-336">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="96493-337">limit przydziału</span><span class="sxs-lookup"><span data-stu-id="96493-337">quota</span></span>|<span data-ttu-id="96493-338">Element główny.</span><span class="sxs-lookup"><span data-stu-id="96493-338">Root element.</span></span>|<span data-ttu-id="96493-339">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="96493-340">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="96493-340">Attributes</span></span>  
  
|<span data-ttu-id="96493-341">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-341">Name</span></span>|<span data-ttu-id="96493-342">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-342">Description</span></span>|<span data-ttu-id="96493-343">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-343">Required</span></span>|<span data-ttu-id="96493-344">Domyślne</span><span class="sxs-lookup"><span data-stu-id="96493-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="96493-345">Przepustowość</span><span class="sxs-lookup"><span data-stu-id="96493-345">bandwidth</span></span>|<span data-ttu-id="96493-346">Witaj maksymalną liczbę kilobajtów dozwolone interwale hello określone w hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="96493-346">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="96493-347">Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.</span><span class="sxs-lookup"><span data-stu-id="96493-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="96493-348">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-348">N/A</span></span>|  
|<span data-ttu-id="96493-349">wywołania</span><span class="sxs-lookup"><span data-stu-id="96493-349">calls</span></span>|<span data-ttu-id="96493-350">Maksymalna całkowita liczba połączeń dozwolona interwale hello określone w hello Hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="96493-350">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="96493-351">Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.</span><span class="sxs-lookup"><span data-stu-id="96493-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="96493-352">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-352">N/A</span></span>|  
|<span data-ttu-id="96493-353">klucz liczników</span><span class="sxs-lookup"><span data-stu-id="96493-353">counter-key</span></span>|<span data-ttu-id="96493-354">Witaj klucza toouse hello zasad przydziału.</span><span class="sxs-lookup"><span data-stu-id="96493-354">hello key toouse for hello quota policy.</span></span>|<span data-ttu-id="96493-355">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-355">Yes</span></span>|<span data-ttu-id="96493-356">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-356">N/A</span></span>|  
|<span data-ttu-id="96493-357">Stan przyrostowy</span><span class="sxs-lookup"><span data-stu-id="96493-357">increment-condition</span></span>|<span data-ttu-id="96493-358">wyrażenie warunkowe Hello określenie, czy hello żądanie powinno być liczone kierunku hello przydziału (`true`)</span><span class="sxs-lookup"><span data-stu-id="96493-358">hello boolean expression specifying if hello request should be counted towards hello quota (`true`)</span></span>|<span data-ttu-id="96493-359">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-359">No</span></span>|<span data-ttu-id="96493-360">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-360">N/A</span></span>|  
|<span data-ttu-id="96493-361">okres odnawiania</span><span class="sxs-lookup"><span data-stu-id="96493-361">renewal-period</span></span>|<span data-ttu-id="96493-362">czas w sekundach, po których hello przydziału resetuje Hello.</span><span class="sxs-lookup"><span data-stu-id="96493-362">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="96493-363">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-363">Yes</span></span>|<span data-ttu-id="96493-364">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="96493-365">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="96493-365">Usage</span></span>  
 <span data-ttu-id="96493-366">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="96493-366">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="96493-367">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="96493-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="96493-368">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="96493-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="96493-369"><a name="ValidateJWT"></a>Sprawdź poprawność JWT</span><span class="sxs-lookup"><span data-stu-id="96493-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="96493-370">Witaj `validate-jwt` zasady wymuszają zastosowanie istnienia i ważności token JWT wyodrębnione z albo określonego nagłówka HTTP lub parametr zapytania określony.</span><span class="sxs-lookup"><span data-stu-id="96493-370">hello `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="96493-371">Witaj `validate-jwt` zasady wymagają tego hello `exp` zarejestrowanych oświadczeń jest inlcuded w hello JWT token, chyba że `require-expiration-time` atrybut jest określona i ustawić także`false`.</span><span class="sxs-lookup"><span data-stu-id="96493-371">hello `validate-jwt` policy requires that hello `exp` registered claim is inlcuded in hello JWT token, unless `require-expiration-time` attribute is specified and set too`false`.</span></span>  
> <span data-ttu-id="96493-372">Witaj `validate-jwt` zasad obsługuje HS256 i RS256 algorytmy podpisywania.</span><span class="sxs-lookup"><span data-stu-id="96493-372">hello `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="96493-373">Dla HS256 hello klucz należy podać wbudowane w ramach zasad hello w postaci kodowany w standardzie base64 hello.</span><span class="sxs-lookup"><span data-stu-id="96493-373">For HS256 hello key must be provided inline within hello policy in hello base64 encoded form.</span></span> <span data-ttu-id="96493-374">RS256 hello klucz ma toobe Podaj za pośrednictwem punktu końcowego Otwórz identyfikator konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="96493-374">For RS256 hello key has toobe provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="96493-375">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="96493-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="96493-376">Przykłady</span><span class="sxs-lookup"><span data-stu-id="96493-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="96493-377">Azure Mobile Services tokenu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="96493-377">Azure Mobile Services token validation</span></span>  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="96493-378">Azure Active Directory tokenu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="96493-378">Azure Active Directory token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="96493-379">Azure Active Directory B2C tokenu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="96493-379">Azure Active Directory B2C token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a><span data-ttu-id="96493-380">Autoryzowanie toooperations dostępu na podstawie tokenu oświadczeń</span><span class="sxs-lookup"><span data-stu-id="96493-380">Authorize access toooperations based on token claims</span></span>  
 <span data-ttu-id="96493-381">W tym przykładzie pokazano sposób toouse hello [JWT do zweryfikowania](api-management-access-restriction-policies.md#ValidateJWT) toopre zasad-toooperations dostępu na podstawie tokenu oświadczeń autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="96493-381">This example shows how toouse hello [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy toopre-authorize access toooperations based on token claims.</span></span> <span data-ttu-id="96493-382">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too13:50.</span><span class="sxs-lookup"><span data-stu-id="96493-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="96493-383">Szybkie przewijanie do przodu too15:00 zasady hello toosee skonfigurowane w edytorze zasad hello, a następnie too18:50 dla pokaz wywołanie operacji z portalu dla deweloperów hello zarówno z i bez hello wymagany token autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="96493-383">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="96493-384">Elementy</span><span class="sxs-lookup"><span data-stu-id="96493-384">Elements</span></span>  
  
|<span data-ttu-id="96493-385">Element</span><span class="sxs-lookup"><span data-stu-id="96493-385">Element</span></span>|<span data-ttu-id="96493-386">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-386">Description</span></span>|<span data-ttu-id="96493-387">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="96493-388">Sprawdź poprawność jwt</span><span class="sxs-lookup"><span data-stu-id="96493-388">validate-jwt</span></span>|<span data-ttu-id="96493-389">Element główny.</span><span class="sxs-lookup"><span data-stu-id="96493-389">Root element.</span></span>|<span data-ttu-id="96493-390">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-390">Yes</span></span>|  
|<span data-ttu-id="96493-391">grupy odbiorców</span><span class="sxs-lookup"><span data-stu-id="96493-391">audiences</span></span>|<span data-ttu-id="96493-392">Zawiera listę oświadczeń dopuszczalne odbiorców, które mogą być obecne w tokenie hello.</span><span class="sxs-lookup"><span data-stu-id="96493-392">Contains a list of acceptable audience claims that can be present on hello token.</span></span> <span data-ttu-id="96493-393">Jeśli wiele wartości odbiorców są obecne, a następnie sprawdzane są poszczególne wartości do momentu wszystkie wyczerpania (w takim przypadku niepowodzenia weryfikacji) lub aż do znalezienia właściwego konta.</span><span class="sxs-lookup"><span data-stu-id="96493-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="96493-394">Należy określić co najmniej jednego odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="96493-394">At least one audience must be specified.</span></span>|<span data-ttu-id="96493-395">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-395">No</span></span>|  
|<span data-ttu-id="96493-396">podpisywania klucze wystawcy</span><span class="sxs-lookup"><span data-stu-id="96493-396">issuer-signing-keys</span></span>|<span data-ttu-id="96493-397">Lista toovalidate klucze używane z algorytmem Base64 zabezpieczeń podpisany tokenów.</span><span class="sxs-lookup"><span data-stu-id="96493-397">A list of Base64-encoded security keys used toovalidate signed tokens.</span></span> <span data-ttu-id="96493-398">Jeśli wiele kluczy zabezpieczeń są obecne, a następnie sprawdzane są poszczególne klucze do momentu wszystkie wyczerpania (w takim przypadku niepowodzenia weryfikacji) lub do chwili pomyślnego jedną (przydatne w przypadku przerzucania token).</span><span class="sxs-lookup"><span data-stu-id="96493-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="96493-399">Kluczowe elementy mają opcjonalny `id` toomatch atrybut przed `kid` oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="96493-399">Key elements have an optional `id` attribute used toomatch against `kid` claim.</span></span>|<span data-ttu-id="96493-400">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-400">No</span></span>|  
|<span data-ttu-id="96493-401">wystawcy</span><span class="sxs-lookup"><span data-stu-id="96493-401">issuers</span></span>|<span data-ttu-id="96493-402">Lista dopuszczalne podmiotów zabezpieczeń, które wystawiły hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="96493-402">A list of acceptable principals that issued hello token.</span></span> <span data-ttu-id="96493-403">Jeśli występują wiele wartości wystawcy, a następnie sprawdzane są poszczególne wartości do momentu wszystkie wyczerpania (w takim przypadku niepowodzenia weryfikacji) lub aż do znalezienia właściwego konta.</span><span class="sxs-lookup"><span data-stu-id="96493-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="96493-404">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-404">No</span></span>|  
|<span data-ttu-id="96493-405">Konfiguracja protokołu openid</span><span class="sxs-lookup"><span data-stu-id="96493-405">openid-config</span></span>|<span data-ttu-id="96493-406">element Hello używany do określania zgodne endpoint konfiguracji Open ID, z którego podpisywania kluczy i wystawcy można uzyskać.</span><span class="sxs-lookup"><span data-stu-id="96493-406">hello element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="96493-407">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-407">No</span></span>|  
|<span data-ttu-id="96493-408">wymagane oświadczenia</span><span class="sxs-lookup"><span data-stu-id="96493-408">required-claims</span></span>|<span data-ttu-id="96493-409">Zawiera listę toobe oświadczeń oczekiwano występuje na powitania token dla niego toobe uważany za prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="96493-409">Contains a list of claims expected toobe present on hello token for it toobe considered valid.</span></span> <span data-ttu-id="96493-410">Gdy hello `match` zbyt ustawiono atrybut`all` każdej wartości oświadczeń w zasadach hello musi być dostępna w tokenie hello toosucceed sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="96493-410">When hello `match` attribute is set too`all` every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="96493-411">Gdy hello `match` zbyt ustawiono atrybut`any` co najmniej jedno oświadczenie musi być dostępna w tokenie hello toosucceed sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="96493-411">When hello `match` attribute is set too`any` at least one claim must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="96493-412">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-412">No</span></span>|  
|<span data-ttu-id="96493-413">zumo głównego klucza</span><span class="sxs-lookup"><span data-stu-id="96493-413">zumo-master-key</span></span>|<span data-ttu-id="96493-414">Klucz główny dla tokenów wystawionych przez usługi Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="96493-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="96493-415">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="96493-416">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="96493-416">Attributes</span></span>  
  
|<span data-ttu-id="96493-417">Nazwa</span><span class="sxs-lookup"><span data-stu-id="96493-417">Name</span></span>|<span data-ttu-id="96493-418">Opis</span><span class="sxs-lookup"><span data-stu-id="96493-418">Description</span></span>|<span data-ttu-id="96493-419">Wymagane</span><span class="sxs-lookup"><span data-stu-id="96493-419">Required</span></span>|<span data-ttu-id="96493-420">Domyślne</span><span class="sxs-lookup"><span data-stu-id="96493-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="96493-421">niedokładność zegara</span><span class="sxs-lookup"><span data-stu-id="96493-421">clock-skew</span></span>|<span data-ttu-id="96493-422">Zakres czasu.</span><span class="sxs-lookup"><span data-stu-id="96493-422">Timespan.</span></span> <span data-ttu-id="96493-423">Zawiera niektóre małych swobodę w przypadku oświadczeń wygaśnięcia tokenu hello jest obecny w tokenie hello i jest poza bieżącym hello Data i godzina.</span><span class="sxs-lookup"><span data-stu-id="96493-423">Provides some small leeway in case hello token's expiration claim is present in hello token and is past hello current date / time.</span></span>|<span data-ttu-id="96493-424">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-424">No</span></span>|<span data-ttu-id="96493-425">0 sekund</span><span class="sxs-lookup"><span data-stu-id="96493-425">0 seconds</span></span>|  
|<span data-ttu-id="96493-426">nie powiodło się weryfikacji komunikatów o błędach</span><span class="sxs-lookup"><span data-stu-id="96493-426">failed-validation-error-message</span></span>|<span data-ttu-id="96493-427">Błąd tooreturn wiadomość w treści odpowiedzi hello HTTP, jeśli hello JWT nie przeszedł pomyślnie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="96493-427">Error message tooreturn in hello HTTP response body if hello JWT does not pass validation.</span></span> <span data-ttu-id="96493-428">Ta wiadomość musi mieć żadnych znaków specjalnych prawidłowo wpisywany.</span><span class="sxs-lookup"><span data-stu-id="96493-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="96493-429">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-429">No</span></span>|<span data-ttu-id="96493-430">Domyślnego komunikatu o błędzie jest zależny od weryfikacji problem, na przykład "token JWT nie istnieje."</span><span class="sxs-lookup"><span data-stu-id="96493-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="96493-431">nie powiodło się weryfikacji httpcode</span><span class="sxs-lookup"><span data-stu-id="96493-431">failed-validation-httpcode</span></span>|<span data-ttu-id="96493-432">Tooreturn kod stanu HTTP, jeśli hello JWT nie przeszedł pomyślnie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="96493-432">HTTP Status code tooreturn if hello JWT doesn't pass validation.</span></span>|<span data-ttu-id="96493-433">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-433">No</span></span>|<span data-ttu-id="96493-434">401</span><span class="sxs-lookup"><span data-stu-id="96493-434">401</span></span>|  
|<span data-ttu-id="96493-435">Nazwa nagłówka</span><span class="sxs-lookup"><span data-stu-id="96493-435">header-name</span></span>|<span data-ttu-id="96493-436">Nazwa Hello nagłówka hello HTTP zawierający hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="96493-436">hello name of hello HTTP header holding hello token.</span></span>|<span data-ttu-id="96493-437">Albo `header-name` lub `query-paremeter-name` musi być określony; ale nie oba.</span><span class="sxs-lookup"><span data-stu-id="96493-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="96493-438">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-438">N/A</span></span>|  
|<span data-ttu-id="96493-439">id</span><span class="sxs-lookup"><span data-stu-id="96493-439">id</span></span>|<span data-ttu-id="96493-440">Hello `id` atrybutu na powitania `key` element umożliwia toospecify hello ciąg, który będzie dopasowywane `kid` oświadczeń w hello toofind tokenu (jeśli istnieje) limit hello odpowiedniego klucza toouse Walidacja podpisu.</span><span class="sxs-lookup"><span data-stu-id="96493-440">hello `id` attribute on hello `key` element allows you toospecify hello string that will be matched against `kid` claim in hello token (if present) toofind out hello appropriate key toouse for signature validation.</span></span>|<span data-ttu-id="96493-441">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-441">No</span></span>|<span data-ttu-id="96493-442">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-442">N/A</span></span>|  
|<span data-ttu-id="96493-443">dopasowanie</span><span class="sxs-lookup"><span data-stu-id="96493-443">match</span></span>|<span data-ttu-id="96493-444">Witaj `match` atrybutu na powitania `claim` element określa, czy wartość oświadczenia, co w zasadach hello musi być dostępna w tokenie hello toosucceed sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="96493-444">hello `match` attribute on hello `claim` element specifies whether every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="96493-445">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="96493-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="96493-446">-                          `all`-każdej wartości oświadczeń w zasadach hello musi być dostępna w tokenie hello toosucceed sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="96493-446">-                          `all` - every claim value in hello policy must be present in hello token for validation toosucceed.</span></span><br /><br /> <span data-ttu-id="96493-447">-                          `any`— wartość co najmniej jedno oświadczenie musi być dostępna w tokenie hello toosucceed sprawdzania poprawności.</span><span class="sxs-lookup"><span data-stu-id="96493-447">-                          `any` - at least one claim value must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="96493-448">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-448">No</span></span>|<span data-ttu-id="96493-449">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="96493-449">all</span></span>|  
|<span data-ttu-id="96493-450">Nazwa zapytania — paremeter</span><span class="sxs-lookup"><span data-stu-id="96493-450">query-paremeter-name</span></span>|<span data-ttu-id="96493-451">Nazwa parametru zapytania hello hello zawierający hello token Hello.</span><span class="sxs-lookup"><span data-stu-id="96493-451">hello name of hello hello query parameter holding hello token.</span></span>|<span data-ttu-id="96493-452">Albo `header-name` lub `query-paremeter-name` musi być określony; ale nie oba.</span><span class="sxs-lookup"><span data-stu-id="96493-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="96493-453">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-453">N/A</span></span>|  
|<span data-ttu-id="96493-454">Wymagaj — wygasa</span><span class="sxs-lookup"><span data-stu-id="96493-454">require-expiration-time</span></span>|<span data-ttu-id="96493-455">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="96493-455">Boolean.</span></span> <span data-ttu-id="96493-456">Określa, czy oświadczenie wygaśnięcia jest wymagany w tokenie hello.</span><span class="sxs-lookup"><span data-stu-id="96493-456">Specifies whether an expiration claim is required in hello token.</span></span>|<span data-ttu-id="96493-457">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-457">No</span></span>|<span data-ttu-id="96493-458">Wartość true</span><span class="sxs-lookup"><span data-stu-id="96493-458">true</span></span>|
|<span data-ttu-id="96493-459">Wymagaj schematu</span><span class="sxs-lookup"><span data-stu-id="96493-459">require-scheme</span></span>|<span data-ttu-id="96493-460">Witaj nazwę schematu tokenu hello, np. "Bearer".</span><span class="sxs-lookup"><span data-stu-id="96493-460">hello name of hello token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="96493-461">Jeśli ten atrybut zostanie ustawiony, hello zasad będzie upewnij się, że który określony schemat jest obecny w hello wartość nagłówka uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="96493-461">When this attribute is set, hello policy will ensure that specified scheme is present in hello Authorization header value.</span></span>|<span data-ttu-id="96493-462">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-462">No</span></span>|<span data-ttu-id="96493-463">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-463">N/A</span></span>|
|<span data-ttu-id="96493-464">Wymagaj podpisany — tokeny</span><span class="sxs-lookup"><span data-stu-id="96493-464">require-signed-tokens</span></span>|<span data-ttu-id="96493-465">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="96493-465">Boolean.</span></span> <span data-ttu-id="96493-466">Określa, czy token jest wymagany toobe podpisany.</span><span class="sxs-lookup"><span data-stu-id="96493-466">Specifies whether a token is required toobe signed.</span></span>|<span data-ttu-id="96493-467">Nie</span><span class="sxs-lookup"><span data-stu-id="96493-467">No</span></span>|<span data-ttu-id="96493-468">Wartość true</span><span class="sxs-lookup"><span data-stu-id="96493-468">true</span></span>|  
|<span data-ttu-id="96493-469">adres URL</span><span class="sxs-lookup"><span data-stu-id="96493-469">url</span></span>|<span data-ttu-id="96493-470">Otwórz adres URL punktu końcowego konfiguracji identyfikator, z której można uzyskać metadanych konfiguracji Open ID.</span><span class="sxs-lookup"><span data-stu-id="96493-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="96493-471">Dla usługi Azure Active Directory użyj następującego adresu URL hello: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` podstawiając nazwa dzierżawy katalogu, np. `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="96493-471">For Azure Active Directory use hello following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="96493-472">Tak</span><span class="sxs-lookup"><span data-stu-id="96493-472">Yes</span></span>|<span data-ttu-id="96493-473">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="96493-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="96493-474">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="96493-474">Usage</span></span>  
 <span data-ttu-id="96493-475">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="96493-475">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="96493-476">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="96493-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="96493-477">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="96493-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="96493-478">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96493-478">Next steps</span></span>
<span data-ttu-id="96493-479">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="96493-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
