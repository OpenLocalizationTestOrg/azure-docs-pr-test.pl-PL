---
title: "Buforowanie niestandardowych w usłudze Azure API Management"
description: "Dowiedz się, jak i pamięci podręcznej elementów przez klucz w usłudze Azure API Management"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f5d5f44e34fbcd122a10be0ca5b3001760c4c64d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="f6596-103">Buforowanie niestandardowych w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="f6596-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="f6596-104">Usługa Azure API Management ma wbudowaną obsługę [buforowanie odpowiedzi HTTP](api-management-howto-cache.md) przy użyciu adresu URL zasobu jako klucz.</span><span class="sxs-lookup"><span data-stu-id="f6596-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="f6596-105">Klucz może być modyfikowany przez nagłówki żądania przy użyciu `vary-by` właściwości.</span><span class="sxs-lookup"><span data-stu-id="f6596-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="f6596-106">Jest to przydatne w przypadku buforowanie całej odpowiedzi HTTP (alias oświadczenia), ale czasami jest przydatne do pamięci podręcznej tylko część reprezentacji.</span><span class="sxs-lookup"><span data-stu-id="f6596-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="f6596-107">Nowy [pamięci podręcznej wyszukiwania wartości](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) i [-magazynu wartość w pamięci podręcznej](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) zasady umożliwiają przechowywanie i pobieranie dowolnych fragmentów danych z poziomu definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="f6596-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="f6596-108">Tę możliwość również dodaje wartość poprzednio wprowadzone [żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) zasad ponieważ teraz może buforować odpowiedzi z usług zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="f6596-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="f6596-109">Architektura</span><span class="sxs-lookup"><span data-stu-id="f6596-109">Architecture</span></span>
<span data-ttu-id="f6596-110">Zarządzanie interfejsami API usługi używa pamięci podręcznej danych dzierżawy udostępnionego tak, aby podczas skalowania do wielu jednostkach nadal uzyskają dostęp do tej samej dane z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f6596-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you will still get access to the same cached data.</span></span> <span data-ttu-id="f6596-111">Podczas pracy z wdrożenia w przypadku istnieją niezależne pamięci podręcznych w poszczególnych regionach.</span><span class="sxs-lookup"><span data-stu-id="f6596-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="f6596-112">Ze względu na to koniecznie traktuje jako magazynu danych, gdzie jest tylko źródło dla elementu informacji o pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f6596-112">Due to this, it is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="f6596-113">Jeśli została i później chcę korzystać z wdrożenia w przypadku klientów z użytkowników, którzy podróżują mogą stracić dostęp do pamięci podręcznej danych.</span><span class="sxs-lookup"><span data-stu-id="f6596-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="f6596-114">Buforowanie fragmentu</span><span class="sxs-lookup"><span data-stu-id="f6596-114">Fragment caching</span></span>
<span data-ttu-id="f6596-115">Brak niektórych przypadkach, gdy odpowiedzi zwracanych zawiera pewną część danych, jest kosztowna ustalić, który jeszcze pozostaje świeże sensownym czasie.</span><span class="sxs-lookup"><span data-stu-id="f6596-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="f6596-116">Na przykład należy wziąć pod uwagę usługę utworzony przez linii lotniczych, który zawiera informacje dotyczące zastrzeżenia transmitowane, stan transmitowane itp. Jeśli użytkownik jest członkiem program punktów airlines, również zostałyby informacji dotyczących ich bieżący stan i zebraniu przebiegu.</span><span class="sxs-lookup"><span data-stu-id="f6596-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and mileage accumulated.</span></span> <span data-ttu-id="f6596-117">Te informacje dotyczące użytkowników mogą być przechowywane w innym systemie, ale może być pożądane, aby uwzględnić go w odpowiedzi dotyczące stanu transmitowane i zastrzeżenia zwrócone.</span><span class="sxs-lookup"><span data-stu-id="f6596-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="f6596-118">Można to zrobić w procesie zwanym buforowanie fragmentu.</span><span class="sxs-lookup"><span data-stu-id="f6596-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="f6596-119">Reprezentacja głównej mogą być zwracane z serwera pochodzenia przy użyciu określonego rodzaju token, aby wskazać, gdzie jest informacji dotyczących użytkownika ma zostać wstawiony.</span><span class="sxs-lookup"><span data-stu-id="f6596-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="f6596-120">Należy wziąć pod uwagę następujące odpowiedzi JSON z zaplecza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f6596-120">Consider the following JSON response from a backend API.</span></span>

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

