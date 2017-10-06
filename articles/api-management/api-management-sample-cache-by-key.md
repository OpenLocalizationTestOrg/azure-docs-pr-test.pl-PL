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
# <a name="custom-caching-in-azure-api-management"></a>Buforowanie niestandardowych w usłudze Azure API Management
Usługa Azure API Management ma wbudowaną obsługę [buforowanie odpowiedzi HTTP](api-management-howto-cache.md) przy użyciu adresu URL zasobu hello jako hello klucza. Witaj klucza może być modyfikowany przez nagłówki żądania przy użyciu hello `vary-by` właściwości. Jest to przydatne w przypadku buforowanie całej odpowiedzi HTTP (alias oświadczenia), ale czasami jest przydatne toojust pamięci podręcznej część reprezentacji. nowe Hello [pamięci podręcznej wyszukiwania wartości](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) i [-magazynu wartość w pamięci podręcznej](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) zasady zapewniają możliwość hello toostore i pobrać dowolnego fragmentów danych z poziomu definicji zasad. Tę możliwość dodaje również toohello wartość poprzednio wprowadzone [żądanie wysłania](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) zasad ponieważ teraz może buforować odpowiedzi z usług zewnętrznych.

## <a name="architecture"></a>Architektura
Zarządzanie interfejsami API usługi używa pamięci podręcznej danych dzierżawy udostępnionego tak, aby podczas skalowania jednostek toomultiple toohello dostępu będą nadal otrzymywać takie same dane z pamięci podręcznej. Podczas pracy z wdrożenia w przypadku istnieją niezależne pamięci podręcznych w regionach hello. Z powodu toothis, ważne jest toonot zaliczenie magazynu danych, jeśli jest to jedyne źródło informacji o elemencie hello hello pamięci podręcznej. Jeśli została i później decyzję tootake zaletą hello w przypadku wdrażania klientów z użytkowników, którzy podróżują może utracić dostęp do danych w pamięci podręcznej toothat.

## <a name="fragment-caching"></a>Buforowanie fragmentu
Brak niektórych przypadkach, gdy odpowiedzi zwracanych zawiera pewną część danych toodetermine kosztowne i jeszcze pozostaje świeże sensownym czasie. Na przykład należy wziąć pod uwagę usługę utworzony przez linii lotniczych, który zawiera informacje dotyczące zastrzeżenia transmitowane, stan transmitowane itp. Jeśli hello użytkownik jest członkiem hello airlines punktów program, również zostałyby informacje dotyczące tootheir bieżący stan i zebraniu przebiegu. Te informacje dotyczące użytkowników mogą być przechowywane w innym systemie, ale może być pożądane tooinclude w odpowiedzi dotyczące stanu transmitowane i zastrzeżenia zwrócone. Można to zrobić w procesie zwanym buforowanie fragmentu. Hello reprezentacja głównej mogą zostać zwrócone z serwera pochodzenia hello przy użyciu określonego rodzaju token tooindicate hello informacji dotyczących użytkownika w przypadku toobe wstawiony. 

Należy wziąć pod uwagę powitania po odpowiedź w formacie JSON z zaplecza interfejsu API.

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

I dodatkowej zasobu pod adresem `/userprofile/{userid}` takie, jak,

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

W kolejności toodetermine hello odpowiedniego użytkownika informacje tooinclude potrzebujemy tooidentify, który użytkownik końcowy hello jest. Ten mechanizm jest zależy od implementacji. Na przykład używam hello `Subject` oświadczeń z `JWT` tokenu. 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

To są przechowywane `enduserid` wartość w zmiennej kontekstu do późniejszego użycia. następnym krokiem Hello jest toodetermine, jeśli poprzednie żądanie ma już pobrane informacje o użytkowniku hello i zapisana w pamięci podręcznej hello. W tym używamy hello `cache-lookup-value` zasad.

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

Jeśli w pamięci podręcznej hello, które odpowiada toohello wartości klucza, a następnie nr nie ma wpisu `userprofile` zmiennej kontekstu, która zostanie utworzona. Musimy sprawdzić, powodzenia hello hello wyszukiwania przy użyciu hello `choose` sterowanie przepływem zasad.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

Jeśli hello `userprofile` zmiennej kontekstu, która nie istnieje, a następnie możemy będzie toohave toomake HTTP żądania tooretrieve go.

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

Używamy hello `enduserid` zasób profilu użytkownika toohello tooconstruct hello adresu URL. Po mamy odpowiedź hello możemy ściągnięcia hello treść poza hello odpowiedzi i zapisze go do zmiennej kontekstu.

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

tooavoid nas o toomake tego żądania HTTP ponownie, gdy hello tego samego użytkownika powoduje, że inne żądanie może przechowujemy hello profilu użytkownika w pamięci podręcznej hello.

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

Wartość hello są przechowywane w pamięci podręcznej hello przy użyciu hello dokładnie tego samego klucza możemy pierwotnie podjęto tooretrieve go. Witaj czas, przez jaki wybrany toostore hello wartość powinna być oparta na częstotliwość hello zmiany informacji i sposobu odporny na błędy użytkowników są tooout informacje o dacie. 

Jest ważne toorealize, że pobieranie z pamięci podręcznej hello jest nadal poza procesem, żądanie sieciowe i potencjalnie można dodawać dziesiątki żądania toohello milisekund. korzyści Hello pochodzić podczas określania informacji o profilu użytkownika hello trwa znacznie dłużej niż zapytań bazy danych toodo tooneeding lub zagregowanych informacji z wielu zapleczy.

