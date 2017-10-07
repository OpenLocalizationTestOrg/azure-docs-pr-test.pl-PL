---
title: "Usługa Azure Active Directory B2C: Hello Użyj interfejsu API programu Graph | Dokumentacja firmy Microsoft"
description: "Jak toocall hello interfejsu API programu Graph dla dzierżawy B2C przy użyciu procesu hello tooautomate tożsamości aplikacji."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a>Usługa Azure AD B2C: Użyj hello interfejsu API programu Graph
Dzierżaw usługi Azure Active Directory (Azure AD) B2C zwykle toobe bardzo duże. Oznacza to, że wiele typowych zadań zarządzania dzierżawy musi wykonać programowo toobe. Podstawowy przykład to zarządzanie użytkownikami. Może być konieczne toomigrate istniejącej dzierżawy B2C tooa magazynu użytkownika. Może mają toohost rejestracja użytkownika na stronie i tworzenia kont użytkowników w katalogu usługi Azure AD B2C w tle hello. Tego rodzaju zadania wymagają toocreate możliwości hello, odczytu, aktualizacji i usuwać konta użytkowników. Można wykonywać te zadania przy użyciu interfejsu API Azure AD Graph hello.

Dla dzierżawcy usługi B2C istnieją dwa tryby głównej komunikowania się z hello interfejsu API programu Graph.

* Interaktywny, jednokrotnego uruchamiania zadań powinny działać jako konto administratora w dzierżawy B2C hello zadań hello. Ten tryb wymaga toosign administratora przy użyciu poświadczeń tego administratora mogą wykonywać wszystkie toohello wywołania interfejsu API programu Graph.
* Zautomatyzowane, ciągłe zadania należy używać pewien typ konta usługi, który podasz z zadaniami zarządzania tooperform niezbędne uprawnienia hello. W usłudze Azure AD możesz to zrobić, rejestrowanie aplikacji i uwierzytelnianie tooAzure AD. Jest to zrobić za pomocą **identyfikator aplikacji** używającą hello [przyznania poświadczeń klienta OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api). W takim przypadku aplikacji hello działa jako sam nie jako użytkownik, hello toocall interfejsu API programu Graph.

W tym artykule omówiono sposób tooperform hello przypadku użycia automatycznego. toodemonstrate, firma Microsoft będzie kompilacji platformy .NET 4.5 `B2CGraphClient` wykonująca użytkownika tworzenia, odczytu, aktualizacji i usuwania (CRUD) operacji. powitania klienta będzie mieć interfejsu wiersza polecenia systemu Windows (CLI), która pozwala tooinvoke różnych metod. Jednak kod hello są zapisywane toobehave w sposób nieinteraktywne, automatycznej.

## <a name="get-an-azure-ad-b2c-tenant"></a>Uzyskiwanie dzierżawy usługi Azure AD B2C
Przed tworzenia aplikacji lub użytkowników lub w ogóle interakcję z usługą Azure AD, konieczne będzie dzierżawy usługi Azure AD B2C i konto administratora globalnego w dzierżawie powitalnych. Jeśli nie masz już, dzierżawcy [wprowadzenie do usługi Azure AD B2C](active-directory-b2c-get-started.md).

