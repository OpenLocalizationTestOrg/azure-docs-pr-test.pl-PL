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
# <a name="using-external-services-from-hello-azure-api-management-service"></a>Za pomocą usług zewnętrznych z hello usługi Zarządzanie interfejsami API Azure
zasady Hello dostępne w usłudze Azure API Management należy szeroką gamę przydatne pracy wyłącznie na podstawie żądania przychodzącego hello, odpowiedzi wychodzącej hello i podstawowe informacje o konfiguracji. Jednak jest możliwe toointeract z usług zewnętrznych z interfejsu API zarządzania otwiera wiele możliwości więcej zasad.

Zaobserwowano wcześniej, jak firma Microsoft może interakcyjnie hello [usługi Azure Event Hub rejestrowania, monitorowania i analizy](api-management-log-to-eventhub-sample.md). W tym artykule przedstawiono usługi opartej na zasadach, które pozwalają toointeract wszelkich zewnętrznych protokołu HTTP. Te zasady mogą służyć do wyzwalania zdarzenia zdalnego lub do pobierania informacji, które będzie używane toomanipulate hello oryginalnego żądania i odpowiedzi w jakiś sposób.

## <a name="send-one-way-request"></a>Sposób żądania, Wyślij co w-
Prawdopodobnie hello najprostszym zewnętrzne jest interakcja hello fire i zapomnij styl żądania, które umożliwia toobe zewnętrznej usługi zgłoszone pewnego rodzaju ważnych zdarzeń. Możemy użyć zasad przepływu sterowania hello `choose` toodetect spełniony jest dowolny rodzaj warunek, który firma Microsoft są zainteresowani, a następnie, jeśli hello warunku, firma Microsoft może wprowadzać zewnętrznych żądań HTTP przy użyciu hello [— jeden — sposób — żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) zasad. Może to być tooa żądania, systemu, takie jak Hipchat lub Slack lub poczty interfejsu API SendGrid lub MailChimp obsługi wiadomości, lub do obsługi krytycznych zdarzeń coś tak jak PagerDuty. Wszystkie te systemy obsługi komunikatów mają prostych interfejsów API protokołu HTTP, które firma Microsoft może łatwo wywołać.

### <a name="alerting-with-slack"></a>Alerty z zapas czasu
Witaj poniższy przykład pokazuje, jak toosend tooa komunikat Slack pokoju rozmów, jeśli kod stanu odpowiedzi HTTP hello jest większa niż lub równa too500. Błąd zakresu 500 oznacza, że nie można się samoistnie rozwiązać problem z naszych zaplecza interfejsu API, który hello klienta interfejsach API. Zwykle wymagają określonego rodzaju interwencji z naszej strony.  

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

Zapas czasu ma hello pojęcie punkty zaczepienia dla ruchu przychodzącego sieci web. Podczas konfigurowania punktu zaczepienia przychodzący sieci web, zapas czasu generuje specjalne adresu URL, który pozwala toodo prostego żądania POST, toopass komunikat do kanału Slack hello. Hello treści JSON, który utworzymy jest oparty na formacie zdefiniowane przez zapas czasu.