Hello ostatnim krokiem w procesie hello jest hello tooupdate zwrócił odpowiedź o naszych informacje o profilu użytkownika.

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

Wybrano tooinclude hello cudzysłów jako część tokenu hello, dzięki czemu nawet wtedy, gdy nie występuje Zamień hello, hello odpowiedź była nadal poprawne dane JSON. To przede wszystkim toomake ułatwia debugowanie.

Te kroki są łączone ze sobą, wynik końcowy powitania po zasad, która wygląda jak powitania po jednym.

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

Takie podejście buforowania jest używany głównie w witrynach sieci web gdzie HTML składa się na powitania po stronie serwera, dzięki czemu mogą być renderowane jako pojedynczej strony. Jednak również jest przydatny w interfejsów API, gdzie klienci nie klienta po stronie buforowanie HTTP lub pożądane jest nie tooput że odpowiedzialność na powitania klienta.

Można również wykonać tego samego rodzaju fragmentu buforowanie na serwerze sieci web zaplecza hello za pomocą Redis, buforowanie serwera, jednak przy użyciu tooperform usługi Zarządzanie interfejsami API hello tej pracy jest przydatne, gdy fragmenty hello buforowane pochodzą z różnych zapleczy niż hello podstawowy odpowiedzi.

## <a name="transparent-versioning"></a>Przechowywanie wersji przezroczyste
Jest typowym rozwiązaniem w przypadku wielu wersji inną implementację toobe interfejsu API, obsługiwane w dowolnym momencie. Jest to prawdopodobnie różnych środowiskach toosupport deweloperów, testu, produkcji itd., lub może być toosupport starsze wersje czasu toogive hello interfejsu API dla wersji toonewer toomigrate konsumentów interfejsu API. 

Jednym z podejść toohandling tym zamiast elementu wymagające adresy URL hello toochange deweloperzy klienta z `/v1/customers` zbyt`/v2/customers` jest toostore w dane profilu użytkownika hello wersję interfejsu API hello one obecnie ma toouse i Wywołaj hello odpowiednie adres URL wewnętrznej bazy danych. W kolejności toodetermine hello zaplecza poprawny adres URL toocall dla określonego klienta, jest konieczne tooquery niektóre dane konfiguracji. Buforowanie danych konfiguracji, możemy zminimalizować spadek wydajności hello prowadzenia tego wyszukiwania.

pierwszym krokiem Hello jest używany identyfikator hello toodetermine tooconfigure hello żądanej wersji. W tym przykładzie wybrano tooassociate hello wersji toohello subskrypcji klucza. 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

Jeśli już pobrano wersji klienta żądaną hello następnie jak toosee wyszukiwania pamięci podręcznej.

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

Następnie sprawdzamy toosee, jeśli nie znaleziono go w pamięci podręcznej hello.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

Jeśli firma Microsoft nie możemy przejść i pobrać go.

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

Wyodrębnij tekst treści odpowiedzi hello z hello odpowiedzi.

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

Zapisz go w pamięci podręcznej hello do użytku w przyszłości.

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

I na koniec zaktualizuj hello wewnętrznego adresu URL tooselect hello wersji żądanej przez klienta na powitania usługi hello.

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

Witaj całkowicie zasad ma następującą składnię.

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

Włączanie tootransparently sterowanie konsumentów interfejsu API, która wersja wewnętrznej bazy danych jest uzyskiwany przez klientów bez konieczności tooupdate i ponownego wdrażania klientów jest atrakcyjny rozwiązaniem, które rozwiązuje wiele problemów przechowywanie wersji interfejsu API.

## <a name="tenant-isolation"></a>Izolacji dzierżawców
W przypadku większych i wielodostępne wdrożeń niektóre firmy utworzenie oddzielnych grup dzierżawcy na różnych wdrożeń sprzętu wewnętrznej bazy danych. Pozwala to zmniejszyć hello liczbę klientów, którzy mają wpływ problemem sprzętowym hello wewnętrznej bazy danych. Umożliwia również nowe toobe wersji oprogramowania wprowadzanie etapami. W idealnym przypadku tej architektury wewnętrznej bazy danych powinny być przezroczyste tooAPI konsumentów. Można to osiągnąć w podobne versioning tootransparent sposób ponieważ jest ona oparta na powitania tę samą metodę manipulowania hello URL wewnętrznej bazy danych przy użyciu stan konfiguracji na klucz interfejsu API.  

Zamiast zwracać preferowanych wersji hello interfejsu API dla każdego klucza subskrypcji, zwróci identyfikator, który dotyczy grupy sprzętu toohello przypisane dzierżawy. Ten identyfikator może być URL odpowiedniej wewnętrznej bazy danych hello tooconstruct używane.

## <a name="summary"></a>Podsumowanie
Witaj swobodę toouse Witaj pamięci podręcznej zarządzania interfejsu API Azure do przechowywania każdego typu danych umożliwia wydajne dostępu tooconfiguration dane, które mogą mieć wpływ na sposób hello przetwarzanie żądania przychodzącego. Można także toostore używane fragmenty danych, które można rozszerzyć odpowiedzi zwrócone przez interfejs API zaplecza.

## <a name="next-steps"></a>Następne kroki
Daj nam swoją opinię w hello wątku usługi Disqus dla tego tematu, jeśli istnieją inne scenariusze, czy te zasady mają włączona lub jeśli istnieją scenariusze chcieliby tooachieve, ale nie jest konieczne są obecnie możliwe.

