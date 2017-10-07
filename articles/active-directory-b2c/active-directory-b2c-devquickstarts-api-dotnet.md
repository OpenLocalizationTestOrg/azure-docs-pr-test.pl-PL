---
title: aaaAzure AD B2C | Dokumentacja firmy Microsoft
description: "Jak toobuild interfejsu API sieci Web platformy .NET przy użyciu usługi Azure Active Directory B2C zabezpieczonej przy użyciu tokenów dostępu protokołu OAuth 2.0 do uwierzytelniania."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: 
ms.assetid: 7146ed7f-2eb5-49e9-8d8b-ea1a895e1966
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: d45364216deda38ef44b60dd11e86d9a089ad509
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-build-a-net-web-api"></a>Azure Active Directory B2C: tworzenie interfejsu API sieci Web platformy .NET

Usługa Azure Active Directory (Azure AD) B2C umożliwia zabezpieczanie interfejsu API sieci Web za pomocą tokenów dostępu protokołu OAuth 2.0. Tokeny te Zezwalaj klienta toohello tooauthenticate aplikacji interfejsu API. W tym artykule opisano, jak toocreate interfejs API programu .NET MVC "Lista zadań do wykonania" umożliwiająca użytkownikom klienta zadań tooCRUD aplikacji. Interfejs API sieci web Hello jest zabezpieczone przy użyciu usługi Azure AD B2C i tylko umożliwia toomanage uwierzytelnionym użytkownikom ich listy zadań do wykonania.

## <a name="create-an-azure-ad-b2c-directory"></a>Tworzenie katalogu usługi Azure AD B2C

Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę. Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów. Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.

> [!NOTE]
> Aplikacja kliencka Hello i interfejs API sieci web muszą używać katalogu B2C hello tej samej usługi Azure AD.
>

## <a name="create-a-web-api"></a>Tworzenie interfejsu API sieci Web

Następnie należy toocreate aplikacji interfejsu API sieci web w katalogu usługi B2C. Dzięki temu informacje usługi Azure AD, czy go wymaga toosecurely komunikować się z aplikacją. toocreate usługi aplikacji, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md). Należy pamiętać o wykonaniu następujących czynności:

* Obejmują **aplikacji sieci web** lub **interfejs API sieci web** w aplikacji hello.
* Użyj hello **identyfikator URI przekierowania** `https://localhost:44332/` hello aplikacji sieci web. To jest domyślna lokalizacja hello powitania klienta aplikacji sieci web dla tego przykładu kodu.
* Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji. Będzie on potrzebny później.
* Wprowadź identyfikator aplikacji do **identyfikatora URI aplikacji**.
* Należy dodać uprawnienia za pomocą hello **opublikowane zakresy** menu.

  [!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Tworzenie zasad

W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md). Konieczne będzie toocreate toocommunicate zasad w usłudze Azure AD B2C. Zaleca się przy użyciu hello połączone konta-konta/zasad logowania, zgodnie z opisem w hello [artykule o zasadach](active-directory-b2c-reference-policies.md). Podczas tworzenia zasad należy pamiętać, aby:

* Wybrać wartość **Nazwa wyświetlana** i inne atrybuty tworzenia konta w zasadach.
* Wybrać oświadczenia **Nazwa wyświetlana** i **Identyfikator obiektu** jako oświadczenia aplikacji dla wszystkich zasad. Można również wybrać inne oświadczenia.
* Kopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu. Nazwa zasad hello będą potrzebne później.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Po pomyślnym utworzeniu zasad hello wszystko jest gotowe toobuild aplikacji.

## <a name="download-hello-code"></a>Pobierz kod hello

Witaj kod dla tego samouczka jest przechowywany w [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi). Przykład Witaj można sklonować, uruchamiając:

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

Po pobraniu hello przykładowy kod tooget plik SLN programu Visual Studio Otwórz hello jest uruchomiona. Witaj plik rozwiązania zawiera dwa projekty: `TaskWebApp` i `TaskService`. `TaskWebApp`to aplikacja sieci web MVC, która hello użytkownika współdziała z. `TaskService`to interfejs API sieci web zaplecza aplikacji hello, który przechowuje listy zadań do wykonania poszczególnych użytkowników. W tym artykule przedstawimy tylko hello `TaskService` aplikacji. toolearn jak toobuild `TaskWebApp` za pomocą usługi Azure AD B2C, zobacz [naszym samouczku aplikacji sieci web .NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md).

