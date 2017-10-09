---
title: "aaaRegister hello bieżącego użytkownika dla powiadomień wypychanych przy użyciu interfejsu API sieci Web | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toorequest rejestracja powiadomień wypychanych w aplikacji systemu iOS za pomocą usługi Azure Notification Hubs rejestracja jest wykonywane przez interfejs API sieci Web platformy ASP.NET."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f859feb436093e703d7e1db38354dd356fff8efe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a>Zarejestruj hello bieżącego użytkownika dla powiadomień wypychanych przy użyciu platformy ASP.NET
> [!div class="op_single_selector"]
> * [iOS](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a>Omówienie
W tym temacie pokazano, jak toorequest rejestracja powiadomień wypychanych przy użyciu usługi Azure Notification Hubs rejestracji jest wykonywane przez interfejs API sieci Web platformy ASP.NET. W tym temacie rozszerza samouczek hello [powiadomić użytkowników z usługą Notification Hubs]. Została już ukończona hello wymagane kroki tego samouczka toocreate usługi mobilnej hello uwierzytelniony. Aby uzyskać więcej informacji na temat hello powiadomić użytkowników scenariusza, zobacz [powiadomić użytkowników z usługą Notification Hubs].

## <a name="update-your-app"></a>Aktualizowanie aplikacji
1. W Twojej MainStoryboard_iPhone.storyboard Dodaj hello poniższych składników z biblioteki obiektów hello:
   
   * **Etykieta**: "TooUser z koncentratorami powiadomień wypychanych"
   * **Etykieta**: "Identyfikator InstallationId"
   * **Etykieta**: "Użytkownika"
   * **Pole tekstowe**: "Użytkownika"
   * **Etykieta**: "Password"
   * **Pole tekstowe**: "Password"
   * **Przycisk**: "Logowanie"
     
     W tym momencie z scenorysu wygląda hello:
     
      ![][0]
2. W edytorze Asystenta hello, utworzyć gniazda dla wszystkich kontrolek hello przełączono połączeń telefonicznych z nimi, uzyskuj pól tekstowych hello hello kontrolera widoku (delegat) i utworzyć **akcji** dla hello **logowania** przycisku.
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. Utwórz klasę o nazwie **DeviceInfo**, i kopiowania hello po kodu do sekcji interfejsu hello hello pliku DeviceInfo.h:
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. Skopiuj hello następującego kodu w sekcji implementacji hello hello DeviceInfo.m pliku:
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store hello install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. W PushToUserAppDelegate.h Dodaj następujące właściwości singleton hello:
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. W hello **didFinishLaunchingWithOptions** metody w PushToUserAppDelegate.m, Dodaj hello następującego kodu:
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    pierwszy wiersz Hello inicjuje hello **DeviceInfo** singleton. Witaj drugiego wiersza uruchamia hello rejestracji dla powiadomień wypychanych, który znajduje się już jest zostały już wykonane hello [Rozpoczynanie pracy z usługą Notification Hubs] samouczka.
7. W PushToUserAppDelegate.m, zaimplementuj metodę hello **didRegisterForRemoteNotificationsWithDeviceToken** w Twojej AppDelegate i Dodaj hello następującego kodu:
   
        self.deviceInfo.deviceToken = deviceToken;
   
    To ustawienie token urządzenia hello hello żądania.
   
   > [!NOTE]
   > W tym momencie nie powinien zawierać dowolny kod w ramach tej metody. Jeśli masz już toohello wywołanie **registerNativeWithDeviceToken** metodę, która została dodana po zakończeniu hello [Rozpoczynanie pracy z usługą Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) samouczka musisz komentarz lub które zostaną usunięte wywołanie.
   > 
   > 
8. W pliku PushToUserAppDelegate.m hello Dodaj następujące metody obsługi hello:
   
   * informacje o użytkowniku aplikacji (void):(UIApplication *) aplikacji didReceiveRemoteNotification:(NSDictionary *) {NSLog (@"% @", informacje o użytkowniku);   UIAlertView * alert = [[UIAlertView alokacji] initWithTitle:@"Notification" komunikat: cancelButtonTitle delegata: nil [informacje o użytkowniku objectForKey:@"inAppMessage"]: @ otherButtonTitles:nil "OK", nil];   [Pokaż alert] }
   
   Ta metoda wyświetla alert w hello interfejsu użytkownika, gdy aplikacji otrzymuje powiadomienia, gdy jest on uruchomiony.
9. Otwórz plik PushToUserViewController.m hello i klawiatury hello zwracany powitania po implementacji:
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. W hello **viewDidLoad** metody w pliku PushToUserViewController.m hello zainicjować hello installationId etykietę w następujący sposób:
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. Dodaj następujące właściwości w interfejsie w PushToUserViewController.m hello:
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. Następnie należy dodać powitania po implementacji:
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. Kopiuj hello poniższy kod do hello **logowania** metoda obsługi utworzone przez XCode:
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    Ta metoda pobiera zarówno identyfikator instalacji, jak i kanału dla powiadomień wypychanych i wysyła je, wraz z typem urządzenia hello, toohello uwierzytelniony metody interfejsu API sieci Web, która tworzy rejestracji w usłudze Notification Hubs. Ten interfejs API sieci Web został zdefiniowany w [powiadomić użytkowników z usługą Notification Hubs].

Teraz, gdy hello klienta aplikacja została zaktualizowana, zwróć toohello [powiadomić użytkowników z usługą Notification Hubs] i zaktualizować hello usługi mobilnej toosend powiadomienia przy użyciu usługi Notification Hubs.

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[powiadomić użytkowników z usługą Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet

[Rozpoczynanie pracy z usługą Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-ios
