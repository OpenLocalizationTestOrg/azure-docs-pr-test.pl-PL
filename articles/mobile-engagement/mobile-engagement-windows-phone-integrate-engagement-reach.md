---
title: "aaaWindows osiągnąć integracji zestawu SDK programu Phone Silverlight"
description: "Jak tooIntegrate usługi Azure Mobile Engagement nawiązać połączenia z aplikacjami programu Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Windows Phone Silverlight dotarcia do integracji zestawu SDK
Musisz wykonać procedurę integracji hello opisanego w hello [integracji zestawu SDK usługi Engagement Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) przed wykonaniem tego przewodnika.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>Osadź hello Engagement Reach SDK do projektu systemu Windows Phone Silverlight
Nie masz żadnych tooadd. `EngagementReach`referencje i zasoby są już w projekcie.

> [!TIP]
> Można dostosować obrazy znajdujące się w hello `Resources` folderu projektu, szczególnie hello brand ikona (tej domyślnej toohello Engagement).
> 
> 

## <a name="add-hello-capabilities"></a>Dodawanie funkcji hello
zestaw SDK Reach usługi Engagement Hello musi niektóre dodatkowe funkcje.

Otwórz z `WMAppManifest.xml` plików i pamiętaj, że hello następujące funkcje są deklarowane jako:

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

Hello najpierw jednym jest używana przez hello MPNS usługi tooallow hello wyświetlanie wyskakujących powiadomień. Witaj drugim jest używane tooembed zadania przeglądarki do hello zestawu SDK.

Edytuj hello `WMAppManifest.xml` plik i dodać wewnątrz hello `<Capabilities />` tagu:

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>Włącz hello Microsoft Push Notification Service
W kolejności toouse hello **Microsoft Push Notification Service** (określanych jako usługi MPNS) z `WMAppManifest.xml` plik musi mieć `<App />` tagu z `Publisher` ustawiony atrybut toohello nazwę projektu.

## <a name="initialize-hello-engagement-reach-sdk"></a>Zainicjuj zestaw SDK Reach usługi Engagement hello
### <a name="engagement-configuration"></a>Konfiguracja usługi Engagement
konfiguracji usługi Engagement Hello jest scentralizowana w hello `Resources\EngagementConfiguration.xml` pliku projektu.

Zmień konfigurację reach toospecify tego pliku:

* *Opcjonalne*, wskazuje, czy włączono hello natywnych powiadomień wypychanych (MPNS), czy między `<enableNativePush>` i `</enableNativePush>` tagi (`true` domyślnie).
* *Opcjonalne*, nazwa hello kanału wypychanych hello między `<channelName>` i `</channelName>` tagów, podaj hello tej samej aplikacji mogą obecnie korzystać lub pozostaw puste.

Jeśli chcesz, aby toospecify go w czasie wykonywania zamiast tego możesz wywołać program hello następujące metody przed zainicjowaniem agenta zaangażowania hello:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> Można określić nazwę hello kanału wypychanych usługi MPNS hello aplikacji. Domyślnie program zaangażowania tworzy nazwę oparte na powitania appId. Możesz nie mieć potrzeby toospecify hello nazwy użytkownika, z wyjątkiem przypadków, jeśli planujesz kanału wypychanych hello toouse poza zaangażowania.
> 
> 

### <a name="engagement-initialization"></a>Inicjowania usługi Engagement
Modyfikowanie hello `App.xaml.cs`:

* Dodaj tooyour `using` instrukcji:
  
      using Microsoft.Azure.Engagement;
* Wstaw `EngagementReach.Instance.Init` tuż po `EngagementAgent.Instance.Init` w `Application_Launching` :
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* Wstaw `EngagementReach.Instance.OnActivated` w hello `Application_Activated` metody:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> Witaj `EngagementReach.Instance.Init` działa w dedykowanym wątku. Nie masz toodo ją samodzielnie.
> 
> 

## <a name="app-store-submission-considerations"></a>Zagadnienia dotyczące przesyłania magazynu aplikacji
Microsoft nakłada niektórych reguł przy użyciu powiadomień wypychanych hello:

Z hello Microsoft [zasady aplikacji] dokumentacji, sekcja 2.9:

1) Musisz poprosić hello wysyłanie powiadomień wypychanych tooreceive tooaccept użytkownika. Następnie w ustawieniach, należy dodać powiadomień wypychanych hello toodisable sposób.

Obiekt EngagementReach Hello oferuje dwie metody toomanage hello w/opt — zrezygnować, `EnableNativePush()` i `DisableNativePush()`. Można na przykład utworzyć opcję w ustawieniach hello z toodisable przełącznika lub włączyć usługi MPNS.

Można również określić, że toodeactivate MPNS za pomocą konfiguracji zaangażowania hello\<konfiguracji systemu windows-phone-sdk-reach —\>.

> 2.9.1) aplikacji hello najpierw musi opisywać toobe powiadomienia hello podane i **uzyskać wyraźnej zgody użytkownika hello (opt — ruch przychodzący)**, i **podać mechanizm, za pomocą których hello użytkownik może zrezygnować z odbierania powiadomienia wypychane**. Wszystkie powiadomienia realizowane przy użyciu usługi powiadomień wypychanych firmy Microsoft hello muszą być zgodne z hello dostarczony opis toohello użytkownika i musi spełniać wszystkie odpowiednie [zasady aplikacji] [ Content Policies]i [dodatkowe wymagania dotyczące typów określonej aplikacji].
> 
> 

