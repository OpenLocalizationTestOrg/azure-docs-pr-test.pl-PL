---
title: "buforowanie aaaCustom w usłudze Azure API Management"
description: "Dowiedz się, jak toocache elementów przez klucz w usłudze Azure API Management"
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
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="9d7a9-103">Buforowanie niestandardowych w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="9d7a9-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="9d7a9-104">Usługa Azure API Management ma wbudowaną obsługę [buforowanie odpowiedzi HTTP](api-management-howto-cache.md) przy użyciu adresu URL zasobu hello jako hello klucza.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using hello resource URL as hello key.</span></span> <span data-ttu-id="9d7a9-105">Witaj klucza może być modyfikowany przez nagłówki żądania przy użyciu hello `vary-by` właściwości.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-105">hello key can be modified by request headers using hello `vary-by` properties.</span></span> <span data-ttu-id="9d7a9-106">Jest to przydatne w przypadku buforowanie całej odpowiedzi HTTP (alias oświadczenia), ale czasami jest przydatne toojust pamięci podręcznej część reprezentacji.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful toojust cache a portion of a representation.</span></span> <span data-ttu-id="9d7a9-107">nowe Hello [pamięci podręcznej wyszukiwania wartości](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) i [-magazynu wartość w pamięci podręcznej](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) zasady zapewniają możliwość hello toostore i pobrać dowolnego fragmentów danych z poziomu definicji zasad.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-107">hello new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide hello ability toostore and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="9d7a9-108">Tę możliwość dodaje również toohello wartość poprzednio wprowadzone [żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) zasad ponieważ teraz może buforować odpowiedzi z usług zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-108">This ability also adds value toohello previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="9d7a9-109">Architektura</span><span class="sxs-lookup"><span data-stu-id="9d7a9-109">Architecture</span></span>
<span data-ttu-id="9d7a9-110">Zarządzanie interfejsami API usługi używa pamięci podręcznej danych dzierżawy udostępnionego tak, aby podczas skalowania jednostek toomultiple toohello dostępu będą nadal otrzymywać takie same dane z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-110">API Management service uses a shared per-tenant data cache so that, as you scale up toomultiple units you will still get access toohello same cached data.</span></span> <span data-ttu-id="9d7a9-111">Podczas pracy z wdrożenia w przypadku istnieją niezależne pamięci podręcznych w regionach hello.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-111">However, when working with a multi-region deployment there are independent caches within each of hello regions.</span></span> <span data-ttu-id="9d7a9-112">Z powodu toothis, ważne jest toonot zaliczenie magazynu danych, jeśli jest to jedyne źródło informacji o elemencie hello hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-112">Due toothis, it is important toonot treat hello cache as a data store, where it is hello only source of some piece of information.</span></span> <span data-ttu-id="9d7a9-113">Jeśli została i później decyzję tootake zaletą hello w przypadku wdrażania klientów z użytkowników, którzy podróżują może utracić dostęp do danych w pamięci podręcznej toothat.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-113">If you did, and later decided tootake advantage of hello multi-region deployment, then customers with users that travel may lose access toothat cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="9d7a9-114">Buforowanie fragmentu</span><span class="sxs-lookup"><span data-stu-id="9d7a9-114">Fragment caching</span></span>
<span data-ttu-id="9d7a9-115">Brak niektórych przypadkach, gdy odpowiedzi zwracanych zawiera pewną część danych toodetermine kosztowne i jeszcze pozostaje świeże sensownym czasie.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-115">There are certain cases where responses being returned contain some portion of data that is expensive toodetermine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="9d7a9-116">Na przykład należy wziąć pod uwagę usługę utworzony przez linii lotniczych, który zawiera informacje dotyczące zastrzeżenia transmitowane, stan transmitowane itp. Jeśli hello użytkownik jest członkiem hello airlines punktów program, również zostałyby informacje dotyczące tootheir bieżący stan i zebraniu przebiegu.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If hello user is a member of hello airlines points program, they would also have information relating tootheir current status and mileage accumulated.</span></span> <span data-ttu-id="9d7a9-117">Te informacje dotyczące użytkowników mogą być przechowywane w innym systemie, ale może być pożądane tooinclude w odpowiedzi dotyczące stanu transmitowane i zastrzeżenia zwrócone.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-117">This user-related information might be stored in a different system, but it may be desirable tooinclude it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="9d7a9-118">Można to zrobić w procesie zwanym buforowanie fragmentu.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="9d7a9-119">Hello reprezentacja głównej mogą zostać zwrócone z serwera pochodzenia hello przy użyciu określonego rodzaju token tooindicate hello informacji dotyczących użytkownika w przypadku toobe wstawiony.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-119">hello primary representation can be returned from hello origin server using some kind of token tooindicate where hello user-related information is toobe inserted.</span></span> 

