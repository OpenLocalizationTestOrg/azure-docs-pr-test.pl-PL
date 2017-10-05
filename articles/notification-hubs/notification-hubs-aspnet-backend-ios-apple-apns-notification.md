---
title: "Azure Notification Hubs Notify Users for iOS with .NET backend (Powiadamianie użytkowników urządzeń z systemem iOS przy użyciu usługi Azure Notification Hubs z zapleczem programu .NET)"
description: "Dowiedz się, jak wysyłać powiadomienia wypychane do użytkowników na platformie Azure. Przykłady kodu napisane w języku Objective C i interfejsu API programu .NET dla wewnętrznej bazy danych."
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
ms.openlocfilehash: 0fa7a886e1ecb0a90b6aebc1dbf9ef0c6ce1acf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="87904-104">Azure Notification Hubs Notify Users for iOS with .NET backend (Powiadamianie użytkowników urządzeń z systemem iOS przy użyciu usługi Azure Notification Hubs z zapleczem programu .NET)</span><span class="sxs-lookup"><span data-stu-id="87904-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="87904-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="87904-105">Overview</span></span>
<span data-ttu-id="87904-106">Obsługa powiadomień wypychanych na platformie Azure umożliwia dostęp do łatwego w użyciu, multiplatform i wypychanych skalowanej infrastruktury, co znacznie upraszcza implementację powiadomienia wypychane dla aplikacji zarówno konsumenckie i korporacyjne dla platform urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="87904-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="87904-107">W tym samouczku pokazano, jak wysyłać powiadomienia wypychane do użytkownika konkretnej aplikacji na konkretnym urządzeniu za pomocą usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="87904-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="87904-108">Zaplecza ASP.NET WebAPI jest używany do uwierzytelniania klientów i generowania powiadomień, jak pokazano w temacie wskazówki [rejestrowanie z zaplecza aplikacji](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="87904-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="87904-109">Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="87904-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="87904-110">W tym samouczku jest również wymagana do [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="87904-110">This tutorial is also the prerequisite to the [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="87904-111">Jeśli chcesz korzystać z aplikacji mobilnej jako usługi wewnętrznej bazy danych, zobacz [Mobile Apps wprowadzenie wypychania](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="87904-111">If you want to use Mobile Apps as your backend service, see the [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="87904-112">Modyfikowanie aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="87904-112">Modify your iOS app</span></span>
1. <span data-ttu-id="87904-113">Otwórz aplikację widoku pojedynczej strony utworzone w [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="87904-113">Open the Single Page view app you created in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="87904-114">W tej sekcji przyjęto założenie, projektu skonfigurowano nazwę organizacji puste.</span><span class="sxs-lookup"><span data-stu-id="87904-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="87904-115">Jeśli nie, konieczne będzie dołączenie wartości Nazwa organizacji do wszystkich nazw klas.</span><span class="sxs-lookup"><span data-stu-id="87904-115">If not, you will need to prepend your organization name to all class names.</span></span>
   > 
   > 
2. <span data-ttu-id="87904-116">W Twojej Main.storyboard dodać składniki pokazane na zrzucie ekranu poniżej z biblioteki obiektów.</span><span class="sxs-lookup"><span data-stu-id="87904-116">In your Main.storyboard add the components shown in the screenshot below from the object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="87904-117">**Nazwa użytkownika**: UITextField A tekstem zastępczym *wprowadź nazwę użytkownika*, znajdujący się bezpośrednio pod wysyłania wyników etykiety i ograniczony do lewego i prawego marginesu i poniżej etykiety wyniki wysyłania.</span><span class="sxs-lookup"><span data-stu-id="87904-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath the send results label and constrained to the left and right margins and beneath the send results label.</span></span>
   * <span data-ttu-id="87904-118">**Hasło**: UITextField A tekstem zastępczym *wprowadź hasło*, natychmiast poniżej nazwę użytkownika tekst pola i ograniczone do lewego i prawego marginesu oraz poniżej pola tekstowego nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="87904-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath the username text field and constrained to the left and right margins and beneath the username text field.</span></span> <span data-ttu-id="87904-119">Sprawdź **Secure wpisywanie tekstu** w obszarze opcji Inspektora atrybutu *zwraca klucz*.</span><span class="sxs-lookup"><span data-stu-id="87904-119">Check the **Secure Text Entry** option in the Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="87904-120">**Zaloguj się za**: A UIButton etykietą bezpośrednio poniżej pola tekstowego hasła i usuń zaznaczenie pola wyboru **włączone** w obszarze opcji Inspektora atrybuty *zawartości kontrolki*</span><span class="sxs-lookup"><span data-stu-id="87904-120">**Log in**: A UIButton labeled immediately beneath the password text field and uncheck the **Enabled** option in the Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="87904-121">**WNS**: etykiety i przełącznik, aby umożliwić wysyłanie powiadomień usługi powiadomień systemu Windows, jeśli został instalacji w Centrum.</span><span class="sxs-lookup"><span data-stu-id="87904-121">**WNS**: Label and switch to enable sending the notification Windows Notification Service if it has been setup on the hub.</span></span> <span data-ttu-id="87904-122">Zobacz [systemu Windows wprowadzenie](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="87904-122">See the [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="87904-123">**GCM**: etykiety i przełącznika, aby włączyć wysyłanie powiadomienia do usługi Google Cloud Messaging została już Instalator koncentratora.</span><span class="sxs-lookup"><span data-stu-id="87904-123">**GCM**: Label and switch to enable sending the notification to Google Cloud Messaging if it has been setup on the hub.</span></span> <span data-ttu-id="87904-124">Zobacz [Android wprowadzenie](notification-hubs-android-push-notification-google-gcm-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="87904-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="87904-125">**APNS**: etykiety i przełącznik, aby włączyć wysyłanie powiadomienia do usługi powiadomień platformy firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="87904-125">**APNS**: Label and switch to enable sending the notification to the Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="87904-126">**Recipent Username**: UITextField A tekstem zastępczym *tag username odbiorcy*, natychmiast poniżej GCM etykiety i ograniczony do lewego i prawego marginesu oraz poniżej etykiety usługi GCM.</span><span class="sxs-lookup"><span data-stu-id="87904-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath the GCM label and constrained to the left and right margins and beneath the GCM label.</span></span>

    <span data-ttu-id="87904-127">Niektóre składniki zostały dodane w [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="87904-127">Some components were added in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="87904-128">**CTRL** przeciągnij z składniki w widoku ViewController.h i dodać tych nowych punktów.</span><span class="sxs-lookup"><span data-stu-id="87904-128">**Ctrl** drag from the components in the view to ViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used to enable the buttons on the UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used to enabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="87904-129">W ViewController.h, Dodaj następujący `#define` poniżej Twojej instrukcje importu.</span><span class="sxs-lookup"><span data-stu-id="87904-129">In ViewController.h, add the following `#define` just below your import statements.</span></span> <span data-ttu-id="87904-130">SUBSTITUTE *< wprowadź swój Endpoint zaplecza\>*  symbol zastępczy docelowy adres URL używany do wdrażania aplikacji zaplecza w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="87904-130">Substitute the *<Enter Your Backend Endpoint\>* placeholder with the Destination URL you used to deploy your app backend in the previous section.</span></span> <span data-ttu-id="87904-131">Na przykład *http://you_backend.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="87904-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="87904-132">W projekcie, Utwórz nową **Cocoa Touch klasy** o nazwie **RegisterClient** do interfejsu z zaplecza ASP.NET został utworzony.</span><span class="sxs-lookup"><span data-stu-id="87904-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** to interface with the ASP.NET back-end you created.</span></span> <span data-ttu-id="87904-133">Tworzenie dziedziczenia z klasy `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="87904-133">Create the class inheriting from `NSObject`.</span></span> <span data-ttu-id="87904-134">Następnie dodaj następujący kod w RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="87904-134">Then add the following code in the RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="87904-135">W ramach aktualizacji RegisterClient.m `@interface` sekcji:</span><span class="sxs-lookup"><span data-stu-id="87904-135">In the RegisterClient.m update the `@interface` section:</span></span>
   
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
5. <span data-ttu-id="87904-136">Zastąp `@implementation` części RegisterClient.m następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="87904-136">Replace the `@implementation` section in the RegisterClient.m with the following code.</span></span>

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

    <span data-ttu-id="87904-137">Powyższy kod implementuje logiki wyjaśniono w artykule wskazówki [rejestrowanie z zaplecza aplikacji](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) wykonać REST przy użyciu polecenia NSURLSession wywołań zapleczu swojej aplikacji i NSUserDefaults do przechowywania lokalnie registrationId zwrócony przez Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="87904-137">The code above implements the logic explained in the guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession to perform REST calls to your app backend, and NSUserDefaults to locally store the registrationId returned by the notification hub.</span></span>

    <span data-ttu-id="87904-138">Należy pamiętać, że ta klasa wymaga jego właściwość **authorizationHeader** ustawiono prawidłowego funkcjonowania.</span><span class="sxs-lookup"><span data-stu-id="87904-138">Note that this class requires its property **authorizationHeader** to be set in order to work properly.</span></span> <span data-ttu-id="87904-139">Ta właściwość jest ustawiana przez **ViewController** klasy po stronie logowania.</span><span class="sxs-lookup"><span data-stu-id="87904-139">This property is set by the **ViewController** class after the log in.</span></span>

1. <span data-ttu-id="87904-140">W ViewController.h, Dodaj `#import` instrukcji dla RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="87904-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="87904-141">Następnie dodaj deklarację dla tokenu urządzenia i odwołać się do `RegisterClient` wystąpienia w `@interface` sekcji:</span><span class="sxs-lookup"><span data-stu-id="87904-141">Then add a declaration for the device token and reference to a `RegisterClient` instance in the `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="87904-142">W ViewController.m, Dodaj deklarację Metoda prywatna w `@interface` sekcji:</span><span class="sxs-lookup"><span data-stu-id="87904-142">In ViewController.m, add a private method declaration in the `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create the Authorization header to perform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="87904-143">Poniższy fragment kodu nie jest schemat bezpiecznego uwierzytelniania, należy zastąpić wykonania **createAndSetAuthenticationHeaderWithUsername:AndPassword:** z mechanizmu uwierzytelniania określonych generujący token uwierzytelniania do użycia przez klienta rejestru klasę, np. OAuth, usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="87904-143">The following snippet is not a secure authentication scheme, you should substitute the implementation of the **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token to be consumed by the register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="87904-144">Następnie w `@implementation` sekcji ViewController.m Dodaj następujący kod, który dodaje implementacji do ustawiania nagłówka tokenu i uwierzytelnienia urządzenia.</span><span class="sxs-lookup"><span data-stu-id="87904-144">Then in the `@implementation` section of ViewController.m add the following code which adds the implementation for setting the device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="87904-145">Należy zwrócić uwagę, jak ustawienie token urządzenia włącza przycisk Zaloguj.</span><span class="sxs-lookup"><span data-stu-id="87904-145">Note how setting the device token enables the log in button.</span></span> <span data-ttu-id="87904-146">Jest to spowodowane w ramach akcji logowania, kontroler widoku rejestruje dla powiadomień wypychanych przy użyciu zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="87904-146">This is becasue as a part of the login action, the view controller registers for push notifications with the app backend.</span></span> <span data-ttu-id="87904-147">W związku z tym nie chcemy dziennika w akcji była dostępna, dopóki token urządzenia został poprawnie skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="87904-147">Hence, we do not want Log In action to be accessible till the device token has been properly set up.</span></span> <span data-ttu-id="87904-148">Logowania z rejestracji wypychania jest oddzielana, tak długo, jak wcześniejsze nastąpi przed jego.</span><span class="sxs-lookup"><span data-stu-id="87904-148">You can decouple the log in from the push registration as long as the former happens before the latter.</span></span>
2. <span data-ttu-id="87904-149">W ViewController.m, należy użyć poniższej wstawki Aby zaimplementować metodę akcji dla Twojego **dziennika w** przycisk, a także metodę można wysłać komunikatu powiadomienia przy użyciu zaplecza ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="87904-149">In ViewController.m, use the following snippets to implement the action method for your **Log In** button and a method to send the notification message using the ASP.NET backend.</span></span>
   
       - <span data-ttu-id="87904-150">(IBAction) LogInAction: nadawcy (id) {/ / Utwórz nagłówek uwierzytelnienia i ustaw go w rejestrze klienta NSString * nazwa użytkownika = samodzielnie. UsernameField.text;   Hasło NSString * = samodzielnie. PasswordField.text;</span><span class="sxs-lookup"><span data-stu-id="87904-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="87904-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="87904-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="87904-152">__weak ViewController * selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tagi: nil andCompletion:^(NSError* error) {Jeśli (! błędu) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES;               [samoobsługowego MessageBox:@"Success" message:@"Registered pomyślnie!"];});}}];}</span><span class="sxs-lookup"><span data-stu-id="87904-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="87904-153">-SendNotificationASPNETBackend (void): (NSString*) systemu powiadomień platformy UsernameTag: (NSString*) usernameTag komunikat: (NSString*) komunikat {NSURLSession* sesji = [NSURLSession sessionWithConfiguration: delegateQueue:nil delegata: nil [NSURLSessionConfiguration defaultSessionConfiguration]];</span><span class="sxs-lookup"><span data-stu-id="87904-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="87904-154">Przekaż tag systemu powiadomień platformy i nazwa użytkownika jako parametry z adresem URL REST do zaplecza ASP.NET nsurl OCZEKIWANEGO * Adres_url_żądania = [URLWithString nsurl OCZEKIWANEGO: [NSString stringWithFormat:@"%@/api/notifications? systemu powiadomień platformy = % @& to_tag = % @", BACKEND_ENDPOINT, pns, usernameTag]];</span><span class="sxs-lookup"><span data-stu-id="87904-154">// Pass the pns and username tag as parameters with the REST URL to the ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="87904-155">Żądanie NSMutableURLRequest * = [NSMutableURLRequest requestWithURL:requestURL];    [setHTTPMethod:@"POST"żądania];</span><span class="sxs-lookup"><span data-stu-id="87904-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="87904-156">Pobierz zasymulować authenticationheader z rejestru klienta authorizationHeaderValue NSString * = [NSString stringWithFormat:@"Basic % @", self.registerClient.authenticationHeader];    [setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"żądania];</span><span class="sxs-lookup"><span data-stu-id="87904-156">// Get the mock authenticationheader from the register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="87904-157">Dodaj treść wiadomości powiadomienia [żądania setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [żądanie setHTTPBody: [komunikatów dataUsingEncoding:NSUTF8StringEncoding]];</span><span class="sxs-lookup"><span data-stu-id="87904-157">//Add the notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="87904-158">Wykonanie wysyłania powiadomień interfejsu API REST na dataTask ASP.NET zaplecza NSURLSessionDataTask * = [sesji dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) odpowiedź;        Jeśli (błąd || httpResponse.statusCode! = 200) {NSString* stan = [NSString stringWithFormat:@"Error stanu % @: % d\nError: %@\n", pns, httpResponse.statusCode, błąd];            dispatch_async(dispatch_get_main_queue(), ^ {/ / Append tekstu, ponieważ wszystkie wywołania systemu powiadomień platformy 3 może również zawierać informacje do widoku [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span><span class="sxs-lookup"><span data-stu-id="87904-158">// Execute the send notification REST API on the ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information to view                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="87904-159">}];    [dataTask Wznów]; }</span><span class="sxs-lookup"><span data-stu-id="87904-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="87904-160">Akcja dla aktualizacji **Wyślij powiadomienie E-mail** przycisk, aby użyć zaplecza ASP.NET i wysłać do dowolnego systemu powiadomień platformy włączane przez przełącznik.</span><span class="sxs-lookup"><span data-stu-id="87904-160">Update the action for the **Send Notification** button to use the ASP.NET backend and send to any PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="87904-161">W funkcji **ViewDidLoad**, Dodaj następujące można utworzyć wystąpienia RegisterClient wystąpienia i ustawić delegata dla pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="87904-161">In function **ViewDidLoad**, add the following to instantiate the RegisterClient instance and set the delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="87904-162">Teraz w **AppDelegate.m**, Usuń całą zawartość metody **aplikacji: didRegisterForPushNotificationWithDeviceToken:** i zastąp go z następujących czynności, aby upewnić się, że kontroler widoku zawiera najnowsze token urządzenia pobierane z usługi APNs:</span><span class="sxs-lookup"><span data-stu-id="87904-162">Now in **AppDelegate.m**, remove all the content of the method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with the following to make sure that the view controller contains the latest device token retrieved from APNs:</span></span>
   
       // Add import to the top of the file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="87904-163">Na koniec w **AppDelegate.m**, upewnij się, że masz następujące metody:</span><span class="sxs-lookup"><span data-stu-id="87904-163">Finally in **AppDelegate.m**, make sure you have the following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-the-application"></a><span data-ttu-id="87904-164">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="87904-164">Test the Application</span></span>
1. <span data-ttu-id="87904-165">W programie XCode Uruchom aplikację na urządzenie fizyczne z systemem iOS (wypychanie powiadomień nie będzie działać w symulatorze).</span><span class="sxs-lookup"><span data-stu-id="87904-165">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="87904-166">W aplikacji systemu iOS interfejsu użytkownika wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="87904-166">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="87904-167">Mogą to być dowolny ciąg, ale oba muszą być taką samą wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="87904-167">These can be any string, but they must both be the same string value.</span></span> <span data-ttu-id="87904-168">Następnie kliknij przycisk **dziennika w**.</span><span class="sxs-lookup"><span data-stu-id="87904-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="87904-169">Powinny zostać wyświetlone okno podręczne informujące o Powodzenie rejestracji.</span><span class="sxs-lookup"><span data-stu-id="87904-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="87904-170">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="87904-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="87904-171">W **tag username odbiorcy* tekst Wprowadź tag nazwę użytkownika używane z rejestracją z innego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="87904-171">In the **Recipient username tag* text field, enter the user name tag used with the registration from another device.</span></span>
5. <span data-ttu-id="87904-172">Wprowadź komunikat powiadomienia, a następnie kliknij przycisk **Wyślij powiadomienie E-mail**.</span><span class="sxs-lookup"><span data-stu-id="87904-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="87904-173">Tylko urządzenia, które ma rejestracji z tagiem nazwy użytkownika odbiorcy komunikat powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="87904-173">Only the devices that have a registration with the recipient user name tag receive the notification message.</span></span>  <span data-ttu-id="87904-174">Jest wysyłane tylko do tych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="87904-174">It is only sent to those users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
