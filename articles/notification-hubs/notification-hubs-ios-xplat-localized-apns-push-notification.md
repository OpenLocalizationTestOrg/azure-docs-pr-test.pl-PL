---
title: "aaaNotification koncentratory zlokalizowane fundamentalne wiadomości samouczek dla systemu iOS"
description: "Dowiedz się, jak toosend usługi centra powiadomień Azure Service Bus toouse zlokalizowane powiadomienia o najważniejszych wiadomościach (iOS)."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a><span data-ttu-id="ff760-103">Używanie urządzeń tooiOS wiadomości podziału toosend zlokalizowane centra powiadomień</span><span class="sxs-lookup"><span data-stu-id="ff760-103">Use Notification Hubs toosend localized breaking news tooiOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff760-104">Sklep Windows C#</span><span class="sxs-lookup"><span data-stu-id="ff760-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="ff760-105">iOS</span><span class="sxs-lookup"><span data-stu-id="ff760-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ff760-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ff760-106">Overview</span></span>
<span data-ttu-id="ff760-107">W tym temacie opisano sposób toouse hello [szablony](notification-hubs-templates-cross-platform-push-messages.md) funkcji usługi Azure Notification Hubs toobroadcast fundamentalne powiadomień wiadomości, które zostały zlokalizowane według języka i urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ff760-107">This topic shows you how toouse hello [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="ff760-108">W tym samouczku początkowo utworzony w aplikacji dla systemu iOS hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości].</span><span class="sxs-lookup"><span data-stu-id="ff760-108">In this tutorial you start with hello iOS app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="ff760-109">Po zakończeniu będziesz w stanie tooregister dla kategorii, które planuje się, określ język w powiadomienia, które hello tooreceive i otrzymywać tylko powiadomienia wypychane dla kategorii hello wybrany w tym języku.</span><span class="sxs-lookup"><span data-stu-id="ff760-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="ff760-110">Istnieją dwie części toothis scenariusza:</span><span class="sxs-lookup"><span data-stu-id="ff760-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="ff760-111">Aplikacja systemu iOS umożliwia klienta toospecify urządzeń język i toodifferent toosubscribe fundamentalne kategorie nowości;</span><span class="sxs-lookup"><span data-stu-id="ff760-111">iOS app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="ff760-112">Witaj zaplecza emituje hello powiadomień, przy użyciu hello **tag** i **szablonu** feautres usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="ff760-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff760-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ff760-113">Prerequisites</span></span>
<span data-ttu-id="ff760-114">Należy zostały już wykonane hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] samouczka i mieć kod hello jest dostępne, ponieważ w tym samouczku bezpośrednio oparta na kod.</span><span class="sxs-lookup"><span data-stu-id="ff760-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="ff760-115">Visual Studio 2012 lub nowszy jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="ff760-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="ff760-116">Pojęcia dotyczące szablonów</span><span class="sxs-lookup"><span data-stu-id="ff760-116">Template concepts</span></span>
<span data-ttu-id="ff760-117">W [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] utworzono aplikację, która jest używana **tagi** toonotifications toosubscribe dla różnych grup dyskusyjnych kategorii.</span><span class="sxs-lookup"><span data-stu-id="ff760-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="ff760-118">Wiele aplikacji, jednak docelowy kilku rynkach i wymagają lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="ff760-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="ff760-119">Oznacza to, czy zawartość hello hello powiadomień, się toobe zlokalizowane i dostarczonego toohello Popraw zbiór urządzeń.</span><span class="sxs-lookup"><span data-stu-id="ff760-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="ff760-120">W tym temacie pokazano, jak toouse hello **szablonu** funkcji tooeasily świadczenia usługi Notification Hubs zlokalizowane powiadomienia o najważniejszych wiadomościach.</span><span class="sxs-lookup"><span data-stu-id="ff760-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="ff760-121">Uwaga: jednokierunkowej toosend zlokalizowane powiadomień jest toocreate wiele wersji każdego znacznika.</span><span class="sxs-lookup"><span data-stu-id="ff760-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="ff760-122">Na przykład toosupport angielskim, francuskim i mandaryński, potrzebujemy czy trzy różne znaczniki dla wiadomości world: "world_en", "world_fr" i "world_ch".</span><span class="sxs-lookup"><span data-stu-id="ff760-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="ff760-123">Firma Microsoft będzie zmuszony toosend zlokalizowanej wersji hello world wiadomości tooeach tych tagów.</span><span class="sxs-lookup"><span data-stu-id="ff760-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="ff760-124">W tym temacie używamy szablony tooavoid hello mnożenie tagów i wymagania hello wielu operacji wysyłania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ff760-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="ff760-125">Na wysokim poziomie, szablony są toospecify sposób jak określonym urządzeniu powinno zostać odebrane powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="ff760-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="ff760-126">Szablon Hello Określa format ładunku dokładne hello odwołując tooproperties, które są częścią hello wiadomość wysłana przez zaplecze Twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ff760-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="ff760-127">W tym przypadku firma Microsoft wyśle komunikat niezależny od ustawień regionalnych zawierający wszystkie obsługiwane języki:</span><span class="sxs-lookup"><span data-stu-id="ff760-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="ff760-128">Następnie firma Microsoft zapewnia Zarejestruj szablon, który odwołuje się właściwość poprawne toohello przez urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ff760-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="ff760-129">Na przykład aplikację systemu iOS, która potrzebuje tooregister dla wiadomości francuskim zarejestruje hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="ff760-129">For instance,  an iOS app that wants tooregister for French news will register hello following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="ff760-130">Szablony są bardzo przydatna funkcja, możesz dowiedzieć się więcej w naszym [szablony](notification-hubs-templates-cross-platform-push-messages.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ff760-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="hello-app-user-interface"></a><span data-ttu-id="ff760-131">Interfejs użytkownika aplikacji Hello</span><span class="sxs-lookup"><span data-stu-id="ff760-131">hello app user interface</span></span>
<span data-ttu-id="ff760-132">Firma Microsoft będzie teraz zmodyfikować aplikacji fundamentalne wiadomości powitania, utworzonego w temacie hello [toosend użyciu usługi Notification Hubs fundamentalne wiadomości] toosend zlokalizowane najważniejszych wiadomości przy użyciu szablonów.</span><span class="sxs-lookup"><span data-stu-id="ff760-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="ff760-133">W Twojej MainStoryboard_iPhone.storyboard dodać kontrolkę segmentu z językami hello trzech, które firma Microsoft będzie obsługiwać: angielski, francuski i mandaryński.</span><span class="sxs-lookup"><span data-stu-id="ff760-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with hello three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="ff760-134">Następnie upewnij się, że tooadd IBOutlet w Twojej ViewController.h w sposób przedstawiony poniżej:</span><span class="sxs-lookup"><span data-stu-id="ff760-134">Then make sure tooadd an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-hello-ios-app"></a><span data-ttu-id="ff760-135">IOS — aplikacja hello kompilowanie</span><span class="sxs-lookup"><span data-stu-id="ff760-135">Building hello iOS app</span></span>
1. <span data-ttu-id="ff760-136">W Twojej Notification.h dodać hello *retrieveLocale* metody i zmodyfikować hello magazynu oraz subskrybowania metody, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="ff760-136">In your Notification.h add hello *retrieveLocale* method, and modify hello store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="ff760-137">W Twojej Notification.m zmodyfikować hello *storeCategoriesAndSubscribe* metody, dodając parametr ustawień regionalnych hello i przechowywanie ich w ustawieniach domyślnych użytkownika hello:</span><span class="sxs-lookup"><span data-stu-id="ff760-137">In your Notification.m, modify hello *storeCategoriesAndSubscribe* method, by adding hello locale parameter and storing it in hello user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="ff760-138">Następnie zmodyfikuj hello *subskrypcji* ustawień regionalnych hello tooinclude metody:</span><span class="sxs-lookup"><span data-stu-id="ff760-138">Then modify hello *subscribe* method tooinclude hello locale:</span></span>
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    <span data-ttu-id="ff760-139">Należy zwrócić uwagę, jak teraz użyto metody hello *registerTemplateWithDeviceToken*, zamiast *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="ff760-139">Note how we are now using hello method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="ff760-140">Gdy firma Microsoft rejestrowania dla szablonu mamy tooprovide hello json szablonu, a także nazwę dla szablonu hello (zgodnie z naszej aplikacji może być tooregister różnych szablonów).</span><span class="sxs-lookup"><span data-stu-id="ff760-140">When we register for a template we have tooprovide hello json template and also a name for hello template (as our app might want tooregister different templates).</span></span> <span data-ttu-id="ff760-141">Upewnij się, że tooregister kategorie jako tagi, zgodnie z chcemy się notifciations hello tooreceive toomake dla tych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ff760-141">Make sure tooregister your categories as tags, as we want toomake sure tooreceive hello notifciations for those news.</span></span>
   
    <span data-ttu-id="ff760-142">Dodaj ustawień regionalnych hello tooretrieve metody w ustawieniach domyślnych użytkownika hello:</span><span class="sxs-lookup"><span data-stu-id="ff760-142">Add a method tooretrieve hello locale from hello user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="ff760-143">Teraz, gdy firma Microsoft zmodyfikowane klasy Nasze powiadomienia, mamy toomake się upewnić, że nasze ViewController sprawia, że użycie hello UISegmentControl nowe.</span><span class="sxs-lookup"><span data-stu-id="ff760-143">Now that we modified our Notifications class, we have toomake sure that our ViewController makes use of hello new UISegmentControl.</span></span> <span data-ttu-id="ff760-144">Dodaj powitania po wierszu hello *viewDidLoad* metody toomake czy tooshow hello ustawień regionalnych aktualnie wybranego:</span><span class="sxs-lookup"><span data-stu-id="ff760-144">Add hello following line in hello *viewDidLoad* method toomake sure tooshow hello locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="ff760-145">Następnie w Twojej *subskrypcji* metody, zmień Twoje toohello wywołania *storeCategoriesAndSubscribe* toohello następujące:</span><span class="sxs-lookup"><span data-stu-id="ff760-145">Then, in your *subscribe* method, change your call toohello *storeCategoriesAndSubscribe* toohello following:</span></span>
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. <span data-ttu-id="ff760-146">Na koniec masz tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* w Twojej AppDelegate.m metody, dzięki czemu można poprawnie odświeżyć rejestracji podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ff760-146">Finally, you have tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="ff760-147">Zmień toohello Twojego wywołania *subskrypcji* metody powiadomienia przy użyciu następujących hello:</span><span class="sxs-lookup"><span data-stu-id="ff760-147">Change your call toohello *subscribe* method of notifications with hello following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="ff760-148">(opcjonalnie) Wysyłanie powiadomień zlokalizowanego szablonu z aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="ff760-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a><span data-ttu-id="ff760-149">(opcjonalnie) Wysyłanie powiadomień zlokalizowanego szablonu z hello urządzenia</span><span class="sxs-lookup"><span data-stu-id="ff760-149">(optional) Send localized template notifications from hello device</span></span>
<span data-ttu-id="ff760-150">Jeśli nie masz dostępu tooVisual w Studio lub mają testu toojust wysyłanie powiadomień szablonu hello zlokalizowane bezpośrednio z aplikacji hello hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ff760-150">If you don't have access tooVisual Studio, or want toojust test sending hello localized template notifications directly from hello app on hello device.</span></span>  <span data-ttu-id="ff760-151">Można w prosty dodać toohello parametry szablonu hello zlokalizowane `SendNotificationRESTAPI` metody zdefiniowanej w samouczku poprzedniej hello.</span><span class="sxs-lookup"><span data-stu-id="ff760-151">You can simple add hello localized template parameters toohello `SendNotificationRESTAPI` method you defined in hello previous tutorial.</span></span>

        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];

            NSString *json;

            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];

            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];

            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];

            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];

            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];

            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];

            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];

            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];

            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];

            [dataTask resume];
        }




## <a name="next-steps"></a><span data-ttu-id="ff760-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff760-152">Next Steps</span></span>
<span data-ttu-id="ff760-153">Aby uzyskać więcej informacji na temat używania szablonów zobacz:</span><span class="sxs-lookup"><span data-stu-id="ff760-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="ff760-154">[Powiadom użytkowników z usługą Notification Hubs: ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="ff760-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="ff760-155">[Powiadom użytkowników z usługą Notification Hubs: Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="ff760-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Powiadom użytkowników z usługą Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Powiadom użytkowników z usługą Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
