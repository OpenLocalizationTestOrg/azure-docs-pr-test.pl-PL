---
title: "aaaUpgrade z tooAzure usług Mobile Services App Service"
description: "Dowiedz się, jak tooeasily uaktualnienia programu tooan aplikacji usługi Mobile Services aplikację usługi Mobile aplikacji"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a>Uaktualnij istniejący tooApp usługi mobilnej Azure .NET usługi
Mobile App Service jest nowy sposób toobuild aplikacji dla urządzeń przenośnych przy użyciu programu Microsoft Azure. toolearn więcej, zobacz [co to są Mobile Apps?].

W tym temacie opisano sposób tooupgrade istniejącej aplikacji zaplecza .NET z usług Azure Mobile Services tooa nowej aplikacji usługi Mobile Apps. Podczas wykonywania tego uaktualnienia istniejącej aplikacji usługi Mobile Services można nadal toooperate.   Jeśli potrzebujesz tooupgrade aplikacji zaplecza Node.js odwoływać się za[uaktualniania usług Mobile Node.js](app-service-mobile-node-backend-upgrading-from-mobile-services.md).

Zaplecze aplikacji mobilnej jest uaktualniony tooAzure usługi aplikacji, ma tooall dostęp do funkcji usługi aplikacji i są rozliczane według zbyt[cennik usługi aplikacji], nie Mobile Services cennik.

## <a name="migrate-vs-upgrade"></a>Migrowanie i uaktualnianie
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Zaleca się że [przeprowadzenie migracji](app-service-mobile-migrating-from-mobile-services.md) przed rozpoczęciem uaktualnienia. W ten sposób można umieścić obie wersje aplikacji hello tego samego planu usługi App Service i pociągnąć za sobą nie dodatkowych kosztów.
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a>Ulepszenia serwera Mobile Apps .NET SDK
Uaktualnianie toohello nowe [zestaw SDK usługi Mobile Apps](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) zapewnia hello następujące korzyści:

* Większa elastyczność w zależności NuGet. Hello Środowisko hostingu nie jest już zawiera własną wersje pakietów NuGet, dzięki czemu można użyć alternatywnej wersji zgodne. Jednak jeśli istnieją nowe bugfixes krytycznych lub toohello aktualizacje zabezpieczeń zestaw SDK usługi Mobile serwera lub zależności, należy ręcznie zaktualizować usługę.
* Większą elastyczność hello przenośnych zestawu SDK. Jawnie można kontrolować, które funkcje i trasy są skonfigurowane, takich jak uwierzytelnianie, tabeli interfejsów API i hello wypychania punktu końcowego rejestracji. toolearn więcej, zobacz [jak toouse hello serwer .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).
* Obsługa innych typów projektów programu ASP.NET i trasy. Można hostować kontrolerów MVC i interfejsu API sieci Web w hello sam projektu jako projektu zaplecza aplikacji mobilnych.
* Obsługa nowych funkcji uwierzytelniania usługi aplikacji, umożliwiających toouse typowych konfiguracji uwierzytelniania w sieci web i aplikacji mobilnych.

## <a name="overview"></a>Ogólne omówienie uaktualnienia
W wielu przypadkach uaktualniania będzie najprostszą przełączanie toohello nowy serwer Mobile Apps SDK i ponownego publikowania kodu na nowe wystąpienie aplikacji mobilnej. Istnieją, jednak niektóre scenariusze, które będą wymagać dodatkowej konfiguracji, takich jak uwierzytelnianie zaawansowanych scenariuszy i Praca z zaplanowanych zadań. Każdy z tych jest objęte hello później sekcje.

> [!TIP]
> Zaleca się, że należy dokładnie zapoznać się hello pozostałej części tego tematu całkowicie przed rozpoczęciem uaktualniania. Zwróć uwagę na każdej funkcji Użyj wymienione poniżej.
>
>

są zestawy SDK klienta usługi Mobile Services Hello **nie** zgodny z hello nowy serwer Mobile Apps SDK. W kolejności tooprovide ciągłości usługi dla aplikacji nie należy opublikować zmian tooa lokacji aktualnie obsługujący opublikowanych klientów. Zamiast tego należy utworzyć nowej aplikacji mobilnej, która służy jako duplikat. Możesz też zaznaczyć tę aplikację na powitania same usługi aplikacji — planowanie tooavoid ponoszenia dodatkowych kosztów finansowych.

