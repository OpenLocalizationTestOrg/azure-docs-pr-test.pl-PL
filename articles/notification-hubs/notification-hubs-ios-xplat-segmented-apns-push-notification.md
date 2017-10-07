---
title: "aaaNotification koncentratory fundamentalne wiadomości Samouczek — systemu iOS"
description: "Dowiedz się, jak toosend usługi centra powiadomień Azure Service Bus toouse fundamentalne urządzeń tooiOS powiadomień wiadomości."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Użyj usługi Notification Hubs toosend fundamentalne wiadomości
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Omówienie
W tym temacie opisano sposób toouse usługi Azure Notification Hubs toobroadcast najważniejszych wiadomości powiadomienia tooan iOS aplikacji. Po zakończeniu będzie być może tooregister zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii. Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, w której powiadomienia mają toogroups toobe wysyłane użytkowników, które wcześniej zostały zadeklarowane zainteresowanie je, np. czytnik danych RSS, aplikacje wentylatory utworów muzycznych itp.

Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień hello. Gdy tooa tag wysyłane są powiadomienia, wszystkie urządzenia, które zostały zarejestrowane dla tagu hello będzie wysyłane powiadomienie hello. Ponieważ tagi są po prostu ciągów, nie mają toobe udostępnione wcześniej. Aby uzyskać więcej informacji na temat tagów, zobacz zbyt[routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Wymagania wstępne
W tym temacie opiera się na aplikacji hello utworzony w [Rozpoczynanie pracy z usługą Notification Hubs][get-started]. Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Dodaj aplikację toohello wybór kategorii
pierwszym krokiem Hello jest tooadd hello interfejsu użytkownika elementy tooyour istniejących scenorysu umożliwiające hello użytkownika tooselect kategorii tooregister. Witaj kategorie wybrane przez użytkownika są przechowywane na urządzeniu hello. Po uruchomieniu aplikacji hello rejestracji urządzenia jest tworzony w Centrum powiadomień z kategorii hello wybrany jako znaczniki.

1. W Twojej MainStoryboard_iPhone.storyboard Dodaj hello poniższych składników z biblioteki obiektów hello:
   
   * Etykiety z tekstem "Krytyczne wiadomości"
   * Etykiety z teksty kategorii "World", "Polityka", "Business", "Technologii", "Nauki", "Sport",
   * Sześć przełączników, jeden dla każdej kategorii, ustaw każdy przełącznik **stanu** toobe **poza** domyślnie.
   * Jeden z przycisków z etykietą "Subskrybuj"
     
     Twoje scenorysu powinna wyglądać następująco:
     
     ![][3]
2. W edytorze Asystenta hello utworzyć gniazda dla wszystkich przełączników hello i połączeń telefonicznych z nimi "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"
3. Utwórz działanie dla przycisk o nazwie "subskrypcji". Twoje ViewController.h powinien zawierać następujące hello:
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. Utwórz nową **klasy Touch Cocoa** o nazwie `Notifications`. Skopiuj hello następującego kodu w sekcji interfejsu hello hello pliku Notifications.h:
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. Dodaj powitania po tooNotifications.m dyrektywy importu:
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. Skopiuj hello następującego kodu w sekcji implementacji hello hello pliku Notifications.m.
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    Ta klasa korzysta z lokalnej pamięci masowej toostore i pobrać kategorii hello wiadomości, który otrzyma tego urządzenia. Ponadto zawiera tooregister metody, dla tych kategorii przy użyciu [szablonu](notification-hubs-templates-cross-platform-push-messages.md) rejestracji.

1. W pliku AppDelegate.h hello Dodaj instrukcję import Notifications.h i dodawania właściwości dla wystąpienia hello klasy powiadomień:
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. W hello **didFinishLaunchingWithOptions** metody w AppDelegate.m, Dodaj hello kodu tooinitialize hello powiadomienia wystąpienia na początku hello hello metody.  
   
    `HUBNAME`i `HUBLISTENACCESS` (zdefiniowany w pliku hubinfo.h) ma już hello `<hub name>` i `<connection string with listen access>` symbole zastępcze zastąpione powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultListenSharedAccessSignature*uzyskany wcześniej
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, hello klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta. Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować tooregister Twojej aplikacji dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia. klucz pełny dostęp Hello jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.
   > 
   > 
3. W hello **didRegisterForRemoteNotificationsWithDeviceToken** metody w AppDelegate.m, Zamień hello kod w metodzie hello hello następującego kodu toopass hello urządzenie tokenu toohello powiadomienia klasy. Klasa powiadomienia Hello wykona hello rejestrowanie na potrzeby powiadomień z kategorii hello. Jeśli hello użytkownik zmieni ułatwia wybieranie kategorii, nazywamy hello `subscribeWithCategories` metody w odpowiedzi toohello **subskrypcji** tooupdate przycisk je.
   
   > [!NOTE]
   > Ponieważ token urządzenia hello przypisał hello Notification Service (APNS, Apple Push) szansy można w dowolnym momencie, należy zarejestrować powiadomienia o często tooavoid powiadomień błędów. W tym przykładzie rejestruje powiadomienia o każdym uruchomieniu danej aplikacji hello. Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, prawdopodobnie Jeśli możesz pominąć rejestrację toopreserve przepustowości od poprzedniej rejestracji hello upłynął krótszy niż doba.
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    Należy pamiętać, że w tym momencie nie powinno być nie innych kodu w hello **didRegisterForRemoteNotificationsWithDeviceToken** metody.

1. Hello następujących metod powinna już być obecne w AppDelegate.m ukończenie hello [Rozpoczynanie pracy z usługą Notification Hubs] [ get-started] samouczka.  Jeśli nie, dodaj je.
   
    -(void) MessageBox:(NSString *) tytułu wiadomości:(NSString *) messageText {
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * didReceiveRemoteNotification aplikacji:(UIApplication *) aplikacji (void): (NSDictionary *) informacje o użytkowniku {NSLog (@"% @", informacje o użytkowniku);   [self MessageBox:@"Notification" komunikat: [valueForKey:@"alert [informacje o użytkowniku objectForKey:@"aps"]"]]; }
   
   Ta metoda obsługuje powiadomienia otrzymane uruchomionej aplikacji hello wyświetlając prostą **UIAlert**.
2. W ViewController.m, Dodaj instrukcję import dla AppDelegate.h i skopiuj powitania po kodu na powitania generowanych przez XCode **subskrypcji** metody. Ten kod będzie aktualizować hello powiadomień rejestracji toouse hello nowej kategorii znaczniki hello użytkownik wybierze w interfejsie użytkownika hello.
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   Ta metoda tworzy **NSMutableArray** z kategorii i używa hello **powiadomienia** klasy toostore hello liście hello lokalnego magazynu i rejestruje hello odpowiednie tagi w Centrum powiadomień. Zmiana kategorii rejestracji hello zostaje odtworzone w hello nowych kategorii.
3. W ViewController.m, Dodaj hello następującego kodu w hello **viewDidLoad** interfejsu użytkownika hello tooset metody na podstawie hello wcześniej zapisany kategorii.

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



Aplikacja Hello teraz można przechowywać zestawu kategorii w hello urządzenia magazynu lokalnego używane tooregister hello Centrum powiadomień, przy każdym uruchomieniu aplikacji hello.  Hello użytkownik może zmienić wybór hello kategorii w czasie wykonywania i kliknij hello **subskrypcji** metody tooupdate hello rejestracji dla urządzenia hello. Następnie zostanie zaktualizowana hello toosend aplikacji hello fundamentalne wiadomości powiadomienia bezpośrednio w aplikacji hello.

## <a name="optional-sending-tagged-notifications"></a>(opcjonalnie) Wysyłanie powiadomień oznakowany
Jeśli nie masz dostępu tooVisual w Studio można pominąć toohello następnej sekcji i wysyłania powiadomień z samej aplikacji hello. Można również wysłać hello prawidłowego szablonu powiadomień z hello [klasycznego portalu Azure] za pomocą karty debugowanie hello Centrum powiadomień. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a>(opcjonalnie) Wysyłanie powiadomień z hello urządzenia
Zwykle usługi wewnętrznej bazy danych będą wysyłane powiadomienia, ale możesz wysłać powiadomienia o najważniejszych wiadomościach bezpośrednio z aplikacji hello. toodo to modyfikacjom hello `SendNotificationRESTAPI` metody zdefiniowanego w hello [Rozpoczynanie pracy z usługą Notification Hubs] [ get-started] samouczka.

1. W hello aktualizacji ViewController.m `SendNotificationRESTAPI` metodę jako zgodna tak, aby przyjmuje parametr hello kategorii tagu i wysyła odpowiednie hello [szablonu](notification-hubs-templates-cross-platform-push-messages.md) powiadomień.
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];
   
            [dataTask resume];
        }
