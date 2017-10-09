---
title: "aaaWindows uniwersalnych aplikacji osiągnąć integracji zestawu SDK"
description: "Jak tooIntegrate usługi Azure Mobile Engagement nawiązać połączenia z uniwersalnych aplikacji systemu Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a>Integracja zestawu SDK osiągnąć uniwersalnych aplikacji systemu Windows
Musisz wykonać procedurę integracji hello opisanego w hello [Windows Universal integracji zestawu SDK usługi Engagement](mobile-engagement-windows-store-integrate-engagement.md) przed wykonaniem tego przewodnika.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a>Osadź hello Engagement Reach SDK do projektu uniwersalnych systemu Windows
Nie masz żadnych tooadd. `EngagementReach`referencje i zasoby są już w projekcie.

> [!TIP]
> Można dostosować obrazy znajdujące się w hello `Resources` folderu projektu, szczególnie hello brand ikona (tej domyślnej toohello Engagement). W aplikacjach uniwersalnych można również przenosić hello `Resources` folderu na Twojej tooshare projektu udostępnionego jego zawartości między aplikacjami, ale będzie mieć tookeep hello `Resources\EngagementConfiguration.xml` pliku w domyślnej lokalizacji, ponieważ jest on zależny platformy.
> 
> 

## <a name="enable-hello-windows-notification-service"></a>Włącz hello usługi powiadomień systemu Windows
### <a name="windows-8x-and-windows-phone-81-only"></a>Windows 8.x i Windows Phone 8.1 tylko
W kolejności toouse hello **usługi powiadomień systemu Windows** (określanych jako WNS) w Twojej `Package.appxmanifest` plików na `Application UI` kliknij `All Image Assets` hello bot po lewej stronie pola. Na powitania prawej strony pola hello w `Notifications`, zmień `toast capable` z `(not set)` zbyt`(Yes)`.

