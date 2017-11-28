---
title: "Wypychania sformatowanego centra powiadomień Azure"
description: "Dowiedz się, jak wysyłać powiadomienia wypychane sformatowanego do aplikacji systemu iOS z platformy Azure. Przykłady kodu napisane w języku Objective C i C#."
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
ms.openlocfilehash: 394efdc2dfaff0666bc23d8a448b0a00d414da99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="8c958-104">Wypychania sformatowanego centra powiadomień Azure</span><span class="sxs-lookup"><span data-stu-id="8c958-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="8c958-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8c958-105">Overview</span></span>
<span data-ttu-id="8c958-106">Aby angażowania użytkowników błyskawicznych sformatowanego zawartość, aplikacja może być push poza zwykły tekst.</span><span class="sxs-lookup"><span data-stu-id="8c958-106">In order to engage users with instant rich contents, an application might want to push beyond plain text.</span></span> <span data-ttu-id="8c958-107">Te powiadomienia wspierania interakcji użytkowników i obecny zawartości, takie jak adresy URL, dźwięki, obrazy/bony i.</span><span class="sxs-lookup"><span data-stu-id="8c958-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="8c958-108">W tym samouczku opiera się na [Powiadom użytkowników](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tematu i pokazuje, jak wysyłać powiadomienia wypychane, zawierające ładunków (na przykład obraz).</span><span class="sxs-lookup"><span data-stu-id="8c958-108">This tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how to send push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="8c958-109">W tym samouczku jest zgodny z systemem iOS 7 i 8.</span><span class="sxs-lookup"><span data-stu-id="8c958-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="8c958-110">Na wysokim poziomie:</span><span class="sxs-lookup"><span data-stu-id="8c958-110">At a high level:</span></span>

1. <span data-ttu-id="8c958-111">Zaplecze aplikacji:</span><span class="sxs-lookup"><span data-stu-id="8c958-111">The app backend:</span></span>
   * <span data-ttu-id="8c958-112">Przechowuje sformatowanego ładunku (w tym przypadku obrazu) w magazynie bazy danych i lokalnym wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="8c958-112">Stores the rich payload (in this case, image) in the backend database/local storage</span></span>
   * <span data-ttu-id="8c958-113">Wysyła identyfikator sformatowanego powiadomienia do urządzenia</span><span class="sxs-lookup"><span data-stu-id="8c958-113">Sends ID of this rich notification to the device</span></span>
2. <span data-ttu-id="8c958-114">Aplikacją na urządzeniu:</span><span class="sxs-lookup"><span data-stu-id="8c958-114">App on the device:</span></span>
   * <span data-ttu-id="8c958-115">Kontakty zaplecza sformatowanego ładunku o identyfikatorze odbiera żądanie</span><span class="sxs-lookup"><span data-stu-id="8c958-115">Contacts the backend requesting the rich payload with the ID it receives</span></span>
   * <span data-ttu-id="8c958-116">Wysyła powiadomienia użytkowników na urządzeniu, po zakończeniu pobierania danych i pokazuje ładunku natychmiast, gdy użytkownik naciśnie polecenie, aby dowiedzieć się więcej</span><span class="sxs-lookup"><span data-stu-id="8c958-116">Sends users notifications on the device when data retrieval is complete, and shows the payload immediately when users tap to learn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="8c958-117">WebAPI projektu</span><span class="sxs-lookup"><span data-stu-id="8c958-117">WebAPI Project</span></span>
