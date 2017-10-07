---
title: "aaaNotification koncentratory fundamentalne wiadomości Samouczek — systemu iOS"
description: "Dowiedz się, jak toosend usługi centra powiadomień Azure Service Bus toouse fundamentalne urządzeń tooiOS powiadomień wiadomości."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="3abba-103">Użyj usługi Notification Hubs toosend fundamentalne wiadomości</span><span class="sxs-lookup"><span data-stu-id="3abba-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="3abba-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3abba-104">Overview</span></span>
<span data-ttu-id="3abba-105">W tym temacie opisano sposób toouse usługi Azure Notification Hubs toobroadcast najważniejszych wiadomości powiadomienia tooan iOS aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3abba-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan iOS app.</span></span> <span data-ttu-id="3abba-106">Po zakończeniu będzie być może tooregister zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="3abba-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="3abba-107">Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, w której powiadomienia mają toogroups toobe wysyłane użytkowników, które wcześniej zostały zadeklarowane zainteresowanie je, np. czytnik danych RSS, aplikacje wentylatory utworów muzycznych itp.</span><span class="sxs-lookup"><span data-stu-id="3abba-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="3abba-108">Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="3abba-109">Gdy tooa tag wysyłane są powiadomienia, wszystkie urządzenia, które zostały zarejestrowane dla tagu hello będzie wysyłane powiadomienie hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="3abba-110">Ponieważ tagi są po prostu ciągów, nie mają toobe udostępnione wcześniej.</span><span class="sxs-lookup"><span data-stu-id="3abba-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="3abba-111">Aby uzyskać więcej informacji na temat tagów, zobacz zbyt[routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="3abba-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3abba-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3abba-112">Prerequisites</span></span>
<span data-ttu-id="3abba-113">W tym temacie opiera się na aplikacji hello utworzony w [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="3abba-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="3abba-114">Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="3abba-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="3abba-115">Dodaj aplikację toohello wybór kategorii</span><span class="sxs-lookup"><span data-stu-id="3abba-115">Add category selection toohello app</span></span>
<span data-ttu-id="3abba-116">pierwszym krokiem Hello jest tooadd hello interfejsu użytkownika elementy tooyour istniejących scenorysu umożliwiające hello użytkownika tooselect kategorii tooregister.</span><span class="sxs-lookup"><span data-stu-id="3abba-116">hello first step is tooadd hello UI elements tooyour existing storyboard that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="3abba-117">Witaj kategorie wybrane przez użytkownika są przechowywane na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="3abba-118">Po uruchomieniu aplikacji hello rejestracji urządzenia jest tworzony w Centrum powiadomień z kategorii hello wybrany jako znaczniki.</span><span class="sxs-lookup"><span data-stu-id="3abba-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="3abba-119">W Twojej MainStoryboard_iPhone.storyboard Dodaj hello poniższych składników z biblioteki obiektów hello:</span><span class="sxs-lookup"><span data-stu-id="3abba-119">In your MainStoryboard_iPhone.storyboard add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="3abba-120">Etykiety z tekstem "Krytyczne wiadomości"</span><span class="sxs-lookup"><span data-stu-id="3abba-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="3abba-121">Etykiety z teksty kategorii "World", "Polityka", "Business", "Technologii", "Nauki", "Sport",</span><span class="sxs-lookup"><span data-stu-id="3abba-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="3abba-122">Sześć przełączników, jeden dla każdej kategorii, ustaw każdy przełącznik **stanu** toobe **poza** domyślnie.</span><span class="sxs-lookup"><span data-stu-id="3abba-122">Six switches, one per category, set each switch **State** toobe **Off** by default.</span></span>
   * <span data-ttu-id="3abba-123">Jeden z przycisków z etykietą "Subskrybuj"</span><span class="sxs-lookup"><span data-stu-id="3abba-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="3abba-124">Twoje scenorysu powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="3abba-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="3abba-125">W edytorze Asystenta hello utworzyć gniazda dla wszystkich przełączników hello i połączeń telefonicznych z nimi "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span><span class="sxs-lookup"><span data-stu-id="3abba-125">In hello assistant editor, create outlets for all hello switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="3abba-126">Utwórz działanie dla przycisk o nazwie "subskrypcji".</span><span class="sxs-lookup"><span data-stu-id="3abba-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="3abba-127">Twoje ViewController.h powinien zawierać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="3abba-127">Your ViewController.h should contain hello following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="3abba-128">Utwórz nową **klasy Touch Cocoa** o nazwie `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="3abba-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="3abba-129">Skopiuj hello następującego kodu w sekcji interfejsu hello hello pliku Notifications.h:</span><span class="sxs-lookup"><span data-stu-id="3abba-129">Copy hello following code in hello interface section of hello file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="3abba-130">Dodaj powitania po tooNotifications.m dyrektywy importu:</span><span class="sxs-lookup"><span data-stu-id="3abba-130">Add hello following import directive tooNotifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="3abba-131">Skopiuj hello następującego kodu w sekcji implementacji hello hello pliku Notifications.m.</span><span class="sxs-lookup"><span data-stu-id="3abba-131">Copy hello following code in hello implementation section of hello file Notifications.m.</span></span>
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    <span data-ttu-id="3abba-132">Ta klasa korzysta z lokalnej pamięci masowej toostore i pobrać kategorii hello wiadomości, który otrzyma tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3abba-132">This class uses local storage toostore and retrieve hello categories of news that this device will receive.</span></span> <span data-ttu-id="3abba-133">Ponadto zawiera tooregister metody, dla tych kategorii przy użyciu [szablonu](notification-hubs-templates-cross-platform-push-messages.md) rejestracji.</span><span class="sxs-lookup"><span data-stu-id="3abba-133">Also, it contains a method tooregister for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="3abba-134">W pliku AppDelegate.h hello Dodaj instrukcję import Notifications.h i dodawania właściwości dla wystąpienia hello klasy powiadomień:</span><span class="sxs-lookup"><span data-stu-id="3abba-134">In hello AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of hello Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="3abba-135">W hello **didFinishLaunchingWithOptions** metody w AppDelegate.m, Dodaj hello kodu tooinitialize hello powiadomienia wystąpienia na początku hello hello metody.</span><span class="sxs-lookup"><span data-stu-id="3abba-135">In hello **didFinishLaunchingWithOptions** method in AppDelegate.m, add hello code tooinitialize hello notifications instance at hello beginning of hello method.</span></span>  
   
    <span data-ttu-id="3abba-136">`HUBNAME`i `HUBLISTENACCESS` (zdefiniowany w pliku hubinfo.h) ma już hello `<hub name>` i `<connection string with listen access>` symbole zastępcze zastąpione powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultListenSharedAccessSignature*uzyskany wcześniej</span><span class="sxs-lookup"><span data-stu-id="3abba-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have hello `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="3abba-137">Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, hello klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="3abba-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="3abba-138">Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować tooregister Twojej aplikacji dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="3abba-138">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="3abba-139">klucz pełny dostęp Hello jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.</span><span class="sxs-lookup"><span data-stu-id="3abba-139">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="3abba-140">W hello **didRegisterForRemoteNotificationsWithDeviceToken** metody w AppDelegate.m, Zamień hello kod w metodzie hello hello następującego kodu toopass hello urządzenie tokenu toohello powiadomienia klasy.</span><span class="sxs-lookup"><span data-stu-id="3abba-140">In hello **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace hello code in hello method with hello following code toopass hello device token toohello notifications class.</span></span> <span data-ttu-id="3abba-141">Klasa powiadomienia Hello wykona hello rejestrowanie na potrzeby powiadomień z kategorii hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-141">hello notifications class will perform hello registering for notifications with hello categories.</span></span> <span data-ttu-id="3abba-142">Jeśli hello użytkownik zmieni ułatwia wybieranie kategorii, nazywamy hello `subscribeWithCategories` metody w odpowiedzi toohello **subskrypcji** tooupdate przycisk je.</span><span class="sxs-lookup"><span data-stu-id="3abba-142">If hello user changes category selections, we call hello `subscribeWithCategories` method in response toohello **subscribe** button tooupdate them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3abba-143">Ponieważ token urządzenia hello przypisał hello Notification Service (APNS, Apple Push) szansy można w dowolnym momencie, należy zarejestrować powiadomienia o często tooavoid powiadomień błędów.</span><span class="sxs-lookup"><span data-stu-id="3abba-143">Because hello device token assigned by hello Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="3abba-144">W tym przykładzie rejestruje powiadomienia o każdym uruchomieniu danej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-144">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="3abba-145">Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, prawdopodobnie Jeśli możesz pominąć rejestrację toopreserve przepustowości od poprzedniej rejestracji hello upłynął krótszy niż doba.</span><span class="sxs-lookup"><span data-stu-id="3abba-145">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="3abba-146">Należy pamiętać, że w tym momencie nie powinno być nie innych kodu w hello **didRegisterForRemoteNotificationsWithDeviceToken** metody.</span><span class="sxs-lookup"><span data-stu-id="3abba-146">Note that at this point there should be no other code in hello **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="3abba-147">Hello następujących metod powinna już być obecne w AppDelegate.m ukończenie hello [Rozpoczynanie pracy z usługą Notification Hubs] [ get-started] samouczka.</span><span class="sxs-lookup"><span data-stu-id="3abba-147">hello following methods should already be present in AppDelegate.m from completing hello [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="3abba-148">Jeśli nie, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="3abba-148">If not, add them.</span></span>
   
    <span data-ttu-id="3abba-149">-(void) MessageBox:(NSString *) tytułu wiadomości:(NSString *) messageText {</span><span class="sxs-lookup"><span data-stu-id="3abba-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="3abba-150">}</span><span class="sxs-lookup"><span data-stu-id="3abba-150">}</span></span>
   
   * <span data-ttu-id="3abba-151">didReceiveRemoteNotification aplikacji:(UIApplication *) aplikacji (void): (NSDictionary *) informacje o użytkowniku {NSLog (@"% @", informacje o użytkowniku);   [self MessageBox:@"Notification" komunikat: [valueForKey:@"alert [informacje o użytkowniku objectForKey:@"aps"]"]]; }</span><span class="sxs-lookup"><span data-stu-id="3abba-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="3abba-152">Ta metoda obsługuje powiadomienia otrzymane uruchomionej aplikacji hello wyświetlając prostą **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="3abba-152">This method handles notifications received when hello app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="3abba-153">W ViewController.m, Dodaj instrukcję import dla AppDelegate.h i skopiuj powitania po kodu na powitania generowanych przez XCode **subskrypcji** metody.</span><span class="sxs-lookup"><span data-stu-id="3abba-153">In ViewController.m, add a import statement for AppDelegate.h and copy hello following code into hello XCode-generated **subscribe** method.</span></span> <span data-ttu-id="3abba-154">Ten kod będzie aktualizować hello powiadomień rejestracji toouse hello nowej kategorii znaczniki hello użytkownik wybierze w interfejsie użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-154">This code will update hello notification registration toouse hello new category tags hello user has chosen in hello user interface.</span></span>
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   <span data-ttu-id="3abba-155">Ta metoda tworzy **NSMutableArray** z kategorii i używa hello **powiadomienia** klasy toostore hello liście hello lokalnego magazynu i rejestruje hello odpowiednie tagi w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="3abba-155">This method creates an **NSMutableArray** of categories and uses hello **Notifications** class toostore hello list in hello local storage and registers hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="3abba-156">Zmiana kategorii rejestracji hello zostaje odtworzone w hello nowych kategorii.</span><span class="sxs-lookup"><span data-stu-id="3abba-156">When categories are changed, hello registration is recreated with hello new categories.</span></span>
3. <span data-ttu-id="3abba-157">W ViewController.m, Dodaj hello następującego kodu w hello **viewDidLoad** interfejsu użytkownika hello tooset metody na podstawie hello wcześniej zapisany kategorii.</span><span class="sxs-lookup"><span data-stu-id="3abba-157">In ViewController.m, add hello following code in hello **viewDidLoad** method tooset hello user interface based on hello previously saved categories.</span></span>

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="3abba-158">Aplikacja Hello teraz można przechowywać zestawu kategorii w hello urządzenia magazynu lokalnego używane tooregister hello Centrum powiadomień, przy każdym uruchomieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-158">hello app can now store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello app starts.</span></span>  <span data-ttu-id="3abba-159">Hello użytkownik może zmienić wybór hello kategorii w czasie wykonywania i kliknij hello **subskrypcji** metody tooupdate hello rejestracji dla urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-159">hello user can change hello selection of categories at runtime and click hello **subscribe** method tooupdate hello registration for hello device.</span></span> <span data-ttu-id="3abba-160">Następnie zostanie zaktualizowana hello toosend aplikacji hello fundamentalne wiadomości powiadomienia bezpośrednio w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-160">Next, you will update hello app toosend hello breaking news notifications directly in hello app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="3abba-161">(opcjonalnie) Wysyłanie powiadomień oznakowany</span><span class="sxs-lookup"><span data-stu-id="3abba-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="3abba-162">Jeśli nie masz dostępu tooVisual w Studio można pominąć toohello następnej sekcji i wysyłania powiadomień z samej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-162">If you don't have access tooVisual Studio, you can skip toohello next section and send notifications from hello app itself.</span></span> <span data-ttu-id="3abba-163">Można również wysłać hello prawidłowego szablonu powiadomień z hello [klasycznego portalu Azure] za pomocą karty debugowanie hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="3abba-163">You can also send hello proper template notification from hello [Azure Classic Portal] using hello debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a><span data-ttu-id="3abba-164">(opcjonalnie) Wysyłanie powiadomień z hello urządzenia</span><span class="sxs-lookup"><span data-stu-id="3abba-164">(optional) Send notifications from hello device</span></span>
<span data-ttu-id="3abba-165">Zwykle usługi wewnętrznej bazy danych będą wysyłane powiadomienia, ale możesz wysłać powiadomienia o najważniejszych wiadomościach bezpośrednio z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from hello app.</span></span> <span data-ttu-id="3abba-166">toodo to modyfikacjom hello `SendNotificationRESTAPI` metody zdefiniowanego w hello [Rozpoczynanie pracy z usługą Notification Hubs] [ get-started] samouczka.</span><span class="sxs-lookup"><span data-stu-id="3abba-166">toodo this we will update hello `SendNotificationRESTAPI` method that we defined in hello [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="3abba-167">W hello aktualizacji ViewController.m `SendNotificationRESTAPI` metodę jako zgodna tak, aby przyjmuje parametr hello kategorii tagu i wysyła odpowiednie hello [szablonu](notification-hubs-templates-cross-platform-push-messages.md) powiadomień.</span><span class="sxs-lookup"><span data-stu-id="3abba-167">In ViewController.m update hello `SendNotificationRESTAPI` method as follows so that it accepts a parameter for hello category tag and sends hello proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
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
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
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
2. <span data-ttu-id="3abba-168">W hello aktualizacji ViewController.m **Wyślij powiadomienie E-mail** akcji, jak pokazano w kodzie hello, który jest zgodny.</span><span class="sxs-lookup"><span data-stu-id="3abba-168">In ViewController.m update hello **Send Notification** action as shown in hello code that follows.</span></span> <span data-ttu-id="3abba-169">Tak, aby będzie wysyłać powiadomienia hello każdego tagu indywidualnie i wysłać toomultiple platform.</span><span class="sxs-lookup"><span data-stu-id="3abba-169">So that it will send hello notifications using each tag individually and send toomultiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="3abba-170">Ponownie skompiluj projekt i upewnij się, że żadne błędy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="3abba-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="3abba-171">Uruchamianie aplikacji hello i generować powiadomienia</span><span class="sxs-lookup"><span data-stu-id="3abba-171">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="3abba-172">Naciśnij klawisz hello uruchomienia projektu hello toobuild przycisk i uruchomić aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="3abba-172">Press hello Run button toobuild hello project and start hello app.</span></span> <span data-ttu-id="3abba-173">Wybierz tooand toosubscribe niektóre najważniejszych wiadomości opcje, a następnie naciśnij klawisz hello **Subskrybuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3abba-173">Select some breaking news options toosubscribe tooand then press hello **Subscribe** button.</span></span> <span data-ttu-id="3abba-174">Okno dialogowe wskazujący hello, które zostały subskrypcję powiadomień powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="3abba-174">You should see a dialog indicating hello notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="3abba-175">Po wybraniu **Subskrybuj**, hello kategorii hello wybrane konwertuje aplikacji do tagów i żąda nowej rejestracji urządzenia hello wybrane tagów z hello Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="3abba-175">When you choose **Subscribe**, hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span>
2. <span data-ttu-id="3abba-176">Wprowadź toobe wiadomości wysłane w postaci naciśnij najważniejszych wiadomości powitania **Wyślij powiadomienie E-mail** przycisku.</span><span class="sxs-lookup"><span data-stu-id="3abba-176">Enter a message toobe sent as breaking news then press hello **Send Notification** button.</span></span> <span data-ttu-id="3abba-177">Można również uruchomić hello .NET konsoli aplikacji toogenerate powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="3abba-177">Alternatively, run hello .NET console app toogenerate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="3abba-178">Każdej wiadomości toobreaking urządzenia subskrybowane otrzyma hello powiadomienia o najważniejszych wiadomościach właśnie wysłania.</span><span class="sxs-lookup"><span data-stu-id="3abba-178">Each device subscribed toobreaking news will receive hello breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3abba-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3abba-179">Next steps</span></span>
<span data-ttu-id="3abba-180">W tym samouczku opisano sposób toobroadcast krytyczne według kategorii wiadomości.</span><span class="sxs-lookup"><span data-stu-id="3abba-180">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="3abba-181">Należy rozważyć wykonanie jednej hello następujące samouczki dotyczące innych zaawansowanych scenariuszy centra powiadomień:</span><span class="sxs-lookup"><span data-stu-id="3abba-181">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="3abba-182">**[Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]**</span><span class="sxs-lookup"><span data-stu-id="3abba-182">**[Use Notification Hubs toobroadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="3abba-183">Dowiedz się, jak fundamentalne wysyłania tooenable aplikacji wiadomości powitania tooexpand zlokalizowane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="3abba-183">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Użyj usługi Notification Hubs toobroadcast zlokalizowane najważniejszych wiadomości]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[klasycznego portalu Azure]: https://manage.windowsazure.com
