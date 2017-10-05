---
title: "Zasady ograniczeń dostępu w usłudze Azure zarządzanie interfejsami API | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad ograniczeń dostępu dostępne do użycia w usłudze Azure API Management."
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
ms.openlocfilehash: 4c9991baf3fbcf3b8ea01f8dd573e2336db88b68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="e05a1-103">Zasady ograniczeń dostępu do interfejsu API zarządzania</span><span class="sxs-lookup"><span data-stu-id="e05a1-103">API Management access restriction policies</span></span>
<span data-ttu-id="e05a1-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="e05a1-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="e05a1-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="e05a1-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="e05a1-106"><a name="AccessRestrictionPolicies"></a>Zasady ograniczeń dostępu</span><span class="sxs-lookup"><span data-stu-id="e05a1-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="e05a1-107">[Nagłówek HTTP wyboru](api-management-access-restriction-policies.md#CheckHTTPHeader) — wymusza istnienia i/lub wartość nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="e05a1-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="e05a1-108">[Limit szybkości wywołanie przez subskrypcji](api-management-access-restriction-policies.md#LimitCallRate) — użycie uniemożliwia API wzrósł poprzez ograniczenie wywołań szybkości, na podstawie subskrypcji na.</span><span class="sxs-lookup"><span data-stu-id="e05a1-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="e05a1-109">[Limit szybkości wywołanie przez klucz](#LimitCallRateByKey) — użycie uniemożliwia API wzrósł ograniczając szybkość połączenia, na podstawie na klucz.</span><span class="sxs-lookup"><span data-stu-id="e05a1-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="e05a1-110">[Ograniczenia adresów IP wywołującego](api-management-access-restriction-policies.md#RestrictCallerIPs) -wywołania filtrów (umożliwia/nie zezwala na) z określonych adresów IP i/lub zakresów adresów.</span><span class="sxs-lookup"><span data-stu-id="e05a1-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="e05a1-111">[Ustaw przydział użycia subskrypcji](api-management-access-restriction-policies.md#SetUsageQuota) — umożliwia egzekwowanie odnawialnymi lub okres istnienia wywołania woluminu i/lub przepustowości limit przydziału, na podstawie na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="e05a1-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="e05a1-112">[Ustaw przydział użycia przez klucz](#SetUsageQuotaByKey) — umożliwia egzekwowanie odnawialnymi lub okres istnienia wywołania woluminu i/lub przepustowości limit przydziału, na podstawie według klucza.</span><span class="sxs-lookup"><span data-stu-id="e05a1-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="e05a1-113">[Sprawdź poprawność JWT](api-management-access-restriction-policies.md#ValidateJWT) — wymusza istnienia i ważności wyodrębniony z określonego nagłówka HTTP lub parametr zapytania określony token JWT.</span><span class="sxs-lookup"><span data-stu-id="e05a1-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="e05a1-114"><a name="CheckHTTPHeader"></a>Sprawdź nagłówka HTTP</span><span class="sxs-lookup"><span data-stu-id="e05a1-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="e05a1-115">Użyj `check-header` zasady do wymuszenia, że żądanie ma określonego nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="e05a1-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="e05a1-116">Można opcjonalnie sprawdzić, czy nagłówek nie ma określonej wartości lub sprawdź, czy zakres dozwolonych wartości.</span><span class="sxs-lookup"><span data-stu-id="e05a1-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="e05a1-117">W przypadku niepowodzenia sprawdzania zasad przerywa przetwarzania żądania i zwraca komunikat kodu i błąd stanu HTTP określone przez zasady.</span><span class="sxs-lookup"><span data-stu-id="e05a1-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e05a1-118">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="e05a1-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="e05a1-119">Przykład</span><span class="sxs-lookup"><span data-stu-id="e05a1-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="e05a1-120">Elementy</span><span class="sxs-lookup"><span data-stu-id="e05a1-120">Elements</span></span>  
  
|<span data-ttu-id="e05a1-121">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-121">Name</span></span>|<span data-ttu-id="e05a1-122">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-122">Description</span></span>|<span data-ttu-id="e05a1-123">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e05a1-124">Sprawdź — nagłówek</span><span class="sxs-lookup"><span data-stu-id="e05a1-124">check-header</span></span>|<span data-ttu-id="e05a1-125">Element główny.</span><span class="sxs-lookup"><span data-stu-id="e05a1-125">Root element.</span></span>|<span data-ttu-id="e05a1-126">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-126">Yes</span></span>|  
|<span data-ttu-id="e05a1-127">wartość</span><span class="sxs-lookup"><span data-stu-id="e05a1-127">value</span></span>|<span data-ttu-id="e05a1-128">Dozwolone wartości nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="e05a1-128">Allowed HTTP header value.</span></span> <span data-ttu-id="e05a1-129">Jeśli wiele elementów wartości są określone, sprawdzania jest uznawany sukcesu, jeśli jedna z wartości jest dopasowanie.</span><span class="sxs-lookup"><span data-stu-id="e05a1-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="e05a1-130">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e05a1-131">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="e05a1-131">Attributes</span></span>  
  
|<span data-ttu-id="e05a1-132">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-132">Name</span></span>|<span data-ttu-id="e05a1-133">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-133">Description</span></span>|<span data-ttu-id="e05a1-134">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-134">Required</span></span>|<span data-ttu-id="e05a1-135">Domyślne</span><span class="sxs-lookup"><span data-stu-id="e05a1-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e05a1-136">nie powiodło się wyboru komunikatów o błędach</span><span class="sxs-lookup"><span data-stu-id="e05a1-136">failed-check-error-message</span></span>|<span data-ttu-id="e05a1-137">Komunikat o błędzie zwracany w treści odpowiedzi HTTP, jeśli nagłówek nie istnieje lub ma nieprawidłową wartość.</span><span class="sxs-lookup"><span data-stu-id="e05a1-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="e05a1-138">Ta wiadomość musi mieć żadnych znaków specjalnych prawidłowo wpisywany.</span><span class="sxs-lookup"><span data-stu-id="e05a1-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="e05a1-139">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-139">Yes</span></span>|<span data-ttu-id="e05a1-140">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-140">N/A</span></span>|  
|<span data-ttu-id="e05a1-141">nie powiodło się wyboru httpcode</span><span class="sxs-lookup"><span data-stu-id="e05a1-141">failed-check-httpcode</span></span>|<span data-ttu-id="e05a1-142">Kod stanu HTTP do zwrócenia, jeśli nagłówek nie istnieje lub ma nieprawidłową wartość.</span><span class="sxs-lookup"><span data-stu-id="e05a1-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="e05a1-143">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-143">Yes</span></span>|<span data-ttu-id="e05a1-144">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-144">N/A</span></span>|  
|<span data-ttu-id="e05a1-145">Nazwa nagłówka</span><span class="sxs-lookup"><span data-stu-id="e05a1-145">header-name</span></span>|<span data-ttu-id="e05a1-146">Nazwa nagłówka HTTP do sprawdzenia.</span><span class="sxs-lookup"><span data-stu-id="e05a1-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="e05a1-147">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-147">Yes</span></span>|<span data-ttu-id="e05a1-148">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-148">N/A</span></span>|  
|<span data-ttu-id="e05a1-149">Ignoruj case</span><span class="sxs-lookup"><span data-stu-id="e05a1-149">ignore-case</span></span>|<span data-ttu-id="e05a1-150">Można ustawić na wartość True lub False.</span><span class="sxs-lookup"><span data-stu-id="e05a1-150">Can be set to True or False.</span></span> <span data-ttu-id="e05a1-151">Jeśli jest ustawiona na True przypadek jest ignorowane w przypadku wartość nagłówka jest porównywana zbiór dopuszczalnych wartości.</span><span class="sxs-lookup"><span data-stu-id="e05a1-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="e05a1-152">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-152">Yes</span></span>|<span data-ttu-id="e05a1-153">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e05a1-154">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="e05a1-154">Usage</span></span>  
 <span data-ttu-id="e05a1-155">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e05a1-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e05a1-156">**Sekcje zasad:** przychodzące, wychodzące</span><span class="sxs-lookup"><span data-stu-id="e05a1-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="e05a1-157">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="e05a1-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e05a1-158"><a name="LimitCallRate"></a>Limit szybkości wywołanie przez subskrypcję</span><span class="sxs-lookup"><span data-stu-id="e05a1-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="e05a1-159">`rate-limit` Zasad uniemożliwia nagłego interfejsu API na podstawie subskrypcji na ograniczając szybkość wywołania do określonej liczby na określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="e05a1-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="e05a1-160">Po wyzwoleniu tych zasad wywołującego odbiera `429 Too Many Requests` kod stanu odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e05a1-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e05a1-161">Te zasady mogą być użyte tylko raz na dokument zasad.</span><span class="sxs-lookup"><span data-stu-id="e05a1-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="e05a1-162">[Wyrażenie zasad](api-management-policy-expressions.md) nie można użyć w żadnym z atrybutów zasad dla tej zasady.</span><span class="sxs-lookup"><span data-stu-id="e05a1-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e05a1-163">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="e05a1-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="e05a1-164">Przykład</span><span class="sxs-lookup"><span data-stu-id="e05a1-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e05a1-165">Elementy</span><span class="sxs-lookup"><span data-stu-id="e05a1-165">Elements</span></span>  
  
|<span data-ttu-id="e05a1-166">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-166">Name</span></span>|<span data-ttu-id="e05a1-167">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-167">Description</span></span>|<span data-ttu-id="e05a1-168">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e05a1-169">Ustaw limit</span><span class="sxs-lookup"><span data-stu-id="e05a1-169">set-limit</span></span>|<span data-ttu-id="e05a1-170">Element główny.</span><span class="sxs-lookup"><span data-stu-id="e05a1-170">Root element.</span></span>|<span data-ttu-id="e05a1-171">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-171">Yes</span></span>|  
|<span data-ttu-id="e05a1-172">api</span><span class="sxs-lookup"><span data-stu-id="e05a1-172">api</span></span>|<span data-ttu-id="e05a1-173">Dodaj co najmniej jeden z tych elementów do narzuca ograniczenia szybkości wywołania interfejsów API w obrębie produktu.</span><span class="sxs-lookup"><span data-stu-id="e05a1-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="e05a1-174">Produktu i interfejsu API wywołać szybkość, z jaką ograniczenia są stosowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="e05a1-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="e05a1-175">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-175">No</span></span>|  
|<span data-ttu-id="e05a1-176">Operacja</span><span class="sxs-lookup"><span data-stu-id="e05a1-176">operation</span></span>|<span data-ttu-id="e05a1-177">Dodaj co najmniej jeden z tych elementów do narzuca ograniczenia szybkości wywołania operacji w obrębie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e05a1-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="e05a1-178">Produkt, interfejsu API i operacji należy wywołać szybkość, z jaką ograniczenia są stosowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="e05a1-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="e05a1-179">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e05a1-180">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="e05a1-180">Attributes</span></span>  
  
|<span data-ttu-id="e05a1-181">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-181">Name</span></span>|<span data-ttu-id="e05a1-182">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-182">Description</span></span>|<span data-ttu-id="e05a1-183">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-183">Required</span></span>|<span data-ttu-id="e05a1-184">Domyślne</span><span class="sxs-lookup"><span data-stu-id="e05a1-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e05a1-185">name</span><span class="sxs-lookup"><span data-stu-id="e05a1-185">name</span></span>|<span data-ttu-id="e05a1-186">Nazwa interfejsu API, do których chcesz zastosować limit szybkości.</span><span class="sxs-lookup"><span data-stu-id="e05a1-186">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="e05a1-187">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-187">Yes</span></span>|<span data-ttu-id="e05a1-188">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-188">N/A</span></span>|  
|<span data-ttu-id="e05a1-189">wywołania</span><span class="sxs-lookup"><span data-stu-id="e05a1-189">calls</span></span>|<span data-ttu-id="e05a1-190">Maksymalna liczba połączeń dozwolona określona w interwale `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e05a1-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="e05a1-191">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-191">Yes</span></span>|<span data-ttu-id="e05a1-192">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-192">N/A</span></span>|  
|<span data-ttu-id="e05a1-193">okres odnawiania</span><span class="sxs-lookup"><span data-stu-id="e05a1-193">renewal-period</span></span>|<span data-ttu-id="e05a1-194">Okres czasu w sekundach, po których resetuje limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="e05a1-194">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="e05a1-195">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-195">Yes</span></span>|<span data-ttu-id="e05a1-196">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e05a1-197">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="e05a1-197">Usage</span></span>  
 <span data-ttu-id="e05a1-198">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e05a1-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e05a1-199">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="e05a1-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e05a1-200">**Zakresy zasad:** produktu</span><span class="sxs-lookup"><span data-stu-id="e05a1-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="e05a1-201"><a name="LimitCallRateByKey"></a>Limit szybkości wywołanie przez klucz</span><span class="sxs-lookup"><span data-stu-id="e05a1-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="e05a1-202">`rate-limit-by-key` Zasad uniemożliwia nagłego interfejsu API na podstawie klucza na ograniczając szybkość wywołania do określonej liczby na określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="e05a1-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="e05a1-203">Klucz może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.</span><span class="sxs-lookup"><span data-stu-id="e05a1-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="e05a1-204">Aby określić, które żądania powinno być liczone się do limitu można dodać warunku opcjonalnie przyrostu.</span><span class="sxs-lookup"><span data-stu-id="e05a1-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="e05a1-205">Po wyzwoleniu tych zasad wywołującego odbiera `429 Too Many Requests` kod stanu odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="e05a1-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="e05a1-206">Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [Zaawansowane żądanie ograniczania z usługą Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="e05a1-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e05a1-207">Te zasady mogą być użyte tylko raz na dokument zasad.</span><span class="sxs-lookup"><span data-stu-id="e05a1-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e05a1-208">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="e05a1-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="e05a1-209">Przykład</span><span class="sxs-lookup"><span data-stu-id="e05a1-209">Example</span></span>  
 <span data-ttu-id="e05a1-210">W poniższym przykładzie limit szybkości jest wyznaczaną przez obiekt wywołujący adresu IP.</span><span class="sxs-lookup"><span data-stu-id="e05a1-210">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e05a1-211">Elementy</span><span class="sxs-lookup"><span data-stu-id="e05a1-211">Elements</span></span>  
  
|<span data-ttu-id="e05a1-212">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-212">Name</span></span>|<span data-ttu-id="e05a1-213">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-213">Description</span></span>|<span data-ttu-id="e05a1-214">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e05a1-215">Ustaw limit</span><span class="sxs-lookup"><span data-stu-id="e05a1-215">set-limit</span></span>|<span data-ttu-id="e05a1-216">Element główny.</span><span class="sxs-lookup"><span data-stu-id="e05a1-216">Root element.</span></span>|<span data-ttu-id="e05a1-217">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e05a1-218">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="e05a1-218">Attributes</span></span>  
  
|<span data-ttu-id="e05a1-219">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-219">Name</span></span>|<span data-ttu-id="e05a1-220">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-220">Description</span></span>|<span data-ttu-id="e05a1-221">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-221">Required</span></span>|<span data-ttu-id="e05a1-222">Domyślne</span><span class="sxs-lookup"><span data-stu-id="e05a1-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e05a1-223">wywołania</span><span class="sxs-lookup"><span data-stu-id="e05a1-223">calls</span></span>|<span data-ttu-id="e05a1-224">Maksymalna liczba połączeń dozwolona określona w interwale `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e05a1-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="e05a1-225">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-225">Yes</span></span>|<span data-ttu-id="e05a1-226">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-226">N/A</span></span>|  
|<span data-ttu-id="e05a1-227">klucz liczników</span><span class="sxs-lookup"><span data-stu-id="e05a1-227">counter-key</span></span>|<span data-ttu-id="e05a1-228">Klucz do użycia zasad limitu szybkości.</span><span class="sxs-lookup"><span data-stu-id="e05a1-228">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="e05a1-229">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-229">Yes</span></span>|<span data-ttu-id="e05a1-230">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-230">N/A</span></span>|  
|<span data-ttu-id="e05a1-231">Stan przyrostowy</span><span class="sxs-lookup"><span data-stu-id="e05a1-231">increment-condition</span></span>|<span data-ttu-id="e05a1-232">Wyrażenie warunkowe określenie, czy żądanie powinno być liczone kierunku przydział (`true`).</span><span class="sxs-lookup"><span data-stu-id="e05a1-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="e05a1-233">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-233">No</span></span>|<span data-ttu-id="e05a1-234">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-234">N/A</span></span>|  
|<span data-ttu-id="e05a1-235">okres odnawiania</span><span class="sxs-lookup"><span data-stu-id="e05a1-235">renewal-period</span></span>|<span data-ttu-id="e05a1-236">Okres czasu w sekundach, po których resetuje limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="e05a1-236">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="e05a1-237">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-237">Yes</span></span>|<span data-ttu-id="e05a1-238">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e05a1-239">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="e05a1-239">Usage</span></span>  
 <span data-ttu-id="e05a1-240">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e05a1-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e05a1-241">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="e05a1-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e05a1-242">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="e05a1-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e05a1-243"><a name="RestrictCallerIPs"></a>Ograniczenia adresów IP wywołującego</span><span class="sxs-lookup"><span data-stu-id="e05a1-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="e05a1-244">`ip-filter` (Umożliwia/nie zezwala na) wywołania z określonych adresów IP i/lub zakresów adresów filtry zasad.</span><span class="sxs-lookup"><span data-stu-id="e05a1-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e05a1-245">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="e05a1-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="e05a1-246">Przykład</span><span class="sxs-lookup"><span data-stu-id="e05a1-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="e05a1-247">Elementy</span><span class="sxs-lookup"><span data-stu-id="e05a1-247">Elements</span></span>  
  
|<span data-ttu-id="e05a1-248">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-248">Name</span></span>|<span data-ttu-id="e05a1-249">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-249">Description</span></span>|<span data-ttu-id="e05a1-250">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e05a1-251">Filtr IP</span><span class="sxs-lookup"><span data-stu-id="e05a1-251">ip-filter</span></span>|<span data-ttu-id="e05a1-252">Element główny.</span><span class="sxs-lookup"><span data-stu-id="e05a1-252">Root element.</span></span>|<span data-ttu-id="e05a1-253">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-253">Yes</span></span>|  
|<span data-ttu-id="e05a1-254">Adres</span><span class="sxs-lookup"><span data-stu-id="e05a1-254">address</span></span>|<span data-ttu-id="e05a1-255">Określa pojedynczy adres IP, na których chcesz filtrować.</span><span class="sxs-lookup"><span data-stu-id="e05a1-255">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="e05a1-256">Co najmniej jeden `address` lub `address-range` element jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="e05a1-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="e05a1-257">zakres adresów z = "address" Aby = "address"</span><span class="sxs-lookup"><span data-stu-id="e05a1-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="e05a1-258">Określa adres zakresu adresów IP, na których chcesz filtrować.</span><span class="sxs-lookup"><span data-stu-id="e05a1-258">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="e05a1-259">Co najmniej jeden `address` lub `address-range` element jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="e05a1-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e05a1-260">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="e05a1-260">Attributes</span></span>  
  
|<span data-ttu-id="e05a1-261">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-261">Name</span></span>|<span data-ttu-id="e05a1-262">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-262">Description</span></span>|<span data-ttu-id="e05a1-263">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-263">Required</span></span>|<span data-ttu-id="e05a1-264">Domyślne</span><span class="sxs-lookup"><span data-stu-id="e05a1-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e05a1-265">zakres adresów z = "address" Aby = "address"</span><span class="sxs-lookup"><span data-stu-id="e05a1-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="e05a1-266">Zakres adresów IP, aby zezwolić lub odmówić dostępu.</span><span class="sxs-lookup"><span data-stu-id="e05a1-266">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="e05a1-267">Wymagany, gdy `address-range` element jest używany.</span><span class="sxs-lookup"><span data-stu-id="e05a1-267">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="e05a1-268">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-268">N/A</span></span>|  
|<span data-ttu-id="e05a1-269">Filtr IP akcji = "Zezwalaj na &#124; zabraniać"</span><span class="sxs-lookup"><span data-stu-id="e05a1-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="e05a1-270">Określa, czy powinno być dozwolone wywołania nie dla określonych adresów IP i zakresów.</span><span class="sxs-lookup"><span data-stu-id="e05a1-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="e05a1-271">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-271">Yes</span></span>|<span data-ttu-id="e05a1-272">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e05a1-273">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="e05a1-273">Usage</span></span>  
 <span data-ttu-id="e05a1-274">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e05a1-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e05a1-275">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="e05a1-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e05a1-276">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="e05a1-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e05a1-277"><a name="SetUsageQuota"></a>Ustaw przydział użycia przez subskrypcję</span><span class="sxs-lookup"><span data-stu-id="e05a1-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="e05a1-278">`quota` Zasady wymuszają zastosowanie odnawialnymi lub okres istnienia wywołania woluminu i/lub przepustowości limit przydziału, na podstawie na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="e05a1-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e05a1-279">Te zasady mogą być użyte tylko raz na dokument zasad.</span><span class="sxs-lookup"><span data-stu-id="e05a1-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="e05a1-280">[Wyrażenie zasad](api-management-policy-expressions.md) nie można użyć w żadnym z atrybutów zasad dla tej zasady.</span><span class="sxs-lookup"><span data-stu-id="e05a1-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e05a1-281">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="e05a1-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="e05a1-282">Przykład</span><span class="sxs-lookup"><span data-stu-id="e05a1-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e05a1-283">Elementy</span><span class="sxs-lookup"><span data-stu-id="e05a1-283">Elements</span></span>  
  
|<span data-ttu-id="e05a1-284">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-284">Name</span></span>|<span data-ttu-id="e05a1-285">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-285">Description</span></span>|<span data-ttu-id="e05a1-286">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e05a1-287">limit przydziału</span><span class="sxs-lookup"><span data-stu-id="e05a1-287">quota</span></span>|<span data-ttu-id="e05a1-288">Element główny.</span><span class="sxs-lookup"><span data-stu-id="e05a1-288">Root element.</span></span>|<span data-ttu-id="e05a1-289">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-289">Yes</span></span>|  
|<span data-ttu-id="e05a1-290">api</span><span class="sxs-lookup"><span data-stu-id="e05a1-290">api</span></span>|<span data-ttu-id="e05a1-291">Dodaj co najmniej jeden z tych elementów do nakładają limit przydziału na interfejsy API w obrębie produktu.</span><span class="sxs-lookup"><span data-stu-id="e05a1-291">Add one  or more of these elements to impose a quota on APIs within the product.</span></span> <span data-ttu-id="e05a1-292">Przydziały produktu i interfejsu API są stosowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="e05a1-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="e05a1-293">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-293">No</span></span>|  
|<span data-ttu-id="e05a1-294">Operacja</span><span class="sxs-lookup"><span data-stu-id="e05a1-294">operation</span></span>|<span data-ttu-id="e05a1-295">Dodaj co najmniej jeden z tych elementów do nakładają limit przydziału na operacje w interfejsie API.</span><span class="sxs-lookup"><span data-stu-id="e05a1-295">Add one  or more of these elements to impose a quota on operations within an API.</span></span> <span data-ttu-id="e05a1-296">Przydziały produktu, interfejsu API i operacji są stosowane niezależnie.</span><span class="sxs-lookup"><span data-stu-id="e05a1-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="e05a1-297">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e05a1-298">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="e05a1-298">Attributes</span></span>  
  
|<span data-ttu-id="e05a1-299">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-299">Name</span></span>|<span data-ttu-id="e05a1-300">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-300">Description</span></span>|<span data-ttu-id="e05a1-301">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-301">Required</span></span>|<span data-ttu-id="e05a1-302">Domyślne</span><span class="sxs-lookup"><span data-stu-id="e05a1-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e05a1-303">name</span><span class="sxs-lookup"><span data-stu-id="e05a1-303">name</span></span>|<span data-ttu-id="e05a1-304">Nazwa interfejsu API lub operacji, którego dotyczy limitu przydziału.</span><span class="sxs-lookup"><span data-stu-id="e05a1-304">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="e05a1-305">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-305">Yes</span></span>|<span data-ttu-id="e05a1-306">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-306">N/A</span></span>|  
|<span data-ttu-id="e05a1-307">Przepustowość</span><span class="sxs-lookup"><span data-stu-id="e05a1-307">bandwidth</span></span>|<span data-ttu-id="e05a1-308">Maksymalna liczba kilobajtów dozwolone określona w interwale `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e05a1-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="e05a1-309">Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.</span><span class="sxs-lookup"><span data-stu-id="e05a1-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e05a1-310">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-310">N/A</span></span>|  
|<span data-ttu-id="e05a1-311">wywołania</span><span class="sxs-lookup"><span data-stu-id="e05a1-311">calls</span></span>|<span data-ttu-id="e05a1-312">Maksymalna liczba połączeń dozwolona określona w interwale `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e05a1-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="e05a1-313">Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.</span><span class="sxs-lookup"><span data-stu-id="e05a1-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e05a1-314">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-314">N/A</span></span>|  
|<span data-ttu-id="e05a1-315">okres odnawiania</span><span class="sxs-lookup"><span data-stu-id="e05a1-315">renewal-period</span></span>|<span data-ttu-id="e05a1-316">Okres czasu w sekundach, po których resetuje limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="e05a1-316">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="e05a1-317">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-317">Yes</span></span>|<span data-ttu-id="e05a1-318">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e05a1-319">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="e05a1-319">Usage</span></span>  
 <span data-ttu-id="e05a1-320">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e05a1-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e05a1-321">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="e05a1-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e05a1-322">**Zakresy zasad:** produktu</span><span class="sxs-lookup"><span data-stu-id="e05a1-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="e05a1-323"><a name="SetUsageQuotaByKey"></a>Ustaw przydział użycia według klucza</span><span class="sxs-lookup"><span data-stu-id="e05a1-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="e05a1-324">`quota-by-key` Zasady wymuszają zastosowanie odnawialnymi lub okres istnienia wywołania woluminu i/lub przepustowości limit przydziału, na podstawie według klucza.</span><span class="sxs-lookup"><span data-stu-id="e05a1-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="e05a1-325">Klucz może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.</span><span class="sxs-lookup"><span data-stu-id="e05a1-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="e05a1-326">Opcjonalne przyrostu warunku można dodać do określenia żądań, które powinno być liczone kierunku limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="e05a1-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="e05a1-327">Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [Zaawansowane żądanie ograniczania z usługą Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="e05a1-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e05a1-328">Te zasady mogą być użyte tylko raz na dokument zasad.</span><span class="sxs-lookup"><span data-stu-id="e05a1-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="e05a1-329">[Wyrażenie zasad](api-management-policy-expressions.md) nie można użyć w żadnym z atrybutów zasad dla tej zasady.</span><span class="sxs-lookup"><span data-stu-id="e05a1-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e05a1-330">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="e05a1-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="e05a1-331">Przykład</span><span class="sxs-lookup"><span data-stu-id="e05a1-331">Example</span></span>  
 <span data-ttu-id="e05a1-332">W poniższym przykładzie przydział jest wyznaczaną przez obiekt wywołujący adresu IP.</span><span class="sxs-lookup"><span data-stu-id="e05a1-332">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="e05a1-333">Elementy</span><span class="sxs-lookup"><span data-stu-id="e05a1-333">Elements</span></span>  
  
|<span data-ttu-id="e05a1-334">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-334">Name</span></span>|<span data-ttu-id="e05a1-335">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-335">Description</span></span>|<span data-ttu-id="e05a1-336">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e05a1-337">limit przydziału</span><span class="sxs-lookup"><span data-stu-id="e05a1-337">quota</span></span>|<span data-ttu-id="e05a1-338">Element główny.</span><span class="sxs-lookup"><span data-stu-id="e05a1-338">Root element.</span></span>|<span data-ttu-id="e05a1-339">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e05a1-340">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="e05a1-340">Attributes</span></span>  
  
|<span data-ttu-id="e05a1-341">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-341">Name</span></span>|<span data-ttu-id="e05a1-342">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-342">Description</span></span>|<span data-ttu-id="e05a1-343">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-343">Required</span></span>|<span data-ttu-id="e05a1-344">Domyślne</span><span class="sxs-lookup"><span data-stu-id="e05a1-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e05a1-345">Przepustowość</span><span class="sxs-lookup"><span data-stu-id="e05a1-345">bandwidth</span></span>|<span data-ttu-id="e05a1-346">Maksymalna liczba kilobajtów dozwolone określona w interwale `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e05a1-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="e05a1-347">Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.</span><span class="sxs-lookup"><span data-stu-id="e05a1-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e05a1-348">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-348">N/A</span></span>|  
|<span data-ttu-id="e05a1-349">wywołania</span><span class="sxs-lookup"><span data-stu-id="e05a1-349">calls</span></span>|<span data-ttu-id="e05a1-350">Maksymalna liczba połączeń dozwolona określona w interwale `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e05a1-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="e05a1-351">Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.</span><span class="sxs-lookup"><span data-stu-id="e05a1-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e05a1-352">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-352">N/A</span></span>|  
|<span data-ttu-id="e05a1-353">klucz liczników</span><span class="sxs-lookup"><span data-stu-id="e05a1-353">counter-key</span></span>|<span data-ttu-id="e05a1-354">Klucz do użycia zasad przydziału.</span><span class="sxs-lookup"><span data-stu-id="e05a1-354">The key to use for the quota policy.</span></span>|<span data-ttu-id="e05a1-355">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-355">Yes</span></span>|<span data-ttu-id="e05a1-356">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-356">N/A</span></span>|  
|<span data-ttu-id="e05a1-357">Stan przyrostowy</span><span class="sxs-lookup"><span data-stu-id="e05a1-357">increment-condition</span></span>|<span data-ttu-id="e05a1-358">Wyrażenie warunkowe określenie, czy żądanie powinno być liczone kierunku przydział (`true`)</span><span class="sxs-lookup"><span data-stu-id="e05a1-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="e05a1-359">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-359">No</span></span>|<span data-ttu-id="e05a1-360">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-360">N/A</span></span>|  
|<span data-ttu-id="e05a1-361">okres odnawiania</span><span class="sxs-lookup"><span data-stu-id="e05a1-361">renewal-period</span></span>|<span data-ttu-id="e05a1-362">Okres czasu w sekundach, po których resetuje limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="e05a1-362">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="e05a1-363">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-363">Yes</span></span>|<span data-ttu-id="e05a1-364">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e05a1-365">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="e05a1-365">Usage</span></span>  
 <span data-ttu-id="e05a1-366">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e05a1-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e05a1-367">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="e05a1-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e05a1-368">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="e05a1-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e05a1-369"><a name="ValidateJWT"></a>Sprawdź poprawność JWT</span><span class="sxs-lookup"><span data-stu-id="e05a1-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="e05a1-370">`validate-jwt` Zasady wymuszają zastosowanie istnienia i ważności token JWT wyodrębnione z albo określonego nagłówka HTTP lub parametr zapytania określony.</span><span class="sxs-lookup"><span data-stu-id="e05a1-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e05a1-371">`validate-jwt` Zasad wymaga, aby `exp` zarejestrowanych oświadczeń jest inlcuded w JWT token, chyba że `require-expiration-time` atrybut jest określona i ustawić `false`.</span><span class="sxs-lookup"><span data-stu-id="e05a1-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="e05a1-372">`validate-jwt` Zasad obsługuje HS256 i RS256 algorytmy podpisywania.</span><span class="sxs-lookup"><span data-stu-id="e05a1-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="e05a1-373">Dla HS256 klucz należy podać wbudowane w ramach zasad w postaci kodowany w standardzie base64.</span><span class="sxs-lookup"><span data-stu-id="e05a1-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="e05a1-374">RS256 klucz ma zapewnienie za pośrednictwem punktu końcowego Otwórz identyfikator konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e05a1-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e05a1-375">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="e05a1-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
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
    <claim name="name of the claim as it appears in the token" match="all|any">  
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="e05a1-376">Przykłady</span><span class="sxs-lookup"><span data-stu-id="e05a1-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="e05a1-377">Azure Mobile Services tokenu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="e05a1-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="e05a1-378">Azure Active Directory tokenu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="e05a1-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="e05a1-379">Azure Active Directory B2C tokenu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="e05a1-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="e05a1-380">Autoryzacja dostępu do operacji na podstawie tokenu oświadczeń</span><span class="sxs-lookup"><span data-stu-id="e05a1-380">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="e05a1-381">Ten przykład przedstawia sposób użycia [JWT do zweryfikowania](api-management-access-restriction-policies.md#ValidateJWT) zasad do wstępnie autoryzacji dostępu do operacji na podstawie tokenu oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="e05a1-381">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="e05a1-382">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybkie przewijanie do przodu do 13:50.</span><span class="sxs-lookup"><span data-stu-id="e05a1-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="e05a1-383">Szybko przewiń do przodu do 15:00, aby wyświetlić zasady skonfigurowane w edytorze zasad, a następnie do 18:50 dla pokaz wywołanie operacji z portalu dla deweloperów zarówno z i bez tokenu autoryzacji wymagane.</span><span class="sxs-lookup"><span data-stu-id="e05a1-383">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
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
  
### <a name="elements"></a><span data-ttu-id="e05a1-384">Elementy</span><span class="sxs-lookup"><span data-stu-id="e05a1-384">Elements</span></span>  
  
|<span data-ttu-id="e05a1-385">Element</span><span class="sxs-lookup"><span data-stu-id="e05a1-385">Element</span></span>|<span data-ttu-id="e05a1-386">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-386">Description</span></span>|<span data-ttu-id="e05a1-387">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="e05a1-388">Sprawdź poprawność jwt</span><span class="sxs-lookup"><span data-stu-id="e05a1-388">validate-jwt</span></span>|<span data-ttu-id="e05a1-389">Element główny.</span><span class="sxs-lookup"><span data-stu-id="e05a1-389">Root element.</span></span>|<span data-ttu-id="e05a1-390">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-390">Yes</span></span>|  
|<span data-ttu-id="e05a1-391">grupy odbiorców</span><span class="sxs-lookup"><span data-stu-id="e05a1-391">audiences</span></span>|<span data-ttu-id="e05a1-392">Zawiera listę oświadczeń dopuszczalne odbiorców, które mogą być obecne w tokenie.</span><span class="sxs-lookup"><span data-stu-id="e05a1-392">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="e05a1-393">Jeśli wiele wartości odbiorców są obecne, a następnie sprawdzane są poszczególne wartości do momentu wszystkie wyczerpania (w takim przypadku niepowodzenia weryfikacji) lub aż do znalezienia właściwego konta.</span><span class="sxs-lookup"><span data-stu-id="e05a1-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="e05a1-394">Należy określić co najmniej jednego odbiorcy.</span><span class="sxs-lookup"><span data-stu-id="e05a1-394">At least one audience must be specified.</span></span>|<span data-ttu-id="e05a1-395">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-395">No</span></span>|  
|<span data-ttu-id="e05a1-396">podpisywania klucze wystawcy</span><span class="sxs-lookup"><span data-stu-id="e05a1-396">issuer-signing-keys</span></span>|<span data-ttu-id="e05a1-397">Lista kluczy algorytmem Base64 zabezpieczeń używany do weryfikowania podpisanych tokenów.</span><span class="sxs-lookup"><span data-stu-id="e05a1-397">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="e05a1-398">Jeśli wiele kluczy zabezpieczeń są obecne, a następnie sprawdzane są poszczególne klucze do momentu wszystkie wyczerpania (w takim przypadku niepowodzenia weryfikacji) lub do chwili pomyślnego jedną (przydatne w przypadku przerzucania token).</span><span class="sxs-lookup"><span data-stu-id="e05a1-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="e05a1-399">Kluczowe elementy mają opcjonalny `id` atrybut używany do dopasowywania `kid` oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="e05a1-399">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="e05a1-400">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-400">No</span></span>|  
|<span data-ttu-id="e05a1-401">wystawcy</span><span class="sxs-lookup"><span data-stu-id="e05a1-401">issuers</span></span>|<span data-ttu-id="e05a1-402">Lista dopuszczalne podmiotów zabezpieczeń, które wystawiony token.</span><span class="sxs-lookup"><span data-stu-id="e05a1-402">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="e05a1-403">Jeśli występują wiele wartości wystawcy, a następnie sprawdzane są poszczególne wartości do momentu wszystkie wyczerpania (w takim przypadku niepowodzenia weryfikacji) lub aż do znalezienia właściwego konta.</span><span class="sxs-lookup"><span data-stu-id="e05a1-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="e05a1-404">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-404">No</span></span>|  
|<span data-ttu-id="e05a1-405">Konfiguracja protokołu openid</span><span class="sxs-lookup"><span data-stu-id="e05a1-405">openid-config</span></span>|<span data-ttu-id="e05a1-406">Element używany do określania zgodne endpoint konfiguracji Open ID, z którego podpisywania kluczy i wystawcy można uzyskać.</span><span class="sxs-lookup"><span data-stu-id="e05a1-406">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="e05a1-407">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-407">No</span></span>|  
|<span data-ttu-id="e05a1-408">wymagane oświadczenia</span><span class="sxs-lookup"><span data-stu-id="e05a1-408">required-claims</span></span>|<span data-ttu-id="e05a1-409">Zawiera listę oświadczeń powinien znajdować się na token, aby były uważane za prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="e05a1-409">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="e05a1-410">Gdy `match` atrybut ma ustawioną `all` każdej wartości oświadczeń w zasadzie musi znajdować się w tokenem Weryfikacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="e05a1-410">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="e05a1-411">Gdy `match` atrybut ma ustawioną `any` co najmniej jedno oświadczenie musi być obecny w tokenie Weryfikacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="e05a1-411">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="e05a1-412">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-412">No</span></span>|  
|<span data-ttu-id="e05a1-413">zumo głównego klucza</span><span class="sxs-lookup"><span data-stu-id="e05a1-413">zumo-master-key</span></span>|<span data-ttu-id="e05a1-414">Klucz główny dla tokenów wystawionych przez usługi Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="e05a1-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="e05a1-415">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e05a1-416">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="e05a1-416">Attributes</span></span>  
  
|<span data-ttu-id="e05a1-417">Nazwa</span><span class="sxs-lookup"><span data-stu-id="e05a1-417">Name</span></span>|<span data-ttu-id="e05a1-418">Opis</span><span class="sxs-lookup"><span data-stu-id="e05a1-418">Description</span></span>|<span data-ttu-id="e05a1-419">Wymagane</span><span class="sxs-lookup"><span data-stu-id="e05a1-419">Required</span></span>|<span data-ttu-id="e05a1-420">Domyślne</span><span class="sxs-lookup"><span data-stu-id="e05a1-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e05a1-421">niedokładność zegara</span><span class="sxs-lookup"><span data-stu-id="e05a1-421">clock-skew</span></span>|<span data-ttu-id="e05a1-422">Zakres czasu.</span><span class="sxs-lookup"><span data-stu-id="e05a1-422">Timespan.</span></span> <span data-ttu-id="e05a1-423">Zawiera niektóre małych swobodę w przypadku oświadczeń wygaśnięcia tokenu jest obecny w tokenie i jest poza bieżącą datę / godzinę.</span><span class="sxs-lookup"><span data-stu-id="e05a1-423">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span></span>|<span data-ttu-id="e05a1-424">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-424">No</span></span>|<span data-ttu-id="e05a1-425">0 sekund</span><span class="sxs-lookup"><span data-stu-id="e05a1-425">0 seconds</span></span>|  
|<span data-ttu-id="e05a1-426">nie powiodło się weryfikacji komunikatów o błędach</span><span class="sxs-lookup"><span data-stu-id="e05a1-426">failed-validation-error-message</span></span>|<span data-ttu-id="e05a1-427">Komunikat o błędzie do zwrócenia w treści odpowiedzi HTTP, jeśli token JWT nie przeszedł pomyślnie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="e05a1-427">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="e05a1-428">Ta wiadomość musi mieć żadnych znaków specjalnych prawidłowo wpisywany.</span><span class="sxs-lookup"><span data-stu-id="e05a1-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="e05a1-429">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-429">No</span></span>|<span data-ttu-id="e05a1-430">Domyślnego komunikatu o błędzie jest zależny od weryfikacji problem, na przykład "token JWT nie istnieje."</span><span class="sxs-lookup"><span data-stu-id="e05a1-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="e05a1-431">nie powiodło się weryfikacji httpcode</span><span class="sxs-lookup"><span data-stu-id="e05a1-431">failed-validation-httpcode</span></span>|<span data-ttu-id="e05a1-432">Kod stanu HTTP do zwrócenia, jeśli token JWT nie przeszedł pomyślnie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="e05a1-432">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="e05a1-433">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-433">No</span></span>|<span data-ttu-id="e05a1-434">401</span><span class="sxs-lookup"><span data-stu-id="e05a1-434">401</span></span>|  
|<span data-ttu-id="e05a1-435">Nazwa nagłówka</span><span class="sxs-lookup"><span data-stu-id="e05a1-435">header-name</span></span>|<span data-ttu-id="e05a1-436">Nazwa nagłówka HTTP zawierający token.</span><span class="sxs-lookup"><span data-stu-id="e05a1-436">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="e05a1-437">Albo `header-name` lub `query-paremeter-name` musi być określony; ale nie oba.</span><span class="sxs-lookup"><span data-stu-id="e05a1-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="e05a1-438">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-438">N/A</span></span>|  
|<span data-ttu-id="e05a1-439">id</span><span class="sxs-lookup"><span data-stu-id="e05a1-439">id</span></span>|<span data-ttu-id="e05a1-440">`id` Atrybutu `key` element umożliwia określenie ciąg, który będzie dopasowywane `kid` oświadczenia w tokenie (jeśli istnieje) dowiedzieć się, odpowiedni klucz do użycia w celu weryfikacji podpisu.</span><span class="sxs-lookup"><span data-stu-id="e05a1-440">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="e05a1-441">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-441">No</span></span>|<span data-ttu-id="e05a1-442">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-442">N/A</span></span>|  
|<span data-ttu-id="e05a1-443">dopasowanie</span><span class="sxs-lookup"><span data-stu-id="e05a1-443">match</span></span>|<span data-ttu-id="e05a1-444">`match` Atrybutu `claim` element określa, czy każda wartość oświadczenia w zasadach musi być obecny w tokenie Weryfikacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="e05a1-444">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="e05a1-445">Możliwe wartości:</span><span class="sxs-lookup"><span data-stu-id="e05a1-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="e05a1-446">-                          `all`-każdej wartości oświadczeń w zasadzie musi znajdować się w tokenem Weryfikacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="e05a1-446">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="e05a1-447">-                          `any`— wartość co najmniej jedno oświadczenie musi być obecny w tokenie Weryfikacja powiodła się.</span><span class="sxs-lookup"><span data-stu-id="e05a1-447">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="e05a1-448">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-448">No</span></span>|<span data-ttu-id="e05a1-449">Wszystkie</span><span class="sxs-lookup"><span data-stu-id="e05a1-449">all</span></span>|  
|<span data-ttu-id="e05a1-450">Nazwa zapytania — paremeter</span><span class="sxs-lookup"><span data-stu-id="e05a1-450">query-paremeter-name</span></span>|<span data-ttu-id="e05a1-451">Nazwa parametru zapytania zawierający token.</span><span class="sxs-lookup"><span data-stu-id="e05a1-451">The name of the the query parameter holding the token.</span></span>|<span data-ttu-id="e05a1-452">Albo `header-name` lub `query-paremeter-name` musi być określony; ale nie oba.</span><span class="sxs-lookup"><span data-stu-id="e05a1-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="e05a1-453">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-453">N/A</span></span>|  
|<span data-ttu-id="e05a1-454">Wymagaj — wygasa</span><span class="sxs-lookup"><span data-stu-id="e05a1-454">require-expiration-time</span></span>|<span data-ttu-id="e05a1-455">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="e05a1-455">Boolean.</span></span> <span data-ttu-id="e05a1-456">Określa, czy oświadczenie wygaśnięcia jest wymagany w tokenie.</span><span class="sxs-lookup"><span data-stu-id="e05a1-456">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="e05a1-457">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-457">No</span></span>|<span data-ttu-id="e05a1-458">Wartość true</span><span class="sxs-lookup"><span data-stu-id="e05a1-458">true</span></span>|
|<span data-ttu-id="e05a1-459">Wymagaj schematu</span><span class="sxs-lookup"><span data-stu-id="e05a1-459">require-scheme</span></span>|<span data-ttu-id="e05a1-460">Nazwa tokenu schemat, np. "Bearer".</span><span class="sxs-lookup"><span data-stu-id="e05a1-460">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="e05a1-461">Gdy tego atrybutu jest ustawiona, zasady zapewni określony schemat jest obecny w wartość nagłówka uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="e05a1-461">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="e05a1-462">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-462">No</span></span>|<span data-ttu-id="e05a1-463">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-463">N/A</span></span>|
|<span data-ttu-id="e05a1-464">Wymagaj podpisany — tokeny</span><span class="sxs-lookup"><span data-stu-id="e05a1-464">require-signed-tokens</span></span>|<span data-ttu-id="e05a1-465">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="e05a1-465">Boolean.</span></span> <span data-ttu-id="e05a1-466">Określa, czy token jest wymagany do podpisania.</span><span class="sxs-lookup"><span data-stu-id="e05a1-466">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="e05a1-467">Nie</span><span class="sxs-lookup"><span data-stu-id="e05a1-467">No</span></span>|<span data-ttu-id="e05a1-468">Wartość true</span><span class="sxs-lookup"><span data-stu-id="e05a1-468">true</span></span>|  
|<span data-ttu-id="e05a1-469">adres URL</span><span class="sxs-lookup"><span data-stu-id="e05a1-469">url</span></span>|<span data-ttu-id="e05a1-470">Otwórz adres URL punktu końcowego konfiguracji identyfikator, z której można uzyskać metadanych konfiguracji Open ID.</span><span class="sxs-lookup"><span data-stu-id="e05a1-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="e05a1-471">Dla usługi Azure Active Directory, użyj następującego adresu URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` podstawiając nazwa dzierżawy katalogu, np. `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="e05a1-471">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="e05a1-472">Tak</span><span class="sxs-lookup"><span data-stu-id="e05a1-472">Yes</span></span>|<span data-ttu-id="e05a1-473">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="e05a1-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e05a1-474">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="e05a1-474">Usage</span></span>  
 <span data-ttu-id="e05a1-475">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e05a1-475">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e05a1-476">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="e05a1-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e05a1-477">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="e05a1-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="e05a1-478">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e05a1-478">Next steps</span></span>
<span data-ttu-id="e05a1-479">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e05a1-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
