---
title: "aaaAuthentication scenariusze dla usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Omówienie hello 5 najbardziej typowych scenariuszy uwierzytelniania dla usługi Azure Active Directory (AAD)"
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 0c84e7d0-16aa-4897-82f2-f53c6c990fd9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: 5b391e3f096fcb52934c4a8aff08688352bfd3dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-scenarios-for-azure-ad"></a>Scenariusze uwierzytelniania dla usługi Azure AD
Azure Active Directory (Azure AD) ułatwia uwierzytelniania dla deweloperów, zapewniając tożsamości jako usługa, z obsługą, dla standardowych protokołów, takich jak OAuth 2.0 i OpenID Connect, a także biblioteki typu open source dla różnych platform toohelp możesz programować szybko. Ten dokument pomaga zrozumieć hello różnych scenariuszy usługi Azure AD obsługuje i opisano sposób uruchamiania tooget. Scenariusz jest podzielony na powitania następujące sekcje:

* [Podstawy uwierzytelniania w usłudze Azure AD](#basics-of-authentication-in-azure-ad)
* [Oświadczenia w tokenach zabezpieczających usługi Azure AD](#claims-in-azure-ad-security-tokens)
* [Podstawowe informacje dotyczące rejestrowania aplikacji w usłudze Azure AD](#basics-of-registering-an-application-in-azure-ad)
* [Typy aplikacji i scenariusze](#application-types-and-scenarios)
  
  * [TooWeb przeglądarki sieci Web aplikacji](#web-browser-to-web-application)
  * [Jednostronicowej aplikacji JEDNOSTRONICOWEJ](#single-page-application-spa)
  * [Natywny tooWeb aplikacji interfejsu API](#native-application-to-web-api)
  * [TooWeb aplikacji sieci Web interfejsu API](#web-application-to-web-api)
  * [TooWeb demon lub serwera aplikacji interfejsu API](#daemon-or-server-application-to-web-api)

## <a name="basics-of-authentication-in-azure-ad"></a>Podstawy uwierzytelniania w usłudze Azure AD
Jeśli znasz podstawowe koncepcje uwierzytelniania w usłudze Azure AD, do odczytu w tej sekcji. W przeciwnym razie możesz tooskip dół za[typy aplikacji i scenariusze](#application-types-and-scenarios).

Teraz Rozważmy scenariusz najbardziej podstawowa hello, gdy wymagana jest tożsamość: aplikacja sieci web tooa tooauthenticate musi użytkownika w przeglądarce sieci web. Ten scenariusz jest opisany bardziej szczegółowo na powitania [tooWeb przeglądarki sieci Web aplikacji](#web-browser-to-web-application) sekcji, ale jego przydatne tooillustrate punkt początkowy hello możliwości usługi Azure AD i conceptualize, jak działa hello scenariusza. Należy wziąć pod uwagę powitania po diagramu dla tego scenariusza:

![Omówienie logowania jednokrotnego tooweb aplikacji](./media/active-directory-authentication-scenarios/basics_of_auth_in_aad.png)

Diagram hello powyżej pamiętać, Oto co należy tooknow o jego różne składniki:

* Usługi Azure AD jest hello dostawcy tożsamości, odpowiedzialny za weryfikowanie hello tożsamości użytkowników i aplikacje, które znajdują się w katalogu organizacji, a ostatecznie wystawiania tokenów zabezpieczających na pomyślne uwierzytelnienie tych użytkowników i aplikacji.
* Aplikacja, która chce toooutsource tooAzure uwierzytelniania AD muszą być zarejestrowane w usłudze Azure AD, który rejestruje i unikatowo identyfikuje aplikacji hello w katalogu hello.
* Deweloperzy mogą używać hello typu open source usługi Azure AD authentication bibliotek toomake uwierzytelniania łatwe dzięki obsłudze szczegółów protokołu hello za Ciebie. Zobacz [bibliotek uwierzytelniania usługi Azure Active Directory](active-directory-authentication-libraries.md) Aby uzyskać więcej informacji.

• Raz użytkownik został uwierzytelniony, aplikacja hello zweryfikować tooensure tokenu zabezpieczeń użytkownika hello tego uwierzytelnianie zakończyło się pomyślnie, na powitania przeznaczone strony. Deweloperzy mogą używać hello podane Weryfikacja toohandle biblioteki uwierzytelniania żadnych tokenu z usługi Azure AD, w tym tokenów sieci Web JSON (JWT) lub SAML 2.0. Sprawdzanie poprawności tooperform ręcznie, zobacz hello [programu obsługi tokenów JWT](https://msdn.microsoft.com/library/dn205065.aspx) dokumentacji.

> [!IMPORTANT]
> Usługi Azure AD używa tokenów toosign kluczem publicznym i sprawdź, czy są prawidłowe. Zobacz [ważne informacje dotyczące podpisywania klucza przerzucania w usłudze Azure AD](active-directory-signing-key-rollover.md) więcej informacji na temat logiki niezbędne hello musi mieć w Twojej aplikacji tooensure on jest zawsze zaktualizowane hello najnowsze kluczy.
> 
> 

• hello przepływ żądań i odpowiedzi dla procesu uwierzytelniania hello jest określany przez protokół uwierzytelniania hello, który był używany, takich jak OAuth 2.0, OpenID Connect, WS-Federation oraz SAML 2.0. Te protokoły omówiono bardziej szczegółowo w hello [protokoły uwierzytelniania usługi Active Directory Azure](active-directory-authentication-protocols.md) tematu w poniższych sekcjach hello.

> [!NOTE]
> Usługi Azure AD obsługuje hello OAuth 2.0 i standardów OpenID Connect, które szeroką gamę wykorzystanie tokenów elementu nośnego, łącznie z tokenów elementu nośnego reprezentowane jako tokenów Jwt. Token elementu nośnego jest token zabezpieczający lekkie, że przyznaje hello tooa dostępu "bearer" chronionych zasobów. W tym sensie "bearer" hello jest każda strona, która może ona powodować hello tokenu. Jeśli strona muszą najpierw zostać uwierzytelnione z tokenu elementu nośnego hello tooreceive usługi Azure AD, czy hello wymagane kroki nie są brane toosecure hello token w transmisji i przechowywania, można przechwycony i używane przez firmę niezamierzone. Chociaż w niektórych tokeny zabezpieczające wbudowany mechanizm uniemożliwia ich użycie przez osoby nieupoważnione, tokenów elementu nośnego nie mają ten mechanizm i musi być transportowane bezpiecznego kanału, takie jak zabezpieczeń warstwy transportu (HTTPS). Jeśli token elementu nośnego jest przesyłany w hello Wyczyść, środkowej atak powitania man-in mogą być używane przez token hello tooacquire strony złośliwych i użyć jej do zasobu tooa chronione nieautoryzowanego dostępu. Witaj te same zasady zabezpieczeń mają zastosowanie po zapisaniu lub buforowanie tokenów elementu nośnego do późniejszego użycia. Zawsze upewnij się, że aplikacja przesyła i przechowuje tokenów elementu nośnego w bezpieczny sposób. Aby uzyskać więcej zagadnienia dotyczące zabezpieczeń na tokenów elementu nośnego, zobacz [RFC 6750 sekcji 5](http://tools.ietf.org/html/rfc6750).
> 
> 

Teraz, gdy masz omówienie podstawy hello, przeczytaj hello sekcjami toounderstand sposób inicjowania obsługi administracyjnej działa w usłudze Azure AD i obsługuje hello typowych scenariuszy usługi Azure AD.

## <a name="claims-in-azure-ad-security-tokens"></a>Oświadczenia w tokenach zabezpieczających usługi Azure AD
Tokenów zabezpieczających wydanych przez usługę Azure AD zawiera oświadczenia lub potwierdzenia informacji na temat hello, który został uwierzytelniony. Te oświadczenia mogą posłużyć aplikacji hello dla różnych zadań. Na przykład można je używane toovalidate hello token, zidentyfikować dzierżawy directory hello podmiotu, Wyświetl informacje o użytkowniku, określa autoryzację hello podmiotu i itd. oświadczenia Hello w dowolnym tokenu zabezpieczeń są zależne od typu hello tokenu, hello typ poświadczeń używanych tooauthenticate hello użytkownika i konfiguracji aplikacji hello. W poniższej tabeli hello znajduje się krótki opis każdego typu oświadczenia emitowane przez usługę Azure AD. Aby uzyskać więcej informacji, zobacz zbyt[obsługiwany Token i typy oświadczeń](active-directory-token-and-claims.md).

| Claim | Opis |
| --- | --- |
| Identyfikator aplikacji |Identyfikuje aplikacji hello, która używa hello tokenu. |
| Grupy odbiorców |Określa zasób odbiorcy hello hello token jest przeznaczony dla. |
| Application Authentication Context Class Reference |Wskazuje, jak powitania klienta został uwierzytelniony (publicznego klienta a poufne klienta). |
| Błyskawiczne uwierzytelniania |Rejestruje hello Data i godzina wystąpienia hello uwierzytelniania. |
| Metoda uwierzytelniania |Wskazuje, jak został uwierzytelniony podmiot hello hello tokenu (hasło, certyfikat itp.). |
| Imię |Udostępnia hello imię użytkownika hello zgodnie z ustawieniami w usłudze Azure AD. |
| Grupy |Zawiera grupy identyfikatorów Azure AD obiektu, który hello użytkownik jest członkiem. |
| Dostawca tożsamości |Rejestruje hello dostawcy tożsamości, który uwierzytelniony podmiot hello hello tokenu. |
| Wystawiony w |W których hello token został wystawiony, często używany do tokenu świeżości czas hello rekordów. |
| Wystawcy |Identyfikuje STS hello, które wysyłanego hello token, a także hello dzierżawy usługi Azure AD. |
| Nazwisko |Udostępnia hello nazwisko użytkownika hello zgodnie z ustawieniami w usłudze Azure AD. |
| Nazwa |Udostępnia człowieka wartość do odczytu, która identyfikuje podmiotu hello hello tokenu. |
| Identyfikator obiektu: |Zawiera niezmienne, unikatowy identyfikator podmiotu hello w usłudze Azure AD. |
| Role |Zawiera przyjaznych nazw ról aplikacji w usłudze Azure AD tego hello użytkownikowi zostało udzielone. |
| Zakres |Wskazuje hello uprawnienia nadanego toohello klienta aplikacji. |
| Temat |Wskazuje hello podmiot zabezpieczeń, o które hello token deklaracji rozkazujących informacji. |
| Identyfikator dzierżawy |Zawiera niezmienne, unikatowy identyfikator hello katalogu dzierżawy, który wystawił hello tokenu. |
| Okres istnienia tokenu |Definiuje hello interwał czasu, w którym token jest prawidłowy. |
| Główna nazwa użytkownika |Zawiera hello nazwy głównej użytkownika hello podmiotu. |
| Wersja |Zawiera numer wersji hello hello tokenu. |

## <a name="basics-of-registering-an-application-in-azure-ad"></a>Podstawowe informacje dotyczące rejestrowania aplikacji w usłudze Azure AD
Dowolnej aplikacji, która outsources tooAzure uwierzytelniania, AD muszą być rejestrowane w katalogu. Ten krok obejmuje informuje usługi Azure AD o aplikacji, w tym hello adresu URL, jeśli jest to znajduje się, hello toosend adres URL odpowiedzi po uwierzytelnieniu hello tooidentify identyfikator URI aplikacji i inne. Te informacje są niezbędne dla kilka przyczyn, dla klucza:

* Usługi Azure AD musi toocommunicate współrzędnych z aplikacji hello podczas obsługi logowania jednokrotnego lub wymianę tokenów. Obejmują one hello następujące czynności:
  
  * Identyfikator URI Identyfikatora aplikacji: hello identyfikator dla aplikacji. Ta wartość jest wysyłana tooAzure AD podczas tooindicate uwierzytelniania, których aplikacja hello wywołującego chce token dla. Ponadto ta wartość jest uwzględnione w tokenie hello tak, aby aplikacja hello wie, że był hello mającą docelowej.
  * Odpowiedz na adres URL i identyfikator URI przekierowania: W przypadku hello interfejsu API sieci web lub aplikacji sieci web, hello adres URL odpowiedzi jest hello toowhich lokalizacji usługi Azure AD będzie wysyłać odpowiedzi uwierzytelniania hello, w tym tokenu, jeśli uwierzytelnianie zakończyło się pomyślnie. W przypadku hello natywnych aplikacji hello identyfikator URI przekierowania jest unikatowy identyfikator toowhich usługi Azure AD przekieruje agenta użytkownika hello w żądaniu protokołu OAuth 2.0.
  * Identyfikator aplikacji: hello identyfikator dla aplikacji, które jest generowany przez usługę Azure AD, gdy aplikacja hello jest zarejestrowana. Podczas żądania kodu autoryzacji lub na tokenie, hello identyfikator aplikacji i klucz są wysyłane tooAzure AD podczas uwierzytelniania.
  * Klucz: hello klucz, który jest wysyłany razem z Identyfikatorem aplikacji podczas uwierzytelniania toocall tooAzure AD interfejs API sieci web.
* Azure musi AD aplikacja hello tooensure hello tooaccess uprawnienia wymagane dane katalogu innych aplikacji w organizacji i tak dalej

Inicjowanie obsługi administracyjnej staje się jaśniejszy po zapoznaniu się, że istnieją dwie kategorie aplikacji, które mogą być opracowane i zintegrowane z usługą Azure AD:

* Pojedyncza aplikacja dzierżawy: aplikacji pojedynczej dzierżawy jest przeznaczony do użytku w jednej z organizacji. Są to zazwyczaj — biznesowych (LoB) aplikacje napisane przez autora przedsiębiorstwa. Stosowanie pojedynczej dzierżawy musi tylko toobe dostępne dla użytkowników w jednym katalogu, i w związku z tym tylko musi toobe udostępniane w jednym katalogu. Te aplikacje zwykle są rejestrowane przez dewelopera w organizacji hello.
* Wielodostępne aplikacji: aplikacji wielodostępnych jest przeznaczony do użycia w wielu organizacjach nie tylko jednej z organizacji. Są to zazwyczaj oprogramowania jako — usługa (SaaS) aplikacje napisane przez niezależnego dostawcy oprogramowania (ISV). Aplikacje wielodostępne muszą toobe udostępniane w każdym katalogu gdzie będą one używane, co wymaga tooregister zgody użytkownika lub administratora je. Ten proces zgody uruchamiana, gdy aplikacja została zarejestrowana w katalogu hello i uzyskuje dostęp do interfejsu API programu Graph toohello lub być może inny interfejs API sieci web. Gdy użytkownik lub administrator z innej organizacji zarejestrowaniu aplikacji hello toouse, mają być przedstawiane z okna dialogowego, które wyświetla hello uprawnienia, które wymaga aplikacji hello. Witaj użytkownik lub administrator może następnie zgody toohello aplikacji, co daje toohello dostępu aplikacji hello określone dane, a na koniec rejestrów hello aplikacji w ich katalogu. Aby uzyskać więcej informacji, zobacz [omówienie hello zgody Framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).

Kilka dodatkowych kwestii dotyczących wystąpić podczas opracowywania aplikacji wielodostępnych, zamiast aplikacji pojedynczej dzierżawy. Na przykład, jeśli tworzysz toousers dostępne w Twojej aplikacji w wielu katalogach, należy toodetermine mechanizmu dzierżawy, które występowały w. Aplikacji pojedynczej dzierżawy musi tylko toolook w jego własnej katalogu dla użytkownika, gdy aplikacji wielodostępnych musi tooidentify określonego użytkownika ze wszystkich katalogów hello w usłudze Azure AD. tooaccomplish tego zadania, usługa Azure AD zapewnia wspólnego punktu końcowego uwierzytelniania gdzie wszelkie aplikacje wielodostępne może kierować żądań logowania, zamiast punktu końcowego specyficznego dla dzierżawy. Ten punkt końcowy jest https://login.microsoftonline.com/common dla wszystkich katalogów w usłudze Azure AD, punkt końcowy specyficznego dla dzierżawy może być https://login.microsoftonline.com/contoso.onmicrosoft.com. Witaj wspólnego punktu końcowego jest szczególnie ważne tooconsider podczas opracowywania aplikacji, ponieważ będziesz potrzebować toohandle niezbędne logiki hello wielu dzierżawców podczas logowania, wylogowania i tokenu weryfikacji.

Jeśli obecnie opracowujesz aplikację pojedynczej dzierżawy, ale mają toomake go dostępne toomany organizacji, można łatwo wprowadzać zmiany toohello aplikacji i jej konfiguracji w usłudze Azure AD toomake go obsługujących wielu dzierżawców. Ponadto usługi Azure AD używa hello tego samego klucza dla wszystkich tokenów we wszystkich katalogach podpisywania czy udostępniasz uwierzytelniania w pojedynczej dzierżawy lub aplikacji wielu dzierżawców.

Każdy scenariusz wymienione w niniejszym dokumencie zawiera podsekcja opisującą jego wymagania inicjowania obsługi administracyjnej. Aby uzyskać bardziej szczegółowe informacje dotyczące inicjowania obsługi aplikacji w usłudze Azure AD i hello różnice między aplikacjami pojedynczych i wielu dzierżawców, zobacz [integracji aplikacji z usługą Azure Active Directory](active-directory-integrating-applications.md) Aby uzyskać więcej informacji. Nadal odczytywania toounderstand hello typowych scenariuszy aplikacji w usłudze Azure AD.

## <a name="application-types-and-scenarios"></a>Typy aplikacji i scenariusze
Każdy z opisanych w tym dokumencie scenariuszy hello mogą być opracowane za pomocą różnych języków i platform. One wszystkich bazują na pełną przykłady, które są dostępne w naszych [przykłady kodu przewodnik](active-directory-code-samples.md), lub bezpośrednio z odpowiadającego hello [repozytoriów GitHub próbki](https://github.com/Azure-Samples?utf8=%E2%9C%93&query=active-directory). Ponadto jeśli aplikacja wymaga konkretne lub segment end-to-end scenariusz, w większości przypadków te funkcje można dodać niezależnie. Na przykład jeśli masz natywnych aplikacji, która wywołuje interfejs API sieci web, można łatwo dodać aplikacji sieci web wywołująca hello interfejsu API sieci web. Witaj poniższym diagramie przedstawiono te scenariusze i typy aplikacji i w jaki sposób można dodać różnych składników:

![Typy aplikacji i scenariusze](./media/active-directory-authentication-scenarios/application_types_and_scenarios.png)

Są to pięć scenariuszy głównej aplikacji hello, obsługiwane przez usługę Azure AD:

* [Sieci Web przeglądarce tooWeb aplikacji](#web-browser-to-web-application): użytkownik musi toosign w tooa aplikacji sieci web chronionej przez usługę Azure AD.
* [Pojedynczy strony aplikacji JEDNOSTRONICOWEJ](#single-page-application-spa): użytkownik musi toosign w tooa jednostronicowej aplikacji chronionej przez usługę Azure AD.
* [Natywny tooWeb aplikacji interfejsu API](#native-application-to-web-api): aplikacji natywnej działającym na telefonie, tablecie lub tooauthenticate potrzeb PC tooget użytkownika zasobów z interfejsu API sieci web chronionej przez usługę Azure AD.
* [Interfejs API tooWeb aplikacji sieci Web](#web-application-to-web-api): aplikacja sieci web wymaga zasobów tooget ze składnika web API zabezpieczone przez usługę Azure AD.
* [TooWeb demon lub serwera aplikacji interfejsu API](#daemon-or-server-application-to-web-api): aplikację demona lub serwera bez interfejsu użytkownika sieci web wymaga zasobów tooget ze składnika web API zabezpieczone przez usługę Azure AD.

### <a name="web-browser-tooweb-application"></a>TooWeb przeglądarki sieci Web aplikacji
W tej sekcji opisano aplikację, która służy do uwierzytelniania użytkowników w aplikacji sieci web tooa przeglądarki sieci web. W tym scenariuszu aplikacji sieci web hello kieruje użytkownika hello przeglądarki toosign w tooAzure AD. Usługi Azure AD zwraca odpowiedź logowania za pośrednictwem przeglądarki hello użytkownika, który zawiera oświadczenia dotyczące użytkownika hello w tokenie zabezpieczającym. Ten scenariusz obsługuje logowania przy użyciu protokołów hello WS-Federation, SAML 2.0 i OpenID Connect.

#### <a name="diagram"></a>Diagram
![Przepływ uwierzytelniania dla aplikacji tooweb przeglądarki](./media/active-directory-authentication-scenarios/web_browser_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Opis protokołu przepływu
1. Gdy użytkownik odwiedza aplikacji hello i wymaga toosign w, zostanie przekierowany za pośrednictwem punktu końcowego uwierzytelniania toohello żądania logowania w usłudze Azure AD.
2. Witaj użytkownik loguje się na powitania strony logowania.
3. Jeśli uwierzytelnianie zakończy się pomyślnie, usługi Azure AD umożliwia utworzenie tokenu uwierzytelniania i zwraca adres URL odpowiedzi aplikacji toohello logowania odpowiedzi, który został skonfigurowany w hello portalu Azure. W przypadku aplikacji produkcyjnej ten adres URL odpowiedzi powinna być HTTPS. Witaj zwrócił token zawiera oświadczenia dotyczące użytkownika hello i Azure AD, które są wymagane przez token hello toovalidate aplikacji hello.
4. Aplikacja Hello weryfikuje hello token przy użyciu publicznego klucza podpisywania i wystawcy informacji dostępnych w hello dokument metadanych usług federacyjnych dla usługi Azure AD. Po aplikacji hello weryfikuje hello token, usługi Azure AD nowa sesja rozpoczyna się od hello użytkownika. Ta sesja umożliwia tooaccess użytkownika hello hello aplikacji do momentu wygaśnięcia.

#### <a name="code-samples"></a>Przykłady kodu
Zobacz hello przykłady kodu dla scenariuszy aplikacji tooWeb przeglądarki sieci Web. I wrócić tu często — możemy dodać nowe próbki cały czas hello. [Sieci Web przeglądarce tooWeb aplikacji](active-directory-code-samples.md#web-browser-to-web-application).

#### <a name="registering"></a>Rejestrowanie
* Pojedynczej dzierżawy: Jeśli tworzysz aplikację tylko dla organizacji, musi być zarejestrowana w katalogu firmy przy użyciu hello portalu Azure.
* Wielodostępne: Jeśli tworzysz aplikację, która może być używane przez użytkowników spoza organizacji, to musi być zarejestrowana w katalogu firmy, ale musi być zarejestrowana w poszczególnych organizacji w katalogu, który będzie używany w aplikacji hello. toomake dostępnych w ich katalogu aplikacji, można dołączyć procesu tworzenia konta dla klientów, które umożliwia im tooconsent tooyour aplikacji. Rejestracji aplikacji, ich zostanie wyświetlone okno dialogowe, które pokazuje aplikacji hello uprawnienia hello wymaga, a następnie hello tooconsent opcji. W zależności od hello wymagane uprawnienia administratora w hello innej organizacji mogą być wymagane zgody toogive. Gdy hello użytkownik lub administrator wyraża zgodę, aplikacja hello jest zarejestrowany w ich katalogu. Aby uzyskać więcej informacji, zobacz [integracji aplikacji z usługą Azure Active Directory](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Wygaśnięcia tokenu
Hello sesja wygasa po upływie okresu istnienia hello hello token wystawiony przez usługę Azure AD. Aplikację można zmniejszyć tym okresie, w razie potrzeby, takie jak wylogowywania użytkowników oparte na okresie braku aktywności. Po wygaśnięciu sesji hello hello użytkownik będzie ponownie zostanie wyświetlony monit o toosign w.

### <a name="single-page-application-spa"></a>Jednostronicowej aplikacji JEDNOSTRONICOWEJ
W tej sekcji opisano uwierzytelnianie dla jednej aplikacji strony, która używa usługi Azure AD i hello niejawne autoryzacji OAuth 2.0 udzielić toosecure zakończenia jego interfejsu API sieci web ponownie. Aplikacje jednostronicowe zwykle mają strukturę jako Warstwa prezentacji JavaScript (frontonu) uruchomioną w przeglądarce hello i interfejsu API sieci Web wewnętrznej działającą na serwerze i implementuje hello logiki biznesowej aplikacji. Zobacz toolearn więcej informacji na temat udzielania autoryzacji niejawne hello i pomoc można zdecydować, czy odpowiednie dla danego scenariusza aplikacji [hello opis OAuth2 niejawne Przyznaj przepływu w usłudze Azure Active Directory](active-directory-dev-understanding-oauth2-implicit-grant.md).

W tym scenariuszu po zalogowaniu użytkownika hello hello JavaScript front end używa [biblioteki uwierzytelniania usługi Active Directory dla języka JavaScript (ADAL. JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js/tree/dev) i autoryzacji niejawne hello udzielić tooobtain identyfikator tokenu (żądaniu) z usługi Azure AD. Hello token jest buforowany i powitania klienta dołączona toohello żądania jako token elementu nośnego hello wywołania końcowego, który jest zabezpieczone przy użyciu oprogramowania pośredniczącego OWIN hello powrotem tooits interfejsu API sieci Web. 

#### <a name="diagram"></a>Diagram
![Jeden diagram strony aplikacji](./media/active-directory-authentication-scenarios/single_page_app.png)

#### <a name="description-of-protocol-flow"></a>Opis protokołu przepływu
1. Witaj, użytkownik przechodzi toohello aplikacji sieci web.
2. Aplikacja Hello zwraca hello JavaScript frontonu (Warstwa prezentacji) toohello przeglądarki.
3. Użytkownik Hello inicjuje logowania, na przykład klikając znak łącza. Przeglądarka Hello wysyła toorequest toohello punktu końcowego autoryzacji usługi Azure AD GET token Identyfikatora. To żądanie zawiera hello identyfikator i odpowiedzi adres URL aplikacji hello parametry zapytania.
4. Usługi Azure AD weryfikuje hello adres URL odpowiedzi przed hello zarejestrowany adres URL odpowiedzi, który został skonfigurowany w hello portalu Azure.
5. Witaj użytkownik loguje się na powitania strony logowania.
6. Jeśli uwierzytelnianie zakończy się pomyślnie, usługi Azure AD umożliwia utworzenie tokenu identyfikator i zwraca go jako adresu URL fragmentu # toohello odpowiedzi adresem URL aplikacji. W przypadku aplikacji produkcyjnej ten adres URL odpowiedzi powinna być HTTPS. Witaj zwrócił token zawiera oświadczenia dotyczące użytkownika hello i Azure AD, które są wymagane przez token hello toovalidate aplikacji hello.
7. Kod klienta JavaScript Hello uruchomiony w przeglądarce hello wyodrębnia hello token z toouse odpowiedzi hello zabezpieczania wywołania zakończenia toohello aplikacji interfejsu API sieci web ponownie.
8. wywołania przeglądarki Hello hello aplikacji sieci web w nagłówku autoryzacji hello interfejsu API z powrotem kończyć hello tokenu dostępu.

#### <a name="code-samples"></a>Przykłady kodu
Zobacz hello przykłady kodu dla scenariuszy jednej strony aplikacji JEDNOSTRONICOWEJ. Należy się toocheck wstecz często — możemy dodać nowe próbki cały czas hello. [Pojedynczy strony aplikacji JEDNOSTRONICOWEJ](active-directory-code-samples.md#single-page-application-spa).

#### <a name="registering"></a>Rejestrowanie
* Pojedynczej dzierżawy: Jeśli tworzysz aplikację tylko dla organizacji, musi być zarejestrowana w katalogu firmy przy użyciu hello portalu Azure.
* Wielodostępne: Jeśli tworzysz aplikację, która może być używane przez użytkowników spoza organizacji, to musi być zarejestrowana w katalogu firmy, ale musi być zarejestrowana w poszczególnych organizacji w katalogu, który będzie używany w aplikacji hello. toomake dostępnych w ich katalogu aplikacji, można dołączyć procesu tworzenia konta dla klientów, które umożliwia im tooconsent tooyour aplikacji. Rejestracji aplikacji, ich zostanie wyświetlone okno dialogowe, które pokazuje aplikacji hello uprawnienia hello wymaga, a następnie hello tooconsent opcji. W zależności od hello wymagane uprawnienia administratora w hello innej organizacji mogą być wymagane zgody toogive. Gdy hello użytkownik lub administrator wyraża zgodę, aplikacja hello jest zarejestrowany w ich katalogu. Aby uzyskać więcej informacji, zobacz [integracji aplikacji z usługą Azure Active Directory](active-directory-integrating-applications.md).

Po zarejestrowaniu aplikacji hello musi być skonfigurowany toouse protokołu OAuth 2.0 niejawne Przyznaj. Domyślnie ten protokół jest wyłączone dla aplikacji. Witaj tooenable protokołu OAuth2 niejawne Przyznaj aplikacji, Edytuj jej w manifeście aplikacji z portalu Azure hello i ustaw tootrue wartość "oauth2AllowImplicitFlow" hello. Aby uzyskać szczegółowe instrukcje, zobacz [włączenie OAuth 2.0 niejawne Przyznaj dla aplikacje jednostronicowe](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Wygaśnięcia tokenu
Gdy używasz uwierzytelniania toomanage ADAL.js z usługą Azure AD, korzystać z kilku funkcji, które ułatwiają wygasły token odświeżania, a także uzyskiwania tokenów dodatkowe sieci web interfejsu API zasobów, które może być wywoływany przez aplikacji hello. Gdy hello użytkownik zostanie pomyślnie uwierzytelniony z usługą Azure AD, zabezpieczone przez plik cookie sesji zostanie nawiązane dla użytkownika hello między hello przeglądarki i Azure AD. Jest ważne toonote, który hello sesji istnieje między hello użytkownika i Azure AD i nie między hello użytkownika i aplikacji sieci web hello na powitania serwera. Po wygaśnięciu tokenu ADAL.js używa tej sesji toosilently uzyskać inny token. Dokonuje tego przy użyciu toosend ukryte iFrame, a mógł odebrać Żądanie hello przy użyciu protokołu OAuth niejawne Przyznaj hello. ADAL.js można również użyć ten sam mechanizm toosilently uzyskanie tokenów dostępu z usługą Azure AD, inne zasoby interfejsu API czy wywołania aplikacji hello tak długo, jak te zasoby obsługuje współużytkowanie zasobów między źródłami (CORS), do udostępniania są zarejestrowane w katalogu użytkownika hello i wszystkie wymagane zgody podał hello użytkownika podczas logowania.

### <a name="native-application-tooweb-api"></a>Natywny tooWeb aplikacji interfejsu API
W tej sekcji opisano natywnych aplikacji, która wywołuje interfejs API sieci web w imieniu użytkownika. Ten scenariusz jest zbudowany na typ grant kodu autoryzacji hello OAuth 2.0 za pomocą publicznego klienta, zgodnie z opisem w sekcji 4.1 hello [Specyfikacja protokołu OAuth 2.0](http://tools.ietf.org/html/rfc6749). natywnych aplikacji Hello uzyskuje token dostępu dla użytkownika hello przy użyciu protokołu hello OAuth 2.0. Ten token dostępu jest następnie wysyłane hello żądanie toohello interfejsu API sieci web, które autoryzują użytkowników hello i zwraca hello żądanego zasobu.

#### <a name="diagram"></a>Diagram
![Natywny tooWeb aplikacji interfejsu API diagramu](./media/active-directory-authentication-scenarios/native_app_to_web_api.png)

#### <a name="authentication-flow-for-native-application-tooapi"></a>Przepływ uwierzytelniania dla aplikacji natywnej tooAPI
#### <a name="description-of-protocol-flow"></a>Opis protokołu przepływu
Jeśli korzystasz z biblioteki uwierzytelniania hello AD, większość szczegóły protokołu hello opisanych poniżej są obsługiwane, takich jak okienko wyskakujące przeglądarki hello buforowaniem tokena i Obsługa tokenów odświeżania.

1. Przy użyciu okienko wyskakujące przeglądarki, natywnych aplikacji hello sprawia, że punkt końcowy autoryzacji toohello żądania w usłudze Azure AD. To żądanie zawiera hello identyfikator aplikacji i hello przekierowania URI natywnych aplikacji hello, jak pokazano na powitania portalu Azure i aplikacji hello identyfikator URI dla interfejsu API sieci web hello. Jeśli użytkownik hello nie jest już zalogowany, zostanie wyświetlony monit o toosign w ponownie są
2. Usługa Azure AD uwierzytelnia użytkownika hello. Jeśli jest to aplikacja wielodostępnych aplikacji hello toouse wymagana jest zgoda, użytkownik hello będzie tooconsent wymagane, jeśli ich nie zostało to jeszcze zrobione. Po przyznaniu zgody i po pomyślnym uwierzytelnieniu usługa Azure AD wystawia autoryzacji kod odpowiedzi wstecz toohello klienta przez identyfikator URI przekierowania aplikacji.
3. Gdy usługa Azure AD wystawia wstecz odpowiedzi kod autoryzacji toohello identyfikator URI przekierowania, hello kodem aplikacji klienta zatrzymuje przeglądarki interakcji i wyodrębnia hello autoryzacji z odpowiedzi hello. Przy użyciu tego kodu autoryzacji, aplikacja kliencka hello wysyła żądanie tooAzure Directory token punktu końcowego, który zawiera kod autoryzacji hello, szczegółowe informacje o hello aplikacji klienta (identyfikator aplikacji i identyfikator URI przekierowania) i hello żądanego zasobu (identyfikator aplikacji Identyfikator URI dla interfejsu API sieci web hello).
4. Kod autoryzacji Hello i informacje dotyczące aplikacji klienckiej hello i interfejs API sieci web są weryfikowane przez usługę Azure AD. Po pomyślnym zweryfikowaniem usługi Azure AD zwraca dwa tokeny: token JWT dostępu i token odświeżania JWT. Ponadto usługi Azure AD zwraca podstawowe informacje o użytkowniku hello, takie jak ich wyświetlaną nazwę i dzierżawy identyfikatorów.
5. Przy użyciu protokołu HTTPS aplikacja kliencka hello używa hello zwracane hello tooadd tokenu dostępu JWT ciąg tokenu JWT z oznaczeniem "Bearer" w nagłówku autoryzacji hello hello żądanie toohello interfejsu API sieci web. Interfejs API sieci web Hello następnie weryfikuje hello JWT token, a Jeśli weryfikacja zakończy się pomyślnie, zwraca hello żądanego zasobu.
6. Po wygaśnięciu tokenu dostępu hello powitania klienta aplikacji zostanie wyświetlony błąd, który wskazuje, że użytkownik hello musi tooauthenticate ponownie. Aplikacja hello ma token odświeżania prawidłowy, można używane tooacquire nowy token dostępu bez monitowania użytkownika toosign w Witaj ponownie. Jeśli token odświeżania hello wygaśnie, należy aplikacji hello toointeractively uwierzytelnić użytkownika hello jeszcze raz.

> [!NOTE]
> token odświeżania Hello wystawiony przez usługę Azure AD mogą być używane tooaccess wielu zasobów. Na przykład jeśli masz aplikacji klienckiej, która ma uprawnienia interfejsów API sieci web toocall dwa token odświeżania hello może być używane tooget dostępu tokenu toohello innego interfejsu API sieci web w również.
> 
> 

#### <a name="code-samples"></a>Przykłady kodu
Zobacz hello przykłady kodu dla scenariuszy interfejsu API tooWeb natywnych aplikacji. I wrócić tu często — możemy dodać nowe próbki cały czas hello. [Natywny tooWeb aplikacji interfejsu API](active-directory-code-samples.md#native-application-to-web-api).

#### <a name="registering"></a>Rejestrowanie
* Pojedynczej dzierżawy: Zarówno hello aplikacji natywnej i hello interfejsu API sieci web musi być zarejestrowana w hello tym samym katalogu w usłudze Azure AD. Witaj interfejsu API sieci web może być skonfigurowany tooexpose zestaw uprawnień, które są używane toolimit hello natywnych aplikacji dostęp do zasobów tooits. następnie aplikacja kliencka Hello wybiera hello potrzebne uprawnienia z menu rozwijanego "TooOther uprawnienia aplikacji" hello w hello portalu Azure.
* Wielodostępne: Po raz pierwszy, natywnych aplikacji hello tylko zarejestrowane w katalogu wydawcy lub hello developer. Po drugie natywnych aplikacji hello są uprawnienia hello skonfigurowanego tooindicate wymaga toobe funkcjonalności. Ta lista wymaganych uprawnień jest wyświetlany w oknie dialogowym, jeśli użytkownik lub administrator w katalogu docelowym hello daje aplikacji toohello zgody, dzięki czemu dostępne tootheir organizacji. Niektóre aplikacje wymagają tylko użytkownika poziomu uprawnień, które każdy użytkownik w organizacji hello można wyrazić zgodę na. Inne aplikacje wymagają uprawnień na poziomie administratora, które użytkownik w organizacji hello nie można wyrazić zgodę na. Tylko administrator katalogu, który pozwala tooapplications zgody, które wymagają tego poziomu uprawnień. Gdy użytkownik hello lub administrator wyrazi na to zgody, tylko hello interfejsu API sieci web jest zarejestrowany w ich katalogu. Aby uzyskać więcej informacji, zobacz [integracji aplikacji z usługą Azure Active Directory](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Wygaśnięcia tokenu
Gdy natywnych aplikacji hello używa jej tooget kod autoryzacji tokenu JWT dostępu, również odbiera token odświeżania JWT. Po wygaśnięciu tokenu dostępu hello token odświeżania hello mogą być używane toore-uwierzytelnić użytkownika hello bez konieczności ich toosign w ponownie. Ten token odświeżania jest używane tooauthenticate hello użytkownika, nowe dostępu, którego wynikiem token i Odśwież tokenu.

### <a name="web-application-tooweb-api"></a>TooWeb aplikacji sieci Web interfejsu API
W tej sekcji opisano aplikacji sieci web, która potrzebuje zasobów tooget z interfejsu API sieci web. W tym scenariuszu istnieją dwa typy tożsamości, które hello aplikacji sieci web można używać tooauthenticate i wywołania interfejsu API sieci web hello: tożsamość aplikacji lub tożsamości użytkownika delegowanego.

*Tożsamość aplikacji:* interfejs API sieci web to scenariusz korzysta z poświadczeń klienta OAuth 2.0 przyznanie tooauthenticate jako aplikacja hello i hello dostępu. Korzystając z tożsamością aplikacji sieci web hello interfejsu API tylko może wykryć, czy wywołanie aplikacji sieci web hello, jako hello interfejsu API sieci web nie otrzymuje żadnych informacji o hello użytkownika. Jeśli aplikacja hello odbiera informacje o użytkowniku hello, zostaną wysłane za pośrednictwem protokołu aplikacji hello i nie jest podpisany przez usługę Azure AD. Interfejs API sieci web Hello zaufania, czy aplikacja sieci web hello uwierzytelniony użytkownik hello. Z tego powodu ten wzorzec jest wywoływana zaufany podsystem.

*Delegowane tożsamości użytkownika:* w tym scenariuszu można przeprowadzić na dwa sposoby: OpenID Connect i udzielania kodu autoryzacji protokołu OAuth 2.0 z klientem poufne. Aplikacja sieci web Hello uzyskuje token dostępu dla użytkownika hello, który okaże się toohello składnika web API tej aplikacji sieci web toohello użytkownik pomyślnie uwierzytelniony hello i aplikacji sieci web hello został tooobtain stanie delegowany użytkownik tożsamości toocall hello interfejsu API sieci web. Ten token dostępu jest wysyłane w hello żądanie toohello interfejsu API sieci web, które autoryzują użytkowników hello i zwraca hello żądanego zasobu.

#### <a name="diagram"></a>Diagram
![Diagram tooWeb interfejsu API aplikacji w sieci Web](./media/active-directory-authentication-scenarios/web_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Opis protokołu przepływu
Zarówno hello tożsamości aplikacji i typów tożsamości użytkownika delegowanego omówiono w przepływie hello poniżej. Witaj klucza różnica między nimi polega na tym, że tożsamość użytkownika hello delegowane muszą kupić kod autoryzacji przed hello użytkownik może logowania i uzyskania interfejsu API sieci web toohello dostępu.

##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Udziel poświadczenia tożsamości aplikacji z klienta OAuth 2.0
1. Użytkownik jest zalogowany tooAzure AD w aplikacji sieci web hello (zobacz hello [tooWeb przeglądarki sieci Web aplikacji](#web-browser-to-web-application) powyżej).
2. Aplikacja sieci web Hello musi tooacquire tokenu dostępu, który można uwierzytelnić interfejsu API sieci web toohello i pobrać hello żądanego zasobu. Powoduje to dodanie tooAzure żądania AD dla punktu końcowego tokena, hello poświadczeń, identyfikator aplikacji i aplikacji sieci web interfejsu API identyfikator URI.
3. Usługi Azure AD uwierzytelnia aplikacji hello i zwraca token dostępu JWT jest interfejs API sieci web hello toocall używane.
4. Przy użyciu protokołu HTTPS aplikacja sieci web hello używa hello zwracane hello tooadd tokenu dostępu JWT ciąg tokenu JWT z oznaczeniem "Bearer" w nagłówku autoryzacji hello hello żądanie toohello interfejsu API sieci web. Interfejs API sieci web Hello następnie weryfikuje hello JWT token, a Jeśli weryfikacja zakończy się pomyślnie, zwraca hello żądanego zasobu.

##### <a name="delegated-user-identity-with-openid-connect"></a>Tożsamość użytkownika delegowanego z OpenID Connect
1. Użytkownik jest zalogowany w aplikacji sieci web tooa przy użyciu usługi Azure AD (zobacz hello [tooWeb przeglądarki sieci Web aplikacji](#web-browser-to-web-application) powyższej sekcji). Jeśli użytkownik hello hello aplikacji sieci web nie zgodził jeszcze tooallowing hello web toocall hello sieci web aplikacji interfejsu API w jego imieniu, hello użytkownicy będą musieli tooconsent. Aplikacja Hello wyświetli hello uprawnienia, które wymaga, a jeśli którakolwiek z tych uprawnień na poziomie administratora, zwykłego użytkownika w katalogu hello nie będą mogli tooconsent. Ten proces zgody dotyczy tylko toomulti dzierżawy, aplikacje nie pojedynczej dzierżawy zgodnie z aplikacji hello mają już hello niezbędne uprawnienia. Podczas hello użytkownik zalogowany, hello aplikacji sieci web odebrał identyfikator tokenu z informacjami o hello użytkownika, a także kod autoryzacji.
2. Przy użyciu kodu autoryzacji hello wystawiony przez usługę Azure AD, hello aplikacji sieci web wysyła żądanie tooAzure Directory token punktu końcowego, który zawiera kod autoryzacji hello, szczegółowe informacje o aplikacji klienckiej hello (identyfikator aplikacji i identyfikator URI przekierowania) i hello żądanego zasobu ( Aplikacja identyfikator URI dla interfejsu API sieci web hello).
3. Kod autoryzacji Hello i informacji na temat interfejsu API sieci web i aplikacji sieci web hello są weryfikowane przez usługę Azure AD. Po pomyślnym zweryfikowaniem usługi Azure AD zwraca dwa tokeny: token JWT dostępu i token odświeżania JWT.
4. Przy użyciu protokołu HTTPS aplikacja sieci web hello używa hello zwracane hello tooadd tokenu dostępu JWT ciąg tokenu JWT z oznaczeniem "Bearer" w nagłówku autoryzacji hello hello żądanie toohello interfejsu API sieci web. Interfejs API sieci web Hello następnie weryfikuje hello JWT token, a Jeśli weryfikacja zakończy się pomyślnie, zwraca hello żądanego zasobu.

##### <a name="delegated-user-identity-with-oauth-20-authorization-code-grant"></a>Tożsamość użytkownika delegowanej za udzielania kodu autoryzacji OAuth 2.0
1. Użytkownik jest już zalogowany tooa aplikacji sieci web, w których mechanizm uwierzytelniania jest niezależna od usługi Azure AD.
2. Witaj aplikacji sieci web wymaga autoryzacji code tooacquire tokenu dostępu, więc emituje żądanie za pośrednictwem punktu końcowego autoryzacji hello przeglądarki tooAzure przez usługi AD, podając identyfikator aplikacji hello i identyfikator URI przekierowania dla aplikacji sieci web powitania po pomyślnym uwierzytelnianie. Witaj użytkownik loguje się tooAzure AD.
3. Jeśli użytkownik hello hello aplikacji sieci web nie zgodził jeszcze tooallowing hello web toocall hello sieci web aplikacji interfejsu API w jego imieniu, hello użytkownicy będą musieli tooconsent. Aplikacja Hello wyświetli hello uprawnienia, które wymaga, a jeśli którakolwiek z tych uprawnień na poziomie administratora, zwykłego użytkownika w katalogu hello nie będą mogli tooconsent. Tej zgody dotyczy aplikacji tooboth pojedynczych i wielu dzierżawców.  W przypadku pojedynczej dzierżawy hello administrator może wykonywać tooconsent zgody administratora w imieniu użytkowników.  Można to zrobić przy użyciu hello `Grant Permissions` przycisku na powitania [Azure Portal](https://portal.azure.com). 
4. Po hello użytkownik zgodził się, aplikacji sieci web hello odbiera kod autoryzacji hello, że wymaga ona tooacquire tokenu dostępu.
5. Przy użyciu kodu autoryzacji hello wystawiony przez usługę Azure AD, hello aplikacji sieci web wysyła żądanie tooAzure Directory token punktu końcowego, który zawiera kod autoryzacji hello, szczegółowe informacje o aplikacji klienckiej hello (identyfikator aplikacji i identyfikator URI przekierowania) i hello żądanego zasobu ( Aplikacja identyfikator URI dla interfejsu API sieci web hello).
6. Kod autoryzacji Hello i informacji na temat interfejsu API sieci web i aplikacji sieci web hello są weryfikowane przez usługę Azure AD. Po pomyślnym zweryfikowaniem usługi Azure AD zwraca dwa tokeny: token JWT dostępu i token odświeżania JWT.
7. Przy użyciu protokołu HTTPS aplikacja sieci web hello używa hello zwracane hello tooadd tokenu dostępu JWT ciąg tokenu JWT z oznaczeniem "Bearer" w nagłówku autoryzacji hello hello żądanie toohello interfejsu API sieci web. Interfejs API sieci web Hello następnie weryfikuje hello JWT token, a Jeśli weryfikacja zakończy się pomyślnie, zwraca hello żądanego zasobu.

#### <a name="code-samples"></a>Przykłady kodu
Zobacz hello przykłady kodu dla scenariuszy interfejsu API tooWeb aplikacji sieci Web. I wrócić tu często — możemy dodać nowe próbki cały czas hello. Web [tooWeb aplikacji interfejsu API](active-directory-code-samples.md#web-application-to-web-api).

#### <a name="registering"></a>Rejestrowanie
* Pojedynczej dzierżawy: Tożsamość aplikacji hello i przypadków tożsamości użytkownika delegowanego hello aplikacji sieci web i hello interfejsu API sieci web musi być zarejestrowana w hello tym samym katalogu w usłudze Azure AD. Witaj interfejsu API sieci web może być skonfigurowany tooexpose zestaw uprawnień, które są używane toolimit hello tej aplikacji sieci web dostęp do zasobów tooits. Jeśli jest używany typ tożsamości użytkownika delegowanego hello aplikacji sieci web musi tooselect hello potrzebne uprawnienia z menu rozwijanego "TooOther uprawnienia aplikacji" hello w hello portalu Azure. Ten krok nie jest wymagane, jeśli typ tożsamości aplikacji hello jest używany.
* Wielodostępne: Najpierw hello aplikacji sieci web jest skonfigurowany tooindicate hello uprawnienia wymaga toobe funkcjonalności. Ta lista wymaganych uprawnień jest wyświetlany w oknie dialogowym, jeśli użytkownik lub administrator w katalogu docelowym hello daje aplikacji toohello zgody, dzięki czemu dostępne tootheir organizacji. Niektóre aplikacje wymagają tylko użytkownika poziomu uprawnień, które każdy użytkownik w organizacji hello można wyrazić zgodę na. Inne aplikacje wymagają uprawnień na poziomie administratora, które użytkownik w organizacji hello nie można wyrazić zgodę na. Tylko administrator katalogu, który pozwala tooapplications zgody, które wymagają tego poziomu uprawnień. Gdy hello zgody użytkownika lub administratora, hello hello i aplikacji sieci web interfejsu API sieci web są oba zarejestrowane w ich katalogu.

#### <a name="token-expiration"></a>Wygaśnięcia tokenu
Gdy hello aplikacji sieci web używa jej tooget kod autoryzacji tokenu JWT dostępu, również odbiera token odświeżania JWT. Po wygaśnięciu tokenu dostępu hello token odświeżania hello mogą być używane toore-uwierzytelnić użytkownika hello bez konieczności ich toosign w ponownie. Ten token odświeżania jest używane tooauthenticate hello użytkownika, nowe dostępu, którego wynikiem token i Odśwież tokenu.

### <a name="daemon-or-server-application-tooweb-api"></a>TooWeb demon lub serwera aplikacji interfejsu API
W tej sekcji opisano demon lub serwera aplikacji, która potrzebuje zasobów tooget z interfejsu API sieci web. Istnieją dwa scenariusze podrzędne, stosowane sekcji toothis: demon wymagające toocall interfejsu API sieci web, oparty na typ przydziału poświadczeń klienta OAuth 2.0; i aplikacji serwera (np. interfejsu API sieci web), która wymaga toocall składnika web API, oparty na OAuth 2.0 On-Behalf-Of specyfikacji wersji roboczej.

W scenariuszu hello podczas demon aplikację toocall interfejs API sieci web jest ważne toounderstand kilka rzeczy. Po pierwsze interakcji z użytkownikiem nie jest możliwe z aplikacją demon, który wymaga toohave aplikacji hello jego tożsamość. Przykładem aplikacji demon jest zadanie wsadowe lub uruchomione w tle hello usługa systemu operacyjnego. Aplikacje tego typu żądania tokenu dostępu przy użyciu tożsamości aplikacji i umożliwienie korzystania z jego identyfikator aplikacji, dostęp do poświadczeń (hasło lub certyfikat) i tooAzure identyfikator URI aplikacji usługi AD. Po pomyślnym uwierzytelnieniu demon hello odbiera token dostępu z usługi Azure AD, która jest następnie używane toocall hello interfejsu API sieci web.

W scenariuszu hello gdy aplikacja serwera wymaga toocall składnika web API, jest przydatne toouse przykład. Załóżmy, że użytkownik został uwierzytelniony w natywnej aplikacji i tej aplikacji natywnej musi toocall interfejs API sieci web. Usługa Azure AD wystawia token JWT dostępu tokenu toocall hello interfejsu API sieci web. Jeśli hello interfejsu API sieci web wymaga toocall inny podrzędny interfejs API sieci web, go za pomocą hello imieniu-przepływ "w" toodelegate hello tożsamości użytkownika i toohello interfejsu API sieci web warstwy drugiego uwierzytelniania.

#### <a name="diagram"></a>Diagram
![Diagram tooWeb interfejsu API demon lub serwera aplikacji](./media/active-directory-authentication-scenarios/daemon_server_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Opis protokołu przepływu
##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>Udziel poświadczenia tożsamości aplikacji z klienta OAuth 2.0
1. Powitania serwera aplikacji musi najpierw tooauthenticate z usługą Azure AD jako, bez interakcji ludzi, takich jak interakcyjne okno logowania jednokrotnego. Powoduje to dodanie tooAzure żądania AD dla punktu końcowego tokena, hello poświadczeń, identyfikator aplikacji i identyfikator URI aplikacji.
2. Usługi Azure AD uwierzytelnia aplikacji hello i zwraca token dostępu JWT jest interfejs API sieci web hello toocall używane.
3. Przy użyciu protokołu HTTPS aplikacja sieci web hello używa hello zwracane hello tooadd tokenu dostępu JWT ciąg tokenu JWT z oznaczeniem "Bearer" w nagłówku autoryzacji hello hello żądanie toohello interfejsu API sieci web. Interfejs API sieci web Hello następnie weryfikuje hello JWT token, a Jeśli weryfikacja zakończy się pomyślnie, zwraca hello żądanego zasobu.

##### <a name="delegated-user-identity-with-oauth-20-on-behalf-of-draft-specification"></a>Tożsamość użytkownika delegowanego ze specyfikacją w imieniu — z wersji próbnej OAuth 2.0
Przepływ Hello omówiony poniżej założono, że użytkownik został uwierzytelniony w innej aplikacji (na przykład aplikacji natywnej) i ich tożsamość użytkownika została tooacquire używany interfejs API sieci web warstwy pierwszej toohello tokenu dostępu.

1. aplikacja macierzysta Hello wysyła hello dostępu tokenu toohello pierwszej warstwy interfejsu API sieci web.
2. Witaj interfejsu API sieci web warstwy pierwszej wysyła żądania tooAzure Directory punktu końcowego tokena, podając jego identyfikator aplikacji i poświadczenia, a także hello tokenu dostępu. Ponadto są wysyłane żądania hello on_behalf_of parametrem, który wskazuje hello nowych żąda interfejsu API sieci web tokeny toocall interfejs API sieci web podrzędne w imieniu hello oryginalnego użytkownika.
3. Usługi Azure AD sprawdza tego hello pierwszej warstwy interfejsu API sieci web ma uprawnienia tooaccess hello podrzędne składnika web API i weryfikuje Żądanie hello zwracanie tokenu JWT dostępu i token JWT interfejsu API sieci web warstwy pierwszej token toohello odświeżania.
4. Przy użyciu protokołu HTTPS sieci web warstwy pierwszej hello, który wywołuje interfejs API hello podrzędne interfejsu API sieci web przez dodanie hello ciąg tokenu w nagłówku autoryzacji hello w żądaniu hello. Witaj interfejsu API sieci web warstwy pierwszej nadal toocall hello podrzędne interfejsu API sieci web tak długo, jak hello token dostępu i tokenów odświeżania są prawidłowe.

#### <a name="code-samples"></a>Przykłady kodu
Zobacz hello przykłady kodu dla scenariuszy tooWeb interfejsu API demon lub serwera aplikacji. I wrócić tu często — możemy dodać nowe próbki cały czas hello. [Serwer lub aplikacja demon tooWeb interfejsu API](active-directory-code-samples.md#server-or-daemon-application-to-web-api)

#### <a name="registering"></a>Rejestrowanie
* Pojedynczej dzierżawy: Tożsamość aplikacji hello i przypadków tożsamości użytkownika delegowanego hello demon lub serwera aplikacji musi być zarejestrowana w hello tym samym katalogu w usłudze Azure AD. Hello interfejsu API sieci web może być skonfigurowany tooexpose zestaw uprawnień, które są używane toolimit hello demon lub zasobów tooits dostępu do serwera. Jeśli jest używany typ tożsamości użytkownika delegowanego powitania serwera aplikacji musi tooselect hello potrzebne uprawnienia z menu rozwijanego "TooOther uprawnienia aplikacji" hello w hello portalu Azure. Ten krok nie jest wymagane, jeśli typ tożsamości aplikacji hello jest używany.
* Wielodostępne: Najpierw hello demon lub serwera aplikacji jest tooindicate skonfigurowane uprawnienia hello wymaga toobe funkcjonalności. Ta lista wymaganych uprawnień jest wyświetlany w oknie dialogowym, jeśli użytkownik lub administrator w katalogu docelowym hello daje aplikacji toohello zgody, dzięki czemu dostępne tootheir organizacji. Niektóre aplikacje wymagają tylko użytkownika poziomu uprawnień, które każdy użytkownik w organizacji hello można wyrazić zgodę na. Inne aplikacje wymagają uprawnień na poziomie administratora, które użytkownik w organizacji hello nie można wyrazić zgodę na. Tylko administrator katalogu, który pozwala tooapplications zgody, które wymagają tego poziomu uprawnień. Gdy użytkownik hello lub administrator wyrazi na to zgody, zarówno hello interfejsów API sieci web są rejestrowane w ich katalogu.

#### <a name="token-expiration"></a>Wygaśnięcia tokenu
Podczas pierwszej aplikacji hello używa jej tooget kod autoryzacji tokenu JWT dostępu, również odbiera token odświeżania JWT. Po wygaśnięciu tokenu dostępu hello token odświeżania hello mogą być używane toore-uwierzytelnić użytkownika hello bez wyświetlania monitu o poświadczenia. Ten token odświeżania jest używane tooauthenticate hello użytkownika, nowe dostępu, którego wynikiem token i Odśwież tokenu.

## <a name="see-also"></a>Zobacz też
[Przewodnik dewelopera usługi Azure Active Directory](active-directory-developers-guide.md)

[Przykłady kodu usługi Azure Active Directory](active-directory-code-samples.md)

[Ważne informacje dotyczące podpisywania przerzucania kluczy w usłudze Azure AD](active-directory-signing-key-rollover.md)

[OAuth 2.0 w usłudze Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx)