<span data-ttu-id="9d7a9-120">Należy wziąć pod uwagę powitania po odpowiedź w formacie JSON z zaplecza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-120">Consider hello following JSON response from a backend API.</span></span>

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

<span data-ttu-id="9d7a9-121">I dodatkowej zasobu pod adresem `/userprofile/{userid}` takie, jak,</span><span class="sxs-lookup"><span data-stu-id="9d7a9-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="9d7a9-122">W kolejności toodetermine hello odpowiedniego użytkownika informacje tooinclude potrzebujemy tooidentify, który użytkownik końcowy hello jest.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-122">In order toodetermine hello appropriate user information tooinclude, we need tooidentify who hello end user is.</span></span> <span data-ttu-id="9d7a9-123">Ten mechanizm jest zależy od implementacji.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="9d7a9-124">Na przykład używam hello `Subject` oświadczeń z `JWT` tokenu.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-124">As an example, I am using hello `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="9d7a9-125">To są przechowywane `enduserid` wartość w zmiennej kontekstu do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="9d7a9-126">następnym krokiem Hello jest toodetermine, jeśli poprzednie żądanie ma już pobrane informacje o użytkowniku hello i zapisana w pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-126">hello next step is toodetermine if a previous request has already retrieved hello user information and stored it in hello cache.</span></span> <span data-ttu-id="9d7a9-127">W tym używamy hello `cache-lookup-value` zasad.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-127">For this we use hello `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="9d7a9-128">Jeśli w pamięci podręcznej hello, które odpowiada toohello wartości klucza, a następnie nr nie ma wpisu `userprofile` zmiennej kontekstu, która zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-128">If there is no entry in hello cache that corresponds toohello key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="9d7a9-129">Musimy sprawdzić, powodzenia hello hello wyszukiwania przy użyciu hello `choose` sterowanie przepływem zasad.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-129">We check hello success of hello lookup using hello `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="9d7a9-130">Jeśli hello `userprofile` zmiennej kontekstu, która nie istnieje, a następnie możemy będzie toohave toomake HTTP żądania tooretrieve go.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-130">If hello `userprofile` context variable doesn’t exist, then we are going toohave toomake an HTTP request tooretrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="9d7a9-131">Używamy hello `enduserid` zasób profilu użytkownika toohello tooconstruct hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-131">We use hello `enduserid` tooconstruct hello URL toohello user profile resource.</span></span> <span data-ttu-id="9d7a9-132">Po mamy odpowiedź hello możemy ściągnięcia hello treść poza hello odpowiedzi i zapisze go do zmiennej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-132">Once we have hello response, we can pull hello body text out of hello response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="9d7a9-133">tooavoid nas o toomake tego żądania HTTP ponownie, gdy hello tego samego użytkownika powoduje, że inne żądanie może przechowujemy hello profilu użytkownika w pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-133">tooavoid us having toomake this HTTP request again, when hello same user makes another request, we can store hello user profile in hello cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="9d7a9-134">Wartość hello są przechowywane w pamięci podręcznej hello przy użyciu hello dokładnie tego samego klucza możemy pierwotnie podjęto tooretrieve go.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-134">We store hello value in hello cache using hello exact same key that we originally attempted tooretrieve it with.</span></span> <span data-ttu-id="9d7a9-135">Witaj czas, przez jaki wybrany toostore hello wartość powinna być oparta na częstotliwość hello zmiany informacji i sposobu odporny na błędy użytkowników są tooout informacje o dacie.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-135">hello duration that we choose toostore hello value should be based on how often hello information changes and how tolerant users are tooout of date information.</span></span> 

<span data-ttu-id="9d7a9-136">Jest ważne toorealize, że pobieranie z pamięci podręcznej hello jest nadal poza procesem, żądanie sieciowe i potencjalnie można dodawać dziesiątki żądania toohello milisekund.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-136">It is important toorealize that retrieving from hello cache is still an out-of-process, network request and potentially can still add tens of milliseconds toohello request.</span></span> <span data-ttu-id="9d7a9-137">korzyści Hello pochodzić podczas określania informacji o profilu użytkownika hello trwa znacznie dłużej niż zapytań bazy danych toodo tooneeding lub zagregowanych informacji z wielu zapleczy.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-137">hello benefits come when determining hello user profile information takes significantly longer than that due tooneeding toodo database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="9d7a9-138">Hello ostatnim krokiem w procesie hello jest hello tooupdate zwrócił odpowiedź o naszych informacje o profilu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-138">hello final step in hello process is tooupdate hello returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="9d7a9-139">Wybrano tooinclude hello cudzysłów jako część tokenu hello, dzięki czemu nawet wtedy, gdy nie występuje Zamień hello, hello odpowiedź była nadal poprawne dane JSON.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-139">I chose tooinclude hello quotation marks as part of hello token so that even when hello replace doesn’t occur, hello response was still valid JSON.</span></span> <span data-ttu-id="9d7a9-140">To przede wszystkim toomake ułatwia debugowanie.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-140">This was primarily toomake debugging easier.</span></span>

