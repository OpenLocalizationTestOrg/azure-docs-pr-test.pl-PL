---
title: "Dodawanie powiadomień wypychanych do aplikacji systemu Windows platformy Uniwersalnej | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wysyłać powiadomienia wypychane do aplikacji systemu Windows platformy Uniwersalnej za pomocą usługi Azure App Service Mobile Apps i usługi Azure Notification Hubs."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: a14bb0320c1f6a563f766a6a0fad5cf556fe7b70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-windows-app"></a><span data-ttu-id="0573c-103">Dodawanie powiadomień wypychanych do aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="0573c-103">Add push notifications to your Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="0573c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0573c-104">Overview</span></span>
<span data-ttu-id="0573c-105">W tym samouczku, dodawanie powiadomień wypychanych do [szybki start systemu Windows](app-service-mobile-windows-store-dotnet-get-started.md) projektu, aby powiadomienia wypychane są wysyłane do urządzenia, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="0573c-105">In this tutorial, you add push notifications to the [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="0573c-106">Jeśli nie używasz Projekt serwera pobrany szybki start, konieczne będzie pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="0573c-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="0573c-107">Zobacz [pracować z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="0573c-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="0573c-108"><a name="configure-hub"></a>Konfigurowanie Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="0573c-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="0573c-109">Rejestrowanie aplikacji dla usługi powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="0573c-109">Register your app for push notifications</span></span>
<span data-ttu-id="0573c-110">Należy do przesyłania aplikacji do Sklepu Windows, a następnie skonfigurować Projekt serwera do integracji z usługi WNS (Windows Notification) do wysyłania wypychania.</span><span class="sxs-lookup"><span data-stu-id="0573c-110">You need to submit your app to the Windows Store, then configure your server project to integrate with Windows Notification Services (WNS) to send push.</span></span>

1. <span data-ttu-id="0573c-111">W Eksploratorze rozwiązań programu Visual Studio, kliknij prawym przyciskiem myszy projekt aplikacji platformy uniwersalnej systemu Windows, kliknij przycisk **magazynu** > **Skojarz aplikację ze sklepem...** .</span><span class="sxs-lookup"><span data-stu-id="0573c-111">In Visual Studio Solution Explorer, right-click the UWP app project, click **Store** > **Associate App with the Store...**.</span></span>

    ![Skojarz aplikację ze Sklepu Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="0573c-113">W kreatorze kliknij **dalej**, zaloguj się przy użyciu konta Microsoft, wpisz nazwę aplikacji w **Zarezerwuj nazwę nowej aplikacji**, następnie kliknij przycisk **rezerwy**.</span><span class="sxs-lookup"><span data-stu-id="0573c-113">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="0573c-114">Po pomyślnym utworzeniu rejestracji aplikacji, wybierz nową nazwę aplikacji, kliknij przycisk **dalej**, a następnie kliknij przycisk **skojarzyć**.</span><span class="sxs-lookup"><span data-stu-id="0573c-114">After the app registration is successfully created, select the new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="0573c-115">Spowoduje to dodanie wymaganych informacji dotyczących rejestracji w Sklepie Windows do manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0573c-115">This adds the required Windows Store registration information to the application manifest.</span></span>  
4. <span data-ttu-id="0573c-116">Przejdź do [Centrum deweloperów systemu Windows](https://dev.windows.com/en-us/overview), logowanie przy użyciu konta Microsoft, kliknij przycisk nowej rejestracji aplikacji w **Moje aplikacje**, następnie rozwiń węzeł **usług**  >   **Powiadomienia wypychane**.</span><span class="sxs-lookup"><span data-stu-id="0573c-116">Navigate to the [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click the new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="0573c-117">W **powiadomienia wypychane** kliknij przycisk **witryna usług Live** w obszarze **Microsoft Azure Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="0573c-117">In the **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="0573c-118">Na stronie rejestracji Zanotuj wartość w kluczu **klucze tajne aplikacji** i **identyfikatora SID pakietu**, który następnie będzie używane do konfigurowania zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="0573c-118">In the registration page, make a note of the value under **Application secrets** and the **Package SID**, which you will next use to configure your mobile app backend.</span></span>

    ![Skojarz aplikację ze Sklepu Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="0573c-120">Klucz tajny klienta i identyfikator SID pakietu są ważnymi poświadczeniami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="0573c-120">The client secret and package SID are important security credentials.</span></span> <span data-ttu-id="0573c-121">Nie udostępniaj nikomu tych wartości ani nie rozpowszechniaj ich razem z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="0573c-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="0573c-122">**Identyfikator aplikacji** jest używany z klucza tajnego do konfigurowania uwierzytelniania Account firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0573c-122">The **Application Id** is used with the secret to configure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-the-backend-to-send-push-notifications"></a><span data-ttu-id="0573c-123">Konfigurowanie zaplecza do wysyłania powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="0573c-123">Configure the backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="0573c-124"><a id="update-service"></a>Zaktualizuj serwer do wysyłania powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="0573c-124"><a id="update-service"></a>Update the server to send push notifications</span></span>
<span data-ttu-id="0573c-125">Poniższa procedura odpowiadający danemu typowi projektu zaplecza&mdash;albo [zaplecza .NET](#dotnet) lub [zaplecza Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="0573c-125">Use the procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="0573c-126"><a name="dotnet"></a>Projektu zaplecza .NET</span><span class="sxs-lookup"><span data-stu-id="0573c-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="0573c-127">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt serwera, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**, wyszukaj Microsoft.Azure.NotificationHubs, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="0573c-127">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="0573c-128">Spowoduje to zainstalowanie biblioteki klienta usługi Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="0573c-128">This installs the Notification Hubs client library.</span></span>
2. <span data-ttu-id="0573c-129">Rozwiń węzeł **kontrolerów**, otwórz TodoItemController.cs i dodaj następujące instrukcje using:</span><span class="sxs-lookup"><span data-stu-id="0573c-129">Expand **Controllers**, open TodoItemController.cs, and add the following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="0573c-130">W **PostTodoItem** metody, Dodaj następujący kod po wywołaniu **InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="0573c-130">In the **PostTodoItem** method, add the following code after the call to **InsertAsync**:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create the notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send the push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write the success result to the logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write the failure result to the logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="0573c-131">Ten kod informuje Centrum powiadomień do wysyłania powiadomień wypychanych po Wstawianie nowego elementu.</span><span class="sxs-lookup"><span data-stu-id="0573c-131">This code tells the notification hub to send a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="0573c-132">Ponownie opublikować projekt serwera.</span><span class="sxs-lookup"><span data-stu-id="0573c-132">Republish the server project.</span></span>

### <span data-ttu-id="0573c-133"><a name="nodejs"></a>Projektu zaplecza node.js</span><span class="sxs-lookup"><span data-stu-id="0573c-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="0573c-134">Jeśli jeszcze tego nie zrobiono, [pobieranie projektu Szybki Start](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) lub użyj innego [edytora online w portalu Azure](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="0573c-134">If you haven't already done so, [download the quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use the [online editor in the Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="0573c-135">Zastąp istniejący kod w pliku todoitem.js następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0573c-135">Replace the existing code in the todoitem.js file with the following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about the Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define the WNS payload that contains the new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute the insert.  The insert returns the results as a Promise,
        // Do the push as a post-execute action within the promise flow.
        return context.execute()
            .then(function (results) {
                // Only do the push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget to return the results from the context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="0573c-136">To wysyła wyskakujących powiadomień WNS zawierający item.text po wstawieniu nowe zadanie do wykonania.</span><span class="sxs-lookup"><span data-stu-id="0573c-136">This sends a WNS toast notification that contains the item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="0573c-137">Podczas edytowania pliku na komputerze lokalnym, należy ponownie opublikować projekt serwera.</span><span class="sxs-lookup"><span data-stu-id="0573c-137">When editing the file on your local computer, republish the server project.</span></span>

## <span data-ttu-id="0573c-138"><a id="update-app"></a>Dodawanie powiadomień wypychanych do aplikacji</span><span class="sxs-lookup"><span data-stu-id="0573c-138"><a id="update-app"></a>Add push notifications to your app</span></span>
<span data-ttu-id="0573c-139">Następnie zarejestrować dla powiadomień wypychanych przy uruchamianiu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0573c-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="0573c-140">Jeśli już zostało włączone uwierzytelnianie, upewnij się, że zalogowaniu się użytkownika przed podjęciem próby rejestracji powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="0573c-140">When you have already enabled authentication, make sure that the user signs-in before trying to register for push notifications.</span></span>

1. <span data-ttu-id="0573c-141">Otwórz **App.xaml.cs** pliku projektu i dodaj następującą `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="0573c-141">Open the **App.xaml.cs** project file and add the following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="0573c-142">W tym samym pliku Dodaj następujące **InitNotificationsAsync** definicję metody do **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="0573c-142">In the same file, add the following **InitNotificationsAsync** method definition to the **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register the channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="0573c-143">Ten kod pobiera ChannelURI dla aplikacji z usługi WNS, a następnie rejestruje ten ChannelURI w aplikacji mobilnej usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0573c-143">This code retrieves the ChannelURI for the app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="0573c-144">W górnej części **OnLaunched** obsługi zdarzeń w **App.xaml.cs**, Dodaj **async** modyfikator do definicji — metoda i dodaj następujące wywołanie do nowego  **InitNotificationsAsync** metody, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="0573c-144">At the top of the **OnLaunched** event handler in **App.xaml.cs**, add the **async** modifier to the method definition and add the following call to the new **InitNotificationsAsync** method, as in the following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="0573c-145">Gwarantuje to, czy krótkim okresie ChannelURI jest zarejestrowana w każdym razem, gdy aplikacja jest uruchamiana.</span><span class="sxs-lookup"><span data-stu-id="0573c-145">This guarantees that the short-lived ChannelURI is registered each time the application is launched.</span></span>
4. <span data-ttu-id="0573c-146">Ponownie skompiluj projekt aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0573c-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="0573c-147">Aplikacja jest teraz gotowa do odbierania wyskakujących powiadomień.</span><span class="sxs-lookup"><span data-stu-id="0573c-147">Your app is now ready to receive toast notifications.</span></span>

## <span data-ttu-id="0573c-148"><a id="test"></a>Testowych powiadomień wypychanych w aplikacji</span><span class="sxs-lookup"><span data-stu-id="0573c-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="0573c-149"><a id="more"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0573c-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="0573c-150">Dowiedz się więcej na temat powiadomień wypychanych:</span><span class="sxs-lookup"><span data-stu-id="0573c-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="0573c-151">Jak używać zarządzanego klienta usługi Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="0573c-151">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="0573c-152">Szablony zapewniają elastyczność i możliwość wysyłania wypchnięć i platform i wypchnięć zlokalizowanego.</span><span class="sxs-lookup"><span data-stu-id="0573c-152">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="0573c-153">Dowiedz się, jak zarejestrować szablonów.</span><span class="sxs-lookup"><span data-stu-id="0573c-153">Learn how to register templates.</span></span>
* [<span data-ttu-id="0573c-154">Diagnozowanie problemów powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="0573c-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="0573c-155">Istnieją różne przyczyny, dlaczego powiadomienia mogą pobrać usunięte lub nie kończą na urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="0573c-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="0573c-156">W tym temacie przedstawiono sposób analizowania i ustalić główną przyczynę niepowodzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="0573c-156">This topic shows you how to analyze and figure out the root cause of push notification failures.</span></span>

<span data-ttu-id="0573c-157">Należy rozważyć kontynuowanie na jedno z następujących samouczków:</span><span class="sxs-lookup"><span data-stu-id="0573c-157">Consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="0573c-158">Dodawanie uwierzytelniania do aplikacji</span><span class="sxs-lookup"><span data-stu-id="0573c-158">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="0573c-159">Dowiedz się, jak uwierzytelniać użytkowników aplikacji przy użyciu dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="0573c-159">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="0573c-160">Włączanie synchronizacji w trybie offline dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="0573c-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="0573c-161">Dowiedz się, jak dodać obsługę aplikacji w trybie offline przy użyciu zaplecza Aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="0573c-161">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="0573c-162">Synchronizacja w trybie offline umożliwia użytkownikom końcowym interakcję z aplikacją mobilną &mdash; przeglądanie, dodawanie lub modyfikowanie danych &mdash; nawet w przypadku braku połączenia sieciowego.</span><span class="sxs-lookup"><span data-stu-id="0573c-162">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