Następnie będzie mieć dwie wersje aplikacji hello: które pozostaje takie same hello i służy opublikowanych aplikacji hello wild i hello innych, które następnie można uaktualnić i obiekt docelowy z nową wersją klienta. Można przenieść i testowanie kodu w tempie użytkownika, ale należy się upewnić, że wszelkie poprawki wprowadzone pobrać tooboth zastosowane. Po uważasz, że odpowiednią liczbę klienta aplikacji w hello wild zaktualizowano toohello najnowszej wersji, można usunąć oryginalny zmigrowana aplikacja hello, jeśli jest to wymagane.

Pełna konspekt procesu uaktualniania hello Hello jest następujący:

1. Tworzenie nowej aplikacji mobilnej
2. Aktualizacja hello projektu toouse hello nowego serwera zestawów SDK.
3. Zwolnij nowej wersji aplikacji klienta
4. (Opcjonalnie) Usuń zmigrowane oryginalnego wystąpienia

## <a name="mobile-app-version"></a>Tworzenie drugiego wystąpienia aplikacji
Witaj pierwszym krokiem podczas uaktualniania jest toocreate hello aplikacji mobilnej zasób, który będzie hostem hello nowej wersji aplikacji. Jeśli już migracji istniejącej usługi mobilnej można toocreate tej wersji na powitania tego samego planu obsługi. Otwórz hello [portalu Azure] i przejdź tooyour migracji aplikacji. Zanotuj hello jest uruchomiona na Plan usługi aplikacji.

Następnie należy utworzyć drugiego wystąpienia aplikacji hello przez następujące hello [instrukcje dotyczące tworzenia zaplecza .NET](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app). Gdy zostanie wyświetlony monit o tooselect, możesz Plan usługi aplikacji lub "plan hostingu" Wybierz hello planu migrowanych aplikacji.

Prawdopodobnie będzie toouse hello tej samej bazy danych i Centrum powiadomień, jak zostało w usłudze Mobile Services. Możesz skopiować te wartości, otwierając [portalu Azure] i nawigacja toohello oryginalnej aplikacji, następnie kliknij przycisk **ustawienia** > **ustawienia aplikacji**. W obszarze **parametry połączenia**, kopiowania `MS_NotificationHubConnectionString` i `MS_TableConnectionString`. Przejdź tooyour nowej lokacji uaktualnienia i wklej je w, zastępując istniejące wartości. Powtórz te kroki dla innych ustawień aplikacji potrzeb aplikacji. Jeśli nie używa zmigrowanej usługi, możesz przeczytać parametry połączenia i ustawień aplikacji z hello **Konfiguruj** kartę hello usług Mobile Services części hello [klasycznego portalu Azure].

Utwórz kopię hello projekt ASP.NET dla aplikacji i opublikować tooyour nowej lokacji. Przy użyciu kopii zaktualizowane hello nowy adres URL aplikacji klienckiej, sprawdź, czy wszystko działa zgodnie z oczekiwaniami.

## <a name="updating-hello-server-project"></a>Aktualizowanie powitania serwera projektu
Mobile Apps udostępnia nową [zestawu SDK serwera aplikacji mobilnych] zapewniające znacznie hello same funkcje co hello usług Mobile Services w czasie wykonywania. Najpierw należy usunąć wszystkie pakiety usługi Mobile Services toohello odwołania. W Menedżerze pakietów NuGet hello, wyszukaj `WindowsAzure.MobileServices.Backend`. Większość aplikacji zostanie wyświetlony kilka pakietów, w tym `WindowsAzure.MobileServices.Backend.Tables` i `WindowsAzure.MobileServices.Backend.Entity`. W takim przypadku Uruchom z pakietem najniższy hello w drzewie zależności hello, takich jak `Entity`i usuń go. Po wyświetleniu monitu, nie należy usuwać wszystkie pakiety zależne. Powtórz ten proces, aż zostaną usunięte `WindowsAzure.MobileServices.Backend` samej siebie.

Na tym etapie należy projektu, który nie odwołuje się do zestawów SDK usługi Mobile.

Następnie dodasz hello odwołania do zestawu SDK aplikacji usługi Mobile. Dla tego uaktualnienia większość deweloperów będzie toodownload i zainstalować hello `Microsoft.Azure.Mobile.Server.Quickstart` pakietów, jak to będzie pobierać hello całego zestawu wymagane.

Będzie kilka błędów wynikających z różnic między hello zestawów SDK, ale są łatwe tooaddress i są objęte hello pozostałej części tej sekcji.

### <a name="base-configuration"></a>Konfiguracja podstawowa
Następnie w WebApiConfig.cs, można zastąpić:

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

Z

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> Jeśli chcesz toolearn, więcej informacji na temat hello nowy serwer .NET SDK i jak tooadd lub usuń funkcji z aplikacji, zobacz hello [jak toouse hello serwer .NET SDK] tematu.
>
>

