---
title: "aaaAzure API Reference zasad zarządzania"
description: "Więcej informacji na temat tooconfigure dostępne hello zasad interfejsu API zarządzania."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="c3ead-103">Informacje o zasadach usługi Azure API Management</span><span class="sxs-lookup"><span data-stu-id="c3ead-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="c3ead-104">Ta sekcja zawiera indeks dla zasad hello w hello [informacje o zasadach usługi API Management][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="c3ead-104">This section provides an index for hello policies in hello [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="c3ead-105">Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="c3ead-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="c3ead-106">Wyrażenie zasad może służyć jako wartości atrybutu lub tekst w żadnym z zasad interfejsu API zarządzania hello, chyba że zasady hello Określa, w przeciwnym razie wartość.</span><span class="sxs-lookup"><span data-stu-id="c3ead-106">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="c3ead-107">Niektóre zasady, takie jak hello [sterowania przepływem] [ Control flow] i [zmiennej zestaw] [ Set variable] zasady są oparte na wyrażeniach zasad.</span><span class="sxs-lookup"><span data-stu-id="c3ead-107">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="c3ead-108">Aby uzyskać więcej informacji, zobacz [zaawansowane zasady] [ Advanced policies] i [wyrażenie zasad][Policy expressions]</span><span class="sxs-lookup"><span data-stu-id="c3ead-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="c3ead-109">Informacje ogólne o zasadach — indeks</span><span class="sxs-lookup"><span data-stu-id="c3ead-109">Policy reference index</span></span>
* <span data-ttu-id="c3ead-110">[Zasady ograniczeń dostępu][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="c3ead-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="c3ead-111">[Nagłówek HTTP wyboru] [ Check HTTP header] — wymusza istnienia i/lub wartość nagłówka HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3ead-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="c3ead-112">[Limit szybkości wywołanie przez subskrypcji] [ Limit call rate by subscription] -API uniemożliwia użycie wzrósł poprzez ograniczenie wywołań szybkości, na podstawie subskrypcji na.</span><span class="sxs-lookup"><span data-stu-id="c3ead-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="c3ead-113">[Limit szybkości wywołanie przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) — użycie uniemożliwia API wzrósł ograniczając szybkość połączenia, na podstawie na klucz.</span><span class="sxs-lookup"><span data-stu-id="c3ead-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="c3ead-114">[Ograniczenia adresów IP wywołującego] [ Restrict caller IPs] -wywołania filtrów (umożliwia/nie zezwala na) z określonych adresów IP i/lub zakresów adresów.</span><span class="sxs-lookup"><span data-stu-id="c3ead-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="c3ead-115">[Przydział użycia zestawu subskrypcji] [ Set usage quota by subscription] — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="c3ead-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="c3ead-116">[Przydział użycia zestawu przez klucz](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie według klucza.</span><span class="sxs-lookup"><span data-stu-id="c3ead-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="c3ead-117">[Sprawdź poprawność JWT] [ Validate JWT] — wymusza istnienia i ważności wyodrębniony z określonego nagłówka HTTP lub parametr zapytania określony token JWT.</span><span class="sxs-lookup"><span data-stu-id="c3ead-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="c3ead-118">[Zaawansowane zasady][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="c3ead-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="c3ead-119">[Przepływ kontroli] [ Control flow] — warunkowo stosuje deklaracji zasad, na podstawie wyników hello oceny hello Boolean [wyrażenia][expressions].</span><span class="sxs-lookup"><span data-stu-id="c3ead-119">[Control flow][Control flow] - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="c3ead-120">[Przekazanie żądania] [ Forward request] -przekazuje hello żądania toohello wewnętrznej bazy danych usługi.</span><span class="sxs-lookup"><span data-stu-id="c3ead-120">[Forward request][Forward request] - Forwards hello request toohello backend service.</span></span>
  * <span data-ttu-id="c3ead-121">[Zaloguj się tooEvent Centrum] [ Log tooEvent Hub] — wysyła komunikaty w hello określonego formatu tooa obiektu docelowego komunikatu zdefiniowane przez [rejestratora](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) jednostki.</span><span class="sxs-lookup"><span data-stu-id="c3ead-121">[Log tooEvent Hub][Log tooEvent Hub] - Sends messages in hello specified format tooa message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="c3ead-122">[Spróbuj ponownie](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -ponownych prób wykonania hello ujęta deklaracji zasad, jeśli i dopóki nie zostanie spełniony warunek hello.</span><span class="sxs-lookup"><span data-stu-id="c3ead-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="c3ead-123">Wykonanie jest powtarzany w hello w określonych odstępach czasu i zapasowej toohello określona liczba ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="c3ead-123">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>
  * <span data-ttu-id="c3ead-124">[Odpowiedź zwrócona](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -przerwań potoku wykonywania i zwraca hello określona odpowiedź bezpośrednio toohello wywołującego.</span><span class="sxs-lookup"><span data-stu-id="c3ead-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>
  * <span data-ttu-id="c3ead-125">[Wyślij żądanie jednokierunkowej](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) — wysyła toohello żądania określony adres URL bez oczekiwania na odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="c3ead-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="c3ead-126">[Wyślij żądanie](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) — wysyła toohello żądania określonego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c3ead-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request toohello specified URL.</span></span>
  * <span data-ttu-id="c3ead-127">[Ustawia metodę żądania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) — pozwala toochange metody hello HTTP dla żądania.</span><span class="sxs-lookup"><span data-stu-id="c3ead-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>
  * <span data-ttu-id="c3ead-128">[Ustaw stan](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -toohello kod stanu hello HTTP zmiany określona wartość.</span><span class="sxs-lookup"><span data-stu-id="c3ead-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>
  * <span data-ttu-id="c3ead-129">[Ustaw zmienną] [ Set variable] -utrwalić wartości w nazwanym [kontekstu] [ context] zmiennej nowsze dostępu.</span><span class="sxs-lookup"><span data-stu-id="c3ead-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="c3ead-130">[Śledzenia](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -dodaje ciąg do hello [inspektora interfejsu API](api-management-howto-api-inspector.md) danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c3ead-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into hello [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="c3ead-131">[Poczekaj](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) — czeka na wysyłanie zamkniętych żądań, pobrać wartości z pamięci podręcznej, lub Sterowanie przepływem toocomplete zasad przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="c3ead-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies toocomplete before proceeding.</span></span>
* <span data-ttu-id="c3ead-132">[Zasady uwierzytelniania][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="c3ead-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="c3ead-133">[Uwierzytelnianie za pomocą Basic] [ Authenticate with Basic] -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="c3ead-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="c3ead-134">[Uwierzytelniania za pomocą certyfikatu klienta] [ Authenticate with client certificate] -uwierzytelniania za pomocą usługi wewnętrznej bazy danych przy użyciu certyfikatów klienta.</span><span class="sxs-lookup"><span data-stu-id="c3ead-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="c3ead-135">[Buforowanie zasad][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="c3ead-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="c3ead-136">[Pobierz z pamięci podręcznej] [ Get from cache] -wykonaj pamięci podręcznej wyszukiwania i zwracać prawidłową odpowiedź buforowana, jeśli jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="c3ead-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="c3ead-137">[Przechowywanie toocache] [ Store toocache] -pamięci podręcznych odpowiedzi zgodnie z toohello określonej konfiguracji kontroli pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c3ead-137">[Store toocache][Store toocache] - Caches response according toohello specified cache control configuration.</span></span>
  * <span data-ttu-id="c3ead-138">[Pobiera wartość z pamięci podręcznej](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) -pobrania elementu pamięci podręcznej według klucza.</span><span class="sxs-lookup"><span data-stu-id="c3ead-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="c3ead-139">[Przechowywana wartość w pamięci podręcznej](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -przechowywania elementu w pamięci podręcznej hello według klucza.</span><span class="sxs-lookup"><span data-stu-id="c3ead-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>
  * <span data-ttu-id="c3ead-140">[Usuń wartość z pamięci podręcznej](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -usunięcie elementu w pamięci podręcznej hello według klucza.</span><span class="sxs-lookup"><span data-stu-id="c3ead-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>
* <span data-ttu-id="c3ead-141">[Krzyżowe zasady domeny][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="c3ead-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="c3ead-142">[Zezwalaj na połączenia między domenami] [ Allow cross-domain calls] — sprawia, że interfejs API hello dostępne od klientów programu Adobe Flash i Microsoft Silverlight bazujące na przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="c3ead-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="c3ead-143">[CORS] [ CORS] -dodaje współużytkowanie zasobów między źródłami (CORS) obsługuje tooan operacji lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="c3ead-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="c3ead-144">[JSONP] [ JSONP] — dodaje JSON dopełnienie (JSONP) operacji tooan pomocy technicznej lub międzydomenowego interfejsu API tooallow wymaga od klientów przeglądarki JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c3ead-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="c3ead-145">[Zasad przekształcania][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="c3ead-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="c3ead-146">[Konwertuj JSON tooXML] [ Convert JSON tooXML] — konwertuje żądania lub odpowiedzi body z JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="c3ead-146">[Convert JSON tooXML][Convert JSON tooXML] - Converts request or response body from JSON tooXML.</span></span>
  * <span data-ttu-id="c3ead-147">[Konwertuj XML tooJSON] [ Convert XML tooJSON] — konwertuje żądania lub odpowiedzi body z XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="c3ead-147">[Convert XML tooJSON][Convert XML tooJSON] - Converts request or response body from XML tooJSON.</span></span>
  * <span data-ttu-id="c3ead-148">[Znajdowanie i zamienianie ciągów w treści] [ Find and replace string in body] — znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.</span><span class="sxs-lookup"><span data-stu-id="c3ead-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="c3ead-149">[Maski adresów URL w zawartości] [ Mask URLs in content] -ponownie zapisuje (maski) łącza w odpowiedzi hello body tak, aby wskazywały toohello równoważne połączenie za pośrednictwem bramy hello.</span><span class="sxs-lookup"><span data-stu-id="c3ead-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>
  * <span data-ttu-id="c3ead-150">[Ustaw usługę zaplecza] [ Set backend service] — zmienia hello usługi wewnętrznej bazy danych dla żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="c3ead-150">[Set backend service][Set backend service] - Changes hello backend service for an incoming request.</span></span>
  * <span data-ttu-id="c3ead-151">[Ustaw treści] [ Set body] -ustawia treść wiadomości powitania żądań przychodzących i wychodzących.</span><span class="sxs-lookup"><span data-stu-id="c3ead-151">[Set body][Set body] - Sets hello message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="c3ead-152">[Set — nagłówek HTTP] [ Set HTTP header] — przypisuje wartość tooan istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.</span><span class="sxs-lookup"><span data-stu-id="c3ead-152">[Set HTTP header][Set HTTP header] - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="c3ead-153">[Wartość parametru ciągu zapytania] [ Set query string parameter] — dodaje, zastępuje wartość lub usuwa parametru ciągu zapytania żądania.</span><span class="sxs-lookup"><span data-stu-id="c3ead-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="c3ead-154">[Ponowne zapisywanie adresów URL] [ Rewrite URL] — konwertuje adres URL żądania w postaci toohello publicznego formularza oczekiwane przez usługę sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="c3ead-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form toohello form expected by hello web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3ead-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c3ead-155">Next steps</span></span>
<span data-ttu-id="c3ead-156">Aby uzyskać więcej informacji na wyrażenia zasad Zobacz powitania po wideo.</span><span class="sxs-lookup"><span data-stu-id="c3ead-156">For more information on policy expressions, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


