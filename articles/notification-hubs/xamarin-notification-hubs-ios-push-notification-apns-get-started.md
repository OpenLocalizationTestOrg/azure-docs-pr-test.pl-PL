---
title: "aaaiOS powiadomień wypychanych przy użyciu usługi Notification Hubs dla aplikacji platformy Xamarin | Dokumentacja firmy Microsoft"
description: "Z tego samouczka dowiesz się, jak toosend usługi Azure Notification Hubs toouse wypychanie powiadomień tooa Xamarin iOS aplikacji."
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
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a><span data-ttu-id="94d93-104">Wysyłanie powiadomień wypychanych do aplikacji platformy Xamarin dla systemu iOS przy użyciu usługi Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="94d93-104">iOS Push Notifications with Notification Hubs for Xamarin apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="94d93-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="94d93-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="94d93-106">toocomplete tego samouczka, musi mieć aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="94d93-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="94d93-107">Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="94d93-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="94d93-108">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="94d93-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="94d93-109">Ten samouczek pokazuje, jak toosend usługi Azure Notification Hubs toouse wypychanych aplikacji dla systemu iOS tooan powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="94d93-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooan iOS application.</span></span>
<span data-ttu-id="94d93-110">Utworzysz pustą aplikację platformy Xamarin.iOS służącą do odbierania powiadomień wypychanych przy użyciu hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span><span class="sxs-lookup"><span data-stu-id="94d93-110">You'll create a blank Xamarin.iOS app that receives push notifications by using hello [Apple Push Notification Service (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html).</span></span> <span data-ttu-id="94d93-111">Po zakończeniu będziesz w stanie toouse Twojego toobroadcast Centrum powiadomień wypychanych powiadomienia tooall hello urządzeń z tą aplikacją.</span><span class="sxs-lookup"><span data-stu-id="94d93-111">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span> <span data-ttu-id="94d93-112">Witaj gotowy kod jest dostępny w hello [aplikacji NotificationHubs] [ GitHub] próbki.</span><span class="sxs-lookup"><span data-stu-id="94d93-112">hello finished code is available in hello [NotificationHubs app][GitHub] sample.</span></span>

<span data-ttu-id="94d93-113">W tym samouczku przedstawiono scenariusz wysyłania powiadomień wypychanych prostego powitania z usługą Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="94d93-113">This tutorial demonstrates hello simple push message broadcast scenario with Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94d93-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="94d93-114">Prerequisites</span></span>
<span data-ttu-id="94d93-115">Ten samouczek wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="94d93-115">This tutorial requires hello following:</span></span>

* <span data-ttu-id="94d93-116">[Xcode 6.0][Install Xcode]</span><span class="sxs-lookup"><span data-stu-id="94d93-116">[Xcode 6.0][Install Xcode]</span></span>
* <span data-ttu-id="94d93-117">Urządzenie zgodne z systemem iOS 7.0 (lub nowszą wersją)</span><span class="sxs-lookup"><span data-stu-id="94d93-117">An iOS 7.0 (or later version) compatible device</span></span>
* <span data-ttu-id="94d93-118">Członkostwo w programie dla deweloperów systemu iOS</span><span class="sxs-lookup"><span data-stu-id="94d93-118">iOS Developer Program membership</span></span>
* <span data-ttu-id="94d93-119">[Program Xamarin Studio]</span><span class="sxs-lookup"><span data-stu-id="94d93-119">[Xamarin Studio]</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="94d93-120">Ze względu na wymagania dotyczące konfiguracji powiadomień wypychanych systemu iOS należy wdrożyć i przetestować aplikację przykładową hello na urządzenie fizyczne z systemem iOS (iPhone i iPad) zamiast w symulatorze hello.</span><span class="sxs-lookup"><span data-stu-id="94d93-120">Because of configuration requirements for iOS push notifications, you must deploy and test hello sample application on a physical iOS device (iPhone or iPad) instead of in hello simulator.</span></span>
  > 
  > 