### <a name="update-hello-azure-ad-b2c-configuration"></a>Zaktualizuj konfigurację hello Azure AD B2C

Naszej próbki jest skonfigurowany toouse hello zasady i klienta identyfikator dzierżawy naszych pokaz. Jeśli chcesz toouse własną dzierżawę, konieczne będzie hello toodo następujące:

1. Otwórz `web.config` w hello `TaskService` projektu i Zastąp wartości hello
    * `ida:Tenant` nazwą dzierżawy
    * `ida:ClientId` identyfikatorem aplikacji interfejsu API sieci Web
    * `ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania

2. Otwórz `web.config` w hello `TaskWebApp` projektu i Zastąp wartości hello
    * `ida:Tenant` nazwą dzierżawy
    * `ida:ClientId` identyfikatorem aplikacji sieci Web
    * `ida:ClientSecret` kluczem tajnym aplikacji sieci Web
    * `ida:SignUpSignInPolicyId` nazwą zasady tworzenia konta/logowania
    * `ida:EditProfilePolicyId` nazwą zasady edycji profilu
    * `ida:ResetPasswordPolicyId` nazwą zasady resetowania hasła


## <a name="secure-hello-api"></a>Zabezpiecz interfejs API hello

Jeśli klient wywołuje interfejs API, należy zabezpieczyć interfejs API (np. `TaskService`) za pomocą tokenów elementu nośnego OAuth 2.0. Dzięki temu API tooyour każdego żądania będą tylko ważne, jeśli Żądanie hello ma token elementu nośnego. Interfejs API może akceptować i weryfikować tokeny elementu nośnego przy użyciu biblioteki interfejsu OWIN (Open Web Interface for .NET) firmy Microsoft.

### <a name="install-owin"></a>Instalowanie interfejsu OWIN

Rozpocznij od zainstalowania potoku uwierzytelniania OAuth interfejsu OWIN hello przy użyciu hello Konsola Menedżera pakietów programu Visual Studio.

```Console
PM> Install-Package Microsoft.Owin.Security.OAuth -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Security.Jwt -ProjectName TaskService
PM> Install-Package Microsoft.Owin.Host.SystemWeb -ProjectName TaskService
```

Spowoduje to zainstalowanie oprogramowania pośredniczącego OWIN hello, który będzie akceptować i sprawdzania poprawności tokenów elementu nośnego.

### <a name="add-an-owin-startup-class"></a>Dodawanie klasy początkowej OWIN

Dodaj toohello klasy interfejsu API OWIN uruchamiania o nazwie `Startup.cs`.  Kliknij prawym przyciskiem myszy na powitania projektu, zaznacz **Dodaj** i **nowy element**, a następnie wyszukaj interfejs OWIN. oprogramowanie pośredniczące OWIN Hello wywoła hello `Configuration(…)` metody podczas uruchamiania aplikacji.

W naszym przykładzie możemy zmienić deklaracji klasy hello zbyt`public partial class Startup` i implementowane hello drugiej klasy hello w `App_Start\Startup.Auth.cs`. Witaj wewnątrz `Configuration` metody dodaliśmy wywołanie za`ConfigureAuth`, który jest zdefiniowany w `Startup.Auth.cs`. Po modyfikacji hello `Startup.cs` wygląda jak poniżej hello:

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

### <a name="configure-oauth-20-authentication"></a>Konfigurowanie uwierzytelniania OAuth 2.0

Witaj Otwórz plik `App_Start\Startup.Auth.cs`i wdrożenie hello `ConfigureAuth(...)` metody. Na przykład może wyglądać podobnie jak poniżej hello:

```CSharp
// App_Start\Startup.Auth.cs

 public partial class Startup
    {
        // These values are pulled from web.config
        public static string AadInstance = ConfigurationManager.AppSettings["ida:AadInstance"];
        public static string Tenant = ConfigurationManager.AppSettings["ida:Tenant"];
        public static string ClientId = ConfigurationManager.AppSettings["ida:ClientId"];
        public static string SignUpSignInPolicy = ConfigurationManager.AppSettings["ida:SignUpSignInPolicyId"];
        public static string DefaultPolicy = SignUpSignInPolicy;

        /*
         * Configure hello authorization OWIN middleware.
         */
        public void ConfigureAuth(IAppBuilder app)
        {
            TokenValidationParameters tvps = new TokenValidationParameters
            {
                // Accept only those tokens where hello audience of hello token is equal toohello client ID of this app
                ValidAudience = ClientId,
                AuthenticationType = Startup.DefaultPolicy
            };

            app.UseOAuthBearerAuthentication(new OAuthBearerAuthenticationOptions
            {
                // This SecurityTokenProvider fetches hello Azure AD B2C metadata & signing keys from hello OpenIDConnect metadata endpoint
                AccessTokenFormat = new JwtFormat(tvps, new OpenIdConnectCachingSecurityTokenProvider(String.Format(AadInstance, Tenant, DefaultPolicy)))
            });
        }
    }
