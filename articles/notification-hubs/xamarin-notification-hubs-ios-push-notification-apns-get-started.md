---
title: "Wysyłanie powiadomień wypychanych do aplikacji platformy Xamarin dla systemu iOS przy użyciu usługi Notification Hubs | Microsoft Docs"
description: "Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji platformy Xamarin dla systemu iOS przy użyciu usługi Azure Notification Hubs."
services: notification-hubs
keywords: "powiadomienia wypychane w systemie ios, wiadomości wypychane, powiadomienia wypychane, wiadomość wypychana"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 72a81fa0deb34ace77b8fb9b1a4e6b24ee164b35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="4e03b-104">Wysyłanie powiadomień wypychanych do aplikacji platformy Xamarin dla systemu iOS przy użyciu usługi Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="4e03b-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="4e03b-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4e03b-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4e03b-106">Do wykonania kroków tego samouczka potrzebne jest aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4e03b-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="4e03b-107">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="4e03b-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4e03b-108">Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="4e03b-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="4e03b-109">Korzystając z tego samouczka, dowiesz się, jak wysyłać powiadomienia wypychane do aplikacji dla systemu iOS przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="4e03b-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to an iOS application.</span></span>
<span data-ttu-id="4e03b-110">Utworzysz pustą aplikację platformy Xamarin.iOS służącą do odbierania powiadomień wypychanych przy użyciu usługi [Apple Push Notification Service (APNS)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="4e03b-110">You'll create a blank Xamarin.iOS app that receives push notifications by using the [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="4e03b-111">Po zakończeniu będzie można za pomocą centrum powiadomień wysyłać powiadomienia wypychane do wszystkich urządzeń z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="4e03b-111">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span> <span data-ttu-id="4e03b-112">Gotowy kod jest dostępny w przykładowej aplikacji [NotificationHubs][GitHub].</span><span class="sxs-lookup"><span data-stu-id="4e03b-112">The finished code is available in the [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="4e03b-113">W tym samouczku został omówiony prosty scenariusz wysyłania powiadomień wypychanych przy użyciu usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="4e03b-113">This tutorial demonstrates the simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e03b-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4e03b-114">Prerequisites</span></span>
<span data-ttu-id="4e03b-115">Dla tego samouczka wymagane są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4e03b-115">This tutorial requires the following:</span></span>

* <span data-ttu-id="4e03b-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="4e03b-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="4e03b-117">Urządzenie zgodne z systemem iOS 7.0 (lub nowszą wersją)</span><span class="sxs-lookup"><span data-stu-id="4e03b-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="4e03b-118">Członkostwo w programie dla deweloperów systemu iOS</span><span class="sxs-lookup"><span data-stu-id="4e03b-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="4e03b-119">[Program Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="4e03b-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4e03b-120">Ze względu na wymagania dotyczące konfiguracji powiadomień wypychanych w systemie iOS należy wdrożyć i przetestować aplikację przykładową na fizycznym urządzeniu z systemem iOS (telefonie iPhone lub tablecie iPad), a nie w symulatorze.</span><span class="sxs-lookup"><span data-stu-id="4e03b-120">Because of configuration requirements for iOS push notifications, you must deploy and test the sample application on a physical iOS device (iPhone or iPad) instead of in the simulator.</span></span>
  > 
  > 

<span data-ttu-id="4e03b-121">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usług Notification Hubs dotyczących aplikacji platformy Xamarin.iOS.</span><span class="sxs-lookup"><span data-stu-id="4e03b-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="4e03b-122">Konfigurowanie centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="4e03b-122">Configure your notification hub</span></span>
<span data-ttu-id="4e03b-123">W tej sekcji opisano kroki tworzenia nowego centrum powiadomień i konfigurowania uwierzytelniania w usłudze APNs przy użyciu utworzonego przez Ciebie certyfikatu powiadomień wypychanych **.p12**.</span><span class="sxs-lookup"><span data-stu-id="4e03b-123">This section walks you through creating a new notification hub and configuring authentication with APNS using the **.p12** push certificate that you created.</span></span> <span data-ttu-id="4e03b-124">Jeśli chcesz użyć już utworzonego centrum powiadomień, możesz przejść do kroku 5.</span><span class="sxs-lookup"><span data-stu-id="4e03b-124">If you want to use a notification hub that you have already created, you can skip to step 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="4e03b-125">Ponieważ wymagane jest skonfigurowanie połączenia usługi APNS, w witrynie Azure Portal otwórz ustawienia usługi Notification Hub, kliknij pozycję <b>Usługi powiadomień</b>, a następnie kliknij pozycję <b>Apple (APNS)</b> na liście.</span><span class="sxs-lookup"><span data-stu-id="4e03b-125">As we want to configure the APNS connection, in the Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click the <b>Apple (APNS)</b> item in the list.</span></span> <span data-ttu-id="4e03b-126">Następnie kliknij pozycję <b>Przekaż certyfikat</b> i wybierz uprzednio wyeksportowany certyfikat <b>.p12</b> oraz hasło tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="4e03b-126">Once done, click on <b>Upload Certificate</b> and select the <b>.p12</b> certificate that you exported earlier, as well as the password for the certificate.</span></span></p>

<p><span data-ttu-id="4e03b-127">Pamiętaj o wybraniu trybu <b>Piaskownica</b>, ponieważ powiadomienia wypychane będą wysyłane w środowisku projektowym.</span><span class="sxs-lookup"><span data-stu-id="4e03b-127">Make sure to select <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="4e03b-128">Ustawienie <b>Produkcja</b> należy wybrać wyłącznie wówczas, gdy chcesz wysyłać powiadomienia wypychane do użytkowników, którzy kupili już Twoją aplikację w sklepie.</span><span class="sxs-lookup"><span data-stu-id="4e03b-128">Only use the <b>Production</b> setting if you want to send push notifications to users who already purchased your app from the store.</span></span></p>
</li>
</ol>
<span data-ttu-id="4e03b-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="4e03b-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="4e03b-130">Twoje centrum powiadomień jest teraz skonfigurowane do pracy z usługą APNs i uzyskano parametry połączenia służące do rejestrowania aplikacji w celu wysyłania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="4e03b-130">Your notification hub is now configured to work with APNS, and you have the connection strings to register your app and send push notifications.</span></span>

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="4e03b-131">Łączenie aplikacji z centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="4e03b-131">Connect your app to the notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="4e03b-132">Tworzenie nowego projektu</span><span class="sxs-lookup"><span data-stu-id="4e03b-132">Create a new project</span></span>
1. <span data-ttu-id="4e03b-133">W programie Xamarin Studio utwórz nowy projekt dla systemu iOS i wybierz szablon **Unified API (Standaryzowany interfejs API)** > **Single View Application (Aplikacja z jednym widokiem)**.</span><span class="sxs-lookup"><span data-stu-id="4e03b-133">In Xamarin Studio, create a new iOS project and select the **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio — wybieranie typu aplikacji][31]
2. <span data-ttu-id="4e03b-135">Dodaj odniesienie do składnika Azure Messaging.</span><span class="sxs-lookup"><span data-stu-id="4e03b-135">Add a reference to the Azure Messaging component.</span></span> <span data-ttu-id="4e03b-136">W widoku Solution (Rozwiązanie) kliknij prawym przyciskiem myszy folder **Components** (Składniki) w projekcie i wybierz polecenie **Get More Components** (Uzyskaj więcej składników).</span><span class="sxs-lookup"><span data-stu-id="4e03b-136">In the Solution view, right-click the **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="4e03b-137">Wyszukaj składnik **Azure Messaging** i dodaj go do projektu.</span><span class="sxs-lookup"><span data-stu-id="4e03b-137">Search for the **Azure Messaging** component and add the component to your project.</span></span>
3. <span data-ttu-id="4e03b-138">W pliku **AppDelegate.cs** dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="4e03b-138">In **AppDelegate.cs**, add the following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="4e03b-139">Zadeklaruj wystąpienie **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="4e03b-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="4e03b-140">Utwórz klasę **Constants.cs** z następującymi zmiennymi:</span><span class="sxs-lookup"><span data-stu-id="4e03b-140">Create a **Constants.cs** class with the following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="4e03b-141">W pliku **AppDelegate.cs** zaktualizuj metodę **FinishedLaunching()** zgodnie z poniższym kodem:</span><span class="sxs-lookup"><span data-stu-id="4e03b-141">In **AppDelegate.cs**, update **FinishedLaunching()** to match the following:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. <span data-ttu-id="4e03b-142">Zastąp metodę **RegisteredForRemoteNotifications()** w pliku **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="4e03b-142">Override the **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. <span data-ttu-id="4e03b-143">Zastąp metodę **ReceivedRemoteNotification()** w pliku **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="4e03b-143">Override the **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="4e03b-144">Utwórz następującą metodę **ProcessNotification()** w pliku **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="4e03b-144">Create the following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check to see if the dictionary has the aps key.  This is the notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get the aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract the alert text
                // NOTE: If you're using the simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from the aps dictionary will be another NSDictionary.
                // Basically the JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from the ReceivedRemoteNotification while the app was running,
                // we of course need to manually process things like the sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > <span data-ttu-id="4e03b-145">Możesz również opcjonalnie zastąpić metodę **FailedToRegisterForRemoteNotifications()** w celu obsługi sytuacji takich jak brak połączenia z siecią.</span><span class="sxs-lookup"><span data-stu-id="4e03b-145">You can choose to override **FailedToRegisterForRemoteNotifications()** to handle situations such as no network connection.</span></span> <span data-ttu-id="4e03b-146">Jest to szczególnie istotne w przypadku, gdy użytkownik może uruchomić aplikację w trybie offline (na przykład w trybie samolotowym), a chcesz obsługiwać scenariusze powiadomień wypychanych specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4e03b-146">This is especially important where the user might start your application in offline mode (e.g. Airplane) and you want to handle push messaging scenarios specific to your app.</span></span>
   > 
   > 
10. <span data-ttu-id="4e03b-147">Uruchom aplikację na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="4e03b-147">Run the app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="4e03b-148">Wysyłanie powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="4e03b-148">Sending Push Notifications</span></span>
<span data-ttu-id="4e03b-149">Możesz przetestować odbieranie powiadomień wypychanych w aplikacji, wysyłając powiadomienia w witrynie [Azure Portal] za pomocą funkcji **Wyślij testowe** w zestawie narzędzi **Rozwiązywanie problemów** na stronie centrum powiadomień, jak pokazano na poniższym zrzucie ekranu.</span><span class="sxs-lookup"><span data-stu-id="4e03b-149">You can test receiving push notifications in your app by sending notifications in the [Azure Portal] via the **Test Send** capability in the **Troubleshooting** toolset, right in the notification hub page, as shown in the screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="4e03b-150">Powiadomienia wypychane są zwykle wysyłane za pośrednictwem usługi zaplecza, takiej jak Mobile Services czy ASP.NET, z użyciem zgodnej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="4e03b-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="4e03b-151">Można również wysyłać powiadomienia wypychane bezpośrednio za pomocą interfejsu API REST, jeśli biblioteka nie jest dostępna w danym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="4e03b-151">You can also use the REST API directly to send push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="4e03b-152">W tym samouczku dla uproszczenia przedstawiono testowanie aplikacji klienckiej przez wysyłanie powiadomień za pomocą zestawu SDK .NET dla usługi Notification Hubs w aplikacji konsoli, a nie za pomocą usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="4e03b-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="4e03b-153">Zalecanym następnym krokiem jest zapoznanie się z samouczkiem [Wysyłanie powiadomień wypychanych do użytkowników przy użyciu usługi Notification Hubs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) dotyczącym wysyłania powiadomień przy użyciu zaplecza ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4e03b-153">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="4e03b-154">Można używać następujących metod wysyłania powiadomień:</span><span class="sxs-lookup"><span data-stu-id="4e03b-154">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="4e03b-155">**Interfejs REST**: powiadomienia wypychane mogą być obsługiwane na dowolnej platformie zaplecza za pomocą [interfejsu REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e03b-155">**REST Interface**:  You can support push notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="4e03b-156">**Zestaw SDK .NET dla usługi Microsoft Azure Notification Hubs**: w menedżerze pakietów NuGet dla programu Visual Studio uruchom polecenie [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="4e03b-156">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="4e03b-157">**Node.js**: [Jak używać usługi Notification Hubs z poziomu środowiska Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4e03b-157">**Node.js** : [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="4e03b-158">**Mobile Apps**: aby zapoznać się z przykładem wysyłania powiadomień z poziomu usługi Azure App Service Mobile Apps zintegrowanej z usługą Notification Hubs, zobacz [Dodawanie powiadomień wypychanych do aplikacji mobilnej](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="4e03b-158">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="4e03b-159">**Java/PHP**: aby zapoznać się z przykładem wysyłania powiadomień wypychanych przy użyciu interfejsów API REST, zobacz „Jak używać usługi Notification Hubs za pomocą języka Java/PHP” ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="4e03b-159">**Java / PHP**: For an example of how to send push notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="4e03b-160">(Opcjonalnie) Wysyłanie powiadomień wypychanych z poziomu aplikacji konsoli .NET</span><span class="sxs-lookup"><span data-stu-id="4e03b-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="4e03b-161">W tej sekcji wyślemy powiadomienia wypychane za pomocą prostej aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="4e03b-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="4e03b-162">Na potrzeby tego przykładu przeniesiemy się do środowiska projektowego systemu Windows, w którym jest już zainstalowany program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e03b-162">For the purposes of this example, we will switch to a Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="4e03b-163">W programie Visual Studio utwórz nową aplikację konsoli języka Visual C#:</span><span class="sxs-lookup"><span data-stu-id="4e03b-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="4e03b-164">W programie Visual Studio kliknij kolejno pozycje **Narzędzia**, **Menedżer pakietów NuGet**, **Konsola menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="4e03b-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="4e03b-165">Powinna zostać wyświetlona Konsola menedżera pakietów zadokowana do dolnej części obszaru roboczego programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e03b-165">The package manager console should appear docked to the bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="4e03b-166">W oknie Konsola menedżera pakietów ustaw nowy projekt aplikacji konsoli jako **Projekt domyślny**, a następnie w oknie konsoli uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4e03b-166">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="4e03b-167">Spowoduje to dodanie odwołania do zestawu SDK usługi Azure Notification Hubs z użyciem <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="4e03b-167">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="4e03b-168">Otwórz plik `Program.cs` i dodaj następującą instrukcję `using` umożliwiającą używanie klas i funkcji platformy Azure w ramach klasy głównej:</span><span class="sxs-lookup"><span data-stu-id="4e03b-168">Open the `Program.cs` file and add the following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="4e03b-169">W klasie `Program` dodaj następującą metodę (pamiętaj o wstawieniu odpowiednich **parametrów połączenia** i **nazwy centrum**):</span><span class="sxs-lookup"><span data-stu-id="4e03b-169">In your `Program` class, add the following method (don't forget to replace the **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="4e03b-170">Dodaj następujące wiersze do metody `Main`:</span><span class="sxs-lookup"><span data-stu-id="4e03b-170">Add the following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="4e03b-171">Naciśnij klawisz F5, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="4e03b-171">Press the F5 key to run the app.</span></span> <span data-ttu-id="4e03b-172">W ciągu kilku sekund na urządzeniu powinno zostać wyświetlone powiadomienie wypychane.</span><span class="sxs-lookup"><span data-stu-id="4e03b-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="4e03b-173">Niezależnie od tego, czy używasz połączenia Wi-Fi, czy sieci danych komórkowych, upewnij się, że urządzenie ma aktywne połączenie z Internetem.</span><span class="sxs-lookup"><span data-stu-id="4e03b-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on the device.</span></span>

<span data-ttu-id="4e03b-174">Wszystkie możliwe ładunki można znaleźć w [Podręczniku programowania powiadomień lokalnych i wypychanych] firmy Apple.</span><span class="sxs-lookup"><span data-stu-id="4e03b-174">You can find all the possible payloads in the Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="4e03b-175">(Opcjonalnie) Wysyłanie powiadomień wypychanych z poziomu usługi mobilnej</span><span class="sxs-lookup"><span data-stu-id="4e03b-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="4e03b-176">W tej sekcji wyślemy powiadomienia wypychane za pomocą usługi mobilnej, za pośrednictwem skryptu węzła.</span><span class="sxs-lookup"><span data-stu-id="4e03b-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="4e03b-177">Aby wysłać powiadomienie przy użyciu usługi mobilnej, wykonaj czynności opisane w temacie [Wprowadzenie do usług Mobile Services], a następnie:</span><span class="sxs-lookup"><span data-stu-id="4e03b-177">To send a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="4e03b-178">Zaloguj się do [klasyczny portal Azure] i wybierz usługę mobilną.</span><span class="sxs-lookup"><span data-stu-id="4e03b-178">Sign in to the [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="4e03b-179">Wybierz kartę **Harmonogram** na górnym pasku.</span><span class="sxs-lookup"><span data-stu-id="4e03b-179">Select the **Scheduler** tab on the top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="4e03b-180">Utwórz nowe zadanie zaplanowane, wstaw nazwę i wybierz opcję **Na żądanie**.</span><span class="sxs-lookup"><span data-stu-id="4e03b-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="4e03b-181">Po utworzeniu zadania kliknij jego nazwę.</span><span class="sxs-lookup"><span data-stu-id="4e03b-181">When the job is created, click the job name.</span></span> <span data-ttu-id="4e03b-182">Następnie kliknij kartę **Skrypt** na górnym pasku.</span><span class="sxs-lookup"><span data-stu-id="4e03b-182">Then click the **Script** tab on the top bar.</span></span>
5. <span data-ttu-id="4e03b-183">Wstaw następujący skrypt w funkcji harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="4e03b-183">Insert the following script inside your scheduler function.</span></span> <span data-ttu-id="4e03b-184">Pamiętaj o zastąpieniu tekstu zastępczego uzyskanymi wcześniej wartościami: nazwą centrum powiadomień i parametrami połączenia *DefaultFullSharedAccessSignature*.</span><span class="sxs-lookup"><span data-stu-id="4e03b-184">Make sure to replace the placeholders with your notification hub name and the connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="4e03b-185">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4e03b-185">Click **Save**.</span></span>
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. <span data-ttu-id="4e03b-186">Kliknij pozycję **Uruchom raz** na dolnym pasku.</span><span class="sxs-lookup"><span data-stu-id="4e03b-186">Click **Run Once** on the bottom bar.</span></span> <span data-ttu-id="4e03b-187">Na urządzeniu powinien zostać wyświetlony alert.</span><span class="sxs-lookup"><span data-stu-id="4e03b-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e03b-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4e03b-188">Next steps</span></span>
<span data-ttu-id="4e03b-189">W tym prostym przykładzie wysłano powiadomienia wypychane do wszystkich urządzeń z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="4e03b-189">In this simple example, you broadcasted push notifications to all your iOS devices.</span></span> <span data-ttu-id="4e03b-190">Aby skierować je do określonych użytkowników, zapoznaj się z samouczkiem [Wysyłanie powiadomień wypychanych do użytkowników przy użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="4e03b-190">In order to target specific users, refer to the tutorial [Use Notification Hubs to push notifications to users].</span></span> <span data-ttu-id="4e03b-191">Jeśli chcesz podzielić użytkowników na grupy zainteresowań, zobacz [Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="4e03b-191">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="4e03b-192">Aby uzyskać więcej informacji na temat korzystania z usługi Notification Hubs, zobacz [Wskazówki dotyczące usługi Notification Hubs] oraz [Poradnik dotyczący usługi Notification Hubs dla systemu iOS].</span><span class="sxs-lookup"><span data-stu-id="4e03b-192">Learn more about how to use Notification Hubs in [Notification Hubs Guidance] and in the [Notification Hubs How-To for iOS].</span></span>

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

<span data-ttu-id="4e03b-193">[Wprowadzenie do usług Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span><span class="sxs-lookup"><span data-stu-id="4e03b-193">[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios</span></span>
<span data-ttu-id="4e03b-194">[klasyczny portal Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="4e03b-194">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="4e03b-195">[Wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="4e03b-195">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
<span data-ttu-id="4e03b-196">[Poradnik dotyczący usługi Notification Hubs dla systemu iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span><span class="sxs-lookup"><span data-stu-id="4e03b-196">[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx</span></span>
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

<span data-ttu-id="4e03b-197">[Wysyłanie powiadomień wypychanych do użytkowników przy użyciu usługi Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="4e03b-197">[Use Notification Hubs to push notifications to users]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="4e03b-198">[Wysyłanie najważniejszych wiadomości przy użyciu usługi Notification Hubs]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="4e03b-198">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

<span data-ttu-id="4e03b-199">[Podręczniku programowania powiadomień lokalnych i wypychanych]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span><span class="sxs-lookup"><span data-stu-id="4e03b-199">[Local and Push Notification Programming Guide]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1</span></span>
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
<span data-ttu-id="4e03b-200">[Program Xamarin Studio]: http://xamarin.com/download</span><span class="sxs-lookup"><span data-stu-id="4e03b-200">[Xamarin Studio]: http://xamarin.com/download</span></span>
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
<span data-ttu-id="4e03b-201">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="4e03b-201">[Azure Portal]: https://portal.azure.com</span></span>
