---
title: "aaaSession zarządzania — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
description: "środki zaradcze w przypadku zagrożeń w hello narzędzie modelowania zagrożeń"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a>Ramka zabezpieczeń: Zarządzanie sesjami | Artykuły 
| Produktów i usług | Artykuł |
| --------------- | ------- |
| **Azure AD**    | <ul><li>[Implementuje prawidłowego wylogowania przy użyciu metod ADAL w przypadku korzystania z usługi Azure AD](#logout-adal)</li></ul> |
| Urządzenia IoT | <ul><li>[Użyj ograniczone okresy istnienia generowanych tokenach SaS](#finite-tokens)</li></ul> |
| **Dokumentów w usłudze Azure DB** | <ul><li>[Minimalny okres istnienia tokenu na użytek generowanych tokenach zasobów](#resource-tokens)</li></ul> |
| **ADFS** | <ul><li>[Implementuje prawidłowego wylogowania przy użyciu metod WsFederation, korzystając z usług AD FS](#wsfederation-logout)</li></ul> |
| **Tożsamości serwera** | <ul><li>[Implementuje prawidłowego wylogowania przy użyciu tożsamości serwera](#proper-logout)</li></ul> |
| **Aplikacja sieci Web** | <ul><li>[Aplikacje dostępne za pośrednictwem protokołu HTTPS muszą używać bezpiecznych plików cookie](#https-secure-cookies)</li><li>[Wszystkie aplikacji oparty na protokole http należy określić http tylko dla definicji pliku cookie](#cookie-definition)</li><li>[Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na stronach sieci web ASP.NET](#csrf-asp)</li><li>[Konfigurowanie sesji dla okresu istnienia aktywności](#inactivity-lifetime)</li><li>[Implementuje prawidłowego wylogowania z aplikacji hello](#proper-app-logout)</li></ul> |
| **Interfejs API sieci Web** | <ul><li>[Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na interfejsów API sieci Web ASP.NET](#csrf-api)</li></ul> |

## <a id="logout-adal"></a>Implementuje prawidłowego wylogowania przy użyciu metod ADAL w przypadku korzystania z usługi Azure AD

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure AD | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Jeśli aplikacja hello opiera się na token dostępu wystawiony przez usługę Azure AD, program obsługi zdarzeń wylogowania hello powinny wywoływać |

### <a name="example"></a>Przykład
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a>Przykład
Należy także zniszczyć sesji użytkownika, wywołując metodę Session.Abandon(). Następujące metody przedstawia bezpiecznej implementacji wylogowania użytkownika:
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a>Użyj ograniczone okresy istnienia generowanych tokenach SaS

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Urządzenia IoT | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Tokeny sygnatury dostępu współdzielonego generowane w celu uwierzytelniania tooAzure Centrum IoT powinny mieć okresu wygaśnięcia. Zachowaj hello SaS okresy istnienia tokenu tooa toolimit minimalna hello ilość czasu, który może być odtwarzany w przypadku naruszenia zabezpieczeń tokeny hello.|

## <a id="resource-tokens"></a>Minimalny okres istnienia tokenu na użytek generowanych tokenach zasobów

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Dokumentów w usłudze Azure DB | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Zmniejsz timespan hello z zasobów tokenu tooa minimalną wartość wymaganą. Tokeny zasobów ma prawidłowy obiekt timespan domyślnej 1 godz.|

## <a id="wsfederation-logout"></a>Implementuje prawidłowego wylogowania przy użyciu metod WsFederation, korzystając z usług AD FS

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | ADFS | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Jeśli aplikacja hello używa tokenu Zabezpieczającego wydane przez usługi AD FS, program obsługi zdarzeń wylogowania hello powinny wywoływać toolog metody WSFederationAuthenticationModule.FederatedSignOut() limit hello użytkownika. Również hello bieżącej sesji należy zniszczyć, a wartość tokenu sesji hello należy zresetować i zniweczone.|

### <a name="example"></a>Przykład
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a>Implementuje prawidłowego wylogowania przy użyciu tożsamości serwera

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Tożsamości serwera | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Federacyjna IdentityServer3 wylogowaniu](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| **Kroki** | IdentityServer obsługuje hello możliwości toofederate przy pomocy dostawcy tożsamości zewnętrznej. Gdy użytkownik zaloguje się poza dostawcy tożsamości nadrzędnego, w zależności od protokołu hello, może być możliwe tooreceive powiadomienie po wylogowaniu się użytkownika hello. Umożliwia on toonotify IdentityServer, które jej klientów, można również zalogują się hello użytkownika. W dokumentacji hello w sekcji odwołań hello hello szczegóły implementacji.|

## <a id="https-secure-cookies"></a>Aplikacje dostępne za pośrednictwem protokołu HTTPS muszą używać bezpiecznych plików cookie

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | EnvironmentType - lokalnego programu |
| **Odwołania**              | [httpCookies — Element (schemat ustawień programu ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure właściwości](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx) |
| **Kroki** | Pliki cookie są zwykle tylko dostępny toohello domeny, dla którego zostały zakres. Niestety definicji hello "domeny" nie zawierają hello protokołu, dlatego plików cookie, które są tworzone przy użyciu protokołu HTTPS są dostępne za pośrednictwem protokołu HTTP. atrybut "secure" Hello wskazuje, że przeglądarka toohello hello plik cookie powinien tylko udostępniane za pośrednictwem protokołu HTTPS. Upewnij się, że wszystkie pliki cookie ustawić przy użyciu protokołu HTTPS używa hello **bezpiecznego** atrybutu. wymaganie Hello można wymusić w pliku web.config hello przez ustawienie tootrue atrybut parametru requireSSL hello. Jest hello preferowane podejście, ponieważ będzie wymuszać hello **bezpiecznego** atrybutu dla wszystkich plików cookie obecne i przyszłe bez hello toomake konieczność zmiany dodatkowy kod.|

### <a name="example"></a>Przykład
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
Ustawienie Hello jest wymuszane, nawet jeśli tooaccess używanych aplikacji hello jest HTTP. Użycie protokołu HTTP tooaccess hello aplikacji, hello podziałów ustawienia, które aplikacji hello ponieważ hello pliki cookie są konfigurowane przy użyciu bezpiecznego atrybutu i hello przeglądarki hello nie będzie wysyłać je kopii toohello aplikacji.

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Formularze sieci Web, MVC5 |
| **Atrybuty**              | EnvironmentType - lokalnego programu |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Gdy hello aplikacji sieci web jest hello zaufania jednostek uzależnionych oraz hello IdP serwera usług AD FS, atrybut bezpiecznego tokenu FedAuth hello można skonfigurować przez ustawienie parametru requireSSL tooTrue w `system.identityModel.services` sekcji w pliku Web.config:|

### <a name="example"></a>Przykład
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a>Wszystkie aplikacji oparty na protokole http należy określić http tylko dla definicji pliku cookie

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Atrybut bezpiecznego pliku Cookie](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| **Kroki** | toomitigate hello ryzyko ujawnienia informacji z atak skryptów między witrynami (XSS), nowy atrybut — httpOnly — zostało wprowadzone toocookies i jest obsługiwany przez wszystkie główne przeglądarki. Atrybut Hello Określa, że plik cookie nie jest dostępny za pośrednictwem skryptu. Za pomocą plików cookie HttpOnly, aplikacji sieci web zmniejsza możliwości hello poufne informacje zawarte w pliku cookie hello może być kradzieży za pomocą skryptu i wysyłane do osoby atakującej tooan witryny sieci Web. |

### <a name="example"></a>Przykład
Wszystkie aplikacje oparte na protokole HTTP, które używają plików cookie należy określić HttpOnly w definicji pliku cookie hello, implementując następujących konfiguracji w pliku web.config:
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Formularze sieci Web |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Właściwość FormsAuthentication.RequireSSL](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| **Kroki** | wartość właściwości parametru RequireSSL Hello jest ustawiana w hello pliku konfiguracji dla aplikacji ASP.NET przy użyciu atrybutu parametru requireSSL hello hello elementu konfiguracji. Można określić w pliku Web.config hello aplikacji ASP.NET czy serwera toohello plików cookie uwierzytelniania formularzy hello tooreturn wymagane przez atrybut parametru requireSSL hello ustawienia protokołu SSL (Secure Sockets Layer).|

### <a name="example"></a>Przykład 
Witaj Poniższy przykładowy kod ustawia atrybut parametru requireSSL hello w pliku Web.config hello.
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC5 |
| **Atrybuty**              | EnvironmentType - lokalnego programu |
| **Odwołania**              | [Windows Identity Foundation (WIF) Konfiguracja — część II](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| **Kroki** | Atrybut httpOnly tooset plików cookie FedAuth, wartość atrybutu hideFromCsript musi być ustawiona tooTrue. |

### <a name="example"></a>Przykład
Poniższa konfiguracja przedstawia hello prawidłowej konfiguracji:
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a>Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na stronach sieci web ASP.NET

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Fałszowanie żądań między witrynami (CSRF lub XSRF) jest typem ataku, w którym atakujący może wykonywać akcje w kontekście zabezpieczeń hello ustanowienie sesji innego użytkownika w witrynie sieci web. Celem Hello jest toomodify lub usuń zawartość, jeśli hello docelowej witryny sieci web opiera się wyłącznie na pliki cookie sesji tooauthenticate odebrane żądanie. Osoba atakująca może wykorzystać tę lukę w zabezpieczeniach, pobierając tooload przeglądarki innego użytkownika adresu URL za pomocą polecenia z lokacji narażony, na którym użytkownik hello jest już zalogowany. Istnieje wiele sposobów toodo osoby atakującej, takich jak obsługując inna witryna sieci web który ładuje zasobu z serwera narażone hello lub pobierania hello tooclick użytkownika łącza. atak powitania można zapobiec, jeśli serwer hello wysyła klientowi dodatkowe toohello token, wymaga hello tooinclude klienta tokenu we wszystkich przyszłych żądań i sprawdza, czy wszystkie przyszłych żądań obejmują token, który dotyczy toohello bieżącej sesji, takie jak przez za pomocą hello ASP.NET AntiForgeryToken lub ViewState. |

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC5, MVC6 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Zapobieganie XSRF/CSRF w platformie ASP.NET MVC i stron sieci Web](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| **Kroki** | Formularze Anti-CSRF i ASP.NET MVC — Użyj hello `AntiForgeryToken` metody pomocniczej w widokach; ujmij `Html.AntiForgeryToken()` do postaci hello, na przykład|

### <a name="example"></a>Przykład
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a>Przykład
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Przykład
Na powitania sam czasu, odwiedzający hello zapewnia Html.AntiForgeryToken() pliku cookie o nazwie __RequestVerificationToken z hello samą wartość jako hello losowych wartości ukryte przedstawionych powyżej. Następnie toovalidate przychodzące post formularza, Dodaj metodę akcji docelową toohello filtru hello [ValidateAntiForgeryToken]. Na przykład:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Filtr autoryzacji, która sprawdza, czy:
* żądanie przychodzące Hello ma pliku cookie o nazwie __RequestVerificationToken
* Witaj żądanie przychodzące ma `Request.Form` wpisu o nazwie __RequestVerificationToken
* Te pliki cookie i `Request.Form` jest dobrze zakładając, że wszystkie wartości są zgodne, Żądanie hello przechodzi przez normalnego. Ale jeśli nie, następnie wystąpił błąd autoryzacji z komunikatem "wymagany token zabezpieczający przed sfałszowaniem nie został podany lub jest nieprawidłowy". 

### <a name="example"></a>Przykład
Anti-CSRF i AJAX: hello tokenu formularza może to stanowić problem dla żądania AJAX, ponieważ żądanie AJAX może wysyłać dane JSON, a nie dane formularza HTML. Jedno rozwiązanie jest toosend hello tokenów w niestandardowy nagłówek HTTP. Witaj następujący kod używa tokenów hello toogenerate składni Razor, a następnie dodanie hello tokenów tooan AJAX żądania. 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Przykład
Podczas przetwarzania żądania hello wyodrębniania nagłówek żądania hello hello tokenów. Następnie wywołaj metodę AntiForgery.Validate hello toovalidate hello tokenów. Witaj metodę Validate zgłasza wyjątek, jeśli hello tokenów nie są prawidłowe.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Formularze sieci Web |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Podejmij korzystać z ASP.NET wbudowane funkcje tooFend poza Web ataków](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| **Kroki** | Ataki CSRF w aplikacjach na podstawie formularza sieci Web można zminimalizować przez ustawienie ViewStateUserKey tooa losowy ciąg, który jest różny dla każdego użytkownika — identyfikator użytkownika lub, lepiej jeszcze sesji identyfikator. Istnieje wiele możliwych przyczyn technicznych i społecznościowych identyfikator sesji jest znacznie lepszym rozwiązaniem, ponieważ identyfikator jest nieoczekiwane, sesji upłynie limit czasu i zmienia się na poszczególnych użytkowników.|

### <a name="example"></a>Przykład
Oto kod hello należy toohave we wszystkich stron:
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a>Konfigurowanie sesji dla okresu istnienia aktywności

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Właściwość HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx) |
| **Kroki** | Limit czasu sesji reprezentuje hello zdarzenie występuje, gdy użytkownik nie wykonywania dowolnych akcji w witrynie sieci web dla interwału (zdefiniowane przez serwer sieci web). Witaj zdarzeń po stronie serwera, zmiany stanu hello too'invalid sesji użytkownika hello "(na przykład" nie już używać") oraz poinstruuj toodestroy serwera sieci web hello go (usunięcie wszystkich danych znajdujących się w niej). Witaj Poniższy przykładowy kod ustawia hello limitu czasu sesji atrybutu too15 minut w pliku Web.config hello.|

### <a name="example"></a>Przykład
"" Kod XML <configuration> < system.web > <sessionState mode="InProc" cookieless="true" timeout="15" /> < /system.web ></configuration>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Formularze sieci Web |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Tworzy Element uwierzytelniania (schemat ustawień programu ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **Kroki** | Ustaw minut hello too15 limitu czasu plików cookie biletu uwierzytelniania formularzy|

### <a name="example"></a>Przykład
"" Kod XML<forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a>Przykład
Również hello wystawiony okres istnienia tokenu SAML oświadczenia usług AD FS należy ustawić too15 min, wykonując następujące polecenia programu powershell na serwerze usług AD FS hello hello:
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a>Implementuje prawidłowego wylogowania z aplikacji hello

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Wykonaj odpowiednie Wyloguj z aplikacji hello, gdy użytkownik naciśnie Wyloguj się przycisk. Podczas wylogowania aplikacji należy zniszczyć sesji użytkownika, resetowanie oraz zniesienia wartość pliku cookie sesji, oraz resetowanie i rozpoczynającą wartość pliku cookie uwierzytelniania. Ponadto jeśli wiele sesji są wiązanej tooa tożsamości pojedynczego użytkownika, ich musi być zbiorczo zakończona na powitania po stronie serwera na limitu czasu lub Wyloguj. Ponadto upewnij się, że wylogowania funkcje są dostępne na każdej stronie. |

## <a id="csrf-api"></a>Ograniczenia przed atakami sfałszowaniem żądań Cross-Site (CSRF) na interfejsów API sieci Web ASP.NET

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Fałszowanie żądań między witrynami (CSRF lub XSRF) jest typem ataku, w którym atakujący może wykonywać akcje w kontekście zabezpieczeń hello ustanowienie sesji innego użytkownika w witrynie sieci web. Celem Hello jest toomodify lub usuń zawartość, jeśli hello docelowej witryny sieci web opiera się wyłącznie na pliki cookie sesji tooauthenticate odebrane żądanie. Osoba atakująca może wykorzystać tę lukę w zabezpieczeniach, pobierając tooload przeglądarki innego użytkownika adresu URL za pomocą polecenia z lokacji narażony, na którym użytkownik hello jest już zalogowany. Istnieje wiele sposobów toodo osoby atakującej, takich jak obsługując inna witryna sieci web który ładuje zasobu z serwera narażone hello lub pobierania hello tooclick użytkownika łącza. atak powitania można zapobiec, jeśli serwer hello wysyła klientowi dodatkowe toohello token, wymaga hello tooinclude klienta tokenu we wszystkich przyszłych żądań i sprawdza, czy wszystkie przyszłych żądań obejmują token, który dotyczy toohello bieżącej sesji, takie jak przez za pomocą hello ASP.NET AntiForgeryToken lub ViewState. |

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC5, MVC6 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Zapobieganie Cross-Site (CSRF) Fałszerstwie żądania w składniku ASP.NET Web API](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| **Kroki** | Anti-CSRF i AJAX: hello tokenu formularza może to stanowić problem dla żądania AJAX, ponieważ żądanie AJAX może wysyłać dane JSON, a nie dane formularza HTML. Jedno rozwiązanie jest toosend hello tokenów w niestandardowy nagłówek HTTP. Witaj następujący kod używa tokenów hello toogenerate składni Razor, a następnie dodanie hello tokenów tooan AJAX żądania. |

### <a name="example"></a>Przykład
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Przykład
Podczas przetwarzania żądania hello wyodrębniania nagłówek żądania hello hello tokenów. Następnie wywołaj metodę AntiForgery.Validate hello toovalidate hello tokenów. Witaj metodę Validate zgłasza wyjątek, jeśli hello tokenów nie są prawidłowe.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a>Przykład
Anti-CSRF i formularzy platformy ASP.NET MVC — hello użyj metody pomocnika AntiForgeryToken w widokach; na przykład umieścić Html.AntiForgeryToken() do postaci hello
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a>Przykład
w powyższym przykładzie Hello dane wyjściowe obejmują przypominać następujące hello:
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Przykład
Na powitania sam czasu, odwiedzający hello zapewnia Html.AntiForgeryToken() pliku cookie o nazwie __RequestVerificationToken z hello samą wartość jako hello losowych wartości ukryte przedstawionych powyżej. Następnie toovalidate przychodzące post formularza, Dodaj metodę akcji docelową toohello filtru hello [ValidateAntiForgeryToken]. Na przykład:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Filtr autoryzacji, która sprawdza, czy:
* żądanie przychodzące Hello ma pliku cookie o nazwie __RequestVerificationToken
* Witaj żądanie przychodzące ma `Request.Form` wpisu o nazwie __RequestVerificationToken
* Te pliki cookie i `Request.Form` jest dobrze zakładając, że wszystkie wartości są zgodne, Żądanie hello przechodzi przez normalnego. Ale jeśli nie, następnie wystąpił błąd autoryzacji z komunikatem "wymagany token zabezpieczający przed sfałszowaniem nie został podany lub jest nieprawidłowy".

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC5, MVC6 |
| **Atrybuty**              | Dostawca tożsamości dostawca — usługi AD FS, tożsamość — usługi Azure AD |
| **Odwołania**              | [Zabezpieczanie interfejsu API sieci Web z indywidualnych kont i logowania lokalnego w składniku ASP.NET Web API 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| **Kroki** | Jeśli hello interfejsu API sieci Web jest zabezpieczone przy użyciu protokołu OAuth 2.0, następnie oczekuje, że token elementu nośnego autoryzacji żądania nagłówek i Udziel dostępu toohello żądania tylko wtedy, gdy hello token jest prawidłowy. W przeciwieństwie do uwierzytelniania opartego na plikach cookie przeglądarki nie dołączaj toorequests tokenów elementu nośnego hello. Witaj żąda się, że klient musi tooexplicitly dołączyć tokenu elementu nośnego hello w nagłówku żądania hello. W związku z tym dla programu ASP.NET interfejsów API sieci Web chronionych przy użyciu protokołu OAuth 2.0, tokenów elementu nośnego są traktowane jako ochrona przed atakami CSRF. Należy pamiętać, że jeśli hello MVC część aplikacji hello korzysta z uwierzytelniania formularzy (np. pliki cookie używane), tokenów zabezpieczających przed sfałszowaniem ma toobe używany przez aplikację sieci web MVC hello. |

### <a name="example"></a>Przykład
Witaj interfejsu API sieci Web ma toobe poinformowany toorely tylko na tokenów elementu nośnego, a nie na pliki cookie. Mogą to robić przez powitania po konfiguracji w `WebApiConfig.Register` — metoda: ' ' config kodu C Sharp. SuppressDefaultHostAuthentication(); Konfiguracja. Filters.Add (nowe HostAuthenticationFilter(OAuthDefaults.AuthenticationType));
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
