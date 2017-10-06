---
title: "aaaAzure usługi Active Directory zakresy v2.0, uprawnienia i zgody | Dokumentacja firmy Microsoft"
description: "Opis autoryzacji w punktu końcowego v2.0 hello Azure AD, w tym zakresy, uprawnienia i zgody."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 8f98cbf0-a71d-4e34-babf-e644ad9ff423
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 5721d368c435868bfb4ae91cff7fbb9bc4a79b66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scopes-permissions-and-consent-in-hello-azure-active-directory-v20-endpoint"></a>Zakresy, uprawnienia i zgody w punktu końcowego v2.0 usługi Azure Active Directory hello
Aplikacje do zintegrowania z usługą Azure Active Directory (Azure AD) wykonaj modelu autoryzacji, która zapewnia użytkownikom kontrolę nad jak aplikacja może uzyskiwać dostępu do danych. Implementacja v2.0 Hello modelu autoryzacji hello została zaktualizowana i zmienia sposób aplikacji musi współdziałać z usługą Azure AD. W tym artykule opisano podstawowe pojęcia hello tego modelu autoryzacji, w tym zakresy, uprawnienia i zgody.

> [!NOTE]
> punktu końcowego v2.0 Hello nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji. toodetermine, czy należy używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
>
>

## <a name="scopes-and-permissions"></a>Zakresy i uprawnień
Usługi Azure AD implementuje hello [OAuth 2.0](active-directory-v2-protocols.md) protokołu autoryzacji. OAuth 2.0 jest to metoda, za pomocą którego aplikacji innych firm mają dostęp do zasobów sieci web hostowanych w imieniu użytkownika. Dowolnego zasobu hostowanych w sieci web, która integruje się z usługą Azure AD ma identyfikator zasobu, lub *aplikacji identyfikator URI*. Na przykład zasobów hostowanych w sieci web firmy Microsoft są między innymi:

* Witaj interfejsu API usługi Office 365 Unified poczty:`https://outlook.office.com`
* Hello Azure AD Graph API:`https://graph.windows.net`
* Program Microsoft Graph:`https://graph.microsoft.com`

