---
title: aaaWindows Phone Silverlight Engagement SDK integracji
description: "Jak tooIntegrate Azure Mobile Engagement przy użyciu systemu Windows Phone Silverlight aplikacji"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a>Windows Phone Silverlight Engagement SDK Integration
> [!div class="op_single_selector"]
> * [Aplikacje uniwersalne systemu Windows](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

W tej procedurze opisano analizy hello najprostszy sposób tooactivate Azure Mobile Engagement i funkcji w aplikacji Windows Phone Silverlight monitorowania.

wymaga wystarczającej ilości raportu hello tooactivate dzienników toocompute wszystkie statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals to Hello następujące kroki. Raport Hello dzienników potrzebne toocompute innych danych statystycznych jak zadań, błędy i zdarzenia musi zostać wykonane ręcznie przy użyciu hello zaangażowania interfejsu API (zobacz [jak toouse hello zaawansowane usługi Mobile Engagement znakowanie interfejsu API w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) poniżej), ponieważ te statystyki są zależne od aplikacji.

## <a name="supported-versions"></a>Obsługiwane wersje
aplikacji mogą być tylko zintegrowane Hello Mobile Engagement SDK dla platformy Silverlight systemu Windows:

* Windows Phone 8.0
* Windows Phone 8.1 Silverlight

> [!NOTE]
> Jeśli przeznaczona dla Windows Phone 8.1 (z systemem innym niż platformy Silverlight), można znaleźć toohello [uniwersalnych systemu Windows procedura integracji](mobile-engagement-windows-store-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a>Zainstaluj zestaw SDK usługi Mobile Engagement Silverlight hello
Witaj Mobile Engagement SDK dla platformy Silverlight systemu Windows jest dostępna jako pakietu Nuget, nazywany *MicrosoftAzure.MobileEngagement*. Można go zainstalować z hello Menedżera pakietów Nuget programu Visual Studio. 

## <a name="add-hello-capabilities"></a>Dodawanie funkcji hello
Witaj Engagement SDK musi niektóre możliwości hello Windows Phone Silverlight SDK w kolejności toowork poprawnie.

Otwórz z `WMAppManifest.xml` plików i pamiętaj, że hello następujące funkcje są zadeklarowane w hello `Capabilities` panelu:

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a>Inicjowanie hello Engagement SDK
### <a name="engagement-configuration"></a>Konfiguracja usługi Engagement
konfiguracji usługi Engagement Hello jest scentralizowana w hello `Resources\EngagementConfiguration.xml` pliku projektu.

Edytuj toospecify tego pliku:

* Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.

Jeśli chcesz, aby toospecify go w czasie wykonywania zamiast tego możesz wywołać program hello następujące metody przed zainicjowaniem agenta zaangażowania hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

Parametry połączenia Hello aplikacji jest wyświetlany na powitania klasycznego portalu Azure.

### <a name="engagement-initialization"></a>Inicjowania usługi Engagement
Podczas tworzenia nowego projektu `App.xaml.cs` plik został wygenerowany. Ta klasa dziedziczy `Application` i zawiera wiele metod ważne. Konieczne będzie również używany tooinitialize hello Engagement SDK.

Modyfikowanie hello `App.xaml.cs`:

* Dodaj tooyour `using` instrukcji:
  
      using Microsoft.Azure.Engagement;
* Wstaw `EngagementAgent.Instance.Init` w hello `Application_Launching` metody:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* Wstaw `EngagementAgent.Instance.OnActivated` w hello `Application_Activated` metody:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> Firma Microsoft zdecydowanie zniechęcić możesz tooadd hello zaangażowania inicjowania w innym miejscu aplikacji. Jednak należy pamiętać, że hello `EngagementAgent.Instance.Init` metoda jest uruchamiana na dedykowanym wątku, a nie na powitania wątku interfejsu użytkownika.
> 
> 

## <a name="basic-reporting"></a>Podstawowym raportowaniem
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a>Zalecana metoda: przeciążenia sieci `PhoneApplicationPage` klas
W raporcie hello tooactivate kolejności wszystkich dzienników hello wymagane przez zaangażowania toocompute użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, możesz po prostu wprowadzić wszystkie Twoje `PhoneApplicationPage` klasy podrzędne dziedziczą hello `EngagementPage` klasy.

Oto przykład tego, jak toodo to strony aplikacji. Możesz zrobić hello samo dla wszystkich stron w aplikacji.

#### <a name="c-source-file"></a>Plik źródłowy języka C#
Zmodyfikuj stronę `.xaml.cs` pliku:

* Dodaj tooyour `using` instrukcji:
  
      using Microsoft.Azure.Engagement;
* Zastąp `PhoneApplicationPage` z `EngagementPage` :

**Bez usługi Engagement:**

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

**Z usługi Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> Jeśli strony dziedziczy hello `OnNavigatedTo` metody, należy zachować ostrożność toolet hello `base.OnNavigatedTo(e)` wywołania. W przeciwnym razie nie będą raportowane działania hello. W rzeczywistości hello `EngagementPage` wywołuje `StartActivity` wewnątrz hello `OnNavigatedTo` metody.
> 
> 

#### <a name="xaml-file"></a>Plik XAML
Zmodyfikuj stronę `.xaml` pliku:

* Dodaj deklaracje przestrzeni nazw tooyour:
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* Zastąp `phone:PhoneApplicationPage` z `engagement:EngagementPage` :

**Bez usługi Engagement:**

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

**Z usługi Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a>Zastąpienie zachowania domyślnego hello
Domyślnie nazwa klasy hello strony hello został zgłoszony jako nazwę działania hello, bez dodatkowych. Jeśli klasa hello korzysta z sufiksem "Page" hello, Engagement spowoduje również usunięcie.

Jeśli chcesz toooverride hello domyślne zachowanie dla nazwy hello, po prostu dodaj ten kod tooyour:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

Jeśli chcesz tooreport pewne dodatkowe informacje o Twoich działaniach, można dodać ten kod tooyour:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

Te metody są wywoływane z wewnątrz hello `OnNavigatedTo` metody na stronie.

### <a name="alternate-method-call-startactivity-manually"></a>Alternatywna metoda: wywołanie `StartActivity()` ręcznie
Jeśli nie możesz lub nie ma toooverload Twojego `PhoneApplicationPage` klas, zamiast tego można uruchomić działań przez wywołanie metody `EngagementAgent` metody bezpośrednio.

Firma Microsoft zaleca wywołania `StartActivity` wewnątrz sieci `OnNavigatedTo` metody z PhoneApplicationPage.

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> Upewnij się, że prawidłowo zakończyć sesję.
> 
> Witaj SDK automatycznie wywołuje hello `EndActivity` metody, gdy aplikacja hello jest zamknięty. W związku z tym jest **wysokiej** zalecane toocall hello `StartActivity` metody zmianie działania hello hello użytkownika i zbyt**nigdy** hello wywołania `EndActivity` — metoda. Ta metoda wysyła komunikat toohello zaangażowania czy bieżący użytkownik hello opuścił aplikacji hello i serwer ma wpływ na wszystkie dzienniki aplikacji.
> 
> 

## <a name="advanced-reporting"></a>Zaawansowane raportowanie
Opcjonalnie możesz tooreport aplikacji określonych zdarzeń, błędów i zadań, toodo tak, użyj hello innych metod znalezione w hello `EngagementAgent` klasy. Witaj interfejsu API usługi Engagement umożliwia toouse wszystkie funkcje zaawansowane usługi Engagement.

Aby uzyskać więcej informacji, zobacz [jak toouse hello zaawansowane usługi Mobile Engagement znakowanie interfejsu API w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).

## <a name="advanced-configuration"></a>Konfiguracja zaawansowana
### <a name="disable-automatic-crash-reporting"></a>Wyłącz automatyczne zgłaszanie awarii
Możesz wyłączyć hello awarii automatyczne funkcję zaangażowania raportowania. Następnie, gdy wystąpi nieobsługiwany wyjątek, Engagement nie będzie wykonywać żadnych czynności.

> [!WARNING]
> Jeśli planujesz toodisable tej funkcji, należy pamiętać, że po awarii nieobsługiwany nastąpi w aplikacji, Engagement nie będą wysyłały awarii hello **i** nie spowoduje zamknięcia sesji hello i zadania.
> 
> 

toodisable awarii automatycznego raportowania, po prostu Dostosuj konfigurację w zależności od sposób hello należy zadeklarować jako:

#### <a name="from-engagementconfigurationxml-file"></a>Z `EngagementConfiguration.xml` pliku
Raport z ustawiania awaria zbyt`false` między `<reportCrash>` i `</reportCrash>` tagów.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Z `EngagementConfiguration` obiektu w czasie wykonywania
Ustaw przy użyciu obiektu EngagementConfiguration toofalse awarii raportu.

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Tryb serii
Domyślnie raporty usługi Engagement hello rejestruje się w czasie rzeczywistym. Jeśli aplikacja zgłasza dzienniki bardzo często, jest lepsze toobuffer hello dzienniki i tooreport ich jednocześnie na regularne podstawy czasu (jest to nazywane hello "tryb serii").

toodo należy wywołać metodę hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hello argument jest wartością w **milisekund**. W dowolnym momencie rejestrowania w czasie rzeczywistym hello tooreactivate należy po prostu Wywołaj metodę hello bez parametrów lub z wartością hello 0.

Witaj tryb serii wydłużyć baterii hello życia ale ma wpływ na powitania Monitor zaangażowania: wszystkie czas trwania zadania i sesje będą zaokrąglone toohello serii próg (w związku z tym sesji i zadania krótsze niż próg serii hello może nie być widoczna). Jest zalecana toouse próg w serii się niż 30000 (30s). Masz toobe wiedzieć, które zapisane dzienniki są ograniczone too300 elementów. W przypadku wysyłania jest zbyt długa może spowodować utratę niektórych dzienników.

> [!WARNING]
> Witaj próg serii nie można skonfigurować okres tooa mniejszym niż 1 sekunda. Jeśli spróbujesz toodo tak, hello zestawu SDK będą Pokaż śledzenia z powodu błędu hello i automatycznie zresetować toohello wartość domyślna, czyli zero sekund. To spowoduje wyzwolenie hello SDK tooreport hello dzienniki w czasie rzeczywistym.
> 
> 