<span data-ttu-id="f6596-121">I dodatkowej zasobu pod adresem `/userprofile/{userid}` takie, jak,</span><span class="sxs-lookup"><span data-stu-id="f6596-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="f6596-122">Aby było możliwe określenie odpowiedniego użytkownika informacje do uwzględnienia, należy określić kto jest użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="f6596-122">In order to determine the appropriate user information to include, we need to identify who the end user is.</span></span> <span data-ttu-id="f6596-123">Ten mechanizm jest zależy od implementacji.</span><span class="sxs-lookup"><span data-stu-id="f6596-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="f6596-124">Na przykład używam `Subject` oświadczeń z `JWT` tokenu.</span><span class="sxs-lookup"><span data-stu-id="f6596-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="f6596-125">To są przechowywane `enduserid` wartość w zmiennej kontekstu do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="f6596-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="f6596-126">Następnym krokiem jest ustalenie, jeśli poprzednie żądanie już pobrane informacje o użytkowniku i zapisana w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f6596-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="f6596-127">W tym używamy `cache-lookup-value` zasad.</span><span class="sxs-lookup"><span data-stu-id="f6596-127">For this we use the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="f6596-128">Jeśli w pamięci podręcznej, która odpowiada wartości klucza, a następnie nr nie ma wpisu `userprofile` zmiennej kontekstu, która zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="f6596-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="f6596-129">Musimy sprawdzić, powodzenia za pomocą wyszukiwania `choose` sterowanie przepływem zasad.</span><span class="sxs-lookup"><span data-stu-id="f6596-129">We check the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="f6596-130">Jeśli `userprofile` zmiennej kontekstu, która nie istnieje, a następnie zamierzamy wykonanie żądania HTTP można go pobrać.</span><span class="sxs-lookup"><span data-stu-id="f6596-130">If the `userprofile` context variable doesn’t exist, then we are going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="f6596-131">Używamy `enduserid` do konstruowania adresu URL do zasobu profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f6596-131">We use the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="f6596-132">Gdy mamy odpowiedzi możemy ściągnięcia treści tekstu z odpowiedzi i zapisze go do zmiennej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="f6596-132">Once we have the response, we can pull the body text out of the response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="f6596-133">Aby uniknąć nam konieczności żądania HTTP ponownie, gdy użytkownik przesyła innego żądania, firma Microsoft może przechowywać profil użytkownika w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f6596-133">To avoid us having to make this HTTP request again, when the same user makes another request, we can store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="f6596-134">Wartości są przechowywane w pamięci podręcznej używa dokładnie tego samego klucza, który pierwotnie próby pobrania za pomocą.</span><span class="sxs-lookup"><span data-stu-id="f6596-134">We store the value in the cache using the exact same key that we originally attempted to retrieve it with.</span></span> <span data-ttu-id="f6596-135">Czas trwania wybranego do przechowywania wartości powinny być oparte na temat często zmiany informacji i sposobu odporny na błędy użytkowników są do nieaktualne informacje.</span><span class="sxs-lookup"><span data-stu-id="f6596-135">The duration that we choose to store the value should be based on how often the information changes and how tolerant users are to out of date information.</span></span> 

