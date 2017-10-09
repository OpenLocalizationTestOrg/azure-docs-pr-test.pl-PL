---
title: "aaaAzure słownik Developer usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Lista warunków dla często używanych koncepcje dla deweloperów usługi Azure Active Directory i funkcji."
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 551512df-46fb-4219-a14b-9c9fc23998ba
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 32a6a6194b8d01409159a2b60263bb66a87a843c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-developer-glossary"></a>Słownik dewelopera usługi Azure Active Directory
Ten artykuł zawiera definicje dla niektórych koncepcje dla deweloperów usługi Azure Active Directory (AD) core hello, które są przydatne podczas nauki opracowywanie aplikacji dla usługi Azure AD.

## <a name="access-token"></a>Token dostępu
Typ [tokenu zabezpieczającego](#security-token) wystawiony przez [serwera autoryzacji](#authorization-server)i używane przez [aplikacji klienckiej](#client-application) w kolejności tooaccess [chroniony serwer zasobów ](#resource-server). Zwykle w formie hello [tokenu Web JSON (JWT)][JWT], hello token stanowią autoryzacji hello przyznane toohello klienta przez hello [właściciel zasobu](#resource-owner), żądany poziom dostępu. Witaj token zawiera wszystkich odpowiednich [oświadczeń](#claim) o podmiotu hello, Włączanie powitania klienta aplikacji toouse go jako formularza poświadczenia podczas uzyskiwania dostępu do zasobu. Eliminuje to potrzebę hello hello zasobów właściciela tooexpose poświadczenia toohello klienta.

Tokeny dostępu są czasami określonego tooas "Użytkownik + aplikacja" lub "App-tylko", w zależności od hello poświadczenia reprezentowanego. Na przykład, jeśli aplikacja kliencka używa:

* ["Kod autoryzacji" udzielania autoryzacji](#authorization-grant), użytkownik końcowy hello uwierzytelnia najpierw jako właściciel zasobu hello, delegowanie toohello autoryzacji tooaccess klienta hello zasobów. powitania klienta uwierzytelnia później podczas uzyskiwania hello tokenu dostępu. Hello token czasami może być określony toomore jako token "Użytkownik + aplikacji", ponieważ reprezentuje on zarówno hello użytkownika, który autoryzowany hello aplikacji klienckiej i aplikacji hello.
* [Udzielania autoryzacji "Poświadczeń klienta"](#authorization-grant)powitania klienta umożliwia uwierzytelnianie wyłącznie hello, działa bez hello zasobów właściciela uwierzytelniania/autoryzacji, co hello token czasami może być określony tooas tokenu "Tylko do aplikacji".

Zobacz [odwołania do usługi Azure AD tokenu] [ AAD-Tokens-Claims] więcej szczegółów.

## <a name="application-manifest"></a>Manifest aplikacji
Funkcja podał hello [portalu Azure][AZURE-portal], która tworzy reprezentację JSON konfiguracji tożsamości aplikacji hello, używany jako mechanizm aktualizacji skojarzone [ Aplikacja] [ AAD-Graph-App-Entity] i [ServicePrincipal] [ AAD-Graph-Sp-Entity] jednostek. Zobacz [manifest aplikacji usługi Azure Active Directory hello opis] [ AAD-App-Manifest] więcej szczegółów.

## <a name="application-object"></a>Obiekt aplikacji
Kiedy należy rejestru/aktualizacji aplikacji w hello [portalu Azure][AZURE-portal], hello portal utworzeń/aktualizacji obiekt aplikacji i odpowiadające mu [obiekt główny usługi](#service-principal-object)dla tego dzierżawcy. obiekt aplikacji Hello *definiuje* hello Konfiguracja tożsamości aplikacji globalnie (za pośrednictwem których ma dostęp do wszystkich dzierżawców), zapewniając szablonu, z którego są odpowiednie obiekty główne usługi  *pochodnych* do użytku lokalnie w czasie wykonywania (w określonym dzierżawcy).

Zobacz [aplikacji i nazwy głównej usługi obiektów] [ AAD-App-SP-Objects] Aby uzyskać więcej informacji.

## <a name="application-registration"></a>Rejestracja aplikacji
W celu tooallow toointegrate aplikacji z a obiektem delegowanym Zarządzanie tożsamościami i dostępem tooAzure funkcji AD, należy je zarejestrować w usłudze Azure AD [dzierżawy](#tenant). Podczas rejestrowania aplikacji z usługą Azure AD, czy podajesz konfiguracji tożsamości aplikacji, dzięki któremu toointegrate z usługą Azure AD i używać funkcji takich jak:

* Niezawodne funkcje zarządzania z logowaniem jednokrotnym przy użyciu usługi Azure AD Identity Management i [OpenID Connect] [ OpenIDConnect] implementacji protokołu
* Obsługiwane przez brokera dostępu zbyt[chronione zasoby](#resource-server) przez [aplikacje klienckie](#client-application), za pomocą usługi Azure AD OAuth 2.0 [serwera autoryzacji](#authorization-server) implementacji
* [Framework zgody](#consent) zarządzania zasobami tooprotected dostępu klienta oparte na autoryzacji właściciela zasobów.

Zobacz [Integrowanie aplikacji z usługą Azure Active Directory] [ AAD-Integrating-Apps] więcej szczegółów.

## <a name="authentication"></a>Uwierzytelnianie
czynność Hello wyzwanie strona uzasadnionych poświadczeń, podając hello podstawy tworzenia zabezpieczeń toobe głównej, używane dla tożsamości i kontroli dostępu. Podczas [udzielania autoryzacji OAuth2](#authorization-grant) na przykład strona hello uwierzytelniania jest wypełnianie hello rolę albo [właściciel zasobu](#resource-owner) lub [aplikacji klienckiej](#client-application), w zależności od Udziel Hello używane.

## <a name="authorization"></a>Autoryzacji
czynność Hello coś udzielanie toodo uprawnienia głównego uwierzytelnionego zabezpieczeń. Istnieją dwa przypadki użycia podstawowy model programowania hello Azure AD:

* Podczas [udzielania autoryzacji OAuth2](#authorization-grant) przepływu: gdy hello [właściciel zasobu](#resource-owner) przyznaje toohello autoryzacji [aplikacji klienckiej](#client-application), umożliwiając tooaccess hello powitania klienta zasoby właściciela zasobów.
* Podczas dostępu do zasobów przez klienta hello: zaimplementowanego hello [serwer zasobów](#resource-server), przy użyciu hello [oświadczeń](#claim) wartości znajdujących się w hello [token dostępu](#access-token) toomake kontroli dostępu decyzje na ich podstawie.

## <a name="authorization-code"></a>Kod autoryzacji
Krótki żyła 'token' podany tooa [aplikacji klienckiej](#client-application) przez hello [punktu końcowego autoryzacji](#authorization-endpoint), jako część przepływu "Kod autoryzacji" hello, hello jednej z czterech OAuth2 [przyznaje autoryzacji ](#authorization-grant). Witaj zostanie zwrócony kod aplikacji klienckiej toohello w tooauthentication odpowiedzi z [właściciel zasobu](#resource-owner), wskazującą właściciel zasobu hello przekazała hello tooaccess autoryzacji wymagane zasoby. W ramach przepływu hello, kod hello później zrealizowane dla [token dostępu](#access-token).

## <a name="authorization-endpoint"></a>Punkt końcowy autoryzacji
Jeden z punktów końcowych hello implementowane przez hello [serwera autoryzacji](#authorization-server), używać toointeract z hello [właściciel zasobu](#resource-owner) w kolejności tooprovide [udzielania autoryzacji](#authorization-grant) podczas Przepływ grant autoryzacji OAuth2. W zależności od autoryzacji hello przyznać przepływu, hello rzeczywiste grant podane mogą się różnić, łącznie z [kod autoryzacji](#authorization-code) lub [tokenu zabezpieczającego](#security-token).

Zobacz specyfikację hello OAuth2 [typy przydziałów autoryzacji] [ OAuth2-AuthZ-Grant-Types] i [punktu końcowego autoryzacji] [ OAuth2-AuthZ-Endpoint] sekcje i hello [Specyfikacji OpenIDConnect] [ OpenIDConnect-AuthZ-Endpoint] więcej szczegółów.

## <a name="authorization-grant"></a>udzielania autoryzacji
Poświadczenie reprezentujący hello [właściciel zasobu](#resource-owner) [autoryzacji](#authorization) tooaccess chronionych zasobów, przyznane tooa [aplikacji klienckiej](#client-application). Aplikacja kliencka można użyć jednej z hello [przyznać cztery typy zdefiniowane przez hello Framework autoryzacji OAuth2] [ OAuth2-AuthZ-Grant-Types] tooobtain grant, w zależności od wymagania typu klienta: "udzielania kodu autoryzacji", " poświadczenia klienta umożliwiają","niejawne Przyznaj"i"przyznać poświadczenia hasła właściciela zasobu". poświadczenie Hello zwrócony toohello klienta albo [token dostępu](#access-token), lub [kod autoryzacji](#authorization-code) (wymieniane później, aby uzyskać token dostępu), w zależności od typu hello udzielania autoryzacji używany.

## <a name="authorization-server"></a>Serwer autoryzacji
Zgodnie z definicją hello [Framework autoryzacji OAuth2][OAuth2-Role-Def], odpowiedzialne za wystawianie dostępu do serwera hello tokeny toohello [klienta](#client-application) po pomyślnym uwierzytelnieniu Witaj [właściciel zasobu](#resource-owner) i uzyskanie jego autoryzacji. A [aplikacji klienckiej](#client-application) współdziała z serwera autoryzacji hello w czasie wykonywania za pośrednictwem jego [autoryzacji](#authorization-endpoint) i [tokenu](#token-endpoint) punktów końcowych, zgodnie z hello OAuth2 zdefiniowany [przyznaje autoryzacji](#authorization-grant).

W przypadku hello integracji aplikacji usługi Azure AD, Azure AD implementuje hello roli serwera autoryzacji dla aplikacji usługi Azure AD i usługi firmy Microsoft interfejsy API, na przykład [Microsoft Graph API][Microsoft-Graph].

## <a name="claim"></a>Oświadczenia
A [tokenu zabezpieczającego](#security-token) zawiera oświadczenia, które zapewniają potwierdzenia jednostek o jednym (takich jak [aplikacji klienckiej](#client-application) lub [właściciel zasobu](#resource-owner)) jednostki tooanother (na przykład hello [serwer zasobów](#resource-server)). Oświadczenia są pary nazwa/wartość, które przekazywania faktów temat tokenu hello (na przykład podmiotu zabezpieczeń hello, który został uwierzytelniony przez hello [serwera autoryzacji](#authorization-server)). token zawiera danego oświadczenia Hello są zależne od kilku zmiennych, takie jak typ hello tokenu, hello typ poświadczeń używanych tooauthenticate hello podmiotu, Konfiguracja aplikacji hello itp.

Zobacz [odwołania do tokenu usługi Azure AD] [ AAD-Tokens-Claims] więcej szczegółów.

## <a name="client-application"></a>Aplikacja kliencka
Zgodnie z definicją hello [Framework autoryzacji OAuth2][OAuth2-Role-Def], aplikacji, która sprawia, że chroniony żądania zasobów w imieniu hello [właściciel zasobu](#resource-owner). Hello termin "klient" oznacza wszystkie właściwości wykonania konkretnego sprzętu (na przykład, czy aplikacja hello jest wykonywana na serwerze, pulpitu lub innych urządzeniach).  

Aplikacja kliencka żąda [autoryzacji](#authorization) z tooparticipate właściciela zasobu, w [udzielania autoryzacji OAuth2](#authorization-grant) przepływu i może uzyskać dostępu do interfejsów API/danych w imieniu właściciela zasobów hello. Witaj Framework autoryzacji OAuth2 [definiują dwa typy klientów][OAuth2-Client-Types]"poufne dane" i "public", oparte na powitania klienta możliwości toomaintain hello poufności swoich poświadczeń. Aplikacje można wdrożyć [klienta sieci web (poufne)](#web-client) na serwerze sieci web, które są uruchamiane [aplikacja native client (publicznej)](#native-client) zainstalowana na urządzeniu, lub [na podstawie agent użytkownika klienta (publicznej)](#user-agent-based-client)które są uruchamiane w przeglądarce urządzenia.

## <a name="consent"></a>Zgody
Witaj proces [właściciel zasobu](#resource-owner) udzielania autoryzacji tooa [aplikacji klienckiej](#client-application), tooaccess chronionych zasobów w ramach określonego [uprawnienia](#permissions), imieniu hello właściciel zasobu. W zależności od uprawnień hello żądany przez klienta hello administrator lub użytkownik zostanie poproszony o zgodę tooallow dostępu tootheir organizacji/poszczególnych danych odpowiednio. Uwaga: w [wielodostępne](#multi-tenant-application) scenariusza, aplikacji hello [nazwy głównej usługi](#service-principal-object) jest zarejestrowany w dzierżawie powitalnych hello zgodę użytkownika.

## <a name="id-token"></a>Identyfikator tokenu
[OpenID Connect] [ OpenIDConnect-ID-Token] [tokenu zabezpieczającego](#security-token) dostarczonych przez [serwera autoryzacji](#authorization-server) [punktu końcowego autoryzacji](#authorization-endpoint), który zawiera [oświadczeń](#claim) dotyczące uwierzytelniania toohello użytkownika końcowego [właściciel zasobu](#resource-owner). Podobnie jak tokenu dostępu, tokeny Identyfikatora również są przedstawiane jako cyfrowo podpisanych [tokenu Web JSON (JWT)][JWT]. W przeciwieństwie do tokenu dostępu, token identyfikator oświadczenia nie są używane do celów pokrewne tooresource dostępu i specjalnie kontroli dostępu.

Zobacz [odwołania do tokenu usługi Azure AD] [ AAD-Tokens-Claims] więcej szczegółów.

## <a name="multi-tenant-application"></a>wielodostępne aplikacji
Klasa aplikacji, która umożliwia logowanie i [zgody](#consent) przez użytkowników udostępniane w dowolnym usługi Azure AD [dzierżawy](#tenant), tym dzierżawcy innej niż hello jedną rejestracji powitania klienta. [Aplikacja Native client](#native-client) aplikacje są wielodostępne domyślnie, natomiast [klienta sieci web](#web-client) i [zasobów/interfejs API sieci web](#resource-server) aplikacje mają tooselect możliwości hello między jednym lub wieloma dzierżawcami. Z drugiej strony aplikacji sieci web zarejestrowany jako pojedynczej dzierżawy, tylko umożliwiałyby logowania z kont użytkowników udostępniane w hello sam dzierżawy jako hello jedną gdzie aplikacja hello jest zarejestrowana.

Zobacz [jak toosign w dowolnej usługi Azure AD użytkownika za pomocą hello wzorzec wielodostępnych aplikacji] [ AAD-Multi-Tenant-Overview] więcej szczegółów.

## <a name="native-client"></a>Aplikacja Native client
Typ [aplikacji klienckiej](#client-application) oryginalnie zainstalowana na urządzeniu. Ponieważ cały kod jest wykonywane na urządzeniu, jest traktowane jako "public" klienta powodu tooits brakiem toostore poświadczenia prywatnie/jako poufne. Zobacz [OAuth2 klienta typów i profile] [ OAuth2-Client-Types] więcej szczegółów.

## <a name="permissions"></a>Uprawnienia
A [aplikacji klienckiej](#client-application) uzyskują dostęp do tooa [serwer zasobów](#resource-server) przez zadeklarowanie żądanych uprawnień. Dostępne są dwa typy:

* "Delegowane" uprawnienia, które określają [zakresu](#scopes) dostępu za pomocą delegowanego autoryzacji z hello zalogowany [właściciel zasobu](#resource-owner), są prezentowane toohello zasobów w czasie wykonywania jako ["punkt połączenia usługi "oświadczenia](#claim) powitania klienta [token dostępu](#access-token).
* Uprawnienia "Aplikacja", które określają [opartej na rolach](#roles) uzyskiwać dostęp za pomocą poświadczeń/tożsamości powitania klienta aplikacji, są prezentowane toohello zasobów w czasie wykonywania jako [oświadczenia "role"](#claim) w hello token dostępu klienta.

Również powierzchni, podczas hello [zgody](#consent) procesu, podając hello administrator lub zasobu właściciela hello możliwości toogrant/niezezwalania powitania klienta dostępu tooresources w swojej dzierżawy.

Żądania uprawnień są skonfigurowane na powitania "Aplikacji" / "Ustawienia" karcie hello [portalu Azure][AZURE-portal], w obszarze "Wymaga uprawnień", wybierając hello potrzeby "Delegowane uprawnienia" i " Uprawnienia aplikacji"(hello ostatnie wymagane jest członkostwo w roli administratora globalnego hello). Ponieważ [publicznego klienta](#client-application) nie może bezpiecznie Obsługa poświadczeń, może zażądać jedynie delegowane uprawnienia podczas [poufne klienta](#client-application) ma hello możliwości toorequest aplikacją i delegowanego uprawnienia. powitania klienta [obiektu aplikacji](#application-object) hello magazynów zadeklarowany uprawnienia w jego [właściwości requiredResourceAccess][AAD-Graph-App-Entity].

## <a name="resource-owner"></a>właściciel zasobu
Zgodnie z definicją hello [Framework autoryzacji OAuth2][OAuth2-Role-Def], możliwość przyznania dostępu tooa jednostki chronionych zasobów. Jeśli właściciel zasobu hello jest osobą, jest tooas określonego użytkownika końcowego. Na przykład, jeśli [aplikacji klienckiej](#client-application) chce tooaccess skrzynek pocztowych użytkowników za pośrednictwem hello [interfejsu API programu Microsoft Graph][Microsoft-Graph], wymaga uprawnień od właściciela zasobu hello Witaj skrzynki pocztowej.

## <a name="resource-server"></a>serwer zasobów
Zgodnie z definicją hello [Framework autoryzacji OAuth2][OAuth2-Role-Def], serwer hostów ochronę zasobów mogą akceptować i odpowiada zasobów tooprotected żądań przez [klienta aplikacje](#client-application) tego obecnie [token dostępu](#access-token). Znanej także jako serwer chronionych zasobów lub zasobów aplikacji.

Serwer zasobów udostępnia interfejsy API i wymusza dostęp do zasobów tooits chronione za pomocą [zakresy](#scopes) i [ról](#roles), przy użyciu hello OAuth 2.0 autoryzacji Framework. Przykładami hello Azure AD Graph API, co zapewnia dostęp do danych dzierżawy tooAzure AD i Office 365 API, zapewniających toodata dostępu, takich jak Poczta i kalendarz hello. Oba te są również dostępne za pośrednictwem hello [interfejsu API programu Microsoft Graph][Microsoft-Graph].  

Podobnie jak aplikacja kliencka, konfiguracja tożsamości aplikacji zasobów zostanie nawiązane za pośrednictwem [rejestracji](#application-registration) w dzierżawie usługi Azure AD, zapewniając zarówno aplikacji hello i obiekt główny usługi. Niektóre firmy Microsoft interfejsy API, takich jak hello Azure AD Graph API, wstępnie zarejestrowane nazwy główne usług dostępnych w wszystkich dzierżawców podczas inicjowania obsługi.

## <a name="roles"></a>role
Podobnie jak [zakresy](#scopes), role umożliwiają [serwer zasobów](#resource-server) toogovern tooits dostęp do chronionych zasobów. Istnieją dwa typy: "rola" implementuje kontroli dostępu opartej na rolach dla użytkowników/grupy, które wymagają dostępu do zasobu toohello, podczas gdy implementuje rolę "aplikacji" hello takie same dla [aplikacje klienckie](#client-application) wymagających dostępu.

Role są zdefiniowane zasobów ciągów (na przykład "osoba zatwierdzająca wydatków", "Tylko do odczytu", "Directory.ReadWrite.All"), zarządzane w hello [portalu Azure] [ AZURE-portal] za pośrednictwem hello zasobów [aplikacji Manifest](#application-manifest)i przechowywane w zasobie hello [właściwości appRoles][AAD-Graph-Sp-Entity]. Witaj Azure portal to również użytkowników używane tooassign zbyt ról "użytkownika" i skonfiguruj klienta [uprawnienia aplikacji](#permissions) tooaccess rolę "aplikacji".

Szczegółowe omówienie ról aplikacji hello udostępnianych przez interfejs API programu Graph usługi Azure AD, zobacz [zakresy uprawnień interfejsu API Graph][AAD-Graph-Perm-Scopes]. Na przykład implementacji krok po kroku, zobacz [oparta na rolach kontrola dostępu w aplikacji w chmurze przy użyciu usługi Azure AD][Duyshant-Role-Blog].

## <a name="scopes"></a>Zakresy
Podobnie jak [ról](#roles), zakresy umożliwiają [serwer zasobów](#resource-server) toogovern tooits dostęp do chronionych zasobów. Zakresy są używane tooimplement [zakresu] [ OAuth2-Access-Token-Scopes] kontroli dostępu, aby uzyskać [aplikacji klienckiej](#client-application) który ma dostęp delegowany toohello zasobów przez jego właściciela.

Zakresy są zdefiniowane zasobów ciągów (na przykład "Mail.Read", "Directory.ReadWrite.All"), zarządzane w hello [portalu Azure] [ AZURE-portal] za pośrednictwem zasobów hello [manifest aplikacji](#application-manifest)i przechowywane w zasobie hello [właściwości oauth2Permissions][AAD-Graph-Sp-Entity]. Hello Azure portal to również tooconfigure używanych aplikacji klienckiej [delegowane uprawnienia](#permissions) tooaccess zakresu.

Najlepsze praktyki konwencji nazewnictwa, jest toouse format "resource.operation.constraint". Szczegółowe omówienie zakresy hello udostępnianych przez interfejs API programu Graph usługi Azure AD, zobacz [zakresy uprawnień interfejsu API Graph][AAD-Graph-Perm-Scopes]. Dla zakresów udostępnianych przez usługi Office 365, zobacz [odwołania uprawnień interfejsu API usługi Office 365][O365-Perm-Ref].

## <a name="security-token"></a>token zabezpieczający
Podpisanego dokumentu zawierające te oświadczenia, takich jak tokenu OAuth2 lub potwierdzenia SAML 2.0. Dla OAuth2 [udzielania autoryzacji](#authorization-grant), [token dostępu](#access-token) (OAuth2) i [Token Identyfikatora](http://openid.net/specs/openid-connect-core-1_0.html#IDToken) są typy tokenów zabezpieczających, które są zaimplementowane jako [JSON Sieci Web Token (JWT)][JWT].

## <a name="service-principal-object"></a>Obiekt główny usługi
Po należy zarejestrować/aktualizacji aplikacji w hello [portalu Azure][AZURE-portal], hello portal utworzeń/aktualizacji zarówno [obiektu aplikacji](#application-object) i odpowiednie nazwy głównej usługi obiekt dla tego dzierżawcy. obiekt aplikacji Hello *definiuje* hello globalnie (za pośrednictwem wszystkich dzierżaw gdzie aplikacja hello skojarzone udzielono dostępu), konfiguracja tożsamości aplikacji i hello szablonu, z którego jest jego odpowiedniej usługi Obiekty główne są *pochodnych* do użytku lokalnie w czasie wykonywania (w określonym dzierżawcy).

Zobacz [aplikacji i nazwy głównej usługi obiektów] [ AAD-App-SP-Objects] Aby uzyskać więcej informacji.

## <a name="sign-in"></a>Logowanie
Witaj proces [aplikacji klienckiej](#client-application) inicjowanie uwierzytelniania użytkownika końcowego i przechwytywanie dotyczące stanu hello w celu uzyskania [tokenu zabezpieczającego](#security-token) i określania zakresu toothat sesji aplikacji hello Stan. Stanu może zawierać artefaktów na przykład informacje o profilu użytkownika i informacji pochodzących z tokenu oświadczeń.

Hello logowania funkcja aplikacji jest zwykle używane tooimplement jednokrotnej (SSO). Go może być poprzedzone funkcję "zapisywania do" jako punkt wejścia hello aplikacji tooan toogain dostępu użytkownika końcowego (na po w wypadku pierwszego logowania). Hello rejestracji funkcji jest używane toogather utrwalić stanu dodatkowe toohello określonego użytkownika i może wymagać [zgody użytkownika](#consent).

## <a name="sign-out"></a>wylogowania
Witaj proces odinstalowywania uwierzytelniający użytkownika końcowego, odłączenie hello stanu użytkownika, skojarzone z hello [aplikacji klienckiej](#client-application) sesji podczas [logowania](#sign-in)

## <a name="tenant"></a>Dzierżawy
Wystąpienie katalogu usługi Azure AD jest określony tooas dzierżawa usługi Azure AD. Zapewnia szereg funkcji, takich jak:

* Usługa rejestru dla zintegrowanych aplikacji
* Uwierzytelnianie konta użytkowników i zarejestrowanych aplikacji
* Punkty końcowe REST wymagane toosupport różnych protokołów, w tym OAuth2 i SAML, w tym hello [punktu końcowego autoryzacji](#authorization-endpoint), [punktu końcowego tokena](#token-endpoint) i Witaj "typowych" punktowi końcowemu używanemu przez [ aplikacje wielodostępne](#multi-tenant-application).

Dzierżawa jest także powiązany z usługą Azure AD lub subskrypcji usługi Office 365 podczas inicjowania obsługi administracyjnej subskrypcji hello, takim funkcjom tożsamość i zarządzanie dostępem hello subskrypcji. Zobacz [jak dzierżawy usługi Azure Active Directory tooget] [ AAD-How-To-Tenant] szczegółowe informacje na temat hello różne sposoby uzyskania dostępu tooa dzierżawy. Zobacz [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory] [ AAD-How-Subscriptions-Assoc] szczegółowe informacje na temat hello relacji między subskrypcjami i dzierżawa usługi Azure AD.

## <a name="token-endpoint"></a>Token punktu końcowego
Jeden z punktów końcowych hello implementowane przez hello [serwera autoryzacji](#authorization-server) toosupport OAuth2 [przyznaje autoryzacji](#authorization-grant). W zależności od hello grant może być używane tooacquire [token dostępu](#access-token) (i powiązanych "Odśwież" token) tooa [klienta](#client-application), lub [token Identyfikatora](#ID-token) w przypadku użycia z hello [ OpenID Connect] [ OpenIDConnect] protokołu.

## <a name="user-agent-based-client"></a>Na podstawie agent użytkownika klienta
Typ [aplikacji klienckiej](#client-application) pobierania kodu z serwera sieci web i wykonuje w agent użytkownika (na przykład przeglądarki sieci web), takich jak jednej strony aplikacji JEDNOSTRONICOWEJ. Ponieważ cały kod jest wykonywane na urządzeniu, jest traktowane jako "public" klienta powodu tooits brakiem toostore poświadczenia prywatnie/jako poufne. Zobacz [OAuth2 klienta typów i profile] [ OAuth2-Client-Types] więcej szczegółów.

## <a name="user-principal"></a>głównej nazwy użytkownika
Toohello podobnie obiekt główny usługi jest używane toorepresent wystąpienia aplikacji, obiekt główny użytkownik jest innego typu podmiot zabezpieczeń, który reprezentuje użytkownika. Hello Azure AD Graph [jednostki użytkownika] [ AAD-Graph-User-Entity] definiuje hello schematu dla obiektu użytkownika, w tym właściwości skojarzone z użytkownikiem, takie jak imię i nazwisko, główna nazwa użytkownika, członkostwo w roli katalogu itp. Zapewnia to hello Konfiguracja tożsamości użytkownika dla usługi Azure AD tooestablish użytkownika podmiotu zabezpieczeń w czasie wykonywania. Hello głównej nazwy użytkownika jest używana toorepresent uwierzytelnionego użytkownika dla logowania jednokrotnego, rejestrowanie [zgody](#consent) delegowania, co decyzje dotyczące kontroli dostępu, itd.

## <a name="web-client"></a>Klient sieci Web
Typ [aplikacji klienckiej](#client-application) , który jest wykonywany całego kodu na serwerze sieci web i stanie toofunction jako "poufne dane" klienta przez bezpieczne przechowywanie swoich poświadczeń na powitania serwera. Zobacz [OAuth2 klienta typów i profile] [ OAuth2-Client-Types] więcej szczegółów.

## <a name="next-steps"></a>Następne kroki
Witaj [przewodnik dewelopera usługi Azure AD] [ AAD-Dev-Guide] toouse portalu hello rozwoju usługi Azure AD jest powiązanych tematów, w tym omówienie [integracji aplikacji] [ AAD-How-To-Integrate] i podstawy hello [uwierzytelniania usługi Azure AD i scenariusze obsługiwane uwierzytelniania][AAD-Auth-Scenarios].

Użyj powitania po opinii tooprovide sekcji komentarzy i pomóc nam dostosować i kształtu zawartość, włącznie z żądaniami dostępność nowych definicji lub aktualizowania istniejących!

<!--Image references-->

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-Subscriptions-Assoc]: ../active-directory-how-subscriptions-associated-directory.md
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-How-To-Tenant]: active-directory-howto-tenant.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Multi-Tenant-Overview]: active-directory-devhowto-multi-tenant-overview.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[Microsoft-Graph]: https://graph.microsoft.io
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Endpoint]: https://tools.ietf.org/html/rfc6749#section-3.1
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-AuthZ-Endpoint]: http://openid.net/specs/openid-connect-core-1_0.html#AuthorizationEndpoint
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken
