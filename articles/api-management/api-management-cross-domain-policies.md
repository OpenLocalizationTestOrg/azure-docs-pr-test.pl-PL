---
title: aaaAzure API Management cross zasady domeny | Dokumentacja firmy Microsoft
description: "Więcej informacji na temat hello cross dostępne do użycia w usłudze Azure API Management zasad domeny."
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
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="dd12d-103">API Management cross domain policies (Zasady usługi API Management obejmujące różne domeny)</span><span class="sxs-lookup"><span data-stu-id="dd12d-103">API Management cross domain policies</span></span>
<span data-ttu-id="dd12d-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management hello.</span><span class="sxs-lookup"><span data-stu-id="dd12d-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="dd12d-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="dd12d-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="dd12d-106"><a name="CrossDomainPolicies"></a>Krzyżowe zasady domeny</span><span class="sxs-lookup"><span data-stu-id="dd12d-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="dd12d-107">[Zezwalaj na połączenia między domenami](api-management-cross-domain-policies.md#AllowCrossDomainCalls) — sprawia, że interfejs API hello dostępne od klientów programu Adobe Flash i Microsoft Silverlight bazujące na przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="dd12d-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="dd12d-108">[CORS](api-management-cross-domain-policies.md#CORS) -dodaje współużytkowanie zasobów między źródłami (CORS) obsługuje tooan operacji lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="dd12d-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="dd12d-109">[JSONP](api-management-cross-domain-policies.md#JSONP) — dodaje JSON dopełnienie (JSONP) operacji tooan pomocy technicznej lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki JavaScript.</span><span class="sxs-lookup"><span data-stu-id="dd12d-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="dd12d-110"><a name="AllowCrossDomainCalls"></a>Zezwalaj na połączenia między domenami</span><span class="sxs-lookup"><span data-stu-id="dd12d-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="dd12d-111">Użyj hello `cross-domain` hello toomake zasad interfejsu API dostępny od klientów programu Adobe Flash i Microsoft Silverlight bazujące na przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="dd12d-111">Use hello `cross-domain` policy toomake hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="dd12d-112">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="dd12d-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="dd12d-113">Przykład</span><span class="sxs-lookup"><span data-stu-id="dd12d-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="dd12d-114">Elementy</span><span class="sxs-lookup"><span data-stu-id="dd12d-114">Elements</span></span>  
  
|<span data-ttu-id="dd12d-115">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dd12d-115">Name</span></span>|<span data-ttu-id="dd12d-116">Opis</span><span class="sxs-lookup"><span data-stu-id="dd12d-116">Description</span></span>|<span data-ttu-id="dd12d-117">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dd12d-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="dd12d-118">między domenami</span><span class="sxs-lookup"><span data-stu-id="dd12d-118">cross-domain</span></span>|<span data-ttu-id="dd12d-119">Element główny.</span><span class="sxs-lookup"><span data-stu-id="dd12d-119">Root element.</span></span> <span data-ttu-id="dd12d-120">Elementy podrzędne muszą być zgodne toohello [specyfikacji pliku zasad międzydomenowych Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="dd12d-120">Child elements must conform toohello [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="dd12d-121">Tak</span><span class="sxs-lookup"><span data-stu-id="dd12d-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="dd12d-122">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="dd12d-122">Usage</span></span>  
 <span data-ttu-id="dd12d-123">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="dd12d-123">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="dd12d-124">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="dd12d-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="dd12d-125">**Zakresy zasad:** globalne</span><span class="sxs-lookup"><span data-stu-id="dd12d-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="dd12d-126"><a name="CORS"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="dd12d-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="dd12d-127">Witaj `cors` zasad dodaje współużytkowanie zasobów między źródłami (CORS) obsługuje tooan operacji lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="dd12d-127">hello `cors` policy adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="dd12d-128">CORS przeglądarce i toointeract serwera i określić, czy tooallow określonych cross-origin żądań (tj. XMLHttpRequests wywołań z poziomu języka JavaScript w domenach tooother strony sieci web).</span><span class="sxs-lookup"><span data-stu-id="dd12d-128">CORS allows a browser and a server toointeract and determine whether or not tooallow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page tooother domains).</span></span> <span data-ttu-id="dd12d-129">To pozwala na większą elastyczność niż tylko zezwalanie żądania z tego samego źródła, ale jest bezpieczniejsze niż stosowanie wszystkich żądań cross-origin.</span><span class="sxs-lookup"><span data-stu-id="dd12d-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="dd12d-130">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="dd12d-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="dd12d-131">Przykład</span><span class="sxs-lookup"><span data-stu-id="dd12d-131">Example</span></span>  
 <span data-ttu-id="dd12d-132">W tym przykładzie pokazano, jak transmitowane wstępne toosupport żądań, takich jak niestandardowe nagłówki lub metod innych niż GET i POST.</span><span class="sxs-lookup"><span data-stu-id="dd12d-132">This example demonstrates how toosupport pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="dd12d-133">Niestandardowe nagłówki toosupport i dodatkowe zleceń HTTP, użyj hello `allowed-methods` i `allowed-headers` sekcjach przedstawiono, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="dd12d-133">toosupport custom headers and additional HTTP verbs, use hello `allowed-methods` and `allowed-headers` sections as shown in hello following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="dd12d-134">Elementy</span><span class="sxs-lookup"><span data-stu-id="dd12d-134">Elements</span></span>  
  
|<span data-ttu-id="dd12d-135">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dd12d-135">Name</span></span>|<span data-ttu-id="dd12d-136">Opis</span><span class="sxs-lookup"><span data-stu-id="dd12d-136">Description</span></span>|<span data-ttu-id="dd12d-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dd12d-137">Required</span></span>|<span data-ttu-id="dd12d-138">Domyślne</span><span class="sxs-lookup"><span data-stu-id="dd12d-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="dd12d-139">cors</span><span class="sxs-lookup"><span data-stu-id="dd12d-139">cors</span></span>|<span data-ttu-id="dd12d-140">Element główny.</span><span class="sxs-lookup"><span data-stu-id="dd12d-140">Root element.</span></span>|<span data-ttu-id="dd12d-141">Tak</span><span class="sxs-lookup"><span data-stu-id="dd12d-141">Yes</span></span>|<span data-ttu-id="dd12d-142">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="dd12d-142">N/A</span></span>|  
|<span data-ttu-id="dd12d-143">dozwolone źródła</span><span class="sxs-lookup"><span data-stu-id="dd12d-143">allowed-origins</span></span>|<span data-ttu-id="dd12d-144">Zawiera `origin` elementy, które opisują hello dozwolone źródła dla żądań między domenami.</span><span class="sxs-lookup"><span data-stu-id="dd12d-144">Contains `origin` elements that describe hello allowed origins for cross-domain requests.</span></span> <span data-ttu-id="dd12d-145">`allowed-origins`może zawierać pojedyncze `origin` element, który określa `*` tooallow każde źródło lub co najmniej jeden `origin` elementów, które zawierają identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="dd12d-145">`allowed-origins` can contain either a single `origin` element that specifies `*` tooallow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="dd12d-146">Tak</span><span class="sxs-lookup"><span data-stu-id="dd12d-146">Yes</span></span>|<span data-ttu-id="dd12d-147">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="dd12d-147">N/A</span></span>|  
|<span data-ttu-id="dd12d-148">Punkt początkowy</span><span class="sxs-lookup"><span data-stu-id="dd12d-148">origin</span></span>|<span data-ttu-id="dd12d-149">Witaj wartość może być albo `*` tooallow wszystkie pochodzenia lub identyfikator URI, który określa pojedynczy punkt początkowy.</span><span class="sxs-lookup"><span data-stu-id="dd12d-149">hello value can be either `*` tooallow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="dd12d-150">Witaj identyfikator URI musi zawierać schemat, hosta i portu.</span><span class="sxs-lookup"><span data-stu-id="dd12d-150">hello URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="dd12d-151">Tak</span><span class="sxs-lookup"><span data-stu-id="dd12d-151">Yes</span></span>|<span data-ttu-id="dd12d-152">W przypadku pominięcia portu hello w identyfikatorze URI jest używany port 80 dla protokołu HTTP i jest używany port 443 dla protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dd12d-152">If hello port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="dd12d-153">dozwolone metody</span><span class="sxs-lookup"><span data-stu-id="dd12d-153">allowed-methods</span></span>|<span data-ttu-id="dd12d-154">Ten element jest wymagany, jeśli metod innych niż GET lub POST są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="dd12d-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="dd12d-155">Zawiera `method` elementy określające hello obsługiwane polecenia HTTP.</span><span class="sxs-lookup"><span data-stu-id="dd12d-155">Contains `method` elements that specify hello supported HTTP verbs.</span></span>|<span data-ttu-id="dd12d-156">Nie</span><span class="sxs-lookup"><span data-stu-id="dd12d-156">No</span></span>|<span data-ttu-id="dd12d-157">Jeśli nie ma tej sekcji, są obsługiwane GET i POST.</span><span class="sxs-lookup"><span data-stu-id="dd12d-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="dd12d-158">— Metoda</span><span class="sxs-lookup"><span data-stu-id="dd12d-158">method</span></span>|<span data-ttu-id="dd12d-159">Określa zlecenie HTTP.</span><span class="sxs-lookup"><span data-stu-id="dd12d-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="dd12d-160">Co najmniej jeden `method` element jest wymagany, jeśli hello `allowed-methods` sekcja jest obecny.</span><span class="sxs-lookup"><span data-stu-id="dd12d-160">At least one `method` element is required if hello `allowed-methods` section is present.</span></span>|<span data-ttu-id="dd12d-161">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="dd12d-161">N/A</span></span>|  
|<span data-ttu-id="dd12d-162">dozwolone nagłówki</span><span class="sxs-lookup"><span data-stu-id="dd12d-162">allowed-headers</span></span>|<span data-ttu-id="dd12d-163">Ten element zawiera `header` Określanie nazw hello nagłówki, które można uwzględnić w żądaniu hello elementów.</span><span class="sxs-lookup"><span data-stu-id="dd12d-163">This element contains `header` elements specifying names of hello headers that can be included in hello request.</span></span>|<span data-ttu-id="dd12d-164">Nie</span><span class="sxs-lookup"><span data-stu-id="dd12d-164">No</span></span>|<span data-ttu-id="dd12d-165">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="dd12d-165">N/A</span></span>|  
|<span data-ttu-id="dd12d-166">Uwidacznianie nagłówki</span><span class="sxs-lookup"><span data-stu-id="dd12d-166">expose-headers</span></span>|<span data-ttu-id="dd12d-167">Ten element zawiera `header` elementy Określanie nazw nagłówków hello, które mają być dostępne przez powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="dd12d-167">This element contains `header` elements specifying names of hello headers that will be accessible by hello client.</span></span>|<span data-ttu-id="dd12d-168">Nie</span><span class="sxs-lookup"><span data-stu-id="dd12d-168">No</span></span>|<span data-ttu-id="dd12d-169">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="dd12d-169">N/A</span></span>|  
|<span data-ttu-id="dd12d-170">nagłówek</span><span class="sxs-lookup"><span data-stu-id="dd12d-170">header</span></span>|<span data-ttu-id="dd12d-171">Określa nazwę nagłówka.</span><span class="sxs-lookup"><span data-stu-id="dd12d-171">Specifies a header name.</span></span>|<span data-ttu-id="dd12d-172">Co najmniej jeden `header` element jest wymagany w `allowed-headers` lub `expose-headers` sekcja hello jest obecny.</span><span class="sxs-lookup"><span data-stu-id="dd12d-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if hello section is present.</span></span>|<span data-ttu-id="dd12d-173">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="dd12d-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="dd12d-174">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="dd12d-174">Attributes</span></span>  
  
|<span data-ttu-id="dd12d-175">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dd12d-175">Name</span></span>|<span data-ttu-id="dd12d-176">Opis</span><span class="sxs-lookup"><span data-stu-id="dd12d-176">Description</span></span>|<span data-ttu-id="dd12d-177">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dd12d-177">Required</span></span>|<span data-ttu-id="dd12d-178">Domyślne</span><span class="sxs-lookup"><span data-stu-id="dd12d-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="dd12d-179">Zezwalaj na poświadczenia</span><span class="sxs-lookup"><span data-stu-id="dd12d-179">allow-credentials</span></span>|<span data-ttu-id="dd12d-180">Witaj `Access-Control-Allow-Credentials` nagłówka odpowiedzi dotyczące stanu wstępnego hello zostanie Ustaw toohello wartość tego atrybutu i wpływają na powitania klienta możliwości toosubmit poświadczeń w żądaniach między domenami.</span><span class="sxs-lookup"><span data-stu-id="dd12d-180">hello `Access-Control-Allow-Credentials` header in hello preflight response will be set toohello value of this attribute and affect hello client’s ability toosubmit credentials in cross-domain requests.</span></span>|<span data-ttu-id="dd12d-181">Nie</span><span class="sxs-lookup"><span data-stu-id="dd12d-181">No</span></span>|<span data-ttu-id="dd12d-182">wartość false</span><span class="sxs-lookup"><span data-stu-id="dd12d-182">false</span></span>|  
|<span data-ttu-id="dd12d-183">Inspekcja result-max-age.</span><span class="sxs-lookup"><span data-stu-id="dd12d-183">preflight-result-max-age</span></span>|<span data-ttu-id="dd12d-184">Witaj `Access-Control-Max-Age` nagłówka odpowiedzi dotyczące stanu wstępnego hello zostanie Ustaw toohello wartość tego atrybutu i wpływają na agenta użytkownika hello możliwości toocache wstępne transmitowane odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="dd12d-184">hello `Access-Control-Max-Age` header in hello preflight response will be set toohello value of this attribute and affect hello user agent’s ability toocache pre-flight response.</span></span>|<span data-ttu-id="dd12d-185">Nie</span><span class="sxs-lookup"><span data-stu-id="dd12d-185">No</span></span>|<span data-ttu-id="dd12d-186">0</span><span class="sxs-lookup"><span data-stu-id="dd12d-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="dd12d-187">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="dd12d-187">Usage</span></span>  
 <span data-ttu-id="dd12d-188">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="dd12d-188">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="dd12d-189">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="dd12d-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="dd12d-190">**Zakresy zasad:** interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="dd12d-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="dd12d-191"><a name="JSONP"></a>FORMAT JSONP</span><span class="sxs-lookup"><span data-stu-id="dd12d-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="dd12d-192">Witaj `jsonp` zasad dodaje JSON z dopełnienie operacji tooan pomocy technicznej (JSONP) lub tooallow międzydomenowego interfejsu API z klientów przeglądarki języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="dd12d-192">hello `jsonp` policy adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="dd12d-193">Format JSONP jest metodę JavaScript programy toorequest danych z serwera w innej domenie.</span><span class="sxs-lookup"><span data-stu-id="dd12d-193">JSONP is a method used in JavaScript programs toorequest data from a server in a different domain.</span></span> <span data-ttu-id="dd12d-194">JSONP pomija ograniczenia hello wymuszane przez większość przeglądarek internetowych, w którym strony tooweb dostępu muszą być w hello tej samej domenie.</span><span class="sxs-lookup"><span data-stu-id="dd12d-194">JSONP bypasses hello limitation enforced by most web browsers where access tooweb pages must be in hello same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="dd12d-195">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="dd12d-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="dd12d-196">Przykład</span><span class="sxs-lookup"><span data-stu-id="dd12d-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="dd12d-197">Jeśli należy wywołać metodę hello bez parametru wywołania zwrotnego hello? cb = XXX zwróci JSON zwykły (bez otoka wywołania funkcji).</span><span class="sxs-lookup"><span data-stu-id="dd12d-197">If you call hello method without hello callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="dd12d-198">Jeśli dodasz parametru wywołania zwrotnego hello `?cb=XXX` zostanie zwrócone w wyniku JSONP zawijania hello oryginalne wyniki JSON wokół hello funkcja wywołania zwrotnego, takie jak`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="dd12d-198">If you add hello callback parameter `?cb=XXX` it will return a JSONP result, wrapping hello original JSON results around hello callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="dd12d-199">Elementy</span><span class="sxs-lookup"><span data-stu-id="dd12d-199">Elements</span></span>  
  
|<span data-ttu-id="dd12d-200">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dd12d-200">Name</span></span>|<span data-ttu-id="dd12d-201">Opis</span><span class="sxs-lookup"><span data-stu-id="dd12d-201">Description</span></span>|<span data-ttu-id="dd12d-202">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dd12d-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="dd12d-203">Format jsonp</span><span class="sxs-lookup"><span data-stu-id="dd12d-203">jsonp</span></span>|<span data-ttu-id="dd12d-204">Element główny.</span><span class="sxs-lookup"><span data-stu-id="dd12d-204">Root element.</span></span>|<span data-ttu-id="dd12d-205">Tak</span><span class="sxs-lookup"><span data-stu-id="dd12d-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="dd12d-206">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="dd12d-206">Attributes</span></span>  
  
|<span data-ttu-id="dd12d-207">Nazwa</span><span class="sxs-lookup"><span data-stu-id="dd12d-207">Name</span></span>|<span data-ttu-id="dd12d-208">Opis</span><span class="sxs-lookup"><span data-stu-id="dd12d-208">Description</span></span>|<span data-ttu-id="dd12d-209">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dd12d-209">Required</span></span>|<span data-ttu-id="dd12d-210">Domyślne</span><span class="sxs-lookup"><span data-stu-id="dd12d-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="dd12d-211">nazwy parametru wywołania zwrotnego</span><span class="sxs-lookup"><span data-stu-id="dd12d-211">callback-parameter-name</span></span>|<span data-ttu-id="dd12d-212">Witaj wywołanie funkcji JavaScript między domenami prefiksem nazwy FQDN hello gdzie hello znajduje się funkcja.</span><span class="sxs-lookup"><span data-stu-id="dd12d-212">hello cross-domain JavaScript function call prefixed with hello fully qualified domain name where hello function resides.</span></span>|<span data-ttu-id="dd12d-213">Tak</span><span class="sxs-lookup"><span data-stu-id="dd12d-213">Yes</span></span>|<span data-ttu-id="dd12d-214">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="dd12d-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="dd12d-215">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="dd12d-215">Usage</span></span>  
 <span data-ttu-id="dd12d-216">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="dd12d-216">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="dd12d-217">**Sekcje zasad:** ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="dd12d-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="dd12d-218">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="dd12d-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="dd12d-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dd12d-219">Next steps</span></span>
<span data-ttu-id="dd12d-220">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="dd12d-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  