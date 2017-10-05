---
title: "Za pomocą usługi Zarządzanie interfejsami API do generowania żądań HTTP"
description: "Dowiedz się, jak użyć zasad żądań i odpowiedzi w usłudze API Management do wywołania usług zewnętrznych z interfejsu API"
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
ms.openlocfilehash: e778943715d6ca5256ad612d82bdc1f82197df0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="a8259-103">Za pomocą usług zewnętrznych z usługi Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a8259-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="a8259-104">Zasady dostępne w usłudze Azure API Management należy szeroką gamę przydatne pracy wyłącznie na podstawie żądania przychodzącego, odpowiedzi wychodzącej i podstawowe informacje o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a8259-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="a8259-105">Jednak możliwość interakcji z usługami zewnętrznych z interfejsu API zarządzania otwiera wiele możliwości więcej zasad.</span><span class="sxs-lookup"><span data-stu-id="a8259-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="a8259-106">Zaobserwowano wcześniej, jak firma Microsoft może interakcyjnie [usługi Azure Event Hub rejestrowania, monitorowania i analizy](api-management-log-to-eventhub-sample.md).</span><span class="sxs-lookup"><span data-stu-id="a8259-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="a8259-107">W tym artykule przedstawiono usługi opartej na zasadach, które umożliwiają interakcję z wszelkich zewnętrznych HTTP.</span><span class="sxs-lookup"><span data-stu-id="a8259-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="a8259-108">Te zasady mogą służyć do wyzwalania zdarzenia zdalnego lub do pobierania informacji, która będzie służyć do modyfikowania oryginalnego żądania i odpowiedzi w jakiś sposób.</span><span class="sxs-lookup"><span data-stu-id="a8259-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="a8259-109">Sposób żądania, Wyślij co w-</span><span class="sxs-lookup"><span data-stu-id="a8259-109">Send-One-Way-Request</span></span>
<span data-ttu-id="a8259-110">Prawdopodobnie styl fire i zapomnij żądania, które umożliwia zewnętrznej usługi użytkownik jest powiadamiany określonego rodzaju zdarzenia ważne jest najprostsza interakcja zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="a8259-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="a8259-111">Możemy użyć zasad przepływu sterowania `choose` do wykrywania warunku, że Dbamy o, a następnie, jeśli spełniony jest warunek, firma Microsoft może wprowadzać zewnętrznych HTTP żądania przy użyciu dowolnego rodzaju [— jeden — sposób — żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) zasad.</span><span class="sxs-lookup"><span data-stu-id="a8259-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="a8259-112">Może to być żądanie systemu obsługi wiadomości, takie jak Hipchat lub Slack lub poczty interfejsu API SendGrid lub MailChimp, lub do obsługi krytycznych zdarzeń coś tak jak PagerDuty.</span><span class="sxs-lookup"><span data-stu-id="a8259-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="a8259-113">Wszystkie te systemy obsługi komunikatów mają prostych interfejsów API protokołu HTTP, które firma Microsoft może łatwo wywołać.</span><span class="sxs-lookup"><span data-stu-id="a8259-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="a8259-114">Alerty z zapas czasu</span><span class="sxs-lookup"><span data-stu-id="a8259-114">Alerting with Slack</span></span>
<span data-ttu-id="a8259-115">W poniższym przykładzie pokazano sposób wysyłania wiadomości Slack pokoju rozmów, jeśli kod stanu odpowiedzi HTTP jest większa niż lub równa 500.</span><span class="sxs-lookup"><span data-stu-id="a8259-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="a8259-116">Błąd zakresu 500 wskazuje na problem z naszych zaplecza interfejsu API klienta interfejsie API nie mogą się samoistnie rozwiązać.</span><span class="sxs-lookup"><span data-stu-id="a8259-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="a8259-117">Zwykle wymagają określonego rodzaju interwencji z naszej strony.</span><span class="sxs-lookup"><span data-stu-id="a8259-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="a8259-118">Zapas czasu ma pojęcie punkty zaczepienia dla ruchu przychodzącego sieci web.</span><span class="sxs-lookup"><span data-stu-id="a8259-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="a8259-119">Podczas konfigurowania punktu zaczepienia przychodzący sieci web, zapas czasu generuje specjalne adresu URL, który umożliwia przeprowadzenie prostego żądania POST i przekazania wiadomości do kanału Slack.</span><span class="sxs-lookup"><span data-stu-id="a8259-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="a8259-120">Treść kodu JSON, który utworzymy jest oparty na formacie zdefiniowane przez zapas czasu.</span><span class="sxs-lookup"><span data-stu-id="a8259-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Haku Slack sieci Web](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="a8259-122">To jest fire i zapomnij wystarczająco dobre?</span><span class="sxs-lookup"><span data-stu-id="a8259-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="a8259-123">Brak niektórych wady i zalety używając stylu fire i zapomnij żądania.</span><span class="sxs-lookup"><span data-stu-id="a8259-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="a8259-124">Jeśli dla jakiegoś powodu żądanie zakończy się niepowodzeniem, a następnie błędu nie będzie raportowana.</span><span class="sxs-lookup"><span data-stu-id="a8259-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="a8259-125">W takiej sytuacji określonego złożoność o awarii dodatkowej raportowania systemu i koszt wydajności dodatkowe oczekiwania na odpowiedź nie jest uzasadnione.</span><span class="sxs-lookup"><span data-stu-id="a8259-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="a8259-126">W scenariuszach, w których jest sprawdzenie odpowiedzi a następnie [żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) zasad jest lepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="a8259-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="a8259-127">Żądanie wysłania</span><span class="sxs-lookup"><span data-stu-id="a8259-127">Send-Request</span></span>
<span data-ttu-id="a8259-128">`send-request` Umożliwia zasad za pomocą zewnętrznej usługi do wykonywania zadań przetwarzania złożone i zwraca dane do usługi API management usług, który może służyć do dalszego przetwarzania zasad.</span><span class="sxs-lookup"><span data-stu-id="a8259-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="a8259-129">Autoryzowanie tokenów odwołań</span><span class="sxs-lookup"><span data-stu-id="a8259-129">Authorizing reference tokens</span></span>
<span data-ttu-id="a8259-130">Główna funkcja interfejsu API zarządzania jest ochrona zasobów wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a8259-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="a8259-131">Jeśli serwer autoryzacji używany przez interfejs API tworzy [tokenów JWT](http://jwt.io/) w ramach swojego przepływu OAuth2 jako [usługi Azure Active Directory](../active-directory/active-directory-aadconnect.md) tak, możesz użyć `validate-jwt` zasad w celu zweryfikowania jego ważności tokenu.</span><span class="sxs-lookup"><span data-stu-id="a8259-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="a8259-132">Jednak niektóre serwery autoryzacji utworzyć są nazywane [odwołania tokenów](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) nie można zweryfikować bez wykonywania wywołań do serwera autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="a8259-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="a8259-133">Introspection standardowych</span><span class="sxs-lookup"><span data-stu-id="a8259-133">Standardized introspection</span></span>
<span data-ttu-id="a8259-134">W przeszłości nie było żadnych standardowych możliwości sprawdzenia tokenu odwołania z serwera autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="a8259-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="a8259-135">Jednak ostatnio proponowany standard [RFC 7662](https://tools.ietf.org/html/rfc7662) została opublikowana przez grupę roboczą IETF, który definiuje sposób serwer zasobów można sprawdzić poprawności tokenu.</span><span class="sxs-lookup"><span data-stu-id="a8259-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="a8259-136">Wyodrębnianie tokenu</span><span class="sxs-lookup"><span data-stu-id="a8259-136">Extracting the token</span></span>
<span data-ttu-id="a8259-137">Pierwszym krokiem jest wyodrębnić tokenu w nagłówku autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="a8259-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="a8259-138">Wartość nagłówka powinien być sformatowany z `Bearer` schematu autoryzacji, pojedyncze spacje, a następnie autoryzację token zgodnie [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="a8259-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="a8259-139">Niestety istnieją przypadki, w których pominięto schematu autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="a8259-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="a8259-140">Aby to uwzględniać podczas analizowania, możemy podzielić wartość nagłówka w miejscu i wybierz ostatni ciąg z zwrócony tablicy ciągów.</span><span class="sxs-lookup"><span data-stu-id="a8259-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="a8259-141">Zapewnia to obejście nagłówki autoryzacji nieprawidłowo sformatowany.</span><span class="sxs-lookup"><span data-stu-id="a8259-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="a8259-142">Zgłoszenia żądania weryfikacji</span><span class="sxs-lookup"><span data-stu-id="a8259-142">Making the validation request</span></span>
<span data-ttu-id="a8259-143">Gdy mamy token autoryzacji, firma Microsoft może wprowadzać żądania do zweryfikowania tokenu.</span><span class="sxs-lookup"><span data-stu-id="a8259-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="a8259-144">RFC 7662 wywołuje introspection ten proces i wymaga, aby użytkownik `POST` formularza HTML do zasobu introspection.</span><span class="sxs-lookup"><span data-stu-id="a8259-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="a8259-145">Formularza HTML przy użyciu klucza musi zawierać co najmniej parę klucz/wartość `token`.</span><span class="sxs-lookup"><span data-stu-id="a8259-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="a8259-146">To żądanie do serwera autoryzacji również musi zostać uwierzytelniony do zapewnienia, że złośliwe klientów nie można go połowów włokiem dla prawidłowych tokenów.</span><span class="sxs-lookup"><span data-stu-id="a8259-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-the-response"></a><span data-ttu-id="a8259-147">Sprawdzanie odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a8259-147">Checking the response</span></span>
<span data-ttu-id="a8259-148">`response-variable-name` Atrybut jest używany do udostępnienia zwrócona odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="a8259-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="a8259-149">Nazwa zdefiniowana w tej właściwości może służyć jako klucza do `context.Variables` słownika dostępu do `IResponse` obiektu.</span><span class="sxs-lookup"><span data-stu-id="a8259-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="a8259-150">Z obiektu odpowiedzi można pobrać treści i RFC 7622 nam informuje, że odpowiedź musi być obiektem JSON i musi zawierać co najmniej właściwość o nazwie `active` będący wartością logiczną.</span><span class="sxs-lookup"><span data-stu-id="a8259-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="a8259-151">Gdy `active` ma wartość true, a następnie token jest uznawany za ważny.</span><span class="sxs-lookup"><span data-stu-id="a8259-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="a8259-152">Niepowodzenie raportowania</span><span class="sxs-lookup"><span data-stu-id="a8259-152">Reporting failure</span></span>
<span data-ttu-id="a8259-153">Używamy `<choose>` zasady, aby wykryć, czy token jest nieprawidłowy, a jeśli tak, zwracać odpowiedzi 401.</span><span class="sxs-lookup"><span data-stu-id="a8259-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="a8259-154">Zgodnie [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) którym opisano sposób `bearer` tokenów należy również zwróconych `WWW-Authenticate` nagłówek odpowiedzi 401.</span><span class="sxs-lookup"><span data-stu-id="a8259-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="a8259-155">WWW-Authenticate ma na celu poinstruować klienta, jak utworzyć prawidłowo nieautoryzowane żądanie.</span><span class="sxs-lookup"><span data-stu-id="a8259-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="a8259-156">Z powodu różnych metod niemożliwe w ramach protokołu OAuth2 jest trudne do komunikowania się wszystkich wymaganych informacji.</span><span class="sxs-lookup"><span data-stu-id="a8259-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="a8259-157">Na szczęście są przetwarzane, aby ułatwić [klientów dowiedzieć się, jak poprawnie autoryzować żądania do serwera zasobów](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span><span class="sxs-lookup"><span data-stu-id="a8259-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="a8259-158">Końcowa rozwiązania</span><span class="sxs-lookup"><span data-stu-id="a8259-158">Final solution</span></span>
<span data-ttu-id="a8259-159">Zestawienie wszystkie elementy, uzyskujemy następujące zasady:</span><span class="sxs-lookup"><span data-stu-id="a8259-159">Putting all the pieces together, we get the following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request to Token Server to validate token (see RFC 7662) -->
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

<span data-ttu-id="a8259-160">To jest tylko jedna wiele przykładów jak `send-request` zasad służy do integrowania przydatne usług zewnętrznych przetwarzania żądań i odpowiedzi przepływających przez usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="a8259-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="a8259-161">Kompozycja odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="a8259-161">Response Composition</span></span>
<span data-ttu-id="a8259-162">`send-request` Zasad może być używany do podnoszenia żądania podstawowego z systemem zaplecza jako widzieliśmy w poprzednim przykładzie, albo może służyć jako zakończenie Zamień dla wywołania wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a8259-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="a8259-163">Ta technika można łatwo utworzyć złożonego zasoby, które są agregowane z wielu różnych systemów.</span><span class="sxs-lookup"><span data-stu-id="a8259-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="a8259-164">Tworzenie pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="a8259-164">Building a dashboard</span></span>
<span data-ttu-id="a8259-165">Czasami ma być możliwe na celu ujawnienie informacji, który istnieje w wielu systemach wewnętrznej bazy danych, na przykład, aby dysk na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="a8259-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="a8259-166">Kluczowych wskaźników wydajności pochodzić z wszystkich różnych zapleczy, ale nie chcesz zapewnić bezpośredni dostęp do nich, i byłoby nieuprzywilejowany w ramach pojedynczego żądania można pobrać wszystkich informacji.</span><span class="sxs-lookup"><span data-stu-id="a8259-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="a8259-167">Prawdopodobnie niektóre informacje wewnętrznej bazy danych wymaga niektórych dzielenie i grupowanie i niewielką najpierw oczyszczania!</span><span class="sxs-lookup"><span data-stu-id="a8259-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="a8259-168">Możliwość buforowania złożonego zasobu będzie można zmniejszyć obciążenie wewnętrznej bazy danych, ponieważ wiadomo, że użytkownicy mają rodzaj atakowaniu klawisz F5, aby zobaczyć, czy ich underperforming metryki mogą ulec zmianie.</span><span class="sxs-lookup"><span data-stu-id="a8259-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="a8259-169">Faking zasobu</span><span class="sxs-lookup"><span data-stu-id="a8259-169">Faking the resource</span></span>
<span data-ttu-id="a8259-170">Pierwszy krok w celu tworzenia zasobów naszej pulpit nawigacyjny jest do skonfigurowania nowej operacji w portalu zarządzania interfejsu API wydawcy.</span><span class="sxs-lookup"><span data-stu-id="a8259-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="a8259-171">Jest to operacja symbolu zastępczego, używany do konfigurowania naszymi zasadami kompozycji do naszej zasobu dynamicznego tworzenia.</span><span class="sxs-lookup"><span data-stu-id="a8259-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![Operacja pulpitu nawigacyjnego](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="a8259-173">Tworzenie żądania</span><span class="sxs-lookup"><span data-stu-id="a8259-173">Making the requests</span></span>
<span data-ttu-id="a8259-174">Raz `dashboard` utworzono operacji można skonfigurować zasady dla tej operacji.</span><span class="sxs-lookup"><span data-stu-id="a8259-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![Operacja pulpitu nawigacyjnego](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="a8259-176">Pierwszym krokiem jest Wyodrębnij wszystkie parametry zapytania z żądania przychodzącego, dzięki czemu możemy przekazują je do naszej wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a8259-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="a8259-177">W tym przykładzie naszych pulpit nawigacyjny jest pokazywane są informacje oparte na pewien czas w związku z tym ma `fromDate` i `toDate` parametru.</span><span class="sxs-lookup"><span data-stu-id="a8259-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="a8259-178">Możemy użyć `set-variable` zasady w celu wyodrębnienia informacji z adresu URL żądania.</span><span class="sxs-lookup"><span data-stu-id="a8259-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="a8259-179">Gdy mamy tych informacji firma Microsoft może wprowadzać żądania we wszystkich systemach wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a8259-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="a8259-180">Każde żądanie tworzy nowy adres URL z parametrów i wywołuje jego odpowiedniego serwera i przechowuje odpowiedzi w zmiennej kontekstu.</span><span class="sxs-lookup"><span data-stu-id="a8259-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

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

<span data-ttu-id="a8259-181">Te żądania będą wykonywane w kolejności, która nie jest idealnym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="a8259-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="a8259-182">W kolejnych wersji możemy można wprowadzenia nowych zasad o nazwie `wait` umożliwi wszystkie te żądania do wykonywania równoległego.</span><span class="sxs-lookup"><span data-stu-id="a8259-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="a8259-183">Odpowiada</span><span class="sxs-lookup"><span data-stu-id="a8259-183">Responding</span></span>
<span data-ttu-id="a8259-184">Do utworzenia złożonego odpowiedzi, możemy użyć [odpowiedzi zwracany](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) zasad.</span><span class="sxs-lookup"><span data-stu-id="a8259-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="a8259-185">`set-body` Elementu można użyć wyrażenia do utworzenia nowego `JObject` z reprezentacji składnika osadzony jako właściwości.</span><span class="sxs-lookup"><span data-stu-id="a8259-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

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

<span data-ttu-id="a8259-186">Zasady w pełnej wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="a8259-186">The complete policy looks as follows:</span></span>

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

<span data-ttu-id="a8259-187">W konfiguracji symbol zastępczy operacji można skonfigurować zasobów pulpitu nawigacyjnego można buforować przez co najmniej godzinę, ponieważ Rozumiemy charakter danych oznacza, że nawet jeśli jest nieaktualna, będzie on nadal dostępny wystarczająco skuteczne w celu przedstawienia cenne informacje, które użytkownicy godzinę.</span><span class="sxs-lookup"><span data-stu-id="a8259-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="a8259-188">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="a8259-188">Summary</span></span>
<span data-ttu-id="a8259-189">Usługi Zarządzanie interfejsami API Azure oferuje elastyczne zasady, które można wybiórczo zastosować do ruchu HTTP i umożliwia kompozycji usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a8259-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="a8259-190">Czy chcesz zwiększyć bramy interfejsu API z alerty funkcje, weryfikacji i sprawdzania poprawności możliwości lub utworzyć nowe zasoby złożonego na podstawie wielu usług zaplecza, `send-request` i związane z nią zasady Otwórz world możliwości.</span><span class="sxs-lookup"><span data-stu-id="a8259-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="a8259-191">Obejrzyj film poglądowy dotyczący tych zasad</span><span class="sxs-lookup"><span data-stu-id="a8259-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="a8259-192">Aby uzyskać więcej informacji na temat [sposób żądania, Wyślij co w-](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), i [odpowiedzi zwracany](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) zasady omówione w tym artykule, obserwuj poniższego klipu wideo.</span><span class="sxs-lookup"><span data-stu-id="a8259-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

