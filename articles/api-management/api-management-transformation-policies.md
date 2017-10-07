---
title: "zasad przekształcania zarządzanie interfejsami API aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad przekształcania hello dostępne do użycia w usłudze Azure API Management."
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
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a>Zarządzanie interfejsami API zasad przekształcania
W tym temacie znajdują się informacje na następujące zasady usługi API Management hello. Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="TransformationPolicies"></a>Zasad przekształcania  
  
-   [Konwertuj JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) — konwertuje żądania lub odpowiedzi body z JSON tooXML.  
  
-   [Konwertuj XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) — konwertuje żądania lub odpowiedzi body z XML tooJSON.  
  
-   [Znajdowanie i zamienianie ciągów w treści](api-management-transformation-policies.md#Findandreplacestringinbody) — znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.  
  
-   [Maski adresów URL w zawartości](api-management-transformation-policies.md#MaskURLSContent) -ponownie zapisuje (maski) łącza w odpowiedzi hello body tak, aby wskazywały toohello równoważne połączenie za pośrednictwem bramy hello.  
  
-   [Ustaw usługę zaplecza](api-management-transformation-policies.md#SetBackendService) — zmienia hello usługi wewnętrznej bazy danych dla żądania przychodzącego.  
  
-   [Ustaw treści](api-management-transformation-policies.md#SetBody) -ustawia treść wiadomości powitania żądań przychodzących i wychodzących.  
  
-   [Set — nagłówek HTTP](api-management-transformation-policies.md#SetHTTPheader) — przypisuje wartość tooan istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.  
  
-   [Wartość parametru ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) — dodaje, zastępuje wartość lub usuwa parametru ciągu zapytania żądania.  
  
-   [Ponowne zapisywanie adresów URL](api-management-transformation-policies.md#RewriteURL) — konwertuje adres URL żądania w postaci toohello publicznego formularza oczekiwane przez usługę sieci web hello.  
  
-   [Przekształcanie XML za pomocą XSLT](api-management-transformation-policies.md#XSLTransform) — ma zastosowanie tooXML transformacji XSL w treści żądania lub odpowiedzi hello.  
  
##  <a name="ConvertJSONtoXML"></a>Konwertuj JSON tooXML  
 Witaj `json-to-xml` zasad konwertuje treści żądania lub odpowiedzi z JSON tooXML.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Przykład  
  
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
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|JSON do pliku xml|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|Zastosuj|Atrybut Hello musi być ustawiona tooone hello następujące wartości.<br /><br /> -zawsze — Zawsze stosuj konwersji.<br />convert zawartości typu json - tylko wtedy, gdy nagłówek odpowiedzi Content-Type wskazuje obecność JSON.|Tak|Nie dotyczy|  
|należy wziąć pod uwagę zaakceptować — nagłówek|Atrybut Hello musi być ustawiona tooone hello następujące wartości.<br /><br /> — wartość true — zastosowania konwersji w żądaniu nagłówka Accept żądania JSON.<br />— wartość false — Zawsze stosuj konwersji.|Nie|Wartość true|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzące, wychodzące, na błąd  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="ConvertXMLtoJSON"></a>Konwertuj XML tooJSON  
 Witaj `xml-to-json` zasad konwertuje treści żądania lub odpowiedzi z XML tooJSON. Te zasady mogą być używane toomodernize, podstawą interfejsów API usług sieci web XML — tylko do wewnętrznej bazy danych.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a>Przykład  
  
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
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|XML do formatu json|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|rodzaj|Atrybut Hello musi być ustawiona tooone hello następujące wartości.<br /><br /> javascript — przyjazne - hello przekonwertować JSON ma deweloperzy przyjazną tooJavaScript formularza.<br />-bezpośredni — Witaj przekonwertowanego JSON odzwierciedla strukturę dokumentu XML oryginalnego hello.|Tak|Nie dotyczy|  
|Zastosuj|Atrybut Hello musi być ustawiona tooone hello następujące wartości.<br /><br /> -zawsze - przekonwertować zawsze.<br />convert zawartości — typ xml - tylko wtedy, gdy nagłówek odpowiedzi Content-Type wskazuje obecność XML.|Tak|Nie dotyczy|  
|należy wziąć pod uwagę zaakceptować — nagłówek|Atrybut Hello musi być ustawiona tooone hello następujące wartości.<br /><br /> Jeśli żądanie XML w żądaniu nagłówek Accept - wartość true — mają zastosowanie konwersji.<br />— wartość false — Zawsze stosuj konwersji.|Nie|Wartość true|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzące, wychodzące, na błąd  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="Findandreplacestringinbody"></a>Znajdowanie i zamienianie ciągów w treści  
 Witaj `find-and-replace` zasad znajduje podciąg żądania lub odpowiedzi i zastępuje go inny podciąg.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a>Przykład  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|Znajdź i Zamień|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|Z|toosearch ciąg Hello dla.|Tak|Nie dotyczy|  
|na|Witaj ciąg zastępczy. Określ zero długość ciągu tooremove hello wyszukiwania ciąg zastępczy.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="MaskURLSContent"></a>Adresy URL maski w zawartości  
 Witaj `redirect-content-urls` zasad ponownie zapisuje łącza (maski) w treści odpowiedzi hello tak, aby wskazywały toohello równoważne połączenie za pośrednictwem bramy hello. Są używane w hello wychodzącego sekcji toore zapisu odpowiedzi treści łącza toomake toohello punktu bramy. Użyj w hello ruchu przychodzącego sekcji odwrotny efekt.  
  
> [!NOTE]
>  Ta zasada nie zmienia żadnych wartości nagłówka takich `Location` nagłówków. wartości nagłówka toochange, użyj hello [nagłówka set](api-management-transformation-policies.md#SetHTTPheader) zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a>Przykład  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|adresy URL zawartości przekierowań|Element główny.|Tak|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzące, wychodzące  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="SetBackendService"></a>Ustawianie usługi wewnętrznej bazy danych  
 Użyj hello `set-backend-service` tooredirect zasad przychodzącego żądania tooa różnych wewnętrznej bazy danych niż hello określonego w ustawieniach hello interfejsu API dla tej operacji. Ta zasada zmienia hello wewnętrznej bazy danych usługi podstawowy adres URL hello przychodzącego żądania toohello jednym określonym w zasadach hello.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a>Przykład  
  
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
W tym hello przykład zasad usługi wewnętrznej bazy danych dla zestawu kieruje żądania na podstawie wartości wersji hello przekazano hello zapytania ciąg tooa różnych wewnętrznej bazy danych usługi niż hello hello określony w jednej z interfejsu API.
  
Początkowo hello podstawowy adres URL usługi wewnętrznej bazy danych jest pochodną hello ustawień interfejsu API. Dlatego hello adresu URL żądania `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` staje się `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` gdzie `http://contoso.com/api/10.4/` hello wewnętrznej bazy danych usługi adresu URL określonego w ustawieniach hello interfejsu API.  
  
Gdy hello [< Wybierz\> ](api-management-advanced-policies.md#choose) deklaracji zasad są stosowane hello wewnętrznej bazy danych usługi podstawowy adres URL może zmienić ponownie albo zbyt`http://contoso.com/api/8.2` lub `http://contoso.com/api/9.1`, w zależności od hello wartość parametru zapytania żądania hello w wersji. Na przykład jeśli hello jest wartość `"2013-15"` hello żądania końcowego adresu URL staje się `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.  
  
Jeśli dodatkowo przekształcenie żądania hello jest żądany, inne [zasad przekształcania](api-management-transformation-policies.md#TransformationPolicies) mogą być używane. Na przykład tooremove hello wersji zapytania parametru skoro hello żądanie jest kierowane tooa zaplecza określonej wersji, hello [ustawić parametr ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) zasadę można następnie atrybut version nadmiarowe obecnie hello tooremove używane.  
  
### <a name="example"></a>Przykład  
  
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
W tym przykładzie hello zasad trasy hello żądania tooa usługi sieci szkieletowej zapleczu przy użyciu ciągu zapytania identyfikatora userId hello jako klucza partycji hello i hello repliki podstawowej hello partycji.  

### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|zestaw wewnętrznej bazy danych usługi|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|adres url Base|Nowego zaplecza podstawowy adres URL usługi.|Nie|Nie dotyczy|  
|Identyfikator wewnętrznej bazy danych|Identyfikator hello tooroute wewnętrznej bazy danych do.|Nie|Nie dotyczy|  
|rz partycji klucza|Dotyczy tylko gdy hello wewnętrznej bazy danych to usługa sieci szkieletowej usług i jest określona za pomocą "wewnętrznej bazy danych id". Używane tooresolve określonej partycji z usługi rozpoznawania nazw hello.|Nie|Nie dotyczy|  
|rz repliki typu|Dotyczy tylko gdy hello wewnętrznej bazy danych to usługa sieci szkieletowej usług i jest określona za pomocą "wewnętrznej bazy danych id". Kontroluje, czy powinien pojawiać się żądania hello toohello podstawowej lub pomocniczej replice partycji. |Nie|Nie dotyczy|    
|rz resolve warunków|Dotyczy tylko gdy hello wewnętrznej bazy danych to usługa sieci szkieletowej usług. Identyfikowanie warunku hello rozmowy telefonicznej tooService sieci szkieletowej wewnętrznej bazy danych ma toobe powtarzany z nowego rozwiązania.|Nie|Nie dotyczy|    
|rz usługi wystąpienie nazwa-|Dotyczy tylko gdy hello wewnętrznej bazy danych to usługa sieci szkieletowej usług. Umożliwia toochange wystąpień usługi w czasie wykonywania. |Nie|Nie dotyczy|    

### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** wewnętrznej bazy danych dla ruchu przychodzącego  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="SetBody"></a>Zestaw treści  
 Użyj hello `set-body` treści wiadomości powitania tooset zasad żądań przychodzących i wychodzących. tooaccess hello treści wiadomości, można użyć hello `context.Request.Body` właściwości lub hello `context.Response.Body`, w zależności od tego, czy zasady hello jest hello sekcji ruchu przychodzącego lub wychodzącego.  
  
> [!IMPORTANT]
>  Należy pamiętać, że domyślnie, gdy uzyskujesz dostęp do hello przy użyciu treści komunikatu `context.Request.Body` lub `context.Response.Body`, oryginalnej wiadomości powitania treści zostaną utracone i musi być ustawione przez zwrócenie treści hello Wstecz w wyrażeniu hello. Treść hello toopreserve zawartości, ustaw hello `preserveContent` parametru zbyt`true` podczas uzyskiwania dostępu do wiadomości powitania. Jeśli `preserveContent` ustawiono zbyt`true` i różnych treści jest zwracany przez wyrażenie hello hello zwrócił treści jest używany.  
>   
>  Należy pamiętać, hello następujące zagadnienia, korzystając z hello `set-body` zasad.  
>   
>  -   Jeśli używasz hello `set-body` tooreturn zasad nowych lub zaktualizowanych treści, nie potrzebujesz tooset `preserveContent` zbyt`true` ponieważ są jawnie dostarczanie hello nowej zawartości w treści.  
> -   Zachowywanie hello treści odpowiedzi w potoku przychodzącego hello sensu ponieważ nie istnieje jeszcze żadnej odpowiedzi.  
> -   Zachowywanie hello zawartości żądania w potoku wychodzącego hello nie sensu, ponieważ Żądanie hello została już wysłana toohello wewnętrznej bazy danych w tym momencie.  
> -   Jeśli zasada ta jest używana, gdy brak treści wiadomości, na przykład w przychodzącej GET, jest zwracany wyjątek.  
  
 Aby uzyskać więcej informacji, zobacz hello `context.Request.Body`, `context.Response.Body`i hello `IMessage` części hello [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables) tabeli.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a>Przykłady  
  
#### <a name="literal-text-example"></a>Przykład literału tekstu  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a>Przykład dostęp do treści hello jako ciąg. Należy pamiętać, że są firma Microsoft zachowuje hello oryginalnego treści żądania, aby firma Microsoft dostęp do niego później w potoku hello.
  
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
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a>Przykład dostęp do treści hello jako JObject. Należy pamiętać, że od czasu firma Microsoft nie są rezerwowania hello oryginalnego treści żądania później w potoku hello spowoduje wyjątek w celu dostępu.  
  
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
  
#### <a name="filter-response-based-on-product"></a>Filtrowanie oparte na produktu odpowiedzi  
 W tym przykładzie pokazano, jak tooperform filtrowanie zawartości przez usunięcie elementów danych z hello odpowiedzi otrzymanych od hello usługi wewnętrznej bazy danych przy użyciu hello `Starter` produktu. Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too34:30. Rozpocznij od 31:50 toosee omówienie [hello ciemny niebo prognozy API](https://developer.forecast.io/) używane na potrzeby tego pokazu.  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
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

### <a name="using-liquid-templates-with-set-body"></a>Za pomocą szablonów płynne o treści zestawu 
Witaj `set-body` zasad może być skonfigurowany toouse hello [płynne](https://shopify.github.io/liquid/basics/introduction/) tworzenia szablonów języka tootransfom hello treści żądania lub odpowiedzi. Może to być bardzo skuteczne, jeśli potrzebujesz toocompletely Przekształć hello format wiadomości.

> [!IMPORTANT]
> Witaj implementacji płynnych używane w hello `set-body` zasada jest skonfigurowana w trybie"C#". Jest to szczególnie ważne podczas wykonywania czynności takich jak filtrowania. Na przykład przy użyciu filtru daty wymaga użycia hello Pascal wielkości liter i C# Data formatowania, np.:
>
> {{body.foo.startDateTime| Data: "yyyyMMddTHH:mm:ddZ"}}

> [!IMPORTANT]
> W kolejności toocorrectly bind tooan treści XML przy użyciu szablonu płynne hello, użyj `set-header` tooeither tooset Content-Type zasad application/xml, tekstu/xml (lub dowolnego typu kończąc + xml); treść kodu JSON, musi być application/json (tekstu/json lub zakończenia dowolnego typu z + json).

#### <a name="convert-json-toosoap-using-a-liquid-template"></a>Konwertuj tooSOAP JSON przy użyciu szablonu płynne
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

#### <a name="tranform-json-using-a-liquid-template"></a>Tranform ciągu JSON przy użyciu szablonu płynne
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|zestaw treści|Element główny. Zawiera treść hello lub wyrażeń, które zwraca treści.|Tak|  

### <a name="properties"></a>Właściwości  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|szablon|Tryb tworzenia szablonów hello toochange używane hello zestaw treści zasad będą uruchamiane w. Obecnie jest hello tylko obsługiwane wartości:<br /><br />-płynne - hello zestaw treści zasad użyje hello płynne tworzenia szablonów aparatu |Nie|płynnych|  

Do uzyskiwania dostępu do informacji na temat hello żądań i odpowiedzi, hello płynne szablonu można powiązać obiektu context tooa hello następujące właściwości: <br />
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



### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="SetHTTPheader"></a>Set — nagłówek HTTP  
 Witaj `set-header` zasad przypisuje wartość tooan istniejących odpowiedzi i/lub nagłówek żądania lub dodaje nowy nagłówek odpowiedzi i/lub żądania.  
  
 Wstawia listę nagłówków HTTP do wiadomości HTTP. Po umieszczeniu w potoku dla ruchu przychodzącego, ta zasada ustawia hello nagłówków HTTP dla żądania hello przekazywany toohello usługi docelowej. Po umieszczeniu w potoku wychodzącego, ta zasada ustawia nagłówki HTTP hello hello odpowiedzi wysyłane klienta toohello bramy.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a>Przykłady  
  
#### <a name="example"></a>Przykład  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Kontekst informacji toohello wewnętrznej bazy danych usługi przekazywania  
 Ten przykład przedstawia, jak zasady tooapply na powitania interfejsu API na poziomie toosupply kontekstu informacji toohello wewnętrznej bazy danych usługi. Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too10:30. Na 12:10 istnieje pokaz wywołanie operacji w portalu dla deweloperów hello umożliwia wyświetlenie zasad hello w miejscu pracy.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|set — nagłówek|Element główny.|Tak|  
|wartość|Określa wartość hello hello nagłówka toobe zestawu. Wiele nagłówków o hello tej samej nazwy dodanie dodatkowych `value` elementów.|Tak|  
  
### <a name="properties"></a>Właściwości  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|istnieje akcja|Określa jaki tootake akcji, gdy nagłówek hello został już określony. Ten atrybut musi mieć jedną z hello następujące wartości.<br /><br /> -- zastępuje hello wartość zastępczą hello istniejący nagłówek.<br />-skip — nie zastępuje istniejącą wartość nagłówka hello.<br />-dołączania - dołącza hello wartość toohello istniejącą wartość nagłówka.<br />-Usunięcie — usuwa hello nagłówek z żądania hello.<br /><br /> Gdy ustawiona zbyt`override` rejestrowanie wiele wpisów z hello sama nazwa wyniki w nagłówku hello jest zestaw zgodnie z tooall zapisów (które zostaną wyświetlone wiele razy); w wyniku hello zostanie ustawiona tylko wartości wyświetlane.|Nie|zastąpienie|  
|name|Określa nazwę zestawu toobe hello nagłówka.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="SetQueryStringParameter"></a>Parametr ciągu zapytania dla zestawu  
 Witaj `set-query-parameter` zasad dodaje wartość zastępuje, lub usuwa żądania parametru ciągu zapytania. Może być używane toopass oczekiwany przez usługi zaplecza hello parametry zapytania, które są opcjonalne lub nigdy nie są obecne w żądaniu hello.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a>Przykłady  
  
#### <a name="example"></a>Przykład  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a>Kontekst informacji toohello wewnętrznej bazy danych usługi przekazywania  
 Ten przykład przedstawia, jak zasady tooapply na powitania interfejsu API na poziomie toosupply kontekstu informacji toohello wewnętrznej bazy danych usługi. Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too10:30. Na 12:10 istnieje pokaz wywołanie operacji w portalu dla deweloperów hello umożliwia wyświetlenie zasad hello w miejscu pracy.  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|Parametr zestawu — zapytania|Element główny.|Tak|  
|wartość|Określa wartość hello zestawu toobe parametru zapytania hello. Wiele parametrów zapytania z hello tej samej nazwy dodanie dodatkowych `value` elementów.|Tak|  
  
### <a name="properties"></a>Właściwości  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|istnieje akcja|Określa jaki tootake akcji, gdy parametr zapytania hello jest już określony. Ten atrybut musi mieć jedną z hello następujące wartości.<br /><br /> -- zastępuje hello wartość zastąpienia istniejącego parametru hello.<br />-skip — nie zastępuje hello istniejącą wartość parametru zapytania.<br />-dołączania - dołącza hello wartość toohello istniejącą wartość parametru zapytania.<br />-Usunięcie — usuwa parametru zapytania hello hello żądania.<br /><br /> Gdy ustawiona zbyt`override` rejestrowanie wiele wpisów z hello sama nazwa powoduje parametru zapytania hello jest zestaw zgodnie z tooall zapisów (które zostaną wyświetlone wiele razy); w wyniku hello zostanie ustawiona tylko wartości wyświetlane.|Nie|zastąpienie|  
|name|Określa nazwę zestawu toobe parametru zapytania hello.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** wewnętrznej bazy danych dla ruchu przychodzącego  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="RewriteURL"></a>Ponowne zapisywanie adresów URL  
 Witaj `rewrite-uri` zasad konwertuje adresie URL żądania w postaci toohello publicznego formularza oczekiwane przez usługę sieci web hello, jak pokazano w hello poniższy przykład.  
  
-   Publiczny adres URL-`http://api.example.com/storenumber/ordernumber`  
  
-   Adres URL żądania —`http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`  
  
 Te zasady można podczas transformacji do formatu adresu URL hello oczekiwanego przez usługę sieci web hello człowieka i/lub przeglądarki przyjaznego adresu URL. Ta zasada musi tylko toobe stosowane, gdy udostępnianie innego formatu adresu URL, takie jak czystą adresów URL, adresy URL RESTful, adresów URL przyjaznych dla użytkownika lub adresów URL przyjaznych dla aparatów wyszukiwania, które są całkowicie strukturalnych adresów URL, które zawiera ciąg zapytania i zamiast tego zawierają tylko hello ścieżka hello zasób (po hello schemat i urząd hello). Często jest to estetycznych, użyteczność lub aparat wyszukiwania (SEO) optymalizacji.  
  
> [!NOTE]
>  Można dodawać tylko za pomocą zasad hello parametrów ciągu zapytania. Nie można dodać dodatkowe szablonu ścieżki parametrów w hello ponowne zapisywanie adresów URL.  

### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a>Przykład  
  
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
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

### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|Identyfikator uri ponownego napisania|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|-------------|  
|szablon|Hello web rzeczywisty adres URL usługi z parametrów ciągu zapytania. Używając wyrażenia wartości całkowitej hello musi być wyrażeniem.|Tak|Nie dotyczy|  
|Kopiuj niedopasowane — parametry|Określa, czy parametry zapytania w hello żądania przychodzącego, jeśli nie znajduje się w oryginalnym szablonie adresu URL hello są dodawane toohello adres URL zdefiniowany przez hello ponownie zapisać szablon|Nie|Wartość true|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** operacja produktu, interfejsu API,  
  
##  <a name="XSLTransform"></a>Przekształcanie XML za pomocą XSLT  
 Witaj `Transform XML using an XSLT` tooXML transformacji XSL w treści żądania lub odpowiedzi hello dotyczą zasady.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
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
  
### <a name="example"></a>Przykład  
  
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
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|Transformacja XSL|Element główny.|Tak|  
|Parametr|Zmienne używane toodefine używane w hello przekształcenia|Nie|  
|XSL: stylesheet|Elemencie głównym arkusza stylów. Wszystkie elementy i atrybuty zdefiniowane w ramach wykonaj standardowe hello [specyfikacji XSLT](http://www.w3.org/TR/xslt)|Tak|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzące, wychodzące  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).  
