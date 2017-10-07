---
title: "aaaAzure Notification Hubs Powiadom użytkowników dla systemu iOS z zaplecza programu .NET"
description: "Dowiedz się, jak toosend push toousers powiadomienia na platformie Azure. Przykłady kodu napisane w języku Objective C i hello interfejs API .NET dla hello wewnętrznej bazy danych."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a>Azure Notification Hubs Notify Users for iOS with .NET backend (Powiadamianie użytkowników urządzeń z systemem iOS przy użyciu usługi Azure Notification Hubs z zapleczem programu .NET)
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Omówienie
Obsługa powiadomień wypychanych na platformie Azure umożliwia tooaccess łatwy w użyciu, multiplatform i wypychanych skalowanej infrastruktury, co znacznie upraszcza hello stosowania powiadomienia wypychane zarówno konsumenckie i korporacyjne aplikacji dla urządzeń przenośnych platform. Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień tooa specyficzne dla aplikacji użytkownika na określonym urządzeniu. Zaplecza ASP.NET WebAPI jest używane tooauthenticate klientów i powiadomienia toogenerate przedstawioną w temacie wskazówki hello [rejestrowanie z zaplecza aplikacji](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).

> [!NOTE]
> Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md). W tym samouczku jest również hello wymagań wstępnych toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) samouczka.
> Jeśli chcesz toouse Mobile Apps jako usługi wewnętrznej bazy danych, zobacz hello [Mobile Apps wprowadzenie wypychania](../app-service-mobile/app-service-mobile-ios-get-started-push.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a>Modyfikowanie aplikacji systemu iOS
1. Otwórz hello jednej strony Wyświetl aplikację utworzony w hello [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) samouczka.
   
   > [!NOTE]
   > W tej sekcji przyjęto założenie, projektu skonfigurowano nazwę organizacji puste. Jeśli nie, konieczne będzie tooprepend nazwy klasy tooall nazwę organizacji.
   > 
   > 
2. W Twojej Main.storyboard Dodaj składniki hello pokazano zrzut ekranu hello poniżej hello obiekt bibliotece.
   
    ![][1]
   
   * **Nazwa użytkownika**: UITextField A tekstem zastępczym *wprowadź nazwę użytkownika*, natychmiast poniżej hello wysyłać wyniki etykiety i ograniczonego toohello po lewej i kliknij prawym przyciskiem myszy marginesy i poniżej hello wysyłanie etykiety wyników.
   * **Hasło**: UITextField A tekstem zastępczym *wprowadź hasło*, natychmiast podrzędne hello pole tekstowe nazwy użytkownika i ograniczonego toohello po lewej i prawej marginesy i poniżej pola tekstowego hello nazwy użytkownika. Sprawdź hello **Secure wpisywanie tekstu** hello inspektora atrybutu, opcji w obszarze *zwraca klucz*.
   * **Zaloguj się za**: A UIButton etykietą bezpośrednio poniżej pola tekstowego hasła hello i usuń zaznaczenie pola wyboru hello **włączone** w obszarze opcji hello inspektora atrybuty *zawartości kontrolki*
   * **WNS**: etykiety i wysyłanie tooenable przełącznika hello powiadomień usługi powiadomień systemu Windows została już Instalatora na powitania koncentratora. Zobacz hello [systemu Windows wprowadzenie](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) samouczka.
   * **GCM**: etykiety i wysyłanie tooenable przełącznika hello tooGoogle powiadomień Cloud Messaging została już Instalatora na powitania koncentratora. Zobacz [Android wprowadzenie](notification-hubs-android-push-notification-google-gcm-get-started.md) samouczka.
   * **APNS**: etykiety i wysyłanie tooenable przełącznika hello toohello powiadomienia usługi powiadomień platformy firmy Apple.
   * **Recipent Username**: UITextField A tekstem zastępczym *tag username odbiorcy*, natychmiast poniżej hello GCM etykiety i ograniczonego toohello lewej i prawej marży i poniżej hello GCM etykiety.

    Niektóre składniki zostały dodane w hello [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) samouczka.

1. **CTRL** przeciągnij od składników hello hello widoku tooViewController.h i dodać tych nowych punktów.
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. W ViewController.h, Dodaj następujące hello `#define` poniżej Twojej instrukcje importu. SUBSTITUTE hello *< wprowadź swój punkt końcowy w wewnętrznej bazy danych\>*  symbol zastępczy hello docelowy adres URL używany zapleczu swojej aplikacji toodeploy hello w poprzedniej sekcji. Na przykład *http://you_backend.azurewebsites.net*.
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. W projekcie, Utwórz nową **Cocoa Touch klasy** o nazwie **RegisterClient** toointerface z hello zaplecza ASP.NET został utworzony. Utworzenie dziedziczenia z klasy hello `NSObject`. Następnie można dodać następującego kodu w hello RegisterClient.h hello.
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. Witaj RegisterClient.m aktualizacji hello `@interface` sekcji:
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. Zastąp hello `@implementation` części hello RegisterClient.m z hello następującego kodu.

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    Powyższy kod Hello implementuje logiki hello wyjaśniono w artykule wskazówki hello [rejestrowanie z zaplecza aplikacji](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) przy użyciu NSURLSession tooperform REST wywołuje zaplecza aplikacji tooyour i NSUserDefaults toolocally magazynu hello registrationId zwrócony przez hello Centrum powiadomień.

    Należy pamiętać, że ta klasa wymaga jego właściwość **authorizationHeader** toobe w kolejności toowork poprawnie ustawiony. Ta właściwość jest ustawiana przez hello **ViewController** klasy po hello zalogować.

1. W ViewController.h, Dodaj `#import` instrukcji dla RegisterClient.h. Następnie dodaj deklarację hello tokenu urządzenia i referencyjne tooa `RegisterClient` wystąpienie w hello `@interface` sekcji:
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. W ViewController.m, Dodaj deklarację Metoda prywatna w hello `@interface` sekcji:
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> Hello następujący fragment kodu nie jest schemat bezpiecznego uwierzytelniania, należy zastąpić hello implementacja hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** z mechanizmu uwierzytelniania określonych Spowoduje to wygenerowanie toobe token uwierzytelniania używane przez hello register klasy klienta, np. OAuth, usługi Active Directory.
> 
> 

1. Następnie w hello `@implementation` sekcji ViewController.m dodać hello następującego kodu, który dodaje implementacji hello ustawienie hello urządzenie tokenu i uwierzytelnienia nagłówka.
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    Należy zwrócić uwagę, jak token urządzenia hello ustawienie umożliwia hello przycisk Zaloguj. Jest to spowodowane jako część hello logowania akcji kontrolera widoku hello rejestruje dla powiadomień wypychanych przy użyciu zaplecza aplikacji hello. W związku z tym nie chcemy dziennika w toobe akcji dostępny dopóki hello token urządzenia został poprawnie skonfigurowany. Hello logowania z rejestracji wypychanych hello jest oddzielana, jak długo była hello nastąpi przed ostatnim hello.
2. W ViewController.m, użyj hello następujące metody akcji hello tooimplement wstawki dla Twojego **dziennika w** przycisk i metody toosend hello powiadomień wiadomości przy użyciu zaplecza ASP.NET hello.
   
       - (IBAction) LogInAction: nadawcy (id) {/ / Utwórz nagłówek uwierzytelnienia i ustaw go w rejestrze klienta NSString * nazwa użytkownika = samodzielnie. UsernameField.text;   Hasło NSString * = samodzielnie. PasswordField.text;
   
           [self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];
   
           __weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tagi: nil andCompletion:^(NSError* error) {Jeśli (! błędu) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [samoobsługowego MessageBox:@"Success" message:@"Registered pomyślnie!"];});}}];}

        -SendNotificationASPNETBackend (void): (NSString*) systemu powiadomień platformy UsernameTag: (NSString*) usernameTag komunikat: (NSString*) komunikat {NSURLSession* sesji = [NSURLSession sessionWithConfiguration: delegateQueue:nil delegata: nil [NSURLSessionConfiguration defaultSessionConfiguration]];

            Przekaż hello tag systemu powiadomień platformy i nazwa użytkownika jako parametrów z hello adresu URL usługi REST toohello ASP.NET zaplecza nsurl OCZEKIWANEGO * Adres_url_żądania = [URLWithString nsurl OCZEKIWANEGO: [NSString stringWithFormat:@"%@/api/notifications? systemu powiadomień platformy = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];

            Żądanie NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [setHTTPMethod:@"POST"żądania];

            Uzyskanie authenticationheader zasymulować hello powitania klienta rejestru authorizationHeaderValue NSString * = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"żądania];

            Dodaj treść wiadomości powiadomienia hello [żądania setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [żądanie setHTTPBody: [komunikatów dataUsingEncoding:NSUTF8StringEncoding]];

            Wykonanie hello wysyłania powiadomień interfejsu API REST na powitania ASP.NET zaplecza NSURLSessionDataTask * dataTask = [sesji dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *Błąd) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) odpowiedź;        Jeśli (błąd || httpResponse.statusCode! = 200) {NSString* stan = [NSString stringWithFormat:@"Error stanu % @: % d\nError: %@\n", pns, httpResponse.statusCode, błąd];            dispatch_async(dispatch_get_main_queue(), ^ {/ / Append tekstu, ponieważ wszystkie wywołania systemu powiadomień platformy 3 może być również tooview informacji [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            }];    [dataTask Wznów]; }


1. Aktualizowanie akcji hello hello **Wyślij powiadomienie E-mail** przycisk zaplecza ASP.NET hello toouse i wysłać tooany systemu powiadomień platformy włączane przez przełącznik.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. W funkcji **ViewDidLoad**, Dodaj następujące wystąpienia RegisterClient hello tooinstantiate hello i ustaw hello delegowanego dla pól tekstowych.
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. Teraz w **AppDelegate.m**, Usuń całą zawartość hello metody hello **aplikacji: didRegisterForPushNotificationWithDeviceToken:** i zastąp go hello się, że po toomake, który hello widoku Kontroler zawiera hello najnowsze token urządzenia pobierane z usługi APNs:
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. Na koniec w **AppDelegate.m**, upewnij się, że masz hello następujące metody:
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a>Test hello aplikacji
1. W programie XCode uruchamianie aplikacji hello na urządzenie fizyczne z systemem iOS (push, które nie będą działać powiadomienia w symulatorze hello).
2. W aplikacji dla systemu iOS hello interfejsu użytkownika wprowadź nazwę użytkownika i hasło. Mogą to być dowolny ciąg, ale oba muszą być hello takie same wartości ciągu. Następnie kliknij przycisk **dziennika w**.
   
    ![][2]
3. Powinny zostać wyświetlone okno podręczne informujące o Powodzenie rejestracji. Kliknij przycisk **OK**.
   
    ![][3]
4. W hello **tag username odbiorcy* tekst Wprowadź tag nazwy użytkownika hello używany z rejestracją hello z innego urządzenia.
5. Wprowadź komunikat powiadomienia, a następnie kliknij przycisk **Wyślij powiadomienie E-mail**.  Hello tylko te urządzenia, które ma rejestracji hello odbiorcy użytkownika nazwa znacznika odbierać wiadomości powitania powiadomień.  Jest wysyłane tylko toothose użytkowników.
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
