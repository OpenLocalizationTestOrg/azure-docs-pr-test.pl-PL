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
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="e98f1-104">Wypychania sformatowanego centra powiadomień Azure</span><span class="sxs-lookup"><span data-stu-id="e98f1-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="e98f1-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e98f1-105">Overview</span></span>
<span data-ttu-id="e98f1-106">W kolejności tooengage użytkownikom błyskawiczne sformatowanego zawartość aplikacja może być toopush poza zwykły tekst.</span><span class="sxs-lookup"><span data-stu-id="e98f1-106">In order tooengage users with instant rich contents, an application might want toopush beyond plain text.</span></span> <span data-ttu-id="e98f1-107">Te powiadomienia wspierania interakcji użytkowników i obecny zawartości, takie jak adresy URL, dźwięki, obrazy/bony i.</span><span class="sxs-lookup"><span data-stu-id="e98f1-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="e98f1-108">W tym samouczku opiera się na powitania [Powiadom użytkowników](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tematu i pokazuje, jak toosend wypychanie powiadomień, zawierające ładunków (na przykład obraz).</span><span class="sxs-lookup"><span data-stu-id="e98f1-108">This tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how toosend push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="e98f1-109">W tym samouczku jest zgodny z systemem iOS 7 i 8.</span><span class="sxs-lookup"><span data-stu-id="e98f1-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="e98f1-110">Na wysokim poziomie:</span><span class="sxs-lookup"><span data-stu-id="e98f1-110">At a high level:</span></span>

1. <span data-ttu-id="e98f1-111">zaplecze aplikacji Hello:</span><span class="sxs-lookup"><span data-stu-id="e98f1-111">hello app backend:</span></span>
   * <span data-ttu-id="e98f1-112">Magazyny hello ładunku sformatowanego (w tym przypadku obrazu) w magazynie bazy danych i lokalnym zaplecza hello</span><span class="sxs-lookup"><span data-stu-id="e98f1-112">Stores hello rich payload (in this case, image) in hello backend database/local storage</span></span>
   * <span data-ttu-id="e98f1-113">Wysyła identyfikator tego urządzenia toohello sformatowanego powiadomień</span><span class="sxs-lookup"><span data-stu-id="e98f1-113">Sends ID of this rich notification toohello device</span></span>
2. <span data-ttu-id="e98f1-114">Aplikacja hello urządzenia:</span><span class="sxs-lookup"><span data-stu-id="e98f1-114">App on hello device:</span></span>
   * <span data-ttu-id="e98f1-115">Kontakty hello hello ładunku sformatowanym identyfikatorem hello odbierze żądanie wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="e98f1-115">Contacts hello backend requesting hello rich payload with hello ID it receives</span></span>
   * <span data-ttu-id="e98f1-116">Wysyła powiadomienia użytkowników na urządzeniu hello, po zakończeniu pobierania danych i zawiera ładunek hello natychmiast, gdy użytkownik naciśnie polecenie toolearn więcej</span><span class="sxs-lookup"><span data-stu-id="e98f1-116">Sends users notifications on hello device when data retrieval is complete, and shows hello payload immediately when users tap toolearn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="e98f1-117">WebAPI projektu</span><span class="sxs-lookup"><span data-stu-id="e98f1-117">WebAPI Project</span></span>
