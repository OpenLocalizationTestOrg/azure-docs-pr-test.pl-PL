---
title: "aaaAzure Mobile Engagement iOS SDK Integration osiągnąć | Dokumentacja firmy Microsoft"
description: "Najnowsze aktualizacje i procedury dla systemu iOS SDK dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a>W jaki sposób Reach usługi Engagement tooIntegrate w systemie iOS
Musisz wykonać procedurę integracji hello opisanego w hello [jak tooIntegrate Engagement iOS dokumentu](mobile-engagement-ios-integrate-engagement.md) przed wykonaniem tego przewodnika.

Ta dokumentacja wymaga XCode 8. Jeśli naprawdę są zależne od XCode 7, możesz użyć hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Jest znaną usterką w poprzedniej podczas uruchamiania na urządzeniach z systemem iOS 10: powiadomień systemowych nie są których wykonano akcje. toofix to będzie miał tooimplement hello przestarzałe interfejsu API `application:didReceiveRemoteNotification:` w aplikacji delegowanie w następujący sposób:

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Nie zaleca się rozwiązanie** jak to zachowanie można zmienić w jakiegokolwiek uaktualnienia wersji nadchodzących iOS (nawet pomocnicze), ponieważ ten iOS interfejsu API jest przestarzały. Należy jak najszybciej przełącznika tooXCode 8.
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Włącz tooreceive Twojej aplikacji cichych powiadomień wypychanych
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a>Kroki integracji
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a>Osadź hello Engagement Reach SDK do projektu systemu iOS
* Dodawanie zestawu sdk modułu Reach hello w projekcie Xcode. W środowisku Xcode Przejdź zbyt**projektu \> dodać tooproject** i wybierz polecenie hello `EngagementReach` folderu.

### <a name="modify-your-application-delegate"></a>Modyfikowanie delegata aplikacji
* U góry hello pliku implementacji Zaimportuj moduł Reach usługi Engagement hello:

      [...]
      #import "AEReachModule.h"
* Wewnątrz metody `applicationDidFinishLaunching:` lub `application:didFinishLaunchingWithOptions:`, Utwórz moduł reach i przekaż go tooyour istniejącego wiersza inicjowania usługi Engagement:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* Modyfikowanie **"icon.png"** ciągu o nazwie obraz powitania ma jako ikonę powiadomienia.
* Jeśli chcesz, aby opcja hello toouse *wartość wskaźnika aktualizacji* kampanie Zasięgowe lub jeśli chcesz natywnych powiadomień wypychanych toouse \<SaaS/Reach interfejsu API/kampanii format/Native Push\> kampanie, należy przeprowadzić moduł Reach hello Zarządzanie Witaj wskaźnika ikona sam (zostanie automatycznie usunięty wskaźnika aplikacji hello i również zresetować wartość hello przechowywane przez zaangażowania za każdym razem, gdy aplikacja hello jest uruchomiony lub foregrounded). Można to zrobić przez dodanie następującego wiersza po zainicjowaniu modułu Reach hello:

      [reach setAutoBadgeEnabled:YES];
* Jeśli chcesz wypychanie danych Reach toohandle musi umożliwić delegata aplikacji jest zgodna z toohello `AEReachDataPushDelegate` protokołu. Dodaj następującego wiersza po zainicjowaniu modułu Reach hello:

      [reach setDataPushDelegate:self];
* Następnie można zaimplementować metody hello `onDataPushStringReceived:` i `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` w delegata aplikacji:

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a>Kategoria
Witaj kategorii parametr jest opcjonalny, podczas tworzenia kampanii wypychania danych i umożliwia wypychanie danych toofilter. Jest to przydatne w przypadku różnych rodzajów toopush z `Base64` tooidentify danych i chcesz ich typu przed ich analizowania.

**Aplikacja jest teraz gotowy tooreceive i wyświetlanie osiągnąć zawartość!**

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a>Jak tooreceive anonsów i sond w dowolnym momencie
Zaangażowania można wysłać powiadomienia Reach tooyour użytkowników końcowych w dowolnym momencie przy użyciu hello Apple Push Notification Service.

tooenable ta funkcja zostanie tooprepare aplikacji dla powiadomień wypychanych firmy Apple oraz modyfikowanie delegata aplikacji.