<span data-ttu-id="94d93-121">Wykonanie czynności opisanych w tym samouczku jest wymaganiem wstępnym dla wszystkich innych samouczków usług Notification Hubs dotyczących aplikacji platformy Xamarin.iOS.</span><span class="sxs-lookup"><span data-stu-id="94d93-121">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Xamarin iOS apps.</span></span>

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a><span data-ttu-id="94d93-122">Konfigurowanie centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="94d93-122">Configure your notification hub</span></span>
<span data-ttu-id="94d93-123">Ta sekcja przeprowadzi Cię przez proces tworzenia nowego centrum powiadomień i konfigurowania uwierzytelniania w usłudze APNS przy użyciu hello **.p12** utworzony certyfikat wypychania.</span><span class="sxs-lookup"><span data-stu-id="94d93-123">This section walks you through creating a new notification hub and configuring authentication with APNS using hello **.p12** push certificate that you created.</span></span> <span data-ttu-id="94d93-124">Jeśli chcesz toouse Centrum powiadomień, które zostały już utworzone, możesz pominąć toostep 5.</span><span class="sxs-lookup"><span data-stu-id="94d93-124">If you want toouse a notification hub that you have already created, you can skip toostep 5.</span></span>

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p><span data-ttu-id="94d93-125">Ponieważ chcemy tooconfigure hello APNS połączenia w hello portalu Azure Otwórz ustawienia Centrum powiadomień, kliknij Hub na <b>usługi powiadomień</b>, a następnie kliknij przycisk hello <b>Apple (APNS)</b> element na liście hello.</span><span class="sxs-lookup"><span data-stu-id="94d93-125">As we want tooconfigure hello APNS connection, in hello Azure Portal, open your Notification Hub settings, ande click on <b>Notification Services</b>, and then click hello <b>Apple (APNS)</b> item in hello list.</span></span> <span data-ttu-id="94d93-126">Po zakończeniu kliknij <b>Przekaż certyfikat</b> i wybierz hello <b>.p12</b> certyfikat wyeksportowany wcześniej, a także hello hasło dla certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="94d93-126">Once done, click on <b>Upload Certificate</b> and select hello <b>.p12</b> certificate that you exported earlier, as well as hello password for hello certificate.</span></span></p>

<p><span data-ttu-id="94d93-127">Upewnij się, że tooselect <b>piaskownicy</b> trybu, ponieważ będą wysyłane wypychania wiadomości w środowisku projektowym.</span><span class="sxs-lookup"><span data-stu-id="94d93-127">Make sure tooselect <b>Sandbox</b> mode since you will be sending push messages in a development environment.</span></span> <span data-ttu-id="94d93-128">Należy używać tylko hello <b>produkcji</b> toosend toousers powiadomień wypychanych, którzy kupili już twoją aplikację w sklepie hello ustawienie.</span><span class="sxs-lookup"><span data-stu-id="94d93-128">Only use hello <b>Production</b> setting if you want toosend push notifications toousers who already purchased your app from hello store.</span></span></p>
</li>
</ol>
<span data-ttu-id="94d93-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span><span class="sxs-lookup"><span data-stu-id="94d93-129">&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)</span></span>

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

<span data-ttu-id="94d93-130">Centrum powiadomień jest teraz skonfigurowany toowork przy użyciu usługi APNS i mieć tooregister ciągów połączenia hello aplikacji oraz wysyłać powiadomienia wypychane.</span><span class="sxs-lookup"><span data-stu-id="94d93-130">Your notification hub is now configured toowork with APNS, and you have hello connection strings tooregister your app and send push notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="94d93-131">Łączenie aplikacji toohello Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="94d93-131">Connect your app toohello notification hub</span></span>
#### <a name="create-a-new-project"></a><span data-ttu-id="94d93-132">Tworzenie nowego projektu</span><span class="sxs-lookup"><span data-stu-id="94d93-132">Create a new project</span></span>
1. <span data-ttu-id="94d93-133">W programie Xamarin Studio Utwórz nowy projekt dla systemu iOS, a następnie wybierz hello **Unified API** > **pojedynczą aplikacją widoku** szablonu.</span><span class="sxs-lookup"><span data-stu-id="94d93-133">In Xamarin Studio, create a new iOS project and select hello **Unified API** > **Single View Application** template.</span></span>
   
     ![Xamarin Studio — wybieranie typu aplikacji][31]