1. <span data-ttu-id="e98f1-118">W programie Visual Studio Otwórz hello **AppBackend** projektu, który został utworzony w hello [Powiadom użytkowników](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="e98f1-118">In Visual Studio, open hello **AppBackend** project that you created in hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="e98f1-119">Uzyskaj obraz chcesz toonotify użytkownikom i umieszcza je **img** folderu w katalogu projektu.</span><span class="sxs-lookup"><span data-stu-id="e98f1-119">Obtain an image you would like toonotify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="e98f1-120">Kliknij przycisk **Pokaż wszystkie pliki** w hello Eksploratorze rozwiązań i kliknij prawym przyciskiem myszy hello folder zbyt**załącz do projektu**.</span><span class="sxs-lookup"><span data-stu-id="e98f1-120">Click **Show All Files** in hello Solution Explorer, and right-click hello folder too**Include In Project**.</span></span>
4. <span data-ttu-id="e98f1-121">Wybrany obraz powitania, zmienić jego Akcja kompilacji w oknie właściwości zbyt**osadzonego zasobu**.</span><span class="sxs-lookup"><span data-stu-id="e98f1-121">With hello image selected, change its Build Action in Properties window too**Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="e98f1-122">W **Notifications.cs**, Dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="e98f1-122">In **Notifications.cs**, add hello following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="e98f1-123">Aktualizacja hello całego **powiadomienia** klasy z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="e98f1-123">Update hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="e98f1-124">Należy się tooreplace symbole zastępcze hello poświadczenia Centrum powiadomień i nazwę pliku obrazu.</span><span class="sxs-lookup"><span data-stu-id="e98f1-124">Be sure tooreplace hello placeholders with your notification hub credentials and image file name.</span></span>
   
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
   > <span data-ttu-id="e98f1-125">(opcjonalnie) Odwołuje się zbyt[jak tooembed i dostęp do zasobów przy użyciu programu Visual C#](http://support.microsoft.com/kb/319292) Aby uzyskać więcej informacji na temat tooadd i uzyskiwanie zasobów projektu.</span><span class="sxs-lookup"><span data-stu-id="e98f1-125">(optional) Refer too[How tooembed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how tooadd and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="e98f1-126">W **NotificationsController.cs**, Zmień definicję **NotificationsController** z powitania po fragmentów.</span><span class="sxs-lookup"><span data-stu-id="e98f1-126">In **NotificationsController.cs**, redefine **NotificationsController**  with hello following snippets.</span></span> <span data-ttu-id="e98f1-127">Wysyła toodevice identyfikator początkowym powiadomieniu sformatowanego dyskretnej i umożliwia pobranie obrazu po stronie klienta:</span><span class="sxs-lookup"><span data-stu-id="e98f1-127">This sends an initial silent rich notification id toodevice and allows client-side retrieval of image:</span></span>
   
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
8. <span data-ttu-id="e98f1-128">Teraz ponownie wdrożymy ten tooan aplikacji witryny sieci Web Azure w kolejności toomake go ze wszystkich urządzeń.</span><span class="sxs-lookup"><span data-stu-id="e98f1-128">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="e98f1-129">Kliknij prawym przyciskiem myszy na powitania **AppBackend** projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="e98f1-129">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="e98f1-130">Wybierz urządzenie docelowe publikowania witryny sieci Web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e98f1-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="e98f1-131">Zaloguj się przy użyciu konta platformy Azure i wybierz istniejącą lub nową witrynę sieci Web i zanotuj hello **docelowy adres URL** właściwości w hello **połączenia** kartę. Odnoszą się adres URL toothis Twojego *wewnętrznej bazy danych punktu końcowego* dalszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="e98f1-131">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="e98f1-132">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="e98f1-132">Click **Publish**.</span></span>

## <a name="modify-hello-ios-project"></a><span data-ttu-id="e98f1-133">Modyfikowanie hello projekt dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="e98f1-133">Modify hello iOS project</span></span>
<span data-ttu-id="e98f1-134">Teraz, gdy zmieniono Twojej aplikacji zaplecza toosend tylko hello *identyfikator* powiadomienia, będzie zmienić ten identyfikator użytkownika toohandle aplikacji systemu iOS i pobrać sformatowanego wiadomość hello z poziomu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="e98f1-134">Now that you have modified your app backend toosend just hello *id* of a notification, you will change your iOS app toohandle that id and retrieve hello rich message from your backend.</span></span>

1. <span data-ttu-id="e98f1-135">Otwórz projekt dla systemu iOS, a następnie Włącz powiadomienia zdalne przez przechodzi do docelowej aplikacji głównej tooyour w hello **cele** sekcji.</span><span class="sxs-lookup"><span data-stu-id="e98f1-135">Open your iOS project, and enable remote notifications by going tooyour main app target in hello **Targets** section.</span></span>
2. <span data-ttu-id="e98f1-136">Polecenie **możliwości**, Włącz **tryby tła**i sprawdź hello **zdalnego powiadomienia** wyboru.</span><span class="sxs-lookup"><span data-stu-id="e98f1-136">Click on **Capabilities**, turn on **Background Modes**, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="e98f1-137">Przejdź za**Main.storyboard**i upewnij się, że masz kontroler widoku (tooas określonej Home kontrolera widoku w tym samouczku) z [powiadamia użytkownika](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="e98f1-137">Go too**Main.storyboard**, and make sure you have a View Controller (refered tooas Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="e98f1-138">Dodaj **kontrolera nawigacji** tooyour scenorysu, a następnie przeciągnij formant toomake kontrolera widoku tooHome go hello **Widok główny** nawigacji.</span><span class="sxs-lookup"><span data-stu-id="e98f1-138">Add a **Navigation Controller** tooyour storyboard, and control-drag tooHome View Controller toomake it hello **root view** of navigation.</span></span> <span data-ttu-id="e98f1-139">Upewnij się, że hello **jest początkowej kontrolera widoku** w atrybutach inspektora został wybrany do hello tylko kontrolera nawigacji.</span><span class="sxs-lookup"><span data-stu-id="e98f1-139">Make sure hello **Is Initial View Controller** in Attributes inspector is selected for hello Navigation Controller only.</span></span>
5. <span data-ttu-id="e98f1-140">Dodaj **kontrolera widoku** toostoryboard i Dodaj **widoku obrazu**.</span><span class="sxs-lookup"><span data-stu-id="e98f1-140">Add a **View Controller** toostoryboard and add an **Image View**.</span></span> <span data-ttu-id="e98f1-141">Jest to strona hello, które użytkownicy zobaczą, gdy wybiera on toolearn więcej klikając hello notifiication.</span><span class="sxs-lookup"><span data-stu-id="e98f1-141">This is hello page users will see once they choose toolearn more by clicking on hello notifiication.</span></span> <span data-ttu-id="e98f1-142">Twoje scenorysu powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e98f1-142">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="e98f1-143">Polecenie hello **Home kontrolera widoku** scenorysu, i upewnij się, że ma ona **homeViewController** jako jego **klasy niestandardowej** i **scenorysu identyfikator**w obszarze hello inspektora tożsamości.</span><span class="sxs-lookup"><span data-stu-id="e98f1-143">Click on hello **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under hello Identity inspector.</span></span>
7. <span data-ttu-id="e98f1-144">Witaj takie same dla obrazu kontroler widoku jako **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="e98f1-144">Do hello same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="e98f1-145">Następnie utwórz nową klasę kontrolera widoku zatytułowany **imageViewController** toohandle hello właśnie utworzony interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e98f1-145">Then, create a new View Controller class titled **imageViewController** toohandle hello UI you just created.</span></span>
9. <span data-ttu-id="e98f1-146">W **imageViewController.h**, Dodaj powitania po deklaracji interfejsów toohello kontrolera.</span><span class="sxs-lookup"><span data-stu-id="e98f1-146">In **imageViewController.h**, add hello following toohello controller's interface declarations.</span></span> <span data-ttu-id="e98f1-147">Upewnij się, że toocontrol i przeciągnij od Witaj scenorysu obrazu widoku toothese właściwości toolink Witaj dwie:</span><span class="sxs-lookup"><span data-stu-id="e98f1-147">Make sure toocontrol-drag from hello storyboard image view toothese properties toolink hello two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="e98f1-148">W **imageViewController.m**, Dodaj następujące hello na końcu hello **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="e98f1-148">In **imageViewController.m**, add hello following at hello end of **viewDidload**:</span></span>
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="e98f1-149">W **AppDelegate.m**, kontrolera obraz powitania importu utworzone:</span><span class="sxs-lookup"><span data-stu-id="e98f1-149">In **AppDelegate.m**, import hello image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="e98f1-150">Dodaj sekcję interfejsu z powitania po deklaracji:</span><span class="sxs-lookup"><span data-stu-id="e98f1-150">Add an interface section with hello following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="e98f1-151">W **AppDelegate**, upewnij się, że aplikacja rejestruje dyskretnej powiadomień w **aplikacji: didFinishLaunchingWithOptions**:</span><span class="sxs-lookup"><span data-stu-id="e98f1-151">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="e98f1-152">Subsitute w powitania po implementacji **aplikacji: didRegisterForRemoteNotificationsWithDeviceToken** tootake hello scenorysu zmiany interfejsu użytkownika do konta:</span><span class="sxs-lookup"><span data-stu-id="e98f1-152">Subsitute in hello following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** tootake hello storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="e98f1-153">Następnie należy dodać następujące metody zbyt hello**AppDelegate.m** tooretrieve hello obrazu z punktu końcowego i wysyłania powiadomień lokalnego, po ukończeniu pobierania.</span><span class="sxs-lookup"><span data-stu-id="e98f1-153">Then, add hello following methods too**AppDelegate.m** tooretrieve hello image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="e98f1-154">Upewnij się, że symbol zastępczy hello toosubstitute `{backend endpoint}` z wewnętrznej bazy danych punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="e98f1-154">Make sure toosubstitute hello placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
3. <span data-ttu-id="e98f1-155">Obsługi powiadamiania lokalne powitania powyżej otwierając kontrolera widoku obraz powitania w **AppDelegate.m** z hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="e98f1-155">Handle hello local notification above by opening up hello image view controller in **AppDelegate.m** with hello following methods:</span></span>
   
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

## <a name="run-hello-application"></a><span data-ttu-id="e98f1-156">Uruchom hello aplikacji</span><span class="sxs-lookup"><span data-stu-id="e98f1-156">Run hello Application</span></span>
1. <span data-ttu-id="e98f1-157">W programie XCode uruchamianie aplikacji hello na urządzenie fizyczne z systemem iOS (push, które nie będą działać powiadomienia w symulatorze hello).</span><span class="sxs-lookup"><span data-stu-id="e98f1-157">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="e98f1-158">W aplikacji dla systemu iOS hello interfejsu użytkownika, wprowadź nazwę użytkownika i hasło hello takie same wartości dla uwierzytelniania i kliknij przycisk **dziennika w**.</span><span class="sxs-lookup"><span data-stu-id="e98f1-158">In hello iOS app UI, enter a username and password of hello same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="e98f1-159">Kliknij przycisk **wysyłania wypychania** i powinien zostać wyświetlony alert w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e98f1-159">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="e98f1-160">Po kliknięciu **więcej**, można wprowadzić toohello obrazu wybrano tooinclude w zapleczu swojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e98f1-160">If you click on **More**, you will be brought toohello image you chose tooinclude in your app backend.</span></span>
4. <span data-ttu-id="e98f1-161">Możesz również kliknąć **wysyłania wypychania** i natychmiast naciśnij przycisk Strona główna hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="e98f1-161">You can also click **Send push** and immediately press hello home button of your device.</span></span> <span data-ttu-id="e98f1-162">Za chwilę otrzymasz powiadomienie wypychane.</span><span class="sxs-lookup"><span data-stu-id="e98f1-162">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="e98f1-163">Wybierz na niej, lub kliknij przycisk więcej, zostanie wyświetlona zawartość sformatowanego obrazu i aplikacji hello tooyour.</span><span class="sxs-lookup"><span data-stu-id="e98f1-163">If you tap on it or click More, you will be brought tooyour app and hello rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