Witaj, który dotyczy także dla wszystkich zasobów innych firm, które zostały zintegrowane z usługą Azure AD. Żadnego z tych zasobów również definiować zestaw uprawnień, które mogą być używane toodivide hello funkcjonalność tego zasobu na mniejsze fragmenty. Na przykład [Microsoft Graph](https://graph.microsoft.io) zdefiniował hello toodo uprawnienia następujące zadania, między innymi:

* Przeczytaj kalendarza użytkownika
* Użytkownik tooa zapisu kalendarza
* Wysyłaj pocztę jako użytkownik

Definiując te typy uprawnień hello zasób ma precyzyjną kontrolę nad jego danych i jak jest udostępniany hello danych. Aplikacji innych firm mogą żądać tych uprawnień przez użytkownika aplikacji. użytkownik aplikacji Hello hello uprawnienia przed zatwierdzić hello aplikacji może działać w imieniu użytkownika hello. Przez podziału zasobów hello funkcje na mniejsze zestawy uprawnień, aplikacje innych firm może być zbudowany toorequest tylko hello określonych uprawnień potrzebnych tooperform ich funkcji. Użytkownicy aplikacji mogą poznać, dokładnie tak jak aplikacja będzie używać swoich danych i może być większa pewność, że danej aplikacji hello nie zachowuje się ze złośliwymi działaniami.

W usłudze Azure AD i OAuth, tego rodzaju uprawnienia są nazywane *zakresy*. Są one również czasami określonego tooas *oAuth2Permissions*. Zakres jest reprezentowana w usłudze Azure AD jako wartość ciągu. W ramach przykładu Microsoft Graph hello, hello wartość zakresu dla każdego uprawnienia jest:

* Przeczytaj kalendarza użytkownika za pomocą`Calendar.Read`
* Zapis kalendarza tooa użytkownika za pomocą`Mail.ReadWrite`
* Wysyłania wiadomości e-mail jako użytkownika przy użyciu przez`Mail.Send`

Aplikacja może wysłać żądanie te uprawnienia za pośrednictwem punktu końcowego v2.0 toohello żądań hello zakresów.

## <a name="openid-connect-scopes"></a>Zakresy OpenID Connect
Witaj v2.0 wdrażania protokołu OpenID Connect ma kilka dobrze zdefiniowanych zakresów, które nie są stosowane do określonego zasobu tooa: `openid`, `email`, `profile`, i `offline_access`.

### <a name="openid"></a>openid
Jeśli aplikacja przeprowadza logowania za pomocą [OpenID Connect](active-directory-v2-protocols.md), należy zażądać hello `openid` zakresu. Witaj `openid` Pokazuje zakres na konto służbowe hello zgody strony, ponieważ uprawnienie "Logowanie się w" hello i na osobiste konto Microsoft hello zgody strony jako hello uprawnienia "Wyświetl swój profil i połączyć tooapps i usługami za pomocą konta Microsoft". Z tego uprawnienia, aplikacja może odbierać Unikatowy identyfikator dla użytkownika hello w formie hello hello `sub` oświadczeń. Udostępnia także hello toohello aplikacji dostęp do punktu końcowego o informacje o użytkowniku. Witaj `openid` zakresu, może być używany w hello v2.0 punktu końcowego tokena tooacquire tokeny Identyfikatora, które mogą być używane toosecure HTTP wywołań między poszczególnymi składnikami aplikacji.

### <a name="email"></a>Adres e-mail
Witaj `email` zakresu, może być używany z hello `openid` zakresu i innych. Udostępnia hello aplikacji dostępu toohello podstawowy adres e-mail użytkownika w postaci hello hello `email` oświadczeń. Witaj `email` tylko wtedy, gdy adres e-mail jest skojarzony z kontem użytkownika hello, który nie jest zawsze przypadku hello oświadczeń znajduje się w tokenu. Gdy jest używana funkcja hello `email` zakresu, aplikacja powinna być przygotowane toohandle przypadek, w którym hello `email` oświadczenia nie istnieje w tokenie hello.

### <a name="profile"></a>Profil
Witaj `profile` zakresu, może być używany z hello `openid` zakresu i innych. Udostępnia hello aplikacji dostępu tooa znacznej ilości informacji o użytkowniku hello. Witaj informacje, które mogą uzyskać dostęp obejmuje, ale nie jest ograniczona do hello użytkownika imię, nazwisko, preferowanych nazwy użytkownika i obiektu identyfikatora. Aby uzyskać pełną listę hello profilu oświadczeń dostępnych w parametrze id_tokens powitania dla określonego użytkownika, zobacz hello [v2.0 tokeny odwołanie](active-directory-v2-tokens.md).

### <a name="offlineaccess"></a>offline_access
Witaj [ `offline_access` zakres](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) daje tooresources dostępu do Twojej aplikacji w imieniu użytkownika hello przez dłuższy czas. Na stronie powitania pracy konta zgody ten zakres jest widoczne jako hello uprawnień "W każdej chwili uzyskać dostęp do danych". Na powitania osobiste zgody strony na koncie Microsoft wygląda na to, jak hello uprawnień "W każdej chwili dostęp do informacji". Jeśli użytkownik zaakceptuje hello `offline_access` zakresu, aplikacja może odbierać tokeny odświeżania z punktu końcowego tokena w wersji 2.0 hello. Tokeny odświeżania są długotrwałe. Aplikację można uzyskać nowe tokeny dostępu, zgodnie z tych starszych wygaśnie.

Jeśli aplikacja nie żąda hello `offline_access` zakresu, nie będziesz otrzymywać tokenów odświeżania. Oznacza to, że gdy zrealizować kod autoryzacji w hello [przepływu kodu autoryzacji protokołu OAuth 2.0](active-directory-v2-protocols.md), otrzymasz token dostępu z hello `/token` punktu końcowego. token dostępu Hello jest ważny przez krótki czas. token dostępu Hello zwykle wygaśnie w ciągu godziny. W tym momencie, Twoja aplikacja powinna tooredirect hello użytkownika wstecz toohello `/authorize` tooget punktu końcowego nowy kod autoryzacji. Podczas tego przekierowania, w zależności od typu hello aplikacji użytkownik hello może muszą tooenter ponownie swoje poświadczenia lub zgody ponownie toopermissions.

Aby uzyskać więcej informacji dotyczących sposobu tooget i używania tokenów odświeżania, zobacz hello [referencyjne protokołu v2.0](active-directory-v2-protocols.md).

## <a name="requesting-individual-user-consent"></a>Żąda zgody użytkownika
W [OpenID Connect i OAuth 2.0](active-directory-v2-protocols.md) poprosić o autoryzacji, aplikacja może zażądać uprawnień hello musi przy użyciu hello `scope` parametr zapytania. Na przykład gdy użytkownik zaloguje się tooan aplikacji, aplikacji hello wysyła żądanie jak hello poniższy przykład (podziałami wierszy dodane dla czytelności):

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=
https%3A%2F%2Fgraph.microsoft.com%2Fcalendar.read%20
https%3A%2F%2Fgraph.microsoft.com%2Fmail.send
&state=12345
```

Witaj `scope` parametr jest żąda rozdzielonej spacjami listy zakresy, które hello aplikacji. Każdego zakresu jest wskazane przez dołączenie hello zakres wartości toohello identyfikator zasobu (hello aplikacji identyfikator URI). Przykład hello żądania jako użytkownik hello aplikacji hello musi użytkownika uprawnień tooread hello kalendarza i wysyłania wiadomości e-mail.

Po hello użytkownik wprowadza swoje poświadczenia, punktu końcowego v2.0 hello sprawdza pasującego rekordu *zgody użytkownika*. Jeśli użytkownik hello nie zgodził tooany hello wymagane uprawnienia w przeszłości, hello punktu końcowego v2.0 hello zapyta toogrant użytkownika hello hello wymagane uprawnienia.

![Zgody konto robocze](../../media/active-directory-v2-flows/work_account_consent.png)

Gdy użytkownik hello zatwierdza hello uprawnień, zgody hello jest rejestrowany tak, aby hello użytkownik nie ma tooconsent ponownie w kolejnych konta logowania.

## <a name="requesting-consent-for-an-entire-tenant"></a>Żąda zgody dla całego dzierżawcy
Często gdy organizacja zakupi licencji lub subskrypcji dla aplikacji, hello organizacji chce aplikacji hello udostępniania toofully dla swoich pracowników. W ramach tego procesu administrator może udzielić zgody tooact aplikacji hello imieniu dowolnego pracownika. Jeśli Witaj, Administratorze przyznaje zgody na powitania całego dzierżawy, pracownicy organizacji hello zobaczą strony zgody dla aplikacji hello.

toorequest zgody dla wszystkich użytkowników w dzierżawie, aplikację można użyć punktu końcowego zgody administratora hello.

## <a name="admin-restricted-scopes"></a>Ograniczonym zakresów
Niektóre wysokiego poziomu uprawnień w ekosystemie Microsoft hello można ustawić także*ograniczonym*. Tego rodzaju zakresy przykładów hello następujących uprawnień:

* Odczytuj dane katalogu organizacji za pomocą`Directory.Read`
* Pisanie katalogiem organizacji tooan danych za pomocą`Directory.ReadWrite`
* Przeczytaj przy użyciu grup zabezpieczeń w katalogu organizacji`Groups.Read.All`

Chociaż użytkownik klienta może udzielić toothis dostępu aplikacji rodzaj danych, użytkowników w organizacji są ograniczone z udzielanie dostępu toohello sam zestaw poufne dane firmy. W przypadku aplikacji żąda dostępu tooone te uprawnienia z organizacji użytkownika, hello użytkownika odbierze komunikat o błędzie z informacją, że nie mają uprawnień autoryzowanych tooconsent tooyour aplikacji.

Jeśli aplikacja wymaga ograniczonej tooadmin zakresy dostępu dla organizacji, należy zażądać ich bezpośrednio z administratorem firmy, również przy użyciu hello endpoint zgody administratora, opisane w dalszej części.

Administrator przydziela się, że te uprawnienia za pomocą Witaj, Administratorze zgody punktu końcowego, dla wszystkich użytkowników w dzierżawie powitalnych będzie udzielany zgody.

## <a name="using-hello-admin-consent-endpoint"></a>Przy użyciu punktu końcowego zgody administratora hello
Jeśli wykonujesz te kroki, aplikację można zbierać uprawnienia dla wszystkich użytkowników w dzierżawie, łącznie z ograniczonym zakresów. toosee przykładem kodu, który implementuje hello instrukcje, zobacz hello [próbki ograniczonym zakresy](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).

### <a name="request-hello-permissions-in-hello-app-registration-portal"></a>Żądanie uprawnienia hello w portalu rejestracji aplikacji hello
1. Przejdź tooyour aplikacji hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub [Utwórz aplikację](active-directory-v2-app-registration.md) Jeśli jeszcze.
2. Zlokalizuj hello **Microsoft Graph uprawnienia** sekcji, a następnie dodaj hello uprawnienia, które wymaga aplikacji.
3. Upewnij się, że **zapisać** hello rejestracji aplikacji.

### <a name="recommended-sign-hello-user-in-tooyour-app"></a>Zalecane: Znak hello użytkownika w aplikacji tooyour
Zazwyczaj podczas tworzenia aplikacji używającej punktu końcowego zgody administratora hello, aplikacja hello potrzebuje strony lub widok, w których hello admin można zatwierdzić aplikacji hello uprawnień. Ta strona może być część przepływu rejestracji aplikacji hello, część ustawień aplikacji hello, lub może być dedykowany "Połącz" przepływu. W wielu przypadkach warto dla tooshow aplikacji hello to "Połącz" Wyświetl tylko wtedy, gdy użytkownik jest zalogowany za pomocą służbowego konta Microsoft.

Po zarejestrowaniu użytkownika hello w tooyour aplikacji hello organizacji można zidentyfikować toowhich Witaj, Administratorze należy przed monitem tooapprove hello niezbędne uprawnienia. Chociaż nie niezbędne, ułatwia tworzenie bardziej intuicyjne środowisko dla użytkowników w organizacji. toosign hello użytkownika w wykonaj naszych [samouczki protocol w wersji 2.0](active-directory-v2-protocols.md).

### <a name="request-hello-permissions-from-a-directory-admin"></a>Żądanie uprawnienia powitania od administratora katalogu
Jeśli wszystko jest gotowe toorequest uprawnienia administratora Twojej organizacji, można przekierowywać hello użytkownika toohello v2.0 *punktu końcowego zgody administratora*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Parametr | Warunek | Opis |
| --- | --- | --- |
| Dzierżawy |Wymagane |Dzierżawca katalogu Hello ma toorequest zgody. Można podać w formacie przyjaznej nazwy lub identyfikatora GUID. |
| client_id |Wymagane |hello tego IDENTYFIKATORA aplikacji Hello [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) przypisane tooyour aplikacji. |
| redirect_uri |Wymagane |Witaj przekierowania URI miejscu hello toobe odpowiedzi wysłanych toohandle Twojej aplikacji. Dokładnie musi odpowiadać jeden hello przekierowania URI, który został zarejestrowany w portalu rejestracji aplikacji hello. |
| state |Zalecane |Wartość zawarte w żądaniu hello, zwracana w hello odpowiedzi tokenu. Można go ciągiem żadnej zawartości, który ma. Użyj hello stanu tooencode informacji o stanie użytkownika hello w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takich jak strony hello lub widoku, które znajdowały się w. |

W tym momencie usługi Azure AD wymaga toosign administratora dzierżawy, w żądaniu hello toocomplete. tooapprove hello wszystkie uprawnienia, które żądanej aplikacji w portalu rejestracji aplikacji hello jest poprosić administratora Hello.

#### <a name="successful-response"></a>Odpowiedź oznaczająca Powodzenie
Jeśli Witaj, Administratorze zatwierdza hello uprawnień dla aplikacji, odpowiedź oznaczająca Powodzenie hello wygląda następująco:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Parametr | Opis |
| --- | --- | --- |
| Dzierżawy |Hello katalogu dzierżawy, który hello aplikacji uprawnień żądał, w formacie GUID. |
| state |Wartość zawarte w żądaniu hello, które również zostaną zwrócone w odpowiedzi tokenu hello. Można go ciągiem żadnej zawartości, który ma. Stan Hello jest używany tooencode informacji na temat stanu hello użytkownika w aplikacji hello przed wystąpieniem hello żądania uwierzytelniania, takich jak strony hello lub widoku, które znajdowały się w. |
| admin_consent |Zostanie ustawiona zbyt**true**. |

#### <a name="error-response"></a>Odpowiedzi na błąd
Witaj, Administratorze nie zatwierdzenia hello uprawnień dla aplikacji, hello nie powiodła się odpowiedzi wygląda następująco:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Parametr | Opis |
| --- | --- | --- |
| error |Ciąg kodu błędu mogą być używane tooclassify typów błędów występujących, która może być używana tooreact tooerrors. |
| error_description |Komunikat o błędzie, które mogą ułatwić dewelopera zidentyfikować hello główną przyczynę błędu. |

Po otrzymaniu pomyślnej odpowiedzi z punktu końcowego zgody administratora hello, aplikację zyskały uprawnienia hello zwróciła. Następnie może żądać tokenu dla żądanego zasobu hello.

## <a name="using-permissions"></a>Korzystając z uprawnień
Po hello użytkownik zgadza toopermissions dla aplikacji, aplikacja może uzyskać tokenów dostępu, które reprezentują tooaccess uprawnienia aplikacji zasobu w niektórych pojemności. Token dostępu można używać tylko do jednego zasobu, ale zakodowanych w tokenie dostępu hello jest uprawnienie każdej aplikacji ma przyznane dla tego zasobu. tooacquire token dostępu aplikacji może wykonać żądania toohello token punktu końcowego v2.0, jak to:

```
POST common/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/json

{
    "grant_type": "authorization_code",
    "client_id": "6731de76-14a6-49ae-97bc-6eba6914391e",
    "scope": "https://outlook.office.com/mail.read https://outlook.office.com/mail.send",
    "code": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq..."
    "redirect_uri": "https://localhost/myapp",
    "client_secret": "zc53fwe80980293klaj9823"  // NOTE: Only required for web apps
}
```

Można użyć tokenu dostępu hello w zasobie toohello żądania HTTP. Wskazuje on niezawodnie zasobów toohello, że aplikacja ma tooperform właściwe uprawnienie hello określonego zadania.  

Aby uzyskać więcej informacji na temat hello OAuth 2.0 protokołu i tooget tokenów dostępu, zobacz temat hello [odwołania protokół punktu końcowego v2.0](active-directory-v2-protocols.md).
