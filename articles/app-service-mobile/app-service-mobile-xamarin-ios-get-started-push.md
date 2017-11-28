---
title: "Dodawanie powiadomień wypychanych do aplikacji platformy Xamarin.iOS za pomocą usługi Azure App Service"
description: "Dowiedz się, jak używać usługi Azure App Service do wysyłania powiadomień wypychanych do aplikacji platformy Xamarin.iOS"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 2921214a-49f8-45e1-a306-a85ce21defca
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: bf922e49c4c92d0065817a5dd6c7d10a04737304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinios-app"></a><span data-ttu-id="52b37-103">Dodawanie powiadomień wypychanych do aplikacji platformy Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="52b37-103">Add push notifications to your Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="52b37-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="52b37-104">Overview</span></span>
<span data-ttu-id="52b37-105">W tym samouczku, dodawanie powiadomień wypychanych do [Xamarin.iOS szybki start](app-service-mobile-xamarin-ios-get-started.md) projektu, aby powiadomienia wypychane są wysyłane do urządzenia, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="52b37-105">In this tutorial, you add push notifications to the [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="52b37-106">Jeśli nie używasz Projekt serwera pobrany szybki start, konieczne będzie pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="52b37-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="52b37-107">Zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="52b37-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52b37-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="52b37-108">Prerequisites</span></span>
* <span data-ttu-id="52b37-109">Zakończenie [szybkiego startu Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="52b37-109">Complete the [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="52b37-110">Urządzenie fizyczne z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="52b37-110">A physical iOS device.</span></span> <span data-ttu-id="52b37-111">Powiadomienia wypychane nie są obsługiwane za pomocą symulatora systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="52b37-111">Push notifications are not supported by the iOS simulator.</span></span>

## <a name="register-the-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="52b37-112">Rejestrowanie aplikacji dla powiadomień wypychanych w portalu dla deweloperów firmy Apple</span><span class="sxs-lookup"><span data-stu-id="52b37-112">Register the app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-to-send-push-notifications"></a><span data-ttu-id="52b37-113">Konfigurowanie aplikacji mobilnej do wysyłania powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="52b37-113">Configure your Mobile App to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-the-server-project-to-send-push-notifications"></a><span data-ttu-id="52b37-114">Aktualizowanie projektów serwera do wysyłania powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="52b37-114">Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="52b37-115">Konfigurowanie projektu platformy Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="52b37-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="52b37-116">Dodawanie powiadomień wypychanych do aplikacji</span><span class="sxs-lookup"><span data-stu-id="52b37-116">Add push notifications to your app</span></span>
1. <span data-ttu-id="52b37-117">W **QSTodoService**, dodaj następującą właściwość, aby **AppDelegate** można uzyskać klientów urządzeń przenośnych:</span><span class="sxs-lookup"><span data-stu-id="52b37-117">In **QSTodoService**, add the following property so that **AppDelegate** can acquire the mobile client:</span></span>
   
            public MobileServiceClient GetClient {
            get
            {
                return client;
            }
            private set
            {
                client = value;
            }
        }
2. <span data-ttu-id="52b37-118">Dodaj następujące `using` instrukcji na początku **AppDelegate.cs** pliku.</span><span class="sxs-lookup"><span data-stu-id="52b37-118">Add the following `using` statement to the top of the **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="52b37-119">W **AppDelegate**, Zastąp **FinishedLaunching** zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="52b37-119">In **AppDelegate**, override the **FinishedLaunching** event:</span></span>
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            // registers for push for iOS8
            var settings = UIUserNotificationSettings.GetSettingsForTypes(
                UIUserNotificationType.Alert
                | UIUserNotificationType.Badge
                | UIUserNotificationType.Sound,
                new NSSet());
   
            UIApplication.SharedApplication.RegisterUserNotificationSettings(settings);
            UIApplication.SharedApplication.RegisterForRemoteNotifications();
   
            return true;
        }
4. <span data-ttu-id="52b37-120">W tym samym pliku, Zastąp **RegisteredForRemoteNotifications** zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="52b37-120">In the same file, override the **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="52b37-121">W tym kodzie rejestrowania dla powiadomień prostego szablonu, który zostanie wysłany na wszystkich platformach obsługiwanych przez serwer.</span><span class="sxs-lookup"><span data-stu-id="52b37-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by the server.</span></span>
   
    <span data-ttu-id="52b37-122">Aby uzyskać więcej informacji dotyczących szablonów z usługą Notification Hubs, zobacz [szablony](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="52b37-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            MobileServiceClient client = QSTodoService.DefaultService.GetClient;

            const string templateBodyAPNS = "{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            JObject templates = new JObject();
            templates["genericMessage"] = new JObject
            {
                {"body", templateBodyAPNS}
            };

            // Register for push with your mobile app
            var push = client.GetPush();
            push.RegisterAsync(deviceToken, templates);
        }


1. <span data-ttu-id="52b37-123">Następnie zastąp **DidReceivedRemoteNotification** zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="52b37-123">Then, override the **DidReceivedRemoteNotification** event:</span></span>
   
        public override void DidReceiveRemoteNotification (UIApplication application, NSDictionary userInfo, Action<UIBackgroundFetchResult> completionHandler)
        {
            NSDictionary aps = userInfo.ObjectForKey(new NSString("aps")) as NSDictionary;
   
            string alert = string.Empty;
            if (aps.ContainsKey(new NSString("alert")))
                alert = (aps [new NSString("alert")] as NSString).ToString();
   
            //show alert
            if (!string.IsNullOrEmpty(alert))
            {
                UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                avAlert.Show();
            }
        }

<span data-ttu-id="52b37-124">Aplikacja jest teraz zaktualizowana do obsługi powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="52b37-124">Your app is now updated to support push notifications.</span></span>

## <span data-ttu-id="52b37-125"><a name="test"></a>Testowych powiadomień wypychanych w aplikacji</span><span class="sxs-lookup"><span data-stu-id="52b37-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="52b37-126">Naciśnij klawisz **Uruchom** przycisk, aby skompilować projekt i uruchomić aplikację w stanie urządzenia z systemem iOS, a następnie kliknij przycisk **OK** do akceptowania powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="52b37-126">Press the **Run** button to build the project and start the app in an iOS capable device, then click **OK** to accept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="52b37-127">Należy jawnie zaakceptować powiadomień wypychanych z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="52b37-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="52b37-128">To żądanie występuje tylko aplikacja jest uruchamiana po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="52b37-128">This request only occurs the first time that the app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="52b37-129">W aplikacji wpisz zadania, a następnie kliknij przycisk plus (**+**) ikona.</span><span class="sxs-lookup"><span data-stu-id="52b37-129">In the app, type a task, and then click the plus (**+**) icon.</span></span>
3. <span data-ttu-id="52b37-130">Sprawdź, czy powiadomienie o odebraniu, a następnie kliknij przycisk **OK** na odrzucenie powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="52b37-130">Verify that a notification is received, then click **OK** to dismiss the notification.</span></span>
4. <span data-ttu-id="52b37-131">Powtórz krok 2 natychmiast zamknij aplikację, a następnie sprawdź, czy powiadomienie jest widoczne.</span><span class="sxs-lookup"><span data-stu-id="52b37-131">Repeat step 2 and immediately close the app, then verify that a notification is shown.</span></span>

<span data-ttu-id="52b37-132">W tym samouczku została pomyślnie ukończona.</span><span class="sxs-lookup"><span data-stu-id="52b37-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