<span data-ttu-id="9d7a9-141">Te kroki są łączone ze sobą, wynik końcowy powitania po zasad, która wygląda jak powitania po jednym.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-141">Once you combine all these steps together, hello end result is a policy that looks like hello following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
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

<span data-ttu-id="9d7a9-142">Takie podejście buforowania jest używany głównie w witrynach sieci web gdzie HTML składa się na powitania po stronie serwera, dzięki czemu mogą być renderowane jako pojedynczej strony.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-142">This caching approach is primarily used in web sites where HTML is composed on hello server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="9d7a9-143">Jednak również jest przydatny w interfejsów API, gdzie klienci nie klienta po stronie buforowanie HTTP lub pożądane jest nie tooput że odpowiedzialność na powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not tooput that responsibility on hello client.</span></span>

<span data-ttu-id="9d7a9-144">Można również wykonać tego samego rodzaju fragmentu buforowanie na serwerze sieci web zaplecza hello za pomocą Redis, buforowanie serwera, jednak przy użyciu tooperform usługi Zarządzanie interfejsami API hello tej pracy jest przydatne, gdy fragmenty hello buforowane pochodzą z różnych zapleczy niż hello podstawowy odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-144">This same kind of fragment caching can also be done on hello backend web servers using a Redis caching server, however, using hello API Management service tooperform this work is useful when hello cached fragments are coming from different back-ends than hello primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="9d7a9-145">Przechowywanie wersji przezroczyste</span><span class="sxs-lookup"><span data-stu-id="9d7a9-145">Transparent versioning</span></span>
<span data-ttu-id="9d7a9-146">Jest typowym rozwiązaniem w przypadku wielu wersji inną implementację toobe interfejsu API, obsługiwane w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-146">It is common practice for multiple different implementation versions of an API toobe supported at any one time.</span></span> <span data-ttu-id="9d7a9-147">Jest to prawdopodobnie różnych środowiskach toosupport deweloperów, testu, produkcji itd., lub może być toosupport starsze wersje czasu toogive hello interfejsu API dla wersji toonewer toomigrate konsumentów interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-147">This is perhaps toosupport different environments, like dev, test, production, etc, or it may be toosupport older versions of hello API toogive time for API consumers toomigrate toonewer versions.</span></span> 

<span data-ttu-id="9d7a9-148">Jednym z podejść toohandling tym zamiast elementu wymagające adresy URL hello toochange deweloperzy klienta z `/v1/customers` zbyt`/v2/customers` jest toostore w dane profilu użytkownika hello wersję interfejsu API hello one obecnie ma toouse i Wywołaj hello odpowiednie adres URL wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-148">One approach toohandling this instead of requiring client developers toochange hello URLs from `/v1/customers` too`/v2/customers` is toostore in hello consumer’s profile data which version of hello API they currently wish toouse and call hello appropriate backend URL.</span></span> <span data-ttu-id="9d7a9-149">W kolejności toodetermine hello zaplecza poprawny adres URL toocall dla określonego klienta, jest konieczne tooquery niektóre dane konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-149">In order toodetermine hello correct backend URL toocall for a particular client, it is necessary tooquery some configuration data.</span></span> <span data-ttu-id="9d7a9-150">Buforowanie danych konfiguracji, możemy zminimalizować spadek wydajności hello prowadzenia tego wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-150">By caching this configuration data, we can minimize hello performance penalty of doing this lookup.</span></span>