![Haku Slack sieci Web](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a>To jest fire i zapomnij wystarczająco dobre?
Brak niektórych wady i zalety używając stylu fire i zapomnij żądania. Jeśli dla jakiegoś powodu hello żądanie kończy się niepowodzeniem, a następnie hello błąd nie będzie raportowana. W takiej sytuacji określonego złożoność hello system raportowania błędu serwera pomocniczego i Oczekiwanie na odpowiedź hello koszt wydajności dodatkowe hello nie jest uzasadnione. W scenariuszach, w których jest istotne toocheck hello odpowiedzi, następnie hello [żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) zasad jest lepszym rozwiązaniem.

## <a name="send-request"></a>Żądanie wysłania
Witaj `send-request` umożliwia zasad za pomocą zewnętrznej usługi tooperform złożonych przetwarzania funkcji a danych zwrotnych toohello interfejsu API zarządzania usługą, która może służyć do dalszego przetwarzania zasad.

### <a name="authorizing-reference-tokens"></a>Autoryzowanie tokenów odwołań
Główna funkcja interfejsu API zarządzania jest ochrona zasobów wewnętrznej bazy danych. Jeśli używane przez interfejs API serwera autoryzacji hello tworzy [tokenów JWT](http://jwt.io/) w ramach swojego przepływu OAuth2 jako [usługi Azure Active Directory](../active-directory/active-directory-aadconnect.md) tak, możesz użyć hello `validate-jwt` ważność hello tooverify zasad Hello token. Jednak niektóre serwery autoryzacji utworzyć są nazywane [odwołania tokenów](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) nie można zweryfikować bez wprowadzania serwera autoryzacji wstecz toohello wywołania.

### <a name="standardized-introspection"></a>Introspection standardowych
W przeszłości hello nie było żadnych standardowych możliwości sprawdzenia tokenu odwołania z serwera autoryzacji. Jednak ostatnio proponowany standard [RFC 7662](https://tools.ietf.org/html/rfc7662) opublikował hello IETF, który określa, jak serwer zasobów można zweryfikować hello ważności tokenu.

### <a name="extracting-hello-token"></a>Wyodrębnianie hello tokenu
pierwszym krokiem Hello jest tokenem hello tooextract z nagłówka autoryzacji hello. wartość nagłówka Hello powinien być sformatowany z hello `Bearer` schematu autoryzacji, pojedyncze spacje i następnie autoryzacji hello token zgodnie [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1). Niestety istnieją przypadki, w którym hello autoryzacji schemat zostanie pominięty. tooaccount tego podczas analizowania, możemy podzielić wartość nagłówka hello miejsca i wybierz hello ostatni ciąg z hello zwrócił tablicę ciągów. Zapewnia to obejście nagłówki autoryzacji nieprawidłowo sformatowany.

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a>Tworzenie żądania sprawdzenia poprawności hello
Gdy mamy hello token autoryzacji, firma Microsoft może wprowadzać hello żądania toovalidate hello tokenu. RFC 7662 wywołuje introspection ten proces i wymaga, aby użytkownik `POST` zasobu introspection toohello formularza HTML. Hello formularza HTML z kluczem hello musi zawierać co najmniej parę klucz/wartość `token`. Ten serwer autoryzacji toohello żądania również musi być uwierzytelniony tooensure, że złośliwe klientów nie można go połowów włokiem dla prawidłowych tokenów.

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

### <a name="checking-hello-response"></a>Sprawdzanie, czy odpowiedź hello
Witaj `response-variable-name` atrybutów jest używane toogive dostępu hello zwrócił odpowiedź. Witaj nazwa zdefiniowana w tej właściwości może być używana jako klucz w hello `context.Variables` hello tooaccess słownika `IResponse` obiektu.

Z obiektu odpowiedzi hello możemy pobrać treści hello i RFC 7622 nam informuje, że hello odpowiedzi musi być obiektem JSON i musi zawierać co najmniej właściwość o nazwie `active` będący wartością logiczną. Gdy `active` ma wartość true, a następnie hello token jest uznawany za ważny.

### <a name="reporting-failure"></a>Niepowodzenie raportowania
Używamy `<choose>` toodetect zasad, jeśli hello token jest nieprawidłowy, a zwracany odpowiedzi 401.

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

Zgodnie [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) którym opisano sposób `bearer` tokenów należy również zwróconych `WWW-Authenticate` nagłówka odpowiedzi hello 401. Witaj WWW-Authenticate jest tooinstruct przeznaczone klienckich na temat tooconstruct prawidłowo nieautoryzowane żądanie. Powodu toohello szerokiej gamy podejścia przy użyciu usługi framework hello OAuth2, trudno jest toocommunicate hello wszystkich potrzebnych informacji. Na szczęście są przetwarzane toohelp [klientów odnajdywania, jak tooproperly autoryzować serwer zasobów tooa żądań](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).

### <a name="final-solution"></a>Końcowa rozwiązania
Zestawienie wszystkie elementy hello, uzyskujemy hello następujące zasady:

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

Jest to tylko jeden z wielu przykłady hello `send-request` zasad mogą być przydatne usług zewnętrznych toointegrate używane w procesie hello żądań i odpowiedzi przepływających przez hello usługi Zarządzanie interfejsami API.

## <a name="response-composition"></a>Kompozycja odpowiedzi
Witaj `send-request` zasady mogą służyć do zwiększenia system wewnętrznej bazy danych żądania podstawowego tooa widzieliśmy w poprzednim przykładzie hello lub może służyć jako pełną Zamień dla hello wywołania wewnętrznej bazy danych. Ta technika można łatwo utworzyć złożonego zasoby, które są agregowane z wielu różnych systemów.

### <a name="building-a-dashboard"></a>Tworzenie pulpitu nawigacyjnego
Czasami ma toobe stanie tooexpose informacji w wielu systemach wewnętrznej bazy danych, na przykład toodrive pulpitu nawigacyjnego. Hello wskaźników KPI pochodzą z wszystkich różnych zapleczy, ale wolisz nie tooprovide bezpośredni dostęp do toothem i byłoby nieuprzywilejowany można pobrać informacji o wszystkich hello pojedyncze żądanie. Możliwe, że niektóre hello wewnętrznej bazy danych informacji muszą niektóre dzielenie i grupowanie i niewielką najpierw oczyszczania! Trwa toocache możliwe, że złożone zasobów będą przydatne tooreduce zaplecza hello załadować wiesz, że użytkownicy mają rodzaj atakowaniu hello klawisz F5 w kolejności toosee, jeśli ich underperforming metryki mogą ulec zmianie.    

### <a name="faking-hello-resource"></a>Faking hello zasobów
pierwszy krok toobuilding Hello naszych zasobów pulpit nawigacyjny jest tooconfigure nowej operacji w portalu wydawcy zarządzanie interfejsami API hello. To będzie tooconfigure stosowaną symbolu zastępczego naszych toobuild zasad kompozycji naszych zasobu dynamicznego.

![Operacja pulpitu nawigacyjnego](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a>Tworzenie żądania hello
Raz hello `dashboard` utworzono operacji można skonfigurować zasady dla tej operacji. 

![Operacja pulpitu nawigacyjnego](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

pierwszym krokiem Hello jest tooextract żadnych parametrów zapytania z żądania przychodzącego hello, tak, aby firma Microsoft może przekazywać tooour wewnętrznej bazy danych. W tym przykładzie naszych pulpit nawigacyjny jest pokazywane są informacje oparte na pewien czas w związku z tym ma `fromDate` i `toDate` parametru. Możemy użyć hello `set-variable` informacje o zasadach tooextract hello z hello adresu URL żądania.

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

Gdy mamy tych informacji firma Microsoft może wprowadzać żądania w systemy zaplecza hello tooall. Każde żądanie tworzy nowy adres URL z informacji o parametrach hello wywołuje jego odpowiedniego serwera i zapisuje odpowiedź hello w zmiennej kontekstu.

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

Te żądania będą wykonywane w kolejności, która nie jest idealnym rozwiązaniem. W kolejnych wersji możemy można wprowadzenia nowych zasad o nazwie `wait` umożliwi wszystkie te żądania tooexecute równolegle.

### <a name="responding"></a>Odpowiada
odpowiedź złożonego hello tooconstruct używamy hello [odpowiedzi zwracany](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) zasad. Witaj `set-body` elementu można użyć wyrażenia tooconstruct nowy `JObject` z wszystkich reprezentacje składnika hello osadzony jako właściwości.

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

zasady pełną Hello wygląda następująco:

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

W konfiguracji hello hello symbolu zastępczego operacji, które można skonfigurować toobe zasobów pulpitu nawigacyjnego hello w pamięci podręcznej dla co najmniej godzinę ponieważ rozumiemy, że hello rodzaj danych hello oznacza, że nawet jeśli jest nieaktualny, będzie on nadal dostępny wystarczająco skuteczne godzinę tooconvey cenne informacje toohello użytkowników.

## <a name="summary"></a>Podsumowanie
Usługi Zarządzanie interfejsami API Azure oferuje elastyczne zasady, które można wybiórczo zastosować tooHTTP ruchu i umożliwia kompozycji usługi wewnętrznej bazy danych. Czy chcesz tooenhance bramy interfejsu API z alerty funkcje, weryfikacji i sprawdzania poprawności możliwości lub tworzenia nowych zasobów złożonego na podstawie wielu usług zaplecza, hello `send-request` i związane z nią zasady Otwórz world możliwości.

## <a name="watch-a-video-overview-of-these-policies"></a>Obejrzyj film poglądowy dotyczący tych zasad
Aby uzyskać więcej informacji na temat hello [sposób żądania, Wyślij co w-](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), i [odpowiedzi zwracany](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) zasady omówione w tym artykule, obserwuj powitania po wideo.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