<span data-ttu-id="f6596-136">Należy koniecznie należy pamiętać, że pobieranie z pamięci podręcznej jest nadal poza procesem, żądanie sieciowe i potencjalnie można nadal dodawać dziesiątki w milisekundach czas oczekiwania na żądanie.</span><span class="sxs-lookup"><span data-stu-id="f6596-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="f6596-137">Zalety trybu podczas ustalania, czy informacje o profilu użytkownika znacznie dłużej, niż ze względu na potrzeby bazy danych zapytania lub zagregowanych informacji z wielu zapleczy.</span><span class="sxs-lookup"><span data-stu-id="f6596-137">The benefits come when determining the user profile information takes significantly longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="f6596-138">Ostatnim krokiem w procesie jest aktualizacja odpowiedź zwrócona z naszych informacje o profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f6596-138">The final step in the process is to update the returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="f6596-139">Wybrano do znaki cudzysłowu należy uwzględnić jako część tokenu, dzięki czemu nawet wtedy, gdy Zastąp nie zachodzi, odpowiedź była nadal poprawne dane JSON.</span><span class="sxs-lookup"><span data-stu-id="f6596-139">I chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response was still valid JSON.</span></span> <span data-ttu-id="f6596-140">To przede wszystkim ułatwia debugowanie.</span><span class="sxs-lookup"><span data-stu-id="f6596-140">This was primarily to make debugging easier.</span></span>

<span data-ttu-id="f6596-141">Te kroki są łączone ze sobą, wynik końcowy po zasad, która wygląda podobnie do następującego.</span><span class="sxs-lookup"><span data-stu-id="f6596-141">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="f6596-142">Takie podejście buforowania jest używany głównie w witrynach sieci web w przypadku gdy składa HTML po stronie serwera, dzięki czemu mogą być renderowane jako pojedynczej strony.</span><span class="sxs-lookup"><span data-stu-id="f6596-142">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="f6596-143">Jednak również jest przydatny w interfejsów API, gdzie klienci nie klienta po stronie buforowanie HTTP lub jest wprowadzania że odpowiedzialność na kliencie.</span><span class="sxs-lookup"><span data-stu-id="f6596-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="f6596-144">Można również wykonać tego samego rodzaju fragmentu buforowanie na serwerach sieci web zaplecza przy użyciu Redis, buforowanie serwera, jednak przy użyciu usługi API Management do wykonywania tej pracy jest przydatne, gdy buforowane fragmenty pochodzą z różnych zapleczy niż podstawowy odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f6596-144">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="f6596-145">Przechowywanie wersji przezroczyste</span><span class="sxs-lookup"><span data-stu-id="f6596-145">Transparent versioning</span></span>
<span data-ttu-id="f6596-146">Jest typowym rozwiązaniem w przypadku wielu wersji inną implementację interfejsu API do obsługi w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="f6596-146">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="f6596-147">Jest to prawdopodobnie do obsługi różnych środowiskach, takich jak deweloperów, testu, produkcji itp., lub może być do obsługi starszych wersji interfejsu API, aby zapewnić czas dla konsumentów interfejsu API przeprowadzić migrację do nowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="f6596-147">This is perhaps to support different environments, like dev, test, production, etc, or it may be to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="f6596-148">Jeden ze sposobów to obsługi zamiast deweloperom klienta zmiany adresów URL z `/v1/customers` do `/v2/customers` jest do przechowywania danych profilu konsumenta wersji interfejsu API obecnie chcą korzystać, a następnie wywołać URL odpowiedniej wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f6596-148">One approach to handling this instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="f6596-149">W celu ustalenia zaplecza poprawny adres URL do wywołania dla określonego klienta, należy zbadać niektóre dane konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f6596-149">In order to determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="f6596-150">Buforowanie danych konfiguracji, możemy zminimalizować spadek wydajności prowadzenia tego wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f6596-150">By caching this configuration data, we can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="f6596-151">Pierwszym krokiem jest identyfikator używany do konfigurowania żądanej wersji.</span><span class="sxs-lookup"><span data-stu-id="f6596-151">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="f6596-152">W tym przykładzie wybrano skojarzyć tę wersję produktu klucza subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f6596-152">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="f6596-153">Następnie przejdziemy wyszukiwania pamięci podręcznej, aby zobaczyć, jeśli już pobrano wersja żądanego klienta.</span><span class="sxs-lookup"><span data-stu-id="f6596-153">We then do a cache lookup to see if we already have retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="f6596-154">Następnie możemy Sprawdź, czy nie znaleziono go w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f6596-154">Then we check to see if we did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="f6596-155">Jeśli firma Microsoft nie możemy przejść i pobrać go.</span><span class="sxs-lookup"><span data-stu-id="f6596-155">If we didn’t then we go and retrieve it.</span></span>

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="f6596-156">Wyodrębnienie z odpowiedzi tekstu treści odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f6596-156">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="f6596-157">Zapisz go w pamięci podręcznej do użycia w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="f6596-157">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="f6596-158">I na koniec zaktualizuj adres URL zaplecza, aby wybrać wersję żądanej przez klienta usługi.</span><span class="sxs-lookup"><span data-stu-id="f6596-158">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="f6596-159">Zasady całkowicie ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="f6596-159">The completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in the cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

