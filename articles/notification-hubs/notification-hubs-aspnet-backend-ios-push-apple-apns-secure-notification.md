---
title: aaaAzure powiadomienia Push Secure koncentratory
description: "Dowiedz się, jak bezpieczne toosend push aplikacji dla systemu iOS tooan powiadomienia z platformy Azure. Przykłady kodu napisane w języku Objective C i C#."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Azure Notification Hubs bezpiecznego Push
> [!div class="op_single_selector"]
> * [Aplikacje uniwersalne systemu Windows](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Omówienie
Obsługa powiadomień wypychanych w Microsoft Azure umożliwia tooaccess infrastruktury wypychania łatwy w użyciu, wieloplatformową skalowalnych w poziomie, który jest znacznie ułatwione hello stosowania powiadomienia wypychane zarówno konsumenckie i korporacyjne aplikacji dla urządzeń przenośnych platform.

Czasami ze względu na ograniczenia tooregulatory lub zabezpieczeń, aplikacja może być tooinclude coś w hello powiadomienie, które nie są przesyłane za pośrednictwem infrastruktury powiadomień wypychanych standardowe hello. W tym samouczku opisano, jak tooachieve hello tego samego środowiska poprzez wysłanie poufnych informacji za pośrednictwem bezpiecznego połączenia uwierzytelnionego między powitania klienta urządzenia i aplikacji hello wewnętrznej bazy danych.

Na wysokim poziomie przepływu hello jest następujący:

1. Witaj zaplecze aplikacji:
   * Magazyny bezpiecznego ładunku w wewnętrznej bazie danych.
   * Wysyła identyfikator hello tego urządzenia toohello powiadomienie (nie bezpiecznego informacje są wysyłane).
2. Aplikacja Hello na urządzeniu hello podczas odbierania powiadomień hello:
   * urządzenie Hello kontaktuje się hello zaplecza żądania hello bezpiecznego ładunku.
   * Aplikacja Hello można wyświetlić ładunku hello jako powiadomienie na urządzeniu hello.

Jest ważne toonote, że w hello poprzedzających przepływu (i w tym samouczku) przyjęto założenie, urządzenia hello po zalogowaniu użytkownika hello przechowuje token uwierzytelniania w magazynie lokalnym. Gwarantuje to całkowicie sprawnie, jak urządzenia hello mogą pobierać ładunku bezpiecznego hello powiadomienia za pomocą tego tokenu. Jeśli aplikacja nie przechowuje tokeny uwierzytelniania na urządzeniu hello lub tokeny te mogą wygasnąć, hello aplikacji urządzenia po otrzymaniu powiadomienia hello powinien być wyświetlany ogólny powiadomienie aplikacji hello toolaunch użytkownika hello monitowania. Aplikacja Hello następnie uwierzytelnia użytkownika hello i zawiera ładunek powiadomienia hello.

W tym samouczku Secure wypychania przedstawiono sposób toosend powiadomienie wypychane bezpieczny sposób. Samouczek Hello opiera się na powitania [Powiadom użytkowników](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczku, dlatego należy wykonać kroki hello w tym samouczku najpierw.

> [!NOTE]
> Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a>Modyfikowanie hello projekt dla systemu iOS
Teraz, aby modyfikować tylko aplikacji hello w toosend zaplecza *identyfikator* powiadomienia, masz toochange Twojego toohandle aplikacji systemu iOS, czy powiadomień i wywołanie zwrotne użytkownika hello tooretrieve zaplecza secure toobe komunikat wyświetlany.

tooachieve tego celu mamy toowrite hello logiki tooretrieve hello bezpieczne zawartości z hello zaplecze aplikacji.

1. W **AppDelegate.m**, upewnij się, że rejestruje powiadomienia dyskretnej aplikacji hello tak przetwarza hello identyfikator powiadomień wysyłanych z hello wewnętrznej bazy danych. Dodaj hello **UIRemoteNotificationTypeNewsstandContentAvailability** opcji w didFinishLaunchingWithOptions:
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. W Twojej **AppDelegate.m** Dodaj sekcji implementacji u góry hello z powitania po deklaracji:
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. Następnie dodaj w hello hello sekcji implementacja po kod, zastępując hello symbolu zastępczego `{back-end endpoint}` z punktem końcowym hello na danym zapleczu uzyskany wcześniej:

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. Teraz możemy mają toohandle hello przychodzące powiadomienia i użyj metody hello powyżej toodisplay zawartości hello tooretrieve. Po pierwsze mamy tooenable Twojego toorun aplikacji systemu iOS w tle hello podczas odbierania powiadomień wypychanych. W **XCode**, wybierz projekt aplikacji hello lewym panelu, a następnie kliknij urządzenie docelowe głównej aplikacji w hello **cele** sekcji w okienku centralnym hello.
2. Następnie kliknij przycisk z **możliwości** u góry hello okienka centralnej i sprawdź hello **zdalnego powiadomienia** wyboru.
   
    ![][IOS1]
3. W **AppDelegate.m** dodać hello następujące powiadomienia wypychane toohandle — metoda:
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    Należy pamiętać, że preferowane toohandle hello przypadków brakujących właściwości nagłówka uwierzytelniania lub odrzucenia przez hello zaplecza. Obsługa określonego Hello powyższych przypadkach zależą od przede wszystkim użytkowników docelowych. Jedną z opcji jest toodisplay powiadomienie z wierszem ogólnego hello użytkownika tooauthenticate tooretrieve hello rzeczywiste powiadomienia o.

## <a name="run-hello-application"></a>Uruchom hello aplikacji
toorun hello aplikacji, hello następujące:

1. W programie XCode uruchamianie aplikacji hello na urządzenie fizyczne z systemem iOS (push, które nie będą działać powiadomienia w symulatorze hello).
2. W aplikacji dla systemu iOS hello interfejsu użytkownika wprowadź nazwę użytkownika i hasło. Mogą to być dowolny ciąg, ale muszą one być hello tę samą wartość.
3. W aplikacji dla systemu iOS hello interfejsu użytkownika, kliknij przycisk **Zaloguj**. Następnie kliknij przycisk **wysyłania wypychania**. Powinny pojawić się powiadomienie bezpiecznego hello będzie wyświetlany w Centrum powiadomień.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