### <a name="all-platforms"></a>Wszystkie platformy
Należy toosynchronize Twojego tooyour Microsoft konta i toohello zaangażowania platformy aplikacji. W tym muszą toocreate konto lub zaloguj się na [Centrum deweloperów systemu windows](https://dev.windows.com). Po którym tworzenie nowej aplikacji i znajdowanie hello identyfikator SID i klucz tajny. Na frontonie zaangażowania hello, przejdź na ustawienia aplikacji w `native push` i Wklej swoje poświadczenia. Następnie kliknij prawym przyciskiem myszy projekt, wybierz opcję `store` i `Associate App with hello Store...`. Wystarczy, że aplikacja hello tooselect ma przed toosynchronize jego utworzeniu.

## <a name="initialize-hello-engagement-reach-sdk"></a>Zainicjuj zestaw SDK Reach usługi Engagement hello
Modyfikowanie hello `App.xaml.cs`:

* Wstaw `EngagementReach.Instance.Init` tuż po `EngagementAgent.Instance.Init` w Twojej `InitEngagement` metody:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  Witaj `EngagementReach.Instance.Init` działa w dedykowanym wątku. Nie masz toodo ją samodzielnie.

> [!NOTE]
> Jeśli używasz powiadomień wypychanych w innym miejscu w aplikacji, masz zbyt[udostępnianie kanału wypychania](#push-channel-sharing) z Reach usługi Engagement.
> 
> 

## <a name="integration"></a>Integracja
Engagement udostępnia dwa sposoby tooadd hello Reach w aplikacji transparentach i międzysegmentowe widoków w przypadku anonsów i sond w aplikacji: hello nakładki integracji i hello integracja ręczna widoki sieci web. Nie należy łączyć oba podejścia na powitania tej samej stronie.

Hello wybór między Witaj dwie integracji można podsumować w ten sposób:

* Integracja z nakładką hello może wybrać, jeśli strony już dziedziczy hello agenta `EngagementPage`, jest wystarczy zastępowanie `EngagementPage` przez `EngagementPageOverlay` i `xmlns:engagement="using:Microsoft.Azure.Engagement"` przez `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` na swoich stronach.
* Można wybrać integracji ręczne widoki sieci web hello tooprecisely miejsce hello osiągnąć interfejsu użytkownika w ramach strony lub jeśli nie chcesz tooadd innej strony poziomu tooyour dziedziczenia. 

### <a name="overlay-integration"></a>Integracja z nakładką
Hello zaangażowania nakładki są dodawane dynamicznie hello elementy interfejsu użytkownika używanych kampanie Zasięgowe toodisplay na stronie. Jeśli hello nakładki nie własnych układu należy rozważyć hello widoki sieci web integracji ręczne zamiast tego.

W przypadku zmiany pliku .xaml `EngagementPage` zbyt odwołania`EngagementPageOverlay`

* Dodaj deklaracje przestrzeni nazw tooyour:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* Zastąp `engagement:EngagementPage` z `engagement:EngagementPageOverlay`:

**Z EngagementPage:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

**Z EngagementPageOverlay:**

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

Następnie w pliku .cs tag strony w `EngagementPageOverlay` zamiast `EngagementPage` i zaimportować `Microsoft.Azure.Engagement.Overlay`.

            using Microsoft.Azure.Engagement.Overlay;

* Zastąp `EngagementPage` z `EngagementPageOverlay`:

**Z EngagementPage:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

**Z EngagementPageOverlay:**

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


Hello nakładki zaangażowania dodaje `Grid` element na stronie składa się z układ i hello dwa `WebView` elementy co hello banner i hello jeden z nich hello międzysegmentowe widoku.

Można dostosowywać elementy nakładki hello bezpośrednio w hello `EngagementPageOverlay.cs` pliku.

### <a name="web-views-manual-integration"></a>Integracja ręczna widoki sieci Web
Reach będzie wyszukiwanie stron dla hello dwa `WebView` elementy odpowiada za wyświetlanie banera hello i hello międzysegmentowe widoku. Witaj, co ma toodo jest tooadd tylko tych dwóch `WebView` elementy gdzieś na swoich stronach Oto przykład:

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


W tym hello przykład `WebView` elementy są rozciągane toofit ich kontenera, który automatycznie ponownie rozmiary je w przypadku zmiany rozmiaru ekranu obrotu lub okno.

> [!WARNING]
> Koniecznie tookeep hello tej samej nazwy `engagement_notification_content` i `engagement_announcement_content` dla hello `WebView` elementów. Zasięg identyfikuje je według nazwy. 
> 
> 

## <a name="handle-datapush-optional"></a>Dojście datapush (opcjonalnie)
Aby wypychania Twojej aplikacji toobe tooreceive stanie Reach danych, masz tooimplement dwa zdarzenia hello EngagementReach klasy:

W pliku App.xaml.cs w Konstruktorze App() hello należy dodać:

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

Wywołanie zwrotne hello każdego metoda zwraca wartość logiczną jest widoczny. Zaangażowania wysyła opinii tooits zaplecza po wysłaniu hello wypychanie danych. Jeśli wywołanie zwrotne hello zwraca wartość false, hello `exit` opinii będzie wysyłania. W przeciwnym razie będzie `action`. Jeśli bez wywołania zwrotnego ustawiono dla zdarzeń hello, hello `drop` Opinia zostanie zwrócony tooEngagement.

> [!WARNING]
> Zaangażowania nie jest możliwe tooreceive wielokrotności opinie do wypychania danych. Jeśli planujesz tooset kilka programów obsługi zdarzeń, należy pamiętać, że opinia hello będzie odpowiadać toohello ostatnią wysłane. W takim przypadku zalecamy tooalways zwraca hello tego samego tooavoid wartość o mylące opinii na powitania frontonu.
> 
> 

## <a name="customize-ui-optional"></a>Dostosowywanie interfejsu użytkownika (opcjonalne)
### <a name="first-step"></a>Pierwszym krokiem
Zezwolimy toocustomize hello reach interfejsu użytkownika.

toodo więc z toocreate podklasą hello `EngagementReachHandler` klasy.

**Przykładowy kod:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

Następnie ustaw hello zawartość hello `EngagementReach.Instance.Handler` pole z niestandardowego obiektu w Twojej `App.xaml.cs` klasa w hello `App()` — metoda.

**Przykładowy kod:**

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> Domyślnie program zaangażowania używa własną implementację `EngagementReachHandler`.
> Nie masz toocreate własny, a jeśli tak zrobisz, nie masz toooverride każdej metody. Witaj domyślne zachowanie to obiektu podstawowego tooselect hello zaangażowania.
> 
> 

### <a name="web-view"></a>Widok sieci Web
Domyślnie Reach będzie używać zasobów osadzonych hello hello DLL toodisplay hello powiadomień i strony.

tooprovide pełne możliwości dostosowywania używany tylko w widoku sieci web. Układy toocustomize należy zastąpić bezpośrednio plików zasobów hello `EngagementAnnouncement.html` i `EngagementNotification.html`. Engagement wymaga cały kod w `<body></body>` toorun poprawnie. Możesz dodać tag zewnętrzne, ale `engagement_webview_area`.

Jednak można określić toouse własnych zasobów.

Można zastąpić `EngagementReachHandler` metody w Twojej toouse zaangażowania tootell podklasy układów, ale przyjmują mechanizmu zaangażowania hello tooembedded szczególną uwagę:

**Przykładowy kod:**

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


Domyślnie jest AnnouncementHTML `ms-appx-web:///Resources/EngagementAnnouncement.html`. Reprezentuje hello plik html, który projektowania zawartości hello wiadomości wypychanych (tekst anonsu, anoucement sieci Web i anonsu sondowania). Jest AnnouncementName `engagement_announcement_content`. To nazwa hello hello projektu widoku sieci Web na stronie xaml.

Jest NotfificationHTML `ms-appx-web:///Resources/EngagementNotification.html`. Reprezentuje hello plik html, który projekt hello powiadomienie o wiadomości wypychanych. Jest NotfificationName `engagement_notification_content`. To nazwa hello hello projektu widoku sieci Web na stronie xaml.

### <a name="customization"></a>Dostosowywanie
Możesz dostosować powiadomień i anonsu widoku sieci web ma użytkownik w przypadku zachowania obiektu zaangażowania. Zajmie się obiekt widoku sieci Web jest opisano trzy razy — Witaj po raz pierwszy w Twojej xaml drugi raz w pliku .cs w metodzie "setwebview()" hello, a trzeci czas w pliku html hello.

* W Twojej xaml opisywane hello bieżącego układu graficznego widoku sieci Web składnika.
* W pliku .cs można zdefiniować "setwebview()", w którym można ustawić hello wymiaru webview dwóch hello (powiadomienia, anons). Jest bardzo skuteczne, gdy aplikacja hello jest zmiana rozmiaru.
* W pliku html zaangażowania hello nasz opisano hello webview zawartości, projektowania i hello pozycji elementy między sobą.

### <a name="launch-message"></a>Uruchamianie wiadomości
Gdy użytkownik kliknie powiadomienie systemowe (alert), Engagement uruchamia aplikacji hello, zawartość hello obciążenia hello push wiadomości i wyświetlenia strony hello hello odpowiedniego kampanii.

Występuje opóźnienie między uruchamiania hello hello aplikacji i hello wyświetlania strony hello (w zależności od szybkości hello sieci).

tooindicate toohello użytkownika, który wystąpił podczas ładowania, należy podać visual informacji, takich jak pasek postępu lub wskaźnik postępu. Zaangażowania nie może obsłużyć, ale udostępnia kilka programy obsługi dla Ciebie.

Dodaj wywołanie zwrotne hello tooimplement, w pliku App.xaml.cs "Publicznego App() {}":

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

Wywołanie zwrotne hello można ustawić w metodzie "Publicznego App() {}" z `App.xaml.cs` plików, najlepiej przed hello `EngagementReach.Instance.Init()` wywołania.

> [!TIP]
> Każdy program obsługi jest wywoływana przez hello wątku interfejsu użytkownika. Nie masz tooworry, korzystając z MessageBox lub coś związanych z interfejsu użytkownika.
> 
> 

## <a id="push-channel-sharing"></a>Wypychanie do udostępniania kanału
Jeśli używasz powiadomień wypychanych do innych celów w aplikacji należy kanału wypychanych hello toouse udostępniania funkcji hello Engagement SDK. Jest to wypychania tooavoid pominięte.

* Możesz podać własne wypychania toohello Reach usługi Engagement inicjacji kanału. Witaj zestawu SDK będą używać go zamiast nowego żądania.

Zaktualizuj hello inicjowania Reach usługi Engagement za pomocą wypychania kanału w hello `InitEngagement` metody z hello `App.xaml.cs` pliku:

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* Alternatywnie wystarczy tooconsume hello push kanału po zainicjowaniu Reach hello wywołania zwrotnego można ustawić w kanale wypychania hello tooget Reach usługi Engagement po jego utworzeniu przez hello zestawu SDK.

Ustaw wywołanie zwrotne w dowolnym miejscu **po** hello inicjowania zasięgu:

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a>Porada schematu niestandardowego
Udostępniamy Użyj schematu niestandardowego. Możesz wysłać innego typu identyfikatora URI z toobe frontonu zaangażowania używane w aplikacji usługi engagement. Domyślny schemat, takich jak `http, ftp, ...` są zarządzanie przez system Windows, zostanie okno wierszu są zainstalowane na urządzeniu domyślnej aplikacji. Można również utworzyć własny niestandardowy schemat dla aplikacji.

Witaj prosty sposób tooset schematu niestandardowego w aplikacji jest tooopen Twojego `Package.appxmanifest` Przejdź w `Declarations` panelu. Wybierz `Protocol` w hello Przewiń dostępne deklaracje i dodać go. Edytuj hello `Name` pola z Twojej nowy protokół żądaną nazwę.

Teraz toouse tego protokołu, Edytuj Twojej `App.xaml.cs` z hello `OnActivated` metody i nie zapomnij zaangażowania tooinitialize tutaj również:

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

