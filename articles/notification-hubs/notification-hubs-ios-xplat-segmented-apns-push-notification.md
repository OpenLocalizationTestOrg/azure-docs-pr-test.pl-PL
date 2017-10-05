---
title: "Centra powiadomień w najważniejszych wiadomości Samouczek — systemu iOS"
description: "Dowiedz się, jak używać usługi Azure Service Bus Notification Hubs można wysłać powiadomienia o najważniejszych wiadomościach do urządzeń z systemem iOS."
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
ms.openlocfilehash: dc47250db6fb3a2853dae24e02bda236154d93fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="4c9e8-103">Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="4c9e8-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="4c9e8-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4c9e8-104">Overview</span></span>
<span data-ttu-id="4c9e8-105">W tym temacie przedstawiono sposób użycia usługi Azure Notification Hubs wysyłać powiadomienia o najważniejszych wiadomościach do aplikacji systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an iOS app.</span></span> <span data-ttu-id="4c9e8-106">Po zakończeniu będzie można rejestrować zakłócenia w kategorii wiadomości i odbierać tylko powiadomienia wypychane dla tych kategorii.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="4c9e8-107">Ten scenariusz jest wspólnego wzorca dla wielu aplikacji, gdzie powiadomienia muszą być wysłane do grup użytkowników, które wcześniej zostały zadeklarowane zainteresowanie je, np. czytnik danych RSS, aplikacje wentylatory utworów muzycznych itp.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="4c9e8-108">Scenariusze emisji są włączone, umieszczając w niej co najmniej jeden *tagi* podczas tworzenia rejestracji w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="4c9e8-109">Gdy powiadomienia są wysyłane do tagu, wszystkie urządzenia, które zostały zarejestrowane dla tagu będą otrzymywać powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="4c9e8-110">Ponieważ tagi są po prostu ciągów, nie mają być przygotowana z wyprzedzeniem.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="4c9e8-111">Aby uzyskać więcej informacji na temat tagów, zapoznaj się [routingu centra powiadomień i wyrażeń tagów](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="4c9e8-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c9e8-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4c9e8-112">Prerequisites</span></span>
<span data-ttu-id="4c9e8-113">W tym temacie opiera się na aplikacji utworzony w [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="4c9e8-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="4c9e8-114">Przed rozpoczęciem tego samouczka należy zostały już wykonane [Rozpoczynanie pracy z usługą Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="4c9e8-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="4c9e8-115">Dodaj wybrane kategorii do aplikacji</span><span class="sxs-lookup"><span data-stu-id="4c9e8-115">Add category selection to the app</span></span>
<span data-ttu-id="4c9e8-116">Pierwszym krokiem jest dodanie elementów interfejsu użytkownika do Twoje istniejące scenorysu, który umożliwia użytkownikowi wybierz kategorie, aby zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-116">The first step is to add the UI elements to your existing storyboard that enable the user to select categories to register.</span></span> <span data-ttu-id="4c9e8-117">Kategorie wybrane przez użytkownika są przechowywane na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="4c9e8-118">Po uruchomieniu aplikacji, rejestracji urządzenia jest tworzony w Centrum powiadomień z wybranych kategorii jako znaczniki.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="4c9e8-119">W Twojej MainStoryboard_iPhone.storyboard Dodaj poniższe składniki z biblioteki obiektów:</span><span class="sxs-lookup"><span data-stu-id="4c9e8-119">In your MainStoryboard_iPhone.storyboard add the following components from the object library:</span></span>
   
   * <span data-ttu-id="4c9e8-120">Etykiety z tekstem "Krytyczne wiadomości"</span><span class="sxs-lookup"><span data-stu-id="4c9e8-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="4c9e8-121">Etykiety z teksty kategorii "World", "Polityka", "Business", "Technologii", "Nauki", "Sport",</span><span class="sxs-lookup"><span data-stu-id="4c9e8-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="4c9e8-122">Sześć przełączników, jeden dla każdej kategorii, ustaw każdy przełącznik **stanu** jako **poza** domyślnie.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-122">Six switches, one per category, set each switch **State** to be **Off** by default.</span></span>
   * <span data-ttu-id="4c9e8-123">Jeden z przycisków z etykietą "Subskrybuj"</span><span class="sxs-lookup"><span data-stu-id="4c9e8-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="4c9e8-124">Twoje scenorysu powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="4c9e8-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="4c9e8-125">W edytorze Asystenta utworzyć gniazda dla wszystkich przełączników i połączeń telefonicznych z nimi "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span><span class="sxs-lookup"><span data-stu-id="4c9e8-125">In the assistant editor, create outlets for all the switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="4c9e8-126">Utwórz działanie dla przycisk o nazwie "subskrypcji".</span><span class="sxs-lookup"><span data-stu-id="4c9e8-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="4c9e8-127">Twoje ViewController.h powinien zawierać następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="4c9e8-127">Your ViewController.h should contain the following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="4c9e8-128">Utwórz nową **klasy Touch Cocoa** o nazwie `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="4c9e8-129">Skopiuj następujący kod w sekcji interfejsu pliku Notifications.h:</span><span class="sxs-lookup"><span data-stu-id="4c9e8-129">Copy the following code in the interface section of the file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="4c9e8-130">Dodaj następujące dyrektywy importu do Notifications.m:</span><span class="sxs-lookup"><span data-stu-id="4c9e8-130">Add the following import directive to Notifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="4c9e8-131">Skopiuj następujący kod w sekcji implementacji pliku Notifications.m.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-131">Copy the following code in the implementation section of the file Notifications.m.</span></span>
   
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



    <span data-ttu-id="4c9e8-132">Ta klasa korzysta z magazynu lokalnego do przechowywania i pobierania kategorii wiadomości, który otrzyma tego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-132">This class uses local storage to store and retrieve the categories of news that this device will receive.</span></span> <span data-ttu-id="4c9e8-133">Ponadto zawiera metody do rejestrowania dla tych kategorii przy użyciu [szablonu](notification-hubs-templates-cross-platform-push-messages.md) rejestracji.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-133">Also, it contains a method to register for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="4c9e8-134">W pliku AppDelegate.h Dodaj instrukcję import Notifications.h i Dodaj właściwość do wystąpienia klasy powiadomień:</span><span class="sxs-lookup"><span data-stu-id="4c9e8-134">In the AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of the Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="4c9e8-135">W **didFinishLaunchingWithOptions** metody w AppDelegate.m, Dodaj kod, aby zainicjować wystąpienia powiadomienia na początku metody.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-135">In the **didFinishLaunchingWithOptions** method in AppDelegate.m, add the code to initialize the notifications instance at the beginning of the method.</span></span>  
   
    <span data-ttu-id="4c9e8-136">`HUBNAME`i `HUBLISTENACCESS` (zdefiniowany w pliku hubinfo.h) ma już `<hub name>` i `<connection string with listen access>` zastąpione symbole zastępcze nazwą Centrum powiadomień i parametry połączenia dla *DefaultListenSharedAccessSignature* uzyskany wcześniej</span><span class="sxs-lookup"><span data-stu-id="4c9e8-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have the `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="4c9e8-137">Ponieważ poświadczenia, które są dystrybuowane wraz z aplikacji przez klienta nie są zazwyczaj bezpieczna, klucz dostępu do nasłuchiwania należy dystrybuować tylko z aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="4c9e8-138">Nasłuchiwanie umożliwia dostęp, nie można zmodyfikować aplikację, aby zarejestrować dla powiadomień, ale istniejące rejestracje i nie mogą być wysyłane powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-138">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="4c9e8-139">Klucz pełny dostęp jest używany w usłudze zabezpieczonych wewnętrznej bazy danych do wysyłania powiadomień i zmianę istniejącego rejestracji.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-139">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="4c9e8-140">W **didRegisterForRemoteNotificationsWithDeviceToken** metody w AppDelegate.m, Zastąp kod w metodzie następujący kod, aby przekazać token urządzenia do klasy powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-140">In the **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace the code in the method with the following code to pass the device token to the notifications class.</span></span> <span data-ttu-id="4c9e8-141">Klasa powiadomienia będzie wykonywać rejestrowanie na potrzeby powiadomień z kategorii.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-141">The notifications class will perform the registering for notifications with the categories.</span></span> <span data-ttu-id="4c9e8-142">Jeśli użytkownik zmieni ułatwia wybieranie kategorii, nazywamy `subscribeWithCategories` metody w odpowiedzi na **subskrypcji** przycisk, aby je aktualizować.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-142">If the user changes category selections, we call the `subscribeWithCategories` method in response to the **subscribe** button to update them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4c9e8-143">Ponieważ token urządzenia przypisane przez Notification Service (APNS, Apple Push) szansy można w dowolnym momencie, należy zarejestrować powiadomień często uniknąć niepowodzeń powiadomień.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-143">Because the device token assigned by the Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="4c9e8-144">W tym przykładzie rejestruje powiadomienia każdym uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-144">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="4c9e8-145">Dla aplikacji, które są uruchamiane często więcej niż raz dziennie, można prawdopodobnie pominąć rejestrację, aby zachować przepustowość, jeśli krótszy niż doba upłynął od czasu poprzedniej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-145">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves the categories from local storage and requests a registration for these categories
        // each time the app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="4c9e8-146">Należy pamiętać, że w tym momencie nie powinno być nie innych kodu w **didRegisterForRemoteNotificationsWithDeviceToken** metody.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-146">Note that at this point there should be no other code in the **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="4c9e8-147">Następujące metody już powinien znajdować się w AppDelegate.m ukończenie [Rozpoczynanie pracy z usługą Notification Hubs] [ get-started] samouczka.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-147">The following methods should already be present in AppDelegate.m from completing the [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="4c9e8-148">Jeśli nie, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-148">If not, add them.</span></span>
   
    <span data-ttu-id="4c9e8-149">-(void) MessageBox:(NSString *) tytułu wiadomości:(NSString *) messageText {</span><span class="sxs-lookup"><span data-stu-id="4c9e8-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="4c9e8-150">}</span><span class="sxs-lookup"><span data-stu-id="4c9e8-150">}</span></span>
   
   * <span data-ttu-id="4c9e8-151">didReceiveRemoteNotification aplikacji:(UIApplication *) aplikacji (void): (NSDictionary *) informacje o użytkowniku {NSLog (@"% @", informacje o użytkowniku);   [self MessageBox:@"Notification" komunikat: [valueForKey:@"alert [informacje o użytkowniku objectForKey:@"aps"]"]]; }</span><span class="sxs-lookup"><span data-stu-id="4c9e8-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="4c9e8-152">Ta metoda obsługuje powiadomienia otrzymane, gdy aplikacja jest uruchomiona, wyświetlając prostą **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-152">This method handles notifications received when the app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="4c9e8-153">W ViewController.m, Dodaj instrukcję import AppDelegate.h i skopiuj następujący kod do generowanych XCode **subskrypcji** metody.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-153">In ViewController.m, add a import statement for AppDelegate.h and copy the following code into the XCode-generated **subscribe** method.</span></span> <span data-ttu-id="4c9e8-154">Ten kod zaktualizuje rejestracji powiadomień do używania nowych tagów kategorii, którą użytkownik wybrał w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-154">This code will update the notification registration to use the new category tags the user has chosen in the user interface.</span></span>
   
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
   
   <span data-ttu-id="4c9e8-155">Ta metoda tworzy **NSMutableArray** kategorii i używa **powiadomienia** klasę do przechowywania listy w lokalnej pamięci masowej i rejestruje odpowiednie znaczniki w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-155">This method creates an **NSMutableArray** of categories and uses the **Notifications** class to store the list in the local storage and registers the corresponding tags with your notification hub.</span></span> <span data-ttu-id="4c9e8-156">Zmiana kategorii rejestracji zostaje odtworzone w nowej kategorii.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-156">When categories are changed, the registration is recreated with the new categories.</span></span>
3. <span data-ttu-id="4c9e8-157">W ViewController.m, Dodaj następujący kod w **viewDidLoad** metodę w celu ustawienia interfejsu użytkownika na podstawie wcześniej zapisany kategorii.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-157">In ViewController.m, add the following code in the **viewDidLoad** method to set the user interface based on the previously saved categories.</span></span>

        // This updates the UI on startup based on the status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="4c9e8-158">Aplikacja może teraz przechowywać zestaw kategorii w magazynie lokalnym urządzenia używane do rejestrowania w Centrum powiadomień przy każdym uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-158">The app can now store a set of categories in the device local storage used to register with the notification hub whenever the app starts.</span></span>  <span data-ttu-id="4c9e8-159">Użytkownik może zmienić wybór kategorii środowiska uruchomieniowego i kliknij przycisk **subskrypcji** metodę, aby zaktualizować rejestrację urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-159">The user can change the selection of categories at runtime and click the **subscribe** method to update the registration for the device.</span></span> <span data-ttu-id="4c9e8-160">Następnie zostanie zaktualizowania aplikacji można wysłać powiadomienia o najważniejszych wiadomościach bezpośrednio w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-160">Next, you will update the app to send the breaking news notifications directly in the app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="4c9e8-161">(opcjonalnie) Wysyłanie powiadomień oznakowany</span><span class="sxs-lookup"><span data-stu-id="4c9e8-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="4c9e8-162">Jeśli nie masz dostępu do programu Visual Studio, można przejść do następnej sekcji i wysyłania powiadomień z samej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-162">If you don't have access to Visual Studio, you can skip to the next section and send notifications from the app itself.</span></span> <span data-ttu-id="4c9e8-163">Możesz również wysłać powiadomienie prawidłowego szablonu z [klasycznego portalu Azure] za pomocą karty debugowanie w Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-163">You can also send the proper template notification from the [Azure Classic Portal] using the debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-the-device"></a><span data-ttu-id="4c9e8-164">(opcjonalnie) Wysyłanie powiadomień z urządzenia</span><span class="sxs-lookup"><span data-stu-id="4c9e8-164">(optional) Send notifications from the device</span></span>
<span data-ttu-id="4c9e8-165">Zwykle usługi wewnętrznej bazy danych będą wysyłane powiadomienia, ale możesz wysłać powiadomienia o najważniejszych wiadomościach bezpośrednio z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from the app.</span></span> <span data-ttu-id="4c9e8-166">W tym modyfikacjom `SendNotificationRESTAPI` metody zdefiniowanego w [Rozpoczynanie pracy z usługą Notification Hubs] [ get-started] samouczka.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-166">To do this we will update the `SendNotificationRESTAPI` method that we defined in the [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="4c9e8-167">W ramach aktualizacji ViewController.m `SendNotificationRESTAPI` metodę jako zgodna, który akceptuje parametr dla tagu kategorii i wysyła właściwego [szablonu](notification-hubs-templates-cross-platform-push-messages.md) powiadomień.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-167">In ViewController.m update the `SendNotificationRESTAPI` method as follows so that it accepts a parameter for the category tag and sends the proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct the messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated the token to be used in the authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the template notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add the category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
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
2. <span data-ttu-id="4c9e8-168">W ramach aktualizacji ViewController.m **Wyślij powiadomienie E-mail** akcji, jak pokazano w następującym kodzie.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-168">In ViewController.m update the **Send Notification** action as shown in the code that follows.</span></span> <span data-ttu-id="4c9e8-169">Tak, aby będzie wysyłania powiadomień przy użyciu tagami indywidualnie i wysłać do wielu platform.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-169">So that it will send the notifications using each tag individually and send to multiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send the message as breaking news for each category to WNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="4c9e8-170">Ponownie skompiluj projekt i upewnij się, że żadne błędy kompilacji.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="4c9e8-171">Uruchom aplikację i generować powiadomienia</span><span class="sxs-lookup"><span data-stu-id="4c9e8-171">Run the app and generate notifications</span></span>
1. <span data-ttu-id="4c9e8-172">Naciśnij przycisk Uruchom, aby skompilować projekt i uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-172">Press the Run button to build the project and start the app.</span></span> <span data-ttu-id="4c9e8-173">Wybierz niektóre opcje wiadomości podziału subskrybować, a następnie naciśnij klawisz **Subskrybuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-173">Select some breaking news options to subscribe to and then press the **Subscribe** button.</span></span> <span data-ttu-id="4c9e8-174">Powinny zostać wyświetlone okno dialogowe wskazujący, że zostały subskrypcję powiadomień.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-174">You should see a dialog indicating the notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="4c9e8-175">Po wybraniu **Subskrybuj**, konwertuje wybranych kategorii do tagów i żąda nowej rejestracji urządzeń dla wybranych tagów z Centrum powiadomień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-175">When you choose **Subscribe**, the app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span>
2. <span data-ttu-id="4c9e8-176">Wpisz wiadomość, aby wysłane w postaci najważniejszych wiadomości naciśnij **Wyślij powiadomienie E-mail** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-176">Enter a message to be sent as breaking news then press the **Send Notification** button.</span></span> <span data-ttu-id="4c9e8-177">Można również uruchomić aplikacji konsoli .NET do generowania powiadomień.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-177">Alternatively, run the .NET console app to generate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="4c9e8-178">Każdego urządzenia, które subskrybuje fundamentalne wiadomości otrzymają powiadomienia o najważniejszych wiadomościach właśnie wysłania.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-178">Each device subscribed to breaking news will receive the breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c9e8-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4c9e8-179">Next steps</span></span>
<span data-ttu-id="4c9e8-180">W tym samouczku opisano sposób emisji najważniejszych wiadomości według kategorii.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-180">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="4c9e8-181">Należy rozważyć wykonanie jednej z następujących samouczków, w których są wyróżniane innych zaawansowanych scenariuszy centra powiadomień:</span><span class="sxs-lookup"><span data-stu-id="4c9e8-181">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="4c9e8-182">**[Emisji zlokalizowanych najważniejszych wiadomości przy użyciu usługi Notification Hubs]**</span><span class="sxs-lookup"><span data-stu-id="4c9e8-182">**[Use Notification Hubs to broadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="4c9e8-183">Dowiedz się, jak rozszerzyć aplikację wiadomości podziału, aby umożliwić wysyłanie powiadomień zlokalizowane.</span><span class="sxs-lookup"><span data-stu-id="4c9e8-183">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="4c9e8-184">[Emisji zlokalizowanych najważniejszych wiadomości przy użyciu usługi Notification Hubs]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="4c9e8-184">[Use Notification Hubs to broadcast localized breaking news]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
<span data-ttu-id="4c9e8-185">[klasycznego portalu Azure]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="4c9e8-185">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
