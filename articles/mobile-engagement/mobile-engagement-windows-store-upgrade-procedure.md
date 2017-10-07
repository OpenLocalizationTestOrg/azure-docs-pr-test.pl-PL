---
title: aaaWindows uniwersalnych aplikacji zestawu SDK procedur uaktualniania
description: "Procedury uaktualniania systemu Windows Universal SDK aplikacji dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a>Procedury uaktualniania uniwersalnych aplikacji systemu Windows SDK
Jeśli już jest zintegrowany starszą wersję programu zaangażowania do aplikacji, należy hello tooconsider następujące punkty podczas uaktualniania hello zestawu SDK.

Masz toofollow kilka procedur Jeśli pominięte różne wersje hello zestawu SDK. Na przykład w przypadku migracji z 0.10.1 too0.11.0 masz toofirst wykonaj hello "z 0.9.0 too0.10.1" procedury, a następnie hello "z 0.10.1 too0.11.0" procedury.

## <a name="from-330-too340"></a>Z 3.3.0 too3.4.0
### <a name="test-logs"></a>Dzienniki testów
Dzienniki konsoli utworzonego przez zestaw SDK hello można teraz włączone/wyłączone/odfiltrowane. toocustomize ta, właściwość hello aktualizacji `EngagementAgent.Instance.TestLogEnabled` tooone hello wartość dostępna hello `EngagementTestLogLevel` wyliczenia, na przykład:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a>Zasoby
udoskonalono Hello Reach nakładki. Jest ona częścią zasoby pakietu SDK NuGet hello.

Podczas uaktualniania toohello nowej wersji zestawu SDK hello można wybrać, czy ma tookeep istniejących plików z hello nakładki folderu zasobów:

* Jeśli poprzednie nakładki hello jest pracuje lub jest integrowany hello `WebView` elementy ręcznie, a następnie użytkownik może określić tookeep istniejących plików, to nadal będzie działać. 
* Jeśli chcesz, aby tooupdate toohello nowe nakładki, po prostu zastąpić hello całego `overlay` folder z Twoich zasobów z hello nową z pakietu SDK hello (aplikacji platformy uniwersalnej systemu Windows: po uaktualnieniu hello, możesz pobrać ze strony % USERPROFILE % hello nowy folder na nakładce\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Przy użyciu nowego nakładki hello zastąpią wszelkie zmiany wprowadzone na powitania poprzedniej wersji.
> 
> 

## <a name="from-320-too330"></a>Z 3.2.0 too3.3.0
### <a name="resources"></a>Zasoby
Ten krok dotyczy tylko zasobów niestandardowych. Jeśli dostosowano zasobów hello udostępnianych przez hello SDK (html, obrazy, nakładki), następnie toobackup je przed uaktualnieniem, a następnie Zastosuj ponownie dostosowanie na uaktualniony zasobów.

## <a name="from-310-too320"></a>Z 3.1.0 too3.2.0
### <a name="resources"></a>Zasoby
Ten krok dotyczy tylko zasobów niestandardowych. Jeśli dostosowano zasobów hello udostępnianych przez hello SDK (html, obrazy, nakładki), następnie toobackup je przed uaktualnieniem, a następnie Zastosuj ponownie dostosowanie na uaktualniony zasobów.

### <a name="webview-integration"></a>Integracja z widoku sieci Web
Niektóre ulepszenia toomatch innego urządzenia rozmiarach zostały wprowadzone w tej wersji. Upewnij się, że Twoje integracji hello webview zgodne hello następujące:

W Twojej XAML strony ():

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

W pliku skojarzone CS:

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a>Z 2.0.0 too3.0.0
### <a name="resources"></a>Zasoby
Ten krok dotyczy tylko zasobów niestandardowych. Jeśli dostosowano zasobów hello udostępnianych przez hello SDK (html, obrazy, nakładki), następnie toobackup je przed uaktualnieniem, a następnie Zastosuj ponownie dostosowanie na uaktualniony zasobów.

## <a name="from-111-too200"></a>Z 1.1.1 too2.0.0
Witaj poniżej opisano sposób toomigrate integracji zestawu SDK z hello Capptain usługi oferowane przez Capptain SAS w aplikacji obsługiwane przez usługę Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain i usługi Mobile Engagement nie hello tej samej usługi i procedury hello tylko podane poniżej prezentuje sposób toomigrate hello aplikacji klienckiej. Migrowanie hello zestawu SDK w aplikacji hello nie będą migrowane dane z hello Capptain serwerów toohello Mobile Engagement serwerów
> 
> 

W przypadku migracji z wcześniejszej wersji, należy najpierw zapoznaj się hello Capptain witryny sieci web toomigrate too1.1.1, zastosuj hello procedury

### <a name="nuget-package"></a>Pakiet Nuget
Zastąp **Capptain.WindowsPhone** przez **MicrosoftAzure.MobileEngagement** pakietu Nuget.

### <a name="applying-mobile-engagement"></a>Stosowanie usługi Mobile Engagement
Hello SDK używany termin hello `Engagement`. Należy tooupdate toomatch Twojego projektu tej zmiany.

Należy toouninstall bieżącego Capptain pakietu nuget. Należy wziąć pod uwagę, że wszystkie zmiany w folderze Capptain zasoby zostaną usunięte. Jeśli tookeep tych plików, a następnie utworzyć ich kopię.

Po wykonaniu tej instalacji nowego pakietu nuget usługi Microsoft Azure Engagement hello w projekcie. Znajdziesz ją bezpośrednio witrynie sieci Web [nuget]. lub indeks tutaj. Zastępuje tej akcji, wszystkich plików zasobów używanych przez usługi Engagement i dodaje nowe tooyour DLL zaangażowania hello projektu odwołań.

Masz tooclean odwołania projektu o usunięcie odwołania do biblioteki DLL Capptain. Jeśli nie wprowadzisz to, wersja hello Capptain spowoduje konflikt i nastąpi błędy.

Jeśli dostosowano Capptain zasobów, skopiuj stare pliki zawartości i wklej je w nowych plików zaangażowania hello. Należy pamiętać, że pliku xaml, jak i cs toobe aktualizacji.

Po wykonaniu tych kroków wystarczy tooreplace stare odwołania Capptain przez hello nowych zaangażowania odwołań.

1. Wszystkie przestrzenie nazw Capptain ma toobe aktualizacji.
   
    Przed migracją:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Po zakończeniu migracji:
   
        using Microsoft.Azure.Engagement;
2. Wszystkie klasy Capptain, które zawierają "Capptain" powinien zawierać "Zaangażowania".
   
    Przed migracją:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Po zakończeniu migracji:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Pliki xaml Capptain przestrzeni nazw i atrybuty także zmienić.
   
    Przed migracją:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Po zakończeniu migracji:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Nakładki strony zmiany
   
   > [!IMPORTANT]
   > Zmienia także nakładki. Jego nowa przestrzeń nazw to `Microsoft.Azure.Engagement.Overlay`. Ma ona toobe używane w pliku xaml, jak i cs. Ponadto `CapptainGrid` nosi nazwę toobe `EngagementGrid`, `capptain_notification_content` i `capptain_announcement_content` są nazywane `engagement_notification_content` i `engagement_announcement_content`.
   > 
   > 
   
    Do nakładki:
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    Staje się:
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. Dla hello innych zasobów, takich jak obrazy Capptain i pliki HTML, należy pamiętać, że również zostały toouse zmieniono nazwę "Zaangażowania".

### <a name="project-declaration"></a>Deklaracja projektu
Na Package.appxmanifest `File Type Associations` został zaktualizowany od:

* capptain\_osiągnąć\_zawartości tooengagement\_osiągnąć\_zawartości
* capptain\_dziennika\_pliku tooengagement\_dziennika\_pliku

### <a name="application-id--sdk-key"></a>Identyfikator aplikacji / klucz zestawu SDK
Zaangażowania używa parametrów połączenia. Nie masz toospecify identyfikator i klucz zestawu SDK z usługi Mobile Engagement, wystarczy toospecify ciąg połączenia. Możesz można skonfigurować go na plik EngagementConfiguration.

Konfiguracja zaangażowania Hello może zostać ustawiona Twojej `Resources\EngagementConfiguration.xml` pliku projektu.

Edytuj toospecify tego pliku:

* Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.

Jeśli chcesz, aby toospecify go w czasie wykonywania zamiast tego możesz wywołać program hello następujące metody przed zainicjowaniem agenta zaangażowania hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

Parametry połączenia Hello aplikacji jest wyświetlany na powitania klasycznego portalu Azure.

### <a name="items-name-change"></a>Zmiana nazwy elementów
Wszystkie elementy o nazwie *capptain* została nazwana *engagement*. Podobnie dla *Capptain* za*Engagement*.

Przykłady często używanych elementów Capptain:

* CapptainConfiguration teraz nazwę EngagementConfiguration
* Teraz o nazwie EngagementAgent CapptainAgent
* Teraz o nazwie EngagementReach CapptainReach
* Teraz o nazwie EngagementHttpConfig CapptainHttpConfig
* Teraz o nazwie GetEngagementPageName GetCapptainPageName

Należy pamiętać, że zmiany nazwy wpływa na przesłoniętej metody.

