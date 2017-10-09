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
# <a name="register-hello-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="a84fd-103">Zarejestruj hello bieżącego użytkownika dla powiadomień wypychanych przy użyciu platformy ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a84fd-103">Register hello current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a84fd-104">iOS</span><span class="sxs-lookup"><span data-stu-id="a84fd-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a84fd-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a84fd-105">Overview</span></span>
<span data-ttu-id="a84fd-106">W tym temacie pokazano, jak toorequest rejestracja powiadomień wypychanych przy użyciu usługi Azure Notification Hubs rejestracji jest wykonywane przez interfejs API sieci Web platformy ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a84fd-106">This topic shows you how toorequest push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="a84fd-107">W tym temacie rozszerza samouczek hello [powiadomić użytkowników z usługą Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="a84fd-107">This topic extends hello tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="a84fd-108">Została już ukończona hello wymagane kroki tego samouczka toocreate usługi mobilnej hello uwierzytelniony.</span><span class="sxs-lookup"><span data-stu-id="a84fd-108">You must have already completed hello required steps in that tutorial toocreate hello authenticated mobile service.</span></span> <span data-ttu-id="a84fd-109">Aby uzyskać więcej informacji na temat hello powiadomić użytkowników scenariusza, zobacz [powiadomić użytkowników z usługą Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="a84fd-109">For more information on hello notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="a84fd-110">Aktualizowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="a84fd-110">Update your app</span></span>
1. <span data-ttu-id="a84fd-111">W Twojej MainStoryboard_iPhone.storyboard Dodaj hello poniższych składników z biblioteki obiektów hello:</span><span class="sxs-lookup"><span data-stu-id="a84fd-111">In your MainStoryboard_iPhone.storyboard, add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="a84fd-112">**Etykieta**: "TooUser z koncentratorami powiadomień wypychanych"</span><span class="sxs-lookup"><span data-stu-id="a84fd-112">**Label**: "Push tooUser with Notification Hubs"</span></span>
   * <span data-ttu-id="a84fd-113">**Etykieta**: "Identyfikator InstallationId"</span><span class="sxs-lookup"><span data-stu-id="a84fd-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="a84fd-114">**Etykieta**: "Użytkownika"</span><span class="sxs-lookup"><span data-stu-id="a84fd-114">**Label**: "User"</span></span>
   * <span data-ttu-id="a84fd-115">**Pole tekstowe**: "Użytkownika"</span><span class="sxs-lookup"><span data-stu-id="a84fd-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="a84fd-116">**Etykieta**: "Password"</span><span class="sxs-lookup"><span data-stu-id="a84fd-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="a84fd-117">**Pole tekstowe**: "Password"</span><span class="sxs-lookup"><span data-stu-id="a84fd-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="a84fd-118">**Przycisk**: "Logowanie"</span><span class="sxs-lookup"><span data-stu-id="a84fd-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="a84fd-119">W tym momencie z scenorysu wygląda hello:</span><span class="sxs-lookup"><span data-stu-id="a84fd-119">At this point, your storyboard looks like hello following:</span></span>
     
      ![][0]
