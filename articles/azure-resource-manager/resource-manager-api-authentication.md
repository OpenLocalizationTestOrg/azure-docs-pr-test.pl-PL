---
title: "aaaAzure usługi Active Directory uwierzytelniania i Resource Manager | Dokumentacja firmy Microsoft"
description: "Developer's guide tooauthentication hello interfejsu API usługi Azure Resource Manager i usługi Azure Active Directory do integracji aplikacji z innych subskrypcji platformy Azure."
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a>Użyj subskrypcje tooaccess uwierzytelniania interfejsu API usługi Resource Manager
## <a name="introduction"></a>Wprowadzenie
Jeśli jesteś deweloper oprogramowania, który wymaga toocreate aplikację, która zarządza zasobami Azure klienta, w tym temacie przedstawiono, jak tooauthenticate z hello interfejsów API usługi Azure Resource Manager i uzyskanie dostępu tooresources w innych subskrypcji.

Aplikację można uzyskać dostęp do hello interfejsów API Menedżera zasobów kilka sposobów:

1. **Użytkownik i uzyskania dostępu do aplikacji**: dla aplikacji, które uzyskują dostęp do zasobów w imieniu zalogowanego użytkownika. Ta metoda działa w przypadku aplikacji, takich jak aplikacje sieci web i narzędzia wiersza polecenia, które zajmują się tylko "interakcyjne Zarządzanie" zasobów platformy Azure.
2. **Dostęp tylko do aplikacji**: dla aplikacji uruchamianych demon usługi i zaplanowanych zadań. tożsamość aplikacji Hello uzyskuje bezpośredni dostęp do zasobów toohello. Ta metoda działa w przypadku aplikacji potrzebnych długoterminowej tooAzure bezobsługowe dostępu (Instalacja nienadzorowana).

Ten temat zawiera instrukcje krok po kroku toocreate aplikację, która jest stosowana w obu tych metod autoryzacji. Pokazuje, jak tooperform każdego kroku z interfejsu API REST lub C#. kompletna aplikacja platformy ASP.NET MVC Hello jest dostępna na [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).

## <a name="what-hello-web-app-does"></a>Jakie hello aplikacja sieci web nie
Witaj aplikacji sieci web:

1. Logowania użytkownika w usłudze Azure.
2. Pyta użytkownika toogrant hello sieci web aplikacji dostępu tooResource Manager.
3. Pobiera użytkownika + tokenu dostępu aplikacji do uzyskiwania dostępu do Menedżera zasobów.
4. Używa toocall tokenu (z kroku 3) Menedżera zasobów i aplikacji hello Przypisz usługi tooa głównej roli hello subskrypcję, która zapewnia hello aplikacji długoterminowej dostępu toohello subskrypcji.
5. Pobiera token dostępu tylko do aplikacji.
6. Używa zasobów toomanage tokenu (z kroku 5) w subskrypcji hello za pomocą Menedżera zasobów.

Poniżej przedstawiono przepływ end-to-end hello hello aplikacji sieci web.

