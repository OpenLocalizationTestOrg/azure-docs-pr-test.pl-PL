---
title: "Wskazówki dotyczące usługi Azure Active Directory dostępu warunkowego aaaDeveloper | Dokumentacja firmy Microsoft"
description: "Wskazówki dla deweloperów i scenariuszy dostępu warunkowego dla usługi Azure AD"
services: active-directory
keywords: 
author: danieldobalian
manager: mbaldwin
editor: PatAltimore
ms.author: dadobali
ms.date: 07/19/2017
ms.assetid: 115bdab2-e1fd-4403-ac15-d4195e24ac95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.openlocfilehash: 589393f5d084d64872b372d895dc889f300592bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="developer-guidance-for-azure-active-directory-conditional-access"></a>Wskazówki dla deweloperów na potrzeby dostępu warunkowego dla usługi Azure Active Directory

Azure Active Directory (AD) oferuje kilka sposobów toosecure aplikacji i usługi ochrony.  Jedną z tych funkcji unikatowy jest dostępu warunkowego.  Dostęp warunkowy umożliwia deweloperom i usług dla przedsiębiorstw klientów tooprotect w wiele różnych sposobów, na przykład:

* Uwierzytelnianie wieloskładnikowe
* Stosowanie Intune tylko zarejestrowane urządzenia tooaccess określonych usług
* Ograniczenie lokalizacji użytkownika i adres IP z zakresów

Aby uzyskać więcej informacji na powitania pełne możliwości dostępu warunkowego, zobacz [dostępu warunkowego w hello klasycznego portalu Azure](../active-directory-conditional-access.md). 

W tym artykule możemy skupić się na jakie dostępu warunkowego oznacza toodevelopers tworzenie aplikacji dla usługi Azure AD.  Zakłada się znajomość [pojedynczego](active-directory-integrating-applications.md) i [wielodostępne](active-directory-devhowto-multi-tenant-overview.md) aplikacji i [typowe wzorce uwierzytelniania](active-directory-authentication-scenarios.md).

Firma Microsoft będzie Poznaj wpływ hello uzyskiwania dostępu do zasobów, które nie mają kontrolę nad mających zasady dostępu warunkowego są stosowane.  Ponadto Poznaj możemy efekty hello dostępu warunkowego w hello imieniu-przepływ "w", aplikacje sieci web podczas uzyskiwania dostępu do hello Microsoft Graph i wywoływania interfejsów API.

## <a name="how-does-conditional-access-impact-an-app"></a>Jak dostęp warunkowy wpływ aplikacji?

### <a name="app-topologies-impacted"></a>Wpływ na topologie aplikacji

W typowych przypadkach dostępu warunkowego nie powoduje zmiany zachowania aplikacji lub wymaga zmiany z hello developer.  Tylko w niektórych przypadkach, gdy aplikacja pośrednio lub w trybie dyskretnym zażąda token dla usługi, aplikacja wymaga dostępu warunkowego toohandle "wyzwania" zmiany kodu.  Może być tak proste, jak wykonywanie interakcyjne żądania logowania. 

W szczególności hello następujące scenariusze wymagają kodu dostępu warunkowego toohandle "wyzwania": 

* Uzyskiwanie dostępu do aplikacji hello Microsoft Graph
* Aplikacje wykonywania hello imieniu-przepływ "w"
* Uzyskiwanie dostępu do wielu usług/zasoby aplikacji
* Aplikacje jednej strony przy użyciu ADAL.js

