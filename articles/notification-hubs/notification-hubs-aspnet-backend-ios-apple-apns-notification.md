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
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="24326-104">Azure Notification Hubs Notify Users for iOS with .NET backend (Powiadamianie użytkowników urządzeń z systemem iOS przy użyciu usługi Azure Notification Hubs z zapleczem programu .NET)</span><span class="sxs-lookup"><span data-stu-id="24326-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="24326-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="24326-105">Overview</span></span>
<span data-ttu-id="24326-106">Obsługa powiadomień wypychanych na platformie Azure umożliwia tooaccess łatwy w użyciu, multiplatform i wypychanych skalowanej infrastruktury, co znacznie upraszcza hello stosowania powiadomienia wypychane zarówno konsumenckie i korporacyjne aplikacji dla urządzeń przenośnych platform.</span><span class="sxs-lookup"><span data-stu-id="24326-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="24326-107">Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień tooa specyficzne dla aplikacji użytkownika na określonym urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="24326-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="24326-108">Zaplecza ASP.NET WebAPI jest używane tooauthenticate klientów i powiadomienia toogenerate przedstawioną w temacie wskazówki hello [rejestrowanie z zaplecza aplikacji](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="24326-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="24326-109">Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="24326-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="24326-110">W tym samouczku jest również hello wymagań wstępnych toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="24326-110">This tutorial is also hello prerequisite toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="24326-111">Jeśli chcesz toouse Mobile Apps jako usługi wewnętrznej bazy danych, zobacz hello [Mobile Apps wprowadzenie wypychania](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="24326-111">If you want toouse Mobile Apps as your backend service, see hello [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="24326-112">Modyfikowanie aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="24326-112">Modify your iOS app</span></span>
1. <span data-ttu-id="24326-113">Otwórz hello jednej strony Wyświetl aplikację utworzony w hello [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="24326-113">Open hello Single Page view app you created in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="24326-114">W tej sekcji przyjęto założenie, projektu skonfigurowano nazwę organizacji puste.</span><span class="sxs-lookup"><span data-stu-id="24326-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="24326-115">Jeśli nie, konieczne będzie tooprepend nazwy klasy tooall nazwę organizacji.</span><span class="sxs-lookup"><span data-stu-id="24326-115">If not, you will need tooprepend your organization name tooall class names.</span></span>
   > 
   > 
2. <span data-ttu-id="24326-116">W Twojej Main.storyboard Dodaj składniki hello pokazano zrzut ekranu hello poniżej hello obiekt bibliotece.</span><span class="sxs-lookup"><span data-stu-id="24326-116">In your Main.storyboard add hello components shown in hello screenshot below from hello object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="24326-117">**Nazwa użytkownika**: UITextField A tekstem zastępczym *wprowadź nazwę użytkownika*, natychmiast poniżej hello wysyłać wyniki etykiety i ograniczonego toohello po lewej i kliknij prawym przyciskiem myszy marginesy i poniżej hello wysyłanie etykiety wyników.</span><span class="sxs-lookup"><span data-stu-id="24326-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath hello send results label and constrained toohello left and right margins and beneath hello send results label.</span></span>
   * <span data-ttu-id="24326-118">**Hasło**: UITextField A tekstem zastępczym *wprowadź hasło*, natychmiast podrzędne hello pole tekstowe nazwy użytkownika i ograniczonego toohello po lewej i prawej marginesy i poniżej pola tekstowego hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24326-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath hello username text field and constrained toohello left and right margins and beneath hello username text field.</span></span> <span data-ttu-id="24326-119">Sprawdź hello **Secure wpisywanie tekstu** hello inspektora atrybutu, opcji w obszarze *zwraca klucz*.</span><span class="sxs-lookup"><span data-stu-id="24326-119">Check hello **Secure Text Entry** option in hello Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="24326-120">**Zaloguj się za**: A UIButton etykietą bezpośrednio poniżej pola tekstowego hasła hello i usuń zaznaczenie pola wyboru hello **włączone** w obszarze opcji hello inspektora atrybuty *zawartości kontrolki*</span><span class="sxs-lookup"><span data-stu-id="24326-120">**Log in**: A UIButton labeled immediately beneath hello password text field and uncheck hello **Enabled** option in hello Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="24326-121">**WNS**: etykiety i wysyłanie tooenable przełącznika hello powiadomień usługi powiadomień systemu Windows została już Instalatora na powitania koncentratora.</span><span class="sxs-lookup"><span data-stu-id="24326-121">**WNS**: Label and switch tooenable sending hello notification Windows Notification Service if it has been setup on hello hub.</span></span> <span data-ttu-id="24326-122">Zobacz hello [systemu Windows wprowadzenie](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="24326-122">See hello [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="24326-123">**GCM**: etykiety i wysyłanie tooenable przełącznika hello tooGoogle powiadomień Cloud Messaging została już Instalatora na powitania koncentratora.</span><span class="sxs-lookup"><span data-stu-id="24326-123">**GCM**: Label and switch tooenable sending hello notification tooGoogle Cloud Messaging if it has been setup on hello hub.</span></span> <span data-ttu-id="24326-124">Zobacz [Android wprowadzenie](notification-hubs-android-push-notification-google-gcm-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="24326-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="24326-125">**APNS**: etykiety i wysyłanie tooenable przełącznika hello toohello powiadomienia usługi powiadomień platformy firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="24326-125">**APNS**: Label and switch tooenable sending hello notification toohello Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="24326-126">**Recipent Username**: UITextField A tekstem zastępczym *tag username odbiorcy*, natychmiast poniżej hello GCM etykiety i ograniczonego toohello lewej i prawej marży i poniżej hello GCM etykiety.</span><span class="sxs-lookup"><span data-stu-id="24326-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath hello GCM label and constrained toohello left and right margins and beneath hello GCM label.</span></span>

    <span data-ttu-id="24326-127">Niektóre składniki zostały dodane w hello [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="24326-127">Some components were added in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="24326-128">**CTRL** przeciągnij od składników hello hello widoku tooViewController.h i dodać tych nowych punktów.</span><span class="sxs-lookup"><span data-stu-id="24326-128">**Ctrl** drag from hello components in hello view tooViewController.h and add these new outlets.</span></span>
   
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
2. <span data-ttu-id="24326-129">W ViewController.h, Dodaj następujące hello `#define` poniżej Twojej instrukcje importu.</span><span class="sxs-lookup"><span data-stu-id="24326-129">In ViewController.h, add hello following `#define` just below your import statements.</span></span> <span data-ttu-id="24326-130">SUBSTITUTE hello *< wprowadź swój punkt końcowy w wewnętrznej bazy danych\>*  symbol zastępczy hello docelowy adres URL używany zapleczu swojej aplikacji toodeploy hello w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="24326-130">Substitute hello *<Enter Your Backend Endpoint\>* placeholder with hello Destination URL you used toodeploy your app backend in hello previous section.</span></span> <span data-ttu-id="24326-131">Na przykład *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="24326-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="24326-132">W projekcie, Utwórz nową **Cocoa Touch klasy** o nazwie **RegisterClient** toointerface z hello zaplecza ASP.NET został utworzony.</span><span class="sxs-lookup"><span data-stu-id="24326-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** toointerface with hello ASP.NET back-end you created.</span></span> <span data-ttu-id="24326-133">Utworzenie dziedziczenia z klasy hello `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="24326-133">Create hello class inheriting from `NSObject`.</span></span> <span data-ttu-id="24326-134">Następnie można dodać następującego kodu w hello RegisterClient.h hello.</span><span class="sxs-lookup"><span data-stu-id="24326-134">Then add hello following code in hello RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="24326-135">Witaj RegisterClient.m aktualizacji hello `@interface` sekcji:</span><span class="sxs-lookup"><span data-stu-id="24326-135">In hello RegisterClient.m update hello `@interface` section:</span></span>
   
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
5. <span data-ttu-id="24326-136">Zastąp hello `@implementation` części hello RegisterClient.m z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="24326-136">Replace hello `@implementation` section in hello RegisterClient.m with hello following code.</span></span>

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

    <span data-ttu-id="24326-137">Powyższy kod Hello implementuje logiki hello wyjaśniono w artykule wskazówki hello [rejestrowanie z zaplecza aplikacji](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) przy użyciu NSURLSession tooperform REST wywołuje zaplecza aplikacji tooyour i NSUserDefaults toolocally magazynu hello registrationId zwrócony przez hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="24326-137">hello code above implements hello logic explained in hello guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession tooperform REST calls tooyour app backend, and NSUserDefaults toolocally store hello registrationId returned by hello notification hub.</span></span>

    <span data-ttu-id="24326-138">Należy pamiętać, że ta klasa wymaga jego właściwość **authorizationHeader** toobe w kolejności toowork poprawnie ustawiony.</span><span class="sxs-lookup"><span data-stu-id="24326-138">Note that this class requires its property **authorizationHeader** toobe set in order toowork properly.</span></span> <span data-ttu-id="24326-139">Ta właściwość jest ustawiana przez hello **ViewController** klasy po hello zalogować.</span><span class="sxs-lookup"><span data-stu-id="24326-139">This property is set by hello **ViewController** class after hello log in.</span></span>

1. <span data-ttu-id="24326-140">W ViewController.h, Dodaj `#import` instrukcji dla RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="24326-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="24326-141">Następnie dodaj deklarację hello tokenu urządzenia i referencyjne tooa `RegisterClient` wystąpienie w hello `@interface` sekcji:</span><span class="sxs-lookup"><span data-stu-id="24326-141">Then add a declaration for hello device token and reference tooa `RegisterClient` instance in hello `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="24326-142">W ViewController.m, Dodaj deklarację Metoda prywatna w hello `@interface` sekcji:</span><span class="sxs-lookup"><span data-stu-id="24326-142">In ViewController.m, add a private method declaration in hello `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="24326-143">Hello następujący fragment kodu nie jest schemat bezpiecznego uwierzytelniania, należy zastąpić hello implementacja hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** z mechanizmu uwierzytelniania określonych Spowoduje to wygenerowanie toobe token uwierzytelniania używane przez hello register klasy klienta, np. OAuth, usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="24326-143">hello following snippet is not a secure authentication scheme, you should substitute hello implementation of hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token toobe consumed by hello register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="24326-144">Następnie w hello `@implementation` sekcji ViewController.m dodać hello następującego kodu, który dodaje implementacji hello ustawienie hello urządzenie tokenu i uwierzytelnienia nagłówka.</span><span class="sxs-lookup"><span data-stu-id="24326-144">Then in hello `@implementation` section of ViewController.m add hello following code which adds hello implementation for setting hello device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="24326-145">Należy zwrócić uwagę, jak token urządzenia hello ustawienie umożliwia hello przycisk Zaloguj.</span><span class="sxs-lookup"><span data-stu-id="24326-145">Note how setting hello device token enables hello log in button.</span></span> <span data-ttu-id="24326-146">Jest to spowodowane jako część hello logowania akcji kontrolera widoku hello rejestruje dla powiadomień wypychanych przy użyciu zaplecza aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="24326-146">This is becasue as a part of hello login action, hello view controller registers for push notifications with hello app backend.</span></span> <span data-ttu-id="24326-147">W związku z tym nie chcemy dziennika w toobe akcji dostępny dopóki hello token urządzenia został poprawnie skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="24326-147">Hence, we do not want Log In action toobe accessible till hello device token has been properly set up.</span></span> <span data-ttu-id="24326-148">Hello logowania z rejestracji wypychanych hello jest oddzielana, jak długo była hello nastąpi przed ostatnim hello.</span><span class="sxs-lookup"><span data-stu-id="24326-148">You can decouple hello log in from hello push registration as long as hello former happens before hello latter.</span></span>
2. <span data-ttu-id="24326-149">W ViewController.m, użyj hello następujące metody akcji hello tooimplement wstawki dla Twojego **dziennika w** przycisk i metody toosend hello powiadomień wiadomości przy użyciu zaplecza ASP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="24326-149">In ViewController.m, use hello following snippets tooimplement hello action method for your **Log In** button and a method toosend hello notification message using hello ASP.NET backend.</span></span>
   
       - <span data-ttu-id="24326-150">(IBAction) LogInAction: nadawcy (id) {/ / Utwórz nagłówek uwierzytelnienia i ustaw go w rejestrze klienta NSString * nazwa użytkownika = samodzielnie. UsernameField.text;   Hasło NSString * = samodzielnie. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="24326-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="24326-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="24326-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="24326-152">__weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tagi: nil andCompletion:^(NSError* error) {Jeśli (! błędu) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [samoobsługowego MessageBox:@"Success" message:@"Registered pomyślnie!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="24326-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="24326-153">-SendNotificationASPNETBackend (void): (NSString*) systemu powiadomień platformy UsernameTag: (NSString*) usernameTag komunikat: (NSString*) komunikat {NSURLSession* sesji = [NSURLSession sessionWithConfiguration: delegateQueue:nil delegata: nil [NSURLSessionConfiguration defaultSessionConfiguration]];</span><span class="sxs-lookup"><span data-stu-id="24326-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="24326-154">Przekaż hello tag systemu powiadomień platformy i nazwa użytkownika jako parametrów z hello adresu URL usługi REST toohello ASP.NET zaplecza nsurl OCZEKIWANEGO * Adres_url_żądania = [URLWithString nsurl OCZEKIWANEGO: [NSString stringWithFormat:@"%@/api/notifications? systemu powiadomień platformy = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="24326-154">// Pass hello pns and username tag as parameters with hello REST URL toohello ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="24326-155">Żądanie NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [setHTTPMethod:@"POST"żądania];</span><span class="sxs-lookup"><span data-stu-id="24326-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="24326-156">Uzyskanie authenticationheader zasymulować hello powitania klienta rejestru authorizationHeaderValue NSString * = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"żądania];</span><span class="sxs-lookup"><span data-stu-id="24326-156">// Get hello mock authenticationheader from hello register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="24326-157">Dodaj treść wiadomości powiadomienia hello [żądania setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [żądanie setHTTPBody: [komunikatów dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="24326-157">//Add hello notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="24326-158">Wykonanie hello wysyłania powiadomień interfejsu API REST na powitania ASP.NET zaplecza NSURLSessionDataTask * dataTask = [sesji dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *Błąd) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) odpowiedź;        Jeśli (błąd || httpResponse.statusCode! = 200) {NSString* stan = [NSString stringWithFormat:@"Error stanu % @: % d\nError: %@\n", pns, httpResponse.statusCode, błąd];            dispatch_async(dispatch_get_main_queue(), ^ {/ / Append tekstu, ponieważ wszystkie wywołania systemu powiadomień platformy 3 może być również tooview informacji [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="24326-158">// Execute hello send notification REST API on hello ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information tooview                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="24326-159">}];    [dataTask Wznów]; }</span><span class="sxs-lookup"><span data-stu-id="24326-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="24326-160">Aktualizowanie akcji hello hello **Wyślij powiadomienie E-mail** przycisk zaplecza ASP.NET hello toouse i wysłać tooany systemu powiadomień platformy włączane przez przełącznik.</span><span class="sxs-lookup"><span data-stu-id="24326-160">Update hello action for hello **Send Notification** button toouse hello ASP.NET backend and send tooany PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="24326-161">W funkcji **ViewDidLoad**, Dodaj następujące wystąpienia RegisterClient hello tooinstantiate hello i ustaw hello delegowanego dla pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="24326-161">In function **ViewDidLoad**, add hello following tooinstantiate hello RegisterClient instance and set hello delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="24326-162">Teraz w **AppDelegate.m**, Usuń całą zawartość hello metody hello **aplikacji: didRegisterForPushNotificationWithDeviceToken:** i zastąp go hello się, że po toomake, który hello widoku Kontroler zawiera hello najnowsze token urządzenia pobierane z usługi APNs:</span><span class="sxs-lookup"><span data-stu-id="24326-162">Now in **AppDelegate.m**, remove all hello content of hello method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with hello following toomake sure that hello view controller contains hello latest device token retrieved from APNs:</span></span>
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="24326-163">Na koniec w **AppDelegate.m**, upewnij się, że masz hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="24326-163">Finally in **AppDelegate.m**, make sure you have hello following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a><span data-ttu-id="24326-164">Test hello aplikacji</span><span class="sxs-lookup"><span data-stu-id="24326-164">Test hello Application</span></span>
1. <span data-ttu-id="24326-165">W programie XCode uruchamianie aplikacji hello na urządzenie fizyczne z systemem iOS (push, które nie będą działać powiadomienia w symulatorze hello).</span><span class="sxs-lookup"><span data-stu-id="24326-165">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="24326-166">W aplikacji dla systemu iOS hello interfejsu użytkownika wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="24326-166">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="24326-167">Mogą to być dowolny ciąg, ale oba muszą być hello takie same wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="24326-167">These can be any string, but they must both be hello same string value.</span></span> <span data-ttu-id="24326-168">Następnie kliknij przycisk **dziennika w**.</span><span class="sxs-lookup"><span data-stu-id="24326-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="24326-169">Powinny zostać wyświetlone okno podręczne informujące o Powodzenie rejestracji.</span><span class="sxs-lookup"><span data-stu-id="24326-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="24326-170">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="24326-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="24326-171">W hello **tag username odbiorcy* tekst Wprowadź tag nazwy użytkownika hello używany z rejestracją hello z innego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="24326-171">In hello **Recipient username tag* text field, enter hello user name tag used with hello registration from another device.</span></span>
5. <span data-ttu-id="24326-172">Wprowadź komunikat powiadomienia, a następnie kliknij przycisk **Wyślij powiadomienie E-mail**.</span><span class="sxs-lookup"><span data-stu-id="24326-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="24326-173">Hello tylko te urządzenia, które ma rejestracji hello odbiorcy użytkownika nazwa znacznika odbierać wiadomości powitania powiadomień.</span><span class="sxs-lookup"><span data-stu-id="24326-173">Only hello devices that have a registration with hello recipient user name tag receive hello notification message.</span></span>  <span data-ttu-id="24326-174">Jest wysyłane tylko toothose użytkowników.</span><span class="sxs-lookup"><span data-stu-id="24326-174">It is only sent toothose users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