2. <span data-ttu-id="94d93-135">Dodaj odwołanie do składnika Azure Messaging toohello.</span><span class="sxs-lookup"><span data-stu-id="94d93-135">Add a reference toohello Azure Messaging component.</span></span> <span data-ttu-id="94d93-136">W widoku Solution hello, kliknij prawym przyciskiem myszy hello **składniki** folderu projektu i wybierz polecenie **Uzyskaj więcej składników**.</span><span class="sxs-lookup"><span data-stu-id="94d93-136">In hello Solution view, right-click hello **Components** folder for your project and choose **Get More Components**.</span></span> <span data-ttu-id="94d93-137">Wyszukaj hello **Azure Messaging** składników i Dodaj hello składnika tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="94d93-137">Search for hello **Azure Messaging** component and add hello component tooyour project.</span></span>
3. <span data-ttu-id="94d93-138">W **AppDelegate.cs**, Dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="94d93-138">In **AppDelegate.cs**, add hello following using statement:</span></span>
   
        using WindowsAzure.Messaging;
4. <span data-ttu-id="94d93-139">Zadeklaruj wystąpienie **SBNotificationHub**:</span><span class="sxs-lookup"><span data-stu-id="94d93-139">Declare an instance of **SBNotificationHub**:</span></span>
   
        private SBNotificationHub Hub { get; set; }
5. <span data-ttu-id="94d93-140">Utwórz **Constants.cs** klasy z hello następujące zmienne:</span><span class="sxs-lookup"><span data-stu-id="94d93-140">Create a **Constants.cs** class with hello following variables:</span></span>
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. <span data-ttu-id="94d93-141">W **AppDelegate.cs**, zaktualizuj **FinishedLaunching()** toomatch hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="94d93-141">In **AppDelegate.cs**, update **FinishedLaunching()** toomatch hello following:</span></span>
   
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
7. <span data-ttu-id="94d93-142">Zastąpienie hello **RegisteredForRemoteNotifications()** metody w **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="94d93-142">Override hello **RegisteredForRemoteNotifications()** method in **AppDelegate.cs**:</span></span>
   
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
8. <span data-ttu-id="94d93-143">Zastąpienie hello **ReceivedRemoteNotification()** metody w **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="94d93-143">Override hello **ReceivedRemoteNotification()** method in **AppDelegate.cs**:</span></span>
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. <span data-ttu-id="94d93-144">Utwórz następujące hello **ProcessNotification()** metody w **AppDelegate.cs**:</span><span class="sxs-lookup"><span data-stu-id="94d93-144">Create hello following **ProcessNotification()** method in **AppDelegate.cs**:</span></span>
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
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
   > <span data-ttu-id="94d93-145">Możesz wybrać toooverride **FailedToRegisterForRemoteNotifications()** toohandle sytuacjach, takich jak brak połączenia z siecią.</span><span class="sxs-lookup"><span data-stu-id="94d93-145">You can choose toooverride **FailedToRegisterForRemoteNotifications()** toohandle situations such as no network connection.</span></span> <span data-ttu-id="94d93-146">Jest to szczególnie istotne, gdzie hello użytkownik może uruchomić aplikację w trybie offline (np. w trybie Samolotowym) i ma wypychania toohandle wiadomości scenariusze tooyour określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94d93-146">This is especially important where hello user might start your application in offline mode (e.g. Airplane) and you want toohandle push messaging scenarios specific tooyour app.</span></span>
   > 
   > 
10. <span data-ttu-id="94d93-147">Uruchamianie aplikacji hello na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="94d93-147">Run hello app on your device.</span></span>

## <a name="sending-push-notifications"></a><span data-ttu-id="94d93-148">Wysyłanie powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="94d93-148">Sending Push Notifications</span></span>
<span data-ttu-id="94d93-149">Możesz przetestować odbieranie powiadomień wypychanych w aplikacji, wysyłając powiadomienia w hello [Azure Portal] za pośrednictwem hello **wysyłanie testowe** możliwości w hello **Rozwiązywanie problemów** zestaw narzędzi, bezpośrednio w hello stronie Centrum powiadomień, jak pokazano na powitania ekranu poniżej.</span><span class="sxs-lookup"><span data-stu-id="94d93-149">You can test receiving push notifications in your app by sending notifications in hello [Azure Portal] via hello **Test Send** capability in hello **Troubleshooting** toolset, right in hello notification hub page, as shown in hello screen below.</span></span>

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

