---
title: "aaaWindows uniwersalnych integracji zestawu SDK usługi Engagement aplikacji"
description: "Jak tooIntegrate usługi Azure Mobile Engagement z uniwersalnych aplikacji systemu Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a>Integracja zestawu SDK zaangażowania uniwersalnych aplikacji systemu Windows
> [!div class="op_single_selector"]
> * [Platforma uniwersalna systemu Windows](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

W tej procedurze opisano analizy i monitorowania aplikacji uniwersalnych systemu Windows hello najprostszy sposób tooactivate usługi Engagement.

wymaga wystarczającej ilości raportu hello tooactivate dzienników toocompute wszystkie statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals to Hello następujące kroki. Raport Hello dzienników potrzebne toocompute innych danych statystycznych jak zadań, błędy i zdarzenia musi zostać wykonane ręcznie przy użyciu hello zaangażowania interfejsu API (zobacz [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji uniwersalnych systemu Windows usługi Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md) od te statystyki są aplikacji zależnej.

## <a name="supported-versions"></a>Obsługiwane wersje
tylko Hello Mobile Engagement SDK dla uniwersalnych aplikacji systemu Windows mogą być zintegrowane środowisko wykonawcze systemu Windows i aplikacji platformy uniwersalnej systemu Windows:

* Windows 8
* Windows 8.1
* Windows Phone 8.1
* Windows 10 (wersje desktop i mobile rodzin)

> [!NOTE]
> Jeśli przeznaczona dla systemu Windows Phone Silverlight można znaleźć toohello [procedura integracji systemu Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a>Zainstaluj hello Mobile Engagement uniwersalny zestaw SDK aplikacji
### <a name="all-platforms"></a>Wszystkie platformy
Witaj Mobile Engagement SDK dla aplikacji uniwersalnej systemu Windows jest dostępna jako pakietu Nuget, nazywany *MicrosoftAzure.MobileEngagement*. Można go zainstalować z hello Menedżera pakietów Nuget programu Visual Studio.

### <a name="windows-8x-and-windows-phone-81"></a>Windows 8.x i Windows Phone 8.1
NuGet automatycznie wdraża hello zasobów zestawu SDK w hello `Resources` folder w katalogu głównym projektu aplikacji hello.

### <a name="windows-10-universal-windows-platform-applications"></a>Aplikacji platformy uniwersalnej systemu Windows 10 systemu Windows
NuGet nie automatycznie wdrażać hello zasobów zestawu SDK w jeszcze aplikacji platformy uniwersalnej systemu Windows. Masz toodo powraca go ręcznie do wdrażania zasobów w NuGet:

1. Otwieranie Eksploratora plików w sieci.
2. Przejdź toohello następującej lokalizacji (**x.x.x** jest wersja hello w przypadku instalowania usługi Engagement): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*
3. Przeciąganie i upuszczanie hello **zasobów** folderu z katalogu głównego toohello Eksploratora plików hello projektu w programie Visual Studio.
4. W programie Visual Studio wybierz projektu i Aktywuj hello **Pokaż wszystkie pliki** ikony na powitania **Eksploratora rozwiązań**.
5. Niektóre pliki nie znajdują się w projekcie hello. tooimport je jednocześnie kliknij prawym przyciskiem myszy hello **zasobów** folderu, **wykluczyć z projektu** , a następnie innego kliknij prawym przyciskiem myszy hello **zasobów** folderu, **dołączania w projekcie** toore-zawierają hello cały folder. Wszystkie pliki z hello **zasobów** folderze znajdują się teraz w projekcie.

## <a name="add-hello-capabilities"></a>Dodawanie funkcji hello
Witaj Engagement SDK musi niektóre możliwości hello zestaw Windows SDK w kolejności toowork poprawnie.

Otwórz z `Package.appxmanifest` plików i pamiętaj, że hello następujące funkcje są deklarowane jako:

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a>Inicjowanie hello Engagement SDK
### <a name="engagement-configuration"></a>Konfiguracja usługi Engagement
konfiguracji usługi Engagement Hello jest scentralizowana w hello `Resources\EngagementConfiguration.xml` pliku projektu.

Edytuj toospecify tego pliku:

* Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.

Jeśli chcesz, aby toospecify go w czasie wykonywania zamiast tego możesz wywołać program hello następujące metody przed zainicjowaniem agenta zaangażowania hello:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

Parametry połączenia Hello aplikacji jest wyświetlany na powitania klasycznego portalu Azure.

### <a name="engagement-initialization"></a>Inicjowania usługi Engagement
Podczas tworzenia nowego projektu `App.xaml.cs` plik został wygenerowany. Ta klasa dziedziczy `Application` i zawiera wiele metod ważne. Konieczne będzie również używany tooinitialize hello Engagement SDK.

Modyfikowanie hello `App.xaml.cs`:

* Dodaj tooyour `using` instrukcji:
  
      using Microsoft.Azure.Engagement;
* Zdefiniuj inicjowania usługi Engagement — metoda tooshare hello raz dla wszystkich wywołań:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* Wywołanie `InitEngagement` w hello `OnLaunched` metody:
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* Gdy aplikacja jest uruchamiana za pomocą schematu niestandardowego, innego wiersza polecenia aplikacji lub hello następnie hello `OnActivated` metoda jest wywoływana. Należy również hello tooinitiate Engagement SDK po aktywowaniu aplikacji. tak, Zastąp toodo `OnActivated` metody:
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> Firma Microsoft zdecydowanie zniechęcić możesz tooadd hello zaangażowania inicjowania w innym miejscu aplikacji.
> 
> 

## <a name="basic-reporting"></a>Podstawowym raportowaniem
### <a name="recommended-method-overload-your-page-classes"></a>Zalecana metoda: przeciążenia sieci `Page` klas
W raporcie hello tooactivate kolejności wszystkich dzienników hello wymagane przez zaangażowania toocompute użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, możesz po prostu wprowadzić wszystkie Twoje `Page` klasy podrzędne dziedziczą hello `EngagementPage` klasy.

Oto przykład tego, jak toodo to strony aplikacji. Możesz zrobić hello samo dla wszystkich stron w aplikacji.

#### <a name="c-source-file"></a>Plik źródłowy języka C#
Zmodyfikuj stronę `.xaml.cs` pliku:

* Dodaj tooyour `using` instrukcji:
  
      using Microsoft.Azure.Engagement;
* Zastąp `Page` z `EngagementPage`:

**Bez usługi Engagement:**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**Z usługi Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> Jeśli strona zastępuje hello `OnNavigatedTo` metody, należy się toocall `base.OnNavigatedTo(e)`. W przeciwnym razie działanie hello nie będą raportowane (hello `EngagementPage` wywołania `StartActivity` wewnątrz jego `OnNavigatedTo` metody).
> 
> 

#### <a name="xaml-file"></a>Plik XAML
Zmodyfikuj stronę `.xaml` pliku:

* Dodaj deklaracje przestrzeni nazw tooyour:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* Zastąp `Page` z `engagement:EngagementPage`:

**Bez usługi Engagement:**

        <Page>
            <!-- layout -->
            ...
        </Page>

**Z usługi Engagement:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a>Zastąpienie zachowania domyślnego hello
Domyślnie nazwa klasy hello strony hello został zgłoszony jako nazwę działania hello, bez dodatkowych. Jeśli klasa hello korzysta z sufiksem "Page" hello, Engagement spowoduje również usunięcie.

Jeśli chcesz toooverride hello domyślne zachowanie dla nazwy hello, po prostu dodaj ten kod tooyour:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

Jeśli chcesz tooreport niektóre dodatkowe informacje o Twoich działaniach, można dodać ten kod tooyour:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Te metody są wywoływane z wewnątrz hello `OnNavigatedTo` metody na stronie.

### <a name="alternate-method-call-startactivity-manually"></a>Alternatywna metoda: wywołanie `StartActivity()` ręcznie
Jeśli nie możesz lub nie ma toooverload Twojego `Page` klas, zamiast tego można uruchomić działań przez wywołanie metody `EngagementAgent` metody bezpośrednio.

Firma Microsoft zaleca toocall `StartActivity` wewnątrz sieci `OnNavigatedTo` metody na stronie.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Upewnij się, że prawidłowo zakończyć sesję.
> 
> Witaj uniwersalnego zestawu SDK automatycznie wywołuje hello `EndActivity` metody, gdy aplikacja hello jest zamknięty. W związku z tym jest **wysokiej** zalecane toocall hello `StartActivity` metody zmianie działania hello hello użytkownika i zbyt**nigdy** hello wywołania `EndActivity` metoda, ta metoda wysyła tooEngagement serwer, że bieżący użytkownik aplikacji hello pozostaw, spowoduje to ma wpływ na wszystkie dzienniki aplikacji.
> 
> 

## <a name="advanced-reporting"></a>Zaawansowane raportowanie
Opcjonalnie możesz tooreport aplikacji określonych zdarzeń, błędów i zadań, toodo tak, użyj hello innych metod znalezione w hello `EngagementAgent` klasy. Witaj interfejsu API usługi Engagement umożliwia toouse wszystkie funkcje zaawansowane usługi Engagement.

Aby uzyskać więcej informacji, zobacz [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji uniwersalnych systemu Windows usługi Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).

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
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Tryb serii
Domyślnie raporty usługi Engagement hello rejestruje się w czasie rzeczywistym. Jeśli aplikacja zgłasza dzienniki bardzo często, jest lepsze toobuffer hello dzienniki i tooreport ich jednocześnie na regularne podstawy czasu (jest to nazywane hello "tryb serii").

toodo należy wywołać metodę hello:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Hello argument jest wartością w **milisekund**. W dowolnym momencie rejestrowania w czasie rzeczywistym hello tooreactivate należy po prostu Wywołaj metodę hello bez parametrów lub z wartością hello 0.

Witaj tryb serii wydłużyć baterii hello życia ale ma wpływ na powitania Monitor zaangażowania: wszystkie czas trwania zadania i sesje będą zaokrąglone toohello serii próg (w związku z tym sesji i zadania krótsze niż próg serii hello może nie być widoczna). Jest zalecana toouse próg w serii się niż 30000 (30s). Masz toobe wiedzieć, które zapisane dzienniki są ograniczone too300 elementów. W przypadku wysyłania jest zbyt długa może spowodować utratę niektórych dzienników.

> [!WARNING]
> Próg serii Hello nie można skonfigurować okres tooa mniejsza od wartości 1. Jeśli spróbujesz toodo tak, hello zestawu SDK będą Pokaż śledzenia z powodu błędu hello i automatycznie resetować toohello wartość domyślna, czyli 0s. To spowoduje wyzwolenie hello SDK tooreport hello dzienniki w czasie rzeczywistym.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