```

### <a name="secure-hello-task-controller"></a>Zabezpieczanie kontrolera zadań hello

Po aplikacji hello jest uwierzytelnianie skonfigurowanego toouse OAuth 2.0, można zabezpieczyć interfejs API sieci web, dodając `[Authorize]` kontrolera zadań toohello tagu. Jest to kontroler hello, jeśli wszystkie operacje edytowania listy zadań do wykonania ma miejsce, dlatego należy zabezpieczyć cały kontroler hello na poziomie klasy hello. Możesz także dodać hello `[Authorize]` tagu tooindividual akcji dla bardziej szczegółową kontrolę.

```CSharp
// Controllers\TasksController.cs

[Authorize]
public class TasksController : ApiController
{
    ...
}
```

### <a name="get-user-information-from-hello-token"></a>Uzyskiwanie informacji o użytkowniku z hello tokenu

`TasksController`przechowuje zadania w bazie danych, gdzie każde zadanie ma skojarzony użytkownik będący jego "właścicielem" hello zadań. Witaj właściciel jest identyfikowany przez użytkownika hello **obiekt o identyfikatorze**. (Dlatego potrzebne identyfikator obiektu hello tooadd jako aplikacji we wszystkich zasadach.)

```CSharp
// Controllers\TasksController.cs

public IEnumerable<Models.Task> Get()
{
    string owner = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
    IEnumerable<Models.Task> userTasks = db.Tasks.Where(t => t.owner == owner);
    return userTasks;
}
```

### <a name="validate-hello-permissions-in-hello-token"></a>Sprawdź poprawność uprawnień hello w tokenie hello

Typowe wymagania dotyczące interfejsów API sieci web jest hello toovalidate "zakresy" występuje w tokenie hello. Dzięki temu użytkownik hello zgodził usługi listy zadań do wykonania hello toohello uprawnienia wymagane tooaccess.

```CSharp
public IEnumerable<Models.Task> Get()
{
    if (ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/scope").Value != "read")
    {
        throw new HttpResponseException(new HttpResponseMessage {
            StatusCode = HttpStatusCode.Unauthorized,
            ReasonPhrase = "hello Scope claim does not contain 'read' or scope claim not found"
        });
    }
    ...
}
```

## <a name="run-hello-sample-app"></a>Uruchom hello przykładowej aplikacji

Na koniec skompiluj i uruchom oba projekty: `TaskWebApp` i `TaskService`. Utwórz kilka zadań na liście zadań do wykonania hello użytkownika i zwróć uwagę, jak są zachowywane w hello interfejsu API nawet po Zatrzymaj i uruchom ponownie powitania klienta.

## <a name="edit-your-policies"></a>Edytowanie zasad

Po zabezpieczeniu interfejsu API za pomocą usługi Azure AD B2C możesz eksperymentować z zasad logowania — w/tworzenia konta i widoku hello skutki (lub ich brak) na powitania interfejsu API. Można manipulować oświadczeniami aplikacji hello w hello zasad i zmienić informacje o użytkowniku hello dostępnym w hello interfejsu API sieci web. Wszelkie oświadczenia, które można dodać będą dostępne tooyour interfejsu API sieci web .NET MVC w hello `ClaimsPrincipal` obiektu, zgodnie z opisem we wcześniejszej części tego artykułu.