<span data-ttu-id="9d7a9-151">pierwszym krokiem Hello jest używany identyfikator hello toodetermine tooconfigure hello żądanej wersji.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-151">hello first step is toodetermine hello identifier used tooconfigure hello desired version.</span></span> <span data-ttu-id="9d7a9-152">W tym przykładzie wybrano tooassociate hello wersji toohello subskrypcji klucza.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-152">In this example, I chose tooassociate hello version toohello product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="9d7a9-153">Jeśli już pobrano wersji klienta żądaną hello następnie jak toosee wyszukiwania pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-153">We then do a cache lookup toosee if we already have retrieved hello desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="9d7a9-154">Następnie sprawdzamy toosee, jeśli nie znaleziono go w pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-154">Then we check toosee if we did not find it in hello cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="9d7a9-155">Jeśli firma Microsoft nie możemy przejść i pobrać go.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="9d7a9-156">Wyodrębnij tekst treści odpowiedzi hello z hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-156">Extract hello response body text from hello response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="9d7a9-157">Zapisz go w pamięci podręcznej hello do użytku w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-157">Store it back in hello cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="9d7a9-158">I na koniec zaktualizuj hello wewnętrznego adresu URL tooselect hello wersji żądanej przez klienta na powitania usługi hello.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-158">And finally update hello back-end URL tooselect hello version of hello service desired by hello client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="9d7a9-159">Witaj całkowicie zasad ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-159">hello completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
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

<span data-ttu-id="9d7a9-160">Włączanie tootransparently sterowanie konsumentów interfejsu API, która wersja wewnętrznej bazy danych jest uzyskiwany przez klientów bez konieczności tooupdate i ponownego wdrażania klientów jest atrakcyjny rozwiązaniem, które rozwiązuje wiele problemów przechowywanie wersji interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-160">Enabling API consumers tootransparently control which backend version is being accessed by clients without having tooupdate and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="9d7a9-161">Izolacji dzierżawców</span><span class="sxs-lookup"><span data-stu-id="9d7a9-161">Tenant Isolation</span></span>
<span data-ttu-id="9d7a9-162">W przypadku większych i wielodostępne wdrożeń niektóre firmy utworzenie oddzielnych grup dzierżawcy na różnych wdrożeń sprzętu wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="9d7a9-163">Pozwala to zmniejszyć hello liczbę klientów, którzy mają wpływ problemem sprzętowym hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-163">This minimizes hello number of customers who are impacted by a hardware issue on hello backend.</span></span> <span data-ttu-id="9d7a9-164">Umożliwia również nowe toobe wersji oprogramowania wprowadzanie etapami.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-164">It also enables new software versions toobe rolled out in stages.</span></span> <span data-ttu-id="9d7a9-165">W idealnym przypadku tej architektury wewnętrznej bazy danych powinny być przezroczyste tooAPI konsumentów.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-165">Ideally this backend architecture should be transparent tooAPI consumers.</span></span> <span data-ttu-id="9d7a9-166">Można to osiągnąć w podobne versioning tootransparent sposób ponieważ jest ona oparta na powitania tę samą metodę manipulowania hello URL wewnętrznej bazy danych przy użyciu stan konfiguracji na klucz interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-166">This can be achieved in a similar way tootransparent versioning because it is based on hello same technique of manipulating hello backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="9d7a9-167">Zamiast zwracać preferowanych wersji hello interfejsu API dla każdego klucza subskrypcji, zwróci identyfikator, który dotyczy grupy sprzętu toohello przypisane dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-167">Instead of returning a preferred version of hello API for each subscription key, you would return an identifier that relates a tenant toohello assigned hardware group.</span></span> <span data-ttu-id="9d7a9-168">Ten identyfikator może być URL odpowiedniej wewnętrznej bazy danych hello tooconstruct używane.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-168">That identifier can be used tooconstruct hello appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="9d7a9-169">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="9d7a9-169">Summary</span></span>
<span data-ttu-id="9d7a9-170">Witaj swobodę toouse Witaj pamięci podręcznej zarządzania interfejsu API Azure do przechowywania każdego typu danych umożliwia wydajne dostępu tooconfiguration dane, które mogą mieć wpływ na sposób hello przetwarzanie żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-170">hello freedom toouse hello Azure API management cache for storing any kind of data enables efficient access tooconfiguration data that can affect hello way an inbound request is processed.</span></span> <span data-ttu-id="9d7a9-171">Można także toostore używane fragmenty danych, które można rozszerzyć odpowiedzi zwrócone przez interfejs API zaplecza.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-171">It can also be used toostore data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d7a9-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d7a9-172">Next steps</span></span>
<span data-ttu-id="9d7a9-173">Daj nam swoją opinię w hello wątku usługi Disqus dla tego tematu, jeśli istnieją inne scenariusze, czy te zasady mają włączona lub jeśli istnieją scenariusze chcieliby tooachieve, ale nie jest konieczne są obecnie możliwe.</span><span class="sxs-lookup"><span data-stu-id="9d7a9-173">Please give us your feedback in hello Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like tooachieve but do not feel are currently possible.</span></span>