## <a name="register-your-application-in-your-tenant"></a>Zarejestrować aplikację w dzierżawie
Po utworzeniu dzierżawy B2C należy tooregister aplikację za pośrednictwem hello [Azure Portal](https://portal.azure.com).

> [!IMPORTANT]
> toouse hello interfejsu API programu Graph z dzierżawy usługi B2C, trzeba będzie tooregister dedykowanej aplikacji przy użyciu zwykłego hello *rejestracji aplikacji* bloku w hello portalu Azure, **nie** usługi Azure AD B2C  *Aplikacje* bloku. Nie można użyć ponownie hello już istniejących B2C aplikacji, które zarejestrowano w hello Azure AD B2C *aplikacji* bloku.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Wybierz dzierżawy usługi Azure AD B2C, wybierając konto w hello prawym górnym rogu strony hello.
3. W okienku nawigacji po lewej stronie powitania, wybierz **więcej usług**, kliknij przycisk **rejestracji aplikacji**i kliknij przycisk **Dodaj**.
4. Postępuj zgodnie z monitami hello i utworzyć nową aplikację. 
    1. Wybierz **aplikacji sieci Web / interfejs API** jako hello typu aplikacji.    
    2. Podaj **żadnego identyfikator URI przekierowania** (np. https://B2CGraphAPI), ponieważ nie jest to potrzebne w tym przykładzie.  
5. Witaj aplikacji będą teraz wyświetlane w hello listę aplikacji, kliknij go tooobtain hello **identyfikator aplikacji** (znanej także jako identyfikator klienta). Skopiuj go, ponieważ będzie on potrzebny w dalszej części artykułu.
6. W bloku ustawień powitania kliknij **klucze** i Dodaj nowy klucz (znanej także jako klucz tajny klienta). Jest on również kopiowany do użycia w dalszej części artykułu.

## <a name="configure-create-read-and-update-permissions-for-your-application"></a>Skonfiguruj tworzenie, odczytywanie i aktualizowanie uprawnień dla aplikacji
Teraz należy tooconfigure tooget Twojej aplikacji, które hello wszystkie wymagane uprawnienia toocreate, odczytu, aktualizacji i usuwania użytkowników.

1. Kontynuowanie w hello bloku rejestracji aplikacji w portalu Azure, wybierz aplikację.
2. W bloku ustawień powitania kliknij **wymagane uprawnienia**.
3. W bloku wymaganych uprawnień powitania kliknij **Windows Azure Active Directory**.
4. W bloku Włącz dostęp hello, wybierz hello **Odczyt i zapis danych katalogu** zgody **uprawnienia aplikacji** i kliknij przycisk **zapisać**.
5. Ponadto w hello bloku wymaganych uprawnień, kliknij na powitania **udzielanie uprawnień** przycisku.

Masz teraz aplikacja, która ma uprawnienia toocreate, Odczyt i aktualizacja użytkowników z dzierżawy usługi B2C.

## <a name="configure-delete-permissions-for-your-application"></a>Skonfiguruj uprawnienia do usuwania aplikacji
Obecnie hello *Odczyt i zapis danych katalogu* uprawnienie jest **nie** obejmują toodo możliwości hello żadnych usunięć, takich jak usuwanie użytkowników. Jeśli chcesz toogive aplikacji hello możliwości toodelete użytkowników, będziesz potrzebować toodo te dodatkowe kroki, które wymagają programu PowerShell, w przeciwnym razie można pominąć toohello następnej sekcji.

Najpierw należy pobrać i zainstalować hello [Microsoft Online Services Asystenta logowania](http://go.microsoft.com/fwlink/?LinkID=286152). Następnie Pobierz i zainstaluj hello [64-bitowy moduł usługi Azure Active Directory dla środowiska Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).

Po zainstalowaniu modułu PowerShell hello, Otwórz program PowerShell i połączyć tooyour dzierżawy B2C. Po uruchomieniu `Get-Credential`, zostanie wyświetlony monit dla nazwy użytkownika i hasła, wprowadź nazwę użytkownika hello i hasło konta administratora dzierżawy B2C.

> [!IMPORTANT]
> Należy toouse B2C konta administratora dzierżawy, który jest **lokalnego** toohello B2C dzierżawy. Te konta wyglądać następująco: myusername@myb2ctenant.onmicrosoft.com.

```powershell
Connect-MsolService
```

Teraz użyjemy hello **identyfikator aplikacji** w skrypcie hello poniżej tooassign hello aplikacji hello konta administrator roli użytkownika, który umożliwi użytkownikom toodelete. Te role mają dobrze znane identyfikatory, więc wszystko, czego potrzebujesz toodo danych wejściowych użytkownika **identyfikator aplikacji** w poniższym skrypcie hello.

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

Teraz aplikacja ma również uprawnienia toodelete użytkowników z dzierżawy usługi B2C.

## <a name="download-configure-and-build-hello-sample-code"></a>Pobierz, konfigurowanie i tworzenie hello przykładowy kod
Najpierw należy pobrać hello przykładowy kod i będzie działać. Następnie firma Microsoft podejmie bliższe spojrzenie na go.  Możesz [Pobierz hello przykładowy kod w pliku .zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip). Można również sklonować go w wybranym katalogu:

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

Otwórz hello `B2CGraphClient\B2CGraphClient.sln` rozwiązania Visual Studio w programie Visual Studio. W hello `B2CGraphClient` projektu, hello Otwórz plik `App.config`. Zastąp trzy ustawienia aplikacji hello własne wartości:

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Następnie kliknij prawym przyciskiem myszy hello `B2CGraphClient` próbki hello rozwiązania i skompiluj ponownie. W przypadku pomyślnego, po wykonaniu `B2C.exe` plik wykonywalny znajduje się w `B2CGraphClient\bin\Debug`.

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a>Tworzenie operacji CRUD użytkownika przy użyciu interfejsu API programu Graph hello
Otwórz hello toouse B2CGraphClient, `cmd` poleceń systemu Windows, w wierszu polecenia i zmień toohello Twojego katalogu `Debug` katalogu. Następnie uruchom hello `B2C Help` polecenia.

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

Spowoduje to wyświetlenie krótki opis każdego polecenia. Zawsze jednego z tych poleceń, wywołaj `B2CGraphClient` sprawia, że toohello żądania interfejsu API usługi Azure AD Graph.

### <a name="get-an-access-token"></a>Pobranie tokenu dostępu
Wszelkie toohello żądania interfejsu API programu Graph wymaga tokenu dostępu do uwierzytelniania. `B2CGraphClient`używa hello open source Active Directory Authentication Library (ADAL) toohelp uzyskać tokeny dostępu. Biblioteka ADAL ułatwia tokenu nabycia, zapewniając prostych interfejsu API i Dbamy o pewne ważne informacje, takie jak buforowanie tokenów dostępu. Nie masz toouse ADAL tooget tokenów, jednak. Można również uzyskać tokeny przez obsługuje tworzenie żądań HTTP.

> [!NOTE]
> Ten przykładowy kod używa biblioteki ADAL v2 w kolejności toocommunicate z hello interfejsu API programu Graph.  Należy użyć ADAL w wersji 2 lub 3 w kolejności tokenów dostępu tooget, które mogą być używane z hello interfejsu API usługi Azure AD Graph.
> 
> 

Gdy `B2CGraphClient` uruchomieniu tworzy wystąpienie hello `B2CGraphClient` klasy. Witaj konstruktorze tej klasy konfiguruje szkieletów uwierzytelniania ADAL:

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

Użyjemy hello `B2C Get-User` polecenie jako przykład. Gdy `B2C Get-User` jest wywoływana bez żadnych dodatkowych danych wejściowych hello hello wywołania interfejsu wiersza polecenia `B2CGraphClient.GetAllUsers(...)` metody. Ta metoda wywołuje `B2CGraphClient.SendGraphGetRequest(...)`, który przesyła toohello żądania HTTP GET interfejsu API programu Graph. Przed `B2CGraphClient.SendGraphGetRequest(...)` wysyła hello żądania GET, należy go najpierw pobiera token dostępu za pomocą biblioteki ADAL:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

Możesz też uzyskać dostęp do tokenu hello interfejsu API programu Graph przez wywołanie hello ADAL `AuthenticationContext.AcquireToken(...)` metody. Zwraca ADAL `access_token` reprezentujący tożsamość aplikacji hello.

### <a name="read-users"></a>Przeczytaj użytkowników
Gdy ma tooget listę użytkowników lub uzyskać danego użytkownika z interfejsu API programu Graph hello, możesz wysłać HTTP `GET` żądania toohello `/users` punktu końcowego. Żądanie dla wszystkich użytkowników hello w dzierżawie wygląda następująco:

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee to żądanie, uruchom:

 ```
 > B2C Get-User
 ```

Istnieją dwa toonote ważnych rzeczy:

* Witaj tokenu dostępu nabyte za pomocą biblioteki ADAL zostanie dodany toohello `Authorization` nagłówka przy użyciu hello `Bearer` schematu.
* Dla dzierżawcy usługi B2C, należy użyć parametru zapytania hello `api-version=1.6`.

Oba te informacje są obsługiwane w hello `B2CGraphClient.SendGraphGetRequest(...)` metody:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a>Tworzenie konta użytkownika
Podczas tworzenia kont użytkowników w dzierżawie usługi B2C, możesz wysłać HTTP `POST` żądania toohello `/users` punktu końcowego:

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

Większość tych właściwości w tym żądaniu są wymagane toocreate konsumentów. więcej, kliknij przycisk toolearn [tutaj](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser). Należy pamiętać, że hello `//` komentarze zostały włączone na ilustracji. Nie należy wprowadzać ich w rzeczywistego żądania.

Żądanie hello toosee, uruchom następujące polecenia hello:

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

Witaj `Create-User` polecenie przyjmuje jako parametr wejściowy plik JSON. Zawiera reprezentacja JSON obiektu user. Istnieją dwa przykładowe pliki JSON w hello przykładowy kod: `usertemplate-email.json` i `usertemplate-username.json`. Można zmodyfikować te pliki toosuit potrzeb. Ponadto toohello wymagane pola powyżej, kilka opcjonalne pola, które można użyć znajdują się w tych plikach. Szczegółowe informacje o hello opcjonalne pola znajdują się w hello [odwołania do jednostki interfejsu API usługi Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).

Widać, jak żądania POST hello jest tworzony w `B2CGraphClient.SendGraphPostRequest(...)`.

* Dołącza toohello tokenu dostępu `Authorization` nagłówka żądania hello.
* Ustawia `api-version=1.6`.
* Zawiera obiekt użytkownika JSON hello hello treści żądania hello.

> [!NOTE]
> Jeśli hello kont, które mają toomigrate z istniejącym magazynem użytkownika ma niższe siły hasła niż hello [siły silne hasło, wymuszane przez usługę Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), można wyłączyć przy użyciu hello Wymaganiesilnehasłohello`DisableStrongPassword`wartość hello `passwordPolicies` właściwości. Na przykład można zmodyfikować hello Utwórz żądanie użytkownika podanego powyżej w następujący sposób: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.
> 
> 

### <a name="update-consumer-user-accounts"></a>Aktualizowanie kont użytkownika klienta
Podczas aktualizowania obiektów użytkowników procesu hello jest podobne toohello, jednej z nich toocreate obiekty użytkownika. Ten proces wykorzystuje hello HTTP, ale `PATCH` metody:

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

Spróbuj tooupdate użytkownika, aktualizując nowych danych plików JSON. Następnie można użyć `B2CGraphClient` toorun jednego z tych poleceń:

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

Sprawdź hello `B2CGraphClient.SendGraphPatchRequest(...)` metody, aby uzyskać więcej informacji na temat toosend tego żądania.

### <a name="search-users"></a>Wyszukiwania użytkowników
Możesz wyszukać użytkowników w dzierżawie usługi B2C na kilka sposobów. Jeden, za pomocą obiektu o identyfikatorze lub dwóch przy użyciu identyfikatora logowania użytkownika hello hello użytkownika (tj. hello `signInNames` właściwości).

Uruchom jedno z powitania po toosearch poleceń dla określonego użytkownika:

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

Oto kilka przykładów:

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a>Usuwanie użytkowników
proces Hello związanych z usuwaniem użytkowników jest prosta. Użyj hello HTTP `DELETE` metody konstrukcji hello adresu URL i z hello Popraw identyfikator obiektu:

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee przykład, wprowadź tego polecenia i widoku hello delete żądania wydruku toohello konsoli:

```
> B2C Delete-User <object-id-of-user>
```

Sprawdź hello `B2CGraphClient.SendGraphDeleteRequest(...)` metody, aby uzyskać więcej informacji na temat toosend tego żądania.

W przystawce Zarządzanie toouser dodanie można wykonywać wiele innych działania hello Azure AD Graph API. [Dokumentacja interfejsu API Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) podano szczegółowe informacje dotyczące każdej akcji, wraz z próbki żądań.

## <a name="use-custom-attributes"></a>Używanie atrybutów niestandardowych
Większość aplikacji klienta należy toostore pewien typ informacji o profilu użytkownika niestandardowego. Można to zrobić jednym ze sposobów jest toodefine atrybutu niestandardowego w dzierżawie usługi B2C. Następnie można traktować tego atrybutu hello samo Traktuj innych właściwości dla obiektu user. Można zaktualizować atrybutu hello, usuń atrybut hello, zapytania przy użyciu atrybutu hello, wysyłanie atrybutu hello jako oświadczenia w tokeny logowania i inne.

toodefine atrybutu niestandardowego w dzierżawie usługi B2C, zobacz hello [odwołanie do atrybutu niestandardowego B2C](active-directory-b2c-reference-custom-attr.md).

Możesz wyświetlić hello atrybuty niestandardowe zdefiniowane w dzierżawie usługi B2C przy użyciu `B2CGraphClient`:

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

dane wyjściowe Hello tych funkcji ujawnia hello szczegóły każdego z atrybutów niestandardowych, takich jak:

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

Można użyć hello Pełna nazwa, takich jak `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, jako właściwość obiektów użytkownika.  Zaktualizuj plik JSON o hello nowej właściwości i wartości dla właściwości hello, a następnie uruchom:

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

Za pomocą `B2CGraphClient`, masz aplikacji usługi, który można programowo zarządzać użytkownicy dzierżawy B2C. `B2CGraphClient`używa własnego toohello tooauthenticate tożsamości aplikacji interfejsu API usługi Azure AD Graph. Uzyskuje on również tokenów przy użyciu klucza tajnego klienta. Ponieważ ta funkcja jest dołączyć do aplikacji, należy pamiętać o kilka najważniejszych dla aplikacji B2C:

* Należy toogrant hello aplikacji hello odpowiednie uprawnienia w dzierżawie powitalnych.
* Teraz należy tokenów dostępu tooget ADAL (nie MSAL) toouse. (Możesz również wysłać wiadomości protokołu bezpośrednio, bez korzystania z biblioteki.)
* Po wywołaniu interfejsu API programu Graph hello użyj `api-version=1.6`.
* Podczas tworzenia i aktualizowania użytkowników konsumenta, kilka właściwości są wymagane, zgodnie z powyższym opisem.

Jeśli masz pytania lub żądań dla akcji, którą chcesz tooperform przy użyciu interfejsu API programu Graph hello na dzierżawę B2C, zostaw komentarz w tym artykule lub plików problemu w repozytorium przykładowy kod GitHub hello.