![Przepływ uwierzytelniania usługi Resource Manager](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

Jako użytkownik, podaj identyfikator subskrypcji hello hello subskrypcji ma toouse:

![Podaj identyfikator subskrypcji](./media/resource-manager-api-authentication/sample-ux-1.png)

Wybierz hello toouse konta do logowania.

![Wybierz konto](./media/resource-manager-api-authentication/sample-ux-2.png)

Wprowadź swoje poświadczenia.

![Podaj poświadczenia](./media/resource-manager-api-authentication/sample-ux-3.png)

Przyznaj tooyour dostępu aplikacji hello subskrypcji platformy Azure:

![Udzielanie dostępu](./media/resource-manager-api-authentication/sample-ux-4.png)

Zarządzanie subskrypcjami połączone:

![Łączenie subskrypcji](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a>Zarejestrować aplikację
Przed rozpoczęciem kodowania, należy zarejestrować aplikacji sieci web z usługi Azure Active Directory (AD). Rejestracja aplikacji Hello tworzy centralnej tożsamości aplikacji w usłudze Azure AD. Przechowuje podstawowe informacje o aplikacji, takich jak identyfikator klienta OAuth, adresy URL odpowiedzi i poświadczenia do użycia w tooauthenticate i dostępu do interfejsów API usługi Azure Resource Manager. Rejestracja aplikacji Hello rejestruje także hello różnych delegowane uprawnienia, które aplikacja wymaga podczas uzyskiwania dostępu do APIs firmy Microsoft w imieniu użytkownika hello.

Ponieważ aplikacja uzyskuje dostęp do innych subskrypcji, należy go skonfigurować jako aplikacji wielodostępnej. Sprawdzanie poprawności toopass, podaj domeny skojarzonych z usługą Azure Active Directory. domeny hello toosee skojarzone z usługi Azure Active Directory, zaloguj toohello [klasyczny portal](https://manage.windowsazure.com). Wybierz w usłudze Azure Active Directory, a następnie wybierz **domen**.

Witaj poniższy przykład pokazuje, jak tooregister hello aplikacji przy użyciu programu Azure PowerShell. Musi mieć hello najnowszej wersji (sierpnia 2016) programu Azure PowerShell dla toowork tego polecenia.

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

toolog w jako hello aplikacji usługi AD, potrzebujesz identyfikatora aplikacji hello i hasło. Identyfikator aplikacji hello toosee, który jest zwracana z hello poprzedniego polecenia, użyj:

    $app.ApplicationId

Witaj poniższy przykład pokazuje, jak tooregister hello aplikacji przy użyciu wiersza polecenia platformy Azure.

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

Witaj wyniki zawierają hello AppId, który jest wymagany podczas uwierzytelniania jako aplikacja hello.

### <a name="optional-configuration---certificate-credential"></a>Konfiguracja opcjonalna — certyfikat poświadczeń
Usługi Azure AD obsługuje również certyfikat poświadczeń dla aplikacji: utwórz samopodpisany certyfikat lub Zachowaj hello klucza prywatnego i Dodaj Rejestracja aplikacji hello tooyour klucza publicznego usługi Azure AD. W przypadku uwierzytelniania aplikacji wysyła tooAzure ładunku małych, AD podpisany przy użyciu klucza prywatnego i Azure AD sprawdza podpis hello przy użyciu hello klucza publicznego, który został zarejestrowany.

Dla informacji o tworzeniu aplikacji AD przy użyciu certyfikatu znajduje się w temacie [toocreate programu Azure PowerShell Użyj nazwy głównej usługi zasobów tooaccess](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) lub [toocreate wiersza polecenia platformy Azure Użyj nazwy głównej usługi zasobów tooaccess](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).

## <a name="get-tenant-id-from-subscription-id"></a>Uzyskanie identyfikatora dzierżawy z identyfikatorem subskrypcji
toorequest token, który może być używane toocall Resource Manager, aplikacja musi tooknow hello dzierżawy identyfikator dzierżawy hello Azure AD, która obsługuje hello subskrypcji platformy Azure. Prawdopodobnie użytkownicy wiedzą, ich identyfikatorów subskrypcji, ale nie będzie wiadomo, ich dzierżawy identyfikatorów dla usługi Azure Active Directory. tooget hello użytkownika identyfikator dzierżawy, poprosić użytkownika hello hello subskrypcji o identyfikatorze. Podaj ten identyfikator subskrypcji, wysyłając żądanie dotyczące subskrypcji hello:

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

Witaj żądanie kończy się niepowodzeniem, ponieważ hello użytkownik nie zalogował jeszcze, ale można pobrać identyfikatora dzierżawcy hello z hello odpowiedzi. W tym wyjątku pobrać identyfikator dzierżawcy hello hello wartość nagłówka odpowiedzi dla **WWW-Authenticate**. Zobacz to implementacja hello [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) metody.

## <a name="get-user--app-access-token"></a>Pobierz użytkownika + tokenu dostępu do aplikacji
Aplikacja przekierowuje hello tooAzure użytkownika usługi Active Directory z OAuth 2.0 autoryzować żądania - tooauthenticate hello poświadczenia użytkownika i wrócić kod autoryzacji. Aplikacja używa tooget kod autoryzacji hello tokenu dostępu dla Menedżera zasobów. Witaj [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) metoda tworzy hello żądania autoryzacji.

W tym temacie przedstawiono hello interfejsu API REST żądań tooauthenticate hello użytkownika. Umożliwia także pomocnika bibliotek tooperform uwierzytelniania w kodzie. Aby uzyskać więcej informacji o tych bibliotek, zobacz [bibliotek uwierzytelniania usługi Azure Active Directory](../active-directory/active-directory-authentication-libraries.md). Aby uzyskać instrukcje dotyczące integrowania zarządzania tożsamością w aplikacji, zobacz [przewodnik dewelopera usługi Azure Active Directory](../active-directory/active-directory-developers-guide.md).

### <a name="auth-request-oauth-20"></a>Żądanie uwierzytelniania (OAuth 2.0)
Wystawiać Open ID Connect/OAuth2.0 autoryzacji żądania toohello usługi Azure AD punktu końcowego autoryzacji:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

Witaj parametrów ciągu zapytania, które są dostępne dla tego żądania są opisane w hello [kod autoryzacji żądania](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) tematu.

powitania po przykładzie pokazano, jak toorequest OAuth2.0 autoryzacji:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

Usługi Azure AD uwierzytelnia użytkownika hello, a w razie potrzeby zapyta hello użytkownika toogrant uprawnienia toohello aplikacji. Zwraca toohello kod autoryzacji hello adres URL odpowiedzi aplikacji. W zależności od hello zażądał response_mode, usługi Azure AD albo wysyła ponownie hello danych w ciągu zapytania lub jako dane post.

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a>Żądanie uwierzytelniania (Open ID Connect)
Jeśli nie tylko ma tooaccess usługi Azure Resource Manager w imieniu użytkownika hello, ale również umożliwić hello toosign użytkownika w aplikacji tooyour przy użyciu konta usługi Azure AD, należy wydać Open ID autoryzować żądania połączenia. Z Open ID Connect aplikacja odbiera żądaniu z usługi Azure AD aplikacji można użyć toosign w hello użytkownika.

Witaj parametrów ciągu zapytania, które są dostępne dla tego żądania są opisane w hello [żądanie logowania hello wysłania](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) tematu.

Oto przykład Open ID Connect żądania jest:

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

Usługi Azure AD uwierzytelnia użytkownika hello, a w razie potrzeby zapyta hello użytkownika toogrant uprawnienia toohello aplikacji. Zwraca toohello kod autoryzacji hello adres URL odpowiedzi aplikacji. W zależności od hello zażądał response_mode, usługi Azure AD albo wysyła ponownie hello danych w ciągu zapytania lub jako dane post.

Przykład Open ID Connect odpowiedzi to:

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a>Żądania tokenu (OAuth2.0 Code Grant Flow)
Teraz, gdy aplikacja otrzymał hello kod autoryzacji z usługi Azure AD, jest token dostępu hello tooget czasu dla Menedżera zasobów Azure.  Opublikuj OAuth2.0 Code Grant Token żądania toohello Azure AD Token punktu końcowego:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Witaj parametrów ciągu zapytania, które są dostępne dla tego żądania są opisane w hello [kodu autoryzacji hello](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) tematu.

Witaj poniższy przykład przedstawia żądania tokenu grant kodu z poświadczeniami hasło:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Podczas pracy z poświadczeń certyfikatu, Utwórz tokenu Web JSON (JWT) i znak (RSA SHA256) przy użyciu klucza prywatnego hello aplikacji certyfikatu poświadczenia. Witaj oświadczenia dla tokenu hello są wyświetlane w [oświadczeń tokenu JWT](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims). Aby informacje, zobacz hello [kod biblioteki uwierzytelniania Active Directory (.NET)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign tokenów JWT potwierdzenia klienta.

Zobacz hello [specyfikację Open ID Connect](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) szczegółowe informacje dotyczące uwierzytelniania klientów.

Witaj poniższy przykład przedstawia żądania tokenu grant kodu z poświadczeniami certyfikatu:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

Oto przykład odpowiedzi dla kodu umożliwić token:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a>Obsługa odpowiedzi tokenu grant kodu
Odpowiedź oznaczająca Powodzenie tokenu zawiera token dostępu hello (użytkownik + aplikacji) dla usługi Azure Resource Manager. Aplikacja używa tego dostępu tokenu tooaccess Menedżera zasobów w imieniu użytkownika hello. Witaj okres istnienia tokenów dostępu wystawiony przez usługę Azure AD to jedna godzina. Jest mało prawdopodobne, że aplikacja sieci web wymaga tokenu dostępu toorenew hello (użytkownik + aplikacji). Wymaga tokenu dostępu hello toorenew, użyj token odświeżania hello odbierająca aplikacja hello odpowiedzi tokenu. Opublikuj żądania tokenu OAuth2.0 toohello Azure AD Token punktu końcowego:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Witaj toouse parametry z żądaniem odświeżania hello są opisane w [odświeżanie tokenu dostępu hello](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).

Witaj poniższy przykład przedstawia sposób toouse hello odświeżać token:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Tokeny odświeżania mogą być używane tooget nowe tokeny dostępu dla usługi Azure Resource Manager, nie są one odpowiednie dla dostęp w trybie offline przez aplikację. okres istnienia tokenów odświeżania Hello jest ograniczona, a tokeny odświeżania są powiązane toohello użytkownika. Jeśli odejdzie użytkownik, hello hello organizacji, za pomocą tokenu odświeżania hello aplikacji hello utracenia dostępu. Ta metoda nie jest odpowiedni dla aplikacji, które są używane przez zespoły toomanage ich zasobów platformy Azure.

## <a name="check-if-user-can-assign-access-toosubscription"></a>Sprawdź, czy użytkownika można przypisać toosubscription dostępu
Teraz aplikacja ma tooaccess tokenu usługi Azure Resource Manager imieniu hello użytkownika. Witaj, następnym krokiem jest tooconnect subskrypcji toohello aplikacji. Po nawiązaniu połączenia aplikacji można zarządzać te subskrypcje, nawet wtedy, gdy użytkownik hello nie jest obecny (długoterminowej dostęp w trybie offline).

Dla każdego tooconnect subskrypcji wywołać hello [uprawnienia listy Resource Manager](https://docs.microsoft.com/rest/api/authorization/permissions) toodetermine interfejsu API czy hello użytkownika ma uprawnienia do zarządzania dostępu hello subskrypcji.

Witaj [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) metody ASP.NET MVC Przykładowa aplikacja hello implementuje tego wywołania.

powitania po przykładzie pokazano, jak toorequest uprawnienia użytkownika do subskrypcji. 83cfe939-2402-4581-b761-4f59b0a041e4 jest identyfikatorem hello hello subskrypcji.

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

Przykład Witaj odpowiedzi tooget uprawnień użytkownika w subskrypcji jest:

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

uprawnienia Hello interfejsu API zwraca wiele uprawnień. Wszystkie uprawnienia składa się z dozwolonych akcji (Akcje) i niedopuszczalne akcje (notactions). Jeśli akcja jest obecny w hello dozwolone akcje lista żadnych uprawnień i nie znajduje się liście notactions hello te uprawnienia, użytkownik hello jest dozwolone tooperform tej akcji. **Microsoft.Authorization/RoleAssignments/Write** jest akcja hello management rights która udziela dostępu. Aplikacja musi przeanalizować hello uprawnienia wynik toolook wyrażenia regularnego dopasowanie ciągu tej akcji w działaniach hello i notactions każdego uprawnienia.

## <a name="get-app-only-access-token"></a>Uzyskaj token dostępu tylko do aplikacji
Teraz wiesz, jeśli użytkownik hello można przypisać toohello dostępu do subskrypcji platformy Azure. Następne kroki Hello są:

1. Przypisz hello odpowiednie RBAC roli tooyour tożsamości aplikacji hello subskrypcji.
2. Sprawdź poprawność hello przypisania dostępu przez wykonanie zapytania dotyczącego aplikacji hello uprawnienia subskrypcji hello lub uzyskiwania dostępu do usługi Resource Manager przy użyciu tokenu tylko do aplikacji.
3. Połączenie hello rekordów w strukturze danych aplikacji "połączonych subskrypcji" - utrwalanie identyfikator hello hello subskrypcji.

Oto bliżej w pierwszym kroku hello. tooassign hello odpowiednie RBAC roli toohello tożsamości aplikacji, należy określić:

* Identyfikator obiektu Hello tożsamości aplikacji w usłudze Active Directory użytkownika hello Azure
* Identyfikator Hello hello RBAC roli, która wymaga aplikacji hello subskrypcji

Podczas uwierzytelniania użytkownika z usługi Azure AD aplikacja tworzy obiekt główną usługi dla aplikacji w tej usłudze Azure AD. Azure umożliwia toobe role RBAC przypisanych podmiotów tooservice toogrant bezpośredni dostęp toocorresponding aplikacji na zasobów platformy Azure. Ta akcja jest dokładnie, co Życzymy toodo. Zapytanie hello Azure AD interfejsu API programu Graph toodetermine hello identyfikator aplikacji w hello zalogowanego użytkownika, nazwę główną usługi hello użytkownika usługi Azure AD.

Masz tylko token dostępu usługi Azure Resource Manager — należy nowe hello toocall tokenu dostępu do interfejsu API usługi Azure AD Graph. Każda aplikacja sieci Web w usłudze Azure AD ma tooquery uprawnienia własną obiekt główny usługi więc token dostępu tylko do aplikacji jest wystarczająca.

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a>Uzyskaj token dostępu tylko do aplikacji interfejsu API Azure AD Graph
tooauthenticate aplikacji i get tokenu tooAzure AD Graph API, wystawiać OAuth2.0 przyznania poświadczeń klienta przepływ żądania tokenu tooAzure AD punktu końcowego tokena (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/Token**).

Witaj [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) metody hello ASP.net MVC przykładowej aplikacji pobiera token dla przy użyciu interfejsu API programu Graph dostępu tylko do aplikacji hello biblioteki uwierzytelniania usługi Active Directory dla środowiska .NET.

Witaj parametrów ciągu zapytania, które są dostępne dla tego żądania są opisane w hello [żądania tokenu dostępu](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) tematu.

Oto przykład żądania tokenu przyznania poświadczeń klienta:

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

Oto przykład odpowiedzi dla poświadczeń klienta umożliwić token:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a>Pobrania ObjectId nazwy głównej usługi aplikacji w użytkownika usługi Azure AD
Teraz Użyj hello tooquery tokenu dostępu tylko do aplikacji hello [podmiotów zabezpieczeń usługi Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) hello toodetermine interfejsu API aplikacji hello nazwy głównej usługi w katalogu hello identyfikator obiektu.

Witaj [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) metody ASP.net MVC Przykładowa aplikacja hello implementuje tego wywołania.

powitania po przykładzie pokazano, jak toorequest nazwy głównej usługi aplikacji. a0448380-c346-4f9f-b897-c18733de9394 jest hello identyfikator klienta aplikacji hello.

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

Witaj poniższy przykład przedstawia żądania toohello odpowiedzi usługi aplikacji głównej

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a>Pobierz identyfikator roli Azure RBAC
tooassign hello odpowiednie RBAC roli tooyour nazwy głównej usługi, należy określić identyfikator hello hello Azure RBAC roli.

Witaj odpowiednią rolę RBAC dla aplikacji:

* Jeśli aplikacja monitoruje tylko subskrypcji hello bez wprowadzania żadnych zmian, wymaga tylko czytnika uprawnienia na powitania subskrypcji. Przypisz hello **czytnika** roli.
* Jeśli aplikacja Azure hello subskrypcji, Tworzenie/modyfikowanie/usuwanie jednostek wymaga jednego uprawnienia współautora hello.
  * toomanage określonego typu zasobu, Przypisz role współautora określonych zasobów hello (Współautor·maszyny·wirtualnej, współautora sieci wirtualnych, współautora konta magazynu itp.)
  * toomanage dowolnego typu zasobu, przypisz hello **współautora** roli.

Hello przypisania roli dla aplikacji jest widoczne toousers, wybierz hello wymagane najmniejszych uprawnień.

Wywołaj hello [definicji roli Menedżera zasobów interfejsu API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist wszystkie role Azure RBAC i wyszukiwania następnie iteracja hello wynik toofind hello potrzeby definicji roli według nazwy.

Witaj [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) metody ASP.net MVC Przykładowa aplikacja hello implementuje tego wywołania.

następujące Hello żądania przykładzie pokazano sposób tooget Azure RBAC roli identyfikatora. 09cbd307-aa71-4aca-b346-5f253e6e3ebb jest identyfikatorem hello hello subskrypcji.

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

odpowiedź Hello jest hello następującego formatu:

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

Nie trzeba toocall tego interfejsu API w sposób ciągły. Po określeniu hello dobrze znany identyfikator GUID hello definicji roli, można utworzyć identyfikator definicji roli hello jako:

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

Poniżej przedstawiono hello dobrze znane identyfikatory GUID często używane wbudowane role:

| Rola | Identyfikator GUID |
| --- | --- |
| Czytelnik |acdd72a7-3385-48ef-bd42-f606fba81ae7 |
| Współautor |b24988ac-6180-42a0-ab88-20f7382dd24c |
| Współautor maszyny wirtualnej |d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| Współautor sieci wirtualnej |b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| Współautor konta magazynu |86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| Współautor witryny sieci Web |de139f84-1756-47ae-9be6-808fbbe84772 |
| Współautor Plan sieci Web |2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| SQL Server współautora |6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |
| Współautor bazy danych SQL |9b7fa17d-e63e-47B0-bb0a-15c516ac86ec |

### <a name="assign-rbac-role-tooapplication"></a>Przypisz tooapplication roli RBAC
Masz wszystko, co potrzebne tooassign hello odpowiednie RBAC roli tooyour nazwy głównej usługi za pomocą hello [Resource Manager utworzyć przypisanie roli](https://docs.microsoft.com/rest/api/authorization/roleassignments) interfejsu API.

Witaj [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) metody ASP.net MVC Przykładowa aplikacja hello implementuje tego wywołania.

Przykładowe żądanie tooassign RBAC roli tooapplication:

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

W żądaniu hello są używane następujące wartości hello:

| Identyfikator GUID | Opis |
| --- | --- |
| 09cbd307-aa71-4aca-b346-5f253e6e3ebb |Identyfikator subskrypcji hello Hello |
| c3097b31-7309-4c59-b4e3-770f8406bad2 |Identyfikator obiektu Hello nazwy głównej usługi hello aplikacji hello |
| acdd72a7-3385-48ef-bd42-f606fba81ae7 |Identyfikator Hello hello rolę czytelnika |
| 4f87261d-2816-465d-8311-70a27558df4c |Nowy identyfikator guid utworzone dla hello nowe przypisanie roli |

odpowiedź Hello jest hello następującego formatu:

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a>Uzyskaj dostęp tylko do aplikacji token dla usługi Azure Resource Manager
toovalidate danej aplikacji ma dostęp hello potrzeby hello subskrypcji, wykonać zadanie testu na powitania subskrypcji przy użyciu tokenu tylko do aplikacji.

tooget tokenu dostępu tylko do aplikacji, wykonaj instrukcje z sekcji [Uzyskaj token dostępu tylko do aplikacji interfejsu API Azure AD Graph](#app-azure-ad-graph), podając inną wartość dla parametru zasobów hello:

    https://management.core.windows.net/

Witaj [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) metody hello ASP.NET MVC przykładowej aplikacji pobiera token dla usługi Azure Resource Manager przy użyciu dostępu tylko do aplikacji hello biblioteki uwierzytelniania usługi Active Directory dla środowiska .net.

#### <a name="get-applications-permissions-on-subscription"></a>Uzyskać uprawnienia aplikacji w subskrypcji
toocheck, która aplikacja ma hello potrzeby dostępu do subskrypcji platformy Azure, może także wywołać hello [uprawnienia menedżera zasobów](https://docs.microsoft.com/rest/api/authorization/permissions) interfejsu API. Ta metoda jest podobne toohow ustalić, czy hello użytkownik ma uprawnienia dostępu do zarządzania dla subskrypcji hello. Jednak ten czas wywołać interfejs API uprawnienia hello z tokenem dostępu tylko do aplikacji hello, odebrany w poprzednim kroku hello.

Witaj [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) metody ASP.NET MVC Przykładowa aplikacja hello implementuje tego wywołania.

## <a name="manage-connected-subscriptions"></a>Zarządzanie subskrypcjami połączonych
Odpowiednie role RBAC hello przypisany aplikacji tooyour nazwy głównej usługi dla subskrypcji hello, aplikację można zachować monitorowania/zarządzanie przy użyciu tokenów dostępu tylko do aplikacji dla usługi Azure Resource Manager.

Jeśli właściciel subskrypcji usuwa przypisanie roli aplikacji przy użyciu klasycznego portalu hello lub narzędzia wiersza polecenia, aplikacja jest tooaccess nie będzie możliwe tej subskrypcji. W takim przypadku należy powiadomić użytkownika hello hello połączenia z subskrypcją hello Przerwano z zewnętrznej aplikacji hello i nadaj im opcję zbyt "naprawa" hello połączenia. "Napraw" po prostu ponownie utworzyć przypisania roli hello, który został usunięty w trybie offline.

Tak samo, jak włączyć hello użytkownika tooconnect subskrypcje tooyour aplikacji, musisz zezwolić na powitania użytkownika toodisconnect subskrypcje zbyt. Z dostępu administracyjnego punktu widzenia Odłącz oznacza usunięcie przypisania roli hello mającego nazwę główną usługi aplikacji hello na powitania subskrypcji. Opcjonalnie każdy stan w aplikacji hello hello subskrypcji mogą zostać usunięte za.
Tylko użytkownicy z uprawnieniem dostępu administracyjnego na powitania subskrypcji są możliwe toodisconnect hello subskrypcji.

Witaj [metody RevokeRoleFromServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) programu ASP.net MVC hello przykładowej aplikacji implementuje tego wywołania.

To wszystko — użytkownicy mogą teraz łatwo połączyć i zarządzać ich subskrypcjami platformy Azure z aplikacją.
