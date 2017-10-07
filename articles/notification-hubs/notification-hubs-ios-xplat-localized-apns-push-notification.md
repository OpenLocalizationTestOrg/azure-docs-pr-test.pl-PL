---
title: "aaaNotification koncentratory zlokalizowane fundamentalne wiadomości samouczek dla systemu iOS"
description: "Dowiedz się, jak toosend usługi centra powiadomień Azure Service Bus toouse zlokalizowane powiadomienia o najważniejszych wiadomościach (iOS)."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a>Używanie urządzeń tooiOS wiadomości podziału toosend zlokalizowane centra powiadomień
> [!div class="op_single_selector"]
> * [Sklep Windows C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Omówienie
W tym temacie opisano sposób toouse hello [szablony](notification-hubs-templates-cross-platform-push-messages.md) funkcji usługi Azure Notification Hubs toobroadcast fundamentalne powiadomień wiadomości, które zostały zlokalizowane według języka i urządzenia. W tym samouczku początkowo utworzony w aplikacji dla systemu iOS hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości]. Po zakończeniu będziesz w stanie tooregister dla kategorii, które planuje się, określ język w powiadomienia, które hello tooreceive i otrzymywać tylko powiadomienia wypychane dla kategorii hello wybrany w tym języku.

Istnieją dwie części toothis scenariusza:

* Aplikacja systemu iOS umożliwia klienta toospecify urządzeń język i toodifferent toosubscribe fundamentalne kategorie nowości;
* Witaj zaplecza emituje hello powiadomień, przy użyciu hello **tag** i **szablonu** feautres usługi Azure Notification Hubs.

## <a name="prerequisites"></a>Wymagania wstępne
Należy zostały już wykonane hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] samouczka i mieć kod hello jest dostępne, ponieważ w tym samouczku bezpośrednio oparta na kod.

Visual Studio 2012 lub nowszy jest opcjonalna.

## <a name="template-concepts"></a>Pojęcia dotyczące szablonów
W [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] utworzono aplikację, która jest używana **tagi** toonotifications toosubscribe dla różnych grup dyskusyjnych kategorii.
Wiele aplikacji, jednak docelowy kilku rynkach i wymagają lokalizacji. Oznacza to, czy zawartość hello hello powiadomień, się toobe zlokalizowane i dostarczonego toohello Popraw zbiór urządzeń.
W tym temacie pokazano, jak toouse hello **szablonu** funkcji tooeasily świadczenia usługi Notification Hubs zlokalizowane powiadomienia o najważniejszych wiadomościach.

Uwaga: jednokierunkowej toosend zlokalizowane powiadomień jest toocreate wiele wersji każdego znacznika. Na przykład toosupport angielskim, francuskim i mandaryński, potrzebujemy czy trzy różne znaczniki dla wiadomości world: "world_en", "world_fr" i "world_ch". Firma Microsoft będzie zmuszony toosend zlokalizowanej wersji hello world wiadomości tooeach tych tagów. W tym temacie używamy szablony tooavoid hello mnożenie tagów i wymagania hello wielu operacji wysyłania wiadomości.

Na wysokim poziomie, szablony są toospecify sposób jak określonym urządzeniu powinno zostać odebrane powiadomienie. Szablon Hello Określa format ładunku dokładne hello odwołując tooproperties, które są częścią hello wiadomość wysłana przez zaplecze Twojej aplikacji. W tym przypadku firma Microsoft wyśle komunikat niezależny od ustawień regionalnych zawierający wszystkie obsługiwane języki:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Następnie firma Microsoft zapewnia Zarejestruj szablon, który odwołuje się właściwość poprawne toohello przez urządzenia. Na przykład aplikację systemu iOS, która potrzebuje tooregister dla wiadomości francuskim zarejestruje hello poniżej:

    {
        aps:{
            alert: "$(News_French)"
        }
    }

Szablony są bardzo przydatna funkcja, możesz dowiedzieć się więcej w naszym [szablony](notification-hubs-templates-cross-platform-push-messages.md) artykułu.

## <a name="hello-app-user-interface"></a>Interfejs użytkownika aplikacji Hello
Firma Microsoft będzie teraz zmodyfikować aplikacji fundamentalne wiadomości powitania, utworzonego w temacie hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] toosend zlokalizowane najważniejszych wiadomości przy użyciu szablonów.

W Twojej MainStoryboard_iPhone.storyboard dodać kontrolkę segmentu z językami hello trzech, które firma Microsoft będzie obsługiwać: angielski, francuski i mandaryński.

![][13]

Następnie upewnij się, że tooadd IBOutlet w Twojej ViewController.h w sposób przedstawiony poniżej:

![][14]

## <a name="building-hello-ios-app"></a>IOS — aplikacja hello kompilowanie
1. W Twojej Notification.h dodać hello *retrieveLocale* metody i zmodyfikować hello magazynu oraz subskrybowania metody, jak pokazano poniżej:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    W Twojej Notification.m zmodyfikować hello *storeCategoriesAndSubscribe* metody, dodając parametr ustawień regionalnych hello i przechowywanie ich w ustawieniach domyślnych użytkownika hello:
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    Następnie zmodyfikuj hello *subskrypcji* ustawień regionalnych hello tooinclude metody:
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    Należy zwrócić uwagę, jak teraz użyto metody hello *registerTemplateWithDeviceToken*, zamiast *registerNativeWithDeviceToken*. Gdy firma Microsoft rejestrowania dla szablonu mamy tooprovide hello json szablonu, a także nazwę dla szablonu hello (zgodnie z naszej aplikacji może być tooregister różnych szablonów). Upewnij się, że tooregister kategorie jako tagi, zgodnie z chcemy się notifciations hello tooreceive toomake dla tych wiadomości.
   
    Dodaj ustawień regionalnych hello tooretrieve metody w ustawieniach domyślnych użytkownika hello:
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. Teraz, gdy firma Microsoft zmodyfikowane klasy Nasze powiadomienia, mamy toomake się upewnić, że nasze ViewController sprawia, że użycie hello UISegmentControl nowe. Dodaj powitania po wierszu hello *viewDidLoad* metody toomake czy tooshow hello ustawień regionalnych aktualnie wybranego:
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    Następnie w Twojej *subskrypcji* metody, zmień Twoje toohello wywołania *storeCategoriesAndSubscribe* toohello następujące:
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. Na koniec masz tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* w Twojej AppDelegate.m metody, dzięki czemu można poprawnie odświeżyć rejestracji podczas uruchamiania aplikacji. Zmień toohello Twojego wywołania *subskrypcji* metody powiadomienia przy użyciu następujących hello:
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a>(opcjonalnie) Wysyłanie powiadomień zlokalizowanego szablonu z aplikacji konsoli .NET.
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a>(opcjonalnie) Wysyłanie powiadomień zlokalizowanego szablonu z hello urządzenia
Jeśli nie masz dostępu tooVisual w Studio lub mają testu toojust wysyłanie powiadomień szablonu hello zlokalizowane bezpośrednio z aplikacji hello hello urządzenia.  Można w prosty dodać toohello parametry szablonu hello zlokalizowane `SendNotificationRESTAPI` metody zdefiniowanej w samouczku poprzedniej hello.

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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

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




## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat używania szablonów zobacz:

* [Powiadom użytkowników z usługą Notification Hubs: ASP.NET]
* [Powiadom użytkowników z usługą Notification Hubs: Mobile Services]

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Powiadom użytkowników z usługą Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Powiadom użytkowników z usługą Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