Jeśli aplikacja sprawia, że korzystanie z funkcji uwierzytelniania hello, musisz także tooregister oprogramowania pośredniczącego OWIN. W takim przypadku należy przenieść hello powyżej kod konfiguracji do nowej klasy uruchamiania OWIN.

1. Dodaj pakiet NuGet hello `Microsoft.Owin.Host.SystemWeb` Jeśli nie jest już zawarty w projekcie.
2. W programie Visual Studio, kliknij prawym przyciskiem myszy projekt i wybierz **Dodaj** -> **nowy element**. Wybierz **Web** -> **ogólne** -> **klasy początkowej OWIN**.
3. Przenieś hello powyżej kodu dla MobileAppConfiguration z `WebApiConfig.Register()` toohello `Configuration()` metody nowej klasy uruchamiania.

Upewnij się, że hello `Configuration()` metoda kończy się na:

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

Brak tooauthentication powiązane dodatkowe zmiany, które zostały opisane w poniższej sekcji hello pełnego uwierzytelniania.

### <a name="working-with-data"></a>Praca z danymi
W usłudze Mobile Services nazwa aplikacji mobilnej hello są obsługiwane jako nazwy schematu domyślnego hello w Instalatorze programu Entity Framework hello.

tooensure, czy masz hello sam schemat odwołuje jak poprzednio, użyj powitania po tooset hello schematu w hello DbContext aplikacji:

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

Upewnij się, że masz MS_MobileServiceName Jeśli hello powyżej. Jeśli aplikacja dostosowany to wcześniej, można też podać inną nazwę schematu.

### <a name="system-properties"></a>Właściwości systemu
#### <a name="naming"></a>Nazewnictwo
Na serwerze usług Azure Mobile Services hello zestawu SDK, właściwości systemu zawsze zawiera podwójne podkreślenia (`__`) prefiks dla właściwości hello:

* __createdAt
* __updatedAt
* __deleted
* __version

Klient usług Mobile Services Hello zestawów SDK ma specjalną logikę do analizowania właściwości systemu w tym formacie.

W usłudze Azure Mobile Apps właściwości systemu nie będzie już specjalne formatowanie i mieć hello następujące nazwy:

* CreatedAt
* updatedAt
* usunięte
* Wersja

Hello Mobile Apps klienta zestawów SDK Użyj hello nowych właściwości nazwami systemowymi, dlatego zmiany nie są wymagane tooclient kodu. Jednak jeśli bezpośredniego wprowadzania REST wywołuje usługę tooyour, należy odpowiednio zmienić zapytań.

#### <a name="local-store"></a>Lokalny magazyn
Hello zmiany toohello nazwy właściwości systemu oznacza dla usług Mobile Services lokalnej bazy danych synchronizacji w trybie offline nie jest zgodny z usługą Mobile Apps. Jeśli to możliwe należy unikać uaktualniania aplikacji klienta z tooMobile usługi mobilne, aplikacje dopiero po oczekujące zmiany zostały wysłane toohello serwera. Następnie uaktualnionego aplikacji hello należy używać nową nazwę pliku bazy danych.

Jeśli aplikacja kliencka jest uaktualnienie z tooMobile usługi Mobile Apps, gdy istnieją oczekujące zmiany w trybie offline w kolejce operacji hello, hello systemowej bazy danych musi być zaktualizowany toouse hello nowych nazw kolumn. W systemach iOS można to osiągnąć przy użyciu nazwy kolumn hello toochange lekkie migracji. Android i hello .NET zarządzanego klienta należy zapisać niestandardowe toorename SQL hello kolumn tabel obiektu danych.

W systemach iOS należy zmienić schemat podstawowych danych z danych jednostek toomatch hello następującego. Należy pamiętać, że hello właściwości `createdAt`, `updatedAt` i `version` nie będzie już `ms_` prefiksu:

| Atrybut | Typ | Uwaga |
| --- | --- | --- |
| id |Ciąg, oznaczona jako wymagana |klucz podstawowy w magazynie zdalnym |
| CreatedAt |Date |Właściwości systemu toocreatedAt map (opcjonalnie) |
| updatedAt |Date |Właściwości systemu tooupdatedAt map (opcjonalnie) |
| Wersja |Ciąg |(opcjonalnie) używane toodetect konflikty, tooversion mapy |

#### <a name="querying-system-properties"></a>Badanie właściwości systemu
W usłudze Azure Mobile Services właściwości systemu nie są wysyłane domyślnie, ale tylko wtedy, gdy żądanie przy użyciu ciągu zapytania hello `__systemProperties`. Z kolei w systemie Azure Mobile Apps właściwości są **zawsze zaznaczone** ponieważ są one częścią powitania serwera SDK obiektu modelu.

