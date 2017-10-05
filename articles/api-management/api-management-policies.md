---
title: "Zasady zarządzania interfejsu API platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o zasadach dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 485dc3a87a81dc67f5144596a30d498293d6b76a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="c585d-103">API Management policies</span><span class="sxs-lookup"><span data-stu-id="c585d-103">API Management policies</span></span>
<span data-ttu-id="c585d-104">W tej sekcji znajdują się informacje na następujące zasady usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="c585d-104">This section provides a reference for the following API Management policies.</span></span> <span data-ttu-id="c585d-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c585d-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="c585d-106">Zasady są zaawansowanych możliwości systemu, który umożliwia wydawcy, aby zmienić zachowanie interfejsu API za pomocą konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c585d-106">Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="c585d-107">Zasady są zbiór instrukcji, które są wykonywane sekwencyjnie na żądanie lub odpowiedź interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c585d-107">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="c585d-108">Popularne instrukcje obejmują Konwersja formatu z pliku XML do formatu JSON i Wywołaj szybkość ograniczenie, aby ograniczyć ilość przychodzących od dewelopera.</span><span class="sxs-lookup"><span data-stu-id="c585d-108">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="c585d-109">Wiele zasad są dostępne poza pole.</span><span class="sxs-lookup"><span data-stu-id="c585d-109">Many more policies are available out of the box.</span></span>  
  
 <span data-ttu-id="c585d-110">Wyrażenia zasad mogą służyć jako wartości atrybutów lub wartości tekstowe w dowolnej z zasad usługi API Management, o ile w zasadach nie określono inaczej.</span><span class="sxs-lookup"><span data-stu-id="c585d-110">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="c585d-111">Niektóre zasady, np. [Przepływ sterowania](api-management-advanced-policies.md#choose) i [Ustawianie zmiennej](api-management-advanced-policies.md#set-variable), są oparte na wyrażeniach zasad.</span><span class="sxs-lookup"><span data-stu-id="c585d-111">Some policies such as the [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="c585d-112">Aby uzyskać więcej informacji, zobacz [zaawansowane zasady](api-management-advanced-policies.md#AdvancedPolicies) i [wyrażenie zasad](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="c585d-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="c585d-113"><a name="ProxyPolicies"></a>Zasady</span><span class="sxs-lookup"><span data-stu-id="c585d-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="c585d-114">Zasady ograniczeń dostępu</span><span class="sxs-lookup"><span data-stu-id="c585d-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="c585d-115">[Nagłówek HTTP wyboru](api-management-access-restriction-policies.md#CheckHTTPHeader) — wymusza istnienia i/lub wartość nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="c585d-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="c585d-116">[Limit szybkości wywołanie przez subskrypcji](api-management-access-restriction-policies.md#LimitCallRate) — użycie uniemożliwia API wzrósł poprzez ograniczenie wywołań szybkości, na podstawie subskrypcji na.</span><span class="sxs-lookup"><span data-stu-id="c585d-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="c585d-117">[Limit szybkości wywołanie przez klucz](api-management-access-restriction-policies.md#LimitCallRateByKey) — użycie uniemożliwia API wzrósł ograniczając szybkość połączenia, na podstawie na klucz.</span><span class="sxs-lookup"><span data-stu-id="c585d-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="c585d-118">[Ograniczenia adresów IP wywołującego](api-management-access-restriction-policies.md#RestrictCallerIPs) -wywołania filtrów (umożliwia/nie zezwala na) z określonych adresów IP i/lub zakresów adresów.</span><span class="sxs-lookup"><span data-stu-id="c585d-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="c585d-119">[Ustaw przydział użycia subskrypcji](api-management-access-restriction-policies.md#SetUsageQuota) — umożliwia egzekwowanie odnawialnymi lub okres istnienia wywołania woluminu i/lub przepustowości limit przydziału, na podstawie na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="c585d-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="c585d-120">[Ustaw przydział użycia przez klucz](api-management-access-restriction-policies.md#SetUsageQuotaByKey) — umożliwia egzekwowanie odnawialnymi lub okres istnienia wywołania woluminu i/lub przepustowości limit przydziału, na podstawie według klucza.</span><span class="sxs-lookup"><span data-stu-id="c585d-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="c585d-121">[Sprawdź poprawność JWT](api-management-access-restriction-policies.md#ValidateJWT) — wymusza istnienia i ważności wyodrębniony z określonego nagłówka HTTP lub parametr zapytania określony token JWT.</span><span class="sxs-lookup"><span data-stu-id="c585d-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="c585d-122">Zasady zaawansowane</span><span class="sxs-lookup"><span data-stu-id="c585d-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="c585d-123">[Przepływ kontroli](api-management-advanced-policies.md#choose) — warunkowo stosuje deklaracji zasad, na podstawie oceny wyrażeń logicznych.</span><span class="sxs-lookup"><span data-stu-id="c585d-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="c585d-124">[Przekazanie żądania](api-management-advanced-policies.md#ForwardRequest) -przekazuje żądanie do usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="c585d-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
    -   <span data-ttu-id="c585d-125">[Dziennika do Centrum zdarzeń](api-management-advanced-policies.md#log-to-eventhub) — wysyła komunikaty w określonym formacie do obiektu docelowego komunikatu zdefiniowanych przez podmiot rejestratora.</span><span class="sxs-lookup"><span data-stu-id="c585d-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="c585d-126">[Spróbuj ponownie](api-management-advanced-policies.md#Retry) -ponowi próbę wykonania instrukcji objętego zasad, jeśli i do momentu spełnienia warunku.</span><span class="sxs-lookup"><span data-stu-id="c585d-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="c585d-127">Wykonanie Powtórz w określonych odstępach czasu, a także do określonej liczba ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="c585d-127">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
    -   <span data-ttu-id="c585d-128">[Odpowiedź zwrócona](api-management-advanced-policies.md#ReturnResponse) -przerwań potoku wykonywania i zwraca określoną odpowiedzią bezpośrednio do obiektu wywołującego.</span><span class="sxs-lookup"><span data-stu-id="c585d-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
    -   <span data-ttu-id="c585d-129">[Wyślij żądanie jednokierunkowej](api-management-advanced-policies.md#SendOneWayRequest) — wysyła żądanie pod określony adres URL bez oczekiwania na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="c585d-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="c585d-130">[Wyślij żądanie](api-management-advanced-policies.md#SendRequest) — wysyła żądanie do określonego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c585d-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.</span></span>  
  
    -   <span data-ttu-id="c585d-131">[Ustaw zmienną](api-management-advanced-policies.md#set-variable) -utrwalić wartość w zmiennej o nazwie kontekstu nowsze dostępu.</span><span class="sxs-lookup"><span data-stu-id="c585d-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="c585d-132">[Ustawia metodę żądania](api-management-advanced-policies.md#SetRequestMethod) — umożliwia zmianę metody HTTP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="c585d-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="c585d-133">[Ustaw kod stanu](api-management-advanced-policies.md#SetStatus) — zmienia kod stanu HTTP do określonej wartości.</span><span class="sxs-lookup"><span data-stu-id="c585d-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
    -   <span data-ttu-id="c585d-134">[Śledzenia](api-management-advanced-policies.md#Trace) -dodaje ciąg do [inspektora interfejsu API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c585d-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="c585d-135">[Poczekaj](api-management-advanced-policies.md#Wait) -oczekuje dla ujęta [żądanie wysłania](api-management-advanced-policies.md#SendRequest), [pobrać wartości z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey), lub [sterowania przepływem](api-management-advanced-policies.md#choose) zasad, aby ukończyć przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="c585d-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
-   [<span data-ttu-id="c585d-136">Zasady uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="c585d-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="c585d-137">[Uwierzytelnianie za pomocą Basic](api-management-authentication-policies.md#Basic) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="c585d-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="c585d-138">[Uwierzytelniania za pomocą certyfikatu klienta](api-management-authentication-policies.md#ClientCertificate) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="c585d-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="c585d-139">Caching policies</span><span class="sxs-lookup"><span data-stu-id="c585d-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="c585d-140">[Pobierz z pamięci podręcznej](api-management-caching-policies.md#GetFromCache) — wykonaj pamięci podręcznej wyszukiwania i zwracać prawidłową odpowiedź buforowana, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="c585d-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="c585d-141">[Magazynu pamięci podręcznej](api-management-caching-policies.md#StoreToCache) -buforuje odpowiedzi zgodnie z określonym pamięci podręcznej konfiguracji kontroli.</span><span class="sxs-lookup"><span data-stu-id="c585d-141">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="c585d-142">[Pobiera wartość z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey) -pobrania elementu pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="c585d-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="c585d-143">[Przechowywana wartość w pamięci podręcznej](api-management-caching-policies.md#StoreToCacheByKey) -przechowywania elementu w pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="c585d-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="c585d-144">[Usuń wartość z pamięci podręcznej](api-management-caching-policies.md#RemoveCacheByKey) -usunięcie elementu w pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="c585d-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
-   [<span data-ttu-id="c585d-145">Zasady międzydomenowe</span><span class="sxs-lookup"><span data-stu-id="c585d-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="c585d-146">[Zezwalaj na połączenia między domenami](api-management-cross-domain-policies.md#AllowCrossDomainCalls) — może ułatwić interfejsu API programu Adobe Flash i Microsoft Silverlight bazujące na przeglądarce klientów.</span><span class="sxs-lookup"><span data-stu-id="c585d-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="c585d-147">[CORS](api-management-cross-domain-policies.md#CORS) -dodaje współużytkowanie zasobów między źródłami (CORS) obsługi operacji lub interfejsu API w celu zapewnienia obsługi wywołań między domenami od klientów przeglądarki do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="c585d-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="c585d-148">[JSONP](api-management-cross-domain-policies.md#JSONP) -dodaje JSON z obsługą dopełnienie (JSONP) do operacji lub interfejsu API w celu zapewnienia obsługi wywołań między domenami od klientów przeglądarki JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c585d-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="c585d-149">Zasady transformacji</span><span class="sxs-lookup"><span data-stu-id="c585d-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="c585d-150">[Konwertuj JSON do pliku XML](api-management-transformation-policies.md#ConvertJSONtoXML) — konwertuje żądania lub odpowiedzi body z formatu JSON do pliku XML.</span><span class="sxs-lookup"><span data-stu-id="c585d-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
    -   <span data-ttu-id="c585d-151">[Konwertuj do formatu JSON XML](api-management-transformation-policies.md#ConvertXMLtoJSON) — konwertuje żądania lub odpowiedzi body z pliku XML do formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="c585d-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
    -   <span data-ttu-id="c585d-152">[Znajdowanie i zamienianie ciągów w treści](api-management-transformation-policies.md#Findandreplacestringinbody) — znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.</span><span class="sxs-lookup"><span data-stu-id="c585d-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="c585d-153">[Maski adresów URL w zawartości](api-management-transformation-policies.md#MaskURLSContent) -ponownie zapisuje (maski) łącza w odpowiedzi body tak, aby wskazywać równoważne połączenie za pośrednictwem bramy.</span><span class="sxs-lookup"><span data-stu-id="c585d-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
    -   <span data-ttu-id="c585d-154">[Ustaw usługę zaplecza](api-management-transformation-policies.md#SetBackendService) — zmienia usługi wewnętrznej bazy danych dla żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="c585d-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="c585d-155">[Ustaw treści](api-management-transformation-policies.md#SetBody) -ustawia treść komunikatu dla żądań przychodzących i wychodzących.</span><span class="sxs-lookup"><span data-stu-id="c585d-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="c585d-156">[Set — nagłówek HTTP](api-management-transformation-policies.md#SetHTTPheader) — przypisuje wartość do istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.</span><span class="sxs-lookup"><span data-stu-id="c585d-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="c585d-157">[Wartość parametru ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) — dodaje, zastępuje wartość lub usuwa parametru ciągu zapytania żądania.</span><span class="sxs-lookup"><span data-stu-id="c585d-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="c585d-158">[Ponowne zapisywanie adresów URL](api-management-transformation-policies.md#RewriteURL) — konwertuje adresie URL żądania w postaci publicznego do formularza oczekiwane przez usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="c585d-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
    -   <span data-ttu-id="c585d-159">[Przekształcanie XML za pomocą XSLT](api-management-transformation-policies.md#XSLTransform) — ma zastosowanie transformacji XSL do formatu XML w treści żądania lub odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="c585d-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c585d-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c585d-160">Next steps</span></span>
<span data-ttu-id="c585d-161">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c585d-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
