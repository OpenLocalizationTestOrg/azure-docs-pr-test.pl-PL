---
title: Azure Notification Hubs bezpiecznego Push
description: "Dowiedz się, jak wysyłać powiadomienia wypychane bezpieczny do aplikacji systemu iOS z platformy Azure. Przykłady kodu napisane w języku Objective C i C#."
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
ms.openlocfilehash: e5f09fb3716303bb21fe7442aa6fa8832174838e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="262f3-104">Azure Notification Hubs bezpiecznego Push</span><span class="sxs-lookup"><span data-stu-id="262f3-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="262f3-105">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="262f3-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="262f3-106">iOS</span><span class="sxs-lookup"><span data-stu-id="262f3-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="262f3-107">Android</span><span class="sxs-lookup"><span data-stu-id="262f3-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="262f3-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="262f3-108">Overview</span></span>
<span data-ttu-id="262f3-109">Obsługa powiadomień wypychanych w Microsoft Azure pozwala uzyskiwać dostęp do infrastruktury wypychania łatwy w użyciu, wieloplatformową skalowalnych w poziomie, co znacznie upraszcza implementacji powiadomienia wypychane dla aplikacji zarówno konsumenckie i korporacyjne dla platform urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="262f3-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="262f3-110">Z powodu przepisami ograniczeń dotyczących zabezpieczeń, czasami aplikacji może mają zostać uwzględnione coś w powiadomienie, które nie są przesyłane za pośrednictwem infrastruktury powiadomień wypychanych standardowa.</span><span class="sxs-lookup"><span data-stu-id="262f3-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="262f3-111">Ten przewodnik opisuje sposób do osiągnięcia w tym samym środowisku, wysyłając informacje poufne za pośrednictwem bezpiecznego uwierzytelnionego połączenia od urządzeń klienckich i zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="262f3-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="262f3-112">Na wysokim poziomie przepływ wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="262f3-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="262f3-113">Zaplecza aplikacji:</span><span class="sxs-lookup"><span data-stu-id="262f3-113">The app back-end:</span></span>
   * <span data-ttu-id="262f3-114">Magazyny bezpiecznego ładunku w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="262f3-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="262f3-115">Wysyła identyfikator tego powiadomienia do urządzenia (nie informacji o są wysyłane).</span><span class="sxs-lookup"><span data-stu-id="262f3-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="262f3-116">Aplikacją na urządzeniu, podczas odbierania powiadomienia:</span><span class="sxs-lookup"><span data-stu-id="262f3-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="262f3-117">Urządzenie kontaktuje się z zaplecza żąda bezpiecznego ładunku.</span><span class="sxs-lookup"><span data-stu-id="262f3-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="262f3-118">Aplikację można wyświetlić ładunku jako powiadomienie na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="262f3-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="262f3-119">Należy pamiętać, że w poprzednim przepływu (i w tym samouczku) przyjęto założenie, że urządzenia są przechowywane token uwierzytelniania w magazynie lokalnym, po zalogowaniu się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="262f3-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="262f3-120">Gwarantuje to całkowicie nie zakłóca pracy, jak urządzenia mogą pobierać ładunku bezpiecznego powiadomienia za pomocą tego tokenu.</span><span class="sxs-lookup"><span data-stu-id="262f3-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="262f3-121">Jeśli aplikacja nie przechowuje tokeny uwierzytelniania na urządzeniu lub tokeny te mogą wygasnąć, aplikacji urządzenia, po otrzymaniu powiadomienia powinien być wyświetlany ogólny powiadomienie monitowania użytkownika do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="262f3-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="262f3-122">Następnie aplikacja uwierzytelnia użytkownika i zawiera ładunek powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="262f3-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="262f3-123">W tym samouczku Secure wypychania pokazano, jak bezpiecznie wysyłać powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="262f3-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="262f3-124">Samouczek opiera się na [Powiadom użytkowników](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczku, dlatego należy wykonać kroki tego samouczka najpierw.</span><span class="sxs-lookup"><span data-stu-id="262f3-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="262f3-125">Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="262f3-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-ios-project"></a><span data-ttu-id="262f3-126">Zmodyfikuj projekt dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="262f3-126">Modify the iOS project</span></span>
<span data-ttu-id="262f3-127">Teraz, aby modyfikować Twojej aplikacji zaplecza wysłać tylko *identyfikator* powiadomienia, należy zmienić aplikacji systemu iOS w celu obsługi tego powiadomienia i wywołania zwrotnego z zaplecza można pobrać zabezpieczoną wiadomość, który będzie wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="262f3-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>

<span data-ttu-id="262f3-128">Na osiągnięcie tego celu, musimy pisanie logiki można pobrać zawartości bezpiecznej z zaplecza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="262f3-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span></span>

1. <span data-ttu-id="262f3-129">W **AppDelegate.m**, upewnij się, że aplikacja rejestruje dyskretnej powiadomień, przetwarza identyfikator powiadomień wysyłanych z wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="262f3-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span></span> <span data-ttu-id="262f3-130">Dodaj **UIRemoteNotificationTypeNewsstandContentAvailability** opcji w didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="262f3-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="262f3-131">W Twojej **AppDelegate.m** Dodaj sekcji implementacji u góry z deklaracją następujące:</span><span class="sxs-lookup"><span data-stu-id="262f3-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="262f3-132">Następnie dodaj w sekcji implementacji następujący kod, zastępując symbol zastępczy `{back-end endpoint}` z poziomu zaplecza uzyskany wcześniej punktu końcowego:</span><span class="sxs-lookup"><span data-stu-id="262f3-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span></span>

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

    This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences.

1. <span data-ttu-id="262f3-133">Teraz musimy obsługi przychodzących powiadomień i pobrać zawartość do wyświetlenia przy użyciu metody powyżej.</span><span class="sxs-lookup"><span data-stu-id="262f3-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span></span> <span data-ttu-id="262f3-134">Najpierw musimy włączyć uruchomione w tle podczas odbierania powiadomień wypychanych w aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="262f3-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span></span> <span data-ttu-id="262f3-135">W **XCode**, wybierz projekt aplikacji w lewym panelu, a następnie kliknij urządzenie docelowe głównej aplikacji w **cele** sekcji w okienku centralnym.</span><span class="sxs-lookup"><span data-stu-id="262f3-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span></span>
2. <span data-ttu-id="262f3-136">Następnie kliknij przycisk z **możliwości** w górnej części okienka centralnej i sprawdź **zdalnego powiadomienia** wyboru.</span><span class="sxs-lookup"><span data-stu-id="262f3-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="262f3-137">W **AppDelegate.m** Dodaj następującą metodę do obsługi powiadomień wypychanych:</span><span class="sxs-lookup"><span data-stu-id="262f3-137">In **AppDelegate.m** add the following method to handle push notifications:</span></span>
   
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
   
    <span data-ttu-id="262f3-138">Należy pamiętać, że preferowane do obsługi przypadków brakujących właściwości nagłówka uwierzytelniania lub odrzucenia przez zaplecza.</span><span class="sxs-lookup"><span data-stu-id="262f3-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="262f3-139">Obsługę określonych przypadkach zależą od większości użytkowników docelowych.</span><span class="sxs-lookup"><span data-stu-id="262f3-139">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="262f3-140">Jedną z opcji jest powiadomienia z monitem ogólnego dla użytkownika do uwierzytelniania można pobrać rzeczywiste powiadomienia mają być wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="262f3-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="262f3-141">Uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="262f3-141">Run the Application</span></span>
<span data-ttu-id="262f3-142">Aby uruchomić aplikację, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="262f3-142">To run the application, do the following:</span></span>

1. <span data-ttu-id="262f3-143">W programie XCode Uruchom aplikację na urządzenie fizyczne z systemem iOS (wypychanie powiadomień nie będzie działać w symulatorze).</span><span class="sxs-lookup"><span data-stu-id="262f3-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="262f3-144">W aplikacji systemu iOS interfejsu użytkownika wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="262f3-144">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="262f3-145">Mogą to być dowolny ciąg, ale muszą one mieć taką samą wartość.</span><span class="sxs-lookup"><span data-stu-id="262f3-145">These can be any string, but they must be the same value.</span></span>
3. <span data-ttu-id="262f3-146">W aplikacji systemu iOS interfejsu użytkownika, kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="262f3-146">In the iOS app UI, click **Log in**.</span></span> <span data-ttu-id="262f3-147">Następnie kliknij przycisk **wysyłania wypychania**.</span><span class="sxs-lookup"><span data-stu-id="262f3-147">Then click **Send push**.</span></span> <span data-ttu-id="262f3-148">Powinny pojawić się bezpiecznego powiadomienia są wyświetlane w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="262f3-148">You should see the secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
