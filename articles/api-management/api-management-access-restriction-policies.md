---
title: "zasady ograniczeń dostępu do interfejsu API zarządzania aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat zasad ograniczeń dostępu hello dostępne do użycia w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a>Zasady ograniczeń dostępu do interfejsu API zarządzania
W tym temacie znajdują się informacje na następujące zasady usługi API Management hello. Aby uzyskać informacje dotyczące dodawania i konfigurowania zasad, zobacz [zasad w usłudze API Management](http://go.microsoft.com/fwlink/?LinkID=398186).  
  
##  <a name="AccessRestrictionPolicies"></a>Zasady ograniczeń dostępu  
  
-   [Nagłówek HTTP wyboru](api-management-access-restriction-policies.md#CheckHTTPHeader) — wymusza istnienia i/lub wartość nagłówka HTTP.  
  
-   [Limit szybkości wywołanie przez subskrypcji](api-management-access-restriction-policies.md#LimitCallRate) — użycie uniemożliwia API wzrósł poprzez ograniczenie wywołań szybkości, na podstawie subskrypcji na.  
  
-   [Limit szybkości wywołanie przez klucz](#LimitCallRateByKey) — użycie uniemożliwia API wzrósł ograniczając szybkość połączenia, na podstawie na klucz.  
  
-   [Ograniczenia adresów IP wywołującego](api-management-access-restriction-policies.md#RestrictCallerIPs) -wywołania filtrów (umożliwia/nie zezwala na) z określonych adresów IP i/lub zakresów adresów.  
  
-   [Przydział użycia zestawu subskrypcji](api-management-access-restriction-policies.md#SetUsageQuota) — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie na subskrypcję.  
  
-   [Przydział użycia zestawu przez klucz](#SetUsageQuotaByKey) — umożliwia tooenforce odnawialnymi lub okres istnienia połączenia woluminu i/lub przepustowości przydziału na podstawie według klucza.  
  
-   [Sprawdź poprawność JWT](api-management-access-restriction-policies.md#ValidateJWT) — wymusza istnienia i ważności wyodrębniony z określonego nagłówka HTTP lub parametr zapytania określony token JWT.  
  
##  <a name="CheckHTTPHeader"></a>Sprawdź nagłówka HTTP  
 Użyj hello `check-header` tooenforce zasady, czy żądanie ma określonego nagłówka HTTP. Opcjonalnie można sprawdzić toosee, jeśli nagłówek hello ma określoną wartość lub sprawdź, czy zakres wartości dozwolonych. W przypadku niepowodzenia sprawdzania hello zasad hello kończy przetwarzanie żądań i zwraca hello komunikat stanu HTTP kodu i błąd określone przez zasady hello.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a>Przykład  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|Sprawdź — nagłówek|Element główny.|Tak|  
|wartość|Dozwolone wartości nagłówka HTTP. Jeśli wiele elementów wartości są określone, wyboru hello jest uznawany sukcesu, jeśli jedno hello wartości są zgodne.|Nie|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|nie powiodło się wyboru komunikatów o błędach|Błąd tooreturn wiadomość w treści odpowiedzi hello HTTP, jeśli nagłówek hello nie istnieje lub ma nieprawidłową wartość. Ta wiadomość musi mieć żadnych znaków specjalnych prawidłowo wpisywany.|Tak|Nie dotyczy|  
|nie powiodło się wyboru httpcode|Tooreturn kod stanu HTTP, jeśli nagłówek hello nie istnieje lub ma nieprawidłową wartość.|Tak|Nie dotyczy|  
|Nazwa nagłówka|Nazwa Hello hello toocheck nagłówka HTTP.|Tak|Nie dotyczy|  
|Ignoruj case|Można ustawić tooTrue, lub FAŁSZ. Jeśli zestaw tooTrue w wielkość liter jest ignorowana, gdy wartość nagłówka hello jest porównywana hello zbiór dopuszczalnych wartości.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** przychodzące, wychodzące  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="LimitCallRate"></a>Limit szybkości wywołanie przez subskrypcję  
 Witaj `rate-limit` zasad uniemożliwia użycie API nagłego na podstawie subskrypcji na ograniczając hello wywołać tooa szybkość określony numer na określonym przedziale czasu. Po wyzwoleniu tych zasad wywołującego hello odbiera `429 Too Many Requests` kod stanu odpowiedzi.  
  
> [!IMPORTANT]
>  Te zasady mogą być użyte tylko raz na dokument zasad.  
>   
>  [Wyrażenie zasad](api-management-policy-expressions.md) nie można użyć w żadnym hello atrybuty zasady dla tych zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a>Przykład  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|Ustaw limit|Element główny.|Tak|  
|api|Dodaj co najmniej jednego z tych elementów tooimpose limit szybkości wywołanie w interfejsach API w ramach produktu hello. Produktu i interfejsu API wywołać szybkość, z jaką ograniczenia są stosowane niezależnie.|Nie|  
|Operacja|Dodaj co najmniej jednego z tych elementów tooimpose limit szybkości wywołania na operacje w interfejsie API. Produkt, interfejsu API i operacji należy wywołać szybkość, z jaką ograniczenia są stosowane niezależnie.|Nie|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|name|Witaj nazwa hello interfejsu API dla których limit szybkości hello tooapply.|Tak|Nie dotyczy|  
|wywołania|Maksymalna całkowita liczba połączeń dozwolona interwale hello określone w hello Hello `renewal-period`.|Tak|Nie dotyczy|  
|okres odnawiania|czas w sekundach, po których hello przydziału resetuje Hello.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** produktu  
  
##  <a name="LimitCallRateByKey"></a>Limit szybkości wywołanie przez klucz  
 Witaj `rate-limit-by-key` zasad uniemożliwia użycie API nagłego na podstawie na klucz, ograniczając hello wywołać tooa szybkość określony numer na określonym przedziale czasu. klucz Hello może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad. Toospecify żądaniach powinno być liczone się limitu hello można dodać warunku opcjonalnie przyrostu. Po wyzwoleniu tych zasad wywołującego hello odbiera `429 Too Many Requests` kod stanu odpowiedzi.  
  
 Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [Zaawansowane żądanie ograniczania z usługą Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Te zasady mogą być użyte tylko raz na dokument zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a>Przykład  
 W hello poniższy przykład limit szybkości hello jest kluczem według adresu IP hello wywołującego.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|Ustaw limit|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|wywołania|Maksymalna całkowita liczba połączeń dozwolona interwale hello określone w hello Hello `renewal-period`.|Tak|Nie dotyczy|  
|klucz liczników|Witaj toouse klucza dla zasad limitu szybkości hello.|Tak|Nie dotyczy|  
|Stan przyrostowy|wyrażenie warunkowe Hello określenie, czy hello żądanie powinno być liczone kierunku hello przydziału (`true`).|Nie|Nie dotyczy|  
|okres odnawiania|czas w sekundach, po których hello przydziału resetuje Hello.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="RestrictCallerIPs"></a>Ograniczenia adresów IP wywołującego  
 Witaj `ip-filter` (umożliwia/nie zezwala na) wywołania z określonych adresów IP i/lub zakresów adresów filtry zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a>Przykład  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|Filtr IP|Element główny.|Tak|  
|Adres|Określa pojedynczy adres IP, na których toofilter.|Co najmniej jeden `address` lub `address-range` element jest wymagany.|  
|zakres adresów z = "address" Aby = "address"|Określa adres zakresu adresów IP, na których toofilter.|Co najmniej jeden `address` lub `address-range` element jest wymagany.|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|zakres adresów z = "address" Aby = "address"|Zakres IP adresów tooallow lub odmówić dostępu.|Wymagana, gdy hello `address-range` element jest używany.|Nie dotyczy|  
|Filtr IP akcji = "Zezwalaj na &#124; zabraniać"|Określa, czy powinno być dozwolone lub nie dla hello określonych adresów IP i zakresów.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="SetUsageQuota"></a>Ustaw przydział użycia przez subskrypcję  
 Witaj `quota` zasady wymuszają zastosowanie odnawialnymi lub okres istnienia wywołania woluminu i/lub przepustowości limit przydziału, na podstawie na subskrypcję.  
  
> [!IMPORTANT]
>  Te zasady mogą być użyte tylko raz na dokument zasad.  
>   
>  [Wyrażenie zasad](api-management-policy-expressions.md) nie można użyć w żadnym hello atrybuty zasady dla tych zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a>Przykład  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|limit przydziału|Element główny.|Tak|  
|api|Dodaj co najmniej jednego z tych elementów tooimpose limit przydziału w ramach produktu hello w interfejsach API. Przydziały produktu i interfejsu API są stosowane niezależnie.|Nie|  
|Operacja|Dodaj co najmniej jednego z tych elementów tooimpose limit przydziału na operacje w interfejsie API. Przydziały produktu, interfejsu API i operacji są stosowane niezależnie.|Nie|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|name|Nazwa Hello hello API lub operacji, które hello dotyczy limitu przydziału.|Tak|Nie dotyczy|  
|Przepustowość|Witaj maksymalną liczbę kilobajtów dozwolone interwale hello określone w hello `renewal-period`.|Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.|Nie dotyczy|  
|wywołania|Maksymalna całkowita liczba połączeń dozwolona interwale hello określone w hello Hello `renewal-period`.|Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.|Nie dotyczy|  
|okres odnawiania|czas w sekundach, po których hello przydziału resetuje Hello.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** produktu  
  
##  <a name="SetUsageQuotaByKey"></a>Ustaw przydział użycia według klucza  
 Witaj `quota-by-key` zasady wymuszają zastosowanie odnawialnymi lub okres istnienia wywołania woluminu i/lub przepustowości limit przydziału, na podstawie według klucza. klucz Hello może mieć wartość dowolny ciąg i jest zwykle zapewniany przy użyciu wyrażenia zasad. Toospecify żądaniach powinno być liczone kierunku hello przydziału można dodać warunku opcjonalnie przyrostu.  
  
 Aby uzyskać dodatkowe informacje i przykłady tych zasad, zobacz [Zaawansowane żądanie ograniczania z usługą Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).  
  
> [!IMPORTANT]
>  Te zasady mogą być użyte tylko raz na dokument zasad.  
>   
>  [Wyrażenie zasad](api-management-policy-expressions.md) nie można użyć w żadnym hello atrybuty zasady dla tych zasad.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a>Przykład  
 W hello poniższy przykład przydział hello jest wyznaczaną przez adres IP hello wywołującego.  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a>Elementy  
  
|Nazwa|Opis|Wymagane|  
|----------|-----------------|--------------|  
|limit przydziału|Element główny.|Tak|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|Przepustowość|Witaj maksymalną liczbę kilobajtów dozwolone interwale hello określone w hello `renewal-period`.|Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.|Nie dotyczy|  
|wywołania|Maksymalna całkowita liczba połączeń dozwolona interwale hello określone w hello Hello `renewal-period`.|Albo `calls`, `bandwidth`, lub razem muszą być jednocześnie określone.|Nie dotyczy|  
|klucz liczników|Witaj klucza toouse hello zasad przydziału.|Tak|Nie dotyczy|  
|Stan przyrostowy|wyrażenie warunkowe Hello określenie, czy hello żądanie powinno być liczone kierunku hello przydziału (`true`)|Nie|Nie dotyczy|  
|okres odnawiania|czas w sekundach, po których hello przydziału resetuje Hello.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
##  <a name="ValidateJWT"></a>Sprawdź poprawność JWT  
 Witaj `validate-jwt` zasady wymuszają zastosowanie istnienia i ważności token JWT wyodrębnione z albo określonego nagłówka HTTP lub parametr zapytania określony.  
  
> [!IMPORTANT]
>  Witaj `validate-jwt` zasady wymagają tego hello `exp` zarejestrowanych oświadczeń jest inlcuded w hello JWT token, chyba że `require-expiration-time` atrybut jest określona i ustawić także`false`.  
> Witaj `validate-jwt` zasad obsługuje HS256 i RS256 algorytmy podpisywania. Dla HS256 hello klucz należy podać wbudowane w ramach zasad hello w postaci kodowany w standardzie base64 hello. RS256 hello klucz ma toobe Podaj za pośrednictwem punktu końcowego Otwórz identyfikator konfiguracji.  
  
### <a name="policy-statement"></a>Deklaracja zasad  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a>Przykłady  
  
#### <a name="azure-mobile-services-token-validation"></a>Azure Mobile Services tokenu weryfikacji.  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a>Azure Active Directory tokenu weryfikacji.  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a>Azure Active Directory B2C tokenu weryfikacji.  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a>Autoryzowanie toooperations dostępu na podstawie tokenu oświadczeń  
 W tym przykładzie pokazano sposób toouse hello [JWT do zweryfikowania](api-management-access-restriction-policies.md#ValidateJWT) toopre zasad-toooperations dostępu na podstawie tokenu oświadczeń autoryzacji. Aby demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji zarządzania interfejsu API z Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too13:50. Szybkie przewijanie do przodu too15:00 zasady hello toosee skonfigurowane w edytorze zasad hello, a następnie too18:50 dla pokaz wywołanie operacji z portalu dla deweloperów hello zarówno z i bez hello wymagany token autoryzacji.  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a>Elementy  
  
|Element|Opis|Wymagane|  
|-------------|-----------------|--------------|  
|Sprawdź poprawność jwt|Element główny.|Tak|  
|grupy odbiorców|Zawiera listę oświadczeń dopuszczalne odbiorców, które mogą być obecne w tokenie hello. Jeśli wiele wartości odbiorców są obecne, a następnie sprawdzane są poszczególne wartości do momentu wszystkie wyczerpania (w takim przypadku niepowodzenia weryfikacji) lub aż do znalezienia właściwego konta. Należy określić co najmniej jednego odbiorcy.|Nie|  
|podpisywania klucze wystawcy|Lista toovalidate klucze używane z algorytmem Base64 zabezpieczeń podpisany tokenów. Jeśli wiele kluczy zabezpieczeń są obecne, a następnie sprawdzane są poszczególne klucze do momentu wszystkie wyczerpania (w takim przypadku niepowodzenia weryfikacji) lub do chwili pomyślnego jedną (przydatne w przypadku przerzucania token). Kluczowe elementy mają opcjonalny `id` toomatch atrybut przed `kid` oświadczeń.|Nie|  
|wystawcy|Lista dopuszczalne podmiotów zabezpieczeń, które wystawiły hello tokenu. Jeśli występują wiele wartości wystawcy, a następnie sprawdzane są poszczególne wartości do momentu wszystkie wyczerpania (w takim przypadku niepowodzenia weryfikacji) lub aż do znalezienia właściwego konta.|Nie|  
|Konfiguracja protokołu openid|element Hello używany do określania zgodne endpoint konfiguracji Open ID, z którego podpisywania kluczy i wystawcy można uzyskać.|Nie|  
|wymagane oświadczenia|Zawiera listę toobe oświadczeń oczekiwano występuje na powitania token dla niego toobe uważany za prawidłowy. Gdy hello `match` zbyt ustawiono atrybut`all` każdej wartości oświadczeń w zasadach hello musi być dostępna w tokenie hello toosucceed sprawdzania poprawności. Gdy hello `match` zbyt ustawiono atrybut`any` co najmniej jedno oświadczenie musi być dostępna w tokenie hello toosucceed sprawdzania poprawności.|Nie|  
|zumo głównego klucza|Klucz główny dla tokenów wystawionych przez usługi Azure Mobile Services|Nie|  
  
### <a name="attributes"></a>Atrybuty  
  
|Nazwa|Opis|Wymagane|Domyślne|  
|----------|-----------------|--------------|-------------|  
|niedokładność zegara|Zakres czasu. Zawiera niektóre małych swobodę w przypadku oświadczeń wygaśnięcia tokenu hello jest obecny w tokenie hello i jest poza bieżącym hello Data i godzina.|Nie|0 sekund|  
|nie powiodło się weryfikacji komunikatów o błędach|Błąd tooreturn wiadomość w treści odpowiedzi hello HTTP, jeśli hello JWT nie przeszedł pomyślnie weryfikacji. Ta wiadomość musi mieć żadnych znaków specjalnych prawidłowo wpisywany.|Nie|Domyślnego komunikatu o błędzie jest zależny od weryfikacji problem, na przykład "token JWT nie istnieje."|  
|nie powiodło się weryfikacji httpcode|Tooreturn kod stanu HTTP, jeśli hello JWT nie przeszedł pomyślnie weryfikacji.|Nie|401|  
|Nazwa nagłówka|Nazwa Hello nagłówka hello HTTP zawierający hello tokenu.|Albo `header-name` lub `query-paremeter-name` musi być określony; ale nie oba.|Nie dotyczy|  
|id|Hello `id` atrybutu na powitania `key` element umożliwia toospecify hello ciąg, który będzie dopasowywane `kid` oświadczeń w hello toofind tokenu (jeśli istnieje) limit hello odpowiedniego klucza toouse Walidacja podpisu.|Nie|Nie dotyczy|  
|dopasowanie|Witaj `match` atrybutu na powitania `claim` element określa, czy wartość oświadczenia, co w zasadach hello musi być dostępna w tokenie hello toosucceed sprawdzania poprawności. Możliwe wartości:<br /><br /> -                          `all`-każdej wartości oświadczeń w zasadach hello musi być dostępna w tokenie hello toosucceed sprawdzania poprawności.<br /><br /> -                          `any`— wartość co najmniej jedno oświadczenie musi być dostępna w tokenie hello toosucceed sprawdzania poprawności.|Nie|Wszystkie|  
|Nazwa zapytania — paremeter|Nazwa parametru zapytania hello hello zawierający hello token Hello.|Albo `header-name` lub `query-paremeter-name` musi być określony; ale nie oba.|Nie dotyczy|  
|Wymagaj — wygasa|Wartość logiczna. Określa, czy oświadczenie wygaśnięcia jest wymagany w tokenie hello.|Nie|Wartość true|
|Wymagaj schematu|Witaj nazwę schematu tokenu hello, np. "Bearer". Jeśli ten atrybut zostanie ustawiony, hello zasad będzie upewnij się, że który określony schemat jest obecny w hello wartość nagłówka uwierzytelnienia.|Nie|Nie dotyczy|
|Wymagaj podpisany — tokeny|Wartość logiczna. Określa, czy token jest wymagany toobe podpisany.|Nie|Wartość true|  
|adres URL|Otwórz adres URL punktu końcowego konfiguracji identyfikator, z której można uzyskać metadanych konfiguracji Open ID. Dla usługi Azure Active Directory użyj następującego adresu URL hello: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` podstawiając nazwa dzierżawy katalogu, np. `contoso.onmicrosoft.com`.|Tak|Nie dotyczy|  
  
### <a name="usage"></a>Sposób użycia  
 Tej zasady można używać w hello następujące zasady [sekcje](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) i [zakresy](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).  
  
-   **Sekcje zasad:** dla ruchu przychodzącego  
  
-   **Zakresy zasad:** globalnych produktu interfejsu API, operacji  
  
## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji, Praca z zasad, zobacz [zasad w usłudze API Management](api-management-howto-policies.md).  
