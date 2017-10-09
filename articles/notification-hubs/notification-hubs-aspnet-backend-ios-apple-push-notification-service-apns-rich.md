---
title: "aaaAzure Push sformatowanego centra powiadomień"
description: "Dowiedz się, jak sformatowanego toosend wypychanych aplikacji dla systemu iOS tooan powiadomienia z platformy Azure. Przykłady kodu napisane w języku Objective C i C#."
documentationcenter: ios
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: 590304df-c0a4-46c5-8ef5-6a6486bb3340
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5432d8bf47777371bea3521a0c0176ade75fbd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-rich-push"></a>Wypychania sformatowanego centra powiadomień Azure
## <a name="overview"></a>Omówienie
W kolejności tooengage użytkownikom błyskawiczne sformatowanego zawartość aplikacja może być toopush poza zwykły tekst. Te powiadomienia wspierania interakcji użytkowników i obecny zawartości, takie jak adresy URL, dźwięki, obrazy/bony i. W tym samouczku opiera się na powitania [Powiadom użytkowników](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tematu i pokazuje, jak toosend wypychanie powiadomień, zawierające ładunków (na przykład obraz).

W tym samouczku jest zgodny z systemem iOS 7 i 8.

  ![][IOS1]

Na wysokim poziomie:

1. zaplecze aplikacji Hello:
   * Magazyny hello ładunku sformatowanego (w tym przypadku obrazu) w magazynie bazy danych i lokalnym zaplecza hello
   * Wysyła identyfikator tego urządzenia toohello sformatowanego powiadomień
2. Aplikacja hello urządzenia:
   * Kontakty hello hello ładunku sformatowanym identyfikatorem hello odbierze żądanie wewnętrznej bazy danych
   * Wysyła powiadomienia użytkowników na urządzeniu hello, po zakończeniu pobierania danych i zawiera ładunek hello natychmiast, gdy użytkownik naciśnie polecenie toolearn więcej

## <a name="webapi-project"></a>WebAPI projektu
1. W programie Visual Studio Otwórz hello **AppBackend** projektu, który został utworzony w hello [Powiadom użytkowników](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczka.
2. Uzyskaj obraz chcesz toonotify użytkownikom i umieszcza je **img** folderu w katalogu projektu.
3. Kliknij przycisk **Pokaż wszystkie pliki** w hello Eksploratorze rozwiązań i kliknij prawym przyciskiem myszy hello folder zbyt**załącz do projektu**.
4. Wybrany obraz powitania, zmienić jego Akcja kompilacji w oknie właściwości zbyt**osadzonego zasobu**.
   
    ![][IOS2]
5. W **Notifications.cs**, Dodaj następujące hello instrukcję using:
   
        using System.Reflection;
6. Aktualizacja hello całego **powiadomienia** klasy z hello następującego kodu. Należy się tooreplace symbole zastępcze hello poświadczenia Centrum powiadomień i nazwę pliku obrazu.
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message toodisplay toousers
            public string Message { get; set; }
            // Type of rich payload (developer-defined)
            public string RichType { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }
   
        public class Notifications {
            public static Notifications Instance = new Notifications();
   
            private List<Notification> notifications = new List<Notification>();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                // Placeholders: replace with hello connection string (with full access) for your notification hub and hello hub name from hello Azure Classics Portal
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",  "{hub name}");
            }
   
            public Notification CreateNotification(string message, string richType, string payload) {
                var notification = new Notification() {
                    Id = notifications.Count,
                    Message = message,
                    RichType = richType,
                    Payload = payload,
                    Read = false
                };
   
                notifications.Add(notification);
   
                return notification;
            }
   
            public Stream ReadImage(int id) {
                var assembly = Assembly.GetExecutingAssembly();
                // Placeholder: image file name (for example, logo.png).
                return assembly.GetManifestResourceStream("AppBackend.img.{logo.png}");
            }
        }
   
   > [!NOTE]
   > (opcjonalnie) Odwołuje się zbyt[jak tooembed i dostęp do zasobów przy użyciu programu Visual C#](http://support.microsoft.com/kb/319292) Aby uzyskać więcej informacji na temat tooadd i uzyskiwanie zasobów projektu.
   > 
   > 
7. W **NotificationsController.cs**, Zmień definicję **NotificationsController** z powitania po fragmentów. Wysyła toodevice identyfikator początkowym powiadomieniu sformatowanego dyskretnej i umożliwia pobranie obrazu po stronie klienta:
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) tooclient
        public async Task<HttpResponseMessage> Post() {
            // Replace hello placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification tooapns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. Teraz ponownie wdrożymy ten tooan aplikacji witryny sieci Web Azure w kolejności toomake go ze wszystkich urządzeń. Kliknij prawym przyciskiem myszy na powitania **AppBackend** projekt i wybierz **publikowania**.
9. Wybierz urządzenie docelowe publikowania witryny sieci Web platformy Azure. Zaloguj się przy użyciu konta platformy Azure i wybierz istniejącą lub nową witrynę sieci Web i zanotuj hello **docelowy adres URL** właściwości w hello **połączenia** kartę. Odnoszą się adres URL toothis Twojego *wewnętrznej bazy danych punktu końcowego* dalszej części tego samouczka. Kliknij przycisk **Opublikuj**.

## <a name="modify-hello-ios-project"></a>Modyfikowanie hello projekt dla systemu iOS
Teraz, gdy zmieniono Twojej aplikacji zaplecza toosend tylko hello *identyfikator* powiadomienia, będzie zmienić ten identyfikator użytkownika toohandle aplikacji systemu iOS i pobrać sformatowanego wiadomość hello z poziomu zaplecza.

1. Otwórz projekt dla systemu iOS, a następnie Włącz powiadomienia zdalne przez przechodzi do docelowej aplikacji głównej tooyour w hello **cele** sekcji.
2. Polecenie **możliwości**, Włącz **tryby tła**i sprawdź hello **zdalnego powiadomienia** wyboru.
   
    ![][IOS3]
3. Przejdź za**Main.storyboard**i upewnij się, że masz kontroler widoku (tooas określonej Home kontrolera widoku w tym samouczku) z [powiadamia użytkownika](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczka.
4. Dodaj **kontrolera nawigacji** tooyour scenorysu, a następnie przeciągnij formant toomake kontrolera widoku tooHome go hello **Widok główny** nawigacji. Upewnij się, że hello **jest początkowej kontrolera widoku** w atrybutach inspektora został wybrany do hello tylko kontrolera nawigacji.
5. Dodaj **kontrolera widoku** toostoryboard i Dodaj **widoku obrazu**. Jest to strona hello, które użytkownicy zobaczą, gdy wybiera on toolearn więcej klikając hello notifiication. Twoje scenorysu powinna wyglądać następująco:
   
    ![][IOS4]
6. Polecenie hello **Home kontrolera widoku** scenorysu, i upewnij się, że ma ona **homeViewController** jako jego **klasy niestandardowej** i **scenorysu identyfikator**w obszarze hello inspektora tożsamości.
7. Witaj takie same dla obrazu kontroler widoku jako **imageViewController**.
8. Następnie utwórz nową klasę kontrolera widoku zatytułowany **imageViewController** toohandle hello właśnie utworzony interfejsu użytkownika.
9. W **imageViewController.h**, Dodaj powitania po deklaracji interfejsów toohello kontrolera. Upewnij się, że toocontrol i przeciągnij od Witaj scenorysu obrazu widoku toothese właściwości toolink Witaj dwie:
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. W **imageViewController.m**, Dodaj następujące hello na końcu hello **viewDidload**:
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. W **AppDelegate.m**, kontrolera obraz powitania importu utworzone:
    
        #import "imageViewController.h"
12. Dodaj sekcję interfejsu z powitania po deklaracji:
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. W **AppDelegate**, upewnij się, że aplikacja rejestruje dyskretnej powiadomień w **aplikacji: didFinishLaunchingWithOptions**:
    
        // Software version
        self.iOS8 = [[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)] && [[UIApplication sharedApplication] respondsToSelector:@selector(registerForRemoteNotifications)];
    
        // Register for remote notifications for iOS8 and previous versions
        if (self.iOS8) {
            NSLog(@"This device is running with iOS8.");
    
            // Action
            UIMutableUserNotificationAction *richPushAction = [[UIMutableUserNotificationAction alloc] init];
            richPushAction.identifier = @"richPushMore";
            richPushAction.activationMode = UIUserNotificationActivationModeForeground;
            richPushAction.authenticationRequired = NO;
            richPushAction.title = @"More";
    
            // Notification category
            UIMutableUserNotificationCategory* richPushCategory = [[UIMutableUserNotificationCategory alloc] init];
            richPushCategory.identifier = @"richPush";
            [richPushCategory setActions:@[richPushAction] forContext:UIUserNotificationActionContextDefault];
    
            // Notification categories
            NSSet* richPushCategories = [NSSet setWithObjects:richPushCategory, nil];

            UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                    UIUserNotificationTypeAlert |
                                                    UIUserNotificationTypeBadge
                                                                                     categories:richPushCategories];

            [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
            [[UIApplication sharedApplication] registerForRemoteNotifications];

        }
        else {
            // Previous iOS versions
            NSLog(@"This device is running with iOS7 or earlier versions.");

            [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
        }

        return YES;

1. Subsitute w powitania po implementacji **aplikacji: didRegisterForRemoteNotificationsWithDeviceToken** tootake hello scenorysu zmiany interfejsu użytkownika do konta:
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. Następnie należy dodać następujące metody zbyt hello**AppDelegate.m** tooretrieve hello obrazu z punktu końcowego i wysyłania powiadomień lokalnego, po ukończeniu pobierania. Upewnij się, że symbol zastępczy hello toosubstitute `{backend endpoint}` z wewnętrznej bazy danych punktu końcowego:
   
       NSString *const GetNotificationEndpoint = @"{backend endpoint}/api/notifications";
   
       // Helper: retrieve notification content from backend with rich notification id
       - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion {
           UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
           homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
           NSString* authenticationHeader = hvc.registerClient.authenticationHeader;
           // Check if authenticated
           if (!authenticationHeader) return;
   
           NSURLSession* session = [NSURLSession
                                    sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                    delegate:nil
                                    delegateQueue:nil];
   
           NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, richId]];
           NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
           [request setHTTPMethod:@"GET"];
           NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
           [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
   
           NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
   
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
               if (!error && httpResponse.statusCode == 200) {
                   // From NSData tooUIImage
                   self.imagePayload = [UIImage imageWithData:data];
   
                   completion(nil);
               }
               else {
                   NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                   if (error)
                       completion(error);
                   else {
                       completion([NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                   }
               }
           }];
           [dataTask resume];
       }
   
       // Handle silent push notifications when id is sent from backend
       - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler {
           self.userInfo = userInfo;
           int richId = [[self.userInfo objectForKey:@"richId"] intValue];
           NSString* richType = [self.userInfo objectForKey:@"richType"];
   
           // Retrieve image data
           if ([richType isEqualToString:@"img"]) {  
               [self retrieveRichImageWithId:richId completion:^(NSError* error) {
                   if (!error){
                       // Send local notification
                       UILocalNotification* localNotification = [[UILocalNotification alloc] init];
   
                       // "5" is arbitrary here toogive you enough time tooquit out of hello app and receive push notifications
                       localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:5];
                       localNotification.userInfo = self.userInfo;
                       localNotification.alertBody = [self.userInfo objectForKey:@"richMessage"];
                       localNotification.timeZone = [NSTimeZone defaultTimeZone];
   
                       // iOS8 categories
                       if (self.iOS8) {
                           localNotification.category = @"richPush";
                       }
   
                       [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                       handler(UIBackgroundFetchResultNewData);
                   }
                   else{
                       handler(UIBackgroundFetchResultFailed);
                   }
               }];
           }
           // Add "else if" here toohandle more types of rich content such as url, sound files, etc.
       }
3. Obsługi powiadamiania lokalne powitania powyżej otwierając kontrolera widoku obraz powitania w **AppDelegate.m** z hello następujące metody:
   
       // Helper: redirect users tooimage view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image tooimage view controller
           imgViewController.imagePayload = img;
   
           // Redirect
           [navigationController pushViewController:imgViewController animated:YES];
       }
   
       // Handle local notification sent above in didReceiveRemoteNotification
       - (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
           if (application.applicationState == UIApplicationStateActive) {
               // Show in-app alert with an extra "more" button
               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:notification.alertBody delegate:self cancelButtonTitle:@"OK" otherButtonTitles:@"More", nil];
   
               [alert show];
           }
           // App becomes active from user's tap on notification
           else {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
       }
   
       // Handle buttons in in-app alerts and redirect with data/image
       - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
           // Handle "more" button
           if (buttonIndex == 1)
           {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           // Add "else if" here toohandle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-hello-application"></a>Uruchom hello aplikacji
1. W programie XCode uruchamianie aplikacji hello na urządzenie fizyczne z systemem iOS (push, które nie będą działać powiadomienia w symulatorze hello).
2. W aplikacji dla systemu iOS hello interfejsu użytkownika, wprowadź nazwę użytkownika i hasło hello takie same wartości dla uwierzytelniania i kliknij przycisk **dziennika w**.
3. Kliknij przycisk **wysyłania wypychania** i powinien zostać wyświetlony alert w aplikacji. Po kliknięciu **więcej**, można wprowadzić toohello obrazu wybrano tooinclude w zapleczu swojej aplikacji.
4. Możesz również kliknąć **wysyłania wypychania** i natychmiast naciśnij przycisk Strona główna hello urządzenia. Za chwilę otrzymasz powiadomienie wypychane. Wybierz na niej, lub kliknij przycisk więcej, zostanie wyświetlona zawartość sformatowanego obrazu i aplikacji hello tooyour.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
