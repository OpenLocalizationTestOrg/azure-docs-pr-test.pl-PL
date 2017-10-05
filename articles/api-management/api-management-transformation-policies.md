---
title: "Zasad przekształcania usługi Azure API Management | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad przekształcania dostępne do użycia w usłudze Azure API Management."
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
ms.openlocfilehash: c2bed904b82c569b28a6e00d0cc9b49107c148dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="d02b8-103">Zarządzanie interfejsami API zasad przekształcania</span><span class="sxs-lookup"><span data-stu-id="d02b8-103">API Management transformation policies</span></span>
<span data-ttu-id="d02b8-104">W tym temacie znajdują się informacje na następujące zasady usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="d02b8-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="d02b8-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="d02b8-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="d02b8-106"><a name="TransformationPolicies"></a>Zasad przekształcania</span><span class="sxs-lookup"><span data-stu-id="d02b8-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="d02b8-107">[Konwertuj JSON do pliku XML](api-management-transformation-policies.md#ConvertJSONtoXML) — konwertuje żądania lub odpowiedzi body z formatu JSON do pliku XML.</span><span class="sxs-lookup"><span data-stu-id="d02b8-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
-   <span data-ttu-id="d02b8-108">[Konwertuj do formatu JSON XML](api-management-transformation-policies.md#ConvertXMLtoJSON) — konwertuje żądania lub odpowiedzi body z pliku XML do formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="d02b8-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
-   <span data-ttu-id="d02b8-109">[Znajdowanie i zamienianie ciągów w treści](api-management-transformation-policies.md#Findandreplacestringinbody) — znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.</span><span class="sxs-lookup"><span data-stu-id="d02b8-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="d02b8-110">[Maski adresów URL w zawartości](api-management-transformation-policies.md#MaskURLSContent) -ponownie zapisuje (maski) łącza w odpowiedzi body tak, aby wskazywać równoważne połączenie za pośrednictwem bramy.</span><span class="sxs-lookup"><span data-stu-id="d02b8-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
-   <span data-ttu-id="d02b8-111">[Ustaw usługę zaplecza](api-management-transformation-policies.md#SetBackendService) — zmienia usługi wewnętrznej bazy danych dla żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="d02b8-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="d02b8-112">[Ustaw treści](api-management-transformation-policies.md#SetBody) -ustawia treść komunikatu dla żądań przychodzących i wychodzących.</span><span class="sxs-lookup"><span data-stu-id="d02b8-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="d02b8-113">[Set — nagłówek HTTP](api-management-transformation-policies.md#SetHTTPheader) — przypisuje wartość do istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="d02b8-114">[Wartość parametru ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) — dodaje, zastępuje wartość lub usuwa parametru ciągu zapytania żądania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="d02b8-115">[Ponowne zapisywanie adresów URL](api-management-transformation-policies.md#RewriteURL) — konwertuje adresie URL żądania w postaci publicznego do formularza oczekiwane przez usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="d02b8-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
-   <span data-ttu-id="d02b8-116">[Przekształcanie XML za pomocą XSLT](api-management-transformation-policies.md#XSLTransform) — ma zastosowanie transformacji XSL do formatu XML w treści żądania lub odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d02b8-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
##  <span data-ttu-id="d02b8-117"><a name="ConvertJSONtoXML"></a>Konwertuj JSON do pliku XML</span><span class="sxs-lookup"><span data-stu-id="d02b8-117"><a name="ConvertJSONtoXML"></a> Convert JSON to XML</span></span>  
 <span data-ttu-id="d02b8-118">`json-to-xml` Zasad konwertuje treści żądania lub odpowiedzi z formatu JSON do pliku XML.</span><span class="sxs-lookup"><span data-stu-id="d02b8-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d02b8-119">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="d02b8-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="d02b8-120">Przykład</span><span class="sxs-lookup"><span data-stu-id="d02b8-120">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d02b8-121">Elementy</span><span class="sxs-lookup"><span data-stu-id="d02b8-121">Elements</span></span>  
  
|<span data-ttu-id="d02b8-122">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-122">Name</span></span>|<span data-ttu-id="d02b8-123">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-123">Description</span></span>|<span data-ttu-id="d02b8-124">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d02b8-125">JSON do pliku xml</span><span class="sxs-lookup"><span data-stu-id="d02b8-125">json-to-xml</span></span>|<span data-ttu-id="d02b8-126">Element główny.</span><span class="sxs-lookup"><span data-stu-id="d02b8-126">Root element.</span></span>|<span data-ttu-id="d02b8-127">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d02b8-128">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="d02b8-128">Attributes</span></span>  
  
|<span data-ttu-id="d02b8-129">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-129">Name</span></span>|<span data-ttu-id="d02b8-130">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-130">Description</span></span>|<span data-ttu-id="d02b8-131">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-131">Required</span></span>|<span data-ttu-id="d02b8-132">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d02b8-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d02b8-133">Zastosuj</span><span class="sxs-lookup"><span data-stu-id="d02b8-133">apply</span></span>|<span data-ttu-id="d02b8-134">Atrybut musi zostać ustawiony na jedną z następujących wartości.</span><span class="sxs-lookup"><span data-stu-id="d02b8-134">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="d02b8-135">-zawsze — Zawsze stosuj konwersji.</span><span class="sxs-lookup"><span data-stu-id="d02b8-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="d02b8-136">convert zawartości typu json - tylko wtedy, gdy nagłówek odpowiedzi Content-Type wskazuje obecność JSON.</span><span class="sxs-lookup"><span data-stu-id="d02b8-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="d02b8-137">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-137">Yes</span></span>|<span data-ttu-id="d02b8-138">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-138">N/A</span></span>|  
|<span data-ttu-id="d02b8-139">należy wziąć pod uwagę zaakceptować — nagłówek</span><span class="sxs-lookup"><span data-stu-id="d02b8-139">consider-accept-header</span></span>|<span data-ttu-id="d02b8-140">Atrybut musi zostać ustawiony na jedną z następujących wartości.</span><span class="sxs-lookup"><span data-stu-id="d02b8-140">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="d02b8-141">— wartość true — zastosowania konwersji w żądaniu nagłówka Accept żądania JSON.</span><span class="sxs-lookup"><span data-stu-id="d02b8-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="d02b8-142">— wartość false — Zawsze stosuj konwersji.</span><span class="sxs-lookup"><span data-stu-id="d02b8-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="d02b8-143">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-143">No</span></span>|<span data-ttu-id="d02b8-144">Wartość true</span><span class="sxs-lookup"><span data-stu-id="d02b8-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d02b8-145">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d02b8-145">Usage</span></span>  
 <span data-ttu-id="d02b8-146">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d02b8-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d02b8-147">**Sekcje zasad:** przychodzące, wychodzące, na błąd</span><span class="sxs-lookup"><span data-stu-id="d02b8-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="d02b8-148">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="d02b8-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d02b8-149"><a name="ConvertXMLtoJSON"></a>Konwertuj do formatu JSON XML</span><span class="sxs-lookup"><span data-stu-id="d02b8-149"><a name="ConvertXMLtoJSON"></a> Convert XML to JSON</span></span>  
 <span data-ttu-id="d02b8-150">`xml-to-json` Zasad konwertuje treści żądania lub odpowiedzi z pliku XML do formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="d02b8-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span></span> <span data-ttu-id="d02b8-151">Ta zasada może służyć do modernizacji interfejsów API oparty na usługach sieci web XML — tylko do wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d02b8-151">This policy can be used to modernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d02b8-152">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="d02b8-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="d02b8-153">Przykład</span><span class="sxs-lookup"><span data-stu-id="d02b8-153">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d02b8-154">Elementy</span><span class="sxs-lookup"><span data-stu-id="d02b8-154">Elements</span></span>  
  
|<span data-ttu-id="d02b8-155">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-155">Name</span></span>|<span data-ttu-id="d02b8-156">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-156">Description</span></span>|<span data-ttu-id="d02b8-157">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d02b8-158">XML do formatu json</span><span class="sxs-lookup"><span data-stu-id="d02b8-158">xml-to-json</span></span>|<span data-ttu-id="d02b8-159">Element główny.</span><span class="sxs-lookup"><span data-stu-id="d02b8-159">Root element.</span></span>|<span data-ttu-id="d02b8-160">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d02b8-161">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="d02b8-161">Attributes</span></span>  
  
|<span data-ttu-id="d02b8-162">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-162">Name</span></span>|<span data-ttu-id="d02b8-163">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-163">Description</span></span>|<span data-ttu-id="d02b8-164">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-164">Required</span></span>|<span data-ttu-id="d02b8-165">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d02b8-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d02b8-166">rodzaj</span><span class="sxs-lookup"><span data-stu-id="d02b8-166">kind</span></span>|<span data-ttu-id="d02b8-167">Atrybut musi zostać ustawiony na jedną z następujących wartości.</span><span class="sxs-lookup"><span data-stu-id="d02b8-167">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="d02b8-168">javascript — przyjazne - przekonwertowanego JSON ma formę przyjazną dla deweloperów języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d02b8-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span></span><br /><span data-ttu-id="d02b8-169">-bezpośredni — przekonwertowanego JSON odzwierciedla struktury oryginalnego dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="d02b8-169">-   direct - the converted JSON reflects the original XML document's structure.</span></span>|<span data-ttu-id="d02b8-170">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-170">Yes</span></span>|<span data-ttu-id="d02b8-171">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-171">N/A</span></span>|  
|<span data-ttu-id="d02b8-172">Zastosuj</span><span class="sxs-lookup"><span data-stu-id="d02b8-172">apply</span></span>|<span data-ttu-id="d02b8-173">Atrybut musi zostać ustawiony na jedną z następujących wartości.</span><span class="sxs-lookup"><span data-stu-id="d02b8-173">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="d02b8-174">-zawsze - przekonwertować zawsze.</span><span class="sxs-lookup"><span data-stu-id="d02b8-174">-   always - convert always.</span></span><br /><span data-ttu-id="d02b8-175">convert zawartości — typ xml - tylko wtedy, gdy nagłówek odpowiedzi Content-Type wskazuje obecność XML.</span><span class="sxs-lookup"><span data-stu-id="d02b8-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="d02b8-176">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-176">Yes</span></span>|<span data-ttu-id="d02b8-177">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-177">N/A</span></span>|  
|<span data-ttu-id="d02b8-178">należy wziąć pod uwagę zaakceptować — nagłówek</span><span class="sxs-lookup"><span data-stu-id="d02b8-178">consider-accept-header</span></span>|<span data-ttu-id="d02b8-179">Atrybut musi zostać ustawiony na jedną z następujących wartości.</span><span class="sxs-lookup"><span data-stu-id="d02b8-179">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="d02b8-180">Jeśli żądanie XML w żądaniu nagłówek Accept - wartość true — mają zastosowanie konwersji.</span><span class="sxs-lookup"><span data-stu-id="d02b8-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="d02b8-181">— wartość false — Zawsze stosuj konwersji.</span><span class="sxs-lookup"><span data-stu-id="d02b8-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="d02b8-182">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-182">No</span></span>|<span data-ttu-id="d02b8-183">Wartość true</span><span class="sxs-lookup"><span data-stu-id="d02b8-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d02b8-184">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d02b8-184">Usage</span></span>  
 <span data-ttu-id="d02b8-185">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d02b8-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d02b8-186">**Sekcje zasad:** przychodzące, wychodzące, na błąd</span><span class="sxs-lookup"><span data-stu-id="d02b8-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="d02b8-187">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="d02b8-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d02b8-188"><a name="Findandreplacestringinbody"></a>Znajdowanie i zamienianie ciągów w treści</span><span class="sxs-lookup"><span data-stu-id="d02b8-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="d02b8-189">`find-and-replace` Zasad znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.</span><span class="sxs-lookup"><span data-stu-id="d02b8-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d02b8-190">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="d02b8-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="d02b8-191">Przykład</span><span class="sxs-lookup"><span data-stu-id="d02b8-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="d02b8-192">Elementy</span><span class="sxs-lookup"><span data-stu-id="d02b8-192">Elements</span></span>  
  
|<span data-ttu-id="d02b8-193">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-193">Name</span></span>|<span data-ttu-id="d02b8-194">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-194">Description</span></span>|<span data-ttu-id="d02b8-195">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d02b8-196">Znajdź i Zamień</span><span class="sxs-lookup"><span data-stu-id="d02b8-196">find-and-replace</span></span>|<span data-ttu-id="d02b8-197">Element główny.</span><span class="sxs-lookup"><span data-stu-id="d02b8-197">Root element.</span></span>|<span data-ttu-id="d02b8-198">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d02b8-199">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="d02b8-199">Attributes</span></span>  
  
|<span data-ttu-id="d02b8-200">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-200">Name</span></span>|<span data-ttu-id="d02b8-201">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-201">Description</span></span>|<span data-ttu-id="d02b8-202">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-202">Required</span></span>|<span data-ttu-id="d02b8-203">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d02b8-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d02b8-204">Z</span><span class="sxs-lookup"><span data-stu-id="d02b8-204">from</span></span>|<span data-ttu-id="d02b8-205">Ciąg do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-205">The string to search for.</span></span>|<span data-ttu-id="d02b8-206">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-206">Yes</span></span>|<span data-ttu-id="d02b8-207">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-207">N/A</span></span>|  
|<span data-ttu-id="d02b8-208">na</span><span class="sxs-lookup"><span data-stu-id="d02b8-208">to</span></span>|<span data-ttu-id="d02b8-209">Ciąg zastępczy.</span><span class="sxs-lookup"><span data-stu-id="d02b8-209">The replacement string.</span></span> <span data-ttu-id="d02b8-210">Określ długość zastępczy ciąg o zerowej do usunięcia ciąg wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-210">Specify a zero length replacement string to remove the search string.</span></span>|<span data-ttu-id="d02b8-211">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-211">Yes</span></span>|<span data-ttu-id="d02b8-212">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d02b8-213">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d02b8-213">Usage</span></span>  
 <span data-ttu-id="d02b8-214">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d02b8-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d02b8-215">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="d02b8-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="d02b8-216">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="d02b8-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d02b8-217"><a name="MaskURLSContent"></a>Adresy URL maski w zawartości</span><span class="sxs-lookup"><span data-stu-id="d02b8-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="d02b8-218">`redirect-content-urls` Zasad ponownie zapisuje łącza (maski) w treści odpowiedzi tak, aby wskazywać równoważne połączenie za pośrednictwem bramy.</span><span class="sxs-lookup"><span data-stu-id="d02b8-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span> <span data-ttu-id="d02b8-219">Użyj w sekcji wychodzącego ponownie zapisać łącza treści odpowiedzi będą wskazywać bramy.</span><span class="sxs-lookup"><span data-stu-id="d02b8-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span></span> <span data-ttu-id="d02b8-220">Użyj części ruchu przychodzącego dla odwrotny efekt.</span><span class="sxs-lookup"><span data-stu-id="d02b8-220">Use in the inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d02b8-221">Ta zasada nie zmienia żadnych wartości nagłówka takich `Location` nagłówków.</span><span class="sxs-lookup"><span data-stu-id="d02b8-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="d02b8-222">Aby zmienić wartości nagłówka, użyj [nagłówka set](api-management-transformation-policies.md#SetHTTPheader) zasad.</span><span class="sxs-lookup"><span data-stu-id="d02b8-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d02b8-223">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="d02b8-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="d02b8-224">Przykład</span><span class="sxs-lookup"><span data-stu-id="d02b8-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="d02b8-225">Elementy</span><span class="sxs-lookup"><span data-stu-id="d02b8-225">Elements</span></span>  
  
|<span data-ttu-id="d02b8-226">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-226">Name</span></span>|<span data-ttu-id="d02b8-227">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-227">Description</span></span>|<span data-ttu-id="d02b8-228">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d02b8-229">adresy URL zawartości przekierowań</span><span class="sxs-lookup"><span data-stu-id="d02b8-229">redirect-content-urls</span></span>|<span data-ttu-id="d02b8-230">Element główny.</span><span class="sxs-lookup"><span data-stu-id="d02b8-230">Root element.</span></span>|<span data-ttu-id="d02b8-231">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d02b8-232">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d02b8-232">Usage</span></span>  
 <span data-ttu-id="d02b8-233">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d02b8-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d02b8-234">**Sekcje zasad:** przychodzące, wychodzące</span><span class="sxs-lookup"><span data-stu-id="d02b8-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="d02b8-235">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="d02b8-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d02b8-236"><a name="SetBackendService"></a>Ustawianie usługi wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="d02b8-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="d02b8-237">Użyj `set-backend-service` zasad, aby przekierować żądanie przychodzące do wewnętrznej bazy danych innej niż określona w ustawieniach interfejsu API dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="d02b8-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span></span> <span data-ttu-id="d02b8-238">Ta zasada zmiany wewnętrznej bazy danych usługi podstawowy adres URL żądania przychodzącego, jeśli określony w zasadach.</span><span class="sxs-lookup"><span data-stu-id="d02b8-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d02b8-239">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="d02b8-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="d02b8-240">Przykład</span><span class="sxs-lookup"><span data-stu-id="d02b8-240">Example</span></span>  
  
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
<span data-ttu-id="d02b8-241">W tym przykładzie Ustaw zasady usługi wewnętrznej bazy danych przekierowuje żądania na podstawie wartości wersji przekazany ciąg zapytania do usługi zaplecza inny niż określony w interfejsie API.</span><span class="sxs-lookup"><span data-stu-id="d02b8-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span></span>
  
<span data-ttu-id="d02b8-242">Początkowo wewnętrznej bazy danych usługi podstawowy adres URL jest pochodną ustawień interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d02b8-242">Initially the backend service base URL is derived from the API settings.</span></span> <span data-ttu-id="d02b8-243">Dlatego adres URL żądania `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` staje się `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` gdzie `http://contoso.com/api/10.4/` jest adres URL usługi wewnętrznej bazy danych, które zostały określone w ustawieniach interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d02b8-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span></span>  
  
<span data-ttu-id="d02b8-244">Gdy [< Wybierz\> ](api-management-advanced-policies.md#choose) deklaracji zasad są stosowane wewnętrznej bazy danych usługi podstawowy adres URL może zmienić ponownie albo `http://contoso.com/api/8.2` lub `http://contoso.com/api/9.1`, w zależności od wartości parametru zapytania żądania wersji.</span><span class="sxs-lookup"><span data-stu-id="d02b8-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span></span> <span data-ttu-id="d02b8-245">Na przykład, jeśli wartość jest `"2013-15"` żądania końcowego adresu URL staje się `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="d02b8-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="d02b8-246">Jeśli dodatkowo przekształcenie żądania jest odpowiednie, inne [zasad przekształcania](api-management-transformation-policies.md#TransformationPolicies) mogą być używane.</span><span class="sxs-lookup"><span data-stu-id="d02b8-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="d02b8-247">Na przykład, aby teraz, żądanie jest przesyłane do wersji określonej w wewnętrznej bazie danych, należy usunąć parametr zapytania wersji [ustawić parametr ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) zasad może służyć do Usuń atrybut nadmiarowe obecnie wersji.</span><span class="sxs-lookup"><span data-stu-id="d02b8-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="d02b8-248">Przykład</span><span class="sxs-lookup"><span data-stu-id="d02b8-248">Example</span></span>  
  
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
<span data-ttu-id="d02b8-249">W tym przykładzie zasady kieruje żądanie do usługi sieci szkieletowej wewnętrznej bazie danych, przy użyciu identyfikatora userId ciąg zapytania jako klucza partycji i repliką podstawową partycji.</span><span class="sxs-lookup"><span data-stu-id="d02b8-249">In this example the policy routes the request to a service fabric backend, using the userId query string as the partition key and using the primary replica of the partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="d02b8-250">Elementy</span><span class="sxs-lookup"><span data-stu-id="d02b8-250">Elements</span></span>  
  
|<span data-ttu-id="d02b8-251">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-251">Name</span></span>|<span data-ttu-id="d02b8-252">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-252">Description</span></span>|<span data-ttu-id="d02b8-253">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d02b8-254">zestaw wewnętrznej bazy danych usługi</span><span class="sxs-lookup"><span data-stu-id="d02b8-254">set-backend-service</span></span>|<span data-ttu-id="d02b8-255">Element główny.</span><span class="sxs-lookup"><span data-stu-id="d02b8-255">Root element.</span></span>|<span data-ttu-id="d02b8-256">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d02b8-257">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="d02b8-257">Attributes</span></span>  
  
|<span data-ttu-id="d02b8-258">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-258">Name</span></span>|<span data-ttu-id="d02b8-259">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-259">Description</span></span>|<span data-ttu-id="d02b8-260">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-260">Required</span></span>|<span data-ttu-id="d02b8-261">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d02b8-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d02b8-262">adres url Base</span><span class="sxs-lookup"><span data-stu-id="d02b8-262">base-url</span></span>|<span data-ttu-id="d02b8-263">Nowego zaplecza podstawowy adres URL usługi.</span><span class="sxs-lookup"><span data-stu-id="d02b8-263">New backend service base URL.</span></span>|<span data-ttu-id="d02b8-264">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-264">No</span></span>|<span data-ttu-id="d02b8-265">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-265">N/A</span></span>|  
|<span data-ttu-id="d02b8-266">Identyfikator wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="d02b8-266">backend-id</span></span>|<span data-ttu-id="d02b8-267">Identyfikator wewnętrznej bazy danych, aby kierować do.</span><span class="sxs-lookup"><span data-stu-id="d02b8-267">Identifier of the backend to route to.</span></span>|<span data-ttu-id="d02b8-268">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-268">No</span></span>|<span data-ttu-id="d02b8-269">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-269">N/A</span></span>|  
|<span data-ttu-id="d02b8-270">rz partycji klucza</span><span class="sxs-lookup"><span data-stu-id="d02b8-270">sf-partition-key</span></span>|<span data-ttu-id="d02b8-271">Dotyczy tylko podczas wewnętrznej bazy danych to usługa sieci szkieletowej usług i jest określona za pomocą "wewnętrznej bazy danych id".</span><span class="sxs-lookup"><span data-stu-id="d02b8-271">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="d02b8-272">Używany do rozpoznawania określonej partycji z usługi rozpoznawania nazw.</span><span class="sxs-lookup"><span data-stu-id="d02b8-272">Used to resolve a specific partition from the name resolution service.</span></span>|<span data-ttu-id="d02b8-273">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-273">No</span></span>|<span data-ttu-id="d02b8-274">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-274">N/A</span></span>|  
|<span data-ttu-id="d02b8-275">rz repliki typu</span><span class="sxs-lookup"><span data-stu-id="d02b8-275">sf-replica-type</span></span>|<span data-ttu-id="d02b8-276">Dotyczy tylko podczas wewnętrznej bazy danych to usługa sieci szkieletowej usług i jest określona za pomocą "wewnętrznej bazy danych id".</span><span class="sxs-lookup"><span data-stu-id="d02b8-276">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="d02b8-277">Kontroluje, czy żądanie należy przejść do podstawowej lub pomocniczej replice partycji.</span><span class="sxs-lookup"><span data-stu-id="d02b8-277">Controls if the request should go to the primary or secondary replica of a partition.</span></span> |<span data-ttu-id="d02b8-278">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-278">No</span></span>|<span data-ttu-id="d02b8-279">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-279">N/A</span></span>|    
|<span data-ttu-id="d02b8-280">rz resolve warunków</span><span class="sxs-lookup"><span data-stu-id="d02b8-280">sf-resolve-condition</span></span>|<span data-ttu-id="d02b8-281">Dotyczy tylko w przypadku wewnętrznej bazy danych usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d02b8-281">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="d02b8-282">Warunek identyfikowania wywołania do zaplecza usługi sieć szkieletowa usług musi być powtarzana z nowego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-282">Condition identifying if the call to Service Fabric backend has to be repeated with new resolution.</span></span>|<span data-ttu-id="d02b8-283">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-283">No</span></span>|<span data-ttu-id="d02b8-284">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-284">N/A</span></span>|    
|<span data-ttu-id="d02b8-285">rz usługi wystąpienie nazwa-</span><span class="sxs-lookup"><span data-stu-id="d02b8-285">sf-service-instance-name</span></span>|<span data-ttu-id="d02b8-286">Dotyczy tylko w przypadku wewnętrznej bazy danych usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d02b8-286">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="d02b8-287">Pozwala zmienić wystąpień usługi w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-287">Allows to change service instances at runtime.</span></span> |<span data-ttu-id="d02b8-288">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-288">No</span></span>|<span data-ttu-id="d02b8-289">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="d02b8-290">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d02b8-290">Usage</span></span>  
 <span data-ttu-id="d02b8-291">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d02b8-291">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d02b8-292">**Sekcje zasad:** wewnętrznej bazy danych dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="d02b8-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="d02b8-293">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="d02b8-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d02b8-294"><a name="SetBody"></a>Zestaw treści</span><span class="sxs-lookup"><span data-stu-id="d02b8-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="d02b8-295">Użyj `set-body` zasady można ustawić treść komunikatu dla żądań przychodzących i wychodzących.</span><span class="sxs-lookup"><span data-stu-id="d02b8-295">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span></span> <span data-ttu-id="d02b8-296">Aby uzyskać dostęp do treści wiadomości, można użyć `context.Request.Body` właściwości lub `context.Response.Body`, w zależności od tego, czy zasady znajduje się w sekcji ruchu przychodzącego lub wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="d02b8-296">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="d02b8-297">Należy pamiętać, że domyślnie, gdy uzyskujesz dostęp do wiadomości body przy użyciu `context.Request.Body` lub `context.Response.Body`, treści oryginalnej wiadomości zostaną utracone i musi być ustawione przez zwrócenie treści Wstecz w wyrażeniu.</span><span class="sxs-lookup"><span data-stu-id="d02b8-297">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span></span> <span data-ttu-id="d02b8-298">Aby zachować zawartość treści, ustaw `preserveContent` parametr `true` podczas uzyskiwania dostępu do wiadomości.</span><span class="sxs-lookup"><span data-stu-id="d02b8-298">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span></span> <span data-ttu-id="d02b8-299">Jeśli `preserveContent` ustawiono `true` i różnych treści jest zwracany przez wyrażenie, treść zwracane jest używany.</span><span class="sxs-lookup"><span data-stu-id="d02b8-299">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span></span>  
>   
>  <span data-ttu-id="d02b8-300">Należy pamiętać przedstawione poniżej zagadnienia, korzystając z `set-body` zasad.</span><span class="sxs-lookup"><span data-stu-id="d02b8-300">Please note the following considerations when using the `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="d02b8-301">Jeśli używasz `set-body` zasad, aby zwrócić nowe lub zaktualizowane treści, nie trzeba ustawić `preserveContent` do `true` ponieważ są jawnie dostarczenie nowej zawartości w treści.</span><span class="sxs-lookup"><span data-stu-id="d02b8-301">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span></span>  
> -   <span data-ttu-id="d02b8-302">Zachowywanie treść odpowiedzi w potoku dla ruchu przychodzącego sensu ponieważ nie istnieje jeszcze żadnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d02b8-302">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="d02b8-303">Zachowywanie zawartości żądania w potoku wychodzącego nie sensu, ponieważ żądania została już wysłana do wewnętrznej bazy danych w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="d02b8-303">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span></span>  
> -   <span data-ttu-id="d02b8-304">Jeśli zasada ta jest używana, gdy brak treści wiadomości, na przykład w przychodzącej GET, jest zwracany wyjątek.</span><span class="sxs-lookup"><span data-stu-id="d02b8-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="d02b8-305">Aby uzyskać więcej informacji, zobacz `context.Request.Body`, `context.Response.Body`i `IMessage` sekcje w [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables) tabeli.</span><span class="sxs-lookup"><span data-stu-id="d02b8-305">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d02b8-306">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="d02b8-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="d02b8-307">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d02b8-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="d02b8-308">Przykład literału tekstu</span><span class="sxs-lookup"><span data-stu-id="d02b8-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a><span data-ttu-id="d02b8-309">Przykład: uzyskiwanie dostępu do treść jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="d02b8-309">Example accessing the body as a string.</span></span> <span data-ttu-id="d02b8-310">Należy pamiętać, że są firma Microsoft zachowuje oryginalne treści żądania tak, aby firma Microsoft dostęp do niego później w potoku.</span><span class="sxs-lookup"><span data-stu-id="d02b8-310">Note that we are preserving the original request body so that we can access it later in the pipeline.</span></span>
  
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
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a><span data-ttu-id="d02b8-311">Przykład dostęp do treści jako JObject.</span><span class="sxs-lookup"><span data-stu-id="d02b8-311">Example accessing the body as a JObject.</span></span> <span data-ttu-id="d02b8-312">Należy pamiętać, że od czasu firma Microsoft nie są rezerwowania oryginalnego treści żądania, spowoduje ona później w potoku Wystąpił wyjątek w celu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d02b8-312">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span></span>  
  
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
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="d02b8-313">Filtrowanie oparte na produktu odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="d02b8-313">Filter response based on product</span></span>  
 <span data-ttu-id="d02b8-314">W tym przykładzie pokazano, jak wykonać filtrowanie zawartości przez usunięcie elementów danych z odpowiedzi otrzymał od usługi wewnętrznej bazy danych, korzystając z `Starter` produktu.</span><span class="sxs-lookup"><span data-stu-id="d02b8-314">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="d02b8-315">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybkie przewijanie do przodu do 34:30.</span><span class="sxs-lookup"><span data-stu-id="d02b8-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="d02b8-316">Rozpocznij od 31:50 wyświetlić przegląd [ciemny niebo prognozy interfejsu API](https://developer.forecast.io/) używane na potrzeby tego pokazu.</span><span class="sxs-lookup"><span data-stu-id="d02b8-316">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="d02b8-317">Za pomocą szablonów płynne o treści zestawu</span><span class="sxs-lookup"><span data-stu-id="d02b8-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="d02b8-318">`set-body` Zasad może być skonfigurowana do używania [płynne](https://shopify.github.io/liquid/basics/introduction/) tworzenia szablonów języka aby transfom treści żądania lub odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d02b8-318">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span></span> <span data-ttu-id="d02b8-319">Może to być bardzo efektywnym sposobem, aby całkowicie zmienić format wiadomości.</span><span class="sxs-lookup"><span data-stu-id="d02b8-319">This can be very effective if you need to completely reshape the format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d02b8-320">Implementacja płynnych używane w `set-body` zasada jest skonfigurowana w trybie"C#".</span><span class="sxs-lookup"><span data-stu-id="d02b8-320">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="d02b8-321">Jest to szczególnie ważne podczas wykonywania czynności takich jak filtrowania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="d02b8-322">Na przykład przy użyciu filtru daty wymaga użycia Pascal wielkości liter i C# Data formatowania, np.:</span><span class="sxs-lookup"><span data-stu-id="d02b8-322">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="d02b8-323">{{body.foo.startDateTime| Data: "yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="d02b8-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d02b8-324">Aby można było poprawnie powiązać treści XML przy użyciu szablonu płynne, użyj `set-header` zasad, aby ustawić typ zawartości do albo aplikacja/xml, tekstu/xml (lub dowolnego typu kończąc + xml), na treść JSON, musi to być application/json, tekst/json (lub dowolnego typu kończąc + json).</span><span class="sxs-lookup"><span data-stu-id="d02b8-324">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-to-soap-using-a-liquid-template"></a><span data-ttu-id="d02b8-325">Konwertuj JSON przy użyciu szablonu płynne SOAP</span><span class="sxs-lookup"><span data-stu-id="d02b8-325">Convert JSON to SOAP using a Liquid template</span></span>
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

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="d02b8-326">Tranform ciągu JSON przy użyciu szablonu płynne</span><span class="sxs-lookup"><span data-stu-id="d02b8-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="d02b8-327">Elementy</span><span class="sxs-lookup"><span data-stu-id="d02b8-327">Elements</span></span>  
  
|<span data-ttu-id="d02b8-328">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-328">Name</span></span>|<span data-ttu-id="d02b8-329">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-329">Description</span></span>|<span data-ttu-id="d02b8-330">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d02b8-331">zestaw treści</span><span class="sxs-lookup"><span data-stu-id="d02b8-331">set-body</span></span>|<span data-ttu-id="d02b8-332">Element główny.</span><span class="sxs-lookup"><span data-stu-id="d02b8-332">Root element.</span></span> <span data-ttu-id="d02b8-333">Zawiera treść lub wyrażeń, które zwraca treści.</span><span class="sxs-lookup"><span data-stu-id="d02b8-333">Contains the body text or an expressions that returns a body.</span></span>|<span data-ttu-id="d02b8-334">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="d02b8-335">Właściwości</span><span class="sxs-lookup"><span data-stu-id="d02b8-335">Properties</span></span>  
  
|<span data-ttu-id="d02b8-336">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-336">Name</span></span>|<span data-ttu-id="d02b8-337">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-337">Description</span></span>|<span data-ttu-id="d02b8-338">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-338">Required</span></span>|<span data-ttu-id="d02b8-339">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d02b8-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d02b8-340">szablon</span><span class="sxs-lookup"><span data-stu-id="d02b8-340">template</span></span>|<span data-ttu-id="d02b8-341">Pozwala zmienić tryb tworzenia szablonów zasad treści zestaw uruchamianego w.</span><span class="sxs-lookup"><span data-stu-id="d02b8-341">Used to change the templating mode that the set body policy will run in.</span></span> <span data-ttu-id="d02b8-342">Obecnie jest to jedyna obsługiwana wartość:</span><span class="sxs-lookup"><span data-stu-id="d02b8-342">Currently the only supported value is:</span></span><br /><br /><span data-ttu-id="d02b8-343">-płynne — Ustaw zasady treści będzie korzystać z aparatu płynne tworzenia szablonów</span><span class="sxs-lookup"><span data-stu-id="d02b8-343">- liquid - the set body policy will use the liquid templating engine</span></span> |<span data-ttu-id="d02b8-344">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-344">No</span></span>|<span data-ttu-id="d02b8-345">płynnych</span><span class="sxs-lookup"><span data-stu-id="d02b8-345">liquid</span></span>|  

<span data-ttu-id="d02b8-346">Aby uzyskać dostęp do informacji na temat żądania i odpowiedzi, płynne szablonu można powiązać z obiekt kontekstu z następującymi właściwościami:</span><span class="sxs-lookup"><span data-stu-id="d02b8-346">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span></span> <br />
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



### <a name="usage"></a><span data-ttu-id="d02b8-347">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d02b8-347">Usage</span></span>  
 <span data-ttu-id="d02b8-348">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d02b8-348">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d02b8-349">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="d02b8-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="d02b8-350">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="d02b8-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d02b8-351"><a name="SetHTTPheader"></a>Set — nagłówek HTTP</span><span class="sxs-lookup"><span data-stu-id="d02b8-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="d02b8-352">`set-header` Zasad przypisuje wartość do istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-352">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="d02b8-353">Wstawia listę nagłówków HTTP do wiadomości HTTP.</span><span class="sxs-lookup"><span data-stu-id="d02b8-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="d02b8-354">Po umieszczeniu w potoku dla ruchu przychodzącego, ta zasada ustawia nagłówki HTTP dla żądania przekazywany do usługi docelowej.</span><span class="sxs-lookup"><span data-stu-id="d02b8-354">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span></span> <span data-ttu-id="d02b8-355">Po umieszczeniu w potoku wychodzącego, ta zasada ustawia nagłówki HTTP są wysyłane do klienta bramy odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d02b8-355">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d02b8-356">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="d02b8-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="d02b8-357">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d02b8-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="d02b8-358">Przykład</span><span class="sxs-lookup"><span data-stu-id="d02b8-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="d02b8-359">Informacje o kontekście do przodu do usługi zaplecza</span><span class="sxs-lookup"><span data-stu-id="d02b8-359">Forward context information to the backend service</span></span>  
 <span data-ttu-id="d02b8-360">W tym przykładzie przedstawiono sposób zastosowania zasad na poziomie interfejsu API, aby podać informacje o kontekście usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d02b8-360">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="d02b8-361">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybkie przewijanie do przodu do 10:30.</span><span class="sxs-lookup"><span data-stu-id="d02b8-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="d02b8-362">Na 12:10 istnieje pokaz wywołanie operacji w portalu dla deweloperów, w którym można zobaczyć zasad w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="d02b8-362">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="d02b8-363">Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="d02b8-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="d02b8-364">Elementy</span><span class="sxs-lookup"><span data-stu-id="d02b8-364">Elements</span></span>  
  
|<span data-ttu-id="d02b8-365">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-365">Name</span></span>|<span data-ttu-id="d02b8-366">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-366">Description</span></span>|<span data-ttu-id="d02b8-367">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d02b8-368">set — nagłówek</span><span class="sxs-lookup"><span data-stu-id="d02b8-368">set-header</span></span>|<span data-ttu-id="d02b8-369">Element główny.</span><span class="sxs-lookup"><span data-stu-id="d02b8-369">Root element.</span></span>|<span data-ttu-id="d02b8-370">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-370">Yes</span></span>|  
|<span data-ttu-id="d02b8-371">wartość</span><span class="sxs-lookup"><span data-stu-id="d02b8-371">value</span></span>|<span data-ttu-id="d02b8-372">Określa wartość nagłówka do ustawienia.</span><span class="sxs-lookup"><span data-stu-id="d02b8-372">Specifies the value of the header to be set.</span></span> <span data-ttu-id="d02b8-373">Do wiele nagłówków o takiej samej nazwie Dodaj dodatkowe `value` elementy.</span><span class="sxs-lookup"><span data-stu-id="d02b8-373">For multiple headers with the same name add additional `value` elements.</span></span>|<span data-ttu-id="d02b8-374">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="d02b8-375">Właściwości</span><span class="sxs-lookup"><span data-stu-id="d02b8-375">Properties</span></span>  
  
|<span data-ttu-id="d02b8-376">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-376">Name</span></span>|<span data-ttu-id="d02b8-377">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-377">Description</span></span>|<span data-ttu-id="d02b8-378">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-378">Required</span></span>|<span data-ttu-id="d02b8-379">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d02b8-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d02b8-380">istnieje akcja</span><span class="sxs-lookup"><span data-stu-id="d02b8-380">exists-action</span></span>|<span data-ttu-id="d02b8-381">Określa, jakie działania w sytuacji, gdy nagłówek został już określony.</span><span class="sxs-lookup"><span data-stu-id="d02b8-381">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="d02b8-382">Ten atrybut musi mieć jedną z następujących wartości.</span><span class="sxs-lookup"><span data-stu-id="d02b8-382">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="d02b8-383">-override - zastępuje wartość istniejący nagłówek.</span><span class="sxs-lookup"><span data-stu-id="d02b8-383">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="d02b8-384">-skip — nie zastępuje istniejącą wartość nagłówka.</span><span class="sxs-lookup"><span data-stu-id="d02b8-384">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="d02b8-385">-dołączania - dołącza wartość do istniejącej wartości nagłówka.</span><span class="sxs-lookup"><span data-stu-id="d02b8-385">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="d02b8-386">-Usunięcie — usuwa nagłówek z żądania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-386">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="d02b8-387">Jeśli wartość `override` powoduje rejestrowanie wiele wpisów o takiej samej nazwie w nagłówku ustawiany zgodnie ze wszystkich zapisów (które zostaną wyświetlone wiele razy); zostanie ustawiona tylko wartości wyświetlane w wynikach.</span><span class="sxs-lookup"><span data-stu-id="d02b8-387">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="d02b8-388">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-388">No</span></span>|<span data-ttu-id="d02b8-389">zastąpienie</span><span class="sxs-lookup"><span data-stu-id="d02b8-389">override</span></span>|  
|<span data-ttu-id="d02b8-390">name</span><span class="sxs-lookup"><span data-stu-id="d02b8-390">name</span></span>|<span data-ttu-id="d02b8-391">Określa nazwę nagłówka do ustawienia.</span><span class="sxs-lookup"><span data-stu-id="d02b8-391">Specifies name of the header to be set.</span></span>|<span data-ttu-id="d02b8-392">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-392">Yes</span></span>|<span data-ttu-id="d02b8-393">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d02b8-394">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d02b8-394">Usage</span></span>  
 <span data-ttu-id="d02b8-395">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d02b8-395">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d02b8-396">**Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd</span><span class="sxs-lookup"><span data-stu-id="d02b8-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="d02b8-397">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="d02b8-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d02b8-398"><a name="SetQueryStringParameter"></a>Parametr ciągu zapytania dla zestawu</span><span class="sxs-lookup"><span data-stu-id="d02b8-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="d02b8-399">`set-query-parameter` Zasad dodaje wartość zastępuje, lub usuwa żądania parametru ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-399">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="d02b8-400">Może służyć do przekazywania kwerendy parametry oczekiwany przez usługi wewnętrznej bazy danych, które są opcjonalne lub nigdy nie są obecne w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="d02b8-400">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d02b8-401">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="d02b8-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="d02b8-402">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d02b8-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="d02b8-403">Przykład</span><span class="sxs-lookup"><span data-stu-id="d02b8-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="d02b8-404">Informacje o kontekście do przodu do usługi zaplecza</span><span class="sxs-lookup"><span data-stu-id="d02b8-404">Forward context information to the backend service</span></span>  
 <span data-ttu-id="d02b8-405">W tym przykładzie przedstawiono sposób zastosowania zasad na poziomie interfejsu API, aby podać informacje o kontekście usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d02b8-405">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="d02b8-406">Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybkie przewijanie do przodu do 10:30.</span><span class="sxs-lookup"><span data-stu-id="d02b8-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="d02b8-407">Na 12:10 istnieje pokaz wywołanie operacji w portalu dla deweloperów, w którym można zobaczyć zasad w miejscu pracy.</span><span class="sxs-lookup"><span data-stu-id="d02b8-407">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="d02b8-408">Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="d02b8-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="d02b8-409">Elementy</span><span class="sxs-lookup"><span data-stu-id="d02b8-409">Elements</span></span>  
  
|<span data-ttu-id="d02b8-410">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-410">Name</span></span>|<span data-ttu-id="d02b8-411">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-411">Description</span></span>|<span data-ttu-id="d02b8-412">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d02b8-413">Parametr zestawu — zapytania</span><span class="sxs-lookup"><span data-stu-id="d02b8-413">set-query-parameter</span></span>|<span data-ttu-id="d02b8-414">Element główny.</span><span class="sxs-lookup"><span data-stu-id="d02b8-414">Root element.</span></span>|<span data-ttu-id="d02b8-415">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-415">Yes</span></span>|  
|<span data-ttu-id="d02b8-416">wartość</span><span class="sxs-lookup"><span data-stu-id="d02b8-416">value</span></span>|<span data-ttu-id="d02b8-417">Określa wartość parametru zapytania do ustawienia.</span><span class="sxs-lookup"><span data-stu-id="d02b8-417">Specifies the value of the query parameter to be set.</span></span> <span data-ttu-id="d02b8-418">Dla wielu parametrów zapytania o takiej samej nazwie dodanie dodatkowych `value` elementów.</span><span class="sxs-lookup"><span data-stu-id="d02b8-418">For multiple query parameters with the same name add additional `value` elements.</span></span>|<span data-ttu-id="d02b8-419">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="d02b8-420">Właściwości</span><span class="sxs-lookup"><span data-stu-id="d02b8-420">Properties</span></span>  
  
|<span data-ttu-id="d02b8-421">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-421">Name</span></span>|<span data-ttu-id="d02b8-422">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-422">Description</span></span>|<span data-ttu-id="d02b8-423">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-423">Required</span></span>|<span data-ttu-id="d02b8-424">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d02b8-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d02b8-425">istnieje akcja</span><span class="sxs-lookup"><span data-stu-id="d02b8-425">exists-action</span></span>|<span data-ttu-id="d02b8-426">Określa, jakie działania w sytuacji, gdy parametr zapytania został już określony.</span><span class="sxs-lookup"><span data-stu-id="d02b8-426">Specifies what action to take when the query parameter is already specified.</span></span> <span data-ttu-id="d02b8-427">Ten atrybut musi mieć jedną z następujących wartości.</span><span class="sxs-lookup"><span data-stu-id="d02b8-427">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="d02b8-428">-override - zastępuje wartość parametru istniejących.</span><span class="sxs-lookup"><span data-stu-id="d02b8-428">-   override - replaces the value of the existing parameter.</span></span><br /><span data-ttu-id="d02b8-429">-skip — nie zastępuje istniejącą wartość parametru zapytania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-429">-   skip - does not replace the existing query parameter value.</span></span><br /><span data-ttu-id="d02b8-430">-dołączania - dołącza wartość do istniejącej wartości parametru zapytania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-430">-   append - appends the value to the existing query parameter value.</span></span><br /><span data-ttu-id="d02b8-431">-Usunięcie — usuwa parametr zapytania z żądania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-431">-   delete - removes the query parameter from the request.</span></span><br /><br /> <span data-ttu-id="d02b8-432">Jeśli wartość `override` powoduje rejestrowanie wiele wpisów z tą samą nazwą parametru zapytania ustawiany zgodnie ze wszystkich zapisów (które zostaną wyświetlone wiele razy); zostanie ustawiona tylko wartości wyświetlane w wynikach.</span><span class="sxs-lookup"><span data-stu-id="d02b8-432">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="d02b8-433">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-433">No</span></span>|<span data-ttu-id="d02b8-434">zastąpienie</span><span class="sxs-lookup"><span data-stu-id="d02b8-434">override</span></span>|  
|<span data-ttu-id="d02b8-435">name</span><span class="sxs-lookup"><span data-stu-id="d02b8-435">name</span></span>|<span data-ttu-id="d02b8-436">Określa nazwę parametru zapytania do ustawienia.</span><span class="sxs-lookup"><span data-stu-id="d02b8-436">Specifies name of the query parameter to be set.</span></span>|<span data-ttu-id="d02b8-437">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-437">Yes</span></span>|<span data-ttu-id="d02b8-438">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d02b8-439">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d02b8-439">Usage</span></span>  
 <span data-ttu-id="d02b8-440">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d02b8-440">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d02b8-441">**Sekcje zasad:** wewnętrznej bazy danych dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="d02b8-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="d02b8-442">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="d02b8-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d02b8-443"><a name="RewriteURL"></a>Ponowne zapisywanie adresów URL</span><span class="sxs-lookup"><span data-stu-id="d02b8-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="d02b8-444">`rewrite-uri` Zasad konwertuje adresie URL żądania postaci publicznego formularza oczekiwane przez usługę sieci web, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d02b8-444">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span></span>  
  
-   <span data-ttu-id="d02b8-445">Publiczny adres URL-`http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="d02b8-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="d02b8-446">Adres URL żądania —`http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="d02b8-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="d02b8-447">Ta zasada służy podczas transformacji człowieka i/lub przeglądarki przyjaznego adresu URL do formatu URL oczekiwanego przez usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="d02b8-447">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span></span> <span data-ttu-id="d02b8-448">Ta zasada musi tylko ma być stosowany podczas udostępnianie innego formatu adresu URL, takie jak czystą adresów URL, adresy URL RESTful, adresów URL przyjaznych dla użytkownika lub adresów URL przyjaznych dla aparatów wyszukiwania, które są całkowicie strukturalnych adresów URL, które nie zawierają ciągu zapytania i zamiast tego zawierają tylko ścieżki zasobu (po schemat i Urząd).</span><span class="sxs-lookup"><span data-stu-id="d02b8-448">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span></span> <span data-ttu-id="d02b8-449">Często jest to estetycznych, użyteczność lub aparat wyszukiwania (SEO) optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="d02b8-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d02b8-450">Można dodawać tylko przy użyciu zasad parametrów ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-450">You can only add query string parameters using the policy.</span></span> <span data-ttu-id="d02b8-451">Nie można dodać szablon dodatkowe parametry ścieżki w adresie URL ponownego zapisywania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-451">You cannot add extra template path parameters in the rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="d02b8-452">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="d02b8-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="d02b8-453">Przykład</span><span class="sxs-lookup"><span data-stu-id="d02b8-453">Example</span></span>  
  
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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

### <a name="elements"></a><span data-ttu-id="d02b8-454">Elementy</span><span class="sxs-lookup"><span data-stu-id="d02b8-454">Elements</span></span>  
  
|<span data-ttu-id="d02b8-455">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-455">Name</span></span>|<span data-ttu-id="d02b8-456">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-456">Description</span></span>|<span data-ttu-id="d02b8-457">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d02b8-458">Identyfikator uri ponownego napisania</span><span class="sxs-lookup"><span data-stu-id="d02b8-458">rewrite-uri</span></span>|<span data-ttu-id="d02b8-459">Element główny.</span><span class="sxs-lookup"><span data-stu-id="d02b8-459">Root element.</span></span>|<span data-ttu-id="d02b8-460">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d02b8-461">Atrybuty</span><span class="sxs-lookup"><span data-stu-id="d02b8-461">Attributes</span></span>  
  
|<span data-ttu-id="d02b8-462">Atrybut</span><span class="sxs-lookup"><span data-stu-id="d02b8-462">Attribute</span></span>|<span data-ttu-id="d02b8-463">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-463">Description</span></span>|<span data-ttu-id="d02b8-464">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-464">Required</span></span>|<span data-ttu-id="d02b8-465">Domyślne</span><span class="sxs-lookup"><span data-stu-id="d02b8-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="d02b8-466">szablon</span><span class="sxs-lookup"><span data-stu-id="d02b8-466">template</span></span>|<span data-ttu-id="d02b8-467">Adres URL usługi sieci web rzeczywiste wszystkie parametry ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="d02b8-467">The actual web service URL with any query string parameters.</span></span> <span data-ttu-id="d02b8-468">Używając wyrażenia wartości całkowitej musi być wyrażeniem.</span><span class="sxs-lookup"><span data-stu-id="d02b8-468">When using expressions, the whole value must be an expression.</span></span>|<span data-ttu-id="d02b8-469">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-469">Yes</span></span>|<span data-ttu-id="d02b8-470">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="d02b8-470">N/A</span></span>|  
|<span data-ttu-id="d02b8-471">Kopiuj niedopasowane — parametry</span><span class="sxs-lookup"><span data-stu-id="d02b8-471">copy-unmatched-params</span></span>|<span data-ttu-id="d02b8-472">Określa, czy parametry zapytania w żądaniu przychodzącym nie znajduje się w oryginalnym szablonie adres URL są dodawane do adresu URL zdefiniowanej w szablonie Napisz ponownie</span><span class="sxs-lookup"><span data-stu-id="d02b8-472">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span></span>|<span data-ttu-id="d02b8-473">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-473">No</span></span>|<span data-ttu-id="d02b8-474">Wartość true</span><span class="sxs-lookup"><span data-stu-id="d02b8-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d02b8-475">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d02b8-475">Usage</span></span>  
 <span data-ttu-id="d02b8-476">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d02b8-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d02b8-477">**Sekcje zasad:** dla ruchu przychodzącego</span><span class="sxs-lookup"><span data-stu-id="d02b8-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d02b8-478">**Zakresy zasad:** operacja produktu, interfejsu API,</span><span class="sxs-lookup"><span data-stu-id="d02b8-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="d02b8-479"><a name="XSLTransform"></a>Przekształcanie XML za pomocą XSLT</span><span class="sxs-lookup"><span data-stu-id="d02b8-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="d02b8-480">`Transform XML using an XSLT` Zasady dotyczą transformacji XSL XML w treści żądania lub odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="d02b8-480">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d02b8-481">Deklaracja zasad</span><span class="sxs-lookup"><span data-stu-id="d02b8-481">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="d02b8-482">Przykład</span><span class="sxs-lookup"><span data-stu-id="d02b8-482">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d02b8-483">Elementy</span><span class="sxs-lookup"><span data-stu-id="d02b8-483">Elements</span></span>  
  
|<span data-ttu-id="d02b8-484">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d02b8-484">Name</span></span>|<span data-ttu-id="d02b8-485">Opis</span><span class="sxs-lookup"><span data-stu-id="d02b8-485">Description</span></span>|<span data-ttu-id="d02b8-486">Wymagane</span><span class="sxs-lookup"><span data-stu-id="d02b8-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d02b8-487">Transformacja XSL</span><span class="sxs-lookup"><span data-stu-id="d02b8-487">xsl-transform</span></span>|<span data-ttu-id="d02b8-488">Element główny.</span><span class="sxs-lookup"><span data-stu-id="d02b8-488">Root element.</span></span>|<span data-ttu-id="d02b8-489">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-489">Yes</span></span>|  
|<span data-ttu-id="d02b8-490">Parametr</span><span class="sxs-lookup"><span data-stu-id="d02b8-490">parameter</span></span>|<span data-ttu-id="d02b8-491">Używane do definiowania zmiennych w przekształceniu</span><span class="sxs-lookup"><span data-stu-id="d02b8-491">Used to define variables used in the transform</span></span>|<span data-ttu-id="d02b8-492">Nie</span><span class="sxs-lookup"><span data-stu-id="d02b8-492">No</span></span>|  
|<span data-ttu-id="d02b8-493">XSL: stylesheet</span><span class="sxs-lookup"><span data-stu-id="d02b8-493">xsl:stylesheet</span></span>|<span data-ttu-id="d02b8-494">Elemencie głównym arkusza stylów.</span><span class="sxs-lookup"><span data-stu-id="d02b8-494">Root stylesheet element.</span></span> <span data-ttu-id="d02b8-495">Wszystkie elementy i atrybuty zdefiniowane w ramach zgodne ze standardem [specyfikacji XSLT](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="d02b8-495">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="d02b8-496">Tak</span><span class="sxs-lookup"><span data-stu-id="d02b8-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d02b8-497">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d02b8-497">Usage</span></span>  
 <span data-ttu-id="d02b8-498">Te zasady służą następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d02b8-498">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d02b8-499">**Sekcje zasad:** przychodzące, wychodzące</span><span class="sxs-lookup"><span data-stu-id="d02b8-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="d02b8-500">**Zakresy zasad:** globalnych produktu interfejsu API, operacji</span><span class="sxs-lookup"><span data-stu-id="d02b8-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="d02b8-501">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d02b8-501">Next steps</span></span>
<span data-ttu-id="d02b8-502">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d02b8-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
