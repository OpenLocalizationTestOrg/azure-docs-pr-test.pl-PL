---
title: "toowork aaaHow z serwera wewnętrznej bazy danych hello .NET SDK for Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak hello toowork z serwera wewnętrznej bazy danych .NET SDK usługi Azure App Service Mobile Apps."
keywords: "usługi aplikacji, usługa aplikacji azure, aplikacji mobilnej, usługi mobilnej, wdrażanie aplikacji wdrożenia usługi azure app skali, skalowalna,"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a>Praca z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

W tym temacie pokazano, jak toouse hello serwera wewnętrznej bazy danych .NET SDK w różnych kluczowych scenariuszy Azure App Service Mobile Apps. zestaw SDK usługi Azure Mobile Apps Hello pomaga w pracy z klientów mobilnych, z poziomu aplikacji ASP.NET.

> [!TIP]
> Witaj [serwer .NET SDK usługi Azure Mobile Apps] [ 2] jest typu open source w witrynie GitHub. Witaj repozytorium zawiera wszystkie kodu źródłowego, w tym zestaw testów jednostkowych hello całego serwera zestawu SDK i kilka przykładowych projektach.
>
>

## <a name="reference-documentation"></a>Dokumentacja referencyjna
Hello dokumentacji powitania serwera zestawu SDK jest zlokalizowana tutaj: [Azure Mobile Apps .NET Reference][1].

## <a name="create-app"></a>Porady: tworzenie zaplecza aplikacji mobilnej platformy .NET
Jeśli uruchamiasz nowego projektu można utworzyć aplikację usługi aplikacji przy użyciu albo hello [portalu Azure] lub Visual Studio. Można uruchomić lokalnie hello aplikacji usługi App Service lub opublikować hello projektu tooyour oparte na chmurze usługi aplikacji — warstwa aplikacji mobilnej.

