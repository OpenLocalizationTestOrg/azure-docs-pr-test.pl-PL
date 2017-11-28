---
title: "zasad przekształcania zarządzanie interfejsami API aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad przekształcania hello dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="c75b8-103">Zarządzanie interfejsami API zasad przekształcania</span><span class="sxs-lookup"><span data-stu-id="c75b8-103">API Management transformation policies</span></span>
<span data-ttu-id="c75b8-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="c75b8-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="c75b8-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="c75b8-106"><a name="TransformationPolicies"></a>Zasad przekształcania</span><span class="sxs-lookup"><span data-stu-id="c75b8-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="c75b8-107">[Konwertuj JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) — konwertuje żądania lub odpowiedzi body z JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="c75b8-107">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
-   <span data-ttu-id="c75b8-108">[Konwertuj XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) — konwertuje żądania lub odpowiedzi body z XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="c75b8-108">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
-   <span data-ttu-id="c75b8-109">[Znajdowanie i zamienianie ciągów w treści](api-management-transformation-policies.md#Findandreplacestringinbody) — znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.</span><span class="sxs-lookup"><span data-stu-id="c75b8-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="c75b8-110">[Maski adresów URL w zawartości](api-management-transformation-policies.md#MaskURLSContent) -ponownie zapisuje (maski) łącza w odpowiedzi hello body tak, aby wskazywały toohello równoważne połączenie za pośrednictwem bramy hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
-   <span data-ttu-id="c75b8-111">[Ustaw usługę zaplecza](api-management-transformation-policies.md#SetBackendService) — zmienia hello usługi wewnętrznej bazy danych dla żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="c75b8-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="c75b8-112">[Ustaw treści](api-management-transformation-policies.md#SetBody) -ustawia treść wiadomości powitania żądań przychodzących i wychodzących.</span><span class="sxs-lookup"><span data-stu-id="c75b8-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="c75b8-113">[Set — nagłówek HTTP](api-management-transformation-policies.md#SetHTTPheader) — przypisuje wartość tooan istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="c75b8-114">[Wartość parametru ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) — dodaje, zastępuje wartość lub usuwa parametru ciągu zapytania żądania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="c75b8-115">[Ponowne zapisywanie adresów URL](api-management-transformation-policies.md#RewriteURL) — konwertuje adres URL żądania w postaci toohello publicznego formularza oczekiwane przez usługę sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
-   <span data-ttu-id="c75b8-116">[Przekształcanie XML za pomocą XSLT](api-management-transformation-policies.md#XSLTransform) — ma zastosowanie tooXML transformacji XSL w treści żądania lub odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
##  <span data-ttu-id="c75b8-117"><a name="ConvertJSONtoXML"></a>Konwertuj JSON tooXML</span><span class="sxs-lookup"><span data-stu-id="c75b8-117"><a name="ConvertJSONtoXML"></a> Convert JSON tooXML</span></span>  
 <span data-ttu-id="c75b8-118">Witaj `json-to-xml` zasad konwertuje treści żądania lub odpowiedzi z JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="c75b8-118">hello `json-to-xml` policy converts a request or response body from JSON tooXML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c75b8-119">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="c75b8-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="c75b8-120">Przykład</span><span class="sxs-lookup"><span data-stu-id="c75b8-120">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="c75b8-121">Elementy</span><span class="sxs-lookup"><span data-stu-id="c75b8-121">Elements</span></span>  
  
|<span data-ttu-id="c75b8-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-122">Name</span></span>|<span data-ttu-id="c75b8-123">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-123">Description</span></span>|<span data-ttu-id="c75b8-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c75b8-125">JSON do pliku xml</span><span class="sxs-lookup"><span data-stu-id="c75b8-125">json-to-xml</span></span>|<span data-ttu-id="c75b8-126">Element główny.</span><span class="sxs-lookup"><span data-stu-id="c75b8-126">Root element.</span></span>|<span data-ttu-id="c75b8-127">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c75b8-128">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="c75b8-128">Attributes</span></span>  
  
|<span data-ttu-id="c75b8-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-129">Name</span></span>|<span data-ttu-id="c75b8-130">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-130">Description</span></span>|<span data-ttu-id="c75b8-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-131">Required</span></span>|<span data-ttu-id="c75b8-132">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c75b8-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c75b8-133">Zastosuj</span><span class="sxs-lookup"><span data-stu-id="c75b8-133">apply</span></span>|<span data-ttu-id="c75b8-134">Atrybut Hello musi być ustawiona tooone hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="c75b8-134">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c75b8-135">-zawsze — Zawsze stosuj konwersji.</span><span class="sxs-lookup"><span data-stu-id="c75b8-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="c75b8-136">convert zawartości typu json - tylko wtedy, gdy nagłówek odpowiedzi Content-Type wskazuje obecność JSON.</span><span class="sxs-lookup"><span data-stu-id="c75b8-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="c75b8-137">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-137">Yes</span></span>|<span data-ttu-id="c75b8-138">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-138">N/A</span></span>|  
|<span data-ttu-id="c75b8-139">należy wziąć pod uwagę zaakceptować — nagłówek</span><span class="sxs-lookup"><span data-stu-id="c75b8-139">consider-accept-header</span></span>|<span data-ttu-id="c75b8-140">Atrybut Hello musi być ustawiona tooone hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="c75b8-140">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c75b8-141">— wartość true — zastosowania konwersji w żądaniu nagłówka Accept żądania JSON.</span><span class="sxs-lookup"><span data-stu-id="c75b8-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="c75b8-142">— wartość false — Zawsze stosuj konwersji.</span><span class="sxs-lookup"><span data-stu-id="c75b8-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="c75b8-143">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-143">No</span></span>|<span data-ttu-id="c75b8-144">Wartość true</span><span class="sxs-lookup"><span data-stu-id="c75b8-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c75b8-145">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c75b8-145">Usage</span></span>  
 <span data-ttu-id="c75b8-146">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c75b8-146">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c75b8-147">**Sekcje zasad:** przychodzące, wychodzące, na błąd</span><span class="sxs-lookup"><span data-stu-id="c75b8-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="c75b8-148">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="c75b8-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c75b8-149"><a name="ConvertXMLtoJSON"></a>Konwertuj XML tooJSON</span><span class="sxs-lookup"><span data-stu-id="c75b8-149"><a name="ConvertXMLtoJSON"></a> Convert XML tooJSON</span></span>  
 <span data-ttu-id="c75b8-150">Witaj `xml-to-json` zasad konwertuje treści żądania lub odpowiedzi z XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="c75b8-150">hello `xml-to-json` policy converts a request or response body from XML tooJSON.</span></span> <span data-ttu-id="c75b8-151">Te zasady mogą być używane toomodernize, podstawą interfejsów API usług sieci web XML — tylko do wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c75b8-151">This policy can be used toomodernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c75b8-152">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="c75b8-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="c75b8-153">Przykład</span><span class="sxs-lookup"><span data-stu-id="c75b8-153">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="c75b8-154">Elementy</span><span class="sxs-lookup"><span data-stu-id="c75b8-154">Elements</span></span>  
  
|<span data-ttu-id="c75b8-155">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-155">Name</span></span>|<span data-ttu-id="c75b8-156">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-156">Description</span></span>|<span data-ttu-id="c75b8-157">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c75b8-158">XML do formatu json</span><span class="sxs-lookup"><span data-stu-id="c75b8-158">xml-to-json</span></span>|<span data-ttu-id="c75b8-159">Element główny.</span><span class="sxs-lookup"><span data-stu-id="c75b8-159">Root element.</span></span>|<span data-ttu-id="c75b8-160">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c75b8-161">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="c75b8-161">Attributes</span></span>  
  
|<span data-ttu-id="c75b8-162">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-162">Name</span></span>|<span data-ttu-id="c75b8-163">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-163">Description</span></span>|<span data-ttu-id="c75b8-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-164">Required</span></span>|<span data-ttu-id="c75b8-165">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c75b8-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c75b8-166">rodzaj</span><span class="sxs-lookup"><span data-stu-id="c75b8-166">kind</span></span>|<span data-ttu-id="c75b8-167">Atrybut Hello musi być ustawiona tooone hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="c75b8-167">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c75b8-168">javascript — przyjazne - hello przekonwertować JSON ma deweloperzy przyjazną tooJavaScript formularza.</span><span class="sxs-lookup"><span data-stu-id="c75b8-168">-   javascript-friendly - hello converted JSON has a form friendly tooJavaScript developers.</span></span><br /><span data-ttu-id="c75b8-169">-bezpośredni — Witaj przekonwertowanego JSON odzwierciedla strukturę dokumentu XML oryginalnego hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-169">-   direct - hello converted JSON reflects hello original XML document's structure.</span></span>|<span data-ttu-id="c75b8-170">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-170">Yes</span></span>|<span data-ttu-id="c75b8-171">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-171">N/A</span></span>|  
|<span data-ttu-id="c75b8-172">Zastosuj</span><span class="sxs-lookup"><span data-stu-id="c75b8-172">apply</span></span>|<span data-ttu-id="c75b8-173">Atrybut Hello musi być ustawiona tooone hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="c75b8-173">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c75b8-174">-zawsze - przekonwertować zawsze.</span><span class="sxs-lookup"><span data-stu-id="c75b8-174">-   always - convert always.</span></span><br /><span data-ttu-id="c75b8-175">convert zawartości — typ xml - tylko wtedy, gdy nagłówek odpowiedzi Content-Type wskazuje obecność XML.</span><span class="sxs-lookup"><span data-stu-id="c75b8-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="c75b8-176">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-176">Yes</span></span>|<span data-ttu-id="c75b8-177">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-177">N/A</span></span>|  
|<span data-ttu-id="c75b8-178">należy wziąć pod uwagę zaakceptować — nagłówek</span><span class="sxs-lookup"><span data-stu-id="c75b8-178">consider-accept-header</span></span>|<span data-ttu-id="c75b8-179">Atrybut Hello musi być ustawiona tooone hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="c75b8-179">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c75b8-180">Jeśli żądanie XML w żądaniu nagłówek Accept - wartość true — mają zastosowanie konwersji.</span><span class="sxs-lookup"><span data-stu-id="c75b8-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="c75b8-181">— wartość false — Zawsze stosuj konwersji.</span><span class="sxs-lookup"><span data-stu-id="c75b8-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="c75b8-182">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-182">No</span></span>|<span data-ttu-id="c75b8-183">Wartość true</span><span class="sxs-lookup"><span data-stu-id="c75b8-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c75b8-184">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c75b8-184">Usage</span></span>  
 <span data-ttu-id="c75b8-185">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c75b8-185">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c75b8-186">**Sekcje zasad:** przychodzące, wychodzące, na błąd</span><span class="sxs-lookup"><span data-stu-id="c75b8-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="c75b8-187">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="c75b8-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c75b8-188"><a name="Findandreplacestringinbody"></a>Znajdowanie i zamienianie ciągów w treści</span><span class="sxs-lookup"><span data-stu-id="c75b8-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="c75b8-189">Witaj `find-and-replace` zasad znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.</span><span class="sxs-lookup"><span data-stu-id="c75b8-189">hello `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c75b8-190">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="c75b8-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="c75b8-191">Przykład</span><span class="sxs-lookup"><span data-stu-id="c75b8-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="c75b8-192">Elementy</span><span class="sxs-lookup"><span data-stu-id="c75b8-192">Elements</span></span>  
  
|<span data-ttu-id="c75b8-193">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-193">Name</span></span>|<span data-ttu-id="c75b8-194">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-194">Description</span></span>|<span data-ttu-id="c75b8-195">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c75b8-196">Znajdź i Zamień</span><span class="sxs-lookup"><span data-stu-id="c75b8-196">find-and-replace</span></span>|<span data-ttu-id="c75b8-197">Element główny.</span><span class="sxs-lookup"><span data-stu-id="c75b8-197">Root element.</span></span>|<span data-ttu-id="c75b8-198">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c75b8-199">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="c75b8-199">Attributes</span></span>  
  
|<span data-ttu-id="c75b8-200">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-200">Name</span></span>|<span data-ttu-id="c75b8-201">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-201">Description</span></span>|<span data-ttu-id="c75b8-202">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-202">Required</span></span>|<span data-ttu-id="c75b8-203">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c75b8-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c75b8-204">Z</span><span class="sxs-lookup"><span data-stu-id="c75b8-204">from</span></span>|<span data-ttu-id="c75b8-205">toosearch ciąg Hello dla.</span><span class="sxs-lookup"><span data-stu-id="c75b8-205">hello string toosearch for.</span></span>|<span data-ttu-id="c75b8-206">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-206">Yes</span></span>|<span data-ttu-id="c75b8-207">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-207">N/A</span></span>|  
|<span data-ttu-id="c75b8-208">na</span><span class="sxs-lookup"><span data-stu-id="c75b8-208">to</span></span>|<span data-ttu-id="c75b8-209">Witaj ciąg zastępczy.</span><span class="sxs-lookup"><span data-stu-id="c75b8-209">hello replacement string.</span></span> <span data-ttu-id="c75b8-210">Określ zero długość ciągu tooremove hello wyszukiwania ciąg zastępczy.</span><span class="sxs-lookup"><span data-stu-id="c75b8-210">Specify a zero length replacement string tooremove hello search string.</span></span>|<span data-ttu-id="c75b8-211">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-211">Yes</span></span>|<span data-ttu-id="c75b8-212">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c75b8-213">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c75b8-213">Usage</span></span>  
 <span data-ttu-id="c75b8-214">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c75b8-214">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c75b8-215">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="c75b8-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="c75b8-216">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="c75b8-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c75b8-217"><a name="MaskURLSContent"></a>Adresy URL maski w zawartości</span><span class="sxs-lookup"><span data-stu-id="c75b8-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="c75b8-218">Witaj `redirect-content-urls` zasad ponownie zapisuje łącza (maski) w treści odpowiedzi hello tak, aby wskazywały toohello równoważne połączenie za pośrednictwem bramy hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-218">hello `redirect-content-urls` policy re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span> <span data-ttu-id="c75b8-219">Są używane w hello wychodzącego sekcji toore zapisu odpowiedzi treści łącza toomake toohello punktu bramy.</span><span class="sxs-lookup"><span data-stu-id="c75b8-219">Use in hello outbound section toore-write response body links toomake them point toohello gateway.</span></span> <span data-ttu-id="c75b8-220">Użyj w hello ruchu przychodzącego sekcji odwrotny efekt.</span><span class="sxs-lookup"><span data-stu-id="c75b8-220">Use in hello inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c75b8-221">Ta zasada nie zmienia żadnych wartości nagłówka takich `Location` nagłówków.</span><span class="sxs-lookup"><span data-stu-id="c75b8-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="c75b8-222">wartości nagłówka toochange, użyj hello [nagłówka set](api-management-transformation-policies.md#SetHTTPheader) zasad.</span><span class="sxs-lookup"><span data-stu-id="c75b8-222">toochange header values, use hello [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c75b8-223">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="c75b8-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="c75b8-224">Przykład</span><span class="sxs-lookup"><span data-stu-id="c75b8-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="c75b8-225">Elementy</span><span class="sxs-lookup"><span data-stu-id="c75b8-225">Elements</span></span>  
  
|<span data-ttu-id="c75b8-226">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-226">Name</span></span>|<span data-ttu-id="c75b8-227">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-227">Description</span></span>|<span data-ttu-id="c75b8-228">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c75b8-229">adresy URL zawartości przekierowań</span><span class="sxs-lookup"><span data-stu-id="c75b8-229">redirect-content-urls</span></span>|<span data-ttu-id="c75b8-230">Element główny.</span><span class="sxs-lookup"><span data-stu-id="c75b8-230">Root element.</span></span>|<span data-ttu-id="c75b8-231">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c75b8-232">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c75b8-232">Usage</span></span>  
 <span data-ttu-id="c75b8-233">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c75b8-233">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c75b8-234">**Sekcje zasad:** przychodzące, wychodzące</span><span class="sxs-lookup"><span data-stu-id="c75b8-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="c75b8-235">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="c75b8-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c75b8-236"><a name="SetBackendService"></a>Ustawianie usługi wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="c75b8-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="c75b8-237">Użyj hello `set-backend-service` tooredirect zasad przychodzącego żądania tooa różnych wewnętrznej bazy danych niż hello określonego w ustawieniach hello interfejsu API dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="c75b8-237">Use hello `set-backend-service` policy tooredirect an incoming request tooa different backend than hello one specified in hello API settings for that operation.</span></span> <span data-ttu-id="c75b8-238">Ta zasada zmienia hello wewnętrznej bazy danych usługi podstawowy adres URL hello przychodzącego żądania toohello jednym określonym w zasadach hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-238">This policy changes hello backend service base URL of hello incoming request toohello one specified in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c75b8-239">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="c75b8-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="c75b8-240">Przykład</span><span class="sxs-lookup"><span data-stu-id="c75b8-240">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="c75b8-241">W tym hello przykład zasad usługi wewnętrznej bazy danych dla zestawu kieruje żądania na podstawie wartości wersji hello przekazano hello zapytania ciąg tooa różnych wewnętrznej bazy danych usługi niż hello hello określony w jednej z interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c75b8-241">In this example hello set backend service policy routes requests based on hello version value passed in hello query string tooa different backend service than hello one specified in hello API.</span></span>
  
<span data-ttu-id="c75b8-242">Początkowo hello podstawowy adres URL usługi wewnętrznej bazy danych jest pochodną hello ustawień interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c75b8-242">Initially hello backend service base URL is derived from hello API settings.</span></span> <span data-ttu-id="c75b8-243">Dlatego hello adresu URL żądania `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` staje się `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` gdzie `http://contoso.com/api/10.4/` hello wewnętrznej bazy danych usługi adresu URL określonego w ustawieniach hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c75b8-243">So hello request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is hello backend service URL specified in hello API settings.</span></span>  
  
<span data-ttu-id="c75b8-244">Gdy hello [< Wybierz\> ](api-management-advanced-policies.md#choose) deklaracji zasad są stosowane hello wewnętrznej bazy danych usługi podstawowy adres URL może zmienić ponownie albo zbyt`http://contoso.com/api/8.2` lub `http://contoso.com/api/9.1`, w zależności od hello wartość parametru zapytania żądania hello w wersji.</span><span class="sxs-lookup"><span data-stu-id="c75b8-244">When hello [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied hello backend service base URL may change again either too`http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on hello value of hello version request query parameter.</span></span> <span data-ttu-id="c75b8-245">Na przykład jeśli hello jest wartość `"2013-15"` hello żądania końcowego adresu URL staje się `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="c75b8-245">For example, if hello value is `"2013-15"` hello final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="c75b8-246">Jeśli dodatkowo przekształcenie żądania hello jest żądany, inne [zasad przekształcania](api-management-transformation-policies.md#TransformationPolicies) mogą być używane.</span><span class="sxs-lookup"><span data-stu-id="c75b8-246">If further transformation of hello request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="c75b8-247">Na przykład tooremove hello wersji zapytania parametru skoro hello żądanie jest kierowane tooa zaplecza określonej wersji, hello [ustawić parametr ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) zasadę można następnie atrybut version nadmiarowe obecnie hello tooremove używane.</span><span class="sxs-lookup"><span data-stu-id="c75b8-247">For example, tooremove hello version query parameter now that hello request is being routed tooa version specific backend, hello  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used tooremove hello now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="c75b8-248">Przykład</span><span class="sxs-lookup"><span data-stu-id="c75b8-248">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="c75b8-249">W tym przykładzie hello zasad trasy hello żądania tooa usługi sieci szkieletowej zapleczu przy użyciu ciągu zapytania identyfikatora userId hello jako klucza partycji hello i hello repliki podstawowej hello partycji.</span><span class="sxs-lookup"><span data-stu-id="c75b8-249">In this example hello policy routes hello request tooa service fabric backend, using hello userId query string as hello partition key and using hello primary replica of hello partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="c75b8-250">Elementy</span><span class="sxs-lookup"><span data-stu-id="c75b8-250">Elements</span></span>  
  
|<span data-ttu-id="c75b8-251">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-251">Name</span></span>|<span data-ttu-id="c75b8-252">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-252">Description</span></span>|<span data-ttu-id="c75b8-253">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c75b8-254">zestaw wewnętrznej bazy danych usługi</span><span class="sxs-lookup"><span data-stu-id="c75b8-254">set-backend-service</span></span>|<span data-ttu-id="c75b8-255">Element główny.</span><span class="sxs-lookup"><span data-stu-id="c75b8-255">Root element.</span></span>|<span data-ttu-id="c75b8-256">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c75b8-257">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="c75b8-257">Attributes</span></span>  
  
|<span data-ttu-id="c75b8-258">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-258">Name</span></span>|<span data-ttu-id="c75b8-259">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-259">Description</span></span>|<span data-ttu-id="c75b8-260">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-260">Required</span></span>|<span data-ttu-id="c75b8-261">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c75b8-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c75b8-262">adres url Base</span><span class="sxs-lookup"><span data-stu-id="c75b8-262">base-url</span></span>|<span data-ttu-id="c75b8-263">Nowego zaplecza podstawowy adres URL usługi.</span><span class="sxs-lookup"><span data-stu-id="c75b8-263">New backend service base URL.</span></span>|<span data-ttu-id="c75b8-264">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-264">No</span></span>|<span data-ttu-id="c75b8-265">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-265">N/A</span></span>|  
|<span data-ttu-id="c75b8-266">Identyfikator wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="c75b8-266">backend-id</span></span>|<span data-ttu-id="c75b8-267">Identyfikator hello tooroute wewnętrznej bazy danych do.</span><span class="sxs-lookup"><span data-stu-id="c75b8-267">Identifier of hello backend tooroute to.</span></span>|<span data-ttu-id="c75b8-268">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-268">No</span></span>|<span data-ttu-id="c75b8-269">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-269">N/A</span></span>|  
|<span data-ttu-id="c75b8-270">rz partycji klucza</span><span class="sxs-lookup"><span data-stu-id="c75b8-270">sf-partition-key</span></span>|<span data-ttu-id="c75b8-271">Dotyczy tylko gdy hello wewnętrznej bazy danych to usługa sieci szkieletowej usług i jest określona za pomocą "wewnętrznej bazy danych id".</span><span class="sxs-lookup"><span data-stu-id="c75b8-271">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="c75b8-272">Używane tooresolve określonej partycji z usługi rozpoznawania nazw hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-272">Used tooresolve a specific partition from hello name resolution service.</span></span>|<span data-ttu-id="c75b8-273">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-273">No</span></span>|<span data-ttu-id="c75b8-274">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-274">N/A</span></span>|  
|<span data-ttu-id="c75b8-275">rz repliki typu</span><span class="sxs-lookup"><span data-stu-id="c75b8-275">sf-replica-type</span></span>|<span data-ttu-id="c75b8-276">Dotyczy tylko gdy hello wewnętrznej bazy danych to usługa sieci szkieletowej usług i jest określona za pomocą "wewnętrznej bazy danych id".</span><span class="sxs-lookup"><span data-stu-id="c75b8-276">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="c75b8-277">Kontroluje, czy powinien pojawiać się żądania hello toohello podstawowej lub pomocniczej replice partycji.</span><span class="sxs-lookup"><span data-stu-id="c75b8-277">Controls if hello request should go toohello primary or secondary replica of a partition.</span></span> |<span data-ttu-id="c75b8-278">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-278">No</span></span>|<span data-ttu-id="c75b8-279">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-279">N/A</span></span>|    
|<span data-ttu-id="c75b8-280">rz resolve warunków</span><span class="sxs-lookup"><span data-stu-id="c75b8-280">sf-resolve-condition</span></span>|<span data-ttu-id="c75b8-281">Dotyczy tylko gdy hello wewnętrznej bazy danych to usługa sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="c75b8-281">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="c75b8-282">Identyfikowanie warunku hello rozmowy telefonicznej tooService sieci szkieletowej wewnętrznej bazy danych ma toobe powtarzany z nowego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-282">Condition identifying if hello call tooService Fabric backend has toobe repeated with new resolution.</span></span>|<span data-ttu-id="c75b8-283">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-283">No</span></span>|<span data-ttu-id="c75b8-284">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-284">N/A</span></span>|    
|<span data-ttu-id="c75b8-285">rz usługi wystąpienie nazwa-</span><span class="sxs-lookup"><span data-stu-id="c75b8-285">sf-service-instance-name</span></span>|<span data-ttu-id="c75b8-286">Dotyczy tylko gdy hello wewnętrznej bazy danych to usługa sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="c75b8-286">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="c75b8-287">Umożliwia toochange wystąpień usługi w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-287">Allows toochange service instances at runtime.</span></span> |<span data-ttu-id="c75b8-288">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-288">No</span></span>|<span data-ttu-id="c75b8-289">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="c75b8-290">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c75b8-290">Usage</span></span>  
 <span data-ttu-id="c75b8-291">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c75b8-291">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c75b8-292">**Sekcje zasad:** wewnętrznej bazy danych dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="c75b8-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="c75b8-293">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="c75b8-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c75b8-294"><a name="SetBody"></a>Zestaw treści</span><span class="sxs-lookup"><span data-stu-id="c75b8-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="c75b8-295">Użyj hello `set-body` treści wiadomości powitania tooset zasad żądań przychodzących i wychodzących.</span><span class="sxs-lookup"><span data-stu-id="c75b8-295">Use hello `set-body` policy tooset hello message body for incoming and outgoing requests.</span></span> <span data-ttu-id="c75b8-296">tooaccess hello treści wiadomości, można użyć hello `context.Request.Body` właściwości lub hello `context.Response.Body`, w zależności od tego, czy zasady hello jest hello sekcji ruchu przychodzącego lub wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="c75b8-296">tooaccess hello message body you can use hello `context.Request.Body` property or hello `context.Response.Body`, depending on whether hello policy is in hello inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="c75b8-297">Należy pamiętać, że domyślnie, gdy uzyskujesz dostęp do hello przy użyciu treści komunikatu `context.Request.Body` lub `context.Response.Body`, oryginalnej wiadomości powitania treści zostaną utracone i musi być ustawione przez zwrócenie treści hello Wstecz w wyrażeniu hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-297">Note that by default when you access hello message body using `context.Request.Body` or `context.Response.Body`, hello original message body is lost and must be set by returning hello body back in hello expression.</span></span> <span data-ttu-id="c75b8-298">Treść hello toopreserve zawartości, ustaw hello `preserveContent` parametru zbyt`true` podczas uzyskiwania dostępu do wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-298">toopreserve hello body content, set hello `preserveContent` parameter too`true` when accessing hello message.</span></span> <span data-ttu-id="c75b8-299">Jeśli `preserveContent` ustawiono zbyt`true` i różnych treści jest zwracany przez wyrażenie hello hello zwrócił treści jest używany.</span><span class="sxs-lookup"><span data-stu-id="c75b8-299">If `preserveContent` is set too`true` and a different body is returned by hello expression, hello returned body is used.</span></span>  
>   
>  <span data-ttu-id="c75b8-300">Należy pamiętać, hello następujące zagadnienia, korzystając z hello `set-body` zasad.</span><span class="sxs-lookup"><span data-stu-id="c75b8-300">Please note hello following considerations when using hello `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="c75b8-301">Jeśli używasz hello `set-body` tooreturn zasad nowych lub zaktualizowanych treści, nie potrzebujesz tooset `preserveContent` zbyt`true` ponieważ są jawnie dostarczanie hello nowej zawartości w treści.</span><span class="sxs-lookup"><span data-stu-id="c75b8-301">If you are using hello `set-body` policy tooreturn a new or updated body you don't need tooset `preserveContent` too`true` because you are explicitly supplying hello new body contents.</span></span>  
> -   <span data-ttu-id="c75b8-302">Zachowywanie hello treści odpowiedzi w potoku przychodzącego hello sensu ponieważ nie istnieje jeszcze żadnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="c75b8-302">Preserving hello content of a response in hello inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="c75b8-303">Zachowywanie hello zawartości żądania w potoku wychodzącego hello nie sensu, ponieważ Żądanie hello została już wysłana toohello wewnętrznej bazy danych w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="c75b8-303">Preserving hello content of a request in hello outbound pipeline doesn't make sense because hello request has already been sent toohello backend at this point.</span></span>  
> -   <span data-ttu-id="c75b8-304">Jeśli zasada ta jest używana, gdy brak treści wiadomości, na przykład w przychodzącej GET, jest zwracany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="c75b8-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="c75b8-305">Aby uzyskać więcej informacji, zobacz hello `context.Request.Body`, `context.Response.Body`i hello `IMessage` części hello [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables) tabeli.</span><span class="sxs-lookup"><span data-stu-id="c75b8-305">For more information, see hello `context.Request.Body`, `context.Response.Body`, and hello `IMessage` sections in hello [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c75b8-306">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="c75b8-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="c75b8-307">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c75b8-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="c75b8-308">Przykład literału tekstu</span><span class="sxs-lookup"><span data-stu-id="c75b8-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a><span data-ttu-id="c75b8-309">Przykład dostęp do treści hello jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="c75b8-309">Example accessing hello body as a string.</span></span> <span data-ttu-id="c75b8-310">Należy pamiętać, że są firma Microsoft zachowuje hello oryginalnego treści żądania, aby firma Microsoft dostęp do niego później w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-310">Note that we are preserving hello original request body so that we can access it later in hello pipeline.</span></span>
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a><span data-ttu-id="c75b8-311">Przykład dostęp do treści hello jako JObject.</span><span class="sxs-lookup"><span data-stu-id="c75b8-311">Example accessing hello body as a JObject.</span></span> <span data-ttu-id="c75b8-312">Należy pamiętać, że od czasu firma Microsoft nie są rezerwowania hello oryginalnego treści żądania później w potoku hello spowoduje wyjątek w celu dostępu.</span><span class="sxs-lookup"><span data-stu-id="c75b8-312">Note that since we are not reserving hello original request body, accesing it later in hello pipeline will result in an exception.</span></span>  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="c75b8-313">Filtrowanie oparte na produktu odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="c75b8-313">Filter response based on product</span></span>  
 <span data-ttu-id="c75b8-314">W tym przykładzie pokazano, jak tooperform filtrowanie zawartości przez usunięcie elementów danych z hello odpowiedzi otrzymanych od hello usługi wewnętrznej bazy danych przy użyciu hello `Starter` produktu.</span><span class="sxs-lookup"><span data-stu-id="c75b8-314">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="c75b8-315">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too34:30.</span><span class="sxs-lookup"><span data-stu-id="c75b8-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="c75b8-316">Rozpocznij od 31:50 toosee omówienie [hello ciemny niebo prognozy API](https://developer.forecast.io/) używane na potrzeby tego pokazu.</span><span class="sxs-lookup"><span data-stu-id="c75b8-316">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="c75b8-317">Za pomocą szablonów płynne o treści zestawu</span><span class="sxs-lookup"><span data-stu-id="c75b8-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="c75b8-318">Witaj `set-body` zasad może być skonfigurowany toouse hello [płynne](https://shopify.github.io/liquid/basics/introduction/) tworzenia szablonów języka tootransfom hello treści żądania lub odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="c75b8-318">hello `set-body` policy can be configured toouse hello [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language tootransfom hello body of a request or response.</span></span> <span data-ttu-id="c75b8-319">Może to być bardzo skuteczne, jeśli potrzebujesz toocompletely Przekształć hello format wiadomości.</span><span class="sxs-lookup"><span data-stu-id="c75b8-319">This can be very effective if you need toocompletely reshape hello format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c75b8-320">Witaj implementacji płynnych używane w hello `set-body` zasada jest skonfigurowana w trybie"C#".</span><span class="sxs-lookup"><span data-stu-id="c75b8-320">hello implementation of Liquid used in hello `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="c75b8-321">Jest to szczególnie ważne podczas wykonywania czynności takich jak filtrowania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="c75b8-322">Na przykład przy użyciu filtru daty wymaga użycia hello Pascal wielkości liter i C# Data formatowania, np.:</span><span class="sxs-lookup"><span data-stu-id="c75b8-322">As an example, using a date filter requires hello use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="c75b8-323">{{body.foo.startDateTime| Data: "yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="c75b8-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c75b8-324">W kolejności toocorrectly bind tooan treści XML przy użyciu szablonu płynne hello, użyj `set-header` tooeither tooset Content-Type zasad application/xml, tekstu/xml (lub dowolnego typu kończąc + xml); treść kodu JSON, musi być application/json (tekstu/json lub zakończenia dowolnego typu z + json).</span><span class="sxs-lookup"><span data-stu-id="c75b8-324">In order toocorrectly bind tooan XML body using hello Liquid template, use a `set-header` policy tooset Content-Type tooeither application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-toosoap-using-a-liquid-template"></a><span data-ttu-id="c75b8-325">Konwertuj tooSOAP JSON przy użyciu szablonu płynne</span><span class="sxs-lookup"><span data-stu-id="c75b8-325">Convert JSON tooSOAP using a Liquid template</span></span>
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="c75b8-326">Tranform ciągu JSON przy użyciu szablonu płynne</span><span class="sxs-lookup"><span data-stu-id="c75b8-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="c75b8-327">Elementy</span><span class="sxs-lookup"><span data-stu-id="c75b8-327">Elements</span></span>  
  
|<span data-ttu-id="c75b8-328">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-328">Name</span></span>|<span data-ttu-id="c75b8-329">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-329">Description</span></span>|<span data-ttu-id="c75b8-330">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c75b8-331">zestaw treści</span><span class="sxs-lookup"><span data-stu-id="c75b8-331">set-body</span></span>|<span data-ttu-id="c75b8-332">Element główny.</span><span class="sxs-lookup"><span data-stu-id="c75b8-332">Root element.</span></span> <span data-ttu-id="c75b8-333">Zawiera treść hello lub wyrażeń, które zwraca treści.</span><span class="sxs-lookup"><span data-stu-id="c75b8-333">Contains hello body text or an expressions that returns a body.</span></span>|<span data-ttu-id="c75b8-334">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="c75b8-335">Właściwości</span><span class="sxs-lookup"><span data-stu-id="c75b8-335">Properties</span></span>  
  
|<span data-ttu-id="c75b8-336">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-336">Name</span></span>|<span data-ttu-id="c75b8-337">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-337">Description</span></span>|<span data-ttu-id="c75b8-338">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-338">Required</span></span>|<span data-ttu-id="c75b8-339">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c75b8-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c75b8-340">szablon</span><span class="sxs-lookup"><span data-stu-id="c75b8-340">template</span></span>|<span data-ttu-id="c75b8-341">Tryb tworzenia szablonów hello toochange używane hello zestaw treści zasad będą uruchamiane w.</span><span class="sxs-lookup"><span data-stu-id="c75b8-341">Used toochange hello templating mode that hello set body policy will run in.</span></span> <span data-ttu-id="c75b8-342">Obecnie jest hello tylko obsługiwane wartości:</span><span class="sxs-lookup"><span data-stu-id="c75b8-342">Currently hello only supported value is:</span></span><br /><br /><span data-ttu-id="c75b8-343">-płynne - hello zestaw treści zasad użyje hello płynne tworzenia szablonów aparatu</span><span class="sxs-lookup"><span data-stu-id="c75b8-343">- liquid - hello set body policy will use hello liquid templating engine</span></span> |<span data-ttu-id="c75b8-344">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-344">No</span></span>|<span data-ttu-id="c75b8-345">płynnych</span><span class="sxs-lookup"><span data-stu-id="c75b8-345">liquid</span></span>|  

<span data-ttu-id="c75b8-346">Do uzyskiwania dostępu do informacji na temat hello żądań i odpowiedzi, hello płynne szablonu można powiązać obiektu context tooa hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="c75b8-346">For accessing information about hello request and response, hello Liquid template can bind tooa context object with hello following properties:</span></span> <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a><span data-ttu-id="c75b8-347">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c75b8-347">Usage</span></span>  
 <span data-ttu-id="c75b8-348">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c75b8-348">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c75b8-349">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="c75b8-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="c75b8-350">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="c75b8-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c75b8-351"><a name="SetHTTPheader"></a>Set — nagłówek HTTP</span><span class="sxs-lookup"><span data-stu-id="c75b8-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="c75b8-352">Witaj `set-header` zasad przypisuje wartość tooan istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-352">hello `set-header` policy assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="c75b8-353">Wstawia listę nagłówków HTTP do wiadomości HTTP.</span><span class="sxs-lookup"><span data-stu-id="c75b8-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="c75b8-354">Po umieszczeniu w potoku dla ruchu przychodzącego, ta zasada ustawia hello nagłówków HTTP dla żądania hello przekazywany toohello usługi docelowej.</span><span class="sxs-lookup"><span data-stu-id="c75b8-354">When placed in an inbound pipeline, this policy sets hello HTTP headers for hello request being passed toohello target service.</span></span> <span data-ttu-id="c75b8-355">Po umieszczeniu w potoku wychodzącego, ta zasada ustawia nagłówki HTTP hello hello odpowiedzi wysyłane klienta toohello bramy.</span><span class="sxs-lookup"><span data-stu-id="c75b8-355">When placed in an outbound pipeline, this policy sets hello HTTP headers for hello response being sent toohello gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c75b8-356">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="c75b8-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="c75b8-357">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c75b8-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="c75b8-358">Przykład</span><span class="sxs-lookup"><span data-stu-id="c75b8-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="c75b8-359">Kontekst informacji toohello wewnętrznej bazy danych usługi przekazywania</span><span class="sxs-lookup"><span data-stu-id="c75b8-359">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="c75b8-360">Ten przykład przedstawia, jak zasady tooapply na powitania interfejsu API na poziomie toosupply kontekstu informacji toohello wewnętrznej bazy danych usługi.</span><span class="sxs-lookup"><span data-stu-id="c75b8-360">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="c75b8-361">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too10:30.</span><span class="sxs-lookup"><span data-stu-id="c75b8-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="c75b8-362">Na 12:10 istnieje pokaz wywołanie operacji w portalu dla deweloperów hello umożliwia wyświetlenie zasad hello w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="c75b8-362">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="c75b8-363">Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="c75b8-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="c75b8-364">Elementy</span><span class="sxs-lookup"><span data-stu-id="c75b8-364">Elements</span></span>  
  
|<span data-ttu-id="c75b8-365">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-365">Name</span></span>|<span data-ttu-id="c75b8-366">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-366">Description</span></span>|<span data-ttu-id="c75b8-367">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c75b8-368">set — nagłówek</span><span class="sxs-lookup"><span data-stu-id="c75b8-368">set-header</span></span>|<span data-ttu-id="c75b8-369">Element główny.</span><span class="sxs-lookup"><span data-stu-id="c75b8-369">Root element.</span></span>|<span data-ttu-id="c75b8-370">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-370">Yes</span></span>|  
|<span data-ttu-id="c75b8-371">wartość</span><span class="sxs-lookup"><span data-stu-id="c75b8-371">value</span></span>|<span data-ttu-id="c75b8-372">Określa wartość hello hello nagłówka toobe zestawu.</span><span class="sxs-lookup"><span data-stu-id="c75b8-372">Specifies hello value of hello header toobe set.</span></span> <span data-ttu-id="c75b8-373">Wiele nagłówków o hello tej samej nazwy dodanie dodatkowych `value` elementów.</span><span class="sxs-lookup"><span data-stu-id="c75b8-373">For multiple headers with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="c75b8-374">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="c75b8-375">Właściwości</span><span class="sxs-lookup"><span data-stu-id="c75b8-375">Properties</span></span>  
  
|<span data-ttu-id="c75b8-376">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-376">Name</span></span>|<span data-ttu-id="c75b8-377">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-377">Description</span></span>|<span data-ttu-id="c75b8-378">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-378">Required</span></span>|<span data-ttu-id="c75b8-379">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c75b8-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c75b8-380">istnieje akcja</span><span class="sxs-lookup"><span data-stu-id="c75b8-380">exists-action</span></span>|<span data-ttu-id="c75b8-381">Określa jaki tootake akcji, gdy nagłówek hello został już określony.</span><span class="sxs-lookup"><span data-stu-id="c75b8-381">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="c75b8-382">Ten atrybut musi mieć jedną z hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="c75b8-382">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="c75b8-383">-- zastępuje hello wartość zastępczą hello istniejący nagłówek.</span><span class="sxs-lookup"><span data-stu-id="c75b8-383">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="c75b8-384">-skip — nie zastępuje istniejącą wartość nagłówka hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-384">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="c75b8-385">-dołączania - dołącza hello wartość toohello istniejącą wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="c75b8-385">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="c75b8-386">-Usunięcie — usuwa hello nagłówek z żądania hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-386">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="c75b8-387">Gdy ustawiona zbyt`override` rejestrowanie wiele wpisów z hello sama nazwa wyniki w nagłówku hello jest zestaw zgodnie z tooall zapisów (które zostaną wyświetlone wiele razy); w wyniku hello zostanie ustawiona tylko wartości wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="c75b8-387">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="c75b8-388">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-388">No</span></span>|<span data-ttu-id="c75b8-389">zastąpienie</span><span class="sxs-lookup"><span data-stu-id="c75b8-389">override</span></span>|  
|<span data-ttu-id="c75b8-390">name</span><span class="sxs-lookup"><span data-stu-id="c75b8-390">name</span></span>|<span data-ttu-id="c75b8-391">Określa nazwę zestawu toobe hello nagłówka.</span><span class="sxs-lookup"><span data-stu-id="c75b8-391">Specifies name of hello header toobe set.</span></span>|<span data-ttu-id="c75b8-392">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-392">Yes</span></span>|<span data-ttu-id="c75b8-393">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c75b8-394">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c75b8-394">Usage</span></span>  
 <span data-ttu-id="c75b8-395">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c75b8-395">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c75b8-396">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="c75b8-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="c75b8-397">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="c75b8-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c75b8-398"><a name="SetQueryStringParameter"></a>Parametr ciągu zapytania dla zestawu</span><span class="sxs-lookup"><span data-stu-id="c75b8-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="c75b8-399">Witaj `set-query-parameter` zasad dodaje wartość zastępuje, lub usuwa żądania parametru ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-399">hello `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="c75b8-400">Może być używane toopass oczekiwany przez usługi zaplecza hello parametry zapytania, które są opcjonalne lub nigdy nie są obecne w żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-400">Can be used toopass query parameters expected by hello backend service which are optional or never present in hello request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c75b8-401">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="c75b8-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="c75b8-402">Przykłady</span><span class="sxs-lookup"><span data-stu-id="c75b8-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="c75b8-403">Przykład</span><span class="sxs-lookup"><span data-stu-id="c75b8-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="c75b8-404">Kontekst informacji toohello wewnętrznej bazy danych usługi przekazywania</span><span class="sxs-lookup"><span data-stu-id="c75b8-404">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="c75b8-405">Ten przykład przedstawia, jak zasady tooapply na powitania interfejsu API na poziomie toosupply kontekstu informacji toohello wewnętrznej bazy danych usługi.</span><span class="sxs-lookup"><span data-stu-id="c75b8-405">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="c75b8-406">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too10:30.</span><span class="sxs-lookup"><span data-stu-id="c75b8-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="c75b8-407">Na 12:10 istnieje pokaz wywołanie operacji w portalu dla deweloperów hello umożliwia wyświetlenie zasad hello w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="c75b8-407">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="c75b8-408">Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="c75b8-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="c75b8-409">Elementy</span><span class="sxs-lookup"><span data-stu-id="c75b8-409">Elements</span></span>  
  
|<span data-ttu-id="c75b8-410">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-410">Name</span></span>|<span data-ttu-id="c75b8-411">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-411">Description</span></span>|<span data-ttu-id="c75b8-412">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c75b8-413">Parametr zestawu — zapytania</span><span class="sxs-lookup"><span data-stu-id="c75b8-413">set-query-parameter</span></span>|<span data-ttu-id="c75b8-414">Element główny.</span><span class="sxs-lookup"><span data-stu-id="c75b8-414">Root element.</span></span>|<span data-ttu-id="c75b8-415">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-415">Yes</span></span>|  
|<span data-ttu-id="c75b8-416">wartość</span><span class="sxs-lookup"><span data-stu-id="c75b8-416">value</span></span>|<span data-ttu-id="c75b8-417">Określa wartość hello zestawu toobe parametru zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-417">Specifies hello value of hello query parameter toobe set.</span></span> <span data-ttu-id="c75b8-418">Wiele parametrów zapytania z hello tej samej nazwy dodanie dodatkowych `value` elementów.</span><span class="sxs-lookup"><span data-stu-id="c75b8-418">For multiple query parameters with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="c75b8-419">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="c75b8-420">Właściwości</span><span class="sxs-lookup"><span data-stu-id="c75b8-420">Properties</span></span>  
  
|<span data-ttu-id="c75b8-421">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-421">Name</span></span>|<span data-ttu-id="c75b8-422">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-422">Description</span></span>|<span data-ttu-id="c75b8-423">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-423">Required</span></span>|<span data-ttu-id="c75b8-424">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c75b8-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c75b8-425">istnieje akcja</span><span class="sxs-lookup"><span data-stu-id="c75b8-425">exists-action</span></span>|<span data-ttu-id="c75b8-426">Określa jaki tootake akcji, gdy parametr zapytania hello jest już określony.</span><span class="sxs-lookup"><span data-stu-id="c75b8-426">Specifies what action tootake when hello query parameter is already specified.</span></span> <span data-ttu-id="c75b8-427">Ten atrybut musi mieć jedną z hello następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="c75b8-427">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="c75b8-428">-- zastępuje hello wartość zastąpienia istniejącego parametru hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-428">-   override - replaces hello value of hello existing parameter.</span></span><br /><span data-ttu-id="c75b8-429">-skip — nie zastępuje hello istniejącą wartość parametru zapytania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-429">-   skip - does not replace hello existing query parameter value.</span></span><br /><span data-ttu-id="c75b8-430">-dołączania - dołącza hello wartość toohello istniejącą wartość parametru zapytania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-430">-   append - appends hello value toohello existing query parameter value.</span></span><br /><span data-ttu-id="c75b8-431">-Usunięcie — usuwa parametru zapytania hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-431">-   delete - removes hello query parameter from hello request.</span></span><br /><br /> <span data-ttu-id="c75b8-432">Gdy ustawiona zbyt`override` rejestrowanie wiele wpisów z hello sama nazwa powoduje parametru zapytania hello jest zestaw zgodnie z tooall zapisów (które zostaną wyświetlone wiele razy); w wyniku hello zostanie ustawiona tylko wartości wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="c75b8-432">When set too`override` enlisting multiple entries with hello same name results in hello query parameter being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="c75b8-433">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-433">No</span></span>|<span data-ttu-id="c75b8-434">zastąpienie</span><span class="sxs-lookup"><span data-stu-id="c75b8-434">override</span></span>|  
|<span data-ttu-id="c75b8-435">name</span><span class="sxs-lookup"><span data-stu-id="c75b8-435">name</span></span>|<span data-ttu-id="c75b8-436">Określa nazwę zestawu toobe parametru zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="c75b8-436">Specifies name of hello query parameter toobe set.</span></span>|<span data-ttu-id="c75b8-437">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-437">Yes</span></span>|<span data-ttu-id="c75b8-438">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c75b8-439">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c75b8-439">Usage</span></span>  
 <span data-ttu-id="c75b8-440">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c75b8-440">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c75b8-441">**Sekcje zasad:** wewnętrznej bazy danych dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="c75b8-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="c75b8-442">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="c75b8-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c75b8-443"><a name="RewriteURL"></a>Ponowne zapisywanie adresów URL</span><span class="sxs-lookup"><span data-stu-id="c75b8-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="c75b8-444">Witaj `rewrite-uri` zasad konwertuje adresie URL żądania w postaci toohello publicznego formularza oczekiwane przez usługę sieci web hello, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="c75b8-444">hello `rewrite-uri` policy converts a request URL from its public form toohello form expected by hello web service, as shown in hello following example.</span></span>  
  
-   <span data-ttu-id="c75b8-445">Publiczny adres URL-`http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="c75b8-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="c75b8-446">Adres URL żądania —`http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="c75b8-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="c75b8-447">Te zasady można podczas transformacji do formatu adresu URL hello oczekiwanego przez usługę sieci web hello człowieka i/lub przeglądarki przyjaznego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c75b8-447">This policy can be used when a human and/or browser-friendly URL should be transformed into hello URL format expected by hello web service.</span></span> <span data-ttu-id="c75b8-448">Ta zasada musi tylko toobe stosowane, gdy udostępnianie innego formatu adresu URL, takie jak czystą adresów URL, adresy URL RESTful, adresów URL przyjaznych dla użytkownika lub adresów URL przyjaznych dla aparatów wyszukiwania, które są całkowicie strukturalnych adresów URL, które zawiera ciąg zapytania i zamiast tego zawierają tylko hello ścieżka hello zasób (po hello schemat i urząd hello).</span><span class="sxs-lookup"><span data-stu-id="c75b8-448">This policy only needs toobe applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only hello path of hello resource (after hello scheme and hello authority).</span></span> <span data-ttu-id="c75b8-449">Często jest to estetycznych, użyteczność lub aparat wyszukiwania (SEO) optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="c75b8-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c75b8-450">Można dodawać tylko za pomocą zasad hello parametrów ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-450">You can only add query string parameters using hello policy.</span></span> <span data-ttu-id="c75b8-451">Nie można dodać dodatkowe szablonu ścieżki parametrów w hello ponowne zapisywanie adresów URL.</span><span class="sxs-lookup"><span data-stu-id="c75b8-451">You cannot add extra template path parameters in hello rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="c75b8-452">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="c75b8-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="c75b8-453">Przykład</span><span class="sxs-lookup"><span data-stu-id="c75b8-453">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a><span data-ttu-id="c75b8-454">Elementy</span><span class="sxs-lookup"><span data-stu-id="c75b8-454">Elements</span></span>  
  
|<span data-ttu-id="c75b8-455">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-455">Name</span></span>|<span data-ttu-id="c75b8-456">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-456">Description</span></span>|<span data-ttu-id="c75b8-457">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c75b8-458">Identyfikator uri ponownego napisania</span><span class="sxs-lookup"><span data-stu-id="c75b8-458">rewrite-uri</span></span>|<span data-ttu-id="c75b8-459">Element główny.</span><span class="sxs-lookup"><span data-stu-id="c75b8-459">Root element.</span></span>|<span data-ttu-id="c75b8-460">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c75b8-461">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="c75b8-461">Attributes</span></span>  
  
|<span data-ttu-id="c75b8-462">Atrybut</span><span class="sxs-lookup"><span data-stu-id="c75b8-462">Attribute</span></span>|<span data-ttu-id="c75b8-463">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-463">Description</span></span>|<span data-ttu-id="c75b8-464">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-464">Required</span></span>|<span data-ttu-id="c75b8-465">Domyślne</span><span class="sxs-lookup"><span data-stu-id="c75b8-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="c75b8-466">szablon</span><span class="sxs-lookup"><span data-stu-id="c75b8-466">template</span></span>|<span data-ttu-id="c75b8-467">Hello web rzeczywisty adres URL usługi z parametrów ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="c75b8-467">hello actual web service URL with any query string parameters.</span></span> <span data-ttu-id="c75b8-468">Używając wyrażenia wartości całkowitej hello musi być wyrażeniem.</span><span class="sxs-lookup"><span data-stu-id="c75b8-468">When using expressions, hello whole value must be an expression.</span></span>|<span data-ttu-id="c75b8-469">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-469">Yes</span></span>|<span data-ttu-id="c75b8-470">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="c75b8-470">N/A</span></span>|  
|<span data-ttu-id="c75b8-471">Kopiuj niedopasowane — parametry</span><span class="sxs-lookup"><span data-stu-id="c75b8-471">copy-unmatched-params</span></span>|<span data-ttu-id="c75b8-472">Określa, czy parametry zapytania w hello żądania przychodzącego, jeśli nie znajduje się w oryginalnym szablonie adresu URL hello są dodawane toohello adres URL zdefiniowany przez hello ponownie zapisać szablon</span><span class="sxs-lookup"><span data-stu-id="c75b8-472">Specifies whether query parameters in hello incoming request not present in hello original URL template are added toohello URL defined by hello re-write template</span></span>|<span data-ttu-id="c75b8-473">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-473">No</span></span>|<span data-ttu-id="c75b8-474">Wartość true</span><span class="sxs-lookup"><span data-stu-id="c75b8-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c75b8-475">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c75b8-475">Usage</span></span>  
 <span data-ttu-id="c75b8-476">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c75b8-476">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c75b8-477">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="c75b8-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="c75b8-478">**Zakresy zasad:** operacja produktu, interfejsu API,</span><span class="sxs-lookup"><span data-stu-id="c75b8-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="c75b8-479"><a name="XSLTransform"></a>Przekształcanie XML za pomocą XSLT</span><span class="sxs-lookup"><span data-stu-id="c75b8-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="c75b8-480">Witaj `Transform XML using an XSLT` tooXML transformacji XSL w treści żądania lub odpowiedzi hello dotyczą zasady.</span><span class="sxs-lookup"><span data-stu-id="c75b8-480">hello `Transform XML using an XSLT` policy applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c75b8-481">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="c75b8-481">Policy statement</span></span>  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a><span data-ttu-id="c75b8-482">Przykład</span><span class="sxs-lookup"><span data-stu-id="c75b8-482">Example</span></span>  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="c75b8-483">Elementy</span><span class="sxs-lookup"><span data-stu-id="c75b8-483">Elements</span></span>  
  
|<span data-ttu-id="c75b8-484">Nazwa</span><span class="sxs-lookup"><span data-stu-id="c75b8-484">Name</span></span>|<span data-ttu-id="c75b8-485">Opis</span><span class="sxs-lookup"><span data-stu-id="c75b8-485">Description</span></span>|<span data-ttu-id="c75b8-486">Wymagane</span><span class="sxs-lookup"><span data-stu-id="c75b8-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c75b8-487">Transformacja XSL</span><span class="sxs-lookup"><span data-stu-id="c75b8-487">xsl-transform</span></span>|<span data-ttu-id="c75b8-488">Element główny.</span><span class="sxs-lookup"><span data-stu-id="c75b8-488">Root element.</span></span>|<span data-ttu-id="c75b8-489">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-489">Yes</span></span>|  
|<span data-ttu-id="c75b8-490">Parametr</span><span class="sxs-lookup"><span data-stu-id="c75b8-490">parameter</span></span>|<span data-ttu-id="c75b8-491">Zmienne używane toodefine używane w hello przekształcenia</span><span class="sxs-lookup"><span data-stu-id="c75b8-491">Used toodefine variables used in hello transform</span></span>|<span data-ttu-id="c75b8-492">Nie</span><span class="sxs-lookup"><span data-stu-id="c75b8-492">No</span></span>|  
|<span data-ttu-id="c75b8-493">XSL: stylesheet</span><span class="sxs-lookup"><span data-stu-id="c75b8-493">xsl:stylesheet</span></span>|<span data-ttu-id="c75b8-494">Elemencie głównym arkusza stylów.</span><span class="sxs-lookup"><span data-stu-id="c75b8-494">Root stylesheet element.</span></span> <span data-ttu-id="c75b8-495">Wszystkie elementy i atrybuty zdefiniowane w ramach wykonaj standardowe hello [specyfikacji XSLT](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="c75b8-495">All elements and attributes defined within follow hello standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="c75b8-496">Tak</span><span class="sxs-lookup"><span data-stu-id="c75b8-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c75b8-497">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="c75b8-497">Usage</span></span>  
 <span data-ttu-id="c75b8-498">Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c75b8-498">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c75b8-499">**Sekcje zasad:** przychodzące, wychodzące</span><span class="sxs-lookup"><span data-stu-id="c75b8-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="c75b8-500">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="c75b8-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c75b8-501">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c75b8-501">Next steps</span></span>
<span data-ttu-id="c75b8-502">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c75b8-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
