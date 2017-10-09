---
title: "zasad buforowania interfejsu API zarządzania aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello buforowanie zasad dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a>Zarządzanie interfejsami API zasad buforowania
W tym temacie znajdują się informacje na następujące zasady usługi API Management hello. Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="CachingPolicies"></a>Buforowanie zasad  
  
-   Zasad buforowania odpowiedzi  
  
    -   [Pobierz z pamięci podręcznej](api-management-caching-policies.md#GetFromCache) — wykonaj pamięci podręcznej wyszukiwania i zwracać prawidłowy odpowiedzi pamięci podręcznej, jeśli jest dostępna.  
  
    -   [Przechowywanie toocache](api-management-caching-policies.md#StoreToCache) — zgodnie z konfiguracji kontroli określonego pamięci podręcznej toohello odpowiedzi pamięci podręcznych.  
  
-   Wartość zasad buforowania  
  
    -   [Pobiera wartość z pamięci podręcznej](#GetFromCacheByKey) -pobrania elementu pamięci podręcznej według klucza.  
  
    -   [Przechowywana wartość w pamięci podręcznej](#StoreToCacheByKey) -przechowywania elementu w pamięci podręcznej hello według klucza.  
  
    -   [Usuń wartość z pamięci podręcznej](#RemoveCacheByKey) -usunięcie elementu w pamięci podręcznej hello według klucza.  
  
##  <a name="GetFromCache"></a>Pobierz z pamięci podręcznej  
 Użyj hello `cache-lookup` pamięci podręcznej zasad tooperform strzałki w górę i zwracać prawidłową odpowiedź buforowana, jeśli jest dostępna. Te zasady mogą być stosowane w przypadkach, gdy odpowiedzi zawartość pozostaje statyczna w danym okresie czasu. Buforowanie odpowiedzi redukuje przepustowość i wymagania dotyczące przetwarzania nałożone na powitania wewnętrznej bazy danych w sieci web serwera i obniża opóźnienia postrzegane przez konsumentów interfejsu API.  
  
> [!NOTE]
>  Ta zasada musi mieć odpowiednią [toocache magazynu](api-management-caching-policies.md#StoreToCache) zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a>Przykłady  
  
#### <a name="example"></a>Przykład  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Przykład za pomocą wyrażeń zasad  
 W tym przykładzie pokazano, jak czas trwania, że dopasowań hello buforowanie odpowiedzi usługi zaplecza hello określony przez hello buforowania odpowiedzi interfejsu API zarządzania tootooconfigure kopii usługi `Cache-Control` dyrektywy. Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too25:25.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|wyszukiwania w pamięci podręcznej|Element główny.|Tak|  
|różnią się w nagłówku|Rozpoczynają buforowanie odpowiedzi na wartość określony nagłówek Accept, Accept-Charset, Accept-Encoding, Accept-Language autoryzacji, oczekiwania, np. Z hosta i If-Match.|Nie|  
|różnią się za--parametru zapytania|Firmy rozpoczynają buforowanie odpowiedzi na wartości parametrów określonego zapytania. Wprowadź jeden lub wiele parametrów. Użyj średnika jako separatora. Jeśli nie jest określona, używane są wszystkie parametry zapytania.|Nie|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|Zezwalaj na prywatny odpowiedzi buforowania|Gdy ustawiona zbyt`true`, umożliwia buforowanie żądań zawierających nagłówek uwierzytelnienia.|Nie|wartość false|  
|typ podrzędny dla buforowania|Ten atrybut musi określać tooone hello następujące wartości.<br /><br /> -none - podrzędne buforowanie jest niedozwolone.<br />-prywatny - podrzędne buforowanie prywatnej jest dozwolone.<br />-publiczny - prywatnych i udostępnionych podrzędne buforowanie jest dozwolone.|Nie|Brak|  
|musi revalidate|Gdy włączone jest buforowanie podrzędne tego atrybutu Włącza lub wyłącza hello `must-revalidate` dyrektywy sterowania pamięci podręcznej w odpowiedzi bramy.|Nie|Wartość true|  
|różnią się przez dewelopera|Ustaw zbyt`true` toocache odpowiedzi na klucz developer.|Nie|wartość false|  
|różnią się przez developer grupy|Ustaw zbyt`true` toocache odpowiedzi dla każdej roli użytkownika.|Nie|wartość false|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** interfejsu API, działania, produktu  
  
##  <a name="StoreToCache"></a>Toocache magazynu  
 Witaj `cache-store` odpowiedzi pamięci podręcznej zasad zgodnie z toohello określić ustawienia pamięci podręcznej. Te zasady mogą być stosowane w przypadkach, gdy odpowiedzi zawartość pozostaje statyczna w danym okresie czasu. Buforowanie odpowiedzi redukuje przepustowość i wymagania dotyczące przetwarzania nałożone na powitania wewnętrznej bazy danych w sieci web serwera i obniża opóźnienia postrzegane przez konsumentów interfejsu API.  
  
> [!NOTE]
>  Ta zasada musi mieć odpowiednią [pobrać z pamięci podręcznej](api-management-caching-policies.md#GetFromCache) zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a>Przykłady  
  
#### <a name="example"></a>Przykład  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a>Przykład za pomocą wyrażeń zasad  
 W tym przykładzie pokazano, jak czas trwania, że dopasowań hello buforowanie odpowiedzi usługi zaplecza hello określony przez hello buforowania odpowiedzi interfejsu API zarządzania tootooconfigure kopii usługi `Cache-Control` dyrektywy. Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too25:25.  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 Aby uzyskać więcej informacji, zobacz [wyrażenie zasad](api-management-policy-expressions.md) i [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables).  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|magazynu pamięci podręcznej|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|Czas trwania|Czas wygaśnięcia elementu hello buforowane wpisów, określona w sekundach.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** ruchu wychodzącego  
  
-   **Zakresy zasad:** interfejsu API, działania, produktu  
  
##  <a name="GetFromCacheByKey"></a>Pobiera wartość z pamięci podręcznej  
 Użyj hello `cache-lookup-value` tooperform zasad przez klucz pamięci podręcznej wyszukiwania i zwraca wartość w pamięci podręcznej. klucz Hello może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.  
  
> [!NOTE]
>  Ta zasada musi mieć odpowiednią [przechowywana wartość w pamięci podręcznej](#StoreToCacheByKey) zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a>Przykład  
 Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [niestandardowych buforowanie w usłudze Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|wartość w pamięci podręcznej wyszukiwania|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|Wartość domyślna|Wartość, która zostanie przypisana zmienna toohello Jeśli wyszukiwanie klucza pamięci podręcznej hello spowodowała nie trafienia. Jeśli ten atrybut nie jest określony, `null` jest przypisany.|Nie|`null`|  
|key|Wartość klucza toouse w hello wyszukiwania w pamięci podręcznej.|Tak|Nie dotyczy|  
|Nazwa zmiennej|Nazwa hello [zmiennej kontekstu](api-management-policy-expressions.md#ContextVariables) hello przeszukiwać wartość zostanie przypisana do użytkownika, jeśli wyszukiwanie powiedzie się. Jeśli wyszukiwanie powoduje Chybienie, zmienna hello zostaną przypisane wartości hello hello `default-value` atrybutu lub `null`, jeśli hello `default-value` atrybut nie jest określony.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** globalnych, interfejsu API, działania, produktu  
  
##  <a name="StoreToCacheByKey"></a>Wartość magazynu w pamięci podręcznej  
 Witaj `cache-store-value` wykonuje magazynu pamięci podręcznej według klucza. klucz Hello może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.  
  
> [!NOTE]
>  Ta zasada musi mieć odpowiednią [pobrać wartości z pamięci podręcznej](#GetFromCacheByKey) zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a>Przykład  
 Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [niestandardowych buforowanie w usłudze Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|wartość w przypadku magazynu pamięci podręcznej|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|Czas trwania|Wartość będą buforowane na powitania podane wartości czasu trwania, określona w sekundach.|Tak|Nie dotyczy|  
|key|Wartość klucza hello pamięci podręcznej będą przechowywane w obszarze.|Tak|Nie dotyczy|  
|wartość|Witaj toobe wartość w pamięci podręcznej.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** globalnych, interfejsu API, działania, produktu  
  
###  <a name="RemoveCacheByKey"></a>Usuń wartość z pamięci podręcznej  
 Witaj `cache-remove-value` usuwa element pamięci podręcznej identyfikowane za pomocą klucza. klucz Hello może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad.  
  
#### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a>Przykład  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|remove wartość w pamięci podręcznej|Element główny.|Tak|  
  
#### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|key|klucz Hello hello buforowane wcześniej usuniętych z pamięci podręcznej hello toobe wartość.|Tak|Nie dotyczy|  
  
#### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .  
  
-   **Sekcje zasad:** przychodzący, wychodzący wewnętrznej bazy danych, na błąd  
  
-   **Zakresy zasad:** globalnych, interfejsu API, działania, produktu  
  

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).  