<span data-ttu-id="94d93-150">Powiadomienia wypychane są zwykle wysyłane za pośrednictwem usługi zaplecza, takiej jak Mobile Services czy ASP.NET, z użyciem zgodnej biblioteki.</span><span class="sxs-lookup"><span data-stu-id="94d93-150">Push notifications are normally sent through a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="94d93-151">Umożliwia także hello interfejsu API REST bezpośrednio wiadomości wypychanych toosend, jeśli biblioteka nie jest dostępna w danym scenariuszu.</span><span class="sxs-lookup"><span data-stu-id="94d93-151">You can also use hello REST API directly toosend push messages if a library is not available in your scenario.</span></span> 

<span data-ttu-id="94d93-152">W tym samouczku będziemy Zachowaj prostotę i przedstawiono testowanie aplikacji klienckiej przez wysyłanie powiadomień dotyczących usługi notification hubs w aplikacji konsoli usługi zaplecza przy użyciu hello zestawu .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="94d93-152">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="94d93-153">Firma Microsoft zaleca hello [toousers powiadomienia toopush użyciu usługi Notification Hubs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) samouczka jako hello następnego kroku do wysyłania powiadomień z zaplecza ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="94d93-153">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="94d93-154">Jednak po podejścia hello może służyć do wysyłania powiadomień:</span><span class="sxs-lookup"><span data-stu-id="94d93-154">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="94d93-155">**Interfejs REST**: powiadomienia wypychane mogą być obsługiwane na dowolnej platformie zaplecza za pomocą hello [interfejsu REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="94d93-155">**REST Interface**:  You can support push notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="94d93-156">**Microsoft Azure powiadomień koncentratory .NET SDK**: W hello Menedżera pakietów Nuget dla programu Visual Studio, uruchom [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="94d93-156">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="94d93-157">**Node.js** : [jak toouse centra powiadomień w oprogramowaniu Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="94d93-157">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>

<span data-ttu-id="94d93-158">**Aplikacje mobilne**: na przykład jak toosend powiadomień z zaplecza Azure App Service Mobile Apps, który jest zintegrowany z usługą Notification Hubs, zobacz [aplikacji mobilnej tooyour powiadomień wypychanych Dodaj](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="94d93-158">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>

* <span data-ttu-id="94d93-159">**Java / PHP**: przykład sposobu toosend powiadomień wypychanych przy użyciu hello interfejsów API REST, zobacz "jak toouse usługi Notification Hubs za pomocą języka Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="94d93-159">**Java / PHP**: For an example of how toosend push notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a><span data-ttu-id="94d93-160">(Opcjonalnie) Wysyłanie powiadomień wypychanych z poziomu aplikacji konsoli .NET</span><span class="sxs-lookup"><span data-stu-id="94d93-160">(Optional) Send Push Notifications from a .NET Console App</span></span>
<span data-ttu-id="94d93-161">W tej sekcji wyślemy powiadomienia wypychane za pomocą prostej aplikacji konsoli .NET.</span><span class="sxs-lookup"><span data-stu-id="94d93-161">In this section, we will send push notifications by using a simple .NET console app.</span></span> <span data-ttu-id="94d93-162">Celach hello tego przykładu przeniesiemy się tooa środowiska projektowego systemu Windows, który ma już zainstalowanego programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94d93-162">For hello purposes of this example, we will switch tooa Windows development environment that has Visual Studio already installed.</span></span>

1. <span data-ttu-id="94d93-163">W programie Visual Studio utwórz nową aplikację konsoli języka Visual C#:</span><span class="sxs-lookup"><span data-stu-id="94d93-163">In Visual Studio, create a new Visual C# console application:</span></span>
   
       ![Visual Studio - Create a new console application][213]
2. <span data-ttu-id="94d93-164">W programie Visual Studio kliknij kolejno pozycje **Narzędzia**, **Menedżer pakietów NuGet**, **Konsola menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="94d93-164">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="94d93-165">konsoli Menedżera pakietów Hello powinna zostać wyświetlona zadokowanych toohello dolnej części obszaru roboczego programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94d93-165">hello package manager console should appear docked toohello bottom of your Visual Studio workspace.</span></span>
3. <span data-ttu-id="94d93-166">W oknie konsoli Menedżera pakietów hello, ustaw hello **domyślny projekt** tooyour nowy projekt aplikacji konsoli, a następnie w oknie konsoli hello, wykonaj następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="94d93-166">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="94d93-167">Spowoduje to dodanie toohello odwołanie do zestawu SDK usługi Azure Notification Hubs za pomocą hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pakietu Microsoft.Azure.Notification Hubs NuGet</a>.</span><span class="sxs-lookup"><span data-stu-id="94d93-167">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="94d93-168">Otwórz hello `Program.cs` i dodaj następujące hello `using` instrukcji zapewnienie, że możemy użyć Azure klasy i funkcje w ramach klasy głównej:</span><span class="sxs-lookup"><span data-stu-id="94d93-168">Open hello `Program.cs` file and add hello following `using` statement, ensuring that we can use Azure classes and functions within your main class:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="94d93-169">W Twojej `Program` klasy, Dodaj następujące metody hello (nie zapomnij tooreplace hello **ciąg połączenia** i **nazwy centrum**):</span><span class="sxs-lookup"><span data-stu-id="94d93-169">In your `Program` class, add hello following method (don't forget tooreplace hello **connection string** and **hub name**):</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. <span data-ttu-id="94d93-170">Dodaj hello następujące wiersze w Twojej `Main` metody:</span><span class="sxs-lookup"><span data-stu-id="94d93-170">Add hello following lines in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="94d93-171">Naciśnij klawisz hello F5 klucza toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="94d93-171">Press hello F5 key toorun hello app.</span></span> <span data-ttu-id="94d93-172">W ciągu kilku sekund na urządzeniu powinno zostać wyświetlone powiadomienie wypychane.</span><span class="sxs-lookup"><span data-stu-id="94d93-172">Within seconds, you should see a push notification appear on your device.</span></span> <span data-ttu-id="94d93-173">Czy korzystasz z sieci Wi-Fi i sieci danych komórkowych, upewnij się, że masz aktywne połączenie internetowe na urządzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="94d93-173">Whether you are using Wi-Fi or a cellular data network, make sure that you have an active internet connection on hello device.</span></span>

<span data-ttu-id="94d93-174">Wszystkie możliwe ładunki hello można znaleźć w hello Apple [lokalnych i wypychanych Podręcznik programowania powiadomień].</span><span class="sxs-lookup"><span data-stu-id="94d93-174">You can find all hello possible payloads in hello Apple [Local and Push Notification Programming Guide].</span></span>

#### <a name="optional-send-notifications-from-a-mobile-service"></a><span data-ttu-id="94d93-175">(Opcjonalnie) Wysyłanie powiadomień wypychanych z poziomu usługi mobilnej</span><span class="sxs-lookup"><span data-stu-id="94d93-175">(Optional) Send Notifications from a Mobile Service</span></span>
<span data-ttu-id="94d93-176">W tej sekcji wyślemy powiadomienia wypychane za pomocą usługi mobilnej, za pośrednictwem skryptu węzła.</span><span class="sxs-lookup"><span data-stu-id="94d93-176">In this section, we will send push notifications using a mobile service through a node script.</span></span>

<span data-ttu-id="94d93-177">toosend powiadomienia za pomocą usługi mobilnej, wykonaj [wprowadzenie do usług Mobile Services], a następnie:</span><span class="sxs-lookup"><span data-stu-id="94d93-177">toosend a notification by using a mobile service, follow [Get started with Mobile Services], and then:</span></span>

1. <span data-ttu-id="94d93-178">Zaloguj się toohello [klasycznego portalu Azure]i wybierz usługę mobilną.</span><span class="sxs-lookup"><span data-stu-id="94d93-178">Sign in toohello [Azure Classic Portal], and select your mobile service.</span></span>
2. <span data-ttu-id="94d93-179">Wybierz hello **harmonogramu** kartę w górnej części hello.</span><span class="sxs-lookup"><span data-stu-id="94d93-179">Select hello **Scheduler** tab on hello top.</span></span>
   
       ![Azure Classic Portal - Scheduler][215]
3. <span data-ttu-id="94d93-180">Utwórz nowe zadanie zaplanowane, wstaw nazwę i wybierz opcję **Na żądanie**.</span><span class="sxs-lookup"><span data-stu-id="94d93-180">Create a new scheduled job, insert a name, and select **On demand**.</span></span>
   
       ![Azure Classic Portal - Create new job][216]
4. <span data-ttu-id="94d93-181">Po utworzeniu zadania powitania kliknij nazwę zadania hello.</span><span class="sxs-lookup"><span data-stu-id="94d93-181">When hello job is created, click hello job name.</span></span> <span data-ttu-id="94d93-182">Następnie kliknij przycisk hello **skryptu** kartę na górnym pasku hello.</span><span class="sxs-lookup"><span data-stu-id="94d93-182">Then click hello **Script** tab on hello top bar.</span></span>
5. <span data-ttu-id="94d93-183">Wstaw hello następującego skryptu w funkcji harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="94d93-183">Insert hello following script inside your scheduler function.</span></span> <span data-ttu-id="94d93-184">Wprowadź symbole zastępcze hello tooreplace się z powiadomienia Centrum nazwy i hello parametrów połączenia dla *DefaultFullSharedAccessSignature* uzyskany wcześniej.</span><span class="sxs-lookup"><span data-stu-id="94d93-184">Make sure tooreplace hello placeholders with your notification hub name and hello connection string for *DefaultFullSharedAccessSignature* that you obtained earlier.</span></span> <span data-ttu-id="94d93-185">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="94d93-185">Click **Save**.</span></span>
   
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
6. <span data-ttu-id="94d93-186">Kliknij przycisk **uruchom raz** na powitania dolnym pasku.</span><span class="sxs-lookup"><span data-stu-id="94d93-186">Click **Run Once** on hello bottom bar.</span></span> <span data-ttu-id="94d93-187">Na urządzeniu powinien zostać wyświetlony alert.</span><span class="sxs-lookup"><span data-stu-id="94d93-187">You should receive an alert on your device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94d93-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="94d93-188">Next steps</span></span>
<span data-ttu-id="94d93-189">W tym prostym przykładzie wysłano tooall powiadomień wypychanych urządzeń z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="94d93-189">In this simple example, you broadcasted push notifications tooall your iOS devices.</span></span> <span data-ttu-id="94d93-190">W kolejności tootarget określonych użytkowników, zobacz samouczek toohello [toousers powiadomienia toopush użyciu usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="94d93-190">In order tootarget specific users, refer toohello tutorial [Use Notification Hubs toopush notifications toousers].</span></span> <span data-ttu-id="94d93-191">Jeśli chcesz toosegment użytkowników na grupy zainteresowań, możesz przeczytać [toosend użyciu usługi Notification Hubs fundamentalne wiadomości].</span><span class="sxs-lookup"><span data-stu-id="94d93-191">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="94d93-192">Dowiedz się więcej na temat toouse centra powiadomień w [wskazówki dotyczące usługi Notification Hubs] w hello [iOS centra powiadomień w sposób toofor].</span><span class="sxs-lookup"><span data-stu-id="94d93-192">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance] and in hello [Notification Hubs How-toofor iOS].</span></span>

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

[wprowadzenie do usług Mobile Services]: /develop/mobile/tutorials/get-started-xamarin-ios
[klasycznego portalu Azure]: https://manage.windowsazure.com/
[wskazówki dotyczące usługi Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx
[iOS centra powiadomień w sposób toofor]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[toousers powiadomienia toopush użyciu usługi Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet
[toosend użyciu usługi Notification Hubs fundamentalne wiadomości]: /manage/services/notification-hubs/breaking-news-dotnet

[lokalnych i wypychanych Podręcznik programowania powiadomień]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Program Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure Portal]: https://portal.azure.com
