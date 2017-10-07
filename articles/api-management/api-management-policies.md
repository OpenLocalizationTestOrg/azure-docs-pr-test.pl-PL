---
title: "zasady usługi API Management aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad hello dostępne do użycia w usłudze Azure API Management."
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
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="d5fd9-103">API Management policies</span><span class="sxs-lookup"><span data-stu-id="d5fd9-103">API Management policies</span></span>
<span data-ttu-id="d5fd9-104">W tej sekcji znajdują się informacje na następujące zasady usługi API Management hello.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-104">This section provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="d5fd9-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d5fd9-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="d5fd9-106">Zasady są zaawansowanych możliwości hello system, który umożliwia zachowanie hello toochange hello interfejsu API za pomocą konfiguracji hello wydawcy.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-106">Policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="d5fd9-107">Zasady są zbiór instrukcji, które są wykonywane sekwencyjnie na powitania żądania lub odpowiedzi interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-107">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="d5fd9-108">Popularne instrukcje obejmują Konwersja formatu XML tooJSON i Wywołaj tempa ograniczania toorestrict hello ilość przychodzących od dewelopera.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-108">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="d5fd9-109">Wiele zasad są dostępne fabrycznej hello.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-109">Many more policies are available out of hello box.</span></span>  
  
 <span data-ttu-id="d5fd9-110">Wyrażenie zasad może służyć jako wartości atrybutu lub tekst w żadnym z zasad interfejsu API zarządzania hello, chyba że zasady hello Określa, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-110">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="d5fd9-111">Niektóre zasady, takie jak hello [sterowania przepływem](api-management-advanced-policies.md#choose) i [zmiennej zestaw](api-management-advanced-policies.md#set-variable) zasady są oparte na wyrażeniach zasad.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-111">Some policies such as hello [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="d5fd9-112">Aby uzyskać więcej informacji, zobacz [zaawansowane zasady](api-management-advanced-policies.md#AdvancedPolicies) i [wyrażenie zasad](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="d5fd9-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="d5fd9-113"><a name="ProxyPolicies"></a>Zasady</span><span class="sxs-lookup"><span data-stu-id="d5fd9-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="d5fd9-114">Zasady ograniczeń dostępu</span><span class="sxs-lookup"><span data-stu-id="d5fd9-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="d5fd9-115">[Nagłówek HTTP wyboru](api-management-access-restriction-policies.md#CheckHTTPHeader) — wymusza istnienia i/lub wartość nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="d5fd9-116">[Limit szybkości wywołanie przez subskrypcji](api-management-access-restriction-policies.md#LimitCallRate) — użycie uniemożliwia API wzrósł poprzez ograniczenie wywołań szybkości, na podstawie subskrypcji na.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="d5fd9-117">[Limit szybkości wywołanie przez klucz](api-management-access-restriction-policies.md#LimitCallRateByKey) — użycie uniemożliwia API wzrósł ograniczając szybkość połączenia, na podstawie na klucz.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="d5fd9-118">[Ograniczenia adresów IP wywołującego](api-management-access-restriction-policies.md#RestrictCallerIPs) -wywołania filtrów (umożliwia/nie zezwala na) z określonych adresów IP i/lub zakresów adresów.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="d5fd9-119">[Przydział użycia zestawu subskrypcji](api-management-access-restriction-policies.md#SetUsageQuota) — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="d5fd9-120">[Przydział użycia zestawu przez klucz](api-management-access-restriction-policies.md#SetUsageQuotaByKey) — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie według klucza.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="d5fd9-121">[Sprawdź poprawność JWT](api-management-access-restriction-policies.md#ValidateJWT) — wymusza istnienia i ważności wyodrębniony z określonego nagłówka HTTP lub parametr zapytania określony token JWT.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="d5fd9-122">Zasady zaawansowane</span><span class="sxs-lookup"><span data-stu-id="d5fd9-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="d5fd9-123">[Przepływ kontroli](api-management-advanced-policies.md#choose) — warunkowo stosuje deklaracji zasad oparte na ocenie hello wyrażeń logicznych.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="d5fd9-124">[Przekazanie żądania](api-management-advanced-policies.md#ForwardRequest) -przekazuje hello żądania toohello wewnętrznej bazy danych usługi.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards hello request toohello backend service.</span></span>  
  
    -   <span data-ttu-id="d5fd9-125">[Zaloguj się tooEvent Centrum](api-management-advanced-policies.md#log-to-eventhub) — wysyła komunikaty w hello określonego formatu tooa obiektu docelowego komunikatu zdefiniowanych przez podmiot rejestratora.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-125">[Log tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in hello specified format tooa message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="d5fd9-126">[Spróbuj ponownie](api-management-advanced-policies.md#Retry) -ponownych prób wykonania hello ujęta deklaracji zasad, jeśli i dopóki nie zostanie spełniony warunek hello.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="d5fd9-127">Wykonanie jest powtarzany w hello w określonych odstępach czasu i zapasowej toohello określona liczba ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-127">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
    -   <span data-ttu-id="d5fd9-128">[Odpowiedź zwrócona](api-management-advanced-policies.md#ReturnResponse) -przerwań potoku wykonywania i zwraca hello określona odpowiedź bezpośrednio toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>  
  
    -   <span data-ttu-id="d5fd9-129">[Wyślij żądanie jednokierunkowej](api-management-advanced-policies.md#SendOneWayRequest) — wysyła toohello żądania określony adres URL bez oczekiwania na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="d5fd9-130">[Wyślij żądanie](api-management-advanced-policies.md#SendRequest) — wysyła toohello żądania określonego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request toohello specified URL.</span></span>  
  
    -   <span data-ttu-id="d5fd9-131">[Ustaw zmienną](api-management-advanced-policies.md#set-variable) -utrwalić wartość w zmiennej o nazwie kontekstu nowsze dostępu.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="d5fd9-132">[Ustawia metodę żądania](api-management-advanced-policies.md#SetRequestMethod) — pozwala toochange metody hello HTTP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="d5fd9-133">[Ustaw kod stanu](api-management-advanced-policies.md#SetStatus) -toohello kod stanu hello HTTP zmiany określona wartość.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
    -   <span data-ttu-id="d5fd9-134">[Śledzenia](api-management-advanced-policies.md#Trace) -dodaje ciąg do hello [inspektora interfejsu API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="d5fd9-135">[Poczekaj](api-management-advanced-policies.md#Wait) -oczekuje dla ujęta [żądanie wysłania](api-management-advanced-policies.md#SendRequest), [pobrać wartości z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey), lub [sterowania przepływem](api-management-advanced-policies.md#choose) toocomplete zasad przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
-   [<span data-ttu-id="d5fd9-136">Zasady uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="d5fd9-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="d5fd9-137">[Uwierzytelnianie za pomocą Basic](api-management-authentication-policies.md#Basic) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="d5fd9-138">[Uwierzytelniania za pomocą certyfikatu klienta](api-management-authentication-policies.md#ClientCertificate) -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="d5fd9-139">Caching policies</span><span class="sxs-lookup"><span data-stu-id="d5fd9-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="d5fd9-140">[Pobierz z pamięci podręcznej](api-management-caching-policies.md#GetFromCache) — wykonaj pamięci podręcznej wyszukiwania i zwracać prawidłową odpowiedź buforowana, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="d5fd9-141">[Przechowywanie toocache](api-management-caching-policies.md#StoreToCache) -pamięci podręcznych odpowiedzi zgodnie z toohello określonej konfiguracji kontroli pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-141">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches response according toohello specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="d5fd9-142">[Pobiera wartość z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey) -pobrania elementu pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="d5fd9-143">[Przechowywana wartość w pamięci podręcznej](api-management-caching-policies.md#StoreToCacheByKey) -przechowywania elementu w pamięci podręcznej hello według klucza.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="d5fd9-144">[Usuń wartość z pamięci podręcznej](api-management-caching-policies.md#RemoveCacheByKey) -usunięcie elementu w pamięci podręcznej hello według klucza.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
-   [<span data-ttu-id="d5fd9-145">Zasady międzydomenowe</span><span class="sxs-lookup"><span data-stu-id="d5fd9-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="d5fd9-146">[Zezwalaj na połączenia między domenami](api-management-cross-domain-policies.md#AllowCrossDomainCalls) — sprawia, że interfejs API hello dostępne od klientów programu Adobe Flash i Microsoft Silverlight bazujące na przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="d5fd9-147">[CORS](api-management-cross-domain-policies.md#CORS) -dodaje współużytkowanie zasobów między źródłami (CORS) obsługuje tooan operacji lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="d5fd9-148">[JSONP](api-management-cross-domain-policies.md#JSONP) — dodaje JSON dopełnienie (JSONP) operacji tooan pomocy technicznej lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="d5fd9-149">Zasady transformacji</span><span class="sxs-lookup"><span data-stu-id="d5fd9-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="d5fd9-150">[Konwertuj JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) — konwertuje żądania lub odpowiedzi body z JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-150">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
    -   <span data-ttu-id="d5fd9-151">[Konwertuj XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) — konwertuje żądania lub odpowiedzi body z XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-151">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
    -   <span data-ttu-id="d5fd9-152">[Znajdowanie i zamienianie ciągów w treści](api-management-transformation-policies.md#Findandreplacestringinbody) — znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="d5fd9-153">[Maski adresów URL w zawartości](api-management-transformation-policies.md#MaskURLSContent) -ponownie zapisuje (maski) łącza w odpowiedzi hello body tak, aby wskazywały toohello równoważne połączenie za pośrednictwem bramy hello.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
    -   <span data-ttu-id="d5fd9-154">[Ustaw usługę zaplecza](api-management-transformation-policies.md#SetBackendService) — zmienia hello usługi wewnętrznej bazy danych dla żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="d5fd9-155">[Ustaw treści](api-management-transformation-policies.md#SetBody) -ustawia treść wiadomości powitania żądań przychodzących i wychodzących.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="d5fd9-156">[Set — nagłówek HTTP](api-management-transformation-policies.md#SetHTTPheader) — przypisuje wartość tooan istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="d5fd9-157">[Wartość parametru ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) — dodaje, zastępuje wartość lub usuwa parametru ciągu zapytania żądania.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="d5fd9-158">[Ponowne zapisywanie adresów URL](api-management-transformation-policies.md#RewriteURL) — konwertuje adres URL żądania w postaci toohello publicznego formularza oczekiwane przez usługę sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
    -   <span data-ttu-id="d5fd9-159">[Przekształcanie XML za pomocą XSLT](api-management-transformation-policies.md#XSLTransform) — ma zastosowanie tooXML transformacji XSL w treści żądania lub odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="d5fd9-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="d5fd9-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5fd9-160">Next steps</span></span>
<span data-ttu-id="d5fd9-161">Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d5fd9-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
