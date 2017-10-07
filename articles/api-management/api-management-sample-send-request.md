---
title: "żądania toogenerate HTTP usługi Zarządzanie interfejsami API aaaUsing"
description: "Dowiedz się, zasad żądań i odpowiedzi toouse zarządzanie interfejsami API toocall zewnętrznych usług interfejsu API"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8002ee453057513340328d99f298703c3b3a9531
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-external-services-from-hello-azure-api-management-service"></a><span data-ttu-id="428fa-103">Za pomocą usług zewnętrznych z hello usługi Zarządzanie interfejsami API Azure</span><span class="sxs-lookup"><span data-stu-id="428fa-103">Using external services from hello Azure API Management service</span></span>
<span data-ttu-id="428fa-104">zasady Hello dostępne w usłudze Azure API Management należy szeroką gamę przydatne pracy wyłącznie na podstawie żądania przychodzącego hello, odpowiedzi wychodzącej hello i podstawowe informacje o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="428fa-104">hello policies available in Azure API Management service can do a wide range of useful work based purely on hello incoming request, hello outgoing response and basic configuration information.</span></span> <span data-ttu-id="428fa-105">Jednak jest możliwe toointeract z usług zewnętrznych z interfejsu API zarządzania otwiera wiele możliwości więcej zasad.</span><span class="sxs-lookup"><span data-stu-id="428fa-105">However, being able toointeract with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="428fa-106">Zaobserwowano wcześniej, jak firma Microsoft może interakcyjnie hello [usługi Azure Event Hub rejestrowania, monitorowania i analizy](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="428fa-106">We have previously seen how we can interact with hello [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="428fa-107">W tym artykule przedstawiono usługi opartej na zasadach, które pozwalają toointeract wszelkich zewnętrznych protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="428fa-107">In this article we will demonstrate policies that allow you toointeract with any external HTTP based service.</span></span> <span data-ttu-id="428fa-108">Te zasady mogą służyć do wyzwalania zdarzenia zdalnego lub do pobierania informacji, które będzie używane toomanipulate hello oryginalnego żądania i odpowiedzi w jakiś sposób.</span><span class="sxs-lookup"><span data-stu-id="428fa-108">These policies can be used for triggering remote events or for retrieving information that will be used toomanipulate hello original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="428fa-109">Sposób żądania, Wyślij co w-</span><span class="sxs-lookup"><span data-stu-id="428fa-109">Send-One-Way-Request</span></span>
<span data-ttu-id="428fa-110">Prawdopodobnie hello najprostszym zewnętrzne jest interakcja hello fire i zapomnij styl żądania, które umożliwia toobe zewnętrznej usługi zgłoszone pewnego rodzaju ważnych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="428fa-110">Possibly hello simplest external interaction is hello fire-and-forget style of request that allows an external service toobe notified of some kind of important event.</span></span> <span data-ttu-id="428fa-111">Możemy użyć zasad przepływu sterowania hello `choose` toodetect spełniony jest dowolny rodzaj warunek, który firma Microsoft są zainteresowani, a następnie, jeśli hello warunku, firma Microsoft może wprowadzać zewnętrznych żądań HTTP przy użyciu hello [— jeden — sposób — żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) zasad.</span><span class="sxs-lookup"><span data-stu-id="428fa-111">We can use hello control flow policy `choose` toodetect any kind of condition that we are interested in and then, if hello condition is satisfied, we can make an external HTTP request using hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="428fa-112">Może to być tooa żądania, systemu, takie jak Hipchat lub Slack lub poczty interfejsu API SendGrid lub MailChimp obsługi wiadomości, lub do obsługi krytycznych zdarzeń coś tak jak PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="428fa-112">This could be a request tooa messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="428fa-113">Wszystkie te systemy obsługi komunikatów mają prostych interfejsów API protokołu HTTP, które firma Microsoft może łatwo wywołać.</span><span class="sxs-lookup"><span data-stu-id="428fa-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="428fa-114">Alerty z zapas czasu</span><span class="sxs-lookup"><span data-stu-id="428fa-114">Alerting with Slack</span></span>
<span data-ttu-id="428fa-115">Witaj poniższy przykład pokazuje, jak toosend tooa komunikat Slack pokoju rozmów, jeśli kod stanu odpowiedzi HTTP hello jest większa niż lub równa too500.</span><span class="sxs-lookup"><span data-stu-id="428fa-115">hello following example demonstrates how toosend a message tooa Slack chat room if hello HTTP response status code is greater than or equal too500.</span></span> <span data-ttu-id="428fa-116">Błąd zakresu 500 oznacza, że nie można się samoistnie rozwiązać problem z naszych zaplecza interfejsu API, który hello klienta interfejsach API.</span><span class="sxs-lookup"><span data-stu-id="428fa-116">A 500 range error indicates a problem with our backend API that hello client of our API cannot resolve themselves.</span></span> <span data-ttu-id="428fa-117">Zwykle wymagają określonego rodzaju interwencji z naszej strony.</span><span class="sxs-lookup"><span data-stu-id="428fa-117">It usually requires some kind of intervention on our part.</span></span>  

```xml
<choose>
    <when condition="@(context.Response.StatusCode >= 500)">
      <send-one-way-request mode="new">
        <set-url>https://hooks.slack.com/services/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</set-url>
        <set-method>POST</set-method>
        <set-body>@{
                return new JObject(
                        new JProperty("username","APIM Alert"),
                        new JProperty("icon_emoji", ":ghost:"),
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",
                                                context.Request.Method,
                                                context.Request.Url.Path + context.Request.Url.QueryString,
                                                context.Request.Url.Host,
                                                context.Response.StatusCode,
                                                context.Response.StatusReason,
                                                context.User.Email
                                                ))
                        ).ToString();
            }</set-body>
      </send-one-way-request>
    </when>
</choose>
```

<span data-ttu-id="428fa-118">Zapas czasu ma hello pojęcie punkty zaczepienia dla ruchu przychodzącego sieci web.</span><span class="sxs-lookup"><span data-stu-id="428fa-118">Slack has hello notion of inbound web hooks.</span></span> <span data-ttu-id="428fa-119">Podczas konfigurowania punktu zaczepienia przychodzący sieci web, zapas czasu generuje specjalne adresu URL, który pozwala toodo prostego żądania POST, toopass komunikat do kanału Slack hello.</span><span class="sxs-lookup"><span data-stu-id="428fa-119">When configuring an inbound web hook, Slack generates a special URL which allows you toodo a simple POST request and toopass a message into hello Slack channel.</span></span> <span data-ttu-id="428fa-120">Hello treści JSON, który utworzymy jest oparty na formacie zdefiniowane przez zapas czasu.</span><span class="sxs-lookup"><span data-stu-id="428fa-120">hello JSON body that we create is based on a format defined by Slack.</span></span>

![Haku Slack sieci Web](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="428fa-122">To jest fire i zapomnij wystarczająco dobre?</span><span class="sxs-lookup"><span data-stu-id="428fa-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="428fa-123">Brak niektórych wady i zalety używając stylu fire i zapomnij żądania.</span><span class="sxs-lookup"><span data-stu-id="428fa-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="428fa-124">Jeśli dla jakiegoś powodu hello żądanie kończy się niepowodzeniem, a następnie hello błąd nie będzie raportowana.</span><span class="sxs-lookup"><span data-stu-id="428fa-124">If for some reason, hello request fails, then hello failure will not be reported.</span></span> <span data-ttu-id="428fa-125">W takiej sytuacji określonego złożoność hello system raportowania błędu serwera pomocniczego i Oczekiwanie na odpowiedź hello koszt wydajności dodatkowe hello nie jest uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="428fa-125">In this particular situation, hello complexity of having a secondary failure reporting system and hello additional performance cost of waiting for hello response is not warranted.</span></span> <span data-ttu-id="428fa-126">W scenariuszach, w których jest istotne toocheck hello odpowiedzi, następnie hello [żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) zasad jest lepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="428fa-126">For scenarios where it is essential toocheck hello response, then hello [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="428fa-127">Żądanie wysłania</span><span class="sxs-lookup"><span data-stu-id="428fa-127">Send-Request</span></span>
<span data-ttu-id="428fa-128">Witaj `send-request` umożliwia zasad za pomocą zewnętrznej usługi tooperform złożonych przetwarzania funkcji a danych zwrotnych toohello interfejsu API zarządzania usługą, która może służyć do dalszego przetwarzania zasad.</span><span class="sxs-lookup"><span data-stu-id="428fa-128">hello `send-request` policy enables using an external service tooperform complex processing functions and return data toohello API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="428fa-129">Autoryzowanie tokenów odwołań</span><span class="sxs-lookup"><span data-stu-id="428fa-129">Authorizing reference tokens</span></span>
<span data-ttu-id="428fa-130">Główna funkcja interfejsu API zarządzania jest ochrona zasobów wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="428fa-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="428fa-131">Jeśli używane przez interfejs API serwera autoryzacji hello tworzy [tokenów JWT](http://jwt.io/) w ramach swojego przepływu OAuth2 jako [usługi Azure Active Directory](../active-directory/active-directory-aadconnect.md) tak, możesz użyć hello `validate-jwt` ważność hello tooverify zasad Hello token.</span><span class="sxs-lookup"><span data-stu-id="428fa-131">If hello authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use hello `validate-jwt` policy tooverify hello validity of hello token.</span></span> <span data-ttu-id="428fa-132">Jednak niektóre serwery autoryzacji utworzyć są nazywane [odwołania tokenów](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) nie można zweryfikować bez wprowadzania serwera autoryzacji wstecz toohello wywołania.</span><span class="sxs-lookup"><span data-stu-id="428fa-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back toohello authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="428fa-133">Introspection standardowych</span><span class="sxs-lookup"><span data-stu-id="428fa-133">Standardized introspection</span></span>
<span data-ttu-id="428fa-134">W przeszłości hello nie było żadnych standardowych możliwości sprawdzenia tokenu odwołania z serwera autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="428fa-134">In hello past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="428fa-135">Jednak ostatnio proponowany standard [RFC 7662](https://tools.ietf.org/html/rfc7662) opublikował hello IETF, który określa, jak serwer zasobów można zweryfikować hello ważności tokenu.</span><span class="sxs-lookup"><span data-stu-id="428fa-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by hello IETF that defines how a resource server can verify hello validity of a token.</span></span>

### <a name="extracting-hello-token"></a><span data-ttu-id="428fa-136">Wyodrębnianie hello tokenu</span><span class="sxs-lookup"><span data-stu-id="428fa-136">Extracting hello token</span></span>
<span data-ttu-id="428fa-137">pierwszym krokiem Hello jest tokenem hello tooextract z nagłówka autoryzacji hello.</span><span class="sxs-lookup"><span data-stu-id="428fa-137">hello first step is tooextract hello token from hello Authorization header.</span></span> <span data-ttu-id="428fa-138">wartość nagłówka Hello powinien być sformatowany z hello `Bearer` schematu autoryzacji, pojedyncze spacje i następnie autoryzacji hello token zgodnie [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="428fa-138">hello header value should be formatted with hello `Bearer` authorization scheme, a single space and then hello authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="428fa-139">Niestety istnieją przypadki, w którym hello autoryzacji schemat zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="428fa-139">Unfortunately there are cases where hello authorization scheme is omitted.</span></span> <span data-ttu-id="428fa-140">tooaccount tego podczas analizowania, możemy podzielić wartość nagłówka hello miejsca i wybierz hello ostatni ciąg z hello zwrócił tablicę ciągów.</span><span class="sxs-lookup"><span data-stu-id="428fa-140">tooaccount for this when parsing, we split hello header value on a space and select hello last string from hello returned array of strings.</span></span> <span data-ttu-id="428fa-141">Zapewnia to obejście nagłówki autoryzacji nieprawidłowo sformatowany.</span><span class="sxs-lookup"><span data-stu-id="428fa-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a><span data-ttu-id="428fa-142">Tworzenie żądania sprawdzenia poprawności hello</span><span class="sxs-lookup"><span data-stu-id="428fa-142">Making hello validation request</span></span>
<span data-ttu-id="428fa-143">Gdy mamy hello token autoryzacji, firma Microsoft może wprowadzać hello żądania toovalidate hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="428fa-143">Once we have hello authorization token, we can make hello request toovalidate hello token.</span></span> <span data-ttu-id="428fa-144">RFC 7662 wywołuje introspection ten proces i wymaga, aby użytkownik `POST` zasobu introspection toohello formularza HTML.</span><span class="sxs-lookup"><span data-stu-id="428fa-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form toohello introspection resource.</span></span> <span data-ttu-id="428fa-145">Hello formularza HTML z kluczem hello musi zawierać co najmniej parę klucz/wartość `token`.</span><span class="sxs-lookup"><span data-stu-id="428fa-145">hello HTML form must at least contain a key/value pair with hello key `token`.</span></span> <span data-ttu-id="428fa-146">Ten serwer autoryzacji toohello żądania również musi być uwierzytelniony tooensure, że złośliwe klientów nie można go połowów włokiem dla prawidłowych tokenów.</span><span class="sxs-lookup"><span data-stu-id="428fa-146">This request toohello authorization server must also be authenticated tooensure that malicious clients cannot go trawling for valid tokens.</span></span>

```xml
<send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
  <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
  <set-method>POST</set-method>
  <set-header name="Authorization" exists-action="override">
    <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
  </set-header>
  <set-header name="Content-Type" exists-action="override">
    <value>application/x-www-form-urlencoded</value>
  </set-header>
  <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
</send-request>
```

### <a name="checking-hello-response"></a><span data-ttu-id="428fa-147">Sprawdzanie, czy odpowiedź hello</span><span class="sxs-lookup"><span data-stu-id="428fa-147">Checking hello response</span></span>
<span data-ttu-id="428fa-148">Witaj `response-variable-name` atrybutów jest używane toogive dostępu hello zwrócił odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="428fa-148">hello `response-variable-name` attribute is used toogive access hello returned response.</span></span> <span data-ttu-id="428fa-149">Witaj nazwa zdefiniowana w tej właściwości może być używana jako klucz w hello `context.Variables` hello tooaccess słownika `IResponse` obiektu.</span><span class="sxs-lookup"><span data-stu-id="428fa-149">hello name defined in this property can be used as a key into hello `context.Variables` dictionary tooaccess hello `IResponse` object.</span></span>

<span data-ttu-id="428fa-150">Z obiektu odpowiedzi hello możemy pobrać treści hello i RFC 7622 nam informuje, że hello odpowiedzi musi być obiektem JSON i musi zawierać co najmniej właściwość o nazwie `active` będący wartością logiczną.</span><span class="sxs-lookup"><span data-stu-id="428fa-150">From hello response object we can retrieve hello body and RFC 7622 tells us that hello response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="428fa-151">Gdy `active` ma wartość true, a następnie hello token jest uznawany za ważny.</span><span class="sxs-lookup"><span data-stu-id="428fa-151">When `active` is true then hello token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="428fa-152">Niepowodzenie raportowania</span><span class="sxs-lookup"><span data-stu-id="428fa-152">Reporting failure</span></span>
<span data-ttu-id="428fa-153">Używamy `<choose>` toodetect zasad, jeśli hello token jest nieprawidłowy, a zwracany odpowiedzi 401.</span><span class="sxs-lookup"><span data-stu-id="428fa-153">We use a `<choose>` policy toodetect if hello token is invalid and if so, return a 401 response.</span></span>

```xml
<choose>
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
    <return-response response-variable-name="existing response variable">
      <set-status code="401" reason="Unauthorized" />
      <set-header name="WWW-Authenticate" exists-action="override">
        <value>Bearer error="invalid_token"</value>
      </set-header>
    </return-response>
  </when>
</choose>
```

<span data-ttu-id="428fa-154">Zgodnie [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) którym opisano sposób `bearer` tokenów należy również zwróconych `WWW-Authenticate` nagłówka odpowiedzi hello 401.</span><span class="sxs-lookup"><span data-stu-id="428fa-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with hello 401 response.</span></span> <span data-ttu-id="428fa-155">Witaj WWW-Authenticate jest tooinstruct przeznaczone klienckich na temat tooconstruct prawidłowo nieautoryzowane żądanie.</span><span class="sxs-lookup"><span data-stu-id="428fa-155">hello WWW-Authenticate is intended tooinstruct a client on how tooconstruct a properly authorized request.</span></span> <span data-ttu-id="428fa-156">Powodu toohello szerokiej gamy podejścia przy użyciu usługi framework hello OAuth2, trudno jest toocommunicate hello wszystkich potrzebnych informacji.</span><span class="sxs-lookup"><span data-stu-id="428fa-156">Due toohello wide variety of approaches possible with hello OAuth2 framework, it is difficult toocommunicate all hello needed information.</span></span> <span data-ttu-id="428fa-157">Na szczęście są przetwarzane toohelp [klientów odnajdywania, jak tooproperly autoryzować serwer zasobów tooa żądań](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="428fa-157">Fortunately there are efforts underway toohelp [clients discover how tooproperly authorize requests tooa resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="428fa-158">Końcowa rozwiązania</span><span class="sxs-lookup"><span data-stu-id="428fa-158">Final solution</span></span>
<span data-ttu-id="428fa-159">Zestawienie wszystkie elementy hello, uzyskujemy hello następujące zasady:</span><span class="sxs-lookup"><span data-stu-id="428fa-159">Putting all hello pieces together, we get hello following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
    <set-method>POST</set-method>
    <set-header name="Authorization" exists-action="override">
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
    </set-header>
    <set-header name="Content-Type" exists-action="override">
      <value>application/x-www-form-urlencoded</value>
    </set-header>
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
  </send-request>

  <choose>
          <!-- Check active property in response -->
          <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
              <!-- Return 401 Unauthorized with http-problem payload -->
              <return-response response-variable-name="existing response variable">
                  <set-status code="401" reason="Unauthorized" />
                  <set-header name="WWW-Authenticate" exists-action="override">
                      <value>Bearer error="invalid_token"</value>
                  </set-header>
              </return-response>
          </when>
      </choose>
  <base />
</inbound>
```

<span data-ttu-id="428fa-160">Jest to tylko jeden z wielu przykłady hello `send-request` zasad mogą być przydatne usług zewnętrznych toointegrate używane w procesie hello żądań i odpowiedzi przepływających przez hello usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="428fa-160">This is only one of many examples of how hello `send-request` policy can be used toointegrate useful external services into hello process of requests and responses flowing through hello API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="428fa-161">Kompozycja odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="428fa-161">Response Composition</span></span>
<span data-ttu-id="428fa-162">Witaj `send-request` zasady mogą służyć do zwiększenia system wewnętrznej bazy danych żądania podstawowego tooa widzieliśmy w poprzednim przykładzie hello lub może służyć jako pełną Zamień dla hello wywołania wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="428fa-162">hello `send-request` policy can be used for enhancing a primary request tooa backend system, as we saw in hello previous example, or it can be used as a complete replace for of hello backend call.</span></span> <span data-ttu-id="428fa-163">Ta technika można łatwo utworzyć złożonego zasoby, które są agregowane z wielu różnych systemów.</span><span class="sxs-lookup"><span data-stu-id="428fa-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="428fa-164">Tworzenie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="428fa-164">Building a dashboard</span></span>
<span data-ttu-id="428fa-165">Czasami ma toobe stanie tooexpose informacji w wielu systemach wewnętrznej bazy danych, na przykład toodrive pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="428fa-165">Sometimes you want toobe able tooexpose information that exists in multiple backend systems, for example, toodrive a dashboard.</span></span> <span data-ttu-id="428fa-166">Hello wskaźników KPI pochodzą z wszystkich różnych zapleczy, ale wolisz nie tooprovide bezpośredni dostęp do toothem i byłoby nieuprzywilejowany można pobrać informacji o wszystkich hello pojedyncze żądanie.</span><span class="sxs-lookup"><span data-stu-id="428fa-166">hello KPIs come from all different back-ends, but you would prefer not tooprovide direct access toothem and it would be nice if all hello information could be retrieved in a single request.</span></span> <span data-ttu-id="428fa-167">Możliwe, że niektóre hello wewnętrznej bazy danych informacji muszą niektóre dzielenie i grupowanie i niewielką najpierw oczyszczania!</span><span class="sxs-lookup"><span data-stu-id="428fa-167">Perhaps some of hello backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="428fa-168">Trwa toocache możliwe, że złożone zasobów będą przydatne tooreduce zaplecza hello załadować wiesz, że użytkownicy mają rodzaj atakowaniu hello klawisz F5 w kolejności toosee, jeśli ich underperforming metryki mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="428fa-168">Being able toocache that composite resource would be a useful tooreduce hello backend load as you know users have a habit of hammering hello F5 key in order toosee if their underperforming metrics might change.</span></span>    

### <a name="faking-hello-resource"></a><span data-ttu-id="428fa-169">Faking hello zasobów</span><span class="sxs-lookup"><span data-stu-id="428fa-169">Faking hello resource</span></span>
<span data-ttu-id="428fa-170">pierwszy krok toobuilding Hello naszych zasobów pulpit nawigacyjny jest tooconfigure nowej operacji w portalu wydawcy zarządzanie interfejsami API hello.</span><span class="sxs-lookup"><span data-stu-id="428fa-170">hello first step toobuilding our dashboard resource is tooconfigure a new operation in hello API Management publisher portal.</span></span> <span data-ttu-id="428fa-171">To będzie tooconfigure stosowaną symbolu zastępczego naszych toobuild zasad kompozycji naszych zasobu dynamicznego.</span><span class="sxs-lookup"><span data-stu-id="428fa-171">This will be a placeholder operation used tooconfigure our composition policy toobuild our dynamic resource.</span></span>

![Operacja pulpitu nawigacyjnego](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a><span data-ttu-id="428fa-173">Tworzenie żądania hello</span><span class="sxs-lookup"><span data-stu-id="428fa-173">Making hello requests</span></span>
<span data-ttu-id="428fa-174">Raz hello `dashboard` utworzono operacji można skonfigurować zasady dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="428fa-174">Once hello `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Operacja pulpitu nawigacyjnego](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="428fa-176">pierwszym krokiem Hello jest tooextract żadnych parametrów zapytania z żądania przychodzącego hello, tak, aby firma Microsoft może przekazywać tooour wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="428fa-176">hello first step  is tooextract any query parameters from hello incoming request, so that we can forward them tooour backend.</span></span> <span data-ttu-id="428fa-177">W tym przykładzie naszych pulpit nawigacyjny jest pokazywane są informacje oparte na pewien czas w związku z tym ma `fromDate` i `toDate` parametru.</span><span class="sxs-lookup"><span data-stu-id="428fa-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="428fa-178">Możemy użyć hello `set-variable` informacje o zasadach tooextract hello z hello adresu URL żądania.</span><span class="sxs-lookup"><span data-stu-id="428fa-178">We can use hello `set-variable` policy tooextract hello information from hello request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="428fa-179">Gdy mamy tych informacji firma Microsoft może wprowadzać żądania w systemy zaplecza hello tooall.</span><span class="sxs-lookup"><span data-stu-id="428fa-179">Once we have this information we can make requests tooall hello backend systems.</span></span> <span data-ttu-id="428fa-180">Każde żądanie tworzy nowy adres URL z informacji o parametrach hello wywołuje jego odpowiedniego serwera i zapisuje odpowiedź hello w zmiennej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="428fa-180">Each request constructs a new URL with hello parameter information and calls its respective server and stores hello response in a context variable.</span></span>

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="428fa-181">Te żądania będą wykonywane w kolejności, która nie jest idealnym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="428fa-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="428fa-182">W kolejnych wersji możemy można wprowadzenia nowych zasad o nazwie `wait` umożliwi wszystkie te żądania tooexecute równolegle.</span><span class="sxs-lookup"><span data-stu-id="428fa-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests tooexecute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="428fa-183">Odpowiada</span><span class="sxs-lookup"><span data-stu-id="428fa-183">Responding</span></span>
<span data-ttu-id="428fa-184">odpowiedź złożonego hello tooconstruct używamy hello [odpowiedzi zwracany](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) zasad.</span><span class="sxs-lookup"><span data-stu-id="428fa-184">tooconstruct hello composite response we can use hello [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="428fa-185">Witaj `set-body` elementu można użyć wyrażenia tooconstruct nowy `JObject` z wszystkich reprezentacje składnika hello osadzony jako właściwości.</span><span class="sxs-lookup"><span data-stu-id="428fa-185">hello `set-body` element can use an expression tooconstruct a new `JObject` with all hello component representations embedded as properties.</span></span>

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

<span data-ttu-id="428fa-186">zasady pełną Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="428fa-186">hello complete policy looks as follows:</span></span>

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="428fa-187">W konfiguracji hello hello symbolu zastępczego operacji, które można skonfigurować toobe zasobów pulpitu nawigacyjnego hello w pamięci podręcznej dla co najmniej godzinę ponieważ rozumiemy, że hello rodzaj danych hello oznacza, że nawet jeśli jest nieaktualny, będzie on nadal dostępny wystarczająco skuteczne godzinę tooconvey cenne informacje toohello użytkowników.</span><span class="sxs-lookup"><span data-stu-id="428fa-187">In hello configuration of hello placeholder operation we can configure hello dashboard resource toobe cached for at least an hour because we understand hello nature of hello data means that even if it is an hour out of date, it will still be sufficiently effective tooconvey valuable information toohello users.</span></span>

## <a name="summary"></a><span data-ttu-id="428fa-188">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="428fa-188">Summary</span></span>
<span data-ttu-id="428fa-189">Usługi Zarządzanie interfejsami API Azure oferuje elastyczne zasady, które można wybiórczo zastosować tooHTTP ruchu i umożliwia kompozycji usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="428fa-189">Azure API Management service provides flexible policies that can be selectively applied tooHTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="428fa-190">Czy chcesz tooenhance bramy interfejsu API z alerty funkcje, weryfikacji i sprawdzania poprawności możliwości lub tworzenia nowych zasobów złożonego na podstawie wielu usług zaplecza, hello `send-request` i związane z nią zasady Otwórz world możliwości.</span><span class="sxs-lookup"><span data-stu-id="428fa-190">Whether you want tooenhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, hello `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="428fa-191">Obejrzyj film poglądowy dotyczący tych zasad</span><span class="sxs-lookup"><span data-stu-id="428fa-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="428fa-192">Aby uzyskać więcej informacji na temat hello [sposób żądania, Wyślij co w-](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), i [odpowiedzi zwracany](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) zasady omówione w tym artykule, obserwuj powitania po wideo.</span><span class="sxs-lookup"><span data-stu-id="428fa-192">For more information on hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