2. <span data-ttu-id="a84fd-120">W edytorze Asystenta hello, utworzyć gniazda dla wszystkich kontrolek hello przełączono połączeń telefonicznych z nimi, uzyskuj pól tekstowych hello hello kontrolera widoku (delegat) i utworzyć **akcji** dla hello **logowania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a84fd-120">In hello assistant editor, create outlets for all hello switched controls and call them, connect hello text fields with hello View Controller (delegate), and create an **Action** for hello **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain hello following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="a84fd-121">Utwórz klasę o nazwie **DeviceInfo**, i kopiowania hello po kodu do sekcji interfejsu hello hello pliku DeviceInfo.h:</span><span class="sxs-lookup"><span data-stu-id="a84fd-121">Create a class named **DeviceInfo**, and copy hello following code into hello interface section of hello file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="a84fd-122">Skopiuj hello następującego kodu w sekcji implementacji hello hello DeviceInfo.m pliku:</span><span class="sxs-lookup"><span data-stu-id="a84fd-122">Copy hello following code in hello implementation section of hello DeviceInfo.m file:</span></span>
   
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
5. <span data-ttu-id="a84fd-123">W PushToUserAppDelegate.h Dodaj następujące właściwości singleton hello:</span><span class="sxs-lookup"><span data-stu-id="a84fd-123">In PushToUserAppDelegate.h, add hello following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="a84fd-124">W hello **didFinishLaunchingWithOptions** metody w PushToUserAppDelegate.m, Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="a84fd-124">In hello **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add hello following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="a84fd-125">pierwszy wiersz Hello inicjuje hello **DeviceInfo** singleton.</span><span class="sxs-lookup"><span data-stu-id="a84fd-125">hello first line initializes hello **DeviceInfo** singleton.</span></span> <span data-ttu-id="a84fd-126">Witaj drugiego wiersza uruchamia hello rejestracji dla powiadomień wypychanych, który znajduje się już jest zostały już wykonane hello [Rozpoczynanie pracy z usługą Notification Hubs] samouczka.</span><span class="sxs-lookup"><span data-stu-id="a84fd-126">hello second line starts hello registration for push notifications, which is already present is you have already completed hello [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="a84fd-127">W PushToUserAppDelegate.m, zaimplementuj metodę hello **didRegisterForRemoteNotificationsWithDeviceToken** w Twojej AppDelegate i Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="a84fd-127">In PushToUserAppDelegate.m, implement hello method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add hello following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="a84fd-128">To ustawienie token urządzenia hello hello żądania.</span><span class="sxs-lookup"><span data-stu-id="a84fd-128">This sets hello device token for hello request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a84fd-129">W tym momencie nie powinien zawierać dowolny kod w ramach tej metody.</span><span class="sxs-lookup"><span data-stu-id="a84fd-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="a84fd-130">Jeśli masz już toohello wywołanie **registerNativeWithDeviceToken** metodę, która została dodana po zakończeniu hello [Rozpoczynanie pracy z usługą Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) samouczka musisz komentarz lub które zostaną usunięte wywołanie.</span><span class="sxs-lookup"><span data-stu-id="a84fd-130">If you already have a call toohello **registerNativeWithDeviceToken** method that was added when you completed hello [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="a84fd-131">W pliku PushToUserAppDelegate.m hello Dodaj następujące metody obsługi hello:</span><span class="sxs-lookup"><span data-stu-id="a84fd-131">In hello PushToUserAppDelegate.m file, add hello following handler method:</span></span>
   
   * <span data-ttu-id="a84fd-132">informacje o użytkowniku aplikacji (void):(UIApplication *) aplikacji didReceiveRemoteNotification:(NSDictionary *) {NSLog (@"% @", informacje o użytkowniku);   UIAlertView * alert = [[UIAlertView alokacji] initWithTitle:@"Notification" komunikat: cancelButtonTitle delegata: nil [informacje o użytkowniku objectForKey:@"inAppMessage"]: @ otherButtonTitles:nil "OK", nil];   [Pokaż alert] }</span><span class="sxs-lookup"><span data-stu-id="a84fd-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="a84fd-133">Ta metoda wyświetla alert w hello interfejsu użytkownika, gdy aplikacji otrzymuje powiadomienia, gdy jest on uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="a84fd-133">This method displays an alert in hello UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="a84fd-134">Otwórz plik PushToUserViewController.m hello i klawiatury hello zwracany powitania po implementacji:</span><span class="sxs-lookup"><span data-stu-id="a84fd-134">Open hello PushToUserViewController.m file, and return hello keyboard in hello following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="a84fd-135">W hello **viewDidLoad** metody w pliku PushToUserViewController.m hello zainicjować hello installationId etykietę w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a84fd-135">In hello **viewDidLoad** method in hello PushToUserViewController.m file, initialize hello installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="a84fd-136">Dodaj następujące właściwości w interfejsie w PushToUserViewController.m hello:</span><span class="sxs-lookup"><span data-stu-id="a84fd-136">Add hello following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="a84fd-137">Następnie należy dodać powitania po implementacji:</span><span class="sxs-lookup"><span data-stu-id="a84fd-137">Then, add hello following implementation:</span></span>
    
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
13. <span data-ttu-id="a84fd-138">Kopiuj hello poniższy kod do hello **logowania** metoda obsługi utworzone przez XCode:</span><span class="sxs-lookup"><span data-stu-id="a84fd-138">Copy hello following code into hello **login** handler method created by XCode:</span></span>
    
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
    
    <span data-ttu-id="a84fd-139">Ta metoda pobiera zarówno identyfikator instalacji, jak i kanału dla powiadomień wypychanych i wysyła je, wraz z typem urządzenia hello, toohello uwierzytelniony metody interfejsu API sieci Web, która tworzy rejestracji w usłudze Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="a84fd-139">This method gets both an installation ID and channel for push notifications and sends it, along with hello device type, toohello authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="a84fd-140">Ten interfejs API sieci Web został zdefiniowany w [powiadomić użytkowników z usługą Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="a84fd-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="a84fd-141">Teraz, gdy hello klienta aplikacja została zaktualizowana, zwróć toohello [powiadomić użytkowników z usługą Notification Hubs] i zaktualizować hello usługi mobilnej toosend powiadomienia przy użyciu usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="a84fd-141">Now that hello client app has been updated, return toohello [Notify users with Notification Hubs] and update hello mobile service toosend notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
[powiadomić użytkowników z usługą Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet

[Rozpoczynanie pracy z usługą Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-ios