Ta zmiana wpływa głównie implementacji niestandardowych menedżerów domeny, takie jak rozszerzenia `MappedEntityDomainManager`. W usłudze Mobile Services, jeśli klient nie zażąda żadnych właściwości systemu jest możliwe toouse `MappedEntityDomainManager` który nie jest rzeczywiście mapowany wszystkich właściwości. Jednak w usłudze Azure Mobile Apps, te właściwości Niemapowane spowoduje błąd w zapytaniach GET.

Najprostszym sposobem tooresolve hello problem Hello jest toomodify Twojego DTOs, dzięki czemu dziedziczą z `ITableData` zamiast `EntityData`. Następnie należy dodać hello `[NotMapped]` atrybutu toohello pola, które powinny być pominięte.

Na przykład definiuje następujące hello `TodoItem` bez właściwości systemu:

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

Uwaga: Jeśli występują błędy `NotMapped`, Dodaj zestaw toohello odwołania `System.ComponentModel.DataAnnotations`.

### <a name="cors"></a>CORS
Mobile Services zawarte niektórych obsługę mechanizmu CORS zawijania hello rozwiązania ASP.NET CORS. Ta warstwa zawijania został usunięty toogive hello developer większą kontrolę, więc można wykorzystać bezpośrednio [obsługi mechanizmu CORS ASP.NET](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

Witaj główne obszary zainteresowania, jeśli przy użyciu mechanizmu CORS są tym hello `eTag` i `Location` nagłówki może aby powitania klienta zestawów SDK toowork poprawnie.

### <a name="push-notifications"></a>Powiadomienia wypychane
W przypadku wypychania hello elementu głównego, który może się okazać brakuje hello Server SDK jest hello PushRegistrationHandler klasy. Nieco inaczej obsługi rejestracji w aplikacji mobilnej, a tagless rejestracji są domyślnie włączone. Zarządzanie tagów można osiągnąć za pomocą niestandardowych interfejsów API. Zobacz hello [rejestrowanie tagów](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) instrukcje, aby uzyskać więcej informacji.

### <a name="scheduled-jobs"></a>Zaplanowane zadania
Zaplanowane zadania nie są wbudowane w Mobile Apps, więc wszystkie istniejące zadania, które ma w zapleczu swojej .NET, należy uaktualnić pojedynczo toobe. Jedną z opcji jest toocreate zaplanowanego [zadanie sieci Web] na powitania aplikacji mobilnej kodu lokacji. Można także skonfigurować kontroler, który zawiera kod zadania i skonfigurować hello [Harmonogram systemu Azure] toohit tego punktu końcowego zgodnie z harmonogramem hello oczekiwano.

### <a name="miscellaneous-changes"></a>Inne zmiany
Wszystkie ApiControllers, które będą używane przez klienta mobilnego teraz musi mieć hello `[MobileAppController]` atrybutu. To nie jest już uwzględniona domyślnie, aby inne toogo ApiControllers dotknięta hello przenośnych elementy formatujące.

Witaj `ApiServices` obiekt nie jest już częścią hello zestawu SDK. tooaccess ustawień aplikacji mobilnej można użyć następujących hello:

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

Podobnie rejestrowanie teraz odbywa się przy użyciu hello standardowe zapisu śledzenia ASP.NET:

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <a name="authentication"></a>Zagadnienia dotyczące uwierzytelniania
Składniki uwierzytelniania Hello usług Mobile teraz zostały przeniesione do hello funkcji uwierzytelniania/autoryzacji dla aplikacji usługi. Informacje na temat włączenie tej witryny odczytywania hello [aplikacji mobilnej Dodaj authentication tooyour](app-service-mobile-ios-get-started-users.md) tematu.

Dla niektórych dostawców, takich jak usługi AAD i Facebook, Google powinno być możliwe tooleverage hello istniejącej rejestracji z poziomu aplikacji kopii. Po prostu muszą portalu dostawcy toonavigate toohello tożsamości i dodawanie nowej rejestracji toohello adres URL przekierowania. Następnie można skonfigurować uwierzytelniania/autoryzacji dla aplikacji usługi z powitania klienta identyfikator i klucz tajny.

### <a name="controller-action-authorization"></a>Autoryzacji akcji kontrolera
Wszystkie wystąpienia hello `[AuthorizeLevel(AuthorizationLevel.User)]` atrybutu musi być teraz zmienione toouse hello standardowe ASP.NET `[Authorize]` atrybutu. Ponadto kontrolery są teraz anonimowe domyślnie, tak jak inne aplikacje ASP.NET.
Jeśli zostały przy użyciu jednej z hello inne opcje AuthorizeLevel, np. Admin lub aplikacji, należy pamiętać, że są one usunięte. Można zamiast tego ustawienia AuthorizationFilters dla wspólne klucze tajne lub bezpiecznie skonfigurować wywołań do usługi tooenable nazwy głównej usługi AAD.

### <a name="getting-additional-user-information"></a>Otrzymanie informacji dodatkowych użytkowników
Możesz uzyskać dodatkowe informacje dotyczące użytkownika, łącznie z tokenów dostępu za pośrednictwem hello `GetAppServiceIdentityAsync()` metody:

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

Ponadto jeśli aplikacja przejmuje zależności identyfikatory, takie jak przechowywania ich w bazie danych, ważne jest toonote, który hello identyfikatorów użytkownika usługi Mobile Services i aplikacji usługi Mobile Apps są różne. Może nadal otrzymywać hello identyfikator użytkownika usługi mobilnej, mimo że. Wszystkie podklasy ProviderCredentials hello mają właściwości identyfikatora użytkownika. Dlatego kontynuowanie z przykład Witaj przed:

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

Jeśli aplikacja podejmij wszelkie zależności nazwy użytkownika, jest ważne, aby wykorzystać hello samą rejestrację przy użyciu dostawcy tożsamości, jeśli to możliwe. Nazwy użytkowników są Rejestracja aplikacji zwykle zakresie toohello, który był używany, wprowadzenie nowej rejestracji można utworzyć problemy z pasującymi danych tootheir użytkowników.

### <a name="custom-authentication"></a>Niestandardowe uwierzytelnianie
Jeśli aplikacja używa uwierzytelniania niestandardowego rozwiązania, można toomake się tej lokacji uaktualnionego hello ma dostęp toohello systemu. Postępuj zgodnie z nowego dotyczącymi uwierzytelniania niestandardowego w hello hello [Omówienie zestawu SDK .NET server] toointegrate rozwiązania. Należy pamiętać, że składniki uwierzytelniania niestandardowego hello są nadal w wersji zapoznawczej.

## <a name="updating-clients"></a>Aktualizowanie klientów
Po utworzeniu operacyjną zaplecza aplikacji mobilnej, można pracować na nowej wersji aplikacji klienta, która go wykorzystuje. Aplikacje mobilne zawiera również nową wersję klienta hello zestawy SDK i podobne uaktualnienie serwera toohello powyżej, należy tooremove wszystkie odwołania zestawów SDK usługi Mobile toohello przed instalowania hello Mobile Apps wersji.

Jedną z głównych zmian hello między wersjami hello jest czy konstruktorów hello nie wymagają już klucz aplikacji. Możesz teraz po prostu Przekaż hello adres URL aplikacji mobilnej. Na przykład na powitania klientów platformy .NET, hello `MobileServiceClient` Konstruktor jest teraz:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

Informacje o instalacji hello nowe zestawy SDK i przy użyciu nowej struktury hello za pośrednictwem łącza hello poniżej:

* [System iOS w wersji 3.0.0 lub nowszej](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (system Windows/Xamarin) w wersji 2.0.0 lub nowszej](app-service-mobile-dotnet-how-to-use-client-library.md)

Czy aplikacja sprawia, że użycie powiadomień wypychanych, zwróć uwagę na powitania określonej rejestracji instrukcje dotyczące każdej platformy, jak nie zostały niektóre zmiany również.

Jeśli masz hello nową wersję klienta gotowa wypróbuj go na uaktualnionym serwerze projektu. Po weryfikacji, czy działa, można zwolnić nowej wersji toocustomers Twojej aplikacji. Po pewnym czasie po klientów miało tooreceive szansy te aktualizacje, można usunąć usługi Mobile Services hello wersji aplikacji. W tym momencie uaktualnieniu tooan aplikację usługi Mobile aplikacji przy użyciu najnowszych hello serwera Mobile Apps SDK.

<!-- URLs. -->

[portalu Azure]: https://portal.azure.com/
[klasycznego portalu Azure]: https://manage.windowsazure.com/
[co to są Mobile Apps?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[zestawu SDK serwera aplikacji mobilnych]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[Harmonogram systemu Azure]: /en-us/documentation/services/scheduler/
[zadanie sieci Web]: ../app-service-web/websites-webjobs-resources.md
[jak toouse hello serwer .NET SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[cennik usługi aplikacji]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Omówienie zestawu SDK .NET server]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
