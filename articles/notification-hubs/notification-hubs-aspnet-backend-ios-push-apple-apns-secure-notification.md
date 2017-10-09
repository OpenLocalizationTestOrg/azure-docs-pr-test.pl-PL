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
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="4ccda-104">Azure Notification Hubs bezpiecznego Push</span><span class="sxs-lookup"><span data-stu-id="4ccda-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ccda-105">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="4ccda-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="4ccda-106">iOS</span><span class="sxs-lookup"><span data-stu-id="4ccda-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="4ccda-107">Android</span><span class="sxs-lookup"><span data-stu-id="4ccda-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="4ccda-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4ccda-108">Overview</span></span>
<span data-ttu-id="4ccda-109">Obsługa powiadomień wypychanych w Microsoft Azure umożliwia tooaccess infrastruktury wypychania łatwy w użyciu, wieloplatformową skalowalnych w poziomie, który jest znacznie ułatwione hello stosowania powiadomienia wypychane zarówno konsumenckie i korporacyjne aplikacji dla urządzeń przenośnych platform.</span><span class="sxs-lookup"><span data-stu-id="4ccda-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="4ccda-110">Czasami ze względu na ograniczenia tooregulatory lub zabezpieczeń, aplikacja może być tooinclude coś w hello powiadomienie, które nie są przesyłane za pośrednictwem infrastruktury powiadomień wypychanych standardowe hello.</span><span class="sxs-lookup"><span data-stu-id="4ccda-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="4ccda-111">W tym samouczku opisano, jak tooachieve hello tego samego środowiska poprzez wysłanie poufnych informacji za pośrednictwem bezpiecznego połączenia uwierzytelnionego między powitania klienta urządzenia i aplikacji hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4ccda-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="4ccda-112">Na wysokim poziomie przepływu hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="4ccda-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="4ccda-113">Witaj zaplecze aplikacji:</span><span class="sxs-lookup"><span data-stu-id="4ccda-113">hello app back-end:</span></span>
   * <span data-ttu-id="4ccda-114">Magazyny bezpiecznego ładunku w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="4ccda-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="4ccda-115">Wysyła identyfikator hello tego urządzenia toohello powiadomienie (nie bezpiecznego informacje są wysyłane).</span><span class="sxs-lookup"><span data-stu-id="4ccda-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="4ccda-116">Aplikacja Hello na urządzeniu hello podczas odbierania powiadomień hello:</span><span class="sxs-lookup"><span data-stu-id="4ccda-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="4ccda-117">urządzenie Hello kontaktuje się hello zaplecza żądania hello bezpiecznego ładunku.</span><span class="sxs-lookup"><span data-stu-id="4ccda-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="4ccda-118">Aplikacja Hello można wyświetlić ładunku hello jako powiadomienie na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="4ccda-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="4ccda-119">Jest ważne toonote, że w hello poprzedzających przepływu (i w tym samouczku) przyjęto założenie, urządzenia hello po zalogowaniu użytkownika hello przechowuje token uwierzytelniania w magazynie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="4ccda-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="4ccda-120">Gwarantuje to całkowicie sprawnie, jak urządzenia hello mogą pobierać ładunku bezpiecznego hello powiadomienia za pomocą tego tokenu.</span><span class="sxs-lookup"><span data-stu-id="4ccda-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="4ccda-121">Jeśli aplikacja nie przechowuje tokeny uwierzytelniania na urządzeniu hello lub tokeny te mogą wygasnąć, hello aplikacji urządzenia po otrzymaniu powiadomienia hello powinien być wyświetlany ogólny powiadomienie aplikacji hello toolaunch użytkownika hello monitowania.</span><span class="sxs-lookup"><span data-stu-id="4ccda-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="4ccda-122">Aplikacja Hello następnie uwierzytelnia użytkownika hello i zawiera ładunek powiadomienia hello.</span><span class="sxs-lookup"><span data-stu-id="4ccda-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="4ccda-123">W tym samouczku Secure wypychania przedstawiono sposób toosend powiadomienie wypychane bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="4ccda-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="4ccda-124">Samouczek Hello opiera się na powitania [Powiadom użytkowników](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczku, dlatego należy wykonać kroki hello w tym samouczku najpierw.</span><span class="sxs-lookup"><span data-stu-id="4ccda-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="4ccda-125">Ten samouczek zakłada, że utworzony i skonfigurowany Centrum powiadomień, zgodnie z opisem w [wprowadzenie do korzystania z usługi Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4ccda-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a><span data-ttu-id="4ccda-126">Modyfikowanie hello projekt dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="4ccda-126">Modify hello iOS project</span></span>
<span data-ttu-id="4ccda-127">Teraz, aby modyfikować tylko aplikacji hello w toosend zaplecza *identyfikator* powiadomienia, masz toochange Twojego toohandle aplikacji systemu iOS, czy powiadomień i wywołanie zwrotne użytkownika hello tooretrieve zaplecza secure toobe komunikat wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="4ccda-127">Now that you modified your app back-end toosend just hello *id* of a notification, you have toochange your iOS app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>

<span data-ttu-id="4ccda-128">tooachieve tego celu mamy toowrite hello logiki tooretrieve hello bezpieczne zawartości z hello zaplecze aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4ccda-128">tooachieve this goal, we have toowrite hello logic tooretrieve hello secure content from hello app back-end.</span></span>

1. <span data-ttu-id="4ccda-129">W **AppDelegate.m**, upewnij się, że rejestruje powiadomienia dyskretnej aplikacji hello tak przetwarza hello identyfikator powiadomień wysyłanych z hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4ccda-129">In **AppDelegate.m**, make sure hello app registers for silent notifications so it processes hello notification id sent from hello backend.</span></span> <span data-ttu-id="4ccda-130">Dodaj hello **UIRemoteNotificationTypeNewsstandContentAvailability** opcji w didFinishLaunchingWithOptions:</span><span class="sxs-lookup"><span data-stu-id="4ccda-130">Add hello **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="4ccda-131">W Twojej **AppDelegate.m** Dodaj sekcji implementacji u góry hello z powitania po deklaracji:</span><span class="sxs-lookup"><span data-stu-id="4ccda-131">In your **AppDelegate.m** add an implementation section at hello top with hello following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="4ccda-132">Następnie dodaj w hello hello sekcji implementacja po kod, zastępując hello symbolu zastępczego `{back-end endpoint}` z punktem końcowym hello na danym zapleczu uzyskany wcześniej:</span><span class="sxs-lookup"><span data-stu-id="4ccda-132">Then add in hello implementation section hello following code, substituting hello placeholder `{back-end endpoint}` with hello endpoint for your back-end obtained previously:</span></span>

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

1. <span data-ttu-id="4ccda-133">Teraz możemy mają toohandle hello przychodzące powiadomienia i użyj metody hello powyżej toodisplay zawartości hello tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="4ccda-133">Now we have toohandle hello incoming notification and use hello method above tooretrieve hello content toodisplay.</span></span> <span data-ttu-id="4ccda-134">Po pierwsze mamy tooenable Twojego toorun aplikacji systemu iOS w tle hello podczas odbierania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="4ccda-134">First, we have tooenable your iOS app toorun in hello background when receiving a push notification.</span></span> <span data-ttu-id="4ccda-135">W **XCode**, wybierz projekt aplikacji hello lewym panelu, a następnie kliknij urządzenie docelowe głównej aplikacji w hello **cele** sekcji w okienku centralnym hello.</span><span class="sxs-lookup"><span data-stu-id="4ccda-135">In **XCode**, select your app project on hello left panel, then click your main app target in hello **Targets** section from hello central pane.</span></span>
2. <span data-ttu-id="4ccda-136">Następnie kliknij przycisk z **możliwości** u góry hello okienka centralnej i sprawdź hello **zdalnego powiadomienia** wyboru.</span><span class="sxs-lookup"><span data-stu-id="4ccda-136">Then click your **Capabilities** tab at hello top of your central pane, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="4ccda-137">W **AppDelegate.m** dodać hello następujące powiadomienia wypychane toohandle — metoda:</span><span class="sxs-lookup"><span data-stu-id="4ccda-137">In **AppDelegate.m** add hello following method toohandle push notifications:</span></span>
   
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
   
    <span data-ttu-id="4ccda-138">Należy pamiętać, że preferowane toohandle hello przypadków brakujących właściwości nagłówka uwierzytelniania lub odrzucenia przez hello zaplecza.</span><span class="sxs-lookup"><span data-stu-id="4ccda-138">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="4ccda-139">Obsługa określonego Hello powyższych przypadkach zależą od przede wszystkim użytkowników docelowych.</span><span class="sxs-lookup"><span data-stu-id="4ccda-139">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="4ccda-140">Jedną z opcji jest toodisplay powiadomienie z wierszem ogólnego hello użytkownika tooauthenticate tooretrieve hello rzeczywiste powiadomienia o.</span><span class="sxs-lookup"><span data-stu-id="4ccda-140">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="4ccda-141">Uruchom hello aplikacji</span><span class="sxs-lookup"><span data-stu-id="4ccda-141">Run hello Application</span></span>
<span data-ttu-id="4ccda-142">toorun hello aplikacji, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="4ccda-142">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="4ccda-143">W programie XCode uruchamianie aplikacji hello na urządzenie fizyczne z systemem iOS (push, które nie będą działać powiadomienia w symulatorze hello).</span><span class="sxs-lookup"><span data-stu-id="4ccda-143">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="4ccda-144">W aplikacji dla systemu iOS hello interfejsu użytkownika wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="4ccda-144">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="4ccda-145">Mogą to być dowolny ciąg, ale muszą one być hello tę samą wartość.</span><span class="sxs-lookup"><span data-stu-id="4ccda-145">These can be any string, but they must be hello same value.</span></span>
3. <span data-ttu-id="4ccda-146">W aplikacji dla systemu iOS hello interfejsu użytkownika, kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="4ccda-146">In hello iOS app UI, click **Log in**.</span></span> <span data-ttu-id="4ccda-147">Następnie kliknij przycisk **wysyłania wypychania**.</span><span class="sxs-lookup"><span data-stu-id="4ccda-147">Then click **Send push**.</span></span> <span data-ttu-id="4ccda-148">Powinny pojawić się powiadomienie bezpiecznego hello będzie wyświetlany w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="4ccda-148">You should see hello secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