### <a name="prepare-your-application-for-apple-push-notifications"></a>Przygotowanie aplikacji dla powiadomień wypychanych firmy Apple
Wykonaj przewodnik hello: [jak tooPrepare aplikacji dla powiadomień wypychanych firmy Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

### <a name="add-hello-necessary-client-code"></a>Dodaj kod klienta konieczne hello
*W tym momencie aplikacji powinien mieć zarejestrowany certyfikat usługi Apple push hello zaangażowania frontonu.*

Jeśli nie jest jeszcze zrobione, należy tooregister powiadomień wypychanych tooreceive aplikacji.

* Importuj hello `User Notification` framework:

        #import <UserNotifications/UserNotifications.h>
* Dodaj powitania po wierszu, po uruchomieniu aplikacji (zwykle w `application:didFinishLaunchingWithOptions:`):

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

Następnie należy tooprovide tooEngagement hello urządzenia tokenów zwracanych przez serwery firmy Apple. Odbywa się w metodzie hello o nazwie `application:didRegisterForRemoteNotificationsWithDeviceToken:` w delegata aplikacji:

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

Koniec mamy jeszcze hello tooinform Engagement SDK, gdy aplikacja otrzyma powiadomienie zdalnego. toodo, który wywołać hello metody `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` w delegata aplikacji:

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> Domyślnie Reach usługi Engagement steruje hello completionHandler. Jeśli chcesz, aby toohello odpowiedź toomanually `handler` bloków w kodzie, można przekazać nil dla hello `handler` argumentu i kontroli uzupełniania hello zablokować samodzielnie. Zobacz hello `UIBackgroundFetchResult` typu listę możliwych wartości.
>
>

### <a name="full-example"></a>Pełny przykład
Oto pełny przykład integracji:

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Rozwiązywanie konfliktów delegata UNUserNotificationCenter

*Jeśli implementuje jednej z bibliotek innych firm ani aplikacji `UNUserNotificationCenterDelegate` , a następnie można pominąć tej części.*

A `UNUserNotificationCenter` delegata jest używany przez hello SDK toomonitor hello cyklu życia zaangażowania powiadomienia na urządzeniach z systemem iOS, 10 lub nowszy. Witaj SDK ma własną implementację hello `UNUserNotificationCenterDelegate` protokołu, ale może istnieć tylko jedna `UNUserNotificationCenter` delegować na aplikację. Inne delegata dodane toohello `UNUserNotificationCenter` obiektu może powodować konflikt z hello zaangażowania jeden. Jeśli hello SDK wykryje użytkownika lub dowolnej innej strony trzeciej na delegata nie zastosuje toogive własną implementację możesz tooresolve szansy hello konfliktów. Konieczne będzie tooadd hello zaangażowania logiki tooyour właścicielem delegata w kolejności tooresolve hello konfliktów.

Istnieją dwa sposoby tooachieve to.

Wniosek 1, po prostu przesyłając pełnomocnika wywołuje toohello zestawu SDK:

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

Lub propozycji 2, dziedziczenie z hello `AEUserNotificationHandler` — klasa

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> Można określić, czy powiadomienie jest dostarczany z zaangażowania lub nie przez przekazanie jej `userInfo` toohello słownika agenta `isEngagementPushPayload:` metoda klasy.

Upewnij się, że hello `UNUserNotificationCenter` obiektu delegowanego ustawiono tooyour delegata w obu hello `application:willFinishLaunchingWithOptions:` lub hello `application:didFinishLaunchingWithOptions:` metody delegata aplikacji.
Na przykład jeśli zaimplementowano hello powyżej wniosek 1:

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a>Jak toocustomize kampanii
### <a name="notifications"></a>Powiadomienia
Istnieją dwa typy powiadomień: powiadomień systemowych i w aplikacji.

Powiadomienia systemowe są obsługiwane przez system iOS i nie można dostosować.

W aplikacji zawiadomienia widoku, który jest dodawane dynamicznie toohello bieżące okno aplikacji. Jest to nakładce powiadomienia. Nakładki powiadomienia są bardzo szybkiego integracji, ponieważ wymagają one, nie możesz toomodify dowolnym widoku w aplikacji.

#### <a name="layout"></a>Układ
wygląd hello toomodify powiadomienia w aplikacji, wystarczy zmodyfikować plik hello `AENotificationView.xib` tooyour musi, tak długo, jak zabezpieczyć hello wartości tagów i typy widoków istniejących podrzędnych hello.

Domyślnie powiadomienia w aplikacji są prezentowane u dołu hello hello ekranu. Jeśli wolisz toodisplay je u góry ekranu, Edytuj hello hello udostępnione `AENotificationView.xib` i zmień hello `AutoSizing` właściwości hello widoku głównego, mogą być przechowywane na górze hello jego superview.

#### <a name="categories"></a>Kategorie
Po zmodyfikowaniu hello podane układu, możesz zmodyfikować wygląd hello wszystkich powiadomień. Kategorie dopuszczać toodefine możesz przez różne docelowe szuka powiadomienia (prawdopodobnie zachowania). Po utworzeniu kampanii Reach można określić kategorię. Należy pamiętać, że kategorie pozwalają również dostosować anonsów i sond, opisane w dalszej części tego dokumentu.

tooregister kategorii Obsługa powiadomienia, należy tooadd wywołania po modułu reach hello jest zainicjowana.

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

`myNotifier`musi być wystąpieniem obiektu, który jest zgodny z protokołem toohello `AENotifier`.

Można zaimplementować metody protokołu hello samodzielnie lub możesz wybrać tooreimplement hello istniejącej klasy `AEDefaultNotifier` którego już wykonuje większość pracy hello.

Na przykład jeśli chcesz widok powiadomienia hello tooredefine dla określonej kategorii, należy wykonać w tym przykładzie:

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

Ten prosty przykład kategorii założono, że istnieje plik o nazwie `MyNotificationView.xib` w Twojego pakietu aplikacji głównej. Jeśli metoda hello nie jest możliwe toofind odpowiadającego `.xib`, nie będą wyświetlane powiadomienia hello i zaangażowania dane wyjściowe obejmują wiadomość hello konsoli.

Hello podane nib pliku powinna być zgodna hello następujące reguły:

* Powinna ona zawierać tylko jeden widok.
* Widoków podrzędnych powinny być hello typy takie same jak hello tych wewnątrz hello podane nib plik o nazwie`AENotificationView.xib`
* Widoków podrzędnych powinny mieć hello znaczniki takie same jak hello tych wewnątrz hello podane nib plik o nazwie`AENotificationView.xib`

> [!TIP]
> Po prostu skopiuj hello podane nib plik o nazwie `AENotificationView.xib`i rozpocząć pracę z tego miejsca. Jednak należy zachować ostrożność, hello widoku wewnątrz ten plik nib jest skojarzona klasa toohello `AENotificationView`. Ta klasa ponownie definiować metody hello `layoutSubViews` toomove i zmień rozmiar jego widoków podrzędnych zgodnie z toocontext. Może być tooreplace za pomocą `UIView` lub klasy widok niestandardowy.
>
>

Jeśli potrzebujesz bardziej dostosowywania powiadomienia (Jeśli na przykład tooload widoku bezpośrednio z kodu hello), zalecane jest tootake przyjrzeć się hello podano źródła kodu i klasy w dokumentacji `Protocol ReferencesDefaultNotifier` i `AENotifier`.

Należy pamiętać, że można użyć hello tego samego zgłaszający dla wielu kategorii.

Można również ponownie zdefiniowany hello domyślne zgłaszający następująco:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a>Obsługa powiadomień
Korzystając z kategorii domyślnej hello, w przypadku niektórych metod cyklu życia są nazywane na powitania `AEReachContent` obiekt tooreport statystyk i aktualizacji hello kampanii stanu:

* Po wyświetleniu powiadomienia hello w aplikacji hello `displayNotification` metoda jest wywoływana (która statystyki) przez `AEReachModule` Jeśli `handleNotification:` zwraca `YES`.
* Jeśli powiadomienia hello jest odrzucane, hello `exitNotification` metoda jest wywoływana, statystyka jest zgłaszany i dalej kampanii teraz mogą być przetwarzane.
* Po kliknięciu hello powiadomień `actionNotification` jest wywoływana, statystyka jest zgłaszany i hello skojarzona akcja jest wykonywana.

Jeśli implementacji `AENotifier` pomija hello domyślne zachowanie, należy toocall tych metod cyklu życia samodzielnie. Hello następujące przykłady przedstawiają niektórych przypadkach, gdy pomijana jest hello domyślne zachowanie:

* Nie można rozszerzyć `AEDefaultNotifier`, np. zaimplementowano obsługi kategorii od początku.
* Możesz overrode `prepareNotificationView:forContent:`, toomap się, że co najmniej `onNotificationActioned` lub `onNotificationExited` tooone formantów U.I.

> [!WARNING]
> Jeśli `handleNotification:` zwraca wyjątek, hello zawartości zostanie usunięty i `drop` jest wywoływana, jest to raportowane w statystykach i dalej kampanii teraz mogą być przetwarzane.
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a>Powiadomienia jako część istniejącego widoku
Nakładki są bardzo szybkiego integracji, ale może nie może być czasami wygodne lub może mieć niepożądane skutki uboczne.

Jeśli użytkownik nie ma spełnia Twoje wymagania systemu nakładki hello w niektórych widoków, można dostosować go do tych widoków.

Można zdecydować, tooinclude naszych układu powiadomień w istniejących widoków. toodo tak, brak dwa style implementacji:

1. Dodaj widok powiadomienia hello przy użyciu narzędzia Konstruktor interfejsu

   * Otwórz *interfejsu konstruktora*
   * Umieść 320 x 60 (lub jeśli iPad 768 x 60) `UIView` miejscu hello tooappear powiadomień
   * Ustaw wartość tagu powitania dla tego widoku zbyt: **36822491**
2. Dodaj widok powiadomienia hello programowo. Po prostu Dodaj hello następującego kodu po zainicjowaniu widoku:

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

`NOTIFICATION_AREA_VIEW_TAG`Makro można znaleźć w `AEDefaultNotifier.h`.

> [!NOTE]
> zgłaszający domyślne Hello automatycznie wykrywa taki układ powiadomień hello znajduje się w tym widoku i nie dodają nakładki dla niego.
>
>

### <a name="announcements-and-polls"></a>Anonsów i sond
#### <a name="layouts"></a>Układy
Można zmodyfikować plików hello `AEDefaultAnnouncementView.xib` i `AEDefaultPollView.xib` tak długo, jak zabezpieczyć hello wartości tagów i typy widoków istniejących podrzędnych hello.

#### <a name="categories"></a>Kategorie
##### <a name="alternate-layouts"></a>Układy alternatywnej
Jak powiadomienia Kategoria kampanii hello mogą być używane toohave alternatywne układy anonsów i sond.

toocreate kategorii anonsu, należy rozszerzyć **AEAnnouncementViewController** i zarejestruj go po zainicjowaniu moduł reach hello:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> Każdym razem, użytkownik będzie kliknij powiadomienie anonsu z kategorią hello "Mój\_kategorii", kontroler widoku zarejestrowane (w takim przypadku `MyCustomAnnouncementViewController`) zostanie zainicjowana przez wywołanie metody hello `initWithAnnouncement:` i widok hello będzie Dodano toohello bieżące okno aplikacji.
>
>

W implementacji hello `AEAnnouncementViewController` klasy mają właściwość hello tooread `announcement` tooinitialize Twojego widoków podrzędnych. Rozważ przykład Witaj poniżej, w przypadku, gdy dwie etykiety są inicjowane przy użyciu `title` i `body` właściwości hello `AEReachAnnouncement` klasy:

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

Jeśli nie chcesz tooload widoków samodzielnie, ale chcesz tooreuse hello domyślny anonsu widoku Układ, po prostu ułatwia kontroler niestandardowy widok rozszerza klasę hello podane `AEDefaultAnnouncementViewController`. W takim przypadku zduplikowane hello nib pliku `AEDefaultAnnouncementView.xib` i zmień jego nazwę, dlatego może być załadowany przez kontroler niestandardowy widok (dla kontrolera o nazwie `CustomAnnouncementViewController`, należy wywołać pliku nib `CustomAnnouncementView.xib`).

tooreplace hello domyślnej kategorii anonsów, po prostu zarejestrować Kontroler Widok niestandardowy kategorii hello zdefiniowane w `kAEReachDefaultCategory`:

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

Ankiety może być dostosowane hello taki sam sposób:

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

Ten czas, podany hello `MyCustomPollViewController` muszą być rozszerzane `AEPollViewController`. Lub możesz wybrać tooextend hello domyślnego kontrolera: `AEDefaultPollViewController`.

> [!IMPORTANT]
> Nie zapomnij toocall albo `action` (`submitAnswers:` kontrolerów widok niestandardowy sondowania) lub `exit` metoda przed kontrolera widoku hello jest odrzucane. W przeciwnym razie statystyki nie zostaną wysłane (tzn. nie analizy kampanii hello) i więcej kampanii istotne dalej nie zostaną powiadomieni do ponownego uruchomienia procesu aplikacji hello.
>
>

##### <a name="implementation-example"></a>Przykład wdrożenia
W tej implementacji widok niestandardowy anonsu hello są ładowane z pliku xib zewnętrznych.

Podobnie jak dostosowywania powiadomień zaawansowane, zalecane jest toolook na kod źródłowy hello hello standardowej implementacji.

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