Zasady dostępu warunkowego może być zastosowane toohello aplikacji, ale również mogą być zastosowane tooa interfejsu API sieci web aplikacji uzyskuje dostęp. więcej informacji o toolearn, jak tooconfigure zasady dostępu warunkowego, można znaleźć pod adresem [wprowadzenie do korzystania z usługi Azure Active Directory dostępu warunkowego](../active-directory-conditional-access-azuread-connected-apps.md#configure-per-application-access-rules).

W zależności od scenariusza hello klienta przedsiębiorstwa można zastosować i usuwać zasady dostępu warunkowego w dowolnym momencie.  Aby Twojej aplikacji toocontinue działa podczas stosowania nowych zasad należy Obsługa żądania"tooimplement hello". Witaj następujące przykłady przedstawiają żądania obsługi. 

### <a name="conditional-access-examples"></a>Przykłady dostępu warunkowego

W niektórych scenariuszach wymagane dostępu warunkowego toohandle zmiany kodu innych prac, ponieważ jest.  Poniżej przedstawiono kilka scenariuszy przy użyciu dostępu warunkowego toodo Multi-Factor authentication zapewnia dotyczą hello różnicy.

* Tworzenia aplikacji systemu iOS pojedynczej dzierżawy i Zastosuj zasady dostępu warunkowego.  Aplikacja Hello loguje się użytkownik, a nie żądania interfejsu API tooan dostępu.  Po zalogowaniu użytkownika hello zasad hello jest wywoływana automatycznie i użytkownik hello musi tooperform uwierzytelnianie wieloskładnikowe (MFA). 
* Tworzenia aplikacji sieci web z wieloma dzierżawcami, który używa hello Microsoft Graph tooaccess programu Exchange, między innymi usługami.  Klient przedsiębiorstwa, który przyjmuje tej aplikacji ustawia zasady usługi SharePoint Online.  Gdy aplikacja sieci web hello żąda token Graph MS, stosowane są zasady na dowolnym Microsoft Service (w szczególności usług, które mogą być udostępniane za pośrednictwem wykresu).  Ten użytkownik końcowy otrzyma monit o MFA. W przypadku hello hello przez użytkownika końcowego jest zalogowany za pomocą prawidłowych tokenów, oświadczeń "test", jest zwracana toohello aplikacji sieci web.  
* Tworzysz natywnych aplikacji, który używa warstwy środkowej hello tooaccess usługi Microsoft Graph.  Enterprise klienta na powitania firmy za pomocą tej aplikacji ma zastosowanie tooExchange zasady w trybie Online.  Po zalogowaniu użytkownika końcowego aplikacji natywnej hello żądania warstwy środkowej toohello dostępu i wysyła hello token.  warstwy środkowej Hello wykonuje imieniu-przepływ "w" toorequest dostępu toohello MS Graph.  W tym momencie oświadczenia "żądanie" przedstawiono toohello warstwy środkowej. warstwy środkowej Hello wysyła hello wyzwanie wstecz toohello natywnych aplikacji, która wymaga toocomply z zasad dostępu warunkowego hello.

### <a name="complying-with-a-conditional-access-policy"></a>Zgodne z zasadami dostępu warunkowego

Dla kilku topologiach innej aplikacji zasady dostępu warunkowego jest oceniane po ustanowieniu sesji hello.  Jak zasady dostępu warunkowego na powitania szczegółowości aplikacji i usług, punktu hello, w którym następuje jej wywoływanie zależy od silnie na scenariusz hello próbujesz tooaccomplish.

Jeśli aplikacja próbuje tooaccess usługi za pomocą zasad dostępu warunkowego, napotkać żądanie dostępu warunkowego.  Ten problem został zakodowany w hello `claims` parametr, który jest dostarczany w odpowiedzi z usługi Azure AD lub hello Microsoft Graph.  Oto przykład tego parametru żądania: 

```
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Deweloperzy mogą wykonać tego żądania i dołącza je na nowe tooAzure żądania AD.  Przekazywanie ten stan monituje żadnych toocomply niezbędne działania z zasad dostępu warunkowego hello hello tooperform przez użytkownika końcowego. Opisano w hello następujące scenariusze, szczegóły błędu hello i jak tooextract hello parametru. 

## <a name="scenarios"></a>Scenariusze

### <a name="prerequisites"></a>Wymagania wstępne

Azure AD dostęp warunkowy jest to funkcja dostępna w [Azure AD Premium](../active-directory-whatis.md#choose-an-edition).  Dowiedz się więcej na temat wymagań dotyczących hello licencjonowania [raport użycia licencji](../active-directory-conditional-access-unlicensed-usage-report.md).  Deweloperzy mogą dołączyć hello [Microsoft Developer Network](https://msdn.microsoft.com/dn308572.aspx), która obejmuje toohello bezpłatnej subskrypcji pakietu Enterprise Mobility Suite, która obejmuje usługi Azure AD Premium.

### <a name="considerations-for-specific-scenarios"></a>Zagadnienia dotyczące konkretnych scenariuszy

stosuje Hello następujących informacji tylko w tych scenariuszach dostępu warunkowego:

* Uzyskiwanie dostępu do aplikacji hello Microsoft Graph
* Aplikacje wykonywania hello imieniu-przepływ "w"
* Uzyskiwanie dostępu do wielu usług/zasoby aplikacji
* Aplikacje jednej strony przy użyciu ADAL.js

W hello następujące sekcje będzie uzyskujemy do typowe scenariusze, w którym są bardziej złożone.  Zasada działania core Hello jest dostępu warunkowego, które zasady są oceniane w czasie hello żądanej hello token dla usługi hello zasady dostępu warunkowego, chyba że jest uzyskiwany za pośrednictwem hello Microsoft Graph.

### <a name="scenario-app-accessing-hello-microsoft-graph"></a>Scenariusz: Aplikacja uzyskiwanie dostępu do hello Microsoft Graph

W tym scenariuszu firma Microsoft przeprowadzenie hello przypadku, gdy aplikacja sieci web zażąda dostępu toohello Microsoft Graph. zasady dostępu warunkowego Hello w takim przypadku można przypisać tooSharePoint, Exchange lub innych usług, który jest dostępny jako obciążenia za pośrednictwem hello Microsoft Graph.  W tym przykładzie załóżmy, że istnieje zasady dostępu warunkowego w usłudze Sharepoint Online.

![Uzyskiwanie dostępu do diagramu przepływu Microsoft Graph hello aplikacji](media/active-directory-conditional-access-developer/app-accessing-microsoft-graph-scenario.png)

Aplikacja Hello po raz pierwszy żąda autoryzacji toohello Microsoft Graph wymagająca dostępu do podrzędne obciążenia bez dostępu warunkowego.  Żądanie hello zakończy się pomyślnie bez wywoływania dowolne zasady i aplikacja hello odbiera tokeny dla programu Microsoft Graph.  W tym momencie aplikacji hello może używać tokenu dostępu hello w żądaniu elementu nośnego dla punktu końcowego hello żądanie. Teraz aplikacja hello potrzebuje tooaccess punktu końcowego usługi Sharepoint Online programu Microsoft Graph, na przykład:`https://graph.microsoft.com/v1.0/me/mySite`

Aplikacja Hello jest już prawidłowy token dla hello Microsoft Graph, który może wykonywać hello nowe żądanie bez wystawieniu nowy token. To żądanie nie powiedzie się i żądanie oświadczeń jest wystawione przez program Microsoft Graph w formie hello HTTP 403 — Dostęp zabroniony z ```WWW-Authenticate``` żądania.
Oto przykład hello odpowiedzi: 

```
HTTP 403; Forbidden 
error=insufficient_claims
www-authenticate="Bearer realm="", authorization_uri="https://login.windows.net/common/oauth2/authorize", client_id="<GUID>", error=insufficient_claims, claims={"access_token":{"polids":{"essential":true,"values":["<GUID>"]}}}"
```

Witaj żądania oświadczeń znajduje się wewnątrz hello ```WWW-Authenticate``` nagłówek, który może być analizowany tooextract hello oświadczeń parametr dla następnego żądania hello.  Gdy jest dołączany toohello nowe żądanie, usługi Azure AD wie zasady dostępu warunkowego hello tooevaluate po zalogowaniu użytkownika hello i aplikacji hello jest obecnie niezgodne z zasadami dostępu warunkowego hello.  Powtarzanie toohello żądania hello usługi Sharepoint Online punkt końcowy zakończy się pomyślnie.

Przykłady kodu, które przedstawiają sposób toohandle hello oświadczeń wyzwanie, można znaleźć w temacie toohello [przykładowy kod .NET pulpitu](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) ADAL .NET lub hello [przykładowy kod w imieniu — z](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) dla platformy .NET ADAL.

### <a name="scenario-app-performing-hello-on-behalf-of-flow"></a>Scenariusz: Aplikacji hello imieniu-przepływ "w" wykonywania

W tym scenariuszu firma Microsoft przeprowadzenie hello przypadek, w którym aplikacji natywnej wywołania API/usługi sieci web.  Z kolei, ta usługa ma [hello przepływ "w imieniu — z"](active-directory-authentication-scenarios.md#application-types-and-scenarios) toocall podrzędne usługi.  W tym przypadku firma Microsoft zastosowane naszej dostępu warunkowego zasad toohello podrzędne usługi (Web API 2) i korzysta z aplikacji natywnej, a nie aplikacji serwera/demon. 

![Wykonywanie hello w imieniu — z diagram przepływu aplikacji](media/active-directory-conditional-access-developer/app-performing-on-behalf-of-scenario.png)

Witaj początkowe żądanie tokenu 1 interfejsu API sieci Web nie jest wyświetlany monit hello przez użytkownika końcowego w usłudze Multi-Factor authentication, jak 1 interfejsu API sieci Web nie zawsze trafień hello podrzędne interfejsu API.  Po 1 interfejsu API sieci Web próbuje toorequest użytkownika hello token w imieniu — z sieci Web API 2, Żądanie hello nie powiedzie się, ponieważ użytkownik hello nie jest zalogowany za pomocą usługi Multi-Factor authentication.

Usługi Azure AD zwraca odpowiedź HTTP z niektórych interesujące dane: 

> [!NOTE]
> W tym wystąpieniu jest opis błędu uwierzytelniania wieloskładnikowego, ale istnieje szereg `interaction_required` dotyczące tooconditional dostępu.  

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API 2 App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

W naszym 1 interfejsu API sieci Web, możemy catch błąd hello `error=interaction_required`i wysyłać wstecz hello `claims` aplikacji komputerowej toohello żądania.  W tym momencie aplikacji komputerowej hello wprowadzić nowy `acquireToken()` połączenia i Dołącz hello `claims`żądania jako parametr ciągu zapytania dodatkowa.  To nowe żądanie wymaga hello użytkownika toodo usługi Multi-Factor authentication, a następnie wysłać ten nowy token tooWeb wstecz 1 interfejsu API i pełne hello imieniu-przepływ "w".

tootry się tego scenariusza, zobacz nasze [przykładowy kod .NET](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Go pokazuje, jak toopass hello żądania oświadczeń od aplikacji natywnej toohello 1 interfejsu API sieci Web i utworzyć nowe żądanie wewnątrz powitania klienta aplikacji. 

### <a name="scenario-app-accessing-multiple-services"></a>Scenariusz: Aplikacja uzyskiwanie dostępu do wielu usług

W tym scenariuszu firma Microsoft przeprowadzenie przypadku hello w którym aplikacja sieci web uzyskuje dostęp do dwóch usług, z których jedna ma przypisane zasady dostępu warunkowego.  W zależności od logiki aplikacji może istnieć aplikacja nie wymaga usług sieci web tooboth dostępu do ścieżki.  W tym scenariuszu hello kolejności, w której żądania tokenu odgrywa ważną rolę w hello środowisko użytkownika końcowego.

Załóżmy, że mamy usługi sieci web A i B, a usługa sieci web B ma nasze zasady dostępu warunkowego zastosowane.  Podczas żądania początkowego uwierzytelniania interakcyjne hello wymaga zgody dla obu usług, zasady dostępu warunkowego hello nie jest wymagane we wszystkich przypadkach.  Jeśli aplikacja hello żądania tokenu usługi sieci web B, zasad hello jest wywoływany i kolejne żądania usługi sieci web, A także powiedzie się w następujący sposób.

![Uzyskiwanie dostępu do diagramu przepływu wielu usług aplikacji](media/active-directory-conditional-access-developer/app-accessing-multiple-services-scenario.png)

Alternatywnie aplikacji hello początkowo żądanie tokenu, a usługi sieci web, hello przez użytkownika końcowego nie jest wywoływany hello zasady dostępu warunkowego.  Umożliwia Deweloper aplikacji hello hello toocontrol przez użytkownika końcowego i wymusza toobe zasad dostępu warunkowego hello wywoływane we wszystkich przypadkach. Witaj trudnych zdarza się, jeśli aplikacja hello później żądania tokenu usługi sieci web B. W tym momencie hello użytkownik końcowy musi toocomply z zasad dostępu warunkowego hello.  Gdy aplikacja hello próbuje zbyt`acquireToken`, może generować hello następujący błąd (powitania po diagram przedstawia): 

```
HTTP 400; Bad Request
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
``` 

![Dostęp do wielu usług żądania tokenu nowej aplikacji](media/active-directory-conditional-access-developer/app-accessing-multiple-services-new-token.png)

Hello aplikacja używa biblioteki ADAL hello, token awarii tooacquire hello jest zawsze ponowione interaktywnie.  W przypadku wystąpienia tego żądania interakcyjne użytkownika końcowego hello ma toocomply możliwości hello przy użyciu dostępu warunkowego hello.  To jest wartość true, chyba że Żądanie hello jest `AcquireTokenSilentAsync` lub `PromptBehavior.Never` w takim przypadku aplikacja hello potrzebuje tooperform interaktywnej ```AcquireToken``` toogive hello przeznaczenie hello możliwości toocomply z zasadami hello żądania. 

### <a name="scenario-single-page-app-spa-using-adaljs"></a>Scenariusz: Jednej strony aplikacji JEDNOSTRONICOWEJ przy użyciu ADAL.js

W tym scenariuszu firma Microsoft zaprezentuje do sprawę hello mamy aplikacji jednej strony (SPA), za pomocą ADAL.js toocall warunkowego dostępu do chronionego interfejsu API sieci web.  To jest prosty architektury, ale ma niektóre różnice, które należy wziąć pod uwagę podczas tworzenia wokół dostępu warunkowego toobe.

W ADAL.js, istnieje kilka funkcji, które uzyskać tokeny: `login()`, `acquireToken(...)`, `acquireTokenPopup(…)`, i `acquireTokenRedirect(…)`. 

* `login()`uzyskuje identyfikator tokenu za pośrednictwem interaktywnego żądanie logowania, ale nie uzyskanie tokenów dostępu do dowolnej usługi (łącznie z dostępu warunkowego chronione składnika web API).  
* `acquireToken(…)`następnie można używane toosilently uzyskać tokenu dostępu, co oznacza, że nie pokazuje interfejsu użytkownika w żadnym przypadku.  
* `acquireTokenPopup(…)`i `acquireTokenRedirect(…)` są obie używane toointeractively żądania tokenu dla zasobu, co oznacza zawsze pokazuj interfejsu użytkownika logowania.

Gdy aplikacja potrzebuje toocall tokenu dostępu interfejs API sieci Web, podejmuje `acquireToken(…)`.  Jeśli wygasł hello tokenu sesji lub potrzebujemy toocomply za pomocą zasad dostępu warunkowego, następnie hello *acquireToken* funkcji kończy się niepowodzeniem i używa aplikacji hello `acquireTokenPopup()` lub `acquireTokenRedirect()`.

![Przy użyciu biblioteki ADAL diagram przepływu aplikacji jednej strony](media/active-directory-conditional-access-developer/spa-using-adal-scenario.png)

Przejdźmy przykład z naszym scenariuszu dostępu warunkowego.  Hello przez użytkownika końcowego po prostu wyładowany w witrynie hello i nie ma sesji.  Możemy wykonywać `login()` wywołać, uzyskiwanie Identyfikatora tokenu bez usługi Multi-Factor authentication.  Następnie użytkownik hello trafi przycisku, który wymaga danych toorequest aplikacji hello interfejsu API sieci web.  Aplikacja Hello próbuje toodo `acquireToken()` ale kończy się niepowodzeniem, ponieważ użytkownik hello nie przeprowadzono jeszcze uwierzytelnianie wieloskładnikowe i musi toocomply z zasad dostępu warunkowego hello.

Usługi Azure AD wysyła hello wstecz po odpowiedzi HTTP: 

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
```

Nasze aplikacja potrzebuje toocatch hello `error=interaction_required`.  Witaj aplikacji można następnie użyć `acquireTokenPopup()` lub `acquireTokenRedirect()` na takie same hello zasobów.  Użytkownik Hello jest toodo wymuszone uwierzytelnianie wieloskładnikowe. Po zakończeniu uwierzytelniania wieloskładnikowego hello hello użytkownika aplikacji hello jest wystawiony świeża tokenu dostępu dla hello żądanego zasobu.

tootry się tego scenariusza, zobacz nasze [przykładowy kod w imieniu — z JS SPA](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Ten przykładowy kod używa zasad dostępu warunkowego hello i został zarejestrowany wcześniej z toodemonstrate JS SPA w tym scenariuszu interfejsu API sieci web. Widoczny jest sposób tooproperly dojście hello oświadczeń typu challenge i uzyskania tokenu dostępu, który może służyć do interfejsu API sieci Web. Alternatywnie wyewidencjonowania hello ogólne [przykładowy kod Angular.js](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) wskazówki dotyczące SPA dyrektywy Angular


## <a name="see-also"></a>Zobacz też

* Zobacz toolearn więcej informacji na temat możliwości hello [dostępu warunkowego w usłudze Azure AD](../active-directory-conditional-access.md).
* Aby uzyskać przykłady kodu więcej Azure AD, zobacz [repozytorium Github przykładów kodu](https://github.com/azure-samples?utf8=%E2%9C%93&q=active-directory). 
* Aby uzyskać więcej informacji na powitania ADAL SDK oraz dostęp do dokumentacji hello, zobacz [przewodnik biblioteki](active-directory-authentication-libraries.md).
* toolearn więcej informacji na temat wielodostępnej scenariuszy, zobacz [jak toosign wśród użytkowników za pomocą wzorca wielodostępne hello](active-directory-devhowto-multi-tenant-overview.md).
