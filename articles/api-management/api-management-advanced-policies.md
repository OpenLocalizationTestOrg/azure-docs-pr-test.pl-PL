---
title: "aaaAzure zaawansowane zasady zarządzania interfejsu API | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello zaawansowane zasady dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a>Zarządzanie interfejsami API zaawansowane zasady
W tym temacie znajdują się informacje na następujące zasady usługi API Management hello. Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AdvancedPolicies"></a>Zaawansowane zasady  
  
-   [Przepływ kontroli](api-management-advanced-policies.md#choose) — warunkowo stosuje deklaracji zasad, na podstawie wyników hello oceny hello Boolean [wyrażenia](api-management-policy-expressions.md).  
  
-   [Przekazanie żądania](#ForwardRequest) -przekazuje hello żądania toohello wewnętrznej bazy danych usługi.

-   [Ogranicz współbieżności](#LimitConcurrency) — uniemożliwia ujęta zasady wykonania przez więcej niż hello określonej liczby żądań w czasie.
  
-   [Zaloguj się tooEvent Centrum](#log-to-eventhub) — wysyła wiadomości powitania określony format tooan Centrum zdarzeń zdefiniowanych przez podmiot rejestratora. 

-   [Mock odpowiedzi](#mock-response) -przerwań potoku wykonywania i zwraca odpowiedź mocked bezpośrednio toohello wywołującego.
  
-   [Spróbuj ponownie](#Retry) -ponownych prób wykonania hello ujęta deklaracji zasad, jeśli i dopóki nie zostanie spełniony warunek hello. Wykonanie jest powtarzany w hello w określonych odstępach czasu i zapasowej toohello określona liczba ponownych prób.  
  
-   [Odpowiedź zwrócona](#ReturnResponse) -przerwań potoku wykonywania i zwraca hello określona odpowiedź bezpośrednio toohello wywołującego. 
  
-   [Wyślij żądanie jednokierunkowej](#SendOneWayRequest) — wysyła toohello żądania określony adres URL bez oczekiwania na odpowiedź.  
  
-   [Wyślij żądanie](#SendRequest) — wysyła toohello żądania określonego adresu URL.  

-   [Ustaw serwer proxy HTTP](#SetHttpProxy) — pozwala żądań tooroute przekazywane za pośrednictwem serwera proxy HTTP.  

-   [Ustawia metodę żądania](#SetRequestMethod) — pozwala toochange metody hello HTTP dla żądania.  
  
-   [Ustaw kod stanu](#SetStatus) -toohello kod stanu hello HTTP zmiany określona wartość.  
  
-   [Ustaw zmienną](api-management-advanced-policies.md#set-variable) -będzie się powtarzał wartości w nazwanym [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej nowsze dostępu.  

-   [Śledzenia](#Trace) -dodaje ciąg do hello [inspektora interfejsu API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) danych wyjściowych.  
  
-   [Poczekaj](#Wait) -oczekuje dla ujęta [żądanie wysłania](api-management-advanced-policies.md#SendRequest), [pobrać wartości z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey), lub [sterowania przepływem](api-management-advanced-policies.md#choose) toocomplete zasad przed kontynuowaniem.  
  
##  <a name="choose"></a>Przepływ sterowania  
 Witaj `choose` zasad stosuje objętego zasady oparte na powitania wynik oceny wyrażeń logicznych, podobne tooan if to inaczej lub przełącznika instrukcje tworzenia w języku programowania.  
  
###  <a name="ChoosePolicyStatement"></a>Deklaracja zasad  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 Witaj zasady kontroli przepływu musi zawierać co najmniej jeden `<when/>` elementu. Witaj `<otherwise/>` element jest opcjonalny. Warunki w `<when/>` elementy są oceniane w kolejności ich wyglądu w ramach zasad hello. Instrukcji zasad ujętą w nawiasy klamrowe hello najpierw `<when/>` element z równą atrybut warunku `true` zostaną zastosowane. Zasady ujętą w nawiasy klamrowe hello `<otherwise/>` elementu, jeśli jest obecny, zostaną zastosowane, jeśli wszystkie z hello `<when/>` są atrybuty warunku elementu `false`.  
  
### <a name="examples"></a>Przykłady  
  
####  <a name="ChooseExample"></a>Przykład  
 Witaj poniższym przykładzie pokazano [set-variable](api-management-advanced-policies.md#set-variable) zasad i dwie zasady przepływu sterowania.  
  
 Hello Ustaw zasady zmiennej jest hello sekcji ruchu przychodzącego i tworzy `isMobile` logiczna [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej, która ma wartość tootrue, jeśli hello `User-Agent` żądania nagłówek zawiera tekst hello `iPad` lub `iPhone`.  
  
 Hello pierwszy kontroli przepływu zasad jest również w hello sekcji ruchu przychodzącego i warunkowo stosuje się jeden z dwóch [ustawić parametr ciągu zapytania](api-management-transformation-policies.md#SetQueryStringParameter) zasad w zależności od wartości hello hello `isMobile` zmiennej kontekstu.  
  
 drugie zasady przepływu sterowania Hello znajduje się w sekcji wychodzącego hello i warunkowo stosuje hello [tooJSON przekonwertować XML](api-management-transformation-policies.md#ConvertXMLtoJSON) zasad podczas `isMobile` ustawiono zbyt`true`.  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a>Przykład  
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
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|Wybierz pozycję|Element główny.|Tak|  
|Kiedy|Witaj toouse warunek dla hello `if` lub `ifelse` części hello `choose` zasad. Jeśli hello `choose` zasad ma wiele `when` sekcje są oceniane po kolei. Raz hello `condition` z o tym, kiedy element ocenia zbyt`true`, nie musisz `when` oceny warunków.|Tak|  
|w przeciwnym razie|Zawiera toobe fragment zasad hello używane, jeśli żaden z hello `when` warunki oceny zbyt`true`.|Nie|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|  
|---------------|-----------------|--------------|  
|warunek = "wyrażenie warunkowe & #124; Wartość logiczna stała"|wyrażenie warunkowe Hello lub tooevaluated stałej, gdy hello zawierający `when` oceny deklaracji zasad.|Tak|  
  
###  <a name="ChooseUsage"></a>Użycie  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  
  
##  <a name="ForwardRequest"></a>Przekazanie żądania  
 Witaj `forward-request` zasad przekazuje hello przychodzącego żądania toohello usługi wewnętrznej bazy danych określony w żądaniu hello [kontekstu](api-management-policy-expressions.md#ContextVariables). Witaj adres URL usługi wewnętrznej bazy danych jest określona w hello interfejsu API [ustawienia](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) i można zmieniać za pomocą hello [Ustaw usługę zaplecza](api-management-transformation-policies.md) zasad.  
  
> [!NOTE]
>  Usunięcie tego wyników zasad w żądaniu hello nie przesyłane dalej toohello zasady hello i usługi wewnętrznej bazy danych w sekcji wychodzącego hello są oceniane natychmiast na pomyślne zakończenie zasad hello w hello hello ruchu przychodzącego sekcji.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a>Przykłady  
  
#### <a name="example"></a>Przykład  
 Witaj następujące zasady na poziomie interfejsu API przekazuje wszystkie żądania toohello usługi wewnętrznej bazy danych z limit czasu 60 sekund.  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Przykład  
 Zasady na poziomie tej operacji używa hello `base` elementu tooinherit hello zaplecza zasady z poziomu zakresu nadrzędnego interfejsu API hello.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Przykład  
 Tej zasady na poziomie operacji jawnie przekazuje wszystkie usługi wewnętrznej bazy danych z limitem czasu 120 żądań toohello i nie dziedziczy nadrzędnego hello zasad poziomu zaplecza interfejsu API.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a>Przykład  
 Zasady na poziomie tej operacji nie przekazuje żądania toohello usługi wewnętrznej bazy danych.  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|żądanie do przodu|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|-------------|  
|limit czasu = "int"|Witaj — interwał limitu czasu w sekundach przed hello wywołania toohello wewnętrznej bazy danych usługi nie powiedzie się.|Nie|Brak limitu czasu|  
|Wykonaj przekierowania = "true & #124; false"|Określa, czy przekierowań z usługi zaplecza hello są następuje hello bramy lub zwrócił toohello wywołującego.|Nie|wartość false|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** wewnętrznej bazy danych  
  
-   **Zakresy zasad:** wszystkich zakresów  
  
##  <a name="LimitConcurrency"></a>Limit współbieżności  
 Witaj `limit-concurrency` zasad uniemożliwia objętego zasad wykonywania przez więcej niż hello określonej liczby żądań w danym momencie. Po przekroczeniu progu hello, nowe żądania są dodawane kolejki tooa do hello kolejki maksymalną długość. Po wyczerpania kolejki nowe żądania nie powiedzie się natychmiast.
  
###  <a name="LimitConcurrencyStatement"></a>Deklaracja zasad  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a>Przykłady  
  
####  <a name="ChooseExample"></a>Przykład  
 Witaj poniższym przykładzie pokazano, jak toolimit liczba żądań dalej tooa wewnętrznej bazy danych na podstawie wartości hello zmiennej kontekstu.
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|    
|limit współbieżności|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|--------------|  
|key|Ciąg. Wyrażenie jest dozwolone. Określa zakres współbieżności hello. Może być współużytkowane przez wiele zasad.|Tak|Nie dotyczy|  
|Maksymalna liczba|Liczba całkowita. Określa maksymalną liczbę żądań, które mogą tooenter hello zasad.|Tak|Nie dotyczy|  
|timeout|Liczba całkowita. Wyrażenie jest dozwolone. Określa hello liczbę sekund, żądanie powinno czekać tooenter zakresu przed niepowodzeniem z "403 zbyt wiele żądań"|Nie|Infinity|  
|Maksymalna kolejki|Liczba całkowita. Wyrażenie jest dozwolone. Określa hello kolejki maksymalną długość. Żądań przychodzących w trakcie tooenter ta zasada zostanie zakończone z "403 zbyt wiele żądań" natychmiast po wyczerpaniu hello kolejki.|Nie|Infinity|  
  
###  <a name="ChooseUsage"></a>Użycie  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  

##  <a name="log-to-eventhub"></a>Dziennik tooEvent Centrum  
 Witaj `log-to-eventhub` zasad wysyła wiadomości powitania określony format tooan Centrum zdarzeń zdefiniowanych przez podmiot rejestratora. Jak jego nazwa wskazuje, hello zasad służy do zapisywania wybrane informacje kontekstu żądania lub odpowiedzi do analizy w trybie online lub offline.  
  
> [!NOTE]
>  Przewodnik krok po kroku dotyczące konfigurowania Centrum zdarzeń i rejestrowania zdarzeń dla [jak toolog zdarzenia interfejsu API zarządzania za pomocą usługi Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a>Przykład  
 Dowolny ciąg może służyć jako toobe wartość hello rejestrowane w usłudze Event Hubs. W tym przykładzie hello Data i godzina wdrożenia, nazwę usługi, identyfikator żądania adresu ip i nazwy operacji dla wszystkich połączeń przychodzących są Centrum zdarzeń zarejestrowanych toohello rejestratora zarejestrowany hello `contoso-logger` identyfikator.  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|dziennika do Centrum eventhub|Element główny. wartość Hello tego elementu jest Centrum zdarzeń tooyour toolog ciąg hello.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|  
|---------------|-----------------|--------------|  
|identyfikator rejestratora|Identyfikator Hello hello rejestratora zarejestrowana przy użyciu usługi API Management.|Tak|  
|Identyfikator partycji|Określa indeks hello partycji hello wysyłania wiadomości.|Opcjonalny. Ten atrybut nie może być używany, jeśli `partition-key` jest używany.|  
|Klucz partycji|Określa wartość hello używany do przypisania partycji podczas wysyłania wiadomości.|Opcjonalny. Ten atrybut nie może być używany, jeśli `partition-id` jest używany.|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  

##  <a name="mock-response"></a>Zasymulować odpowiedzi  
Witaj `mock-response`, jako nazwa hello oznacza, że jest używana toomock interfejsów API i operacji. Przerywa wykonywanie normalny potok, a zwraca obiekt wywołujący toohello mocked odpowiedzi. zasady Hello zawsze próbuje odpowiedzi tooreturn wierności najwyższy. Preferuje go przykłady zawartości odpowiedzi, gdy dostępne. Generuje on przykładowe odpowiedzi ze schematów, gdy znajdują się schematów i przykłady nie. W przypadku znalezienia przykłady ani schematów odpowiedzi z zawartością, nie są zwracane.
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a>Przykłady  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|makiety odpowiedzi|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|--------------|  
|Kod stanu|Określa kod stanu odpowiedzi i jest używane tooselect odpowiedni przykład lub schematu.|Nie|200|  
|Typ zawartości|Określa `Content-Type` wartość nagłówka odpowiedzi i jest używane tooselect odpowiedni przykład lub schematu.|Nie|Brak|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzące, wychodzące, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów

##  <a name="Retry"></a>Spróbuj ponownie  
 Witaj `retry` zasad jego zasad podrzędnych jest wykonywana raz i ponowi próbę ich realizacji do ponawiania hello `condition` staje się `false` lub ponów próbę `count` jest wyczerpana.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a>Przykład  
 W hello następujące przykładowe żądanie forewarding próba zostanie ponowiona się tooten użyciu algorytm wykładnicze ponów próbę. Ponieważ `first-fast-retry` ustawiono toofalse, Algorytm ponownych prób exponsntial toohello podmiotu są wszystkie ponownych prób.  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|retry|Element główny. Może zawierać inne zasady jako jego elementy podrzędne.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|-------------|  
|Warunek|Logiczna literał lub [wyrażenie](api-management-policy-expressions.md) określenie ponownych prób powinna zostać zatrzymana (`false`) lub nadal (`true`).|Tak|Nie dotyczy|  
|Liczba|Liczba dodatnia określająca maksymalną liczbę ponownych prób tooattempt hello.|Tak|Nie dotyczy|  
|interval|Liczba dodatnia, w sekundach, określając hello interwału oczekiwania między hello ponownych prób.|Tak|Nie dotyczy|  
|Maksymalny interwał|Liczba dodatnia, w sekundach, określając hello oczekiwania maksymalny interwał hello ponownych prób. Jest używana tooimplement algorytm wykładnicze ponów próbę.|Nie|Nie dotyczy|  
|delta|Liczba dodatnia, w sekundach, określając przyrostu interwału oczekiwania hello. Jest używane tooimplement hello liniowej i wykładniczej ponownych prób algorytmów.|Nie|Nie dotyczy|  
|pierwszy ponownej próby fast|Jeśli ustawiona zbyt `true` , hello pierwszy ponowienia próby jest wykonywane bezpośrednio.|Nie|`false`|  
  
> [!NOTE]
>  Gdy tylko hello `interval` jest określony, **stałej** Interwał ponownych prób są wykonywane.  
>  Gdy tylko hello `interval` i `delta` są określone, **liniowej** interwału ponawiania algorytm jest używany, gdy czas oczekiwania między kolejnymi próbami jest obliczeniowej hello zgodnie z następującej formuły — `interval + (count - 1)*delta`.  
>  Gdy hello `interval`, `max-interval` i `delta` są określone, **wykładniczej** interwału ponawiania algorytm jest stosowana, gdy czas oczekiwania hello między kolejnymi próbami hello rośnie wykładniczo od wartości hello `interval`wartość toohello `max-interval` zgodnie z następujących toohello forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) . Należy pamiętać, że ograniczenia użycia zasad podrzędne będą dziedziczone przez te zasady.  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  
  
##  <a name="ReturnResponse"></a>Odpowiedź zwrócona  
 Witaj `return-response` zasad przerwanie wykonywania potoku i zwraca domyślnych lub niestandardowych odpowiedzi toohello wywołującego. Domyślny jest `200 OK` nie jednostki. Za pomocą instrukcji kontekstu zmiennej lub zasad można określić niestandardową odpowiedź. Zarówno udostępniane hello zawartych w zmiennej kontekstu hello modyfikacja odpowiedzi przez deklaracji zasad hello przed zwróceniem toohello wywołującego.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a>Przykład  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|odpowiedź Return|Element główny.|Tak|  
|set — nagłówek|A [nagłówka set](api-management-transformation-policies.md#SetHTTPheader) deklaracji zasad.|Nie|  
|zestaw treści|A [treści zestaw](api-management-transformation-policies.md#SetBody) deklaracji zasad.|Nie|  
|Ustaw stan|A [Ustaw stan](api-management-advanced-policies.md#SetStatus) deklaracji zasad.|Nie|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|  
|---------------|-----------------|--------------|  
|Nazwa zmiennej odpowiedzi|Witaj nazwa zmiennej kontekstu hello odwołuje się do z, na przykład nadrzędnym [żądanie wysłania](api-management-advanced-policies.md#SendRequest) zasad i zawierający `Response` obiektu|Opcjonalny.|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  
  
##  <a name="SendOneWayRequest"></a>Wyślij żądanie jednokierunkowej  
 Witaj `send-one-way-request` zasad wysyła żądanie hello podany adres URL określony toohello bez oczekiwania na odpowiedź.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a>Przykład  
 Ta zasada przykładowych pokazano przykład przy użyciu hello `send-one-way-request` zasad toosend komunikat tooa Slack pokoju rozmów Jeśli hello kod odpowiedzi HTTP jest większa niż lub równa too500. Aby uzyskać więcej informacji na ten przykład, zobacz [za pomocą usług zewnętrznych z usługi Azure API Management hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|sposób żądania, Wyślij co w-|Element główny.|Tak|  
|adres URL|adres URL Hello hello żądania.|Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.|  
|— Metoda|Metoda HTTP dla żądania hello Hello.|Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.|  
|nagłówek|Nagłówek żądania. Użyj wielu elementów nagłówka dla wielu nagłówków żądania.|Nie|  
|Treści|Witaj treści żądania.|Nie|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|-------------|  
|tryb = "string"|Określa, czy jest to nowe żądanie lub kopię hello bieżącego żądania. W trybie wychodzących tryb = kopiowania nie inicjuje hello treści żądania.|Nie|Nowy|  
|name|Określa nazwę hello hello nagłówka toobe zestawu.|Tak|Nie dotyczy|  
|istnieje akcja|Określa jaki tootake akcji, gdy nagłówek hello został już określony. Ten atrybut musi mieć jedną z hello następujące wartości.<br /><br /> -- zastępuje hello wartość zastępczą hello istniejący nagłówek.<br />-skip — nie zastępuje istniejącą wartość nagłówka hello.<br />-dołączania - dołącza hello wartość toohello istniejącą wartość nagłówka.<br />-Usunięcie — usuwa hello nagłówek z żądania hello.<br /><br /> Gdy ustawiona zbyt`override` rejestrowanie wiele wpisów z hello sama nazwa wyniki w nagłówku hello jest zestaw zgodnie z tooall zapisów (które zostaną wyświetlone wiele razy); w wyniku hello zostanie ustawiona tylko wartości wyświetlane.|Nie|zastąpienie|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  
  
##  <a name="SendRequest"></a>Wyślij żądanie  
 Witaj `send-request` zasad wysyła żądanie hello podane toohello określony adres URL, nie jest już oczekujące niż hello ustawić wartość limitu czasu.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a>Przykład  
 Ten przykład przedstawia jednokierunkowej tooverify token odwołania z serwera autoryzacji. Aby uzyskać więcej informacji na ten przykład, zobacz [za pomocą usług zewnętrznych z usługi Azure API Management hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|Żądanie wysłania|Element główny.|Tak|  
|adres URL|adres URL Hello hello żądania.|Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.|  
|— Metoda|Metoda HTTP dla żądania hello Hello.|Jeśli nie trybu = kopiowania; tak, w przeciwnym razie wartość.|  
|nagłówek|Nagłówek żądania. Użyj wielu elementów nagłówka dla wielu nagłówków żądania.|Nie|  
|Treści|Witaj treści żądania.|Nie|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|-------------|  
|tryb = "string"|Określa, czy jest to nowe żądanie lub kopię hello bieżącego żądania. W trybie wychodzących tryb = kopiowania nie inicjuje hello treści żądania.|Nie|Nowy|  
|Nazwa zmiennej odpowiedzi = "string"|Jeśli nie istnieje `context.Response` jest używany.|Nie|Nie dotyczy|  
|limit czasu = "int"|Witaj — interwał limitu czasu w sekundach przed wywołaniem hello toohello adres URL nie powiedzie się.|Nie|60|  
|Ignoruj błąd|Jeśli true, a hello żądania powoduje błąd:<br /><br /> — Jeśli nazwa zmiennej odpowiedzi został określony, będzie zawierać wartości null.<br />— Jeśli nie określono odpowiedzi zmienna nazwy, kontekstu. Żądanie nie zostanie zaktualizowany.|Nie|wartość false|  
|name|Określa nazwę hello hello nagłówka toobe zestawu.|Tak|Nie dotyczy|  
|istnieje akcja|Określa jaki tootake akcji, gdy nagłówek hello został już określony. Ten atrybut musi mieć jedną z hello następujące wartości.<br /><br /> -- zastępuje hello wartość zastępczą hello istniejący nagłówek.<br />-skip — nie zastępuje istniejącą wartość nagłówka hello.<br />-dołączania - dołącza hello wartość toohello istniejącą wartość nagłówka.<br />-Usunięcie — usuwa hello nagłówek z żądania hello.<br /><br /> Gdy ustawiona zbyt`override` rejestrowanie wiele wpisów z hello sama nazwa wyniki w nagłówku hello jest zestaw zgodnie z tooall zapisów (które zostaną wyświetlone wiele razy); w wyniku hello zostanie ustawiona tylko wartości wyświetlane.|Nie|zastąpienie|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  
  
##  <a name="SetHttpProxy"></a>Serwer proxy HTTP zestawu  
 Witaj `proxy` zasad umożliwia tooroute toobackends przekazywania żądań za pośrednictwem serwera proxy HTTP. HTTP (a nie HTTPS) jest obsługiwana między hello bramy i serwera proxy hello. Podstawowe i tylko z uwierzytelniania NTLM.
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a>Przykład  
Należy zwrócić uwagę użycie hello [właściwości](api-management-howto-properties.md) jako wartości tooavoid nazwy użytkownika i hasła hello poufne informacje są przechowywane w dokumencie zasady hello.  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|Serwer proxy|Element główny|Tak|  

### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|-------------|  
|adres URL = "string"|Adres URL serwera proxy w formie hello http://host:port.|Tak|Nie dotyczy|  
|Nazwa użytkownika = "string"|Używany do uwierzytelniania przy użyciu serwera proxy hello toobe nazwy użytkownika.|Nie|Nie dotyczy|  
|hasło = "string"|Używany do uwierzytelniania przy użyciu serwera proxy hello toobe hasła.|Nie|Nie dotyczy|  

### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** wszystkich zakresów  

##  <a name="SetRequestMethod"></a>Set, Metoda żądania  
 Witaj `set-method` zasad umożliwia toochange metoda żądania hello HTTP dla żądania.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a>Przykład  
 Przykładowe zasady używa hello `set-method` zasad przedstawiono przykład wysyłanie komunikatu tooa Slack pokoju rozmów, jeśli kod odpowiedzi HTTP hello jest większa niż lub równe too500. Aby uzyskać więcej informacji na ten przykład, zobacz [za pomocą usług zewnętrznych z usługi Azure API Management hello](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).  
  
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
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|set, metoda|Element główny. wartość Hello elementu hello określa metodę HTTP hello.|Tak|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  
  
##  <a name="SetStatus"></a>Kod stanu zestawu  
 Witaj `set-status` zasad zestawy hello HTTP status kodu toohello określona wartość.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a>Przykład  
 W tym przykładzie pokazano sposób tooreturn odpowiedzi 401, jeśli token autoryzacji hello jest nieprawidłowy. Aby uzyskać więcej informacji, zobacz [za pomocą usług zewnętrznych z hello usługi Zarządzanie interfejsami API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)  
  
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
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|Ustaw stan|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|-------------|  
|Kod = "int"|tooreturn kod stanu Hello HTTP.|Tak|Nie dotyczy|  
|Przyczyna = "string"|Opis Przyczyna hello zwróciło kod stanu hello.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  

##  <a name="set-variable"></a>Ustaw zmienną  
 Witaj `set-variable` deklaruje zasad [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej i przypisuje go za pośrednictwem określoną wartość [wyrażenie](api-management-policy-expressions.md) lub literałem ciągu. Jeśli wyrażenie hello zawiera właściwość literal, zostanie on przekonwertowany typ string i hello tooa hello wartości będzie `System.String`.  
  
###  <a name="set-variablePolicyStatement"></a>Deklaracja zasad  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <a name="set-variableExample"></a>Przykład  
 Witaj poniższym przykładzie pokazano Ustaw zasady zmiennej w hello ruchu przychodzącego sekcji. Ta zasada zmiennej zestaw tworzy `isMobile` logiczna [kontekstu](api-management-policy-expressions.md#ContextVariables) zmiennej, która ma wartość tootrue, jeśli hello `User-Agent` hello tekst zawiera nagłówek żądania `iPad` lub `iPhone`.  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|Ustaw zmienną|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|  
|---------------|-----------------|--------------|  
|name|Nazwa Hello hello zmiennej.|Tak|  
|wartość|wartość Hello hello zmiennej. Może to być wyrażenie lub ciągiem literałowym.|Tak|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  
  
###  <a name="set-variableAllowedTypes"></a>Dozwolonymi typami  
 Wyrażenia używane w hello `set-variable` zasad musi zwracać jedną z hello następujące typy podstawowe.  
  
-   System.Boolean  
  
-   System.SByte  
  
-   System.Byte  
  
-   System.UInt16  
  
-   System.UInt32  
  
-   System.UInt64  
  
-   System.Int16  
  
-   System.Int32  
  
-   System.Int64  
  
-   System.Decimal  
  
-   System.Single  
  
-   System.Double  
  
-   System.Guid  
  
-   System.String  
  
-   System.Char  
  
-   System.DateTime  
  
-   Obiekt System.TimeSpan  
  
-   System.Byte?  
  
-   System.UInt16?  
  
-   System.UInt32?  
  
-   System.UInt64?  
  
-   System.Int16?  
  
-   System.Int32?  
  
-   System.Int64?  
  
-   System.Decimal?  
  
-   System.Single?  
  
-   System.Double?  
  
-   System.Guid?  
  
-   System.String?  
  
-   System.Char?  
  
-   System.DateTime?  

##  <a name="Trace"></a>Śledzenia  
 Witaj `trace` zasad dodaje ciąg do hello [inspektora interfejsu API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) danych wyjściowych. Witaj zasad będą wykonywane tylko gdy śledzenie jest wyzwalane, tj. `Ocp-Apim-Trace` nagłówek żądania jest obecny i ustaw zbyt`true` i `Ocp-Apim-Subscription-Key` nagłówek żądania jest obecny i ma prawidłowy klucz skojarzony z kontem administratora hello.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|śledzenia|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|-------------|  
|Źródło|Przeglądarka śledzenia toohello znaczący literału ciągu i Określanie źródła hello wiadomość hello.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** wszystkich zakresów  
  
##  <a name="Wait"></a>Oczekiwania  
 Witaj `wait` zasad wykonuje jego zasadami bezpośrednio podrzędne równolegle i czeka na wszystkich lub jednego z jego toocomplete zasad bezpośrednio podrzędne przed zakończeniem działania. Hello oczekiwania zasad może mieć jako jego zasadami bezpośrednio podrzędne [żądanie wysłania](api-management-advanced-policies.md#SendRequest), [pobrać wartości z pamięci podręcznej](api-management-caching-policies.md#GetFromCacheByKey), i [sterowania przepływem](api-management-advanced-policies.md#choose) zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a>Przykład  
 W hello poniższy przykład występują dwa `choose` zasad jako zasady bezpośrednio podrzędne hello `wait` zasad. Każdy z tych `choose` zasad wykonywane równolegle. Każdy `choose` zasad prób tooretrieve wartość w pamięci podręcznej. W przypadku Chybienie pamięci podręcznej usługi wewnętrznej bazy danych jest nazywany tooprovide hello wartość. W tym hello przykład `wait` zasad nie zostanie zakończone do czasu ukończenia wszystkich swoich zasad bezpośrednio podrzędne, ponieważ hello `for` zbyt ustawiono atrybut`all`.   W tym przykład hello kontekstu zmiennych (`execute-branch-one`, `value-one`, `execute-branch-two`, i `value-two`) są deklarowane jako poza zakres hello ten przykład zasad.  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|oczekiwania|Element główny. Może zawierać jako elementy podrzędne tylko `send-request`, `cache-lookup-value`, i `choose` zasad.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Atrybut|Opis|Wymagane|Domyślne|  
|---------------|-----------------|--------------|-------------|  
|dla|Określa, czy hello `wait` zasad czeka na wszystkich toobe zasad bezpośrednio podrzędne ukończona lub jest tylko jeden. Dozwolone wartości to:<br /><br /> -   `all`-Poczekaj, aż wszystkie toocomplete zasad bezpośrednio podrzędne<br />-żadnego - poczekaj, aż wszystkie toocomplete zasad bezpośrednio podrzędne. Po zakończeniu pierwszej zasady bezpośrednio podrzędne hello hello `wait` kończy zasad i wykonywania innych zasad bezpośrednio podrzędne zostanie zakończony.|Nie|Wszystkie|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych  
  
-   **Zakresy zasad:**wszystkich zakresów  
  
## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, Praca z zasad Zobacz:
-   [Zasady w usłudze API Management](api-management-howto-policies.md) 
-   [Wyrażenia zasad](api-management-policy-expressions.md)