W przypadku dodawania funkcji mobilnych tooan istniejącego projektu, zobacz hello [pobierania i zainicjuj hello SDK](#install-sdk) sekcji.

### <a name="create-a-net-backend-using-hello-azure-portal"></a>Tworzenie zaplecza .NET przy użyciu hello portalu Azure
toocreate zaplecza aplikacji mobilnych usługi aplikacji, albo wykonaj hello [samouczek Szybki Start] [ 3] lub wykonaj następujące kroki:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

Po powrocie do hello *wprowadzenie* bloku, w obszarze **Utwórz tabelę interfejsu API**, wybierz **C#** jako z **język wewnętrznej bazy danych**. Kliknij przycisk **Pobierz**, Wyodrębnij komputera lokalnego tooyour pliki skompresowane projektu i otwórz rozwiązanie hello w programie Visual Studio.

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a>Tworzenie zaplecza .NET przy użyciu programu Visual Studio 2013 i Visual Studio 2015
Zainstaluj hello [zestawu Azure SDK dla platformy .NET] [ 4] (wersja 2.9.0 lub nowszym) toocreate Azure Mobile Apps projektu programu Visual Studio. Po zainstalowaniu hello zestawu SDK, tworzenie aplikacji ASP.NET przy użyciu hello następujące kroki:

1. Otwórz hello **nowy projekt** okna dialogowego (z *pliku* > **nowy** > **projektu...** ).
2. Rozwiń węzeł **szablony** > **Visual C#**i wybierz **Web**.
3. Wybierz **aplikacji sieci Web ASP.NET**.
4. Wprowadź nazwę projektu hello. Następnie kliknij przycisk **OK**.
5. W obszarze *ASP.NET 4.5.2 szablony*, wybierz pozycję **aplikacji mobilnej Azure**. Sprawdź **Host w chmurze hello** toocreate zaplecza aplikacji mobilnych w hello chmury toowhich można opublikować tego projektu.
6. Kliknij przycisk **OK**.

## <a name="install-sdk"></a>Porady: pobieranie i zainicjuj hello zestawu SDK
Witaj zestaw SDK jest dostępny na [NuGet.org]. Ten pakiet zawiera tooget podstawowe funkcje wymagane hello uruchomiony przy użyciu hello zestawu SDK. tooinitialize hello zestawu SDK, należy tooperform akcje na powitania **HttpConfiguration** obiektu.

### <a name="install-hello-sdk"></a>Zainstaluj hello zestawu SDK
Witaj tooinstall zestawu SDK, kliknij prawym przyciskiem myszy na powitania serwera projektu programu Visual Studio, wybierz **Zarządzaj pakietami NuGet**, wyszukaj hello [Microsoft.Azure.Mobile.Server] pakietu, a następnie kliknij przycisk  **Zainstaluj**.

### <a name="server-project-setup"></a>Inicjowanie hello na serwerze project Server
Projekt serwera zaplecza .NET jest zainicjowane podobne tooother projekty programu ASP.NET, umieszczając w niej klasę początkową OWIN. Upewnij się, że ma odwołanie do pakietu NuGet hello `Microsoft.Owin.Host.SystemWeb`. tooadd tej klasy w Visual Studio, kliknij prawym przyciskiem myszy projekt serwera i wybierz **Dodaj** >
**nowy element**, następnie **Web**  >  ** Ogólne** > **klasy początkowej OWIN**.  Klasa jest generowana za pomocą hello następującego atrybutu:

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

W hello `Configuration()` metoda z klasy początkowej OWIN, użyj **HttpConfiguration** środowisko usługi Azure Mobile Apps hello tooconfigure obiektu.
Poniższy przykład Hello inicjuje Projekt serwera hello z nie dodatkowe funkcje:

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

tooenable poszczególne funkcje, należy wywołać metody rozszerzenia na powitania **MobileAppConfiguration** obiekt przed wywołaniem **metody ApplyTo**. Dodaje na przykład hello następującego kodu domyślnego hello kieruje kontrolerów tooall interfejsu API, które mają atrybut hello `[MobileAppController]` podczas inicjowania:

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

Szybki Start serwera na powitania z hello Azure wywołania portalu **UseDefaultConfiguration()**. To odpowiednik toohello następujące ustawienia:

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

metody rozszerzenia Hello używane są:

* `AddMobileAppHomeController()`udostępnia hello domyślną stronę główną usługi Azure Mobile Apps.
* `MapApiControllers()`udostępnia niestandardowego interfejsu API funkcji WebAPI kontrolerów ozdobione hello `[MobileAppController]` atrybutu.
* `AddTables()`udostępnia mapowanie hello `/tables` kontrolerów tootable punktów końcowych.
* `AddTablesWithEntityFramework()`jest skrótowym dla mapowania hello `/tables` kontrolerów na podstawie punktów końcowych przy użyciu programu Entity Framework.
* `AddPushNotifications()`zapewnia prostą metodę rejestrowania urządzeń do usługi Notification Hubs.
* `MapLegacyCrossDomainController()`zawiera standardowe nagłówki CORS dla rozwoju lokalnych.

### <a name="sdk-extensions"></a>Rozszerzenia zestawu SDK
następujące pakiety NuGet, na podstawie rozszerzenia Hello zapewniają różne funkcje mobilne, które mogą być używane przez aplikację. Włącz rozszerzenia podczas inicjowania przy użyciu hello **MobileAppConfiguration** obiektu.

* [Microsoft.Azure.Mobile.Server.Quickstart] obsługuje hello podstawowa konfiguracja aplikacji mobilnej. Konfiguracja toohello dodanych przez wywołanie hello **UseDefaultConfiguration** — metoda rozszerzenia podczas inicjowania. To rozszerzenie zawiera następujące rozszerzenia: powiadomienia, uwierzytelnianie, jednostki, tabel, między domenami i pakiety głównej. Ten pakiet jest używany przez hello Mobile Apps Szybki Start dostępny na powitania portalu Azure.
* [Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implementuje domyślny hello *tej aplikacji mobilnej jest uruchomiona strona* dla katalogu głównego witryny sieci web hello. Dodaj konfigurację toohello przez wywołanie metody **AddMobileAppHomeController** — metoda rozszerzenia.
* [Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) zawiera klasy do pracy z potoku danych hello danych i ustawia w górę. Dodaj konfigurację toohello przez wywołanie hello **AddTables** — metoda rozszerzenia.
* [Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) umożliwia hello Entity Framework tooaccess danych w hello bazy danych SQL. Dodaj konfigurację toohello przez wywołanie hello **AddTablesWithEntityFramework** — metoda rozszerzenia.
* [Microsoft.Azure.Mobile.Server.Authentication] umożliwia uwierzytelnianie i zestawy w górę hello OWIN oprogramowanie pośredniczące używane toovalidate tokenów. Dodaj konfigurację toohello przez wywołanie hello **AddAppServiceAuthentication** i **IAppBuilder**. **UseAppServiceAuthentication** metody rozszerzenia.
* [Microsoft.Azure.Mobile.Server.Notifications] umożliwia wypychanie powiadomień i definiuje punktu końcowego rejestracji wypychania. Dodaj konfigurację toohello przez wywołanie hello **AddPushNotifications** — metoda rozszerzenia.
* [Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) tworzy kontroler, który służy toolegacy danych przeglądarki sieci web z aplikacji mobilnej. Dodaj konfigurację toohello przez wywołanie metody **MapLegacyCrossDomainController** — metoda rozszerzenia.
* [Microsoft.Azure.Mobile.Server.Login] zapewnia hello AppServiceLoginHandler.CreateToken() metodę, która jest metodą statyczną, używane podczas uwierzytelniania niestandardowego scenariuszy.

## <a name="publish-server-project"></a>Porady: publikowanie projektu serwera hello
W tej sekcji przedstawiono, jak toopublish zaplecza .NET projektu w programie Visual Studio. Można także wdrożyć projektu zaplecza przy użyciu narzędzia Git lub hello żadnego z innych metod opisanych w hello [dokumentacja wdrażania usługi aplikacji Azure](../app-service-web/web-sites-deploy.md).

1. W programie Visual Studio Skompiluj ponownie pakietów NuGet toorestore projektu hello.
2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello projektu, kliknij przycisk **publikowania**. Witaj publikowania, po raz pierwszy należy toodefine profilu publikowania. Jeśli istnieje już profil zdefiniowane, możesz wybrać go i kliknij przycisk **publikowania**.
3. Pytania tooselect, lokalizacja docelowa publikowania, kliknij przycisk **Microsoft Azure App Service** > **dalej**, a następnie (w razie potrzeby) logowania przy użyciu poświadczeń platformy Azure.
   Program Visual Studio pobierze i bezpiecznie przechowywane są Twoje ustawienia publikowania bezpośrednio z platformy Azure.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. Wybierz użytkownika **subskrypcji**, wybierz pozycję **typu zasobu** z **widoku**, rozwiń węzeł **aplikacji mobilnej**i kliknij przycisk zaplecza aplikacji mobilnej, a następnie kliknij przycisk **OK**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. Sprawdź hello publikowania informacji o profilu i kliknij przycisk **publikowania**.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    Po zaplecza aplikacji mobilnej został pomyślnie opublikowany, pojawi się Strona początkowa, informujący o powodzeniu.

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <a name="define-table-controller"></a>Porady: Definiowanie kontrolera tabeli
Zdefiniuj tooexpose kontrolera tabeli klientom toomobile tabeli SQL.  Konfigurowanie kontrolera tabeli wymaga trzy kroki:

1. Utwórz klasę obiektu transferu danych (DTO).
2. Skonfiguruj odwołania do tabeli w hello klasy Mobile DbContext.
3. Tworzenie kontrolera tabeli.

Skanowania danych Transfer obiektu (DTO) jest to zwykły C# obiekt dziedziczący z `EntityData`.  Na przykład:

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

Witaj DTO jest używane toodefine hello tabeli w bazie danych SQL hello.  Witaj toocreate bazy danych wpisu, Dodaj `DbSet<>` właściwości na powitania DbContext używasz.  Witaj domyślny szablon projektu usługi Azure Mobile Apps, hello DbContext nosi nazwę `Models\MobileServiceContext.cs`:

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

Jeśli masz hello zainstalowania zestawu Azure SDK, można teraz utworzyć kontrolera tabeli szablonu w następujący sposób:

1. Kliknij prawym przyciskiem myszy folder kontrolery hello i wybierz **Dodaj** > **kontrolera...** .
2. Wybierz hello **Azure Mobile Apps tabeli kontrolera** opcji, a następnie kliknij przycisk **Dodaj**.
3. W hello **Dodaj kontroler** okna dialogowego:
   * W hello **klasa modelu** listy rozwijanej wybierz Twoje nowe DTO.
   * W hello **DbContext** listy rozwijanej wybierz hello klasy DbContext usługi mobilnej.
   * Nazwa kontrolera Hello jest tworzona.
4. Kliknij pozycję **Dodaj**.

Projekt serwera szybkiego startu Hello zawiera przykład prostą **TodoItemController**.

### <a name="adjust-pagesize"></a>Porady: dopasowywanie hello tabeli stronicowania
Domyślnie program Azure Mobile Apps zwraca 50 rekordów na żądanie.  Stronicowanie gwarantuje, że powitania klienta nie blokuje ich UI wątku ani powitania serwera zbyt długo, zapewniając uzyskać komfortowe środowisko użytkownika. Witaj toochange tabeli stronicowania, po stronie serwera na powitania wzrost "dozwolony rozmiar kwerendy" i hello po stronie klienta rozmiar powitania po stronie serwera "dozwolony rozmiar zapytania" jest dostosowana przy użyciu hello `EnableQuery` atrybutu:

    [EnableQuery(PageSize = 500)]

Upewnij się, że hello PageSize jest hello sam lub większy niż rozmiar hello zażądał powitania klienta.  Zapoznaj się z dokumentacją Porada określonego klienta toohello szczegółowe informacje na temat zmieniania rozmiaru strony powitania klienta.

## <a name="how-to-define-a-custom-api-controller"></a>Porady: Definiowanie niestandardowego kontrolera interfejsu API
kontrolera niestandardowego interfejsu API Hello zapewnia zaplecza aplikacji mobilnej tooyour najbardziej podstawowa funkcjonalność hello przez udostępnianie punktu końcowego. Można zarejestrować kontrolera interfejsu API specyficzne dla mobilnych za pomocą atrybutu hello [MobileAppController]. Witaj `MobileAppController` atrybut rejestruje trasę hello, konfiguruje serializator JSON aplikacji mobilnej hello i włącza [Sprawdzanie wersji klienta](app-service-mobile-client-and-server-versioning.md).

1. W programie Visual Studio, kliknij prawym przyciskiem myszy folder kontrolery hello, następnie kliknij przycisk **Dodaj** > **kontrolera**, wybierz pozycję **kontroler 2 interfejsu API sieci Web&mdash;pusty** i Kliknij przycisk **Dodaj**.
2. Podaj **nazwy kontrolera**, takich jak `CustomController`i kliknij przycisk **Dodaj**.
3. Hello nowy plik klasy kontrolera, Dodaj następujące hello instrukcję using:

        using Microsoft.Azure.Mobile.Server.Config;
4. Zastosuj hello **[MobileAppController]** atrybutu definicji klasy kontrolera toohello interfejsu API, tak jak hello poniższy przykład:

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. W pliku App_Start/Startup.MobileApp.cs Dodaj toohello wywołania **MapApiControllers** — metoda rozszerzenia, tak jak hello poniższy przykład:

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

Można również użyć hello `UseDefaultConfiguration()` — metoda rozszerzenia zamiast `MapApiControllers()`. Każdego kontrolera, który nie ma **MobileAppControllerAttribute** stosowane nadal mogą być używane przez klientów, ale go może nie być poprawnie używane przez klientów przy użyciu dowolnego klienta aplikacji mobilnej zestawu SDK.

## <a name="how-to-work-with-authentication"></a>Porady: Praca z uwierzytelnianiem
Aplikacje mobilne platformy Azure korzysta z aplikacji usługi uwierzytelniania / autoryzacji toosecure z zaplecza aplikacji mobilnych.  W tej sekcji opisano sposób hello tooperform następujące zadania związane z uwierzytelnianiem w projekcie serwera zaplecza .NET:

* [Porady: Dodawanie uwierzytelniania tooa serwera projektu](#add-auth)
* [Porady: użycie uwierzytelniania niestandardowego dla aplikacji](#custom-auth)
* [Porady: pobieranie uwierzytelniony informacje o użytkowniku](#user-info)
* [Porady: ograniczanie autoryzowanym użytkownikom dostęp do danych](#authorize)

### <a name="add-auth"></a>Porady: Dodawanie uwierzytelniania tooa serwera projektu
Można dodać projekt serwera tooyour uwierzytelniania, rozszerzając hello **MobileAppConfiguration** obiektu i konfigurowanie oprogramowania pośredniczącego OWIN. Po zainstalowaniu hello [Microsoft.Azure.Mobile.Server.Quickstart] hello pakietu i wywołanie **UseDefaultConfiguration** — metoda rozszerzenia, możesz pominąć toostep 3.

1. W programie Visual Studio należy zainstalować hello [Microsoft.Azure.Mobile.Server.Authentication] pakietu.
2. W pliku projektu Startup.cs hello, Dodaj następujące wiersz kodu na początku hello hello hello **konfiguracji** metody:

        app.UseAppServiceAuthentication(config);

    Ten składnik oprogramowania pośredniczącego OWIN weryfikuje tokeny wystawione przez bramę usługi aplikacji hello skojarzone.
3. Dodaj hello `[Authorize]` atrybutu tooany kontrolera lub metody, która wymaga uwierzytelnienia.

toolearn temat tooauthenticate klientów tooyour zaplecza Mobile Apps, zobacz [aplikacji tooyour authentication Dodaj](app-service-mobile-ios-get-started-users.md).

### <a name="custom-auth"></a>Porady: użycie uwierzytelniania niestandardowego dla aplikacji
Jeśli nie chcesz, aby toouse jednego z dostawców uwierzytelniania/autoryzacji dla aplikacji usługi hello, można zaimplementować systemu logowania. Zainstaluj hello [Microsoft.Azure.Mobile.Server.Login] pakietu tooassist generacji tokenu uwierzytelniania.  Sprawdzanie poprawności poświadczeń użytkownika Podaj własny kod. Na przykład sprawdzić przed solone i skrótu hasła w bazie danych. W poniższym przykładzie hello, hello `isValidAssertion()` — metoda (zdefiniowany w innym miejscu) jest odpowiedzialny za kontrole.

niestandardowe uwierzytelnianie Hello jest udostępniany przez tworzenie klasy ApiController i udostępnianie `register` i `login` akcje. powitania klienta należy używać niestandardowych informacji hello toocollect interfejsu użytkownika na powitania użytkownika.  informacje Hello są następnie wywołaj przesłanych toohello interfejsu API z standardowe HTTP POST. Gdy serwer hello sprawdza potwierdzenia hello, token jest wystawiane przy użyciu hello `AppServiceLoginHandler.CreateToken()` metody.  Witaj klasy ApiController **nie powinien** Użyj hello `[MobileAppController]` atrybutu.

Przykład `login` akcji:

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

W hello poprzedzających przykładzie LoginResult i LoginResultUser są obiekty możliwe do serializacji udostępnianie wymagane właściwości. powitania klienta oczekuje logowania odpowiedzi toobe zwracane w postaci obiektów JSON hello formularza:

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

Witaj `AppServiceLoginHandler.CreateToken()` metoda zawiera *odbiorców* i *wystawcy* parametru. Oba te parametry są ustawiane toohello adres URL katalogu aplikacji przy użyciu hello schematu HTTPS. Podobnie należy ustawić *secretKey* klucza podpisywania wartość hello toobe aplikacji. Nie rozpowszechniaj hello klucza w kliencie podpisywania, który może być kluczy używanych toomint i personifikować użytkowników. Możesz uzyskać hello klucza podczas hostowanych w usłudze App Service za pomocą odwołań do hello podpisywania *witryny sieci Web\_uwierzytelniania\_podpisywanie\_klucza* zmiennej środowiskowej. W razie potrzeby w kontekście lokalnego debugowania, wykonaj instrukcje hello hello [debugowania lokalnego z uwierzytelnianiem](#local-debug) sekcji tooretrieve hello klucz i zapisz go jako ustawienie aplikacji.

Witaj wystawiony token mogą również obejmować inne oświadczenia oraz datę wygaśnięcia.  Minimalny, hello wystawiony token musi zawierać temat (**sub**) oświadczeń.

Może obsługiwać powitania klienta standardowe `loginAsync()` metoda przeciążenia hello uwierzytelniania trasy.  Jeśli klient hello wywołuje `client.loginAsync('custom');` toolog w, Twoje trasy nie może być `/.auth/login/custom`.  Można ustawić hello trasę dla przy użyciu kontrolera niestandardowego uwierzytelniania hello `MapHttpRoute()`:

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> Przy użyciu hello `loginAsync()` podejście zapewnia token uwierzytelniania hello jest dołączony tooevery kolejne wywołanie toohello usługi.
>
>

### <a name="user-info"></a>Porady: pobieranie uwierzytelniony informacje o użytkowniku
Gdy użytkownik jest uwierzytelniany przez usługę App Service, można uzyskać dostępu do hello przypisany identyfikator użytkownika i inne informacje w kodzie zaplecza .NET. informacje o użytkowniku Hello może służyć do podejmowania decyzji dotyczących autoryzacji w hello wewnętrznej bazy danych. Witaj następujący kod uzyskuje hello identyfikator użytkownika skojarzony z żądaniem:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

Hello identyfikator SID jest określana na podstawie Identyfikatora użytkownika specyficznych dla dostawcy hello i jest statyczny dla danego użytkownika i dostawcy logowania.  Witaj identyfikator SID ma wartość null dla nieprawidłowego uwierzytelniania tokenów.

Usługa App Service umożliwia również żądania określonych oświadczeń od dostawcy logowania. Każdy dostawca tożsamości Aby uzyskać więcej informacji, przy użyciu dostawcy tożsamości zestawu SDK.  Na przykład można użyć hello interfejsu Graph API usługi Facebook informacji znajomych.  W bloku dostawcy hello w hello portalu Azure, można określić oświadczenia, które są wymagane. Niektóre oświadczenia wymagają dodatkowej konfiguracji z hello dostawcy tożsamości.

Witaj poniższy kod hello wywołania **GetAppServiceIdentityAsync** rozszerzenia metody tooget hello poświadczenia logowania, które obejmują żądania tokenu toomake wymagane dostępu hello przed hello interfejsu Graph API usługi Facebook:

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

Dodaj using instrukcji dla `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** — metoda rozszerzenia.

### <a name="authorize"></a>Porady: ograniczanie autoryzowanym użytkownikom dostęp do danych
W poprzedniej sekcji hello możemy pokazano, jak tooretrieve hello identyfikator użytkownika uwierzytelnionego użytkownika. Można ograniczyć toodata dostępu i innych zasobów na podstawie tej wartości. Na przykład dodawanie tootables kolumny userId i filtrowanie wyników zapytania hello przy użyciu Identyfikatora użytkownika hello jest toolimit prosty sposób zwracane tylko użytkownicy tooauthorized danych. Witaj następujący kod zwraca wiersze danych tylko wtedy, gdy hello identyfikator SID jest zgodna z wartością w kolumnie Identyfikator UserId hello w tabeli TodoItem hello:

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

Witaj `Query()` metoda zwraca `IQueryable` który można manipulować filtrowania toohandle LINQ.

## <a name="how-to-add-push-notifications-tooa-server-project"></a>Porady: Dodawanie Projekt serwera tooa powiadomień wypychanych
Dodaj projekt serwera tooyour powiadomienia wypychane przez rozszerzenie hello **MobileAppConfiguration** obiektu i Tworzenie klienta usługi Notification Hubs.

1. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt serwera hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**, wyszukaj `Microsoft.Azure.Mobile.Server.Notifications`, następnie kliknij przycisk **zainstalować**.
2. Powtórz ten krok hello tooinstall `Microsoft.Azure.NotificationHubs` pakiet, który zawiera hello biblioteki klienta usługi Notification Hubs.
3. W App_Start/Startup.MobileApp.cs i Dodaj toohello wywołania **AddPushNotifications()** — metoda rozszerzenia podczas inicjowania:

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. Dodaj następującego kodu tworzącego klienta usługi Notification Hubs hello:

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

Teraz można używać urządzeń tooregistered powiadomień wypychanych toosend hello centra powiadomień klienta. Aby uzyskać więcej informacji, zobacz [aplikacji tooyour powiadomień wypychanych Dodaj](app-service-mobile-ios-get-started-push.md). toolearn więcej informacji na temat usługi Notification Hubs, zobacz [omówienie centra powiadomień](../notification-hubs/notification-hubs-push-notification-overview.md).

## <a name="tags"></a>Porady: Włączanie docelowe wypychanych przy użyciu tagów
Usługi Notification Hubs umożliwia wysyłanie powiadomień docelowe toospecific rejestracji przy użyciu tagów. Kilka tagi są tworzone automatycznie:

* Witaj identyfikator instalacji identyfikuje określonego urządzenia.
* Witaj identyfikator użytkownika na podstawie hello uwierzytelniony identyfikator SID identyfikuje określonego użytkownika.

Witaj instalacji identyfikator jest możliwy z hello **installationId** właściwość hello **MobileServiceClient**.  Hello poniższy przykład przedstawia użycie tooadd identyfikator instalacji instalacji określonych tooa tag w centra powiadomień:

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

Dowolne tagi dostarczonych przez klienta na powitania podczas rejestracji powiadomień wypychanych są ignorowane przez hello wewnętrznej bazy danych, tworząc hello instalacji. tooenable tooadd klienta znaczniki toohello instalacji, należy utworzyć niestandardowego interfejsu API, który dodaje znaczniki przy użyciu hello poprzedzających wzorca.

Zobacz [tagi powiadomień wypychanych dodać klienta] [ 5] w przykładowym ukończone szybkiego startu App Service Mobile Apps hello przykład.

## <a name="push-user"></a>Porady: tooan powiadomień wypychanych wysyłania uwierzytelniony użytkownik
Uwierzytelniony użytkownik rejestruje dla powiadomień wypychanych, tag identyfikator użytkownika jest automatycznie dodawany toohello rejestracji. Za pomocą tego tagu, możesz wysłać powiadomienia tooall urządzeń zarejestrowanych przez tę osobę wypychania. Hello poniższy kod pobiera identyfikator SID użytkownika w żądaniu skierowanym hello i wysyła rejestracji urządzenia tooevery powiadomień wypychanych szablonu dla tej osoby:

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

Podczas rejestrowania dla powiadomień wypychanych z uwierzytelnionego klienta, upewnij się, że przed podjęciem próby wykonania rejestracji zakończeniem uwierzytelniania. Aby uzyskać więcej informacji, zobacz [Push toousers] [ 6] hello App Service Mobile Apps ukończone szybkiego startu próbki dla zaplecza .NET.

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a>Porady: debugowania i rozwiązywania problemów z hello .NET Server SDK
Usługa aplikacji Azure zapewnia kilka debugowania i rozwiązywanie problemów z techniki dla aplikacji ASP.NET:

* [Monitorowanie usługi aplikacji Azure](../app-service-web/web-sites-monitor.md)
* [Włączanie rejestrowania diagnostycznego w usłudze aplikacji Azure](../app-service-web/web-sites-enable-diagnostic-log.md)
* [Rozwiązywanie problemów z usługi aplikacji Azure w programie Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a>Rejestrowanie
Dzienniki diagnostyczne usługi tooApp można pisać przy użyciu hello standardowe zapisu śledzenia ASP.NET. Aby można było tworzyć toohello dzienników, należy włączyć diagnostyki w zaplecza aplikacji mobilnej.

tooenable diagnostyki i zapisu dzienniki toohello:

1. Wykonaj kroki hello w [jak diagnostyki tooenable](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).
2. Dodaj następujące hello przy użyciu instrukcji w pliku kodu:

        using System.Web.Http.Tracing;
3. Utwórz toowrite moduł zapisujący śledzenia z hello .NET backend toohello dzienników diagnostycznych, w następujący sposób:

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. Ponownie opublikować projekt serwera, a hello aplikacji mobilnej zaplecza tooexecute hello kodu ścieżki z rejestrowaniem hello dostępu.
5. Pobierz i ocenić hello dzienniki, zgodnie z opisem w [porady: pobieranie dzienników](../app-service-web/web-sites-enable-diagnostic-log.md#download).

### <a name="local-debug"></a>Debugowanie za pomocą uwierzytelniania lokalnego
Aplikację można uruchomić lokalnie tootest zmiany przed ich opublikowaniem toohello chmury. Dla większości zapleczy Azure Mobile Apps, naciśnij klawisz *F5* while w programie Visual Studio. Istnieją pewne dodatkowe kwestie przy użyciu uwierzytelniania.

Musi być oparta na chmurze aplikacji mobilnej z aplikacji usługi uwierzytelniania/autoryzacji skonfigurowany, a klient musi mieć punktu końcowego w chmurze hello określony jako hello alternatywnego hosta. Zapoznaj się dokumentacją powitania dla danej platformy klienta, aby poznać konkretne kroki hello wymagane.

Upewnij się, że Twoje zaplecze aplikacji mobilnej ma [Microsoft.Azure.Mobile.Server.Authentication] zainstalowane. Następnie, w aplikacji klasy początkowej OWIN, Dodaj następujące hello po `MobileAppConfiguration` został zastosowany tooyour `HttpConfiguration`:

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

W hello poprzedzających przykład, należy skonfigurować hello *authAudience* i *authIssuer* ustawienia aplikacji w pliku Web.config pliku tooeach być adresem URL katalogu aplikacji przy użyciu hello HTTPS schemat. Podobnie należy ustawić *authSigningKey* klucza podpisywania wartość hello toobe aplikacji.
tooobtain hello klucza podpisywania:

1. Przejdź tooyour aplikacji w ramach hello [portalu Azure]
2. Kliknij przycisk **narzędzia**, **Kudu**, **Przejdź**.
3. W witrynie zarządzania Kudu hello, kliknij przycisk **środowiska**.
4. Znajdź wartość hello *witryny sieci Web\_uwierzytelniania\_podpisywanie\_klucza*.

Witaj użycia klucza dla hello podpisywania *authSigningKey* parametru w pliku config aplikacji lokalnej.  Twoje zaplecze aplikacji mobilnej jest teraz tokeny wyposażone toovalidate podczas uruchamiania lokalnego powitania klienta uzyskuje hello tokenu z punktu końcowego hello oparte na chmurze.

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[portalu Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
