---
title: "aaaAdd aplikacji platformy Xamarin.iOS tooyour powiadomienia wypychane z usługi aplikacji Azure"
description: "Dowiedz się, jak toosend usłudze Azure App Service toouse push aplikacji platformy Xamarin.iOS tooyour powiadomienia"
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
ms.openlocfilehash: 3e6439aee4f3fe0f60b9786d0bbfd74c4f5e52d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinios-app"></a><span data-ttu-id="17a0b-103">Dodaj tooyour powiadomienia wypychane aplikacji platformy Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="17a0b-103">Add push notifications tooyour Xamarin.iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="17a0b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="17a0b-104">Overview</span></span>
<span data-ttu-id="17a0b-105">W tym samouczku, możesz dodać toohello powiadomień wypychanych [Xamarin.iOS szybki start](app-service-mobile-xamarin-ios-get-started.md) projektu, aby powiadomienie wypychane zostanie wysłane toohello urządzenia, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="17a0b-105">In this tutorial, you add push notifications toohello [Xamarin.iOS quick start](app-service-mobile-xamarin-ios-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="17a0b-106">Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="17a0b-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="17a0b-107">Zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="17a0b-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17a0b-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="17a0b-108">Prerequisites</span></span>
* <span data-ttu-id="17a0b-109">Zakończenie hello [szybkiego startu Xamarin.iOS](app-service-mobile-xamarin-ios-get-started.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="17a0b-109">Complete hello [Xamarin.iOS quickstart](app-service-mobile-xamarin-ios-get-started.md) tutorial.</span></span>
* <span data-ttu-id="17a0b-110">Urządzenie fizyczne z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="17a0b-110">A physical iOS device.</span></span> <span data-ttu-id="17a0b-111">Powiadomienia wypychane nie są obsługiwane przez hello symulatora systemu iOS.</span><span class="sxs-lookup"><span data-stu-id="17a0b-111">Push notifications are not supported by hello iOS simulator.</span></span>

## <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a><span data-ttu-id="17a0b-112">Rejestrowanie aplikacji hello powiadomień wypychanych na portalu dla deweloperów firmy Apple</span><span class="sxs-lookup"><span data-stu-id="17a0b-112">Register hello app for push notifications on Apple's developer portal</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-your-mobile-app-toosend-push-notifications"></a><span data-ttu-id="17a0b-113">Konfigurowanie powiadomień wypychanych toosend aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="17a0b-113">Configure your Mobile App toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a name="update-hello-server-project-toosend-push-notifications"></a><span data-ttu-id="17a0b-114">Zaktualizuj powiadomień wypychanych toosend powitania serwera projektu</span><span class="sxs-lookup"><span data-stu-id="17a0b-114">Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="configure-your-xamarinios-project"></a><span data-ttu-id="17a0b-115">Konfigurowanie projektu platformy Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="17a0b-115">Configure your Xamarin.iOS project</span></span>
[!INCLUDE [app-service-mobile-xamarin-ios-configure-project](../../includes/app-service-mobile-xamarin-ios-configure-project.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="17a0b-116">Dodaj aplikację tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="17a0b-116">Add push notifications tooyour app</span></span>
1. <span data-ttu-id="17a0b-117">W **QSTodoService**, Dodaj następujące właściwości hello, aby **AppDelegate** można uzyskać hello klientów urządzeń przenośnych:</span><span class="sxs-lookup"><span data-stu-id="17a0b-117">In **QSTodoService**, add hello following property so that **AppDelegate** can acquire hello mobile client:</span></span>
   
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
2. <span data-ttu-id="17a0b-118">Dodaj następujące hello `using` instrukcji toohello początku hello **AppDelegate.cs** pliku.</span><span class="sxs-lookup"><span data-stu-id="17a0b-118">Add hello following `using` statement toohello top of hello **AppDelegate.cs** file.</span></span>
   
        using Microsoft.WindowsAzure.MobileServices;
        using Newtonsoft.Json.Linq;
3. <span data-ttu-id="17a0b-119">W **AppDelegate**, Zastąp hello **FinishedLaunching** zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="17a0b-119">In **AppDelegate**, override hello **FinishedLaunching** event:</span></span>
   
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
4. <span data-ttu-id="17a0b-120">W hello tego samego pliku, Zastąp hello **RegisteredForRemoteNotifications** zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="17a0b-120">In hello same file, override hello **RegisteredForRemoteNotifications** event.</span></span> <span data-ttu-id="17a0b-121">W tym kodzie rejestrowania dla powiadomień prostego szablonu, który zostanie wysłany na wszystkich platformach obsługiwanych przez serwer hello.</span><span class="sxs-lookup"><span data-stu-id="17a0b-121">In this code you are registering for a simple template notification that will be sent across all supported platforms by hello server.</span></span>
   
    <span data-ttu-id="17a0b-122">Aby uzyskać więcej informacji dotyczących szablonów z usługą Notification Hubs, zobacz [szablony](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="17a0b-122">For more information on templates with Notification Hubs, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>

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


1. <span data-ttu-id="17a0b-123">Następnie zastąp hello **DidReceivedRemoteNotification** zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="17a0b-123">Then, override hello **DidReceivedRemoteNotification** event:</span></span>
   
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

<span data-ttu-id="17a0b-124">Aplikacja jest teraz zaktualizowane toosupport powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="17a0b-124">Your app is now updated toosupport push notifications.</span></span>

## <span data-ttu-id="17a0b-125"><a name="test"></a>Testowych powiadomień wypychanych w aplikacji</span><span class="sxs-lookup"><span data-stu-id="17a0b-125"><a name="test"></a>Test push notifications in your app</span></span>
1. <span data-ttu-id="17a0b-126">Naciśnij klawisz hello **Uruchom** przycisk toobuild hello projekt i uruchomić aplikacji hello w stanie urządzenia z systemem iOS, a następnie kliknij **OK** tooaccept powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="17a0b-126">Press hello **Run** button toobuild hello project and start hello app in an iOS capable device, then click **OK** tooaccept push notifications.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="17a0b-127">Należy jawnie zaakceptować powiadomień wypychanych z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="17a0b-127">You must explicitly accept push notifications from your app.</span></span> <span data-ttu-id="17a0b-128">To żądanie występuje tylko hello hello aplikacja działa po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="17a0b-128">This request only occurs hello first time that hello app runs.</span></span>
   > 
   > 
2. <span data-ttu-id="17a0b-129">W aplikacji hello typu zadania, a następnie kliknij przycisk hello plus (**+**) ikona.</span><span class="sxs-lookup"><span data-stu-id="17a0b-129">In hello app, type a task, and then click hello plus (**+**) icon.</span></span>
3. <span data-ttu-id="17a0b-130">Sprawdź, czy powiadomienie o odebraniu, a następnie kliknij przycisk **OK** toodismiss hello powiadomień.</span><span class="sxs-lookup"><span data-stu-id="17a0b-130">Verify that a notification is received, then click **OK** toodismiss hello notification.</span></span>
4. <span data-ttu-id="17a0b-131">Powtórz krok 2 i natychmiast zamknij hello aplikacji, a następnie sprawdź, czy powiadomienie jest widoczne.</span><span class="sxs-lookup"><span data-stu-id="17a0b-131">Repeat step 2 and immediately close hello app, then verify that a notification is shown.</span></span>

<span data-ttu-id="17a0b-132">W tym samouczku została pomyślnie ukończona.</span><span class="sxs-lookup"><span data-stu-id="17a0b-132">You have successfully completed this tutorial.</span></span>

<!-- Images. -->

<!-- URLs. -->