2. W hello aktualizacji ViewController.m **Wyślij powiadomienie E-mail** akcji, jak pokazano w kodzie hello, który jest zgodny. Tak, aby będzie wysyłać powiadomienia hello każdego tagu indywidualnie i wysłać toomultiple platform.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. Ponownie skompiluj projekt i upewnij się, że żadne błędy kompilacji.

## <a name="run-hello-app-and-generate-notifications"></a>Uruchamianie aplikacji hello i generować powiadomienia
1. Naciśnij klawisz hello uruchomienia projektu hello toobuild przycisk i uruchomić aplikacji hello. Wybierz tooand toosubscribe niektóre najważniejszych wiadomości opcje, a następnie naciśnij klawisz hello **Subskrybuj** przycisku. Okno dialogowe wskazujący hello, które zostały subskrypcję powiadomień powinna zostać wyświetlona.
   
    ![][1]
   
    Po wybraniu **Subskrybuj**, hello kategorii hello wybrane konwertuje aplikacji do tagów i żąda nowej rejestracji urządzenia hello wybrane tagów z hello Centrum powiadomień.
2. Wprowadź toobe wiadomości wysłane w postaci naciśnij najważniejszych wiadomości powitania **Wyślij powiadomienie E-mail** przycisku. Można również uruchomić hello .NET konsoli aplikacji toogenerate powiadomienia.
   
    ![][2]
3. Każdej wiadomości toobreaking urządzenia subskrybowane otrzyma hello powiadomienia o najważniejszych wiadomościach właśnie wysłania.

## <a name="next-steps"></a>Następne kroki
W tym samouczku opisano sposób toobroadcast krytyczne według kategorii wiadomości. Należy rozważyć wykonanie jednej hello następujące samouczki dotyczące innych zaawansowanych scenariuszy centra powiadomień:

* **[Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]**
  
    Dowiedz się, jak fundamentalne wysyłania tooenable aplikacji wiadomości powitania tooexpand zlokalizowane powiadomienia.

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[klasycznego portalu Azure]: https://manage.windowsazure.com
