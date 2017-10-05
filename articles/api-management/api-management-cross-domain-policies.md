---
title: Azure API Management cross zasady domeny | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat dostępnych do użycia w usłudze Azure API Management zasady obejmujące różne domeny."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="af4ff-103">API Management cross domain policies (Zasady usługi API Management obejmujące różne domeny)</span><span class="sxs-lookup"><span data-stu-id="af4ff-103">API Management cross domain policies</span></span>
<span data-ttu-id="af4ff-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="af4ff-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="af4ff-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="af4ff-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="af4ff-106"><a name="CrossDomainPolicies"></a>Krzyżowe zasady domeny</span><span class="sxs-lookup"><span data-stu-id="af4ff-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="af4ff-107">[Zezwalaj na połączenia między domenami](api-management-cross-domain-policies.md#AllowCrossDomainCalls) — może ułatwić interfejsu API programu Adobe Flash i Microsoft Silverlight bazujące na przeglądarce klientów.</span><span class="sxs-lookup"><span data-stu-id="af4ff-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="af4ff-108">[CORS](api-management-cross-domain-policies.md#CORS) -dodaje współużytkowanie zasobów między źródłami (CORS) obsługi operacji lub interfejsu API w celu zapewnienia obsługi wywołań między domenami od klientów przeglądarki do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="af4ff-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="af4ff-109">[JSONP](api-management-cross-domain-policies.md#JSONP) -dodaje JSON z obsługą dopełnienie (JSONP) do operacji lub interfejsu API w celu zapewnienia obsługi wywołań między domenami od klientów przeglądarki JavaScript.</span><span class="sxs-lookup"><span data-stu-id="af4ff-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="af4ff-110"><a name="AllowCrossDomainCalls"></a>Zezwalaj na połączenia między domenami</span><span class="sxs-lookup"><span data-stu-id="af4ff-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="af4ff-111">Użyj `cross-domain` zasad, aby udostępnić interfejsu API programu Adobe Flash i Microsoft Silverlight bazujące na przeglądarce klientów.</span><span class="sxs-lookup"><span data-stu-id="af4ff-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="af4ff-112">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="af4ff-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="af4ff-113">Przykład</span><span class="sxs-lookup"><span data-stu-id="af4ff-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="af4ff-114">Elementy</span><span class="sxs-lookup"><span data-stu-id="af4ff-114">Elements</span></span>  
  
|<span data-ttu-id="af4ff-115">Nazwa</span><span class="sxs-lookup"><span data-stu-id="af4ff-115">Name</span></span>|<span data-ttu-id="af4ff-116">Opis</span><span class="sxs-lookup"><span data-stu-id="af4ff-116">Description</span></span>|<span data-ttu-id="af4ff-117">Wymagane</span><span class="sxs-lookup"><span data-stu-id="af4ff-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="af4ff-118">między domenami</span><span class="sxs-lookup"><span data-stu-id="af4ff-118">cross-domain</span></span>|<span data-ttu-id="af4ff-119">Element główny.</span><span class="sxs-lookup"><span data-stu-id="af4ff-119">Root element.</span></span> <span data-ttu-id="af4ff-120">Elementy podrzędne muszą być zgodne z [specyfikacji pliku zasad międzydomenowych Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="af4ff-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="af4ff-121">Tak</span><span class="sxs-lookup"><span data-stu-id="af4ff-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="af4ff-122">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="af4ff-122">Usage</span></span>  
 <span data-ttu-id="af4ff-123">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="af4ff-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="af4ff-124">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="af4ff-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="af4ff-125">**Zakresy zasad:** globalne</span><span class="sxs-lookup"><span data-stu-id="af4ff-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="af4ff-126"><a name="CORS"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="af4ff-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="af4ff-127">`cors` Zasad dodaje współużytkowanie zasobów między źródłami (CORS) obsługi operacji lub interfejsu API w celu zapewnienia obsługi wywołań między domenami od klientów przeglądarki do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="af4ff-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="af4ff-128">CORS pozwala przeglądarką a serwerem interakcji i określić, czy należy zezwolić określonym żądań cross-origin (tj. XMLHttpRequests wywołań z poziomu języka JavaScript na stronie sieci web do innych domen).</span><span class="sxs-lookup"><span data-stu-id="af4ff-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="af4ff-129">To pozwala na większą elastyczność niż tylko zezwalanie żądania z tego samego źródła, ale jest bezpieczniejsze niż stosowanie wszystkich żądań cross-origin.</span><span class="sxs-lookup"><span data-stu-id="af4ff-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="af4ff-130">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="af4ff-130">Policy statement</span></span>  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a><span data-ttu-id="af4ff-131">Przykład</span><span class="sxs-lookup"><span data-stu-id="af4ff-131">Example</span></span>  
 <span data-ttu-id="af4ff-132">W tym przykładzie pokazano, jak obsługiwać żądania wstępnego transmitowane, takich jak niestandardowe nagłówki lub metod innych niż GET i POST.</span><span class="sxs-lookup"><span data-stu-id="af4ff-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="af4ff-133">Aby obsługiwać niestandardowe nagłówki i dodatkowe zleceń HTTP, należy użyć `allowed-methods` i `allowed-headers` sekcjach przedstawiono, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="af4ff-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a><span data-ttu-id="af4ff-134">Elementy</span><span class="sxs-lookup"><span data-stu-id="af4ff-134">Elements</span></span>  
  
|<span data-ttu-id="af4ff-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="af4ff-135">Name</span></span>|<span data-ttu-id="af4ff-136">Opis</span><span class="sxs-lookup"><span data-stu-id="af4ff-136">Description</span></span>|<span data-ttu-id="af4ff-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="af4ff-137">Required</span></span>|<span data-ttu-id="af4ff-138">Domyślne</span><span class="sxs-lookup"><span data-stu-id="af4ff-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="af4ff-139">cors</span><span class="sxs-lookup"><span data-stu-id="af4ff-139">cors</span></span>|<span data-ttu-id="af4ff-140">Element główny.</span><span class="sxs-lookup"><span data-stu-id="af4ff-140">Root element.</span></span>|<span data-ttu-id="af4ff-141">Tak</span><span class="sxs-lookup"><span data-stu-id="af4ff-141">Yes</span></span>|<span data-ttu-id="af4ff-142">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="af4ff-142">N/A</span></span>|  
|<span data-ttu-id="af4ff-143">dozwolone źródła</span><span class="sxs-lookup"><span data-stu-id="af4ff-143">allowed-origins</span></span>|<span data-ttu-id="af4ff-144">Zawiera `origin` elementy, które opisują dozwolonych źródeł dla żądań między domenami.</span><span class="sxs-lookup"><span data-stu-id="af4ff-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="af4ff-145">`allowed-origins`może zawierać pojedyncze `origin` element, który określa `*` zezwalająca na wszystkie pochodzenia, jeden lub więcej `origin` elementów, które zawierają identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="af4ff-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="af4ff-146">Tak</span><span class="sxs-lookup"><span data-stu-id="af4ff-146">Yes</span></span>|<span data-ttu-id="af4ff-147">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="af4ff-147">N/A</span></span>|  
|<span data-ttu-id="af4ff-148">Punkt początkowy</span><span class="sxs-lookup"><span data-stu-id="af4ff-148">origin</span></span>|<span data-ttu-id="af4ff-149">Wartość może być albo `*` zezwalająca na wszystkie pochodzenia lub identyfikator URI, który określa pojedynczy punkt początkowy.</span><span class="sxs-lookup"><span data-stu-id="af4ff-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="af4ff-150">Identyfikator URI musi zawierać schemat, hosta i portu.</span><span class="sxs-lookup"><span data-stu-id="af4ff-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="af4ff-151">Tak</span><span class="sxs-lookup"><span data-stu-id="af4ff-151">Yes</span></span>|<span data-ttu-id="af4ff-152">W przypadku pominięcia w identyfikatorze URI port jest używany port 80 dla protokołu HTTP i jest używany port 443 dla protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="af4ff-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="af4ff-153">dozwolone metody</span><span class="sxs-lookup"><span data-stu-id="af4ff-153">allowed-methods</span></span>|<span data-ttu-id="af4ff-154">Ten element jest wymagany, jeśli metod innych niż GET lub POST są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="af4ff-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="af4ff-155">Zawiera `method` elementy, które określają obsługiwane polecenia HTTP.</span><span class="sxs-lookup"><span data-stu-id="af4ff-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="af4ff-156">Nie</span><span class="sxs-lookup"><span data-stu-id="af4ff-156">No</span></span>|<span data-ttu-id="af4ff-157">Jeśli nie ma tej sekcji, są obsługiwane GET i POST.</span><span class="sxs-lookup"><span data-stu-id="af4ff-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="af4ff-158">— Metoda</span><span class="sxs-lookup"><span data-stu-id="af4ff-158">method</span></span>|<span data-ttu-id="af4ff-159">Określa zlecenie HTTP.</span><span class="sxs-lookup"><span data-stu-id="af4ff-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="af4ff-160">Co najmniej jeden `method` element jest wymagany, jeśli `allowed-methods` sekcja jest obecny.</span><span class="sxs-lookup"><span data-stu-id="af4ff-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="af4ff-161">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="af4ff-161">N/A</span></span>|  
|<span data-ttu-id="af4ff-162">dozwolone nagłówki</span><span class="sxs-lookup"><span data-stu-id="af4ff-162">allowed-headers</span></span>|<span data-ttu-id="af4ff-163">Ten element zawiera `header` elementy Określanie nazw nagłówków, które mogą znajdować się w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="af4ff-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="af4ff-164">Nie</span><span class="sxs-lookup"><span data-stu-id="af4ff-164">No</span></span>|<span data-ttu-id="af4ff-165">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="af4ff-165">N/A</span></span>|  
|<span data-ttu-id="af4ff-166">Uwidacznianie nagłówki</span><span class="sxs-lookup"><span data-stu-id="af4ff-166">expose-headers</span></span>|<span data-ttu-id="af4ff-167">Ten element zawiera `header` elementy Określanie nazw nagłówków, które mają być dostępne dla klienta.</span><span class="sxs-lookup"><span data-stu-id="af4ff-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="af4ff-168">Nie</span><span class="sxs-lookup"><span data-stu-id="af4ff-168">No</span></span>|<span data-ttu-id="af4ff-169">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="af4ff-169">N/A</span></span>|  
|<span data-ttu-id="af4ff-170">nagłówek</span><span class="sxs-lookup"><span data-stu-id="af4ff-170">header</span></span>|<span data-ttu-id="af4ff-171">Określa nazwę nagłówka.</span><span class="sxs-lookup"><span data-stu-id="af4ff-171">Specifies a header name.</span></span>|<span data-ttu-id="af4ff-172">Co najmniej jeden `header` element jest wymagany w `allowed-headers` lub `expose-headers` sekcja jest obecny.</span><span class="sxs-lookup"><span data-stu-id="af4ff-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="af4ff-173">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="af4ff-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="af4ff-174">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="af4ff-174">Attributes</span></span>  
  
|<span data-ttu-id="af4ff-175">Nazwa</span><span class="sxs-lookup"><span data-stu-id="af4ff-175">Name</span></span>|<span data-ttu-id="af4ff-176">Opis</span><span class="sxs-lookup"><span data-stu-id="af4ff-176">Description</span></span>|<span data-ttu-id="af4ff-177">Wymagane</span><span class="sxs-lookup"><span data-stu-id="af4ff-177">Required</span></span>|<span data-ttu-id="af4ff-178">Domyślne</span><span class="sxs-lookup"><span data-stu-id="af4ff-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="af4ff-179">Zezwalaj na poświadczenia</span><span class="sxs-lookup"><span data-stu-id="af4ff-179">allow-credentials</span></span>|<span data-ttu-id="af4ff-180">`Access-Control-Allow-Credentials` Nagłówek odpowiedzi dotyczące stanu wstępnego zostanie ustawiona na wartość tego atrybutu i wpływa na możliwość klienta przesyłania poświadczeń w żądaniach między domenami.</span><span class="sxs-lookup"><span data-stu-id="af4ff-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="af4ff-181">Nie</span><span class="sxs-lookup"><span data-stu-id="af4ff-181">No</span></span>|<span data-ttu-id="af4ff-182">wartość false</span><span class="sxs-lookup"><span data-stu-id="af4ff-182">false</span></span>|  
|<span data-ttu-id="af4ff-183">Inspekcja result-max-age.</span><span class="sxs-lookup"><span data-stu-id="af4ff-183">preflight-result-max-age</span></span>|<span data-ttu-id="af4ff-184">`Access-Control-Max-Age` Nagłówek odpowiedzi dotyczące stanu wstępnego zostanie ustawiona na wartość tego atrybutu i wpływać na zdolność agenta użytkownika do pamięci podręcznej przed transmitowane odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="af4ff-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="af4ff-185">Nie</span><span class="sxs-lookup"><span data-stu-id="af4ff-185">No</span></span>|<span data-ttu-id="af4ff-186">0</span><span class="sxs-lookup"><span data-stu-id="af4ff-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="af4ff-187">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="af4ff-187">Usage</span></span>  
 <span data-ttu-id="af4ff-188">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="af4ff-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="af4ff-189">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="af4ff-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="af4ff-190">**Zakresy zasad:** interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="af4ff-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="af4ff-191"><a name="JSONP"></a>FORMAT JSONP</span><span class="sxs-lookup"><span data-stu-id="af4ff-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="af4ff-192">`jsonp` Zasad dodaje JSON z obsługą dopełnienie (JSONP) do operacji lub interfejsu API w celu zapewnienia obsługi wywołań między domenami od klientów przeglądarki JavaScript.</span><span class="sxs-lookup"><span data-stu-id="af4ff-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="af4ff-193">Format JSONP jest metoda używana w programach języka JavaScript do żądania danych z serwera w innej domenie.</span><span class="sxs-lookup"><span data-stu-id="af4ff-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="af4ff-194">JSONP pomija ograniczenia wymuszane przez większość przeglądarek internetowych, w którym dostęp do stron sieci web musi być w tej samej domenie.</span><span class="sxs-lookup"><span data-stu-id="af4ff-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="af4ff-195">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="af4ff-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="af4ff-196">Przykład</span><span class="sxs-lookup"><span data-stu-id="af4ff-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="af4ff-197">Jeśli należy wywołać metodę bez parametru wywołania zwrotnego? cb = XXX zwróci JSON zwykły (bez otoka wywołania funkcji).</span><span class="sxs-lookup"><span data-stu-id="af4ff-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="af4ff-198">Jeśli dodasz parametru wywołania zwrotnego `?cb=XXX` będzie zwracać wynik JSONP, zawijania oryginalnego JSON wyników wokół funkcja wywołania zwrotnego, takich jak`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="af4ff-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="af4ff-199">Elementy</span><span class="sxs-lookup"><span data-stu-id="af4ff-199">Elements</span></span>  
  
|<span data-ttu-id="af4ff-200">Nazwa</span><span class="sxs-lookup"><span data-stu-id="af4ff-200">Name</span></span>|<span data-ttu-id="af4ff-201">Opis</span><span class="sxs-lookup"><span data-stu-id="af4ff-201">Description</span></span>|<span data-ttu-id="af4ff-202">Wymagane</span><span class="sxs-lookup"><span data-stu-id="af4ff-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="af4ff-203">Format jsonp</span><span class="sxs-lookup"><span data-stu-id="af4ff-203">jsonp</span></span>|<span data-ttu-id="af4ff-204">Element główny.</span><span class="sxs-lookup"><span data-stu-id="af4ff-204">Root element.</span></span>|<span data-ttu-id="af4ff-205">Tak</span><span class="sxs-lookup"><span data-stu-id="af4ff-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="af4ff-206">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="af4ff-206">Attributes</span></span>  
  
|<span data-ttu-id="af4ff-207">Nazwa</span><span class="sxs-lookup"><span data-stu-id="af4ff-207">Name</span></span>|<span data-ttu-id="af4ff-208">Opis</span><span class="sxs-lookup"><span data-stu-id="af4ff-208">Description</span></span>|<span data-ttu-id="af4ff-209">Wymagane</span><span class="sxs-lookup"><span data-stu-id="af4ff-209">Required</span></span>|<span data-ttu-id="af4ff-210">Domyślne</span><span class="sxs-lookup"><span data-stu-id="af4ff-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="af4ff-211">nazwy parametru wywołania zwrotnego</span><span class="sxs-lookup"><span data-stu-id="af4ff-211">callback-parameter-name</span></span>|<span data-ttu-id="af4ff-212">Wywołanie funkcji JavaScript między domenami prefiksem nazwy FQDN, w której znajduje się funkcja.</span><span class="sxs-lookup"><span data-stu-id="af4ff-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="af4ff-213">Tak</span><span class="sxs-lookup"><span data-stu-id="af4ff-213">Yes</span></span>|<span data-ttu-id="af4ff-214">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="af4ff-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="af4ff-215">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="af4ff-215">Usage</span></span>  
 <span data-ttu-id="af4ff-216">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="af4ff-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="af4ff-217">**Sekcje zasad:** ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="af4ff-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="af4ff-218">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="af4ff-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="af4ff-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af4ff-219">Next steps</span></span>
<span data-ttu-id="af4ff-220">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="af4ff-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  