2) Nie należy używać zbyt wiele powiadomień wypychanych. Zaangażowania obsługi powiadomień dla Ciebie.

> 2.9.2) aplikacji hello i jego użycie hello Microsoft Push Notification Service musi nie nadmiernie pojemność sieci lub przepustowości hello usługi powiadomień wypychanych firmy Microsoft lub w przeciwnym razie nadmiernie obciążać Windows Phone lub innych urządzeń firmy Microsoft lub usługi z nadmiernego powiadomień wypychanych, zgodnie z ustaleniami firmy Microsoft uznania i nie musi uszkodzić lub zakłócać żadnych sieci firmy Microsoft lub serwerów lub dowolnych innych firm lub serwerów sieci toohello podłączonej usługi powiadomień wypychanych firmy Microsoft.
> 
> 

3) Nie należy polegać na MPNS toosend criticals informacji. Zaangażowania używana jest usługa MPNS, więc ta reguła ma zastosowanie również kampanii hello tworzone wewnątrz hello zaangażowania frontonu.

> 2.9.3) hello usługi powiadomień wypychanych firmy Microsoft nie może być używane toosend powiadomień, które są misji krytycznych lub w inny sposób mogą wpłynąć na sprawach życia lub śmierci, w tym bez urządzenia medyczne pokrewne tooa krytyczne powiadomienia ograniczenia lub warunku. MICROSOFT wyraźnie, że nie ponosi ANY gwarancji czy hello użycia z hello MICROSOFT PUSH POWIADOMIEŃ usługi lub DOSTARCZANIA z MICROSOFT PUSH POWIADOMIEŃ usługi POWIADOMIEŃ będzie można nieprzerwaną, bez błędów, lub w inny sposób gwarantowane tooOCCUR ON A w czasie rzeczywistym podstawy.
> 
> 

**Nie możemy zagwarantować aplikacji przekazuje proces weryfikacji hello Jeśli nie przestrzega te zalecenia.**

## <a name="handle-data-push-optional"></a>Obsługa wypychanie danych (opcjonalnie)
Aby wypychania Twojej aplikacji toobe tooreceive stanie Reach danych, masz tooimplement dwa zdarzenia hello EngagementReach klasy:

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

Następnie ustaw hello zawartość hello `EngagementReach.Instance.Handler` pole z niestandardowego obiektu w Twojej `App.xaml.cs` klasa w hello `Application_Launching` — metoda.

**Przykładowy kod:**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> Domyślnie program zaangażowania używa własną implementację `EngagementReachHandler`. Nie masz toocreate własny, a jeśli tak zrobisz, nie masz toooverride każdej metody. Witaj domyślne zachowanie to obiektu podstawowego tooselect hello zaangażowania.
> 
> 

### <a name="layouts"></a>Układy
Domyślnie Reach będzie używać zasobów osadzonych hello hello DLL toodisplay hello powiadomień i strony.

Jednak można zdecydować, toouse tooreflect własnych zasobów oznakowanie w tych składników.

Można zastąpić `EngagementReachHandler` metod w Twojej toouse zaangażowania tootell podklasy układów:

**Przykładowy kod:**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> Witaj `CreateNotification` metoda może zwracać wartości zerowej. nie będą wyświetlane powiadomienia Hello, które zostaną usunięte hello reach kampanii.
> 
> 

toosimplify implementacji układu, firma Microsoft udostępnia również własnej xaml, który może służyć jako podstawa dla kodu. Znajdują się one w archiwum Engagement SDK hello (/ src/reach /).

> [!WARNING]
> Hello źródeł, które firma Microsoft udostępnia są dokładnie takie same jak których używamy hello. Dlatego toomodify je bezpośrednio, nie zapomnij toochange hello w przestrzeni nazw i hello nazwy.
> 
> 

### <a name="notification-position"></a>Pozycja powiadomień
Domyślnie na powitania lewym dolnym rogu aplikacji hello zostanie wyświetlone powiadomienie w aplikacji. Możesz zmienić to zachowanie przez zastąpienie hello `GetNotificationPosition` metody hello `EngagementReachHandler` obiektu.

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

Obecnie można wybrać hello `BOTTOM` (ustawienie domyślne) i `TOP` pozycji.

### <a name="launch-message"></a>Uruchamianie wiadomości
Gdy użytkownik kliknie powiadomienie systemowe (alert), aplikacji hello powoduje uruchomienie zaangażowania, zawartość hello obciążenia hello push wiadomości i wyświetlić stronę hello hello odpowiadającego kampanii.

Występuje opóźnienie między uruchamiania hello hello aplikacji i hello wyświetlania strony hello (w zależności od szybkości hello sieci).

tooindicate toohello użytkownika, który wystąpił podczas ładowania, należy podać visual informacji, takich jak pasek postępu lub wskaźnik postępu. Zaangażowania nie może obsłużyć, ale udostępnia kilka programy obsługi dla Ciebie.

tooimplement hello wywołania zwrotnego, czy:

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

Hello wywołania zwrotnego można ustawić w Twojej `Application_Launching` metody z `App.xaml.cs` plików, najlepiej przed hello `EngagementReach.Instance.Init()` wywołania.

> [!TIP]
> Każdy program obsługi jest wywoływana przez hello wątku interfejsu użytkownika. Nie masz tooworry, korzystając z MessageBox lub coś związanych z interfejsu użytkownika.
> 
> 

[zasady aplikacji]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[dodatkowe wymagania dotyczące typów określonej aplikacji]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