<span data-ttu-id="f6596-160">Umożliwiając użytkownikom interfejsu API niewidocznie kontroli wersji wewnętrznej bazy danych jest uzyskiwany przez klientów bez konieczności aktualizacji i wdrożenie klientów jest atrakcyjny rozwiązaniem, które rozwiązuje wiele problemów przechowywanie wersji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f6596-160">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="f6596-161">Izolacji dzierżawców</span><span class="sxs-lookup"><span data-stu-id="f6596-161">Tenant Isolation</span></span>
<span data-ttu-id="f6596-162">W przypadku większych i wielodostępne wdrożeń niektóre firmy utworzenie oddzielnych grup dzierżawcy na różnych wdrożeń sprzętu wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f6596-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="f6596-163">Pozwala to zmniejszyć liczbę klientów, którzy mają wpływ problemem sprzętowym do wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f6596-163">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="f6596-164">Umożliwia również nowe wersje oprogramowania na wprowadzanie etapami.</span><span class="sxs-lookup"><span data-stu-id="f6596-164">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="f6596-165">W idealnym przypadku tej architektury wewnętrznej bazy danych powinny być przezroczyste konsumentom interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f6596-165">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="f6596-166">Można to osiągnąć w sposób podobny do przechowywania wersji przezroczysty, ponieważ jest on oparty na tę samą metodę manipulowania URL wewnętrznej bazy danych przy użyciu stan konfiguracji na klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="f6596-166">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="f6596-167">Zamiast zwracać preferowaną wersję interfejsu API dla każdego klucza subskrypcji, zwróci identyfikator, który dotyczy dzierżawcy grupy przypisanej sprzętu.</span><span class="sxs-lookup"><span data-stu-id="f6596-167">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="f6596-168">Ten identyfikator może służyć do skonstruowania URL odpowiedniej wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f6596-168">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="f6596-169">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="f6596-169">Summary</span></span>
<span data-ttu-id="f6596-170">Swobody obsługi pamięci podręcznej zarządzania interfejsu API Azure do przechowywania każdego typu danych umożliwia wydajne dostępu do danych konfiguracji, które mogą mieć wpływ na sposób przetwarzania przychodzącego żądania.</span><span class="sxs-lookup"><span data-stu-id="f6596-170">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="f6596-171">Można go również używane do przechowywania fragmenty danych, które można rozszerzyć odpowiedzi zwrócone przez interfejs API zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f6596-171">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6596-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6596-172">Next steps</span></span>
<span data-ttu-id="f6596-173">Daj nam swoją opinię w wątku usługi Disqus dla tego tematu, jeśli istnieją inne scenariusze, w których te zasady mają włączona lub jeśli istnieją scenariusze chcesz osiągnąć, ale czy konieczne jest obecnie możliwe.</span><span class="sxs-lookup"><span data-stu-id="f6596-173">Please give us your feedback in the Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like to achieve but do not feel are currently possible.</span></span>

