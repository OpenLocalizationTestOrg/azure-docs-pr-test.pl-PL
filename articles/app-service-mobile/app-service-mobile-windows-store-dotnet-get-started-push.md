---
title: "aaaAdd wypychania powiadomień tooyour Windows platformy Uniwersalnej aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Azure App Service Mobile Apps i usługi Azure Notification Hubs toosend wypychanie powiadomień tooyour Windows platformy Uniwersalnej aplikacji."
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
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="f5999-103">Dodawanie aplikacji dla systemu Windows tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="f5999-103">Add push notifications tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="f5999-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f5999-104">Overview</span></span>
<span data-ttu-id="f5999-105">W tym samouczku, możesz dodać toohello powiadomień wypychanych [szybki start systemu Windows](app-service-mobile-windows-store-dotnet-get-started.md) projektu, aby powiadomienie wypychane zostanie wysłane toohello urządzenia, za każdym razem, gdy wstawieniu rekordu.</span><span class="sxs-lookup"><span data-stu-id="f5999-105">In this tutorial, you add push notifications toohello [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="f5999-106">Jeśli nie używasz hello pobrany Projekt serwera szybki start, muszą hello pakiet rozszerzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="f5999-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="f5999-107">Zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f5999-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="f5999-108"><a name="configure-hub"></a>Konfigurowanie Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="f5999-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="f5999-109">Rejestrowanie aplikacji dla usługi powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="f5999-109">Register your app for push notifications</span></span>
<span data-ttu-id="f5999-110">Możesz toosubmit Twojego toohello aplikacji Sklepu Windows, a następnie skonfiguruj toointegrate projektu z serwera z wypychania toosend powiadomienia usługi WNS (Windows).</span><span class="sxs-lookup"><span data-stu-id="f5999-110">You need toosubmit your app toohello Windows Store, then configure your server project toointegrate with Windows Notification Services (WNS) toosend push.</span></span>

1. <span data-ttu-id="f5999-111">W programie Visual Studio Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt aplikacji platformy uniwersalnej systemu Windows hello, kliknij przycisk **magazynu** > **Skojarz aplikację ze sklepu hello...** .</span><span class="sxs-lookup"><span data-stu-id="f5999-111">In Visual Studio Solution Explorer, right-click hello UWP app project, click **Store** > **Associate App with hello Store...**.</span></span>

    ![Skojarz aplikację ze Sklepu Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="f5999-113">W Kreatorze powitania kliknij **dalej**, zaloguj się przy użyciu konta Microsoft, wpisz nazwę aplikacji w **Zarezerwuj nazwę nowej aplikacji**, następnie kliknij przycisk **rezerwy**.</span><span class="sxs-lookup"><span data-stu-id="f5999-113">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="f5999-114">Po rejestracji aplikacji hello jest hello został pomyślnie utworzony, wybierz nową nazwę aplikacji, kliknij przycisk **dalej**, a następnie kliknij przycisk **skojarzyć**.</span><span class="sxs-lookup"><span data-stu-id="f5999-114">After hello app registration is successfully created, select hello new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="f5999-115">Spowoduje to dodanie manifest aplikacji toohello informacji o rejestracji Sklepu Windows hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="f5999-115">This adds hello required Windows Store registration information toohello application manifest.</span></span>  
4. <span data-ttu-id="f5999-116">Przejdź toohello [Centrum deweloperów systemu Windows](https://dev.windows.com/en-us/overview), logowanie przy użyciu konta Microsoft, kliknij przycisk hello nowej rejestracji aplikacji w **Moje aplikacje**, następnie rozwiń węzeł **usług**  >  **Powiadomienia wypychane**.</span><span class="sxs-lookup"><span data-stu-id="f5999-116">Navigate toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click hello new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="f5999-117">W hello **powiadomienia wypychane** kliknij przycisk **witryna usług Live** w obszarze **Microsoft Azure Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="f5999-117">In hello **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="f5999-118">Hello strony rejestracji, zanotuj wartości hello na **klucze tajne aplikacji** i hello **identyfikatora SID pakietu**, który można następnie użyje tooconfigure zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="f5999-118">In hello registration page, make a note of hello value under **Application secrets** and hello **Package SID**, which you will next use tooconfigure your mobile app backend.</span></span>

    ![Skojarz aplikację ze Sklepu Windows](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="f5999-120">klucz tajny powitania klienta i identyfikatora SID pakietu są ważnymi poświadczeniami zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="f5999-120">hello client secret and package SID are important security credentials.</span></span> <span data-ttu-id="f5999-121">Nie udostępniaj nikomu tych wartości ani nie rozpowszechniaj ich razem z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="f5999-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="f5999-122">Witaj **identyfikator aplikacji** jest używany z hello tajny tooconfigure Account Microsoft uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="f5999-122">hello **Application Id** is used with hello secret tooconfigure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a><span data-ttu-id="f5999-123">Konfigurowanie powiadomień wypychanych toosend hello w wewnętrznej bazie danych</span><span class="sxs-lookup"><span data-stu-id="f5999-123">Configure hello backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="f5999-124"><a id="update-service"></a>Zaktualizuj powiadomień wypychanych toosend serwera hello</span><span class="sxs-lookup"><span data-stu-id="f5999-124"><a id="update-service"></a>Update hello server toosend push notifications</span></span>
<span data-ttu-id="f5999-125">Użyj poniższej procedury hello, odpowiadający danemu typowi projektu zaplecza&mdash;albo [zaplecza .NET](#dotnet) lub [zaplecza Node.js](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="f5999-125">Use hello procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="f5999-126"><a name="dotnet"></a>Projektu zaplecza .NET</span><span class="sxs-lookup"><span data-stu-id="f5999-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="f5999-127">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt serwera hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**, wyszukaj Microsoft.Azure.NotificationHubs, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="f5999-127">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="f5999-128">Spowoduje to zainstalowanie biblioteki klienta usługi Notification Hubs hello.</span><span class="sxs-lookup"><span data-stu-id="f5999-128">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="f5999-129">Rozwiń węzeł **kontrolerów**, otwórz TodoItemController.cs i dodać hello następujące instrukcje using:</span><span class="sxs-lookup"><span data-stu-id="f5999-129">Expand **Controllers**, open TodoItemController.cs, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="f5999-130">W hello **PostTodoItem** metody, Dodaj hello następującego kodu po wywołaniu hello zbyt**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="f5999-130">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="f5999-131">Ten kod informuje toosend Centrum powiadomień hello powiadomienie wypychane po Wstawianie nowego elementu.</span><span class="sxs-lookup"><span data-stu-id="f5999-131">This code tells hello notification hub toosend a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="f5999-132">Ponownie opublikować hello na serwerze project Server.</span><span class="sxs-lookup"><span data-stu-id="f5999-132">Republish hello server project.</span></span>

### <span data-ttu-id="f5999-133"><a name="nodejs"></a>Projektu zaplecza node.js</span><span class="sxs-lookup"><span data-stu-id="f5999-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="f5999-134">Jeśli jeszcze tego nie zrobiono, [pobieranie projektu Szybki Start hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) lub w przeciwnym razie użyj hello [edytora online w portalu Azure hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="f5999-134">If you haven't already done so, [download hello quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="f5999-135">Zastąp hello istniejący kod w pliku todoitem.js hello hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f5999-135">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
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
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="f5999-136">To wysyła wyskakujących powiadomień WNS zawierający item.text powitania po wstawieniu nowe zadanie do wykonania.</span><span class="sxs-lookup"><span data-stu-id="f5999-136">This sends a WNS toast notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="f5999-137">Podczas edytowania pliku hello na komputerze lokalnym, należy ponownie opublikować hello na serwerze project Server.</span><span class="sxs-lookup"><span data-stu-id="f5999-137">When editing hello file on your local computer, republish hello server project.</span></span>

## <span data-ttu-id="f5999-138"><a id="update-app"></a>Dodaj aplikację tooyour powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="f5999-138"><a id="update-app"></a>Add push notifications tooyour app</span></span>
<span data-ttu-id="f5999-139">Następnie zarejestrować dla powiadomień wypychanych przy uruchamianiu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5999-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="f5999-140">Podczas uwierzytelniania jest jeszcze włączone, upewnij się, że hello zalogowaniu się użytkownika przed podjęciem próby tooregister dla powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="f5999-140">When you have already enabled authentication, make sure that hello user signs-in before trying tooregister for push notifications.</span></span>

1. <span data-ttu-id="f5999-141">Otwórz hello **App.xaml.cs** pliku projektu i dodaj następujące hello `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="f5999-141">Open hello **App.xaml.cs** project file and add hello following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="f5999-142">W hello tego samego pliku, należy dodać następujące hello **InitNotificationsAsync** toohello definicję metody **aplikacji** klasy:</span><span class="sxs-lookup"><span data-stu-id="f5999-142">In hello same file, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="f5999-143">Ten kod pobiera hello ChannelURI dla aplikacji hello z usługi WNS, a następnie rejestruje ten ChannelURI w aplikacji mobilnej usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f5999-143">This code retrieves hello ChannelURI for hello app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="f5999-144">U góry hello hello **OnLaunched** obsługi zdarzeń w **App.xaml.cs**, Dodaj hello **async** definicję metody toohello modyfikator i dodaj następujące hello wywołanie Nowetoohello **InitNotificationsAsync** metody hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f5999-144">At hello top of hello **OnLaunched** event handler in **App.xaml.cs**, add hello **async** modifier toohello method definition and add hello following call toohello new **InitNotificationsAsync** method, as in hello following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="f5999-145">Gwarantuje to tego hello krótkim okresie ChannelURI jest zarejestrowana na każdym razem, gdy aplikacja hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="f5999-145">This guarantees that hello short-lived ChannelURI is registered each time hello application is launched.</span></span>
4. <span data-ttu-id="f5999-146">Ponownie skompiluj projekt aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="f5999-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="f5999-147">Aplikacja jest teraz gotowy tooreceive wyskakujące powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="f5999-147">Your app is now ready tooreceive toast notifications.</span></span>

## <span data-ttu-id="f5999-148"><a id="test"></a>Testowych powiadomień wypychanych w aplikacji</span><span class="sxs-lookup"><span data-stu-id="f5999-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="f5999-149"><a id="more"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f5999-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="f5999-150">Dowiedz się więcej na temat powiadomień wypychanych:</span><span class="sxs-lookup"><span data-stu-id="f5999-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="f5999-151">Jak toouse hello zarządzanego klienta usługi Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="f5999-151">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="f5999-152">Szablony umożliwiają wypchnięć wieloplatformowych toosend elastyczność i wypchnięć zlokalizowane.</span><span class="sxs-lookup"><span data-stu-id="f5999-152">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="f5999-153">Dowiedz się, jak szablony tooregister.</span><span class="sxs-lookup"><span data-stu-id="f5999-153">Learn how tooregister templates.</span></span>
* [<span data-ttu-id="f5999-154">Diagnozowanie problemów powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="f5999-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="f5999-155">Istnieją różne przyczyny, dlaczego powiadomienia mogą pobrać usunięte lub nie kończą na urządzeniach.</span><span class="sxs-lookup"><span data-stu-id="f5999-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="f5999-156">W tym temacie pokazano, jak tooanalyze i ustalenie potrzebnej głównego hello. Przyczyna niepowodzenia powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="f5999-156">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="f5999-157">Należy rozważyć kontynuować tooone hello następujące samouczki:</span><span class="sxs-lookup"><span data-stu-id="f5999-157">Consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="f5999-158">Dodaj aplikację tooyour uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="f5999-158">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="f5999-159">Dowiedz się, jak tooauthenticate użytkowników aplikacji przy użyciu dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="f5999-159">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="f5999-160">Włączanie synchronizacji w trybie offline dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="f5999-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="f5999-161">Dowiedz się, jak w trybie offline tooadd obsługują aplikację przy użyciu zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="f5999-161">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="f5999-162">Synchronizacja w trybie offline umożliwia użytkownikom końcowym toointeract z aplikacją mobilną&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.</span><span class="sxs-lookup"><span data-stu-id="f5999-162">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