1. <span data-ttu-id="8c958-118">W programie Visual Studio Otwórz **AppBackend** projektu, który został utworzony w [Powiadom użytkowników](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="8c958-118">In Visual Studio, open the **AppBackend** project that you created in the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="8c958-119">Uzyskaj obraz chcesz powiadamiać użytkowników i umieszcza je **img** folderu w katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="8c958-119">Obtain an image you would like to notify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="8c958-120">Kliknij przycisk **Pokaż wszystkie pliki** w Eksploratorze rozwiązań i kliknij prawym przyciskiem myszy folder, z którego **załącz do projektu**.</span><span class="sxs-lookup"><span data-stu-id="8c958-120">Click **Show All Files** in the Solution Explorer, and right-click the folder to **Include In Project**.</span></span>
4. <span data-ttu-id="8c958-121">Zaznacz obraz, zmienić jego akcji kompilacji w oknie właściwości, aby **osadzonego zasobu**.</span><span class="sxs-lookup"><span data-stu-id="8c958-121">With the image selected, change its Build Action in Properties window to **Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="8c958-122">W **Notifications.cs**, dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="8c958-122">In **Notifications.cs**, add the following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="8c958-123">Aktualizacji całym **powiadomienia** klasy następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="8c958-123">Update the whole **Notifications** class with the following code.</span></span> <span data-ttu-id="8c958-124">Pamiętaj zastąpić symbole zastępcze poświadczenia Centrum powiadomień i nazwę pliku obrazu.</span><span class="sxs-lookup"><span data-stu-id="8c958-124">Be sure to replace the placeholders with your notification hub credentials and image file name.</span></span>
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message to display to users
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
                // Placeholders: replace with the connection string (with full access) for your notification hub and the hub name from the Azure Classics Portal
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
   > <span data-ttu-id="8c958-125">(opcjonalnie) Zapoznaj się [jak osadzić i uzyskiwać dostęp do zasobów przy użyciu programu Visual C#](http://support.microsoft.com/kb/319292) Aby uzyskać więcej informacji na temat sposobu dodawania i uzyskiwanie zasobów projektu.</span><span class="sxs-lookup"><span data-stu-id="8c958-125">(optional) Refer to [How to embed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how to add and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="8c958-126">W **NotificationsController.cs**, Zmień definicję **NotificationsController** z poniższe fragmenty kodu.</span><span class="sxs-lookup"><span data-stu-id="8c958-126">In **NotificationsController.cs**, redefine **NotificationsController**  with the following snippets.</span></span> <span data-ttu-id="8c958-127">Wysyła identyfikator początkowej dyskretnej sformatowanego powiadomień do urządzeń i umożliwia pobranie obrazu po stronie klienta:</span><span class="sxs-lookup"><span data-stu-id="8c958-127">This sends an initial silent rich notification id to device and allows client-side retrieval of image:</span></span>
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) to client
        public async Task<HttpResponseMessage> Post() {
            // Replace the placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification to apns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. <span data-ttu-id="8c958-128">Teraz ponownie wdrożymy tę aplikację do witryny sieci Web platformy Azure, aby udostępnić go ze wszystkich urządzeń.</span><span class="sxs-lookup"><span data-stu-id="8c958-128">Now we will re-deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="8c958-129">Kliknij prawym przyciskiem myszy projekt **AppBackend** i wybierz polecenie **Publikuj**.</span><span class="sxs-lookup"><span data-stu-id="8c958-129">Right-click on the **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="8c958-130">Wybierz urządzenie docelowe publikowania witryny sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8c958-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="8c958-131">Zaloguj się przy użyciu konta platformy Azure i wybierz istniejącą lub nową witrynę sieci Web i zanotuj **docelowy adres URL** właściwości w **połączenia** kartę.</span><span class="sxs-lookup"><span data-stu-id="8c958-131">Log in with your Azure account and select an existing or new Website, and make a note of the **destination URL** property in the **Connection** tab.</span></span> <span data-ttu-id="8c958-132">W dalszej części tego samouczka będziemy nazywać ten adres URL *punktem końcowym zaplecza*.</span><span class="sxs-lookup"><span data-stu-id="8c958-132">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="8c958-133">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="8c958-133">Click **Publish**.</span></span>

## <a name="modify-the-ios-project"></a><span data-ttu-id="8c958-134">Zmodyfikuj projekt dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="8c958-134">Modify the iOS project</span></span>
<span data-ttu-id="8c958-135">Teraz, gdy zmieniono zapleczu swojej aplikacji, aby wysłać tylko *identyfikator* powiadomienia, spowoduje zmianę aplikacji systemu iOS do obsługi tego identyfikatora i pobierania sformatowany komunikat z zaplecza.</span><span class="sxs-lookup"><span data-stu-id="8c958-135">Now that you have modified your app backend to send just the *id* of a notification, you will change your iOS app to handle that id and retrieve the rich message from your backend.</span></span>

1. <span data-ttu-id="8c958-136">Otwórz projekt dla systemu iOS i włączyć zdalne powiadomienia, przechodząc do urządzenie docelowe głównej aplikacji w **cele** sekcji.</span><span class="sxs-lookup"><span data-stu-id="8c958-136">Open your iOS project, and enable remote notifications by going to your main app target in the **Targets** section.</span></span>
2. <span data-ttu-id="8c958-137">Polecenie **możliwości**, Włącz **tryby tła**i sprawdź **zdalnego powiadomienia** wyboru.</span><span class="sxs-lookup"><span data-stu-id="8c958-137">Click on **Capabilities**, turn on **Background Modes**, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="8c958-138">Przejdź do **Main.storyboard**i upewnij się, że masz kontroler widoku (określonej jako Home kontrolera widoku w tym samouczku) z [powiadamia użytkownika](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="8c958-138">Go to **Main.storyboard**, and make sure you have a View Controller (refered to as Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="8c958-139">Dodaj **kontrolera nawigacji** do scenorysu i kontrolki przeciągania Home kontrolera widoku umożliwia **Widok główny** nawigacji.</span><span class="sxs-lookup"><span data-stu-id="8c958-139">Add a **Navigation Controller** to your storyboard, and control-drag to Home View Controller to make it the **root view** of navigation.</span></span> <span data-ttu-id="8c958-140">Upewnij się, że **jest początkowej kontrolera widoku** w atrybutach inspektora wybrano tylko kontrolera nawigacji.</span><span class="sxs-lookup"><span data-stu-id="8c958-140">Make sure the **Is Initial View Controller** in Attributes inspector is selected for the Navigation Controller only.</span></span>
5. <span data-ttu-id="8c958-141">Dodaj **kontrolera widoku** scenorysu, a następnie dodaj **widoku obrazu**.</span><span class="sxs-lookup"><span data-stu-id="8c958-141">Add a **View Controller** to storyboard and add an **Image View**.</span></span> <span data-ttu-id="8c958-142">Jest to strona, którą użytkownicy zobaczą, gdy wybiera on dowiedzieć się więcej, klikając notifiication.</span><span class="sxs-lookup"><span data-stu-id="8c958-142">This is the page users will see once they choose to learn more by clicking on the notifiication.</span></span> <span data-ttu-id="8c958-143">Twoje scenorysu powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="8c958-143">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="8c958-144">Polecenie **Home kontrolera widoku** scenorysu, i upewnij się, że ma ona **homeViewController** jako jego **klasy niestandardowej** i **scenorysu identyfikator**w obszarze inspektora tożsamości.</span><span class="sxs-lookup"><span data-stu-id="8c958-144">Click on the **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under the Identity inspector.</span></span>
7. <span data-ttu-id="8c958-145">Wykonaj te same czynności dla obrazu kontroler widoku jako **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="8c958-145">Do the same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="8c958-146">Następnie utwórz nową klasę kontrolera widoku zatytułowany **imageViewController** do obsługi interfejsu użytkownika został utworzony.</span><span class="sxs-lookup"><span data-stu-id="8c958-146">Then, create a new View Controller class titled **imageViewController** to handle the UI you just created.</span></span>
9. <span data-ttu-id="8c958-147">W **imageViewController.h**, Dodaj następujący kod do kontrolera deklaracji interfejsu.</span><span class="sxs-lookup"><span data-stu-id="8c958-147">In **imageViewController.h**, add the following to the controller's interface declarations.</span></span> <span data-ttu-id="8c958-148">Upewnij się, że formant podczas przeciągania z widoku obrazu scenorysu te właściwości, aby połączyć dwóch:</span><span class="sxs-lookup"><span data-stu-id="8c958-148">Make sure to control-drag from the storyboard image view to these properties to link the two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="8c958-149">W **imageViewController.m**, Dodaj następujący kod na końcu **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="8c958-149">In **imageViewController.m**, add the following at the end of **viewDidload**:</span></span>
    
        // Display the UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="8c958-150">W **AppDelegate.m**, zaimportuj kontrolera obraz został utworzony:</span><span class="sxs-lookup"><span data-stu-id="8c958-150">In **AppDelegate.m**, import the image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="8c958-151">Dodaj sekcję interfejsu z deklaracją następujące:</span><span class="sxs-lookup"><span data-stu-id="8c958-151">Add an interface section with the following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect to Image View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="8c958-152">W **AppDelegate**, upewnij się, że aplikacja rejestruje dyskretnej powiadomień w **aplikacji: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="8c958-152">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="8c958-153">Subsitute w następujących implementacji dla **aplikacji: didRegisterForRemoteNotificationsWithDeviceToken** do wykonania dla scenorysu zmiany interfejsu użytkownika do konta:</span><span class="sxs-lookup"><span data-stu-id="8c958-153">Subsitute in the following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** to take the storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at the root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="8c958-154">Następnie należy dodać następujące metody umożliwiające **AppDelegate.m** można pobrać obrazu z punktu końcowego i wysyłania powiadomień lokalnego, po ukończeniu pobierania.</span><span class="sxs-lookup"><span data-stu-id="8c958-154">Then, add the following methods to **AppDelegate.m** to retrieve the image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="8c958-155">Zastąp symbol zastępczy `{backend endpoint}` z wewnętrznej bazy danych punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="8c958-155">Make sure to substitute the placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
                   // From NSData to UIImage
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
   
                       // "5" is arbitrary here to give you enough time to quit out of the app and receive push notifications
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
           // Add "else if" here to handle more types of rich content such as url, sound files, etc.
       }
3. <span data-ttu-id="8c958-156">Obsługę lokalnego powiadomienia powyżej otwierając kontroler widoku obrazu w **AppDelegate.m** z następujących metod:</span><span class="sxs-lookup"><span data-stu-id="8c958-156">Handle the local notification above by opening up the image view controller in **AppDelegate.m** with the following methods:</span></span>
   
       // Helper: redirect users to image view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image to image view controller
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
           // Add "else if" here to handle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-the-application"></a><span data-ttu-id="8c958-157">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="8c958-157">Run the Application</span></span>
1. <span data-ttu-id="8c958-158">W programie XCode Uruchom aplikację na urządzenie fizyczne z systemem iOS (wypychanie powiadomień nie będzie działać w symulatorze).</span><span class="sxs-lookup"><span data-stu-id="8c958-158">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="8c958-159">W aplikacji systemu iOS interfejsu użytkownika, wprowadź nazwę użytkownika i hasła tę samą wartość do uwierzytelniania i kliknięcie **dziennika w**.</span><span class="sxs-lookup"><span data-stu-id="8c958-159">In the iOS app UI, enter a username and password of the same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="8c958-160">Kliknij przycisk **wysyłania wypychania** i powinien zostać wyświetlony alert w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c958-160">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="8c958-161">Po kliknięciu **więcej**, zostanie przeniesiony do obrazu chcesz uwzględnić w zapleczu swojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8c958-161">If you click on **More**, you will be brought to the image you chose to include in your app backend.</span></span>
4. <span data-ttu-id="8c958-162">Możesz również kliknąć **wysyłania wypychania** i natychmiast naciśnij przycisk macierzystego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="8c958-162">You can also click **Send push** and immediately press the home button of your device.</span></span> <span data-ttu-id="8c958-163">Za chwilę otrzymasz powiadomienie wypychane.</span><span class="sxs-lookup"><span data-stu-id="8c958-163">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="8c958-164">Wybierz na niej, lub kliknij przycisk więcej, zostanie wyświetlona do aplikacji i sformatowanego obrazu.</span><span class="sxs-lookup"><span data-stu-id="8c958-164">If you tap on it or click More, you will be brought to your app and the rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
